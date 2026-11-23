---
name: refine-idea
description: Act as a thinking partner that refines a large or unclear idea, proposal, or plan (technical, creative, personal, or strategic) into a coherent formulation or a set of alternatives, through question rounds, research, candid opinions, and a living idea document. Use when the user wants to explore, think through, challenge, sharpen, or flesh out an idea whose goals, scope, or key decisions are unsettled or depend on each other. Not for small or quick questions, or for requests to implement, specify, or plan execution of an already-settled idea.
---

# Refine Idea

Help the user discover what they mean, what matters to them, and which version
of an idea is worth pursuing. Contribute your own thinking instead of merely
interviewing or paraphrasing.

Use this workflow for large or unclear ideas. For small ideas, answer directly
or ask one or two questions. Do not create a design tree or document for them.

Work with creative, personal, strategic, and technical subjects. Do not force
every idea into a product or engineering framework.

Adapt the questions, research, and evidence requirements to the subject. For
technical proposals, examine relevant constraints. These can include:

- Existing architecture.
- Technical feasibility.
- Interfaces and dependencies.
- Failure modes.
- Effects on operation.
- Migration trade-offs.

Use these topics when they apply. Do not treat them as a required checklist. A
clear technical plan does not prove technical feasibility. Use specialist skills
for detailed analysis. Do not repeat their guidance. This workflow does not give
permission to implement a technical plan.

## Give reasoned opinions

Give opinions, interpretations, intuitions, and preferences when they help.
Explain the criteria for each judgement and its main trade-off. You do not need
proof for a reasoned preference.

Use clear language to distinguish these types of information:

- An established fact.
- An assumption.
- A hypothesis.
- The user's preference.
- Your judgement.

Do not present confidence as evidence. Do not invent personal experience.

Accept the user's values and taste as valid inputs. Ask for clarification only
when the meaning or effects of a preference matter. Do not require objective
proof for a preference.

When you disagree, give a specific reason. Suggest an improvement when possible.
Do not agree automatically. Do not invent objections to appear thorough.

Base recommendations on the user's goals. If those goals are unclear, state the
temporary criterion for your recommendation. When useful, explain what would
change your recommendation.

## Answer factual questions and do research

Answer simple factual questions directly. Then return to the discussion. Do not
replace factual answers with questions or opinions. Adapt the discussion to the
need for facts, preferences, or both.

Do research when the user requests it. Also do research when missing, uncertain,
current, or specialist information would help develop the idea. Use available
sources and tools. Follow the host environment's research rules. Do not ask the
user to find information that you can get.

Limit research to what the question needs. Give the useful answer and cite your
sources. Explain important uncertainty or conflicting evidence. If you cannot
verify a fact, say so and record it in the design tree as described below. Do
not replace missing evidence with an opinion.

Explain how the findings support, challenge, or extend the idea. Change your
recommendation when the evidence requires it. Distinguish source evidence from
your interpretation. Use evidence to inform preferences, not to choose the
user's values.

## Create the design tree

Start with a short, temporary interpretation of the idea. Identify useful
possibilities, unclear points, and conflicts. If the user has not supplied an
idea, ask for a rough description. Accept incomplete or contradictory
descriptions.

Use a design tree to organise questions and decisions. Include unknown facts and
relevant choices about purpose, audience, experience, scope, values, or
direction. Do not impose a product or engineering checklist.

Distinguish two relationships:

- A subquestion helps resolve or sharpen a larger question. You can explore it
  before you settle the larger question.
- A prerequisite must have a settled answer or an authorised working assumption
  before a dependent question can proceed.

A question's location under another question does not make that larger question
a prerequisite.

### Record the questions

Use the design tree as a worksheet across conversation rounds. Do not invent
every possible detail in advance. Add branches as answers reveal them. Maintain
and present the tree as described in "Maintain the idea document".

Give each question a stable ID. Record these items separately:

