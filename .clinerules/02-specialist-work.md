# Specialist Development Rules

## Project Context
This project manages specialized AI assistants for Claude Projects. Each specialist has domain expertise and provides consistent, high-quality assistance in specific areas.

## Specialist Structure
Each specialist follows this pattern:
```
specialist_name/
├── manifest.json       # Configuration and metadata
├── system_prompt.md    # Behavioral instructions
└── frameworks/         # Domain knowledge files
```

## Development Guidelines

### When Working on Specialists
1. **Maintain Consistency**: Follow established patterns across all specialists
2. **Token Efficiency**: Balance comprehensive instructions with context window limits
3. **Clear Boundaries**: Define what each specialist can and cannot do
4. **Version Control**: Document all changes with descriptive commit messages

### System Prompt Best Practices
- Start with clear role definition
- Include core capabilities and constraints
- Provide response patterns and examples
- Add quality checks and self-correction mechanisms

### Framework Organization
- Keep framework files focused and relevant
- Avoid redundancy across specialists
- Use clear headers and structure for AI parsing
- Include only essential domain knowledge

### Testing Approach
- Test specialists in Claude Projects
- Verify token usage and efficiency
- Ensure consistent behavior across sessions
- Document any issues or improvements needed

## Git Workflow
- Make changes locally
- Test thoroughly before committing
- Use descriptive commit messages
- Push to GitHub for version control and backup

## Cross-System Compatibility
Design specialists to work effectively in:
- Claude Projects (primary target)
- Cline with Memory Bank
- Other AI systems as needed
