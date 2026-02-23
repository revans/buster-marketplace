# Buster Marketplace

A curated collection of Claude Code plugins for AI-assisted software development.

---

## What Is This?

Buster Marketplace is a plugin distribution system for Claude Code, Anthropic's official CLI assistant. It packages specialized capabilities as installable plugins that extend Claude's ability to generate production-grade code.

**Core Philosophy:** Encode judgment once, compound infinitely.

Rather than repeatedly describing preferences, plugins capture domain-specific taste, constraints, and patterns as reusable infrastructure. Each plugin turns explicit knowledge into automated leverage.

---

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

### Install from Marketplace

```bash
# Add marketplace repository
claude plugins add buster-marketplace https://github.com/revans/buster-marketplace

# Install documenter plugin
claude plugins install documenter
```

### Local Development

```bash
# Clone repository
git clone https://github.com/revans/buster-marketplace.git
cd buster-marketplace

# Symlink documenter plugin to Claude Code
ln -s $(pwd)/documenter ~/.claude/plugins/documenter
```

---

## Repository Structure

```
buster-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace metadata and plugin registry
├── documenter/                   # Documenter plugin
│   ├── .claude-plugin/
│   │   └── plugin.json           # Plugin manifest
│   ├── commands/
│   │   └── document-system.md    # /documenter:document-system
│   └── skills/
│       └── system-documentation-skill/
│           └── SKILL.md
├── LICENSE
└── README.md                     # This file
```

---

## License

MIT License - see [LICENSE](./LICENSE).
