---
title: "Using Seq2Seq Models to Assemble Reasoning Modules for VQA (Fall 2020)"
collection: projects
permalink: /project/using_seq2seq_models
---
{% include base_path %}

Large Visual Question Answering (VQA) models suffer from problems such as overfitting and bias. One approach to combat these problems is to split the task of answering a question into smaller reasoning operations, also referred to as functional programs, so that smaller models can be used for each operation. Recent datasets such as GQA and CLEVR also explicitly annotate training questions with the functional programs necessary to answer them. We use these annotations as ground truth supervision and investigate the use of sequence- to-sequence (Seq2Seq) models to generate functional programs directly from VQA questions. We evaluate a variety of models and compare their performance to a semantic parser which has been used in previous work. We demonstrate that our Seq2Seq models are able to regress functional programs that are close to the ground truth annotations, suggesting that they can be used in future work involving modular VQA

<iframe src="/files/using_seq2seq_models.pdf" width="100%" height="500" frameborder="no" border="0" marginwidth="0" marginheight="0">
</iframe>
