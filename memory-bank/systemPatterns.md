# System Patterns - Architecture & Design Decisions

## System Architecture

### Core Components
1. **Registry System** (registry.json)
   - Central index of all specialists
   - Metadata and version tracking
   - Status and keyword management

2. **Specialist Modules**
   - Self-contained directories
   - Manifest for configuration
   - System prompt for behavior
   - Framework files for knowledge

3. **Version Control Layer**
   - Git for change tracking
   - GitHub for collaboration
   - Commit history as evolution log

## Key Technical Decisions

### Modular Design
- **Decision**: Each specialist is completely self-contained
- **Rationale**: Enables independent development and deployment
- **Implementation**: Separate directories with all required files

### Markdown-Based Documentation
- **Decision**: All content in markdown format
- **Rationale**: Human-readable, version-controllable, AI-parseable
- **Implementation**: .md files for all documentation

### Registry Pattern
- **Decision**: Central registry.json as index
- **Rationale**: Single source of truth for specialist discovery
- **Implementation**: JSON structure with metadata and paths

### Framework Separation
- **Decision**: Domain knowledge separate from behavioral instructions
- **Rationale**: Allows selective loading and better organization
- **Implementation**: frameworks/ subdirectory in each specialist

## Design Patterns in Use

### Specialist Pattern
```
Input (User Query) → Specialist Selection → Context Loading → Response Generation
```

### Manifest Schema Pattern
```json
{
  "role_id": "unique_identifier",
  "name": "Human-readable name",
  "system_prompt_file": "behavior.md",
  "framework_files": ["knowledge1.md", "knowledge2.md"],
  "capabilities": ["what it can do"],
  "exclusions": ["what it cannot do"]
}
```

### System Prompt Structure Pattern
1. Role Definition
2. Core Capabilities
3. Behavioral Instructions
4. Constraints & Guidelines
5. Response Patterns

## Component Relationships

### Hierarchy
```
registry.json
    ↓
specialist_manifest.json
    ↓
system_prompt.md + frameworks/*.md
    ↓
AI Behavior
```

### Integration Flow
1. User selects specialist from registry
2. System loads manifest to understand configuration
3. System prompt defines behavior
4. Framework files provide domain knowledge
5. AI generates responses within defined constraints

## Critical Implementation Paths

### Adding New Specialist
1. Create directory structure in specialists/
2. Write manifest.json
3. Create system_prompt.md
4. Add framework files
5. Update specialists/registry.json
6. Test and refine
7. Commit to Git

### Updating Existing Specialist
1. Modify relevant files
2. Update version in manifest
3. Test changes
4. Update registry if capabilities changed
5. Commit with descriptive message

### Cross-System Deployment
- **Claude Projects**: Load system prompt + selected frameworks
- **Cline**: Use as custom instructions or .clinerules
- **Other AI Systems**: Adapt format as needed

## Architectural Principles

### Separation of Concerns
- Behavior (system prompt) separate from knowledge (frameworks)
- Configuration (manifest) separate from content
- Index (registry) separate from implementations

### Single Responsibility
- Each specialist has one clear domain
- Each file has one clear purpose
- Each component has defined boundaries

### Open/Closed Principle
- Open for extension (new specialists)
- Closed for modification (existing specialist interfaces)

### DRY (Don't Repeat Yourself)
- Common patterns extracted to templates
- Shared knowledge in framework files
- Reusable structure across specialists
