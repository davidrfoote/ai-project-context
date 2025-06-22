# Organizational Intelligence Philosophy

## Core Principle
**The LLM decides what's important. We store and retrieve it intelligently.**

## Fundamental Architecture
LLM Layer (Pattern Recognition) → MCP Interface → Memory System (Storage & Retrieval)

## Memory Scoping Model

### Personal Memories
- Private to individual: preferences, personal context, individual patterns
- Examples: "I prefer mornings", "I'm learning Rust", "My child has soccer Thursdays"
- Access: User + their AI only

### Project Memories  
- Scoped to project members: decisions, technical choices, project context
- Examples: "Using React", "API timeout is 60s", "Launch March 15"
- Access: Project members only

### Organizational Memories
- Company-wide knowledge: policies, standards, public information
- Examples: "John is Senior Engineer", "Brand color #0066CC", "All-hands Fridays"
- Access: All employees

### Domain Knowledge
- Cross-project expertise: patterns, best practices, reusable knowledge
- Examples: "OAuth2 for auth", "Exponential backoff pattern", "Python style guide"
- Access: Domain participants

## Knowledge Flow Principles

### Natural Permeability
- Knowledge flows through people who work across boundaries
- No artificial barriers where humans would naturally share
- System tracks lineage and attribution

### Progressive Authority
1. Observe: System watches, suggests actions
2. Pattern: System recognizes patterns, predicts needs  
3. Trusted: System acts with earned authority, explains reasoning

### Community Governance
- Anyone can suggest memory updates
- Community validates through voting/discussion
- Authors/contributors approve with full context
- All changes tracked with attribution

## Tool Design Philosophy

### MCP Tools Must Be:
- **Broad in trigger**: "information worth remembering" not specific patterns
- **Simple in interface**: add_memory(content) not complex parameters
- **Intelligent in implementation**: routing and scoping happens internally

### Core Tools:
- `add_memory`: Store important information (LLM decides what's important)
- `search_memories`: Find relevant context (always called before responding)
- `update_memory`: Modify existing knowledge
- `delete_memory`: Remove outdated information
- `suggest_memory_update`: Propose changes for approval

## Processing Philosophy

### What to Capture
- Decisions and rationale
- Preferences and patterns
- Commitments and deadlines
- Knowledge and expertise
- Relationships and dependencies

### What to Ignore
- Transitional phrases
- Social pleasantries
- Redundant information
- Private unrelated content

### Multi-Modal Handling
- Text: Extract and store directly
- Images: Understand content + preserve reference
- Documents: Extract key insights + maintain source link
- Code: Capture pattern + usage context

## Integration Principles

### Source Systems
- Intelligent extraction of high-value knowledge
- Maintain references to original sources
- Respect system boundaries and permissions
- Track extraction lineage

### Knowledge Evolution
- Personal insights → Team patterns → Organizational standards
- Recent knowledge weighted higher than historical
- Conflicts tracked as relationships, not overwrites
- Natural decay through reduced relevance

## Success Metrics
- LLM naturally captures important information without prompting
- Every query enhanced by relevant context
- Knowledge flows where humans would share it
- System earns trust through accuracy
