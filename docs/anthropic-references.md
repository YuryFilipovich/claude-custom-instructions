# Anthropic references

Official documentation reviewed on **November 1, 2026**. Links are living references and can change after this release. This review checked published documentation; it did not test the prompt in a signed-in Claude.ai account.

## Official guidance and its scope

### Prompting best practices

[Anthropic: Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)

The sections on XML tags, roles, output formatting, and reasoning support descriptive structure, an explicit role, clear formatting preferences, and proportionate reasoning. The guide also cautions against over-prompting and includes model-specific verification caveats.

**Project interpretation:** Six named sections make this master easier to inspect. The particular names, section count, prose preference, and ban on arbitrary self-scores are our choices. API system roles and thinking settings are not equivalent to Claude.ai account preferences. The preserved final-check language may be redundant for some models; evaluate it rather than assuming universal benefit.

### Personalization and global instructions

[Claude Help Center: Understanding Claude's personalization features](https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features)

This is the source for the account-wide scope and current/older installation labels used in the [README](../README.md#install-in-claudeai).

**Unverified:** The reviewed article does not document a numeric global-input limit. We do not infer unlimited capacity from that omission or claim that the complete prompt was accepted in a live account.

### Claude Projects

[Claude Help Center: How can I create and manage projects?](https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects)

The project setup section describes **Set project instructions** and **Save instructions**. Those instructions apply to chats in that project. This supports placing situational context there rather than accumulating it globally.

**Project interpretation:** Using a project to hold the complete master when a global field rejects it is a possible scope-changing fallback, not an officially prescribed installation method or a verified size workaround. We avoid plan-availability claims because they are unnecessary to installation and can change.

### Prompt engineering and evaluation

[Anthropic: Prompt engineering overview](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview)

Anthropic frames prompt engineering around defined success criteria and empirical testing and notes that some problems require other interventions. This supports providing an evaluation framework and withholding performance claims until evidence exists.

**Project interpretation:** The ten test inputs, paired trials, blinded review, and manual scoring scheme in this repository are our proposed methodology. They are not an Anthropic benchmark or certification.

### Evidence and uncertainty

[Anthropic: Reduce hallucinations](https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations)

The guide discusses admitting uncertainty, grounding answers in documents, and checking claims against sources. These ideas support the accuracy-and-evidence section.

**Project interpretation:** Preferring primary sources, distinguishing publication and event dates, and never claiming unperformed tool actions are explicit project requirements. None establishes that hallucinations have been eliminated.

### Claude Code instructions

[Claude Code Docs: How Claude remembers your project](https://code.claude.com/docs/en/memory)

The documentation describes `CLAUDE.md` files at user and project scopes and distinguishes behavioral context from enforced settings. This supports treating Claude Code separately from Claude.ai account instructions.

**Project interpretation:** Keep coding conventions and repository procedures in the relevant Code configuration; do not assume installing this master in Claude.ai configures a CLI session. This repository does not install or alter a user's Claude Code configuration.

## Boundaries of this documentation review

The sources support specific techniques and installation guidance. They do not endorse this master, verify its compatibility, or demonstrate performance gains. Where official guidance is model-specific, do not generalize it to every model.

The release preserves the supplied canonical wording even where a newer model might benefit from fewer instructions. See the [design decisions](design-decisions.md) and use the [evaluation prompts](../tests/evaluation-prompts.md) before drawing workflow-specific conclusions.
