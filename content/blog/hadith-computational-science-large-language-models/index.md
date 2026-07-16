---
title: "Hadith Computational Science in the Age of Large Language Models"
date: 2026-07-16T14:30:00+01:00
draft: false
summary: "A plain-language reflection on our preprint about hadith computational science, large language models, retrieval-grounded systems, provenance, reproducibility, and scholar-guided evaluation."
tags: ["Hadith", "Large Language Models", "Islamic Computing", "AI", "Preprint", "Research"]
categories: ["Research", "Islamic Computing"]
---

Our new preprint, **Hadith computational science in the age of large language models: a critical narrative review**, is now available online.

The paper is co-authored with Md. Ashraful Haque and is currently available as a **preprint** on Zenodo. It is also under review with a reputed journal. That means the work is public and citable, but it should still be read as a preprint until the journal review process is complete.

You can read the publication page here: [Hadith computational science in the age of large language models](/publication/haque-hadith-computational-science-2026/).

## Why this paper matters

Hadith collections are among the most important sources of Islamic knowledge. They are also complex textual ecosystems. A single hadith may involve Arabic wording, translation, narrator chains, grading, commentary, legal interpretation, historical context, and relationships with other narrations.

This makes hadith a serious challenge for computational systems.

Search engines, databases, embeddings, and large language models can help people find and explore hadith material. But they can also create risk if they remove context, blur provenance, generate unsupported claims, or present uncertain outputs with false confidence.

The central argument of the paper is that progress in hadith computational science should not be measured only by benchmark scores or impressive demonstrations. It should also be measured by the quality of the evidence infrastructure around the system.

In practical terms, that means asking:

- Where did this answer come from?
- Which text, translation, edition, or dataset was used?
- Can the result be reproduced?
- Can a scholar or expert inspect the reasoning path?
- Does the system communicate uncertainty clearly?
- Is it supporting Islamic scholarship, or replacing careful scholarship with a thin technical shortcut?

These questions become more urgent in the age of large language models.

## From keyword search to retrieval-grounded AI

Older hadith search systems often depended on keywords, metadata, or structured databases. These systems are useful, but they can struggle when people search by meaning rather than exact wording.

Large language models and transformer-based systems change the interface. Users can now ask conversational questions, request summaries, compare narrations, and explore themes across collections. Retrieval-augmented generation can also connect a generated answer to specific source passages.

This creates a real opportunity. A well-designed system could help students, researchers, developers, and institutions navigate hadith sources more effectively.

But the opportunity comes with a responsibility.

Hadith is not ordinary text. It is not enough for a model to produce a fluent answer. In Islamic knowledge work, fluency without traceability is dangerous. A system must be able to show what it used, where it came from, and how much confidence users should place in the output.

This is why the paper gives attention to provenance, reproducibility, expert supervision, and evaluation design.

## What we mean by hadith computational science

By **hadith computational science**, we mean the use of computational methods to collect, structure, search, analyse, compare, retrieve, and present hadith-related material.

This can include:

- digitising and structuring hadith collections
- modelling narrator networks and isnad data
- linking hadith to commentary, fiqh, Seerah, and Qur'anic themes
- evaluating hadith search engines
- building multilingual retrieval systems
- using natural language processing for classification or semantic search
- designing AI systems that support Islamic learning and scholarship

The field sits between computer science, Islamic studies, digital humanities, information retrieval, natural language processing, and human-computer interaction.

That interdisciplinary nature is important. A purely technical approach can miss scholarly nuance. A purely manual approach can struggle with scale, multilingual access, and modern search expectations. The best future work will need both technical competence and serious Islamic scholarly input.

## The main concern: trust

Many conversations about AI focus on capability. Can the model answer the question? Can it summarise a text? Can it retrieve the right passage?

For hadith systems, capability is only one part of the problem.

The deeper issue is trust.

A trustworthy hadith AI system should not behave like a black box oracle. It should behave more like a careful research assistant: useful, limited, transparent, and reviewable.

That means it should cite sources. It should preserve context. It should distinguish between text, translation, commentary, grading, and interpretation. It should make it clear when an answer is generated, when it is retrieved, and when expert review is needed.

This also means that evaluation should go beyond whether a system returns a plausible-looking answer. We need evaluation methods that test retrieval quality, source fidelity, hallucination risk, translation reliability, and the ability to support expert review.

## Why scholar-guided evaluation is essential

Hadith work has established scholarly disciplines, methods, and standards. Computational systems should not ignore that.

A model may identify linguistic similarity between two narrations, but that does not mean it has understood legal relevance. It may retrieve a hadith that looks topically related, but that does not mean it has selected the strongest evidence for a ruling. It may summarise a narration fluently, but still flatten important context.

This is why scholar-guided evaluation is essential.

The goal is not to slow down useful technical work. The goal is to make the work reliable enough to be genuinely useful.

For me, this connects to a wider theme I have been thinking about under the term **Islamic Computing**: how Muslims can build technologies that are not merely impressive, but beneficial, trustworthy, and aligned with the responsibilities of the knowledge they handle.

## What developers and researchers can take from the paper

If you are building systems for Islamic knowledge, this paper suggests a few practical principles.

First, design for provenance from the beginning. Do not treat citation and source tracking as features to add later.

Second, separate retrieval from generation. Users should know which parts of an answer came from source documents and which parts were generated by the system.

Third, make outputs inspectable. A scholar, researcher, or advanced user should be able to trace the evidence path.

Fourth, evaluate failure modes. In this domain, a system that is usually right but confidently wrong in sensitive cases can still be harmful.

Fifth, build with humility. AI can support Islamic learning and research, but it should not be positioned as a replacement for scholarship, adab, or careful human judgement.

## In summary

The preprint argues that large language models can reshape hadith computational science, but only if the field develops stronger standards for evidence infrastructure, provenance, reproducibility, and expert supervision.

The future of Islamic AI should not be driven by novelty alone. It should be driven by trust, transparency, scholarly seriousness, and benefit.

Read the preprint details and DOI here: [Hadith computational science in the age of large language models](/publication/haque-hadith-computational-science-2026/).

The Zenodo record is also available directly at [https://zenodo.org/records/21144826](https://zenodo.org/records/21144826).
