# Buster Marketplace

## Included Plugins

### Documenter (v1.0.0)

**Purpose:** Extracts architecture, design principles, and practical applications from system components into structured technical documentation.

**Problem Solved:**
- Documentation describes *what* code does rather than *why* it exists
- Design rationale and tradeoffs get lost as systems grow
- New team members can't understand decisions without interrogating authors

**Solution:**
- Analyze any system component and generate why-first, architecturally-focused documentation
- Follows a consistent structure: problems → architecture → design principles → practical applications
- Documents get written once, compound in value as the team grows

#### Available Commands

**`/documenter:document-system <component>`** - Document a system component or entire system/repo
Researches implementation files, maps relationships, and produces comprehensive technical documentation.

#### Quick Start

```bash
# Document a system component
/documenter:document-system orchestration.json
/documenter:document-system "agent system"
/documenter:document-system skills framework --output docs/skills.md
```

---

## Installation

### Prerequisites

- Claude Code CLI installed and authenticated
- Claude Code version supporting plugins

### Local Development

```bash
# Clone repository
git clone https://github.com/revans/buster-marketplace.git
cd buster-marketplace

# Symlink documenter plugin to Claude Code
ln -s $(pwd)/documenter ~/.claude/plugins/documenter
```

---
## License

MIT License - see [LICENSE](./LICENSE).
