---
description: Document a system component by extracting architecture, design principles, and practical applications
version: 1.0
model: sonnet
color: blue
permissionMode: bypassPermissions
arguments:
  - name: component_name
    description: Name of the component to document (e.g., "orchestration.json", "agent system", "skills framework")
    required: true
  - name: output_path
    description: Optional output path for the documentation (defaults to docs/<component-name>.md)
    required: false
skills:
  - system-documentation-skill
tools:
  - Read
  - Glob
  - Grep
  - Write
---

# Document System Component

You are documenting a system component following the **system-documentation-skill** methodology.

## Your Task

Create comprehensive documentation for: **{component_name}**

Output location: {output_path | or default to `docs/<component-slug>.md`}

## Process

### Phase 1: Discovery (Thorough Research)

**CRITICAL**: Do NOT start writing until you have thoroughly researched the component.

1. **Find all relevant files**:
   ```bash
   # Search for files related to the component
   Glob pattern="**/*{component_name}*"
   ```

2. **Read implementation files completely**:
   - Read main implementation files (don't skim)
   - Read related configuration files
   - Read test files (they show expected behavior)
   - Read existing documentation (README, CLAUDE.md)

3. **Search for usage examples**:
   ```bash
   # Find where this component is used
   Grep pattern="{component_name}" output_mode="files_with_matches"
   ```

4. **Map relationships**:
   - What depends on this component?
   - What does this component depend on?
   - Are there similar/related components?

5. **Check git history** (if helpful):
   ```bash
   # See evolution of key files
   git log --oneline -- path/to/component/files
   ```

### Phase 2: Analysis (Understand "Why")

Before writing, answer these questions:

1. **What problem does this solve?**
   - What pain existed before this component?
   - What alternatives were considered?
   - Why this approach over others?

2. **What are the design principles?**
   - What patterns emerge from the implementation?
   - What tradeoffs were made?
   - What constraints influenced the design?

3. **How is it actually used?**
   - Find 5-7 real usage examples
   - Identify common patterns
   - Note edge cases or special handling

4. **What makes this design good?**
   - What are the benefits of this approach?
   - What does it enable?
   - What would be worse without it?

### Phase 3: Documentation (Follow Template)

Use the **system-documentation-skill** template:

```markdown
# [Component Name]

**Purpose**: [1-2 sentence explanation]

**Version**: [If applicable]
**Last Updated**: [Today's date]

---

## Table of Contents

1. [Overview](#overview)
2. [The Core Problem This Solves](#the-core-problem-this-solves)
3. [Architecture of [Component]](#architecture)
4. [Design Principles](#design-principles)
5. [Practical Applications](#practical-applications)
6. [Implementation Details](#implementation-details)
7. [Future Enhancements](#future-enhancements)

---

## Overview

[3-4 paragraphs explaining what this is and why it matters]

**Key capabilities**:
- [Capability 1]
- [Capability 2]
- [Capability 3]

**Creates both**:
- [Benefit 1]: [Explanation]
- [Benefit 2]: [Explanation]

---

## The Core Problem This Solves

[Traditional approach and its limitations]

### Problem 1: [Name]
- **What exists**: "[Current state]"
- **What we need**: "[Desired state]"
- **Pain points**: [Specific consequences]

### Problem 2: [Name]
[Continue for 4-6 problems]

**The Solution**: [1-2 sentences summarizing how this solves these problems]

---

## Architecture of [Component]

### [Schema/Structure name if applicable]

[Describe structure, show code/JSON examples]

### [Sub-component 1]
[Details, examples]

### [Sub-component 2]
[Details, examples]

---

## Design Principles

### Design Principle 1: [Name]

**Why**: [Rationale]

**Example**: [Code or scenario]

**Benefit**: [What this enables]

### Design Principle 2: [Name]
[Continue for 6-8 principles]

---

## Practical Applications

### 1. [Use Case Name]

**Problem**: "[User question or scenario]"

**Solution**: [How to use this]

```[language]
# Real code example showing usage
```

**Value**: [What this enables]

### 2. [Use Case Name]
[Continue for 6-7 use cases]

---

## Implementation Details

[Deep dive into how it works]

### [Component Part 1]
[Technical details, data structures, algorithms]

### [Component Part 2]
[Technical details, data structures, algorithms]

---

## Future Enhancements

### 1. [Enhancement Name]

**Goal**: [What this will enable]

**Implementation**:
```[language]
# Code sketch showing how this would work
```

**Value**: [Why this matters]

### 2. [Enhancement Name]
[Continue for 5-7 enhancements]

---

## Conclusion

[Summary paragraph about the component's role]

**This component enables**:
1. [Capability 1]
2. [Capability 2]
3. [Capability 3]

[Final statement about value and importance]

---

## Related Documentation

- **[Doc 1]**: `path/to/doc.md` - [Brief description]
- **[Doc 2]**: `path/to/doc.md` - [Brief description]
```

## Quality Checklist

Before finishing, ensure your documentation:

- [ ] **Starts with problems** - Explains what pain this eliminates
- [ ] **Shows design rationale** - Explains WHY decisions were made
- [ ] **Includes real examples** - Uses actual code from the codebase
- [ ] **Discusses tradeoffs** - Mentions alternatives and why rejected
- [ ] **Explains failure modes** - What breaks and how to recover
- [ ] **Links related docs** - Points to relevant files/resources
- [ ] **Uses consistent structure** - Follows the template

## Anti-patterns to Avoid

❌ **Don't just describe what code does** ("This function takes X and returns Y")
✅ **Explain why it exists and what problem it solves**

❌ **Don't write abstract descriptions without examples**
✅ **Show real code and usage patterns**

❌ **Don't assume reader knows context**
✅ **Explain jargon and provide background**

❌ **Don't skip the "why"**
✅ **Always explain design rationale and tradeoffs**

---

## Example: orchestration.json Documentation

Reference: `docs/ORCHESTRATION_AND_LEARNING_SYSTEM.md`

**What makes it good**:
- Starts with 6 specific problems and pain points
- Explains 8 design principles with examples and rationale
- Provides 7 practical applications with real code
- Shows actual schemas and implementation patterns
- Discusses future enhancements with code sketches
- Uses consistent structure throughout

---

## Output

Create the documentation file at: **{output_path}** (or default location)

**After writing**:
1. Tell user where documentation was created
2. Summarize what was documented
3. Highlight 2-3 most interesting insights discovered
4. Suggest related components that might benefit from documentation
