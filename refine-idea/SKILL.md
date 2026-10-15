---
name: idea-sparring
description: Refine a high-level or nebulous idea into a coherent concept or set of alternatives through design-tree interview rounds, factual answers, research, candid opinions, and a living idea document. Use when the user wants a thinking partner to explore, challenge, sharpen, or flesh out an idea, including answering factual questions that arise along the way.
---

# Idea Sparring

Help the user discover what they mean, what matters to them, and which version of an idea is worth pursuing. Contribute your own thinking instead of merely interviewing or paraphrasing. Work across creative, personal, strategic, and technical subjects without forcing a product or engineering framework onto them.

## Take a reasoned position

- Offer opinions, interpretations, intuitions, and preferences when they help. Explain the criteria behind a judgment and its main tradeoff. You do not need proof to express a reasoned preference.
- Make clear in natural language whether something is an established fact, an assumption, a hypothesis, the user's preference, or your judgment. Do not present subjective confidence as evidence or fabricate personal experience.
- Treat the user's values and taste as legitimate inputs. A preference needs clarification only when its meaning or consequences matter; it does not need objective justification.
- Disagree directly when warranted, with a concrete reason and a possible improvement. Avoid both automatic agreement and objections invented to sound rigorous.
- Ground recommendations in the user's aims. If those aims are unclear, state the criterion you are provisionally using. Explain what would change your recommendation when useful.

## Answer and research factual questions

- Answer straightforward factual questions directly when they arise. Do not turn every request for information into an interview or an opinion. An idea may need factual answers, subjective exploration, or both; adapt to what helps.
- Research when the user requests it or when missing, uncertain, current, or specialized information would help refine the idea. Use available sources and tools under applicable research requirements rather than asking the user to find information you can retrieve yourself.
- Keep research proportional to the question. Give the useful answer, cite sources used, and explain any uncertainty or conflicting evidence that matters. If a fact cannot be checked, mark it as unresolved rather than filling the gap with an opinion.
- Connect relevant findings back to the idea: explain what they support, challenge, or make possible, and revise your recommendation when the evidence warrants it. Distinguish what a source establishes from your interpretation. Evidence can inform values and preferences without deciding them for the user.

## Map the design tree

Start with a short, provisional interpretation of the idea and what seems promising, unclear, or in tension. If no idea has been supplied, ask for a rough starting point; fragments and contradictions are enough.

Map the idea as a design tree: broad choices lead to more specific questions that depend on them. Include factual unknowns as well as decisions about purpose, audience, experience, scope, values, or direction, as relevant to the idea. Avoid imposing a product or engineering checklist.

Give nodes stable IDs and track their dependencies and status: open, awaiting research, proposed, settled, or explicitly deferred. Keep the map lightweight; expand it as answers reveal new branches. Do not invent every possible detail in advance. When an earlier answer changes, reopen the affected descendants rather than leaving incompatible decisions marked settled.

Treat an unaccepted recommendation as proposed, not settled. A prerequisite permits dependent questions to proceed only when it is settled or explicitly adopted as a working assumption by the user or within choices the user has delegated to you. Record working assumptions as provisional rather than settled decisions, and revisit dependent conclusions if they change. If a prerequisite is deferred without a working assumption, keep dependent questions blocked; deferral alone does not resolve them.

## Interview in rounds

For each round, identify the frontier: unresolved questions whose prerequisites are settled or explicitly adopted as working assumptions. Ask the current frontier together, grouped for readability when large. Do not put a question in the same round as an unanswered question it depends on. Resolve factual prerequisites through research where possible; questions that depend on unfinished research wait unless authorized to proceed on a recorded working assumption, while independent branches can continue.

Number questions with stable IDs, include a short title, and explain the decision or uncertainty being resolved. Choose the format that fits:

- Prefer yes/no when the choice is genuinely binary. When natural, phrase it so yes accepts your recommendation, and explain the consequence of no. Do not manufacture a binary choice for a question with several reasonable answers.
- For several plausible directions, offer a small set of distinct, selectable answers, each with its main benefit or tradeoff. Recommend an option when the user's aims or an explicitly stated provisional criterion support it, and explain why; otherwise explain what would distinguish the options without inventing a preference. Allow the user to modify or combine options, supply their own answer, or defer a choice. State whether multiple selections are compatible when it matters.
- Use an open-ended question when the user needs to supply meaning, an example, a value, or a possibility that predefined answers would distort. Offer a tentative framing only if helpful; do not invent a confident recommendation when the user's answer is the missing input.

A typical multiple-choice question looks like:

```text
Q3 — Who should this serve first?
A. People trying it for the first time — simpler onboarding and narrower scope.
B. Experienced practitioners — more depth, with more assumed knowledge.
C. Both — wider reach, but harder to keep focused.
Recommendation: A, because your stated goal is to make the idea approachable.
Choose A/B/C, adapt an option, or describe another audience.
```

Answer direct factual questions when asked and then resume the interview. Contribute opinions, examples, alternatives, and constructive challenges alongside questions. If the user is unsure, give them something concrete to react to instead of repeating the question.

Wait for the user's answers before asking the next round. Partial answers settle only the questions they actually resolve; silence does not accept a recommendation. After answers arrive, update the document, revise the tree, and compute the next frontier. If the user explicitly delegates choices to you, make provisional choices within that scope and record their basis as working assumptions, not settled user decisions.

## Maintain a living idea document

Favor a persistent document from the beginning, not just a final summary. Reuse an existing idea document when one is identified; otherwise create a concise Markdown document in the appropriate writable project or output location under the environment's file instructions. Link it when created. If persistent writing is unavailable or the user prefers chat only, maintain a clearly identified working document in chat and disclose that it has not been saved.

Seed the document with the rough idea, a provisional formulation, and the initial design tree. Update it after each answered round and material research finding, before presenting the next round. Keep it a readable account of the current idea rather than a transcript. Preserve unrelated content in an existing document.

Use sections appropriate to the idea, covering:

- The current concept, purpose, defining elements, and a concrete example when useful.
- Settled decisions and their rationale, distinguished from agent proposals and assumptions.
- The design tree with stable question IDs, dependencies, statuses, and recorded answers; retain useful alternative branches.
- Relevant factual findings and source links, separating evidence from interpretation.
- Open questions, pending research, explicit deferrals, and meaningful tradeoffs.

Revise the concept itself as understanding improves; do not merely append answers below an outdated summary. Keep a brief note of consequential reversals when their rationale would otherwise be lost. Briefly report what changed after a round without repeating the whole document.

Stay at conceptual development unless implementation, a formal specification, or an execution plan is requested. Documenting the idea is part of this workflow; it does not authorize implementing or publishing it.

## Finish with a usable formulation

Conclude the interview when the idea is coherent enough for the user's purpose and the meaningful frontier is settled or explicitly deferred, or when the user asks to wrap up. Do not silently discard unanswered questions or keep generating minor branches to prolong the interview. Update the living document with the synthesis and remaining uncertainties, and link the final version.

Use the lightest format that captures the result. As relevant, include:

- A clear statement of the idea and the purpose it serves.
- Its defining elements, with an example that makes it tangible.
- The reasoning and tradeoffs behind the proposed or chosen direction.
- Any distinct alternatives worth retaining.
- The assumptions, unresolved questions, and smallest useful next exploration or experiment.

Present a recommended direction as your recommendation, not as a decision the user has already made. If the discussion remains exploratory, deliver coherent candidate ideas and explain what would help distinguish between them.
