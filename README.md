# AI Project Context - Claude Specialist System

A comprehensive collection of specialized AI assistants designed for Claude projects, each with dedicated system prompts, frameworks, and knowledge bases.

## 🎯 Overview

This repository contains a modular system of AI specialists, each optimized for specific domains and use cases. The system is designed to provide consistent, high-quality AI assistance across different areas of expertise.

## 📁 Repository Structure

```
ai-project-context/
├── .clinerules/                  # Cline rules for project development
├── memory-bank/                  # Persistent context across sessions
├── specialists/                  # AI specialist configurations
│   ├── registry.json             # Central index of all specialists
│   ├── jarvis_mcp_architect/     # MCP & Organizational Intelligence
│   ├── prompt_specialist/        # Prompt Engineering & Optimization
│   ├── zennya_os_specialist/     # Healthcare Strategy & Operations
│   └── marketing_os_specialist/  # Trust-based Marketing Operations
└── README.md                     # This file
```

## 🤖 Available Specialists

### 1. Jarvis MCP Architect
**Focus**: Memory-Context Protocol systems and organizational intelligence
- **Expertise**: MCP server development, mem0 integration, organizational knowledge capture
- **Mode**: Planning-first approach with implementation on request
- **Key Frameworks**: Organizational intelligence philosophy

### 2. Prompt Specialist
**Focus**: LLM prompt generation and optimization
- **Expertise**: Claude/GPT optimization, template creation, advanced prompting techniques
- **Mode**: Direct prompt generation with ready-to-use outputs
- **Key Frameworks**: CLEAR methodology, best practices, advanced techniques

### 3. Zennya OS Specialist
**Focus**: AI-first healthcare company strategy and operations
- **Expertise**: Founder-level decision making, ritual-first health design, ethical business practices
- **Mode**: Context-aware reasoning using Zennya's organizational DNA
- **Key Frameworks**: Vision & philosophy, mental models, brand ethos, operating model

### 4. Marketing OS Specialist
**Focus**: Trust-based marketing strategy and operations
- **Expertise**: Ethical customer acquisition, B2B channels, ritual-first funnel design
- **Mode**: Trust-based marketing without predatory tactics
- **Key Frameworks**: Marketing principles, funnel design, customer personas, pricing strategy

## 🏗️ System Architecture

### Registry System
The `registry.json` file serves as the central index, containing:
- Specialist metadata and descriptions
- Version tracking
- Capability definitions
- Activation triggers

### Specialist Structure
Each specialist follows a consistent pattern:
```
specialist_name/
├── manifest.json           # Configuration and metadata
├── system_prompt.md        # Core behavioral instructions
└── frameworks/             # Supporting knowledge base
    ├── framework1.md
    ├── framework2.md
    └── ...
```

### Manifest Schema
Each specialist's `manifest.json` includes:
- Role definition and description
- Capabilities and expertise areas
- Framework file references
- Keywords and activation triggers
- Version and creation metadata

## 🚀 Usage

### For Claude Projects
1. Copy the relevant specialist's `system_prompt.md` content
2. Include necessary framework files as context
3. Adapt the prompt for your specific use case
4. Reference the manifest for capability boundaries

### For Development
1. Clone this repository
2. Modify specialists as needed
3. Update the registry when adding new specialists
4. Commit changes with descriptive messages

## 🔄 Workflow Integration

### Git-Based Updates
- **Version Control**: Track all changes to system prompts and frameworks
- **Branching**: Use feature branches for major updates
- **Collaboration**: Share specialists across different Claude instances
- **Rollback**: Easily revert problematic changes

### Recommended Workflow
1. Make changes to specialist files
2. Test with Claude to validate improvements
3. Commit changes with descriptive messages
4. Push to GitHub for backup and sharing
5. Pull updates into other Claude projects as needed

## 📊 Specialist Capabilities Matrix

| Specialist | Strategy | Technical | Content | Analysis | Implementation |
|------------|----------|-----------|---------|----------|----------------|
| Jarvis MCP | ✅ | ✅ | ❌ | ✅ | ✅ |
| Prompt | ❌ | ✅ | ✅ | ✅ | ✅ |
| Zennya OS | ✅ | ✅ | ✅ | ✅ | ✅ |
| Marketing OS | ✅ | ❌ | ✅ | ✅ | ✅ |

## 🛠️ Maintenance

### Adding New Specialists
1. Create new directory with specialist name
2. Add `manifest.json` with proper schema
3. Create `system_prompt.md` with behavioral instructions
4. Add framework files in `frameworks/` directory
5. Update `registry.json` with new specialist entry

### Updating Existing Specialists
1. Modify relevant files (system prompt, frameworks, manifest)
2. Update version numbers in manifest
3. Test changes thoroughly
4. Update registry if capabilities change
5. Document changes in commit messages

## 📈 Version History

- **v1.0.0** (2025-06-17): Initial release with 4 core specialists
  - Jarvis MCP Architect
  - Prompt Specialist
  - Zennya OS Specialist
  - Marketing OS Specialist

## 🤝 Contributing

When contributing to this system:
1. Follow the established directory structure
2. Maintain consistency in manifest schemas
3. Use clear, descriptive commit messages
4. Test specialists thoroughly before committing
5. Update documentation as needed

## 📝 License

This project contains proprietary system prompts and frameworks. Please respect intellectual property and usage rights.

---

**Repository**: https://github.com/davidrfoote/ai-project-context
**Last Updated**: June 2025
