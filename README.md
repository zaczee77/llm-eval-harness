# LLM eval harness

A small reference eval harness for language model outputs, built by Nirmeet Rao. It turns the lesson of his published research on bias mitigation in generative AI into runnable checks: model outputs need structured scrutiny before anyone trusts them.

The research is published under identifier IJISRT24JUL1248. The notes in the docs folder describe what the paper is about and how its lesson shows up in the products he has built. The demo folder holds a small harness in plain Python with no external packages. It scores a set of fixed sample outputs against three checks: a stereotype language scan, a counterfactual pair consistency check, and a citation presence check.

## The idea in one paragraph

A model output is not good because it reads well. It is good when it survives checks that are written down in advance. This harness writes those checks down for three failure modes that matter in real products: stereotyped language about people, answers that change when only a name or a demographic word changes, and factual claims with no source behind them. Each check is small, explainable, and cheap to run, which is the point. Evaluation that costs more than the call it checks will never run in production.

## The three checks

1. Stereotype scan. Each sample output is scanned against a small lexicon of loaded words and phrases. A hit does not prove bias by itself. It marks the output for human review, the same way a lint warning marks code.
2. Counterfactual pair check. Two prompts that differ only in a name are answered, and the two answers are compared. If one answer carries a stereotype term and the paired answer does not, the pair fails. The model should not change its judgment when only the name changes.
3. Citation check. For prompts that ask a factual question, the answer must carry a citation to a source. A confident answer with no source is flagged, even when it sounds right.

## The demo in this repository

The demo folder contains a small reference demo in plain Python with no external packages. It evaluates six fixed sample outputs, runs the three checks on each, and prints a per case verdict plus a summary. The sample outputs are invented examples written only to exercise the checks. They are not outputs from any real model, and they are not results from the research. The harness shows the shape of the evaluation pattern at the smallest possible scale: fixed cases, written checks, and a readable verdict.

## Where this pattern already runs

The same shape appears in the products Nirmeet has built. PharmFlows, the LLM workflows he shipped at Concordia Pharma, reported serving time errors down 86 percent and cycle time down 30 percent on his resume, and those gains came from structure, validation, and review around the model rather than from more model calls. Paxei, his prior authorization preparation product, designs LLM document parsing and clinical drafts around payer criteria guardrails and human review. In each case the model does the part it is uniquely good at, and the surrounding system carries the rest. Evaluation in the loop is the part that keeps the loop honest.

## What this is not

This repository is not the research paper, and it is not a production evaluation system. It contains no real model outputs, no measured results, and no claims about the paper beyond its topic and its published identifier. The sample outputs and the lexicon are illustrative only. The notes in the docs folder describe the evaluation pattern in general terms and do not claim methods or findings that are not part of the public record.

## Links

1. Portfolio: https://nirmeetrao.com
2. GitHub: https://github.com/Zaczee77
3. LinkedIn: https://www.linkedin.com/in/nirmeet-rao
