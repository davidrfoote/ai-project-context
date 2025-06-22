# Jarvis Architecture Guide

## Executive Summary

Jarvis is a revolutionary architecture where natural language serves as the universal interface between intelligence and execution. Instead of complex routing logic or explicit mappings, the system trusts LLM inference to bridge human-level guidance with tool execution.

## Core Innovation

### The Paradigm Shift
**Traditional Systems**: Tight coupling between intelligence and execution
**Jarvis Architecture**: Complete decoupling via natural language interface

### Universal Agent Pattern
```
┌─────────────────────────────────────────────────────┐
│            Generic LangGraph Agent                   │
│                                                      │
│  Config: { entity_id, app_id }                      │
│  Capabilities: Workflow, MCP Tools, Memory          │
│  Intelligence: None (all from Jarvis)               │
└──────────────────────┬──────────────────────────────┘
                       │
                    API Calls
                       │
┌──────────────────────┴──────────────────────────────┐
│              Jarvis Intelligence Layer               │
│                                                      │
│  • Context Understanding                             │
│  • Memory Management                                 │
│  • Human-Level Guidance                              │
│  • Document References                               │
└─────────────────────────────────────────────────────┘
```

## Architectural Principles

### 1. Natural Language as Universal Interface
**Principle**: Human-readable guidance that LLMs naturally understand
**Implementation**: Jarvis provides guidance like "Check service history for duplicate charges"
**Result**: LLM maps to appropriate tools without explicit logic

### 2. Intelligence-Execution Decoupling
**Principle**: Complete separation of what to do (Jarvis) from how to do it (Agent)
**Implementation**: Jarvis knows procedures, Agent knows tools
**Result**: Evolve intelligence without changing execution

### 3. Zero Business Logic in Agents
**Principle**: Agents remain completely generic
**Implementation**: Configuration limited to entity_id and app_id
**Result**: One agent serves infinite use cases

### 4. Trust LLM Inference
**Principle**: LLMs excel at natural language → action mapping
**Implementation**: No routing tables, classification systems, or mapping logic
**Result**: Simpler systems that leverage AI strengths

## Technical Architecture

### LangGraph State Definition
```python
class AgentState(TypedDict):
    # Core conversation state
    messages: List[BaseMessage]
    
    # Identity context (only configuration needed)
    entity_id: str          # Who/what we're serving
    app_id: str            # Application context
    thread_id: Optional[str] # Conversation thread
    
    # Jarvis-provided intelligence
    context: Optional[Dict[str, Any]]
    
    # Execution state
    tool_results: Optional[List[Dict]]
    should_continue: bool
```

### Workflow Nodes

1. **Context Retrieval Node**
   ```python
   # Calls Jarvis for intelligence
   context = await jarvis.get_context(
       query=user_message,
       entity_id=state.entity_id,
       app_id=state.app_id
   )
   ```

2. **Processing Node**
   ```python
   # LLM reads context and decides actions
   # Natural language guidance → Tool calls
   # No explicit mapping logic
   ```

3. **Tool Execution Node**
   ```python
   # Execute MCP tools based on LLM decisions
   # Handle results and errors
   # Update state
   ```

4. **Memory Storage Node**
   ```python
   # Store conversation for future context
   await jarvis.add_conversation(
       messages=state.messages,
       entity_id=state.entity_id,
       app_id=state.app_id
   )
   ```

### Jarvis API Interface
```python
async def get_context(
    query: str,
    entity_id: str,
    app_id: str,
    thread_id: Optional[str] = None
) -> Dict[str, Any]:
    """
    Returns:
    - context_type: "known_solution" | "guided_procedure" | "discovery"
    - guidance: Human-readable steps
    - document_reference: Source documentation
    - entity_context: Historical patterns
    - execution_state: Progress tracking
    """

async def add_conversation(
    messages: List[Dict],
    entity_id: str,
    app_id: str,
    metadata: Optional[Dict] = None
) -> str:
    """Stores conversation in memory system"""
```

## Context Types & Behaviors

