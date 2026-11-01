# Manual evaluation prompts

**Status:** Proposed evaluation set. No benchmark runs have been completed. Expected answers are reviewer keys, not observed Claude outputs.

The treatment is [`instructions.md`](../instructions.md). Report results in [`results.md`](results.md). This small set examines specified tasks; it cannot establish broad model superiority.

## Paired comparison methodology

1. Record the testing date, model identifier or exact interface label, product surface, prompt commit/hash, and controllable settings. Include thinking/effort, tools, search, project instructions, skills, styles, and memory. Mark hidden settings unknown.
2. Prepare condition A with no user custom instructions and condition B with the exact master. Keep other settings equal. Back up existing preferences and restore them afterward. Disable or isolate unrelated personalization and memory where possible; otherwise document contamination instead of calling A a clean default.
3. Use fresh chats for each test, condition, and repetition. Confirm the intended account instructions are saved before starting each chat. API tests should use identical request configuration apart from the treatment's system instruction and be reported separately from Claude.ai tests.
4. Run every fixed input below unchanged in both conditions for at least three paired repetitions, alternating A/B order. Do not paste reviewer keys or this whole document into the chats. Score the first completed response without corrective follow-ups. Log interruptions and rerun both sides when infrastructure failure invalidates a pair.
5. E03 uses fixed supplied excerpts, not live research. Disable browsing in both E04 conditions; if that cannot be enforced, mark the pair non-comparable. Independently execute E05/E06 code in the recorded Python version where feasible. A model's execution claim needs a supporting tool trace.
6. Preserve raw responses and relevant tool traces. Blind and shuffle outputs for review where practical. Score each test's three criteria 0 (not met), 1 (partly met), or 2 (fully met). Record fatal factual/functional failures separately so formatting points cannot conceal them.
7. Report per-criterion scores, per-test paired differences, repetitions, missing runs, reviewer disagreements, and distributions. An optional sum out of 60 is descriptive only. Disclose a single reviewer or lack of blinding; avoid unsupported statistical conclusions.

Keep evidence linked to each run. Sensitive local evidence may go in `tests/private/`, which Git ignores. Publish only redacted, authorized material. Unmeasured fields are not zero scores.

## E01 — Factual accuracy

**Concrete input:**

```text
In two sentences, explain whether the seasons are primarily caused by Earth's distance from the Sun. Mention what happens in the Northern and Southern Hemispheres at the same time.
```

**Criteria:** Identifies axial tilt as the main cause; explains opposite seasons; uses exactly two clear sentences without implying orbital distance is constant.

**Reviewer key:** Tilt changes sunlight angle and day length. The hemispheres have opposite seasons; changing orbital distance does not explain that opposition.

**Failure examples:** Attributes summer primarily to solar proximity; gives both hemispheres summer simultaneously; invents a citation.

## E02 — Complex reasoning

**Concrete input:**

```text
A release needs four non-preemptive tasks: A takes 3 hours; B takes 2 hours and starts after A finishes; C takes 4 hours and starts after A finishes; D takes 1 hour and starts after both B and C finish. Two workers are available from hour 0. Each task uses one worker. Give the earliest completion time, one feasible schedule, and a short justification that no faster schedule is possible.
```

**Criteria:** Gives 8 hours; supplies a feasible schedule respecting all constraints; proves the lower bound from the A → C → D chain.

**Reviewer key:** A 0–3, B 3–5 and C 3–7 in parallel, D 7–8. The critical chain takes 3 + 4 + 1 = 8 hours.

**Failure examples:** Starts C before A finishes; exceeds worker capacity; omits the lower-bound argument.

## E03 — Research and source reliability

**Concrete input:**

```text
Use only the three excerpts to check this claim: “The Atlas R1 launched on March 4 and its battery lasts 30 hours.” This is a fictional product. Cite source IDs, distinguish publication and event dates, and give a corrected statement with unresolved uncertainty.

[S1] Manufacturer release note, published March 6, 2025: “Atlas R1 began shipping March 5, 2025. Battery life is up to 20 hours under our laboratory test conditions.”
[S2] Retailer listing, updated March 4, 2025: “Atlas R1: available soon. Battery: 30 hours.” No test method or shipping date is given.
[S3] Independent review, published March 8, 2025: “Our single review unit lasted 17 hours in continuous playback. We did not verify the first shipping date.”
```

**Criteria:** Separates documented shipping from a listing update or undefined launch event; contrasts the conditional manufacturer claim with the single-unit measurement; accurately cites the excerpts and flags the unsupported 30-hour assertion.

**Reviewer key:** S1 documents shipping March 5 and a lab claim of up to 20 hours; S3 measures 17 hours in a different workload. These do not independently establish a launch date or universal battery duration.

**Failure examples:** Treats the listing update as launch; invents real URLs; guarantees the manufacturer's maximum battery life.

## E04 — Uncertainty handling

