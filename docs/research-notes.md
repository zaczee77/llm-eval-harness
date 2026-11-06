# Research notes: bias mitigation in generative AI

## The paper

Nirmeet Rao published research on bias mitigation in generative AI, under identifier IJISRT24JUL1248. The topic is the problem of language models producing outputs that carry stereotyped or uneven judgments about people, and what can be done about it before those outputs reach a user.

This file is a set of notes on the problem and the evaluation pattern it points to. It does not reproduce the paper, and it does not claim methods, measurements, or findings beyond what is in the public record. What it records is the lesson that runs through the work: outputs need structured scrutiny before anyone calls them good.

## Why bias is an evaluation problem first

A biased output is usually fluent. It reads like a good answer, which is exactly why it is dangerous. The failure is not in the grammar. It is in the judgment the sentence carries, and that judgment only shows up when the output is compared against something: a counterfactual version of the same prompt, a second answer about a different group, or a source the claim is supposed to rest on.

That makes bias mitigation an evaluation problem before it is a training problem. A team that cannot measure the failure cannot tell whether a fix worked. The first artifact in any serious mitigation effort is therefore a set of written checks, run the same way every time, with a verdict a human can read and argue with.

## Three checks that carry the lesson

The demo in this repository implements three checks. Each one corresponds to a way bias actually shows up in model outputs.

### 1. Stereotype language scan

Some outputs carry bias in plain words: a role described with a loaded adjective, a group summed up with a fixed trait, a person reduced to a single story. A lexicon scan looks for those words and phrases. It is a blunt instrument. It will miss subtle cases, and it will flag innocent uses. Its value is not precision. Its value is that it is cheap, explainable, and always on. A flag from this check is a prompt for human review, not a verdict, and the lexicon is a living list that the team updates as it learns.

### 2. Counterfactual pair consistency

Take a prompt, change only a name or a demographic word, and ask again. If the answer changes in a way the prompt change cannot justify, the model is carrying a judgment about the person, not about the question. This is the most direct test of the idea that the same work should get the same judgment whoever does it. In the demo, two performance review prompts differ only in the name, and the pair fails when one review carries a stereotype term the other does not. The check is symmetric: it does not matter which answer carries the term. What matters is that the pair disagrees.

### 3. Citation presence for factual claims

Bias is not only about people. A model that states a fact with no source is asking to be trusted on tone alone, and tone is where uneven judgments hide. For prompts that ask a factual question, the demo requires a citation to a source. A confident answer with no citation fails the check even when it sounds right. This is the same citation discipline that sits at the center of Txvni, his AI deal workspace, where every answer is expected to point to the source material it rests on.

## How the lesson shows up in his products

The evaluation pattern is not abstract for Nirmeet. It is how his products are built.

PharmFlows, the LLM workflows he shipped at Concordia Pharma, reported serving time errors down 86 percent and cycle time down 30 percent on his resume. Those gains came from structure, validation, and review around the model rather than from more model calls. An unchecked model in a pharmacy workflow is a patient safety risk, so the checks are the product, not an afterthought.

Paxei, his prior authorization preparation product, designs LLM document parsing and clinical drafts around payer criteria guardrails and human review. The guardrails are written rules about what the model may and may not conclude, and the human review is the final check. The same shape appears here: write the rule, run the check, let a person decide.

His ephe platform, a Model Context Protocol platform for agent tooling, treats tool contracts as a product surface and context as a budget. The matching idea for evaluation is that check contracts are a product surface too. A check that is written down, versioned, and run on every output is a contract with the user about what good means.

## What good evaluation looks like in practice

Four habits make the difference between evaluation that works and evaluation that is theater.

1. Checks are written down before the outputs are judged. A check invented after seeing the answer is an excuse, not a test.
2. Checks are cheap enough to run every time. An evaluation suite that costs more than the call it checks will be skipped under pressure, and pressure is when it matters most.
3. Every failure names its reason. A verdict without a reason cannot be fixed, argued with, or learned from.
4. A human owns the final call. Checks flag. People decide. The harness in this repository prints verdicts for a person to read, not to obey.

## Limits of these notes

These notes describe the evaluation pattern in general terms. They do not reproduce the paper, its method, or its results. The sample outputs in the demo are invented examples written only to exercise the checks, and the lexicon is illustrative. Nothing here is a measured result from the research or from any product.

## Links

1. Portfolio: https://nirmeetrao.com
2. GitHub: https://github.com/Zaczee77
3. LinkedIn: https://www.linkedin.com/in/nirmeet-rao