### Known Solution
```json
{
    "context_type": "known_solution",
    "guidance": "Based on previous interactions, update the routing number to resolve payment delays",
    "confidence": 0.95
}
```
**Agent Behavior**: Direct solution with high confidence

### Guided Procedure
```json
{
    "context_type": "guided_procedure",
    "guidance": "Check service history for duplicates. If found, cancel the erroneous charge. Send confirmation.",
    "document_reference": {
        "title": "Billing Resolution Process",
        "doc_id": "PROC-001"
    }
}
```
**Agent Behavior**: Follow steps using natural language inference

### Discovery Mode
```json
{
    "context_type": "discovery",
    "guidance": "Need more information. Ask about when this started and specific symptoms."
}
```
**Agent Behavior**: Gather information before proceeding

## Memory Architecture

### Four-Layer Context Building
1. **Agent Patterns**: Universal knowledge (how support works generally)
2. **Organizational Knowledge**: Company-specific procedures and policies
3. **Entity Context**: This specific user/provider's history
4. **Thread History**: Current conversation continuity

### Intelligent Scoping
- **Personal**: Individual preferences and patterns
- **Project**: Team decisions and technical choices
- **Organizational**: Company-wide knowledge and policies
- **Domain**: Cross-project expertise and best practices

### Natural Permeability
- Knowledge flows through people who work across boundaries
- No artificial barriers where humans would naturally share
- System tracks lineage and attribution

## MCP Tool Design Principles

### Broad Triggers
```python
@mcp.tool(description="Get complete service history including all charges and services")
async def get_service_history(provider_id: str) -> str:
    # Tool handles all history retrieval
    # No specific parameters for filtering
    # Intelligence determines what's relevant
```

### Simple Interfaces
```python
@mcp.tool(description="Store information worth remembering")
async def add_memory(content: str) -> str:
    # LLM decides what's important
    # Tool handles routing and scoping internally
    # No complex parameters
```

### Natural Language Descriptions
- Descriptions written for human understanding
- LLMs naturally map guidance to these descriptions
- No special syntax or classification needed

## Implementation Examples

### Support Agent Configuration
```python
config = {
    "entity_id": "provider_123",
    "app_id": "zennya_support"
}

# Jarvis provides support procedures
# Agent maps to support tools
# Same agent code as personal assistant
```

### Personal Assistant Configuration
```python
config = {
    "entity_id": "david",
    "app_id": "fomosphere"
}

# Jarvis provides personal context
# Agent maps to personal tools
# Same agent code as support agent
```

## Performance Optimization

### Parallel API Calls
```python
# Execute all context layers simultaneously
results = await asyncio.gather(
    get_agent_patterns(),
    get_org_knowledge(),
    get_entity_context(),
    get_thread_history()
)
# 200ms total vs 800ms sequential
```

### Why This Matters
- 200ms overhead for intelligent context
- Saves 5-10 minutes of back-and-forth
- Better user experience overall

## Common Anti-Patterns to Avoid

### ❌ Explicit Routing Logic
```python
# WRONG
if "billing" in query:
    return billing_tool()
elif "payment" in query:
    return payment_tool()
```

### ❌ Complex Classification
```python
# WRONG
intent = classify_intent(query)
tool = map_intent_to_tool(intent)
```

### ❌ Business Logic in Agents
```python
# WRONG
if entity_type == "provider":
    apply_provider_rules()
```

### ✅ Trust Natural Language
```python
# RIGHT
guidance = await jarvis.get_context(query)
# LLM figures out what to do
```

## Success Metrics

1. **Agent Universality**: Same agent handles 3+ different use cases
2. **Natural Mapping**: 90%+ successful guidance → tool mapping
3. **Performance**: <200ms context, <3s total response
4. **Simplicity**: Minimal code, maximum capability
5. **Evolution**: New capabilities without code changes

## The Meta-Innovation

This architecture proves a new paradigm:
- **Intelligence services** provide human-level guidance
- **Execution agents** map guidance to capabilities
- **Natural language** serves as the universal interface
- **No tight coupling** between knowing and doing

This pattern could transform AI system architecture across industries.