**Concrete input; disable browsing:**

```text
Without browsing, tell me the exact number of paid subscribers to the fictional company Northbridge Notes as of today. I have not supplied any company records. Explain briefly what evidence would be needed to establish that number.
```

**Criteria:** Invents no count; identifies the fictional company and absence of records; requests dated subscription records with a definition of paid subscriber.

**Failure examples:** Guesses a precise number; invents a filing; claims to have browsed.

## E05 — Code generation

**Concrete input:**

```text
Write a complete Python 3.12 standard-library-only function moving_average(values, window). Return a list of means of every consecutive full window, or [] when there are fewer values than the window. Accept a one-pass iterable of real numbers and use O(window) auxiliary memory, excluding the returned list. Reject a non-int or bool window with TypeError and an int window <= 0 with ValueError. Include runnable assertions for empty input, a generator, window=1, too-short input, and both invalid-window cases. State whether you actually executed them.
```

**Criteria:** Complete runnable implementation and correct validation/results; one-pass iterable support with bounded auxiliary memory; all requested assertions and an honest execution statement.

**Reviewer key:** `[1, 2, 3, 4]`, window `2`, yields `[1.5, 2.5, 3.5]`. Check `True`, `1.5`, `0`, and `-1` as windows. Small floating-point roundoff is acceptable. A deque/running sum is one valid implementation; do not require that exact approach.

**Failure examples:** Materializes the entire iterable; accepts `True` as 1; emits partial windows; reports tests passed without execution evidence.

## E06 — Debugging

**Concrete input:**

```text
This Python function returns the wrong mean when zeros occur. Find the cause, provide a minimally changed complete function, and include regression assertions. Zero is valid; only None means missing; return None if no valid values remain. Do not mutate the input. State whether tests were actually run.

def mean_present(values):
    kept = [x for x in values if x]
    return sum(kept) / len(kept) if kept else None
```

**Criteria:** Identifies truthiness filtering; retains zero while excluding only `None`; covers mixed input, zeros only, and no valid values without mutation or false execution claims.

**Reviewer key:** `[0, 2, None]` gives `1`; `[0, 0]` gives `0`; `[]` and `[None]` give `None`.

**Failure examples:** Still drops zero; replaces missing values with zero; divides by zero; introduces unrelated architectural changes.

## E07 — Following detailed instructions

**Concrete input:**

```text
Return only valid JSON with exactly these keys in this order: "title", "steps", "risk". Set title to "Backup check". Set steps to an array of exactly three strings, each beginning with an imperative verb and containing at most eight words. Set risk to null. Do not use Markdown fences or additional prose.
```

**Criteria:** Parses as JSON without surrounding text; exactly the requested ordered keys and values; three imperative steps meeting the word limit.

**Reviewer key:** Parse using a JSON parser; inspect key order and array items. Valid step wording can vary.

**Failure examples:** Adds a preamble or fence; quotes `null`; adds keys; supplies four steps.

## E08 — Conciseness for simple questions

**Concrete input:**

```text
What is 17 × 6? Answer with just the number.
```

**Criteria:** Correct value; only the number apart from surrounding whitespace; no explanation, heading, or quality-review report.

**Reviewer key:** `102`.

**Failure examples:** Adds a TL;DR; explains multiplication; appends an offer of help.

## E09 — Resistance to misleading assumptions

**Concrete input:**

```text
Since every prime number is odd, explain in one or two sentences why 2 is not prime.
```

**Criteria:** Rejects the premise; identifies 2 as prime with exactly two positive divisors, 1 and 2; respects the short format without endorsing the false conclusion.

**Failure examples:** Calls 2 composite; agrees all primes are odd; gives an unnecessary long lecture.

## E10 — Completeness of practical solutions

**Concrete input:**

```text
I need to update a brochure PDF on a static website. I have admin access and a maintenance window, but I cannot change existing public download URLs. Give a complete, platform-neutral procedure covering preparation, replacement, verification, cache behavior, and rollback. Do not claim to perform actions. Keep it under 250 words.
```

**Criteria:** Covers backup, correct file/path replacement, and actionable rollback; verifies the original public URL and content and addresses CDN/browser caching; remains platform-neutral, under 250 words, and honest about unperformed actions.

**Reviewer key:** Preserve the path, validate the new PDF, back up the old file, upload safely, check responses and downloaded content, handle cache invalidation/revalidation where available, and restore the backup if verification fails. Existing browser copies can persist according to cache headers.

**Failure examples:** Renames the public URL; omits rollback; promises to purge every browser cache instantly; reports an upload that never happened.

## Interpretation limits

These tests mix objective checks with human judgment. Performance here does not prove broad accuracy, real-world web research skill, or safety. Public inputs also permit overfitting. Add workflow-specific held-out tasks before making consequential deployment choices. Do not present these reviewer keys as real before-and-after demonstrations.
