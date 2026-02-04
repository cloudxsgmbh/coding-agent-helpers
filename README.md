# coding-agent-helpers

This repository contains a collection of skills and tools for our coding agents.

## References

- [AGENTS.md](https://agents.md)
- [Skills](https://agentskills.io)

## Coding Agents

### Pi Coding Agent

Installation and usage: https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent

Clone this repository and then create symbolic links.

#### Skills

To link skills for the Pi coding agent:

```bash
# Allow the script to be executed
chmod +x skills/link-skills-pi
# Run the script to link skills to ~/.pi/agent/skills/
./skills/link-skills-pi
```

Invoke a skill by typing `/skill:name` in the chat.

#### Extensions

To link extensions for the Pi coding agent:

```bash
# Allow the script to be executed
chmod +x pi-extensions/link-extensions-pi
# Run the script to link extensions to ~/.pi/agent/extensions/
./pi-extensions/link-extensions-pi
```

| Extension Name | Description                                                                                  |
| -------------- | -------------------------------------------------------------------------------------------- |
| answer         | Extract Q&A pairs from assistant responses. Call `/answer`                                   |
| todos          | Manage and track your to-do items. [How to use](https://www.youtube.com/watch?v=ZcKbzxziA5k) |
| whimsical      | Prints out random messages while working.                                                    |

#### Directories

- `~/.pi/agent/skills/`: Place your custom skills here. Each skill should be in its own directory with a `SKILL.md` file describing the skill.
