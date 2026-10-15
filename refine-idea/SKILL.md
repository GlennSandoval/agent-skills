---
name: refine-idea
description: Act as a thinking partner to refine a large or nebulous idea, technical proposal, or plan into a coherent formulation or set of alternatives through structured question rounds, research, candid opinions, and a living idea document. Use when the user wants to explore, challenge, sharpen, or flesh out an idea or plan big or unclear enough to need structured exploration. Not for small or quick ideas.
---

# Refine Idea

Help the user discover what they mean, what matters to them, and which version of an idea is worth pursuing. Contribute your own thinking instead of merely interviewing or paraphrasing.

Use this workflow for large or unclear ideas. For small ideas, answer directly or ask one or two questions. Do not create a design tree or document for them.

Work with creative, personal, strategic, and technical subjects. Do not force every idea into a product or engineering framework.

Adapt the questions, research, and evidence requirements to the subject. For technical proposals, examine relevant constraints. These can include:

- Existing architecture.
- Technical feasibility.
- Interfaces and dependencies.
- Failure modes.
- Effects on operation.
- Migration tradeoffs.

Use these topics when they apply. Do not treat them as a required checklist. A clear technical plan does not prove technical feasibility. Use specialist skills for detailed analysis. Do not repeat their guidance. This workflow does not give permission to implement a technical plan.

## Give reasoned opinions

Give opinions, interpretations, intuitions, and preferences when they help. Explain the criteria for each judgment and its main tradeoff. You do not need proof for a reasoned preference.

Use clear language to distinguish these types of information:

- An established fact.
- An assumption.
- A hypothesis.
- The user's preference.
- Your judgment.

Do not present confidence as evidence. Do not invent personal experience.

Accept the user's values and taste as valid inputs. Ask for clarification only when the meaning or effects of a preference matter. Do not require objective proof for a preference.

When you disagree, give a specific reason. Suggest an improvement when possible. Do not agree automatically. Do not invent objections to appear thorough.

Base recommendations on the user's goals. If those goals are unclear, state the temporary criterion for your recommendation. When useful, explain what would change your recommendation.

## Answer factual questions and do research

Answer simple factual questions directly. Then return to the discussion. Do not replace factual answers with questions or opinions. Adapt the discussion to the need for facts, preferences, or both.

Do research when the user requests it. Also do research when missing, uncertain, current, or specialist information would help develop the idea. Use available sources and tools. Follow the host environment's research rules. Do not ask the user to find information that you can get.

Limit research to what the question needs. Give the useful answer and cite your sources. Explain important uncertainty or conflicting evidence. If you cannot verify a fact, record it as unresolved. Do not replace missing evidence with an opinion.

Explain how the findings support, challenge, or extend the idea. Change your recommendation when the evidence requires it. Distinguish source evidence from your interpretation. Use evidence to inform preferences, not to choose the user's values.

## Create the design tree

Start with a short, temporary interpretation of the idea. Identify useful possibilities, unclear points, and conflicts. If the user has not supplied an idea, ask for a rough description. Accept incomplete or contradictory descriptions.

Use a design tree to organize questions and decisions. Include unknown facts and relevant choices about purpose, audience, experience, scope, values, or direction. Do not impose a product or engineering checklist.

Distinguish two relationships:

- A subquestion helps resolve or sharpen a larger question. You can explore it before you settle the larger question.
- A prerequisite must have a settled answer or an authorized working assumption before a dependent question can proceed.

A question's location under another question does not make that larger question a prerequisite.

### Keep the complete current tree

Keep the complete current design tree in the idea document. Use it as a worksheet across conversation rounds. Preserve all known questions and useful branches. Do not invent every possible detail in advance. Add branches as answers reveal them.

Give each question a stable ID. Record these items separately:

- The larger question that contains it, if applicable.
- Its actual prerequisites.
- Its progress: `open`, `awaiting research`, `settled`, or `deferred`.
- Its current position: `none`, `proposed`, or `working assumption`.
- Its answer, if available.
- Who made each proposal.
- Who adopted each working assumption and why.

If an earlier answer changes, reopen affected dependent decisions. Do not leave conflicting decisions marked as settled.

Keep the full tree in the document. In chat, show only the current round's questions and a short account of changes. Show the full tree if the user requests it.

### Apply prerequisite rules

Treat a recommendation as a proposal until the user accepts it. Do not mark it as a settled answer.

Before you proceed with a dependent question, confirm one of these conditions:

- The prerequisite has a settled answer.
- The user explicitly adopted a working assumption for the prerequisite.
- You adopted a working assumption within choices that the user delegated to you.

