---
title: ChatGPT sees the herbarium
layout: post
summary: Guest coder Robert Turnbull joins us to describe his work on HESPI
---

This week we paused our reading of *The Little Learner* to entertain a guest: Dr Robert Turnbull, a Senior Research Data Specialist at the [Melbourne Data Analytics Platform](https://www.unimelb.edu.au/mdap). He talked us through the [HESPI](https://rbturnbull.github.io/hespi/) project, which discovers structured data in handwritten herbarium specimen sheets. We then read through [llm.py](https://github.com/rbturnbull/hespi/blob/main/hespi/llm.py), the part of the software which interfaces with an online LLM to perform data cleaning at the end of the pipeline.

We resume *The Little Learner* on page 67 in our next session.

## AI for GLAM

In *The Little Learner*, we are reading the code for building an LLM from the ground up. We have been learning about basic data structures and algorithms, such as tensors, linear functions and loss functions, which we will eventually assemble like Lego bricks into an Artificial Neural Network. This week we examined an LLM from the top down. Once you have an LLM available, what use is it to critical and historical scholars like ourselves?

HESPI solves a problem that is common for Galleries, Libraries, Archives and Museums (GLAM). GLAM institutions often possess an enormous amount of data, but in a hard-to-use form. In this case, the data is in the form of botanical specimen sheets. A specimen sheet includes a dried specimen of a plant, and some handwritten information about the specimen, such as the scientific name and the location where it was collected. It is easy to photograph a specimen sheet, or to allow a person to look at it in a cabinet, but what if you wanted to estimate the historic range of a plant? What if you wanted to compare the collections of multiple museums? What if you wanted to validate a climate model against the location data available in the sheets? Such analysis is extremely difficult if the sheets are only available as photographs or physical objects.

HESPI discovers structured data in the specimen sheets. It segments each part of the photograph, distinguishing the specimen, the data card and the color swatch. It interprets the text on the sheet, and organises it for entry into a database. As part of this process, an LLM plays a crucial role. The specimen sheet first passes through a number of specialised subsystems that discover certain parts of the data. At the final stage, the data is passed as a prompt to the LLM, which attempts to remove any errors that have crept in from earlier stages in the pipeline. It cleans typos, OCR glitches and so on, and according to Rob and the HESPI team, improves the overall accuracy of the system by about 10 percentage points.

We are still on the crest of an AI hype wave, and the CEOs of self-proclaimed "AI Companies" continue to tout their products as revolutionary devices that make computers more creative and conversational. HESPI presents a more realistic model of what LLMs can do: boring, routine writing tasks that require more-or-less mechanical manipulation of text. When used in this way, LLMs are genuinely useful, and can enable cultural institutions to achieve projects that were hitherto out of reach.

## Describing chats in code

In our close reading, we focussed on [llm.py](https://github.com/rbturnbull/hespi/blob/main/hespi/llm.py), the part of HESPI that hooks in to an online LLM for the final data-cleaning step. The main purpose of the file is to construct a prompt that describes the data-cleaning task for an individual specimen sheet, and then send this prompt to either Claude or ChatGPT for data cleaning.

First we need the building-blocks for a prompt. These are imported at the top of the file:

```python
from langchain_core.messages import HumanMessage, AIMessage, SystemMessage
from langchain.prompts import ChatPromptTemplate
```

[`langchain`](https://python.langchain.com/docs/introduction/) is a Python module that provides [Python classes](https://www.w3schools.com/python/python_classes.asp) for interacting with online chatbots. Each class represents an important part of a prompt. In this case, the `HumanMessage` will be the question that HESPI asks the system: this is analogous to the prompt that you might type into the online chat interface of ChatGPT. The `AIMessage` is the answer given by the system itself: this is analogous to the answers you see when you 'chat' with ChatGPT online. We will see shortly that HESPI actually tells the AI how to begin its response, in order to discipline its output. The `SystemMessage` is a hidden message which the chatbot considers before interpreting the `HumanMessage` or generating its own `AIMessage`. Typically, chatbots are designed to give extra weight to `SystemMessage`s, so that developers of AI systems have power to control the output of the model, without necessarily knowing what users wil type. You are generally unable to provide such system messages in the public interface for ChatGPT and similar services. The `ChatPromptTemplate` is the glue that holds the different kinds of message together. Essentially, `llm.py` receives the output from the prior stages of HESPI, generates a `HumanMessage`, `AIMessage` and `SystemMessage` for the current specimen sheet, and then combines them into a single `ChatPromptTemplate` that is sent to the relevant chatbot.

Which chatbot, I hear you ask?

```python
from langchain.chat_models.base import BaseChatModel
from langchain_openai import ChatOpenAI
from langchain_anthropic import ChatAnthropic
```

The `BaseChatModel` is an "abstract class," or a general template for any LLM that you wish to use with `langchain`. At present, HESPI supports two concrete models: `ChatOpenAI` (i.e. ChatGPT) and `ChatAnthropic` (i.e. Claude, Sonnet). As we discussed in the group, this is the first time we have seen brand names in a source file. This is not unusual: it is common enough for source files to contain information about the company that owns them. It is also common for code that interacts with third-party software to include other companies' brands in it: there are thousands of packages out there with `google`, `SQLite`, `MySQL`, `excel` or `aws` scattered among the function names and class definitions. The presence of brand names in HESPI does raise the question, however: as more tasks are offloaded to cloud-based language models such as Claude and GPT-4, how much more frequent will corporate vocabulary become in source code? How will this affect programmers' relationship to the code they write? Perhaps not at all.

This is the key function of `llm.py`, which provides the main "entry point" for the script:

```python
def build_template(institutional_label_image:Path, detection_results:dict) -> ChatPromptTemplate:
```

The function takes two inputs:

- `institutional_label_image`: The image file of the "institutional label" on the specimen sheet, which is the textual part of the document with the species name, etc.
- `detection_results`: A [Python `dict`](https://www.w3schools.com/python/python_dictionaries.asp) containing the output from the prior steps in the HESPI pipeline. This is the data that the LLM will try to clean up, by inspecting the image of the institutional label for itself, and scanning through the language of the detection results.

The output of the function is a `ChatPromptTemplate`, a composite object containing the various kinds of messages described above. This template can be sent to one of OpenAI or Anthropic's systems, and the corrections will be returned in a (hopefully) well-structured and useable form.

## `prompt-english` as a programming language

At the heart of the `build_template` function is a [Python f-string](https://www.w3schools.com/python/python_string_formatting.asp) that collects information from HESPI and massages it into a textual prompt for the LLM. This then forms the `HumanMessage` for the system.

```python
main_prompt = f"""
        We have a pipeline for automatically reading the institutional labels and extracting the following fields:\n{', '.join(label_fields)}.
        
        You need to inspect an image and see if the fields have been extracted correctly. 
        If there are errors, then print out the field name with a colon and then the correct value. Each correction is on a new line.
        If the values provided are correct, then don't output anything for that field.
        When you are finished, print out 5 hyphens '-----' to indicate the end of the text.

        For example, if the 'genus' field and the 'species' field were extracted incorrectly, then you would print:
        genus: Abies
        species: alba
        -----

        Here are the following fields that we have extracted from the institutional label:
        {values_string}

        {ocr_results}

        Here is the image of the institutional label:
    """
```

The three parts in curly braces (`{}`) contain data that is spliced into the prompt. These are specific to the specimen sheet whose data is to be corrected. The rest of the prompt is fixed, and is fed to the LLM every time.

The companies that own LLMs often present them as "natural," "intuitive" and "conversational." But it is apparent from this example that they are nothing of the sort. In order to get an LLM to provide sensible answers to a question, you need to craft the prompt to carefully and repeatedly instruct it what to do. In this case, the relatively simple instructions are given in extremely clear detail. First the task is described in words, e.g. `"If there are errors, then print out the field name with a colon and then the correct value. Each correction is on a new line."`. Then exactly this instruction is shown in an explicit example:`"genus: Abies"`. Clearly some effort went into the engineering of this prompt, to ensure that the LLM gave sensible answers. In addition, a `SystemMessage` is provided to determine the LLM's output:

```python
system_message = SystemMessage("You are an expert curator of a herbarium with vast knowledge of plant species.")
```

And the human programmer also begins the AI's response for it:

```python
ai_message = AIMessage("Certainly, here are the corrections:")
```

Not only this, but these prompts are provided to the LLM *every single time*. If 1,000 specimen sheets are corrected, then the LLM is instructed 1,000 times that it is an "expert curator." It is instructed 1,000 times to put each correction on a new line, with a colon in between the field and the corrected value. It is instructed 1,000 times to begin its answer with the phrase "Certainly, here are the corrections:". If it corrects 10,000 specimen sheets, it receives these instructions 10,000 times. If it corrects 100,000 specimen sheets, it receives these instructions 100,000 times.

This activity of interacting with a chatbot is nothing like conversing with a research assistant. What it is like is programming a computer. The "English" used in the prompt is not spoken or written, but *engineered*. It is written in a clear, technical way to elicit a predictable response from a mechanical system. What LLMs have started to enable is the old dream of "natural language programming," where programmers can become (partly) free of the strictures of formal language. What LLMs have not even come close to doing is replacing *programming* as a human activity: it is still necessary for the human to design the program, to determine the requirements, to structure the system—even if they write some English as they do so.

## Are abstractions high or low?

As an aside, we considered how abstraction is represented in source code. The `BaseChatModel` is the most *abstract* kind of chat model in `langchain`. All chatmodels are instances of `BaseChatModel`. Here abstraction is metaphorically <span style="font-variant-caps: small-caps">low</span>. The more abstract something is, the more *basic* is it. There is a different metaphor for abstraction in `ChatPromptTemplate`. A `Template` is more abstract than a simple `Prompt`, because all `Prompts` fit into the template. In this case, abstraction is metaphorically <span style="font-variant-caps: small-caps">empty</span>. The more abstract something is, the less *filled* it is with *content*.

These are not the only metaphors for abstraction. As we discussed in the group, abstraction can sometimes also be <span style="font-variant-caps: small-caps">cloudy</span> or <span style="font-variant-caps: small-caps">high</span>. The metaphors of <span style="font-variant-caps: small-caps">emptiness</span> and <span style="font-variant-caps: small-caps">lowness</span> don't really work well together, because the lower something is, the more basic it is, then the closer it is to the solid, filled-in, all-too-real <span style="font-variant-caps: small-caps">ground</span>.

Abstraction is a fundamental concept of computer science, and of the art of programming. Even in relatively straightforward, practical code like `llm.py`, programmers are obliged to grapple with *what abstraction is*, and express ideas about its nature, even if they don't mean to.