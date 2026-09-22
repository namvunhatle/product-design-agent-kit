# Product Design Agent Kit

Practical AI skills for product designers who move between exploration, Figma production work, prototypes, and developer handoff.

## What is this?

A portable set of design skills plus optional Claude Code rules and agent templates. Each file teaches a specific workflow and the checks that matter in it. This repository contains generalized versions of lessons from real product-design work; it contains no product specs, client files, screenshots, Figma file keys, or old Git history.

## Who is it for?

Product designers who already use an AI assistant and want it to respect design stage, source fidelity, voice, and motion behavior. The Figma skills and Figma agents assume access to [Figma Console MCP](https://github.com/southleft/figma-console-mcp) for canvas reads and writes. The other skills work without it.

## Why does it exist?

An AI assistant can make a polished screen while missing the actual job: moving too slowly during exploration, treating a port as a redesign, or declaring a prototype correct after checking only static frames. These skills capture the decisions and verification steps that prevent those failures.

## Quick start

1. Clone this repository:

   ```sh
   git clone https://github.com/namvunhatle/product-design-agent-kit.git
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

Each skill is self-contained. Install only the ones relevant to your work. Claude Code users can also copy selected files from `rules/` to the project's `.claude/rules/` directory and from `agents/` to `.claude/agents/`. Check each agent's `tools:` list against the MCP tools installed in your environment before using it.

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
| Build structural screens from a wireframe kit | `figma-wireframe-kit` | Measured grayscale flow and open decisions |
| Build approved UI from an existing design system | `figma-design-system-ui` | Bound components/tokens and visual verification |
| Set a product voice across several contexts | `voice-tone-builder` | Voice guide, tone map, examples, and audit criteria |
| Explore a real frustration through satire | `theboxexplore` | Original ideas and a separate serious-concept table |

## Skills

| Skill | What it covers | Author |
|---|---|---|
| [`explore-vs-final`](skills/explore-vs-final/SKILL.md) | Construction fidelity for options and final designs | namvunhatle |
| [`figma-clone-port`](skills/figma-clone-port/SKILL.md) | Porting components, screens, tokens, and prototype graphs | namvunhatle |
| [`figma-prototype-motion`](skills/figma-prototype-motion/SKILL.md) | Smart Animate rigs, reaction traps, timing, and handoff | namvunhatle |
| [`figma-wireframe-kit`](skills/figma-wireframe-kit/SKILL.md) | Wireframe construction using a kit discovered in the target file | namvunhatle |
| [`figma-design-system-ui`](skills/figma-design-system-ui/SKILL.md) | Production UI using a live, read-only design system | namvunhatle |
| [`voice-tone-builder`](skills/voice-tone-builder/SKILL.md) | Consistent voice with tone changes by user context | namvunhatle |
| [`theboxexplore`](skills/theboxexplore/SKILL.md) | Explicitly invoked satirical idea exploration | namvunhatle; inspired by [Soren's Newsletter](https://sorens.beehiiv.com/) |

For complementary UX, UI, and copy skills, see the [Yummy Labs source and download links](THIRD_PARTY.md). These remain authored and distributed by Yummy Labs; their files are not covered by this repository's MIT license.

## Rules and agents

The [rules](rules/) are optional project conventions for Figma safety, design stage, model choice, and concise writing. The [agents](agents/) are Claude Code templates for bounded work:

| Agent | Scope | Can write? |
|---|---|---|
| [`copy-reviewer`](agents/copy-reviewer.md) | Batch microcopy review | No |
| [`figma-auditor`](agents/figma-auditor.md) | One-file Figma audit | No |
| [`gitbook-porter`](agents/gitbook-porter.md) | Spec-to-GitBook change request | Mirror file and change request; no merge |
| [`wireframe-builder`](agents/wireframe-builder.md) | Settled wireframe brief in a new section | Yes, Figma only in its new section |

These templates are adapted from a private setup, with project-specific facts removed. They are not active just because this repository was cloned. Install only the ones that fit your project and its available tools.

Call an agent by name with a bounded brief. Include the target product, source spec, and Figma file key when relevant; agents start without the main conversation's context. Use `figma-auditor` for read-only checks and `wireframe-builder` only when the flow is settled and a new section is acceptable. Review a GitBook change request before merging it.

## Examples

**Explore:** “I'm comparing three ways to show a saved item in a habit tracker. Use `explore-vs-final`; keep the options quick to change and tell me what must be rebuilt after I choose one.”

**Port:** “Use `figma-clone-port` to move the reviewed search flow from file A into file B. Keep the source flow and copy, use file B's components, and report every token substitution that changes contrast or layout.”

**Prototype:** “Use `figma-prototype-motion` to debug the card exit chain. Check matching layer paths, copied reactions, timeout values, and velocity before changing the easing.”

## Supported tools

- **Claude Code:** project-local `.claude/skills/` folders.
- **Codex:** personal `~/.codex/skills/` folders.
- **Figma Console MCP:** required to execute the Figma-specific procedures. Tool names and available API operations can change; check the connected server before running a snippet.
- **GitBook MCP:** needed only for the optional `gitbook-porter` agent. Verify its tool names before installing that template.

The skills are Markdown instructions. Installing them does not grant Figma access or permission to edit a file.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Contributions should be generalizable, tested on a real design task, and free of client or company information.

## License

The bundled skills, rules, agents, and repository documentation are released under the [MIT License](LICENSE). Third-party material linked in `THIRD_PARTY.md` is governed by its own terms and is not included in this license.
