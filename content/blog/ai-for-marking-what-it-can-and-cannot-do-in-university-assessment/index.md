---
title: "AI for Marking: What It Can (and Cannot) Do in University Assessment"
date: 2025-11-22
author: "Dr Riasat Islam"
summary: "A practical, evidence-based look at how AI can support marking and feedback in higher education without compromising fairness or academic standards."
tags: ["AI in Education", "Assessment", "Higher Education", "LLMs", "Feedback"]
---

Artificial intelligence is now everywhere in higher education, from helping students draft essays to supporting admin tasks. It is natural that universities are asking: **can AI mark assessments**?

The honest answer is: **yes and no**.

There are things AI and automation already do very well, and things that current large language models (LLMs) simply are not built to do reliably enough for high-stakes grading.

## Deterministic vs stochastic: why the difference matters

When we mark, we expect something very simple and very strict: if two students give the same answer, they should get the same mark.

That is a deterministic system: the same input always leads to the same output.

We already have a lot of deterministic automation in assessment, and it has been around for years:

- Autograders for programming tasks  
- Quiz engines that compare student answers with stored correct answers  
- Mathematical question systems that check numeric or algebraic results  
- Simple short-answer marking based on pattern matching or regular expressions  

None of this needs AI. It is just software applying rules we wrote. For well-structured, closed-answer questions, this is reliable and, importantly, reproducible.

Modern LLMs do not work like this.

## Current LLMs are fundamentally stochastic

LLMs such as GPT-style models generate text by predicting the next token based on probability distributions learned during training. In practice, this means:

- Their outputs are shaped by probability and sampling, not fixed rules  
- Even with the same prompt, the same model, and the same settings, you do not always get exactly the same answer  
- Providers can and do update models over time, so the behaviour of "the same" model can drift  

Empirical work has shown this clearly. For example, Chen, Zaharia and Zou evaluated different monthly versions of GPT-3.5 and GPT-4 and found that performance on the same tasks could vary significantly over time, even when prompts were held constant.  


Benchmarks like **HELM (Holistic Evaluation of Language Models)** from Stanford exist precisely because we need systematic ways to track how models behave and change across many tasks and metrics.  


This is a real problem for high-stakes, summative assessment. If a system is non-deterministic from one run to another, and subject to provider updates over time, then we cannot guarantee that identical student work would always receive the same mark.

Regulators and sector bodies are already alert to this. In the UK, the Office for Students and the Quality Assurance Agency (QAA) have both highlighted the risks that generative AI poses to fairness and integrity in assessment, and the need for providers to ensure that their approaches are robust and transparent.  


So for now, **LLMs are not a good fit as fully autonomous markers for summative grading**, especially where marks have serious consequences for progression, graduation or professional accreditation.

## Where AI can genuinely help: feedback, comments and support

That does not mean AI has no place in marking workflows. In fact, there is one area where LLMs are potentially game-changing:

**Feedback.**

A long line of research has shown that feedback, not just grades, is one of the most powerful drivers of learning. Hattie and Timperley’s landmark review found that well-designed feedback can have a large positive effect on achievement, but poor feedback can be unhelpful or even harmful.  


More recently, Winstone and Carless have argued for learning-focused feedback processes that help students actively use feedback, rather than just receive it passively.  


The problem is that high-quality, personalised feedback is time-consuming, especially with large cohorts.

This is where LLMs can be powerful assistants rather than autonomous judges. For example:

- Drafting inline comments on code, essays or worked solutions  
- Producing summary feedback aligned with a rubric  
- Suggesting alternative explanations of a concept when a student seems confused  
- Helping maintain a consistent tone and structure across markers  

There is already emerging empirical work exploring this. Jauhiainen and Garagorry Guerra investigated how ChatGPT-4 could evaluate and provide feedback on students’ open-ended responses using structured prompting and a RAG framework. They found that alignment with teacher judgements could be reasonable with well-designed criteria and human oversight.  


Other pilots internationally converge on the same finding: using LLMs to help draft feedback, with humans making final decisions, can save time while improving richness and consistency.  


## A realistic position: AI as support, not as the marker of record

Putting this together, a pragmatic position looks like this:

- For deterministic assessment tasks (coding tests, quizzes, numeric problems, tightly constrained short answers), continue using traditional automated marking systems. They are rule-based, predictable and auditable.  
- For open-ended work (essays, reports, portfolios), LLMs should not be the final marker. Their stochastic nature and shifting behaviour make them unsuitable for high-stakes grading on their own.  
- For feedback on almost any type of work, LLMs can be genuinely useful as drafting tools when guided by rubrics, exemplars and clear prompts, with human markers always in the loop.

In short:

**Let software handle what is deterministic. Let AI draft, not decide, where human judgement is required.**

## What universities should do next

1. **Be explicit about where automation is already used.**  
   Students and staff should know how quizzes, coding tasks and structured questions are auto-marked.

2. **Develop local patterns for AI-assisted feedback.**  
   Build shared prompt templates for each discipline, informed by existing marking criteria.

3. **Keep a human in the loop for all summative decisions.**  
   AI can draft comments, but humans must review and finalise.

4. **Be transparent with students.**  
   Many universities, including Edinburgh, stress the importance of explaining how AI tools are used.  
   

5. **Invest in AI literacy for staff and students.**  
   Both groups need to understand capabilities, risks and ethical issues.  
   

## Conclusion

The real promise of AI in assessment is not to replace human markers, but to amplify their capacity to give rich, timely and meaningful feedback.

Deterministic automation will continue to handle right-or-wrong questions. That relies on software engineering, not “intelligence”.

Generative AI, meanwhile, is strongest when used to support human judgement, not replace it. With clear workflows and proper oversight, LLMs can reduce workload and improve feedback quality without compromising fairness or academic standards.

---

## References

Chen, L., Zaharia, M., & Zou, J. (2023). *How is ChatGPT’s behavior changing over time?* arXiv. https://arxiv.org/abs/2307.09009

Hattie, J., & Timperley, H. (2007). The power of feedback. *Review of Educational Research, 77*(1), 81–112. https://doi.org/10.3102/003465430298487

Higher Education Policy Institute & Kortext. (2025). *Virtual Control: HEPI-Kortext annual student survey on generative AI.* (Referenced in: Adams, R. (2025, Feb 26). UK universities warned to stress-test assessments as 92% of students use AI. *The Guardian.*)

Jauhiainen, J. S., & Garagorry Guerra, A. (2024). Generative AI in education: ChatGPT-4 in evaluating students’ written responses. *Innovations in Education and Teaching International.* https://doi.org/10.1080/14703297.2024.2422337

Jauhiainen, J. S., & Garagorry Guerra, A. (2024). Evaluating students’ open-ended written responses with LLMs: Using the RAG framework. *Advances in Artificial Intelligence and Machine Learning, 4*(4), 3097–3113.

Liang, P., Bommasani, R., Newman, B., et al. (2023). Holistic evaluation of language models. *Transactions on Machine Learning Research.* https://crfm.stanford.edu/helm

Office for Students. (2023). *Artificial intelligence and the regulation of higher education.* Office for Students.

Quality Assurance Agency for Higher Education. (2023). *QAA response to the Department for Education’s consultation on generative artificial intelligence in education.*

University of Edinburgh. (2024). *Using generative AI in your work: Guidance for staff.* University of Edinburgh Information Services.

Winstone, N., & Carless, D. (2019). *Designing effective feedback processes in higher education: A learning-focused approach.* Routledge.
