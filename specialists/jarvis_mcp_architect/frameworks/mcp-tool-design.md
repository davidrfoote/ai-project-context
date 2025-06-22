# MCP Tool Design for Organizational Intelligence

## Core Design Principle
**Tools are simple interfaces to complex intelligence. The LLM decides when to use them, the system handles the complexity.**

## Tool Specifications

### add_memory
```python
@mcp.tool(description="Add a new memory. Called whenever there is information worth remembering - about people, projects, decisions, or organizational knowledge.")
async def add_memory(content: str) -> str:
    """
    The LLM calls this for any important information.
    System internally determines scope and routing.
    Returns confirmation of what was stored and where.
    """
```

### search_memories
```python
@mcp.tool(description="Search all organizational knowledge. Called for EVERY user query to provide context before responding. Searches across personal, project, and organizational memories.")
async def search_memories(query: str) -> str:
    """
    Always called before responding to users.
    Returns relevant memories from all accessible scopes.
    Results include source scope and confidence scores.
    """
```

### update_memory
```python
@mcp.tool(description="Update an existing memory when information changes or needs correction. Use when you have direct authority to update.")
async def update_memory(memory_id: str, new_content: str) -> str:
    """
    Direct update for memories user has authority over.
    System checks permissions and maintains history.
    Returns confirmation or permission error.
    """
```

### suggest_memory_update
```python
@mcp.tool(description="Suggest an update to a memory you cannot directly edit. Creates a proposal for review by those with authority.")
async def suggest_memory_update(
    memory_id: str, 
    suggested_content: str,
    reason: str
) -> str:
    """
    For memories outside user's direct authority.
    Creates suggestion with context for approval.
    Returns confirmation of suggestion submission.
    """
```

### delete_memory
```python
@mcp.tool(description="Remove outdated or incorrect memories. Use sparingly - prefer updates to maintain history.")
async def delete_memory(memory_id: str, reason: str) -> str:
    """
    Soft delete - maintains history.
    Requires authority or routes through approval.
    Returns confirmation or permission status.
    """
```

### list_memories
```python
@mcp.tool(description="List memories in a specific scope or matching criteria. Useful for understanding what the system knows.")
async def list_memories(
    scope: Optional[str] = None,
    limit: int = 10
) -> str:
    """
    Browse memories without specific search query.
    Scope can be 'personal', 'project', 'org', or None for all.
    Returns formatted list with IDs for potential updates.
    """
```

## Usage Patterns

### Always Search First
Every user interaction should begin with search:
```
User: "What's our deployment process?"
System: search_memories("deployment process")
System: [Responds with context from memories]
```

### Natural Information Capture
LLM recognizes important information without being asked:
```
User: "I found that our API performs better with connection pooling enabled"
System: add_memory("API performs better with connection pooling enabled")
System: "I'll remember that discovery about connection pooling."
```

### Transparent Permission Handling
System explains when routing through approvals:
```
User: "The company color should be blue"
System: suggest_memory_update(
    memory_id="brand_color",
    suggested_content="Primary brand color is blue",
    reason="User suggestion"
)
System: "I've submitted your suggestion to update the brand color. The brand team will review it."
```

## Context Variables (Hidden from Tools)

These are handled by the MCP server, not passed as parameters:
- `user_id`: Current user identity
- `project_id`: Active project context
- `organization_id`: Company identifier
- `role`: User's role in current context
- `timestamp`: When interaction occurred

## Return Value Patterns

### Success Returns
- Clear confirmation of action taken
- Where information was stored/found
- Any relevant metadata (approval needed, etc.)

### Error Returns
- Human-friendly explanation
- Suggested alternative action
- Never expose technical details

## Tool Behavior Guidelines

### Intelligence Over Configuration
❌ `add_memory(content, scope="project", category="decision")`
✅ `add_memory(content)` - system infers scope and category

### Broad Triggers Over Specific Patterns  
❌ "Called when user says 'I prefer' or 'We decided'"
✅ "Called whenever there is information worth remembering"

### Permission Awareness Without Blocking
❌ "Error: Insufficient permissions"
✅ "I've submitted your suggestion for review by the brand team"

### Context Without Complexity
❌ Exposing namespace routing to LLM
✅ System handles routing based on content analysis

## Implementation Notes

The MCP server implementation should:
1. Extract context from MCP context variables
2. Analyze content to determine appropriate scope
3. Check permissions based on user role
4. Route to appropriate storage/approval flow
5. Return human-friendly confirmations

The LLM using these tools should:
1. Always search before responding
2. Naturally recognize important information
3. Trust the system to handle routing
4. Explain permission flows to users
5. Never expose internal complexity
