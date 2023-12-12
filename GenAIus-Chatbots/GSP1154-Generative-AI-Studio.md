# GSP1154 - Get Started with Generative AI Studio

[GSP1154 - Get Started with Generative AI Studio](https://www.cloudskillsboost.google/games/4713/labs/30677)

[Vertex AI Generative AI Studio](https://cloud.google.com/generative-ai-studio) is a cloud-based platform that allows users to create and experiment with generative AI models. The platform provides a variety of tools and resources that make it easy to get started with generative AI, even if you don't have a background in machine learning.

In this lab, you use Generative AI Studio with Vertex AI to create prompts and conversations on Google Cloud console, without using the API or Python SDKs.

* Create prompts with free-form and structured mode.
* Create conversations.
* Explore the prompt gallery.

## Task 1. Create prompts

Vertex AI > Language > `TEXT PROMPT`

### Prompt design

* `Zero-shot prompting` - This is a method where the LLM is given no additional data on the specific task that it is being asked to perform. Instead, it is only given a prompt that describes the task. For example, if you want the LLM to answer a question, you just prompt "what is prompt design?".
* `One-shot prompting` - This is a method where the LLM is given a single example of the task that it is being asked to perform. For example, if you want the LLM to write a poem, you might give it a single example poem.
* `Few-shot prompting` - This is a method where the LLM is given a small number of examples of the task that it is being asked to perform. For example, if you want the LLM to write a news article, you might give it a few news articles to read.

modes

* `FREE-FORM` - This mode provides a free and easy approach to design your prompt. It is suitable for small and experimental prompts with no additional examples. You will be using this to explore zero-shot prompting.
* `STRUCTURED` - This mode provides an easy-to-use template approach to prompt design. Context and multiple examples can be added to the prompt in this mode. This is especially useful for one-shot and few-shot prompting methods which you will be exploring later.

### `FREE-FORM` mode

```text
What is a prompt gallery?
```

* adjust the `Max responses` parameter to `3` and click the SUBMIT button
* adjust the `Token limit` parameter to `1` and click the SUBMIT button
* adjust the `Token limit` parameter to `1024` and click the SUBMIT button
* adjust the `Temperature` parameter to `0.5` and click the SUBMIT button
* adjust the `Temperature` parameter to `1.0` and click the SUBMIT button

### `STRUCTURED` mode

* Test
* Examples: input / output

## Task 2. Create conversations

Vertex AI > Language > `TEXT CHAT`

Context

```text
Your name is Roy.
You are a support technician of an IT department.
You only respond with "Have you tried turning it off and on again?" to any queries.
```

Responses: `My computer is so slow`

## Task 3. Explore prompt gallery

Vertex AI > Language > `Prompt Gallery`
