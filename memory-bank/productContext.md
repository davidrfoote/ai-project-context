# Product Context - AI Specialist System

## Why This System Exists

### The Problem
- AI assistants like Claude reset context between sessions
- Generic AI responses lack domain-specific expertise
- Maintaining consistent AI behavior across projects is challenging
- No standardized way to version control AI personalities
- Token limits require careful context management

### The Solution
A modular system of specialized AI assistants that:
- Provides persistent, domain-specific expertise
- Maintains consistent behavior through structured documentation
- Enables version control and evolution tracking
- Optimizes token usage for efficient context loading
- Works across different AI platforms (Claude, Cline, etc.)

## How It Works

### For Users
1. **Select a Specialist**: Choose the appropriate AI assistant for your task
2. **Load into Claude Project**: Add system prompt and framework files
3. **Get Expert Assistance**: Receive domain-specific, consistent help
4. **Track Changes**: Use Git to manage updates and improvements

### System Architecture
```
Registry (index) → Specialist → System Prompt + Frameworks → AI Behavior
```

### Key Features
- **Modular Design**: Each specialist is self-contained
- **Clear Boundaries**: Defined expertise areas and exclusions
- **Rich Context**: Framework files provide deep domain knowledge
- **Version Control**: Full Git integration for tracking changes
- **Token Efficient**: Optimized for Claude's context window

## User Experience Goals

### Consistency
- Same specialist provides similar responses across sessions
- Predictable behavior within defined domains
- Clear personality and interaction patterns

### Expertise
- Deep domain knowledge in specialized areas
- Practical, actionable guidance
- Awareness of best practices and patterns

### Efficiency
- Quick setup in Claude Projects
- Minimal token usage for maximum value
- Clear documentation for easy understanding

## Integration Points

### Claude Projects
- Primary deployment target
- Cached context for persistent sessions
- System prompt + selected frameworks

### Cline Integration
- Can be used as custom instructions
- Compatible with Memory Bank methodology
- Supports project-specific deployment

### Version Control
- GitHub repository for collaboration
- Change tracking and rollback capability
- Documentation of specialist evolution
