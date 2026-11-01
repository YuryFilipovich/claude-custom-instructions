# Customization guide

Start with the canonical [`instructions.md`](../instructions.md). Try it on representative work before changing it. Maintain one deliberate personal copy; this release does not provide alternative master prompts.

## Choose the right scope

**Global Claude.ai instructions** hold preferences you want across conversations. Use the [README installation steps](../README.md#install-in-claudeai). Keep stable language, communication, and evidence preferences here.

**Claude Project instructions** hold a particular project's audience, terminology, constraints, and workflows. In the project, use **Set project instructions**, enter your guidance, and choose **Save instructions**, as described in the [official project guide](https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects). Avoid duplicating the entire master here when it is already global. Review conflicts with other preferences.

**Task instructions** specify the current deliverable: for example, a 150-word email, a JSON response, or code for a particular runtime. State these explicitly when they differ from your usual preferences.

**Claude Code configuration** is a separate surface. The [official memory documentation](https://code.claude.com/docs/en/memory) describes user instructions in `~/.claude/CLAUDE.md` and shared project instructions in `CLAUDE.md` or `.claude/CLAUDE.md`. Keep coding conventions there and enforce tool permissions through the appropriate product settings. Claude.ai installation does not establish Code installation; natural-language rules are not security controls.

## Adapt by domain

### Software development

Put supported runtimes, dependency policy, build commands, test commands, architecture constraints, and acceptance criteria into the relevant project. Specify whether the deliverable is a patch, a complete file, or an explanation.

For example, a task can require Python 3.12, standard-library-only code, and explicit handling of empty input. Ask the assistant to identify which tests it ran and which remain unexecuted. Do not infer execution from code that merely includes test cases.

### Research and fact-checking

Specify the research question, cutoff date, jurisdiction or population when relevant, source hierarchy, and required citation format. Place recurring research protocols in the project; keep the particular question in the chat.

For a disputed claim, ask for evidence supporting and challenging it, then a conclusion with remaining uncertainty. If browsing is unavailable, provide documents or accept a clearly bounded answer. A request for citations does not make unsupported claims true.

### Business and professional work

Provide the audience, decision to support, budget assumptions, tone, and deliverable format. Keep organizational terminology and approved public claims in the project. Supply only information you are authorized to use.

For a recommendation, identify the constraints that would change the choice. For a document, specify whether you need a final draft or alternatives for review. Explicitly authorize any external actions you intend; the master otherwise asks for confirmation before externally visible actions.

### Everyday use

Keep the initial setup simple. State your preferred language or units if they should override the master defaults. A short question should not need a project or a special workflow.

If replies feel too long, adjust the response-depth preference in your personal copy or specify a short answer for the task. Test that change on both easy and complex questions so brevity does not remove essential caveats.

### Technical troubleshooting

Provide the observed behavior, expected behavior, versions, exact error, recent changes, and checks already tried. Redact credentials and private logs. Put stable environment details in the project, and incident-specific evidence in the conversation.

Request a distinction between confirmed findings and likely causes. Define which changes are authorized, and favor diagnostics and reversible fixes before disruptive changes. Keep a record of what actually changed and what confirmed the result.

### Creative work

Put audience, voice samples you may use, genre, length, and format close to the task. Label fictional premises explicitly. The evidence rules should prevent fictional claims being passed off as facts; they should not prevent invention within a creative brief.

If the default professional tone is unsuitable, request the voice you want. For brainstorming, specify the number and diversity of options. For a finished piece, ask for the finished piece rather than an explanation of the writing process.

## Input limits

The published v1.0.0 master is preserved exactly. The reviewed [personalization article](https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features) gives no numeric global-field limit, and full-text acceptance has not been tested in a signed-in account.

If your interface rejects it, record the displayed limit or error. The smallest adjustment to try is removing blank lines only from your personal pasted copy. Do not delete closing tags or let a field truncate the final sections. Reopen the saved value and compare it with the intended text.

If whitespace removal is insufficient, use only your essential general preferences globally and try the complete master in a Project, subject to that surface's actual limits. This changes the scope to that project and is not a verified global workaround. Another option is a deliberately shortened personal copy, with every omitted requirement recorded. Neither changes the canonical release file.

## Make changes measurable

Change one preference at a time, retain the previous version, and compare the same tasks in fresh chats. Use the [manual evaluation set](../tests/evaluation-prompts.md) and [results template](../tests/results.md). Record prompt modifications and model changes so observations can be interpreted later.

Reduce duplication before adding rules. If a preference only matters for one type of work, move it closer to that work. Check for contradictions whenever global, project, and task instructions overlap.
