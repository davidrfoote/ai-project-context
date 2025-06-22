# Mem0 Technical Reference for MCP Implementation

## Overview

Mem0 provides persistent memory for AI agents through a dual-architecture system combining vector databases and knowledge graphs. It enables AI systems to remember past interactions, learn from them, and build contextual understanding over time.

## Core Architecture Components

### 1. LLM Processing Layer
- Automatically extracts important information from conversations
- Manages memory updates and conflict resolution
- Decides when to add, update, or delete memories

### 2. Vector Storage
- Enables semantic search across all memories
- Finds contextually relevant information even with different phrasing
- Powers the "understanding" of user intent

### 3. Graph Storage (Optional)
- Tracks relationships between entities (people, concepts, projects)
- Enables complex queries about connections
- Builds a knowledge graph from conversations

### 4. Smart Retrieval System
- Combines semantic search with recency and importance
- Uses both vector similarity and graph relationships
- Returns the most relevant memories for current context

## Client Initialization

### Local/OSS Implementation
```python
from mem0 import Memory

# Simple initialization
m = Memory()

# Production configuration
m = Memory.from_config(config_dict={
    "graph_store": {
        "provider": "neo4j",
        "config": {
            "url": "neo4j://localhost:7687",
            "username": "neo4j",
            "password": "password"
        }
    },
    "llm": {
        "provider": "openai",
        "config": {
            "model": "gpt-4o-2024-08-06",
            "temperature": 0.2
        }
    },
    "version": "v1.1"
})
```

### Platform/Cloud Client
```python
from mem0 import MemoryClient

client = MemoryClient(
    api_key="your_api_key",
    org_id="your_org_id",      # Optional
    project_id="your_project_id" # Optional
)
```

## Core Memory Operations

### Add Memories
```python
# Basic add with messages
messages = [
    {"role": "user", "content": "I prefer Python for backend development"},
    {"role": "assistant", "content": "I'll remember your preference for Python"}
]

# Platform client with full parameters
result = client.add(
    messages=messages,
    user_id="user123",        # Required identity parameter
    agent_id="agent456",      # For multi-agent systems
    app_id="myapp",          # Application identifier
    metadata={
        "session": "abc123",
        "importance": "high"
    },
    infer=True,              # Use LLM to extract facts
    categories=["technical", "preferences"]
)
```

### Search Memories (v2)
```python
# Advanced search with complex filters
results = client.search(
    query="backend development preferences",
    filters={
        "AND": [
            {"user_id": {"in": ["user123", "user456"]}},
            {"created_at": {"gte": "2024-01-01"}},
            {"OR": [
                {"categories": {"icontains": "technical"}},
                {"keywords": {"in": ["python", "backend"]}}
            ]},
            {"NOT": {"metadata.archived": {"eq": True}}}
        ]
    },
    limit=10,
    rerank=True
)
```

### Update and Delete
```python
# Update single memory
updated = client.update(
    memory_id="mem_abc123",
    data="User strongly prefers Python with 5 years experience"
)

# Delete with filters
client.delete_all(
    user_id="user123",
    metadata={"session": "old_session"}
)
```

## MCP Implementation Patterns

### Conversation Context Management
```python
class ConversationMemory:
    def __init__(self, user_id):
        self.user_id = user_id
        self.client = MemoryClient(api_key=os.getenv("MEM0_API_KEY"))
        self.session_id = str(uuid.uuid4())
    
    def process_message(self, messages):
        """Process and store conversation turn"""
        result = self.client.add(
            messages=messages,
            user_id=self.user_id,
            metadata={
                "session_id": self.session_id,
                "timestamp": time.time()
            }
        )
        return result
    
    def get_context(self, query, limit=5):
        """Get relevant context for response generation"""
        return self.client.search(
            query=query,
            filters={
                "AND": [
                    {"user_id": self.user_id},
                    {"metadata.session_id": self.session_id}
                ]
            },
            limit=limit
        )
```

### Multi-User Session Handling
```python
class MultiUserMemoryManager:
    def __init__(self):
        self.client = MemoryClient(api_key=os.getenv("MEM0_API_KEY"))
    
    def handle_user_message(self, user_id: str, session_id: str, message: str):
        """Process message with user context"""
        # Get relevant context
        context = self.client.search(
            query=message,
            filters={
                "AND": [
                    {"user_id": user_id},
                    {"OR": [
                        {"metadata.session_id": session_id},
                        {"metadata.persistent": True}
                    ]}
                ]
            },
            limit=3
        )
        
        # Store new memory
        messages = [{"role": "user", "content": message}]
        self.client.add(
            messages=messages,
            user_id=user_id,
            metadata={"session_id": session_id}
        )
        
        return context
```

### Graph Memory Operations
```python
# Graph memory automatically extracts entities and relationships
m.add(
    "John is my colleague and he works on the Python backend with Sarah",
    user_id="user123",
    metadata={"context": "team_info"}
)

# Creates nodes and relationships:
# - John (Person) -> WORKS_ON -> Python backend
# - Sarah (Person) -> WORKS_ON -> Python backend
# - John -> COLLEAGUE_OF -> User
```

## Configuration Patterns

### Development Configuration
```python
DEV_CONFIG = {
    "llm": {
        "provider": "openai",
        "config": {
            "model": "gpt-4o-mini",  # Faster, cheaper
            "temperature": 0.1
        }
    },
    "vector_store": {
        "provider": "chroma",
        "config": {"path": "./dev_memories"}
    },
    "version": "v1.1"
}
```

### Production Configuration
```python
PROD_CONFIG = {
    "graph_store": {
        "provider": "neo4j",
        "config": {
            "url": os.getenv("NEO4J_URL"),
            "username": os.getenv("NEO4J_USER"),
            "password": os.getenv("NEO4J_PASS")
        }
    },
    "llm": {
        "provider": "openai",
        "config": {
            "model": "gpt-4o-2024-08-06",
            "temperature": 0.2
        }
    },
    "vector_store": {
        "provider": "qdrant",
        "config": {
            "url": os.getenv("QDRANT_URL"),
            "api_key": os.getenv("QDRANT_API_KEY")
        }
    },
    "version": "v1.1"
}
```

## Best Practices

### Memory Management
- Always use user_id for multi-user systems
- Add meaningful metadata for filtering
- Let Mem0 resolve conflicts automatically
- Use expires_at for temporary memories

### Performance
- Batch operations for bulk changes
- Implement caching for repeated queries
- Use async operations for concurrent processing
- Optimize search filters for speed

### Error Handling
```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=10)
)
async def safe_add(self, messages, user_id, **kwargs):
    try:
        return self.client.add(messages, user_id=user_id, **kwargs)
    except Exception as e:
        logger.error(f"Failed to add memory: {e}")
        raise
```

### Security & Privacy
- Use environment variables for API keys
- Implement access control before memory access
- Regular cleanup of old memories
- Use memory history for compliance

## Key API Patterns for MCP

1. **Always search before responding** to provide context
2. **Add memories naturally** when important information appears
3. **Use filters extensively** for scoped access
4. **Handle permissions gracefully** with suggestions
5. **Batch operations** for efficiency
6. **Implement retry logic** for reliability
7. **Cache search results** for performance

This reference provides the essential technical patterns for implementing Mem0-based memory systems in MCP contexts.
