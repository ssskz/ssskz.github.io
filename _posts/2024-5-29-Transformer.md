---
title: Transformer
commentable: true
Edit: 2024-5-29
mathjax: true
mermaid: true
tags: python
categories: Artificial-Intelligence
description: Transformer is a deep learning model architecture for NLP and other sequence-to-sequence tasks.
---

# What is Transformer

Transformer是一种用于自然语言处理（NLP）和其他序列到序列（sequence-to-sequence）任务的深度学习模型架构，它在2017年由Vaswani等人首次提出。

Transformer架构引入了**自注意力机制**（self-attention mechanism），这是一个关键的创新，使其在处理序列数据时表现出色。

以下是Transformer的一些重要组成部分和特点：

> - **自注意力机制（Self-Attention）**：这是Transformer的核心概念之一，它使模型能够同时考虑输入序列中的所有位置，而不是像循环神经网络（RNN）或卷积神经网络（CNN）一样逐步处理。自注意力机制允许模型根据输入序列中的不同部分来赋予不同的注意权重，从而更好地捕捉语义关系。
> - **多头注意力（Multi-Head Attention）**：Transformer中的自注意力机制被扩展为多个注意力头，每个头可以学习不同的注意权重，以更好地捕捉不同类型的关系。多头注意力允许模型并行处理不同的信息子空间。
> - **堆叠层（Stacked Layers）**：Transformer通常由多个相同的编码器和解码器层堆叠而成。这些堆叠的层有助于模型学习复杂的特征表示和语义。
> - **位置编码（Positional Encoding）**：由于Transformer没有内置的序列位置信息，它需要额外的位置编码来表达输入序列中单词的位置顺序。
> - **残差连接和层归一化（Residual Connections and Layer Normalization）**：这些技术有助于减轻训练过程中的梯度消失和爆炸问题，使模型更容易训练。
> - **编码器和解码器（Encoder and Decoder）**：Transformer通常包括一个编码器用于处理输入序列和一个解码器用于生成输出序列，这使其适用于序列到序列的任务，如机器翻译。

## The structure of Transformer

假设Nx = 6，即Encoder block由6个encoder堆叠而成，图中的一个框代表的是一个encoder的内部结构，一个Encoder是由Multi-Head Attention和全连接神经网络Feed Forward Network构成。如下图所示：

<img src="https://ssskz.github.io/materials/自然语言处理/transformer.png" width="70%">

简略结构如下（每一个编码器都对应上图的一个encoder结构）：

<img src="https://ssskz.github.io/materials/自然语言处理/encoder.png" width="70%">

Transformer的编码组件是由6个编码器叠加在一起组成的，解码器同样如此。所有的编码器在结构上是相同的，但是它们之间并没有共享参数。编码器和解码器的简略结构如下：

<img src="https://ssskz.github.io/materials/自然语言处理/decoder.png" width="70%">

从编码器输入的句子首先会经过一个自注意力层，这一层帮助编码器在对每个单词编码的时候时刻关注句子的其它单词。解码器中的解码注意力层的作用是关注输入句子的相关部分，类似于seq2seq的注意力。原结构中使用到的是多头注意力机制（Multi-Head Attention），我们先从基础——自注意力机制开始讲起：