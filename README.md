# Product Design Agent Kit

Practical AI skills for product designers who move between exploration, Figma production work, prototypes, and developer handoff.

## What is this?

A small, portable set of `SKILL.md` files. Each skill teaches an AI assistant a specific design workflow and the checks that matter in that workflow. This repository contains generalized versions of lessons from real product-design work; it contains no product specs, client files, screenshots, Figma file keys, or old Git history.

## Who is it for?

Product designers who already use an AI coding assistant with Figma and want the assistant to respect design stage, source fidelity, and motion behavior. The two Figma skills assume access to [Figma Console MCP](https://github.com/southleft/figma-console-mcp) for canvas reads and writes. Designers can use `explore-vs-final` without that integration.

## Why does it exist?

An AI assistant can make a polished screen while missing the actual job: moving too slowly during exploration, treating a port as a redesign, or declaring a prototype correct after checking only static frames. These skills capture the decisions and verification steps that prevent those failures.

## Quick start

1. Clone this repository:

   ```sh
   git clone https://github.com/reventhy/product-design-agent-kit.git
   cd product-design-agent-kit
   ```

2. Copy the skills you want into your assistant's skill directory. For a Claude Code project:

   ```sh
   mkdir -p /path/to/your-project/.claude/skills
   cp -R skills/explore-vs-final /path/to/your-project/.claude/skills/
   ```

   For a personal Codex installation, copy the chosen folders to `~/.codex/skills/`.

3. For the Figma skills, connect Figma Console MCP and verify it can read the intended file. Keep your Figma credentials in your local configuration, never in the project or this repo.

4. Ask for a concrete task, for example: “Use `explore-vs-final` to build three checkout directions for comparison.”

Each skill is self-contained. Install only the ones relevant to your work.

## Core concepts

- **Design stage changes construction.** Exploration favors fast comparison; a selected direction gets maintainable layout, tokens, components, and handoff checks.
- **A port has a source of truth.** Preserve the chosen flow and content while adapting the destination design system.
- **Motion has two kinds of verification.** Inspect the reaction graph and geometry with tools; play the prototype in Figma to judge the feel.
- **Canvas writes need a recovery point.** Pin the target file, save a version-history point, read back uncertain writes, and limit edits to the requested section.

## Workflows

| You need to… | Start with | Deliverable |
|---|---|---|
| Compare directions | `explore-vs-final` | Labeled options and a decision record |
| Prepare a chosen direction for handoff | `explore-vs-final` | Structured final design with intentional exceptions noted |
| Move an existing feature to another Figma file | `figma-clone-port` | Source-to-destination mapping and verification report |
| Build or debug a Smart Animate chain | `figma-prototype-motion` | Verified reaction graph, timing, and motion handoff |

## Skills

| Skill | What it covers | Author |
|---|---|---|
| [`explore-vs-final`](skills/explore-vs-final/SKILL.md) | Construction fidelity for options and final designs | namvunhatle |
| [`figma-clone-port`](skills/figma-clone-port/SKILL.md) | Porting components, screens, tokens, and prototype graphs | namvunhatle |
| [`figma-prototype-motion`](skills/figma-prototype-motion/SKILL.md) | Smart Animate rigs, reaction traps, timing, and handoff | namvunhatle |

For complementary UX, UI, and copy skills, see the [Yummy Labs source and download links](THIRD_PARTY.md). These remain authored and distributed by Yummy Labs; their files are not covered by this repository's MIT license.

## Examples

**Explore:** “I'm comparing three ways to show a saved item in a habit tracker. Use `explore-vs-final`; keep the options quick to change and tell me what must be rebuilt after I choose one.”

**Port:** “Use `figma-clone-port` to move the reviewed search flow from file A into file B. Keep the source flow and copy, use file B's components, and report every token substitution that changes contrast or layout.”

**Prototype:** “Use `figma-prototype-motion` to debug the card exit chain. Check matching layer paths, copied reactions, timeout values, and velocity before changing the easing.”

## Supported tools

- **Claude Code:** project-local `.claude/skills/` folders.
- **Codex:** personal `~/.codex/skills/` folders.
- **Figma Console MCP:** required to execute the Figma-specific procedures. Tool names and available API operations can change; check the connected server before running a snippet.

The skills are Markdown instructions. Installing them does not grant Figma access or permission to edit a file.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Contributions should be generalizable, tested on a real design task, and free of client or company information.

## License

The three bundled skills and repository documentation are released under the [MIT License](LICENSE). Third-party material linked in `THIRD_PARTY.md` is governed by its own terms and is not included in this license.
