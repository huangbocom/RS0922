##  在实际工作中，FM和MF哪个应用的更多，为什么
答: MF只能考虑User和Item的特征，但是现实的工作场景中，一个问题包含的特征维度用很多。正好FM可以解决多个特征维度的预测问题。
FM典型的应用是CTR,应用场景是回归问题，采用least square error，和二分类问题，采用回归+sigmod
## FFM与FM有哪些区别？
答：FFM在FM的基础上引入了Feild，把相同性质的特征归于同一个field
对于FM算法，每个特征有唯一的一个隐向量表示，这个隐向量被用来学习与其他任何特征之间的影响
对于FFM算法，每个特征会有几个不同的隐向量。
FM是FFM的特例。

## DeepFM相比于FM解决了哪些问题，原理是怎样的
答：DeepFM是神经网络+FM,比如FM+DNN, 
FM的缺点：特征组合，如果是高阶的，计算量很大，不可商用， 一般是2阶特征组合。
DeepFM是一种end-to-end的结构，无须特征工程。
所以DeepFM是既考虑低阶（1阶+2阶），又能考虑到高阶特征
DeepFM中有从上到下有，sparse Features, Dense Embedding, FM + Deep Layer, 再就是Output
Sparse Feature层是数据特征抽取层，实际的数据肯定是多个稀疏的。
Dense Embedding，就是把Sparese--> dense, 并且维度仍然是K.
FM，是对一阶和二阶的处理，
Deep Layer是做多层全连接级联。
Output Unit，最后是把FM+Deep的输出做一个sigmod级联。

#### Surprise工具中的baseline算法原理是怎样的？BaselineOnly和KNNBaseline有什么区别？
答： baseline算法的原理是：基于统计的基准预测线打分
bui = u + bu + bi
bu是用户对整体的偏差，bi是商品对整体的偏差。u是整体的平均率
BaseLineOnly就是BaseLine的基础应用。
KNNBaseline是更强调它是KNN的特点，是User_based还是item_based. 只是在需要考虑到用户打分的偏差的场景下，偏差计算时基于baseline，


## 基于邻域的协同过滤都有哪些算法，请简述原理
答：主要是IterCF和UserCF,
UserCF，是先找到和目标用户兴趣相似的用户集合，然后找到用户u对物品i的相似度，等价于去找它的K个邻居对物品i的兴趣度，最后为用户生成推荐列表。
ItemCF, 是先计算物品之间相似度，用户u对物品i的兴趣度，等价于物品i的K个邻居物品，受到用户u的兴趣度，最后为用户u生成推荐列表。
有一些算法：KNNBaseline，KNNBasicWithMeans, KNNBaiscWithZScore。
主要区别在于要考虑不同的因素：
KNNBasicWithMeans考虑的是用户v的平均兴趣
KNNBaseline考虑的是用户打分的偏差，偏差计算时使用baseline
KNNBasicWithZScore考虑的是用户v的平均兴趣及标准差。
