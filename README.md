# Agentic Skills

## Creating new skill

Create a new directory with a `SKILL.md` file. The format highlights:

Front matter:

```
---
name: <name>
description: description of the skill, including possible trigger phrases
---
```

Trigger configuration:

```
## When to activate

Activate when the user says any of:
- "work on the next feature/plan/task"
- "continue the current plan"
- "execute plan `<name>`"
- "what's next?" or "what plans are pending?"
- Any reference to picking up or resuming planned work
```

Then other detailed instructions on how to perform this skill.

## Installation

Refer to your agent's documentation for most updated instructions:

### Claude

Refer to [official docs](https://code.claude.com/docs/en/skills)
copy each folder to `.claude/skills`

run `/skills` to list skills

### Open Code 

To install skills in **OpenCode**, you place `SKILL.md` folders into specific directories and restart the application. OpenCode automatically discovers these files and loads them based on your task.

### Installation Locations

OpenCode searches for skills in the following directories, prioritizing project-specific configurations over global ones:

*   **Global Skills**: Available in every project.
    *   Primary: `~/.config/opencode/skills/`
    *   Alternative: `~/.opencode/skills/`
    *   Claude-Compatible: `~/.claude/skills/`
*   **Project Skills**: Available only within the specific repository.
    *   Primary: `.opencode/skills/` (inside your project root)
    *   Alternative: `.claude/skills/`

### Installation Methods

**1. Manual Installation (Git or ZIP)**
Clone a skill repository or unzip a downloaded skill directly into the skills directory.
```bash
# Example: Installing a global skill from GitHub
git clone https://github.com/user/skill-name ~/.config/opencode/skills/skill-name

# Example: Installing from a ZIP file
unzip skill-name.zip -d ~/.config/opencode/skills/
```
Ensure the folder structure is `skill-name/SKILL.md`.

**2. Using the Skills CLI (Recommended)**
The universal `npx skills` tool installs skills to OpenCode and other supported agents simultaneously.
```bash
# Install a specific skill collection
npx skills add https://github.com/cloudflare/skills

# Install a specific skill from a registry
npx skills add replicate/skills
```

**3. Using OpenCode Marketplace**
For plugins containing skills, commands, and agents, you can use the `opencode-marketplace` CLI.
```bash
# Install from GitHub
bunx opencode-marketplace install https://github.com/user/repo
```

### Verification and Activation

*   **Restart Required**: You must quit and restart OpenCode for new skills to be detected.
*   **Verify**: Run `/list` or ask "What skills do you have?" within the chat.
*   **Trigger**: Skills activate **automatically** when your prompt matches the skill's `description` in the YAML frontmatter; there is no manual "enable" switch.

### Codex

To install skills in **OpenAI Codex**, you primarily use the built-in `$skill-installer` command within the Codex CLI or manually place skill folders into the `~/.codex/skills/` directory. Unlike OpenCode's passive discovery, Codex often requires an explicit install command or a restart to register new capabilities.

### Primary Installation Methods

**1. Using the Built-in `$skill-installer` (Recommended)**
Codex includes a native system skill specifically for managing other skills. You can invoke it directly in your chat session.
*   **List Available Skills**: Ask Codex, "Use `$skill-installer` to list curated skills." This fetches the official list from the `openai/skills` repository.
*   **Install by Name**: Say, "Use `$skill-installer` to install the `create-plan` skill." This downloads the skill from the curated list to your local directory.
*   **Install from GitHub**: You can install experimental or third-party skills by providing a URL: "Use `$skill-installer` to install `https://github.com/openai/skills/tree/main/skills/.experimental/create-plan`."

**2. Manual Installation**
You can manually clone or download skills into your Codex home directory.
*   **Directory**: Place the skill folder (containing `SKILL.md`) into `~/.codex/skills/` (macOS/Linux) or `C:\Users\<You>\.codex\skills\` (Windows).
*   **Command Line**:
    ```bash
    git clone https://github.com/openai/skills.git ~/.codex/skills/temp
    mv ~/.codex/skills/temp/skills/.curated/<skill-name> ~/.codex/skills/
    rm -rf ~/.codex/skills/temp
    ```

**3. Using the `/learn` Command (Community Marketplace)**
For access to over 44,000 community skills, you can install the `/learn` skill first.
*   **Setup**: Run `git clone https://github.com/agentskill-sh/ags.git ~/.codex/skills/learn`.
*   **Usage**: Restart Codex, then type `/learn seo` to search and install specific skills interactively.

### Verification and Activation

*   **Restart Required**: After installing skills manually or via the installer, you must **restart Codex** for the new skills to be loaded into the context.
*   **Verify**: Run `/skills` inside the Codex session to see the list of active skills.
*   **Trigger**: Skills activate automatically when your prompt matches the `description` defined in the skill's `SKILL.md` frontmatter.


