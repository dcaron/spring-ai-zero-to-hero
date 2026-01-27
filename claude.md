# Spring AI Zero to Hero Workshop

A comprehensive educational workshop for learning Spring AI, covering APIs, patterns, and agentic systems across multiple AI providers.

## Project Structure

```
spring-ai-zero-to-hero/
├── components/
│   ├── apis/           # Core Spring AI APIs
│   │   ├── chat/       # 8 progressive chat examples (chat_01-chat_08)
│   │   ├── embedding/  # 4 embedding examples
│   │   ├── image/      # Image generation
│   │   ├── audio/      # Audio/transcription (OpenAI)
│   │   └── vector-store/
│   ├── patterns/       # AI application patterns
│   │   ├── 01-stuff-the-prompt/
│   │   ├── 02-retrieval-augmented-generation/
│   │   ├── 03-chat-memory/
│   │   ├── chain-of-thought/
│   │   └── self-reflection-agent/
│   └── data/           # Example datasets
├── applications/       # Provider-specific apps (6 providers + gateway)
├── agentic-system/     # Agent development examples
├── mcp/                # Model Context Protocol examples (5 modules)
└── docker/             # PostgreSQL + pgvector, observability
```

## Current Versions

- **Spring AI**: 1.1.0 (GA)
- **Spring Boot**: 3.5.6
- **Java**: 21

## Features Covered

### Spring AI APIs
- ChatClient with fluent builder pattern
- Structured output (entity conversion, ListOutputConverter, MapOutputConverter)
- Tool/Function calling (annotation-based, return-direct, named selection)
- Multimodal (image input)
- Streaming responses
- Embeddings and Vector Stores (pgvector)

### Patterns
- RAG with document loaders
- Chat Memory (PromptChatMemoryAdvisor, MessageChatMemoryAdvisor)
- Stuff-the-prompt
- Chain-of-thought
- Self-reflection agents

### MCP Protocol
- STDIO and HTTP transports
- Client and server implementations
- Dynamic tool calling
- Resources, prompts, and completions

### Providers
- OpenAI, Azure OpenAI, AWS Bedrock, Google Vertex AI, Anthropic, Ollama

### Observability
- Prometheus metrics, Zipkin tracing, Loki logging

---

## Upgrade Recommendations (Future Work)

### Medium Effort

1. **Add Recursive Advisors Module**
   - New in Spring AI 1.1, key feature for agentic systems
   - Enables tool calling loops, output validation, retry logic
   - Would enhance the agentic-system examples significantly
   - Reference: https://docs.spring.io/spring-ai/reference/api/advisors-recursive.html

2. **Add ToolCallAdvisor Example**
   - Shows tool execution in advisor chain vs internal model
   - Enables other advisors to intercept and observe tool calling
   - Better for observability of tool execution

3. **Add Persistent ChatMemoryRepository Examples**
   - Current examples use InMemoryChatMemoryRepository
   - Add JDBC or Neo4j repository examples for production use
   - Spring AI provides: JdbcChatMemoryRepository, CassandraChatMemoryRepository, Neo4jChatMemoryRepository

### High Effort (Future Major Upgrade)

5. **Spring Boot 4.0 / Spring AI 2.0 Migration**
   - Spring AI 2.0 GA expected February 2026
   - Requires Spring Boot 4.0 (Spring Framework 7.0)
   - Breaking changes: default model changed to gpt-5-mini, temperature config removed
   - New features: Redis Semantic Cache Advisor, Reactive/NonReactive ChatClient split
   - New vector stores: Amazon S3, Bedrock Knowledge Base, Infinispan

### Low Priority Additions

6. **Prompt Caching Examples**
   - Available for Anthropic and AWS Bedrock
   - Can reduce costs by up to 90%

7. **Anthropic Citations API**
   - For retrieving source citations in model responses

8. **New Model Providers**
   - Google GenAI
   - ElevenLabs text-to-speech

---

## Running the Workshop

### Prerequisites
- Java 21+
- Docker (for PostgreSQL, pgvector, observability stack)
- Ollama (for local models)
- HTTPie (for API testing)

### Pre-downloaded Ollama Models
```bash
ollama pull llama3.2      # Chat
ollama pull mxbai-embed-large  # Embeddings
ollama pull llava         # Multimodal vision
```

### Quick Start
```bash
# Start infrastructure
docker compose -f docker/docker-compose.yml up -d

# Run a provider application
./mvnw spring-boot:run -pl applications/provider-ollama
```

---

## Resources

- [Spring AI Documentation](https://docs.spring.io/spring-ai/reference/)
- [Spring AI GitHub](https://github.com/spring-projects/spring-ai)
- [Spring AI Examples](https://github.com/spring-projects/spring-ai-examples)
