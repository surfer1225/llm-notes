# llm-notes
notes on prompt engineering and other LLM related topics

## Prompt engineering
1. clear & specific instructions
2. give model time to think

### Engineering guide
```
import openai
import os

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv())
openai.api_key = os.getenv('OPEN_API_KEY')
```

