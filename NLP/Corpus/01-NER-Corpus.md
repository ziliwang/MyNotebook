## 简介
NER标注语料十分稀少，大部分开源的模型训练均来源于Wikipedia。本文简单汇总了目前对Wikipedia语料进行NE标注的方法。Wikipedia文本是种标注性文本，构成单位为page，page分为以下情况：
1. article page
2. 目录page
其中article page为主要的信息页，其中包含外链，内链，分类等各种信息。
## 基于人工标注方法（2008）
文章来源于Nothman, J., Curran, J. R., & Murphy, T. (2008). Transforming Wikipedia into named entity training data. In Proceedings of the Australasian Language Technology Association Workshop 2008 (pp. 124-132).
其主要标注途径：
1. 对所有article进行分类（LOC, ORG, PER, MISC， UNK， DAB， NON）。
2. 对article文档进行分句。
3. 通过链接获取所连接文档的类别来对标注字符串。
4. 选择包含NEs的句子作为语料。

该论文采用CONLL类别标准(LOC, ORG, PER, MISC) 。
该论文需要对article进行手工标注。
## 基于类别分类方法（2008）
Richman, A. E., & Schone, P. (2008). Mining wiki resources for multilingual named entity recognition. Proceedings of ACL-08: HLT, 1-9.
该方法通过对英文类别描述做标注，决定实体类型。在非英文下，通过两途径对其他语言实体进行标注：
1. 搜索title英文内链，根据英文内链的实体类型来对非英文实体进行确定。
2. 通过类别内链来对非英文实体进行判别。
## 基于freeBASE
Al-Rfou, R., Kulkarni, V., Perozzi, B., & Skiena, S. (2015, June). Polyglot-NER: Massive multilingual named entity recognition. In Proceedings of the 2015 SIAM International Conference on Data Mining (pp. 586-594). Society for Industrial and Applied Mathematics.
1. 基于freebase对article进行实体分类。
2. 对于缺失的链接采取过采样方法进行补充标注。
