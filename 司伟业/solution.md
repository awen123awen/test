## A.卡片
简单模拟取数过程即可，注意题目要求是求最大能够拼出的数字。
答案：3181
## B.直线
先统计竖直和水平直线，其余直线可以用斜率+截距表示，注意精度问题，可使用eps=$10^{-10}$判断相等。
答案：40257
##  C.货物摆放
枚举n的每一个因数，计算n的每个因数的因数和即可
答案：2430
##  D.路径
建图，堆优化dj最短路模板题。
答案：10266837
## E.回路计数
一看n这么小就是爆搜或者状压，仔细分析一下，似乎爆搜O(n!)不大行，考虑状压，我们设$f[i][j]$表示走过的状态为$i$且最后一个走过的点为$j$的方案数，那么
$f[k+(1<<(j-1)][j]=\sum\ f[k][l]~~~(gcd(l,j)=1)$只需要枚举状态上一步位置和下一步位置即可，时间复杂度O($2^n*n^2$)=O($8*10^6$)卡常两秒时限差不多
## F.砝码称重
设$f[i]$表示状态i是否可得，初始$f[0]=1$对于每个砝码，$\left\{\begin{matrix}f[i+w_i]=f[i]\\
f[i-w_i]=f[i]\end{matrix}\right.$由于数组没有负数下标，开map即可。
## G.异或数列
不难想到从最高位开始考虑，
如果最高位只有一个1，那么先手必胜。
如果最高位有偶数个1，那么在这一位上要么双方都是拿偶数个1，要么双方拿奇数个1，异或之后这一位必然相等，所以不管怎么拿这一位上的值必定一样，因此这一位不予考虑，考虑下一位即可。
如果最高位有奇数个1，而且有奇数个0，先手必败，偶数个0，先手必胜
## H.左孩子右兄弟
简单树形dp
## I.括号序列
容易发现我们需要补齐的括号一定是朝左的右括号和朝右的左括号，而且两部分没有交集，因此答案就是左边的匹配数乘右边的匹配数，对于一侧的括号，我们设$f[i][j]$表示前i个括号形成j个配对括号的方案数,转移即可。
## J.分果果
毒瘤dp题，30暴力走人