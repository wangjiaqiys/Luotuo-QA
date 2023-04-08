# 驼铃QA : 仅使用6B语言模型的阅读理解系统

孙骜, 李鲁鲁

这是一个简短的repo，完成之后会被合并到CamelBell完整的项目中

## 引言

本文是对于我们驼铃QA模型，一个基于GLM-6B的中文阅读理解模型，的简短技术汇报。在语言模型的垂类应用中，关于一段特定文本的理解和QA是一个很重要的问题，有以下原因: 1. 大量涉密企业、或者是金融企业并不能够把自己的机密文档输入到公开的API中。2. 训练或者tuning一个语言模型的成本仍然很高，对于很多专业领域，如果能够在回答问题之前给定一段特定上下文的文本，可以使得模型有快速适应特定垂直领域的能力。3. 给定的文本的事实可以被用户控制，而不像语言模型的输出完全依赖模型的记忆和概率模型，可以让模型在对话中给出更符合事实的回答。

所以在驼铃的这个实验中，我们试图让一个6B的模型，通过Low Rank Adaptation的微调，争取实现对一段特定长度（大约200-600字）的阅读理解的能力。这对于我们之后完成更大的文本的搜索-QA系统，是一个重要的初步尝试。

注意到，完成一个中文的阅读理解模型是不琐碎的。1、过往的基于阅读理解的中文QA没有较大样本量的数据，很少有超过10万量级别的数据。2、类似CoQA的提问方式较为单一，有时候在连续对话中，会省略完整的问题，这往往与真实人类的对话习惯不一致。 3、相比于使用较为复杂的结构，我们希望去探究类似GPT这样的纯Decoder模型的性能。因为这种模型在一个真实的文档QA系统中，往往会有更好的表现。

由于CoQA数据集上的性能已经接近饱和，对于本个工作，我们主要希望研究三点 

1、区别于研究连续对话的机器人，我们将CoQA中的短问题延展为了更为准确的问题。并且在首先的测试中，我们对模型进行了单次提问的测试，我们希望消除连续提问对于性能的影响。我们希望测试相比于GPT这样的大模型，一个较小的模型是否能够完成阅读理解并针对文中的信息的提问进行回答。这对于后期制作更有专业性的模型更为重要。

2、对于CoQA的本来问题，我们进一步对每一个问题进行了5个增广，我们期望更多样的问题，能够带来模型对于数据集外的阅读理解有更好的性能。

3、对于连续对话的阅读理解，基于我们补全的问题，我们希望设计一个架构，模型能够先输出补全的问题，再对补全的问题进行回答。我们期望这种系统相比于直接回答短问题的系统能够表现出更好的性能。

所有的工作包括测试代码、训练代码以及数据将在清理后逐步开源。希望能够帮助中文大语言模型开源社区的发展。

## 相关工作

## CoQA数据集的增广

## 训练

### 连续问答的训练。

## 实验

### Metric

### 单次问答实验

### 连续问答实验