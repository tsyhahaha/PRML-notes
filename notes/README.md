# Bayes classifier

### 贝叶斯公式

后验概率的计算公式（bayes rule）

$$
p(y|x)=\frac{p(x|y)p(y)}{p(x)}
$$

全概率公式

$$
p(x)=\sum_ip(x|y_i)p(y_i)
$$

### 最小错误率决策

给定观测值 $$x$$，预测其类别为 $$c$$ 的错误率为

$$
P(error|x)=1-P(Y=c|x)
$$

因而，最小错误率决策等价于最大后验概率决策，判别规则：

$$
\hat{y}=\argmax_c P(x|Y=c)P(Y=c)
$$

该公式只适合两种相互影响的随机变量，其中某一个在另一个影响下的判别。

### 最小风险决策

引入损失函数/代价函数，为不同的判别结果赋予不同的代价。期望风险定义为：

$$
\begin{aligned}
R(\hat{y})&=\int L(\hat{y},y)p(x,y)dxdy\\ 
&=\int(\int L(\hat{y},y)p(y|x)dy)p(x)dx\\
&=\int R(\hat{y}|x)p(x)dx\\
&=E_x[R(\hat{y}|x)]
\end{aligned}
$$

由于预测的类别是离散的，因此条件风险可重写为：

$$
R(\hat{y}|x)=\sum_{y=1}^C L(\hat{y},y)P(Y=y|x)
$$

将样本 x 分类为类别 c 的条件风险为：

$$
R(\hat{y}=c|x)=\sum_{y=1}^C L(c,y)P(Y=y|x)
$$

即类别 c 的损失，通过后验概率加权之和。决策规则：

$$
\hat{y}=\argmin_c R(c|x)
$$

容易得出，损失函数为 0-1 损失时，最小风险决策等价于最小错误率决策。

#### 引入拒识

分类器对某些样本可以拒绝给出决策。引入拒识代价 $$L_r$$，此时的损失函数为：

$$
f(x) =
\left\{
\begin{aligned}
&0, &y=\hat{y}\\
&L_s, &y\ne \hat{y} \\
&L_r, &reject
\end{aligned}
\right.
$$

损失函数反而简化了，此时判别为 c 的条件风险为：

$$
R(c|x)=
L_s(1-P(c|x)), c=1,2,...,C
$$

若对某个类别，x 的条件风险小于拒识代价，则拒绝判别为该类别，反之则按照最小风险决策即可。

### 贝叶斯最优分类器

以最小风险决策作为决策依据的分类器，称之为贝叶斯最优分类器。然而上述判别器都依赖于：已知后验概率分布，而现实中并不易得。

因此，在大多数情况下需要估计后验概率。生成式分类器，通过直接估计联合分布 $$p(x,y)$$ 来计算后验概率，往往是通过估计先验概率 $$p(y)$$ 和类条件概率 $$p(x|y)$$ 得到的；判别式分类器，则是直接估计后验概率 $$p(y|x)$$。







































