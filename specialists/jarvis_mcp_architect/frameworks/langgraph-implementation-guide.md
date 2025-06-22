# LangGraph Implementation Guide

## Overview

This guide provides practical implementation patterns for building a Generic LangGraph Jarvis Agent. While the architectural vision emphasizes pure natural language interfaces, this implementation guide includes pragmatic patterns that improve reliability and debugging in production systems.

## Core Implementation

### Agent Configuration
```python
# Minimal configuration - the agent only needs to know:
agent_config = {
    "entity_id": "provider_123",  # Who/what we're serving
    "app_id": "zennya_support"    # Which application context
}
```

### LangGraph State Definition
```python
from typing import TypedDict, List, Dict, Optional, Any
from langchain_core.messages import BaseMessage

class AgentState(TypedDict):
    # Core conversation state
    messages: List[BaseMessage]
    
    # Identity context (only configuration needed)
    entity_id: str              # Required: who/what we're talking to
    app_id: str                # Required: application context
    thread_id: Optional[str]    # Optional: conversation thread
    
    # Jarvis-provided intelligence
    context: Optional[Dict[str, Any]]  # Current context from Jarvis
    
    # Execution state
    tool_results: Optional[List[Dict]]  # Results from tool calls
    should_continue: bool               # Workflow control
```

## Workflow Implementation

### 1. Context Retrieval Node
```python
async def get_context_node(state: AgentState) -> AgentState:
    """Retrieve context from Jarvis based on the current query."""
    
    # Get the last user message
    last_message = state["messages"][-1].content
    
    # Call Jarvis API
    context = await jarvis.get_context(
        query=last_message,
        entity_id=state["entity_id"],
        app_id=state["app_id"],
        thread_id=state.get("thread_id")
    )
    
    # Update state with context
    state["context"] = context
    return state
```

### 2. Processing Node
```python
async def process_node(state: AgentState) -> AgentState:
    """Process context and decide next action."""
    
    context = state["context"]
    
    # Route based on context type
    if context["type"] == "standard":
        # Simple conversational response
        response = await generate_response(context)
        state["messages"].append(AIMessage(content=response))
        state["should_continue"] = False
        
    elif context["type"] == "guided_resolution":
        # Need to use tools
        state["should_continue"] = True
        
    elif context["type"] == "procedure":
        # Execute procedure steps
        state["should_continue"] = True
    
    return state
```

### 3. Tool Execution Node
```python
async def tool_execution_node(state: AgentState) -> AgentState:
    """Execute tools based on context guidance."""
    
    context = state["context"]
    
    # Get suggested tools from context
    suggested_tools = context.get("suggested_tools", [])
    
    # Execute tools based on guidance
    # Note: In pure vision, LLM would infer this from natural language
    # In practice, explicit suggestions improve reliability
    
    tool_results = []
    for tool_name in suggested_tools:
        if tool_name in available_tools:
            result = await available_tools[tool_name].invoke(state)
            tool_results.append({
                "tool": tool_name,
                "result": result
            })
    
    state["tool_results"] = tool_results
    return state
```

### 4. Memory Storage Node
```python
async def store_memory_node(state: AgentState) -> AgentState:
    """Store conversation in Jarvis memory system."""
    
    # Prepare conversation data
    conversation_data = {
        "messages": [msg.dict() for msg in state["messages"]],
        "entity_id": state["entity_id"],
        "app_id": state["app_id"],
        "metadata": {
            "tool_results": state.get("tool_results", []),
            "context_type": state["context"].get("type"),
            "timestamp": datetime.utcnow().isoformat()
        }
    }
    
    # Store in Jarvis
    confirmation_id = await jarvis.add_conversation(**conversation_data)
    
    return state
```

## Context Types & Behaviors

### Standard Context
```json
{
    "type": "standard",
    "summary": "Regular conversation",
    "key_points": ["User greeting", "No issues detected"],
    "suggested_response": "Friendly greeting"
}
```
**Implementation**: Generate conversational response, no tools needed

### Guided Resolution
```json
{
    "type": "guided_resolution",
    "issue": "Payment delay",
    "guidance": "Check payment status, verify details, escalate if needed",
    "suggested_tools": ["check_payment_status", "get_bank_details"],
    "entity_context": {"payment_history": "usually on time"}
}
```
**Implementation**: Follow guidance using suggested tools

### Procedure Execution
```json
{
    "type": "procedure",
    "procedure_id": "PROC-PAY-001",
    "steps": ["Step 1: Check status", "Step 2: Verify bank"],
    "current_step": 1,
    "required_tools": ["payment_api", "bank_verification"]
}
```
**Implementation**: Execute procedure steps sequentially

## Complete Workflow Graph

```python
from langgraph.graph import StateGraph, END

def create_jarvis_agent():
    # Initialize graph
    workflow = StateGraph(AgentState)
    
    # Add nodes
    workflow.add_node("get_context", get_context_node)
    workflow.add_node("process", process_node)
    workflow.add_node("execute_tools", tool_execution_node)
    workflow.add_node("store_memory", store_memory_node)
    
    # Set entry point
    workflow.set_entry_point("get_context")
    
    # Add edges
    workflow.add_edge("get_context", "process")
    
    # Conditional routing from process node
    workflow.add_conditional_edges(
        "process",
        lambda x: "execute_tools" if x["should_continue"] else "store_memory",
        {
            "execute_tools": "execute_tools",
            "store_memory": "store_memory"
        }
    )
    
    # Tool execution loops back to process
    workflow.add_edge("execute_tools", "process")
    
    # Memory storage ends the workflow
    workflow.add_edge("store_memory", END)
    
    return workflow.compile()
```