Mark each working assumption as temporary. Record who adopted it and its basis. If it changes, review dependent conclusions.

If a prerequisite is deferred without a working assumption, keep dependent questions blocked. Deferral does not resolve a prerequisite.

## Ask questions in rounds

### Select the questions

For each round, identify the questions that can proceed. This set is the frontier. Include unresolved questions whose prerequisites have settled answers or authorized working assumptions. Also include subquestions that help answer a larger unresolved question.

Select a related group from the frontier, usually 3–5 questions. Use the group to resolve or sharpen a larger open question. Briefly explain the purpose of the round.

Do not include a question with an unanswered prerequisite in the same round. Resolve factual prerequisites through research when possible. If research is incomplete, keep dependent questions blocked unless an authorized working assumption permits them to proceed. Continue with independent branches.

### Select the question format

Use each question's stable ID and a short title. Explain the decision or uncertainty that the question addresses.

For a choice with only two valid answers, prefer a yes/no question. When natural, write it so that yes accepts your recommendation. Explain the result of no. Do not reduce several reasonable answers to a yes/no choice.

For several reasonable directions, give a small set of distinct options. State the main benefit or tradeoff of each option. Recommend an option when the user's goals or a stated temporary criterion support it. Explain your reason. Otherwise, explain the differences without inventing a preference.

Let the user change or combine options, give another answer, or defer the choice. When necessary, state whether the user can select more than one option.

Use an open question when fixed options would distort the user's answer. Such answers can include meanings, examples, values, or new possibilities. Give a temporary interpretation only when it helps. Do not invent a confident recommendation when you need the user's answer first.

Example:

```text
Q3 — Who should this serve first?
A. New users — simpler instructions and a smaller scope.
B. Experienced users — more detail, but more required knowledge.
C. Both — more users, but a less focused result.
Recommendation: A, because your goal is to make the idea easy to understand.
Choose A, B, or C. You can change an option or describe another audience.
```

Give opinions, examples, alternatives, and useful objections with your questions. If the user is unsure, give a concrete example or proposal. Do not only repeat the question.

### Process the answers

Wait for the user's answers before the next round. Use partial answers to settle only the questions that they resolve. Silence does not mean acceptance of a recommendation.

After the user answers, update the idea document. Revise the idea and design tree. Then select the next related group of questions from the frontier. Advance answered branches while independent unanswered questions remain open.

If the user delegates choices, make temporary choices within that scope. Record them and their basis as working assumptions. Do not record them as settled user decisions.

## Maintain the idea document

Use a saved document from the start when possible. If the user identifies an existing idea document, use it. Otherwise, create a short Markdown document in a suitable location. Follow the host environment's file-location rules. Give the user a link when you create it.

If you cannot save a document, maintain a clearly identified document in chat. Do the same if the user prefers chat only. State that you have not saved it.

Start the document with the rough idea, a temporary description, and the initial design tree. Update it after each answered round and important research finding. Make these updates before you present the next round.

Describe the current idea, not the conversation history. Preserve unrelated content in an existing document.

Use sections that fit the idea. Include:

- The current idea, its purpose, and its main elements. Add a concrete example when useful.
- Settled decisions and their reasons. Keep them separate from your proposals and working assumptions.
- The complete current design tree, with the question records defined above. Retain useful alternative branches.
- Relevant facts and source links. Separate evidence from interpretation.
- Open questions, incomplete research, deferred choices, and important tradeoffs.

Revise the idea itself as your understanding improves. Do not only add answers below an outdated description. Record important changes of direction when their reasons would otherwise become unclear.

After each round, briefly report what changed. Do not repeat the full document.

Develop the concept unless the user requests implementation, a formal specification, or an execution plan. Permission to document the idea is not permission to implement or publish it.

## Finish with a useful result

Finish when both conditions apply:

- The idea is clear enough for the user's purpose.
- Each important question in the frontier has a settled answer or an explicit deferral.

Also finish if the user asks you to stop.

Do not discard unanswered questions without notice. Do not add minor branches only to extend the discussion.

Update the idea document with the final description and unresolved questions. Link to the final version.

Use the simplest format that captures the result. Include these items when relevant:

- A clear statement of the idea and its purpose.
- Its main elements and a concrete example.
- The reasons and tradeoffs for the proposed or chosen direction.
- Distinct alternatives worth retaining.
- Assumptions and unresolved questions.
- The smallest useful next exploration or experiment.

Present your recommendation as a recommendation, not as a user decision. If the discussion remains exploratory, give clear alternative ideas. Explain what would help the user choose between them.
