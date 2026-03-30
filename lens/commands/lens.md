---
name: Lens
description: Load behavioral lenses, list available lenses, or clear active lenses. Usage: /lens [name] [name] | /lens list | /lens clear | /lens setup | /lens create | /lens help
color: cyan
---

# Lens

Arguments: [ARGUMENTS]

## Mode Detection

| Arguments | Action |
|-----------|--------|
| Empty or blank | Show active lenses (if any) and suggest `/lens list` |
| `list` | List all available lenses grouped by lens_type |
| `clear` | Clear all active lenses and remove pointer from CLAUDE.md |
| `setup` | Create user lens directories under `~/.dna/lens/` |
| `create` | Start a dialogue to create a new custom lens |
| `help` | Show all available commands and usage |
| One or more names | Load each named lens in order, concat, and apply |

---

## help

Output:

```
Lens — dynamic context switching for Claude.

Commands:
  /lens <name>              — activate a lens by name
  /lens <name> <name>       — activate a role and personality together
  /lens list                — show all available lenses
  /lens create              — create a new custom lens (dialogue)
  /lens setup               — create user lens directories (~/.dna/lens/)
  /lens clear               — deactivate all lenses
  /lens help                — show this help

Examples:
  /lens reality             — load the default reality lens
  /lens brainstorm feynman  — load a role + personality together
  /lens list                — see everything available

Custom lenses live in ~/.dna/lens/lenses/ and take priority over built-ins.
Run /lens setup to create that directory if you haven't already.
```

---

## setup

1. Create the following directories if they don't exist:
   - `~/.dna/lens/lenses/` — user's custom lens files
   - `~/.dna/lens/data/` — lens runtime data files

2. Confirm:
```
Lens directories created:

  ~/.dna/lens/lenses/   — drop custom lens files here
  ~/.dna/lens/data/     — runtime data written here by stateful lenses

Run /lens list to see all available lenses.
```

---

## list

1. Read all `.md` files from both lens directories:
   - Plugin lenses: `lenses/` in this plugin directory
   - User lenses: `~/.dna/lens/lenses/` (if it exists)

2. For each file, extract `name`, `lens_type`, and `description` from frontmatter

3. If a user lens has the same name as a plugin lens, the user lens takes priority (suppress the plugin version)

4. Group by `lens_type`, label the source, and output:

```
Available lenses:

  Roles
    reality     — [description]  (built-in)
    explorer    — [description]  (built-in)
    blindspot   — [description]  (built-in)
    my-lens     — [description]  (custom)

  Personalities
    direct      — [description]  (built-in)
    socratic    — [description]  (built-in)

Active: [role name or "none"] + [personality name or "none"]
```

---

## create

1. Check that `~/.dna/lens/lenses/` exists. If not, tell the user to run `/lens setup` first and stop.

2. Run a minimal dialogue — ask each question and wait for the answer before proceeding:

   **Q1:** "What's the name of this lens?" *(kebab-case, e.g. `investor`, `devil-advocate`)*
   **Q2:** "Is this a `role` or `personality`?"
   **Q3:** "One-line description — what does this lens do?"
   **Q4:** "Describe the intent: what should this lens make Claude do or how should it make Claude behave? Speak freely — this is the raw material."

3. Check if `~/.dna/lens/lenses/<name>.md` already exists. If so, ask: "A lens named `<name>` already exists in your custom directory. Overwrite it?"  If no, stop.

4. Using the four answers as input, generate a complete, well-structured lens file following the established format:
   - Frontmatter with `name`, `lens_type`, and `description`
   - A clear role or personality statement
   - "What Changes" section — specific behavioral directives, not descriptions
   - "What Stays the Same" section — constraints that hold regardless of the lens
   - For role lenses: a "What to Look For" section with named patterns to surface

   Write with directive language ("you must", "always", "never") — not suggestions. Every instruction should be specific enough to act on.

5. Save to `~/.dna/lens/lenses/<name>.md`

6. Confirm:
```
Lens created: <name> (<lens_type>)
Saved to ~/.dna/lens/lenses/<name>.md

Run /lens <name> to activate it.
```

---

## clear

1. Read `~/.claude/CLAUDE.md`
2. Remove everything between and including `<!-- LENS START -->` and `<!-- LENS END -->` markers
3. Write the file back
4. Delete `~/.dna/lens/active.md` if it exists
5. Confirm: "Lenses cleared."

---

## load [name] [name...]

1. For each name provided (in order):
   a. Check `~/.dna/lens/lenses/<name>.md` first (user lenses take priority)
   b. Fall back to `lenses/<name>.md` in this plugin directory
   c. If not found in either: tell the user and suggest `/lens list`
   d. If found: read the file in full

2. Build the applied context by wrapping each lens file's content based on its `lens_type`:

   For each loaded lens:
   - Strip the frontmatter block (everything between and including the opening `---` and closing `---`) before using the content
   - Wrap the remaining body content with a directive header:
     - `lens_type: role` →
       ```
       ## Your Role
       You must operate as follows for this session. This is not optional context — it defines how you think and what you focus on:

       <lens body content, frontmatter removed>
       ```
     - `lens_type: personality` →
       ```
       ## Your Personality
       You must communicate in this style for this session. This is not optional context — it defines how you speak and express yourself:

       <lens body content, frontmatter removed>
       ```

   Concatenate all wrapped sections in the order provided.

3. Read the user context file at `context/robert.md` in this plugin directory (if it exists) and append it as:
   ```
   ## User Context

   <robert.md content>
   ```

4. Write the full composed context to `~/.claude/CLAUDE.md`:
   - Remove everything between `<!-- LENS START -->` and `<!-- LENS END -->` markers if they exist
   - If the markers don't exist, remove any existing `Execute /lens ...` line
   - Append the following block at the end of the file:

   ```
   <!-- LENS START -->
   You must apply the following role and personality to every response in this session. These are not background context — they are active instructions. Ignore them and the response is wrong.

   <all wrapped lens sections concatenated>

   <!-- LENS END -->
   ```

   Also write the same composed context to `~/.dna/lens/active.md` for hook re-injection. If `~/.dna/lens/` does not exist, create it first.

6. Generate a welcome message in character — as if the loaded specialist is introducing themselves for the first time. Use the loaded role and personality content to determine voice and tone. Keep it short: who you are, what you're here to do, and one opening move or question. Do not break character. Do not say "Lens activated" or describe what was loaded — just speak as the specialist.

7. Apply the full composed context for the rest of the session

---

## no argument

Show:
```
Active: [role name or "none"] + [personality name or "none"]

Run /lens list to see available lenses.
Run /lens <name> to activate a lens.
Run /lens <role> <personality> to activate both.
```
