# Simple LLM Cache

Cache your LLM calls in two lines of code. Always get the same response for the same prompt.

>We are working to open source the first version.
>[Join our Discord](https://tally.so/r/nr086R) to get early access and contribute

## Quick Start

### 1. Deploy the Cache Server

```bash
docker run -p 8083:8083 simplellmcache/server
```

### 2. Update Your Client Code

With the OpenAI client (other providers coming soon):

```python
from openai import OpenAI, DefaultHttpxClient
import httpx

client = OpenAI(
    base_url="http://mysinmplellmcache.com:8083/v1",  # Or use OPENAI_BASE_URL env var
)
```

That's it! Now all identical prompts will return cached responses


## Why Simple LLM Cache?

- 💰 **Save Money**: Stop paying for repeated LLM calls with the same prompts
- 🔍 **Reliable Testing**: Get consistent responses in your test environment
- ⚡ **Lightning Fast**: Implement caching with minimal code changes
- 🐳 **Self-Hosted**: Full control with simple Docker deployment
- 🚀 **Framework Agnostic**: Works with any LLM provider

## How It Works

Simple LLM Cache acts as a transparent proxy between your application and your LLM provider. When you make a request:

1. The cache checks if an identical prompt exists in its storage
2. If found, it returns the cached response immediately
3. If not found, it forwards the request to the actual LLM provider and caches the response

Simple LLM Cache only adds a header to let you know if a response was cached or not.

## Use Cases

### Development & Testing
- Cache responses during development to speed up iteration
- Ensure consistent behavior in your test suite
- Develop offline using previously cached responses

### Production
- Reduce costs by caching common queries
- Improve response times for frequently asked questions
- Create a fallback for when LLM services are unavailable or slow

## Configuration

Simple LLM Cache can be configured through environment variables:

```bash
CACHE_TTL=3600           # Time-to-live for cached responses (in seconds)
CACHE_SIZE=1000          # Maximum number of cached responses
CACHE_STORAGE=redis      # Storage backend (redis/memory)
```

## Coming Soon

- This opensource repo!
- Support for more LLM providers
- Advanced caching strategies
- Cache persistence options
- Response streaming
- Semantic caching

## Join the Community

We're building Simple LLM Cache in public and would love your input! Join our [Discord community](https://tally.so/r/nr086R) to:

- Get early access
- Shape the roadmap
- Share your use cases
- Connect with other developers
