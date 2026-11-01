# Claude Custom Instructions

**Accuracy, thoughtful reasoning, clear communication, and practical follow-through.**

[![Version 1.0.0](https://img.shields.io/badge/version-1.0.0-5865F2)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![For Claude](https://img.shields.io/badge/for-Claude-D97757)](#compatibility)

A carefully designed set of custom instructions for Claude, focused on accuracy, reasoning, research, clarity, and practical problem-solving. Use it as an account-wide starting point, then adapt it to the work you actually do.

The instructions ask Claude to check meaningful claims, challenge flawed assumptions, acknowledge uncertainty, and deliver usable results. Simple questions should still get simple answers.

**Status:** Initial release. No comparative benchmarks or model compatibility tests have been completed. This is an independent community project, without Anthropic affiliation or endorsement.

## Quick start

1. Open [`instructions.md`](instructions.md), then select **Raw** on GitHub.
2. Copy the entire text, including all six XML-style sections. Do not copy this README or add Markdown code fences.
3. Paste it into Claude's account-wide instructions using the steps below.
4. Start a new chat and try a familiar task. Judge the result against your own requirements.

[`instructions.md`](instructions.md) is the single source of truth. This repository intentionally has one master prompt, with no alternate editions or installation dependencies.

### Install in Claude.ai

Navigation checked against [Anthropic's personalization documentation](https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features) on **November 1, 2026**:

1. Open [Claude.ai](https://claude.ai) and click your initials in the lower-left corner.
2. Select **Settings → Your Claude**.
3. Find **Instructions** and paste the complete master text. If you already have preferences, keep a backup and reconcile conflicts first.
4. Apply the change using the control provided by your interface, then reopen the field to check that the full text was retained.

In the older Settings layout, Anthropic documents **Settings → Account → Instructions for Claude**. These are account-wide instructions; project-specific guidance belongs in a Project. See the [customization guide](docs/customization-guide.md).

**Length and verification:** The master text contains 6,216 Unicode characters including its final newline. The reviewed official personalization guidance does not specify a numeric input limit. Full-text acceptance in a signed-in Claude.ai account has not been tested. If your interface rejects the text, do not silently truncate it: first remove only blank lines in your personal pasted copy. If it still does not fit, keep a small set of general preferences globally and use the complete master as project instructions where accepted. That changes its scope; it is not an identical global installation. See [input-limit guidance](docs/customization-guide.md#input-limits).

## How the instructions work

Six tagged sections organize the behavioral preferences. Tags separate responsibilities; they are not executable code, an API configuration, or a request for XML output.

| Section | Purpose |
| --- | --- |
| `role_and_objective` | Collaborate with domain-appropriate standards without inventing credentials. |
| `reasoning_and_quality` | Scale reasoning to difficulty, consider relevant alternatives, and review substantial work. |
| `accuracy_and_evidence` | Separate facts from assumptions, consult available sources, and report uncertainty honestly. |
| `communication_style` | Lead with the answer and adapt language, length, examples, and organization. |
| `task_execution` | Complete the requested work, respect constraints, and verify outcomes where feasible. |
| `final_quality_standard` | Apply a proportionate final check for correctness, relevance, clarity, and usefulness. |

The intent is a reusable baseline. Your immediate request supplies the task, audience, constraints, and deliverable. Project instructions supply context that should not apply to every conversation.

Read the [design decisions](docs/design-decisions.md) for the rationale and trade-offs behind each group.

## Where this can help

- **Software development:** Specify an environment, request complete code, and distinguish executed checks from suggested tests.
- **Research:** Ask for evidence behind a claim, source quality, and explicit gaps in available information.
- **Troubleshooting:** Compare plausible causes, identify confirming evidence, and start with reversible fixes.
- **Professional work:** Turn a defined objective and constraints into a concrete deliverable with justified trade-offs.
- **Everyday questions:** Get a direct answer without a mandatory essay or ceremonial introduction.
- **Creative work:** Keep the requested voice and format while distinguishing invented material from factual claims.

These are intended use cases, not measured examples of improvement.

## Design principles

| Rigid prompting pattern | This project's design choice |
| --- | --- |
| Require elaborate reasoning for every response | Ask for depth when the problem warrants it. |
| Repeat revisions until a self-assigned score reaches 98/100 | Check concrete requirements and correct meaningful weaknesses. |
| Claim awards or professional credentials | Demonstrate expertise through the work. |
| Impose the same length and format on every task | Adapt detail and structure to the request. |
| Treat confidence as evidence | Identify assumptions, cite sources, and admit unknowns. |
| Describe a possible solution and stop | Produce the requested usable result within available capabilities. |

These are design comparisons. They do not establish superiority over Claude's defaults or other prompts.

## Limitations and trade-offs

Instructions guide behavior; they do not guarantee correctness, safety, execution, or compliance. They cannot grant browsing, file access, tools, credentials, or permissions. A request to verify facts is useful only when evidence is available and actually checked.

The full prompt adds context and may add latency, verbosity, or unnecessary checking. Some preferences will not suit every workflow: the master discourages unsolicited tables and asks for confirmation before externally visible actions. Give explicit task-level formatting and authorization when appropriate. Existing account preferences, project instructions, and conversation context can also conflict.

Anthropic's current best-practices guide includes model-specific cautions about excessive verification. The preserved v1.0.0 master still asks for a final quality check. Treat that as a trade-off to evaluate, not a universally optimal setting. See [references and compatibility caveats](docs/anthropic-references.md).

For consequential decisions, independently verify material claims. Prompting cannot replace domain expertise, reliable evidence, or real tests.

## Customize for your work

Use the [customization guide](docs/customization-guide.md) for development, research, business, everyday questions, troubleshooting, and creative work. Keep broad preferences globally and situational requirements close to the task. Edit a personal copy deliberately rather than maintaining competing master prompts here.

## Compatibility

The master is plain text intended for Claude's instruction surfaces. It does not depend on a named model version. That is a format intention, not verified compatibility with every Claude model, plan, interface, or context size.

Claude.ai global instructions, Claude Projects, API system instructions, and Claude Code configuration have different scopes. Installing in one does not establish installation in the others. Model behavior and available tools vary; re-evaluate after model or product changes. No Claude model has been tested with this release.

## Evaluation

[`tests/evaluation-prompts.md`](tests/evaluation-prompts.md) provides ten concrete manual tests and a paired comparison method. [`tests/results.md`](tests/results.md) is an unfilled reporting template. No benchmark results, performance gains, or real before-and-after examples are claimed.

## Documentation and official references

- [Design decisions](docs/design-decisions.md)
- [Customization guide](docs/customization-guide.md)
- [Annotated Anthropic references](docs/anthropic-references.md), including the distinction between official guidance and project judgments
- [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
- [Claude personalization](https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features)
- [Claude Projects](https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects)
- [Changelog](CHANGELOG.md)

## Credits and license

Inspired by [DenisSergeevitch/chatgpt-custom-instructions](https://github.com/DenisSergeevitch/chatgpt-custom-instructions). The instructions for this repository are independently written; the inspiration repository's prompt text is not reproduced here.

Original repository content is available under the [MIT License](LICENSE), copyright © 2026 Yury Filipovich. Linked third-party material remains subject to its own terms. Claude and Anthropic names identify the intended product and documentation sources; they do not imply endorsement.
