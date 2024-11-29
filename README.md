# Inference Cache

Cache your LLM calls in two lines of code. Always get the same response for the same prompt.

> We are working to open source the first version.
> [Join our Discord](https://tally.so/r/nr086R) to get early access and contribute

## Quick Start

### 1. Deploy the Inference Cache Server

```bash
docker run -p 8083:8083 Inference Cache/server
# This image is not published yet, join the Discord to get early access!
```

### 2. Update Your Client Code

With the OpenAI client:

```python
from openai import OpenAI, DefaultHttpxClient
import httpx

client = OpenAI(
    base_url="http://localhost:8083/v1",  # Or use OPENAI_BASE_URL env var
)
```

That's it! Now all identical prompts will return cached responses.

## Why Inference Cache?

- 💰 **Save Money**: Stop paying for repeated LLM calls with the same prompts
- 🔍 **Reliable Testing**: Get consistent responses in your test environment
- ⚡ **Lightning Fast**: Implement caching with minimal code changes
- 🐳 **Self-Hosted**: Full control with simple Docker deployment
- 🚀 **Framework Agnostic**: Works with any LLM provider

## How It Works

Inference Cache acts as a transparent proxy between your application and your LLM provider. When you make a request:

1. The cache checks if an identical prompt exists in its storage
2. If found, it returns the cached response immediately
3. If not found, it forwards the request to the actual LLM provider and caches the response

Inference Cache only adds a header to let you know if a response was cached or not.

### Storage

Inference Cache supports two storage backends: Postgres and Redis. It uses a hash to speed up the index lookup.

### Configuration

Inference Cache can be configured through environment variables:

```bash
CACHE_SIZE=5000          # Maximum number of cached responses
CACHE_STORAGE=postgres      # Storage backend (postgres/redis)
```

## Use Cases

### Development & Testing

- Cache responses during development to speed up iteration
- Ensure consistent behavior in your test suite
- Develop offline using previously cached responses

### Production

- Reduce costs by caching common queries
- Improve response times for frequently asked questions
- Create a fallback for when LLM services are unavailable or slow

## FAQ

**How is it different from built-in model caching, like [OpenAI's prompt caching](https://platform.openai.com/docs/guides/prompt-caching) or [Anthropic's cache](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching)?**

OpenAI's prompt caching and Anthropic's cache only cache your prompt (or part of it), not the response. They are a great way to save money on input tokens, but they will not give you consistent responses for the same prompt over time.

**Does it make sense to use Inference Cache together with the built-in model caching?**

Yes! In our experience, you end up using both. With Inference Cache You get consistent responses for the same prompt over time, so we save 100% of the time and money for exactly the same prompt. With the built-in model cache, you save some money and time on similar but new prompts.

## Coming Soon

- This opensource repo!
- Support for more LLM providers
- Advanced caching strategies
- Cache persistence options
- Response streaming
- Semantic caching

## Join the Community

We're building Inference Cache in public and would love your input! Join our [Discord community](https://tally.so/r/nr086R) to:

- Get early access
- Shape the roadmap
- Share your use cases
- Connect with other developers