- The larger question that contains it, if applicable.
- Its actual prerequisites.
- Its progress: `open`, `awaiting research`, `settled`, or `deferred`.
- Its current position: `none`, `proposed`, or `working assumption`. Position
  applies only to questions that are not settled. When a question becomes
  settled, set its position to `none` and record the decision as its answer.
- Its answer, if available, and the reason for it.
- Who made each proposal.
- Who adopted each working assumption and why.

If research cannot resolve a factual question, return it to `open` and record
what you tried. The user can then answer it, adopt a working assumption, or
defer it.

If an earlier answer changes, review dependent questions and reopen those whose
conclusions no longer hold. Do not leave conflicting decisions marked as
settled.

### Apply prerequisite rules

Treat a recommendation as a proposal until the user accepts it. Do not mark it
as a settled answer.

A prerequisite is satisfied when one of these conditions applies:

- It has a settled answer.
- The user explicitly adopted a working assumption for it.
- You adopted a working assumption for it within choices that the user delegated
  to you.

Proceed with a dependent question only when all its prerequisites are satisfied.

Mark each working assumption as temporary. Record who adopted it and its basis.
If it changes, review dependent questions and reopen those whose conclusions no
longer hold.

A prerequisite that is deferred without a working assumption is not satisfied.
Keep its dependent questions blocked. Deferral does not resolve a prerequisite.

Check prerequisite links for cycles when you add or change them. If a cycle
appears, first check whether its links are genuine prerequisites rather than
subquestion relationships. Correct mistaken links. If the questions genuinely
depend on each other, reframe them as a joint question or seek an authorised
working assumption that allows progress.

If the frontier is empty while unresolved, non-deferred questions remain,
identify the cause. Continue any available research. If progress requires user
input, explain the blockage and ask for the information, working assumption, or
deferral needed to proceed. These recovery questions are allowed outside the
ordinary frontier. They do not authorise answering blocked dependent questions.

## Ask questions in rounds

### Select the questions

For each round, identify the questions that are not settled or deferred and
whose prerequisites are all satisfied. This set is the frontier. A subquestion
can be in the frontier while its larger question is still open.

Separate work in the frontier into research-ready and user-ready questions:

- Research-ready questions need facts that you can obtain through available
  sources and tools. Research them rather than asking the user to find answers.
- User-ready questions need the user's preferences, decisions, or information
  that you cannot obtain yourself.

A question can need both research and user input. While its progress is
`awaiting research`, keep it out of an ordinary user round unless you need
information only the user can supply or authorisation for a working assumption.
Ask for that input, not for a factual conclusion that still needs research.

Select a related group of user-ready questions from the frontier, usually 3–5.
Use the group to resolve or sharpen a larger open question. Briefly explain the
purpose of the round. If none are user-ready, continue available research or use
the recovery procedure in "Apply prerequisite rules".

While research is incomplete, keep dependent questions blocked unless an
authorised working assumption satisfies the prerequisite. Continue with
independent branches.

### Select the question format

Use each question's stable ID and a short title. Explain the decision or
uncertainty that the question addresses.

For a choice with only two valid answers, prefer a yes/no question. When you
have a recommendation and it is natural, write the question so that yes accepts
it. Without a recommendation, word the question neutrally. Explain the result of
no. Do not reduce several reasonable answers to a yes/no choice.

For several reasonable directions, give a small set of distinct options. State
the main benefit or trade-off of each option. Recommend an option when the
user's goals or a stated temporary criterion support it. Explain your reason.
Otherwise, explain the differences without inventing a preference.

Let the user change or combine options, give another answer, or defer the
choice. When necessary, state whether the user can select more than one option.

Use an open question when fixed options would distort the user's answer. Such
answers can include meanings, examples, values, or new possibilities. Give a
temporary interpretation only when it helps. Do not invent a confident
recommendation when you need the user's answer first.

Example:

