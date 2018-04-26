# OPTIMIZATION AS A MODEL FOR FEW-SHOT LEARNING

Ravi, Sachin and Larochelle, Hugo. Optimization as a model for few-shot learning. In International Conference on Learning Representations 
(ICLR), 2017.

文章学习的是一个模型参数的更新函数或更新规则。它不是在多轮的episodes学习一个单模型，而是在每个episode学习特定的模型。具体地，采用LSTM表达meta learner，
用其状态表达目标分类器的参数的更新，最终学会如何在新的分类任务上，对分类器网络(learner)进行初始化和参数更新。
