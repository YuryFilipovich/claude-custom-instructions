# Design decisions

The canonical text is [`instructions.md`](../instructions.md). These notes explain its intended behavior; they do not add a second set of master instructions. References are collected in [Anthropic references](anthropic-references.md).

## 1. Role and objective

The collaborator role establishes a standard of work across domains. It asks for useful professional methods without asserting a biography. Invented degrees, awards, employment, or personal experience would make the answer less trustworthy; evidence and sound judgment should carry the explanation.

Role prompting is discussed in Anthropic's best-practices guide. Our emphasis on avoiding fabricated credentials is an editorial and honesty requirement, not a claim that role text confers actual qualifications.

## 2. Reasoning and quality

Adaptive reasoning is the design preference because a one-step question and a complex diagnosis have different needs. Mandatory elaborate reasoning can waste time and obscure a simple answer. Considering alternatives matters when they could change a conclusion; it need not become a ritual for every response.

The master requests conclusions, relevant supporting reasoning, and evidence. It does not ask for private internal deliberations. Natural-language instructions also do not enable API thinking features or set a model's reasoning budget.

Arbitrary self-evaluation targets such as 98/100 were intentionally excluded. A model assigning itself a number is not an independent measurement. The relevant checks are concrete: whether a calculation is correct, a requirement is satisfied, an assumption is justified, or a cited source supports the claim. This is a project judgment, distinct from the externally scored evaluation rubric.

Checking substantial work is intended to catch meaningful problems. It has a cost: redundant verification can increase latency without helping. Current official guidance includes model-specific advice to remove unnecessary verification requests. We preserve the supplied v1.0.0 master exactly and document this tension rather than silently changing it.

## 3. Accuracy and evidence

An answer should make its evidential footing understandable. Established facts, estimates, and hypotheses serve different purposes. Primary sources and official documentation make claims easier to audit; uncertainty should be explicit when the evidence is incomplete.

The evidence requirements are conditional on available tools. They ask for current research when appropriate, not invented browsing. A citation must support the associated claim; adding plausible-looking links is not verification. Publication dates and event dates may differ and should not be conflated.

Evidence quality also depends on context. An official specification can establish documented behavior, but an observed bug may require execution logs and reproducible tests. The master therefore emphasizes direct evidence as well as authoritative sources. It cannot guarantee that Claude will find or interpret that evidence correctly.

## 4. Communication style

Length should follow the complexity and purpose of the task. A short factual question does not need an outline; a migration plan may need assumptions, steps, examples, and trade-offs. Leading with the useful answer helps readers decide what to inspect next.

The prose preference, limited use of tables, latest-message language default, and selective TL;DR are project choices. They are not universal Anthropic requirements. Explicit output requirements should guide a particular task; request a table, JSON object, or specific language when needed.

Direct, natural wording is intended to reduce distraction. Avoiding flattery and fabricated expertise supports trust, while concrete examples and usable commands make the answer easier to apply.

## 5. Task execution

The execution group emphasizes finishing the actual deliverable. For code, that can mean a usable implementation rather than an unexplained fragment; for debugging, it means investigating a cause and validating a proportionate fix. The assistant must still distinguish a proposed action from one actually performed.

Clarifying questions have a cost, but acting on a critical missing detail can be worse. The master therefore permits sensible assumptions while reserving questions for material ambiguity or safety. It also prefers reversible changes and confirmation for consequential actions. A global preference cannot override a tool's permission system or provide authorization by itself.

Completeness is bounded by available evidence, environment, tools, and permissions. Honest partial completion with a precise blocker is more useful than an invented success report.

## 6. Final quality standard

The last section collects the desired outcomes into a short review standard. It is a reminder to check correctness, relevance, completeness, clarity, uncertainty, and practicality in proportion to the task. It is not a requirement for repeated hidden scoring or an assertion that self-review eliminates errors.

## Avoiding instruction overload

The master is already substantial. Keep a single personal version, remove contradictions, and avoid appending every domain workflow globally. Put repository commands, brand constraints, research protocols, and similar situational details into the relevant project or task.

When adapting a personal copy, change one behavior at a time and compare representative outputs. Remove rules that add work without an observable benefit. Preserve the published master for reproducibility; document intentional deviations when evaluating a customized version.

## What prompt engineering cannot do

Prompt text does not supply missing data, create tools, grant permissions, enforce security boundaries, or prove an answer correct. It may interact unpredictably with product instructions, model updates, and long conversations. More instructions can also make compliance harder.

This repository makes no measured claim that its baseline improves Claude's defaults. The [evaluation set](../tests/evaluation-prompts.md) is a way to investigate that question for a defined workflow, not evidence that it has already been answered.
