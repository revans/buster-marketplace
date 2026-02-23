# System Documentation Skill

**Purpose**: Extract and document how system components work, their design rationale, and practical applications. Creates comprehensive, architecturally-focused documentation similar to technical design documents.

---

## Documentation Methodology

When documenting a system component, follow this structure:

### 1. Discovery Phase

**Goal**: Understand the component thoroughly before writing.

**Steps**:
1. **Read all relevant files** - Implementation code, configuration, related documentation
2. **Identify key artifacts** - What files, schemas, or interfaces define this component?
3. **Map relationships** - What depends on this? What does this depend on?
4. **Find examples** - Look for existing usage, test cases, or production instances
5. **Understand evolution** - Check git history for why decisions were made

**Tools**: Use `Glob`, `Grep`, `Read` extensively. Don't guess—read the actual implementation.

### 2. Analysis Phase

**Goal**: Identify the "why" behind the "what".

**Key Questions**:
- **What problem does this solve?** (Don't describe what it does—explain what pain it eliminates)
- **Why this design?** (What alternatives were rejected? What tradeoffs were made?)
- **What patterns emerge?** (Are there recurring design principles?)
- **What are the constraints?** (Technical, business, or architectural limitations)
- **What's the failure mode?** (How does it break? How is it recovered?)

### 3. Documentation Phase

**Goal**: Write comprehensive, structured documentation.

**Required Sections**:

#### Section 1: Overview
- **Purpose statement** (1-2 sentences)
- **Key capabilities** (bullet list)
- **Core value proposition** (what makes this worth having?)

#### Section 2: The Problem This Solves
- **Enumerate specific problems** (Problem 1, Problem 2, etc.)
- **Contrast with alternatives** ("What X tracks" vs "What we need")
- **Explain pain points** (what happens without this component?)

#### Section 3: Architecture
- **High-level structure** (major components, data flow)
- **Key abstractions** (what are the main concepts/entities?)
- **File organization** (where does code live?)
- **Schema/Interface definitions** (what are the contracts?)

#### Section 4: Design Principles
- **Enumerate principles** (Principle 1, Principle 2, etc.)
- **Explain "why"** (rationale for each design decision)
- **Show examples** (concrete code showing the principle in action)
- **Explain benefits** (what does this principle enable?)

#### Section 5: Practical Applications
- **Real-world use cases** (6-7 examples)
- **Code examples** (show actual usage patterns)
- **Explain value** (what does each use case enable?)

#### Section 6: Implementation Details
- **Per-component breakdown** (if system has multiple parts)
- **Data flow** (how does information move through the system?)
- **Key algorithms** (if applicable)
- **Integration points** (how does this connect to other systems?)

#### Section 7: Future Enhancements
- **Planned improvements** (what's on the roadmap?)
- **Implementation sketches** (show how future features would work)
- **Value proposition** (why these enhancements matter)

---

## Documentation Quality Criteria

### ✅ Good Documentation

**Characteristics**:
- **Starts with "why"** - Explains problems before solutions
- **Shows evolution** - Explains how we got here (Problem → Design → Implementation)
- **Includes tradeoffs** - Discusses alternatives and why they were rejected
- **Provides examples** - Real code, not pseudocode
- **Explains failure modes** - What breaks and how to fix it
- **Links to related docs** - Points to relevant files, issues, or decisions
- **Uses consistent structure** - Same sections for similar components

**Example Phrases**:
- "This solves the problem of..."
- "We chose X over Y because..."
- "The tradeoff is..."
- "This enables..."
- "Without this, you would..."

### ❌ Poor Documentation

**Anti-patterns**:
- **Describes what code does** - Just repeating implementation (e.g., "This function takes X and returns Y")
- **Missing "why"** - No explanation of design rationale
- **No examples** - Abstract descriptions without concrete usage
- **Assumes knowledge** - Uses jargon without explanation
- **No structure** - Stream-of-consciousness writing
- **Stale** - Describes how things used to work

**Example Phrases to Avoid**:
- "This file contains..."
- "The function does..."
- "Here's how it works..."
- Without explaining WHY it exists or what problem it solves

---

## Research Strategy

### When Exploring a Component

**Start Broad**:
1. Find the entry point (main file, command, or class)
2. Read top-level documentation (README, CLAUDE.md, module comments)
3. Identify key files with `Glob` (e.g., `**/*orchestration*.{rb,md,json}`)

**Go Deep**:
4. Read implementation files completely (don't skim)
5. Search for usage examples with `Grep` (e.g., how is this called?)
6. Check tests to understand expected behavior
7. Review git history for context on major decisions

**Connect the Dots**:
8. Map dependencies (what does this import/require?)
9. Map dependents (what imports/requires this?)
10. Identify patterns (are there multiple similar components?)

### When Stuck

**If you can't find key information**:
- Search for related concepts (e.g., if looking for "orchestration", also search "pipeline", "workflow", "execution")
- Check parent directories for README or overview docs
- Look at test files (they often show usage patterns)
- Search for comments or docstrings
- Check git blame for the person who wrote it (commit messages often explain why)

**If implementation is unclear**:
- Trace execution flow (start at entry point, follow the calls)
- Look for configuration files (often reveal available options)
- Check for examples in the codebase
- Review related PRs or issues (if available)

---

## Writing Style Guidelines

### Voice and Tone
- **Direct and precise** - No fluff, no marketing speak
- **Technically detailed** - Assume reader is an engineer
- **Explanatory** - Assume reader is smart but unfamiliar with this specific component
- **Opinionated** - State design decisions clearly, explain tradeoffs

### Structure
- **Use headers liberally** - Make sections scannable
- **Use bullet lists** - For enumerations, options, or steps
- **Use code blocks** - Show real examples, not pseudocode
- **Use tables** - For field definitions, comparisons, or matrices
- **Use diagrams (ASCII)** - If helpful for data flow or architecture

### Examples
- **Real code** - From actual implementation, not invented examples
- **Commented** - Explain non-obvious parts
- **Complete** - Show full context, not just snippets
- **Practical** - Focus on common use cases, not edge cases

### Formatting
- **Bold for emphasis** - Key concepts, important warnings
- **Code formatting** - For file paths, variable names, function names, commands
- **Blockquotes** - For important notes or warnings
- **Horizontal rules** - To separate major sections

---

## Document Structure Template

```markdown
# [Component Name]

**Purpose**: [1-2 sentence explanation]

**Version**: [Schema version if applicable]
**Last Updated**: [Date]

---

## Table of Contents

1. [Overview](#overview)
2. [The Core Problem This Solves](#the-core-problem-this-solves)
3. [Architecture of [Component]](#architecture-of-component)
4. [Design Principles](#design-principles)
5. [Practical Applications](#practical-applications)
6. [Implementation Details](#implementation-details)
7. [Future Enhancements](#future-enhancements)

---

## Overview

[High-level explanation of what this component is and what it enables]

**Key capabilities**:
- Capability 1
- Capability 2
- Capability 3

**Value proposition**: [Why this matters]

---

## The Core Problem This Solves

[Describe traditional/alternative approaches and their limitations]

### Problem 1: [Name]
- **What exists**: "Current state..."
- **What we need**: "Desired state..."
- **Pain point**: [Specific consequence of not having this]

### Problem 2: [Name]
- **What exists**: "Current state..."
- **What we need**: "Desired state..."
- **Pain point**: [Specific consequence of not having this]

[Continue for 3-6 problems]

**The Solution**: [1-2 sentence summary of how this component solves these problems]

---

## Architecture of [Component]

[Describe the overall structure]

### [Sub-component 1]

[Details, code examples, schema definitions]

### [Sub-component 2]

[Details, code examples, schema definitions]

---

## Design Principles

### Principle 1: [Name]

**Why**: [Rationale]

**Example**: [Code or scenario showing this principle]

**Benefit**: [What this enables]

### Principle 2: [Name]

[Continue for 5-8 principles]

---

## Practical Applications

### 1. [Use Case Name]

**Problem**: "[User question or scenario]"

**Solution**: [How to use component for this]

```ruby
# Code example
```

**Value**: [What this enables]

### 2. [Use Case Name]

[Continue for 6-7 use cases]

---

## Implementation Details

[Deep dive into how it actually works]

### [Component Part 1]

[Technical details, algorithms, data structures]

### [Component Part 2]

[Technical details, algorithms, data structures]

---

## Future Enhancements

### 1. [Enhancement Name]

**Goal**: [What this will enable]

**Implementation**:
```ruby
# Code sketch
```

**Value**: [Why this matters]

### 2. [Enhancement Name]

[Continue for 5-7 enhancements]

---

## Conclusion

[Summarize the component's role in the system]

**This component enables**:
1. Capability 1
2. Capability 2
3. Capability 3

[Final statement about its value and role]

---

## Related Documentation

- **[Related Doc 1]**: `path/to/doc.md` - [Brief description]
- **[Related Doc 2]**: `path/to/doc.md` - [Brief description]
```

---

## Usage

### For Simple Components (Single File or Concept)

**Use this skill directly:**
1. Read the component's implementation
2. Follow the methodology above
3. Write documentation following the template

### For Complex Systems (Multiple Files, Components)

**Use the `/document-system` command** (if available):
```
/document-system <component-name>
```

Or **use Task tool with general-purpose agent**:
```
Task with subagent_type: general-purpose
Prompt: "Document the [component-name] system following the system-documentation-skill methodology"
```

---

## Examples of Good Documentation

### ✅ Example: orchestration.json Documentation

**What makes it good**:
- Starts with "The Core Problem This Solves" (6 specific problems with pain points)
- Explains design principles with rationale and examples (8 principles)
- Provides practical applications with real code (7 use cases)
- Shows implementation details with actual schemas and code
- Discusses future enhancements with implementation sketches
- Uses consistent structure throughout

**Structure used**:
1. Overview (what + why)
2. Problems (what pain does this eliminate?)
3. Architecture (how is it structured?)
4. Design Principles (why these decisions?)
5. Practical Applications (how to use it?)
6. Implementation Details (how does it work?)
7. Future Enhancements (what's next?)

---

## Anti-patterns to Avoid

### ❌ Writing Code Comments as Documentation

**Bad**:
```markdown
## OrchestrationHelpers Module

This module contains helper methods for orchestration.

### Methods

**read_agent_metadata(agent_type, artifact_path)**
- Reads metadata from agent artifacts
- Parameters: agent_type (string), artifact_path (string)
- Returns: Hash
```

**Why it's bad**: Just repeats what the code says, no insight into WHY or WHEN to use it.

**Good**:
```markdown
## Agent Metadata System

**Purpose**: Track agent confidence, quality scores, and execution metrics to enable cost prediction and quality assessment.

**Problem**: Without this, we can't tell if low-quality outputs are due to bad specs, poor agent performance, or complexity. We also can't predict costs for similar features.

**How it works**: Each agent reports confidence (0-1) and quality_score (0-1) in their output. The orchestrator reads this metadata and aggregates it into learning signals.

### read_agent_metadata

**When to use**: After any agent completes work, call this to extract their insights.

**Example**:
```ruby
metadata = OrchestrationHelpers.read_agent_metadata('architect', plan_path)
architect_confidence = metadata.dig('agent_insights', 'confidence')

if architect_confidence < 0.7
  puts "⚠️  Warning: Low architect confidence suggests unclear spec"
end
```

**Value**: Enables early intervention when quality signals are low.
```

### ❌ Missing "Why" and "Problem"

**Bad**:
```markdown
## Task System

The task system allows creating and updating tasks.

### Usage
```ruby
TaskCreate(...) # Creates a task
TaskUpdate(...) # Updates a task
```
```

**Why it's bad**: Doesn't explain what problem this solves or when to use it.

**Good**:
```markdown
## Task System

**Problem**: Complex multi-step work is hard to track. Users can't see progress, and we can't tell what's blocking.

**Solution**: The task system provides structured TODO tracking for orchestrations.

**When to use**:
- Features with 3+ distinct steps
- Long-running work (>30 minutes)
- When users ask "what's the status?"

**Value**:
- Users see real-time progress
- We can identify blocking issues
- Provides audit trail of what was done

### Usage
[Examples showing real scenarios]
```

---

## Summary

**Good system documentation**:
- Explains **problems** before solutions
- Shows **design principles** with rationale
- Provides **practical examples** with real code
- Discusses **tradeoffs** and alternatives
- Documents **failure modes** and recovery
- Points to **related systems**

**Use this skill when**:
- Creating architecture documentation
- Documenting new system components
- Explaining design decisions
- Training others on system architecture
- Creating reference documentation
