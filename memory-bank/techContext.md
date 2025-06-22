# Tech Context - Technologies & Development Setup

## Core Technologies

### Documentation & Content
- **Markdown**: Primary format for all documentation
- **JSON**: Configuration files (registry, manifests)
- **Git**: Version control system
- **GitHub**: Remote repository hosting

### AI Platforms
- **Claude Projects**: Primary deployment target
  - Cached context system
  - Project capacity limits
  - System prompt + document structure
- **Cline**: VS Code AI assistant
  - Memory Bank methodology
  - Custom instructions support
  - .clinerules for project-specific config

### Development Environment
- **VS Code**: Primary editor
- **Cline Extension**: AI-powered development
- **Git CLI**: Version control operations
- **macOS**: Development platform

## Technical Constraints

### Claude Projects Constraints
- **Context Window**: Limited project capacity (shown as percentage)
- **File Structure**: System prompt + uploaded documents
- **Caching**: Documents cached for all conversations
- **Token Limits**: Must optimize for efficiency

### Git/GitHub Constraints
- **File Size**: Keep individual files reasonable
- **Binary Files**: Avoid (stick to text-based formats)
- **Commit Size**: Atomic, focused commits
- **Branch Strategy**: Main branch for stable versions

### Markdown Constraints
- **Formatting**: Must be parseable by AI systems
- **Structure**: Clear headers and sections
- **Links**: Relative paths for internal references
- **Code Blocks**: Properly formatted for syntax highlighting

## Dependencies

### Required Tools
- Git (version control)
- Text editor (VS Code recommended)
- Cline extension (for Memory Bank workflow)
- GitHub account (for remote repository)

### Optional Tools
- Markdown preview extensions
- JSON validators
- Token counting tools
- Git GUI clients

## Tool Usage Patterns

### Git Workflow
```bash
git add .
git commit -m "Descriptive message"
git push
```

### Cline Integration
1. Custom Instructions: Global application
2. .clinerules: Project-specific rules
3. Memory Bank: Persistent context

### Claude Projects Setup
1. Create new project
2. Set system prompt
3. Upload framework documents
4. Monitor capacity usage

## Development Setup

### Repository Structure
```
ai-project-context/
├── .gitignore
├── README.md
├── registry.json
├── memory-bank/
│   ├── projectbrief.md
│   ├── productContext.md
│   ├── activeContext.md
│   ├── systemPatterns.md
│   ├── techContext.md
│   └── progress.md
├── .clinerules
└── [specialist_directories]/
    ├── manifest.json
    ├── system_prompt.md
    └── frameworks/
```

### Environment Configuration
- **Working Directory**: /Users/davidfoote/Documents/AI Project context
- **Git Remote**: https://github.com/davidrfoote/ai-project-context
- **Default Branch**: main

## Integration Patterns

### Claude + Cline Workflow
1. Use Memory Bank for project context
2. Load specialists into Claude Projects
3. Maintain consistency across both systems
4. Version control all changes

### Cross-Platform Considerations
- Design for multiple AI systems
- Use standard markdown formatting
- Avoid platform-specific features
- Test across different contexts

## Performance Optimization

### Token Efficiency
- Concise but complete documentation
- Avoid redundancy across files
- Use references instead of repetition
- Structure for selective loading

### Load Time Optimization
- Smaller, focused framework files
- Clear file naming conventions
- Logical organization structure
- Efficient markdown formatting
