# GSP1155 - Vertex AI PaLM API

[GSP1155 - Vertex AI PaLM API](https://www.cloudskillsboost.google/games/4713/labs/30674)

The Vertex AI PaLM API enables you to test, customize, and deploy instances of Google's PaLM large language models (LLM) so that you can leverage the capabilities of PaLM in your applications. The PaLM family of models supports text completion and multi-turn chat.

In this lab, you will explore how to leverage Vertex AI for the use cases mentioned above.

* Text completion use cases
* Multi-turn chat integration

## Try text prompts

[Try text prompts](https://cloud.google.com/vertex-ai/docs/generative-ai/start/quickstarts/quickstart-text):

* `prompt`: `Text`. Text input to generate model response
* `temperature`: `0.0-1.0, Default: 0`. The temperature is used for sampling during the response generation, which occurs when topP and topK are applied.
* `maxOutputTokens`: `1-1024, Default: 0`. Maximum number of tokens that can be generated in the response.
* `topK`: `1-40, Default: 40`. Top-k changes how the model selects tokens for output.
* `topP`: `0.0-1.0 Default: 0.95`. Top-p changes how the model selects tokens for output.

## Task 1. Sample text prompts

### Summarization prompt example

```sh
MODEL_ID="text-bison"
PROJECT_ID=$DEVSHELL_PROJECT_ID
curl \
-X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/publishers/google/models/${MODEL_ID}:predict -d \
$'{
  "instances": [
    { "prompt": "Provide a summary with about two sentences for the following article:
The efficient-market hypothesis (EMH) is a hypothesis in financial \
economics that states that asset prices reflect all available \
information. A direct implication is that it is impossible to \
\\"beat the market\\" consistently on a risk-adjusted basis since market \
prices should only react to new information. Because the EMH is \
formulated in terms of risk adjustment, it only makes testable \
predictions when coupled with a particular model of risk. As a \
result, research in financial economics since at least the 1990s has \
focused on market anomalies, that is, deviations from specific \
models of risk. The idea that financial market returns are difficult \
to predict goes back to Bachelier, Mandelbrot, and Samuelson, but \
is closely associated with Eugene Fama, in part due to his \
influential 1970 review of the theoretical and empirical research. \
The EMH provides the basic logic for modern risk-based theories of \
asset prices, and frameworks such as consumption-based asset pricing \
and intermediary asset pricing can be thought of as the combination \
of a model of risk with the EMH. Many decades of empirical research \
on return predictability has found mixed evidence. Research in the \
1950s and 1960s often found a lack of predictability (e.g. Ball and \
Brown 1968; Fama, Fisher, Jensen, and Roll 1969), yet the \
1980s-2000s saw an explosion of discovered return predictors (e.g. \
Rosenberg, Reid, and Lanstein 1985; Campbell and Shiller 1988; \
Jegadeesh and Titman 1993). Since the 2010s, studies have often \
found that return predictability has become more elusive, as \
predictability fails to work out-of-sample (Goyal and Welch 2008), \
or has been weakened by advances in trading technology and investor \
learning (Chordia, Subrahmanyam, and Tong 2014; McLean and Pontiff \
2016; Martineau 2021).
Summary:
"}
  ],
  "parameters": {
    "temperature": 0.2,
    "maxOutputTokens": 256,
    "topK": 40,
    "topP": 0.95
  }
}' > summarization_prompt_example.txt
```

## Ideation prompt example

```sh
MODEL_ID="text-bison"
PROJECT_ID=$DEVSHELL_PROJECT_ID
curl \
-X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/publishers/google/models/${MODEL_ID}:predict -d \
$'{
  "instances": [
    { "prompt": "Give me ten interview questions for the role of program manager."}
  ],
  "parameters": {
    "temperature": 0.2,
    "maxOutputTokens": 1024,
    "topK": 40,
    "topP": 0.8
  }
}' > ideation_prompt_example.txt
```

```sh
export PROJECT_ID=$(gcloud config get-value project)
gsutil cp *.txt gs://$PROJECT_ID
```

## Task 2. Sample chat prompts

Chat API

* `context`
* `examples`
* `messages`

```sh
MODEL_ID="chat-bison"
PROJECT_ID=$DEVSHELL_PROJECT_ID

curl \
-X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/publishers/google/models/${MODEL_ID}:predict -d \
'{
  "instances": [{
      "context":  "My name is Ned. You are my personal assistant. My favorite movies are Lord of the Rings and Hobbit.",
      "examples": [ { 
          "input": {"content": "Who do you work for?"},
          "output": {"content": "I work for Ned."}
      },
      { 
          "input": {"content": "What do I like?"},
          "output": {"content": "Ned likes watching movies."}
      }],
      "messages": [
      { 
          "author": "user",
          "content": "Are my favorite movies based on a book series?",
      }],
  }],
  "parameters": {
    "temperature": 0.3,
    "maxDecodeSteps": 200,
    "topP": 0.8,
    "topK": 40
  }
}'
```

```sh
MODEL_ID="chat-bison"
PROJECT_ID=$DEVSHELL_PROJECT_ID
curl \
-X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/publishers/google/models/${MODEL_ID}:predict -d \
'{
  "instances": [{
      "context":  "My name is Ned. You are my personal assistant. My favorite movies are Lord of the Rings and Hobbit.",
      "examples": [ { 
          "input": {"content": "Who do you work for?"},
          "output": {"content": "I work for Ned."}
      },
      { 
          "input": {"content": "What do I like?"},
          "output": {"content": "Ned likes watching movies."}
      }],
      "messages": [
      { 
          "author": "user",
          "content": "Are my favorite movies based on a book series?",
      }],
  }],
  "parameters": {
    "temperature": 0.3,
    "maxDecodeSteps": 200,
    "topP": 0.8,
    "topK": 40
  }
}' > sample_chat_prompts.txt
```

```sh
export PROJECT_ID=$(gcloud config get-value project)
gsutil cp sample_chat_prompts.txt gs://$PROJECT_ID
```

## Next Steps

* Learn more about prompting for design for [text](https://cloud.google.com/vertex-ai/docs/generative-ai/text/text-prompts) and [chat](https://cloud.google.com/vertex-ai/docs/generative-ai/chat/chat-prompts).
* Learn more about [text embedding](https://cloud.google.com/vertex-ai/docs/generative-ai/embeddings/get-text-embeddings).
