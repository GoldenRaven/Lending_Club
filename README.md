# Lending_Club
Lending Club 是美国知名的网贷平台，同时也是世界上最大的P2P平台。本项目对于2007年到2014年的借贷数据来预测预期损失EL。

## 贷款的预期损失Expected Loss
EL = PD * LGD * EAD
Basel 3协议的内部评级法要求商业银行对这三个量使用自己的方法，以更高的精度和准确性来建立模型，得到对三个量的估计。

## 违约概率Probability of Default
对个人贷款数据集用户是否违约建立逻辑回归来进行分类，以分类概率作为违约概率PD。监管者要求PD模型要有可解释性，所以模型的输入都是dummy变量。

## 违约损失Loss Given Default

LGD = 1- RR

取值范围为0到1之间。LGD模型不需要有可解释性，此项目中分类变量用dummy变量，连续变量依然保持为连续变量。分两步来对LGD建模，第一步用逻辑回归来判断RR是否为零，第二步用线性回归来
预测不为零的RR为多少（Beta回归）。将两步的结果相乘即是LGD的预测值。

## 违约风险暴露EAD
EAD模型的目标变量是CCF，即credit convention factor:

CCF = (funded_amnt - tot_rec_prncp) / funded_amnt

CCF基本上是均匀分布的，所以此处用多元线性回归来预测连续的取值，并将结果限定在0到1之间（Beta回归）。