## Jarvis API Client

```python
class JarvisAPI:
    def __init__(self, api_key: str, base_url: str):
        self.api_key = api_key
        self.base_url = base_url
        self.session = aiohttp.ClientSession()
    
    async def get_context(
        self,
        query: str,
        entity_id: str,
        app_id: str,
        thread_id: Optional[str] = None
    ) -> Dict[str, Any]:
        """Get context from Jarvis intelligence layer."""
        
        payload = {
            "query": query,
            "entity_id": entity_id,
            "app_id": app_id,
            "thread_id": thread_id
        }
        
        async with self.session.post(
            f"{self.base_url}/context",
            json=payload,
            headers={"Authorization": f"Bearer {self.api_key}"}
        ) as response:
            return await response.json()
    
    async def add_conversation(
        self,
        messages: List[Dict[str, str]],
        entity_id: str,
        app_id: str,
        metadata: Optional[Dict] = None
    ) -> str:
        """Store conversation in Jarvis memory system."""
        
        payload = {
            "messages": messages,
            "entity_id": entity_id,
            "app_id": app_id,
            "metadata": metadata or {}
        }
        
        async with self.session.post(
            f"{self.base_url}/conversations",
            json=payload,
            headers={"Authorization": f"Bearer {self.api_key}"}
        ) as response:
            result = await response.json()
            return result["confirmation_id"]
```

## Quick Start Example

```python
# Initialize the agent
agent = create_jarvis_agent()
jarvis = JarvisAPI(api_key="...", base_url="...")

# Run the agent
async def run_agent(message: str, entity_id: str, app_id: str):
    # Initial state
    initial_state = {
        "messages": [HumanMessage(content=message)],
        "entity_id": entity_id,
        "app_id": app_id,
        "should_continue": True
    }
    
    # Execute workflow
    result = await agent.ainvoke(initial_state)
    
    # Return the last AI message
    return result["messages"][-1].content

# Example usage
response = await run_agent(
    message="My payment is late",
    entity_id="provider_123",
    app_id="zennya_support"
)
```

## Implementation Notes

### Pragmatic Deviations from Pure Vision

1. **Tool Suggestions**: While the pure vision relies entirely on LLM inference, the implementation includes explicit tool suggestions for reliability
2. **Context Types**: Provides structured context types to simplify routing logic
3. **Error Handling**: Includes explicit error states not shown in the vision
4. **Debugging**: Structured responses make debugging easier

### Performance Optimizations

```python
# Parallel context retrieval (if using multiple context sources)
async def parallel_context_retrieval(state: AgentState):
    context_tasks = [
        jarvis.get_agent_patterns(state["app_id"]),
        jarvis.get_entity_context(state["entity_id"]),
        jarvis.get_thread_history(state.get("thread_id"))
    ]
    
    results = await asyncio.gather(*context_tasks)
    return merge_contexts(results)
```

### Error Handling

```python
async def safe_tool_execution(tool_name: str, state: AgentState):
    try:
        return await available_tools[tool_name].invoke(state)
    except ToolExecutionError as e:
        # Log error, continue with degraded functionality
        logger.error(f"Tool {tool_name} failed: {e}")
        return {"error": str(e), "tool": tool_name}
```

## Development Workflow

### 1. Start with Mock Jarvis
```python
class MockJarvis:
    async def get_context(self, **kwargs):
        # Return mock contexts for testing
        return {
            "type": "guided_resolution",
            "guidance": "Check payment status",
            "suggested_tools": ["check_payment_status"]
        }
```

### 2. Implement Core Nodes
- Start with simple context → response flow
- Add tool execution incrementally
- Test each node in isolation

### 3. Integration Testing
```python
@pytest.mark.asyncio
async def test_payment_flow():
    agent = create_jarvis_agent()
    result = await agent.ainvoke({
        "messages": [HumanMessage(content="Payment late")],
        "entity_id": "test_123",
        "app_id": "support"
    })
    
    assert result["tool_results"]
    assert "payment_status" in str(result["tool_results"])
```

## Deployment Considerations

### Configuration Management
```python
class AgentConfig:
    def __init__(self):
        self.jarvis_url = os.getenv("JARVIS_API_URL")
        self.jarvis_key = os.getenv("JARVIS_API_KEY")
        self.llm_model = os.getenv("LLM_MODEL", "gpt-4")
        self.temperature = float(os.getenv("LLM_TEMPERATURE", "0.7"))
```

### Monitoring
```python
# Add observability
from langchain.callbacks import LangChainTracer

tracer = LangChainTracer(project_name="jarvis-agent")
agent = create_jarvis_agent().with_config(callbacks=[tracer])
```

### Scaling
- Stateless agent design enables horizontal scaling
- Use connection pooling for Jarvis API calls
- Implement caching for frequently accessed context

## Conclusion

This implementation guide provides practical patterns for building a Generic LangGraph Jarvis Agent. While it includes some pragmatic deviations from the pure architectural vision (like explicit tool suggestions), these patterns improve reliability and debugging in production systems.

The key principle remains: the agent stays generic and simple, with all intelligence coming from Jarvis. The implementation details here are meant to make that vision practical and deployable.
