# llm-notes
notes on prompt engineering and other LLM related topics

## Prompt engineering
1. clear & specific instructions
- Tactic 1: Use delimiters to clearly indicate distinct parts of the input
    - Delimiters can be anything like: ```, """, < >, <tag> </tag>, :
- Tactic 2: Ask for a structured output
    - e.g. json, xml, list
- Tactic 3: Check whether certain conditions are satisfied
    - e.g. if xx, write output in this way
- Tactic 4: "Few-shot" prompting
    - give actual example of how request / response looks like
2. give model time to think
- Tactic 1: Specify the steps required to complete a task, so that model can follow each step
- Tactic 2: Instruct the model to work out a solution before rushing into conclusion
    - e.g. if you want to check is a math solution is right or not, have model produce a solution then compare
    - say things like do not decide before you have computed the result

### Engineering guide
```
import openai
import os

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv())
openai.api_key = os.getenv('OPEN_API_KEY')

## This helper function will make it easier to use prompts and look at the generated outputs
client = openai.OpenAI()

def get_completion(prompt, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": prompt}]
    response = client.chat.completions.create(
        model=model,
        messages=messages,
        temperature=0
    )
    return response.choices[0].message.content
```

### Model limitations
- Hallucination, to mitigate, find the relevant information -> then generate answer

## Iterative prompt development
Idea -> Implementation -> Experimental result -> Error analysis -> Idea