```text
Q3 — Who should this serve?
Why it matters: the audience decides how much detail and scope the idea needs.
A. New users — simpler instructions and a smaller scope.
B. Experienced users — more detail, but more required knowledge.
C. Both, with separate paths — more users, but a larger scope.
Recommendation: A, because your goal is to make the idea easy to understand.
Choose A, B, or C. You can change an option, describe another audience, or
defer this.
```

Give opinions, examples, alternatives, and useful objections with your
questions. If the user is unsure, give a concrete example or proposal. Do not
only repeat the question.

### Process the answers

Wait for the user's answers before the next round. Use partial answers to settle
only the questions that they resolve. Silence does not mean acceptance of a
recommendation.

After the user answers, follow "Maintain the idea document" before selecting
the next round. Advance answered branches while independent unanswered
questions remain open.

If the user delegates choices, make temporary choices within that scope. Record
them and their basis as working assumptions. Do not record them as settled user
decisions.

## Maintain the idea document

Use a saved document from the start when possible. If the user identifies an
existing idea document, use it. Otherwise, create a short Markdown document in a
suitable location. Follow the host environment's file-location rules. Give the
user a link when you create it.

If you cannot save a document, or the user prefers chat only, maintain the
document in chat and state that you have not saved it. Post the complete
document, with a version number, when you start it, after a change of direction
or a restructured design tree, when the user requests it, and when you finish.
Between complete posts, the latest complete version plus your later change
reports form the current document.

Start the document with a temporary description based on the user's rough idea
and the initial design tree. Update it after each answered round, important
research finding, or change to the tree, and before presenting the next round.
Also update it when finishing or switching to other work, with the current
description and all unresolved questions.

Describe the current idea, not the conversation history. Preserve unrelated
content in an existing document.

Use sections that fit the idea. Include:

- The current idea, its purpose, and its main elements. Add a concrete example
  when useful.
- A summary of settled decisions and their reasons, separate from proposals and
  working assumptions.
- The complete current design tree, with the question records defined above.
  Preserve all known questions and useful alternative branches.
- Relevant facts and source links. Separate evidence from interpretation.
- A summary of open questions, incomplete research, deferred choices, and
  important trade-offs.

The design tree is the source of truth for question status. Generate the summary
sections from it and refresh them whenever the tree changes. If a summary
conflicts with the tree, correct the summary.

Revise the idea itself as your understanding improves. Do not only add answers
below an outdated description. Record important changes of direction when their
reasons would otherwise become unclear.

After each round, briefly report what changed. Normally show only the current
round's questions and a short change report rather than the full document or
tree. Show the full tree if the user requests it. Follow the complete-post rules
above for a chat-only document.

Develop the concept unless the user requests implementation, a formal
specification, or an execution plan. If they do, finish this workflow first,
following the update rules above. Then switch to the requested work, using a
relevant skill if one exists.
Permission to document the idea is not permission to implement or publish it.

## Finish with a useful result

Finish when both conditions apply:

- The idea is clear enough for the user's purpose.
- Each important question in the design tree is settled, covered by a recorded
  working assumption, explicitly deferred, or blocked by a deferred
  prerequisite.

Also finish if the user asks you to stop.

Do not discard unanswered questions without notice. Do not add minor branches
only to extend the discussion.

Follow "Maintain the idea document" for the final update. Link to the final
version, or post it in full if the document is chat-only.

Use the simplest format that captures the result. Include these items when
relevant:

- A clear statement of the idea and its purpose.
- Its main elements and a concrete example.
- The reasons and trade-offs for the proposed or chosen direction.
- Distinct alternatives worth retaining.
- Working assumptions and who adopted each one.
- Deferred, blocked, and unresolved questions.
- The smallest useful next exploration or experiment.

Present your recommendation as a recommendation, not as a user decision. If the
discussion remains exploratory, give clear alternative ideas. Explain what would
help the user choose between them.
