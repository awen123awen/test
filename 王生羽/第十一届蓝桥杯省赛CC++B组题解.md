# 第十一届蓝桥杯省赛C/C++B组题解

## A：跑步训练

#### 题目

【问题描述】

小明要做一个跑步训练。初始时，小明充满体力，体力值计为1000010000。如果小明跑步，每分钟损耗

600600的体力。如果小明休息，每分钟增加 300300的体力。体力的损耗和增加都是均匀变化的。

小明打算跑一分钟、休息一分钟、再跑一分钟、再休息一分钟……如此循环。如果某个时刻小明的体力到达 00，他就停止锻炼。

请问小明在多久后停止锻炼。为了使答案为整数，请以秒为单位输出答案。答案中只填写数，不填写单位。

#### 思路

直接模拟（- ~ -）

```c++
int S = 10000;
	int sun = 10, ad = 5;
	
	int t = 0, c = 0;
	bool flag = false;
	while(S > 0){
		if(!flag){
			S -= 10;
			t++;
			c++;
			if(c == 60){
				flag = !flag;
				c = 0;
			}
		}
		else{
			S += 5;
			t++;
			c++;
			if(c == 60) {
				flag = !flag;
				c = 0;
			}
		}
	}
	cout << t << endl;
```

答案：3880

## B：纪念日

#### 题目

【问题描述】

2020 年 7 月 1 日是A组织 成立 99 周年纪念日。 A组织成立于 1921 年 7 月 23 日。请问从 1921 年 7 月 23 日中午 12 时到 2020 年 7 月 1 日中午 12 时一共包含多少分钟？

#### 思路

运用Excel![image-20220212171052485](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220212171052485.png)

### C: 合并检测

#### 题目

【问题描述】

***（敏感字）由 ***（敏感字）引起，最近在 A 国蔓延，为了尽快控制 ***（敏感字），A 国准备给大量民众进病毒核酸检测。然而，用于检测的试剂盒紧缺。为了解决这一困难，科学家想了一个办法：合并检测。即将从多个人（k个）采集的标本放到同一个试剂盒中进行检测。如果结果为阴性，则说明这 k个人都是阴性，用一个试剂盒完成了 k 个人的检测。如果结果为阳性，则说明至少有一个人为阳性，需要将这 k 个人的样本全部重新独立检测（从理论上看，如果检测前k−1k−1个人都是阴性可以推断出第 k 个人是阳性，但是在实际操作中不会利用此推断，而是将 k 个人独立检测），加上最开始的合并检测，一共使用了 k + 1 个试剂盒完成了 k 个人的检测。A 国估计被测的民众的感染率大概是 1%，呈均匀分布。请问 k 取多少能最节省试剂盒？

#### 思路

数学

设总人数为n, 感染率是p, 每次k人，总试剂数sum。

得：sum=⌈n/k⌉+n∗k∗p

导： sum=n∗(0.01∗k2−1)/k2

得： k=10

### D: REPEAT 程序

#### 题目

【问题描述】

附件 prog.txt 中是一个用某种语言写的程序。

其中 REPEAT k 表示一个次数为 k 的循环。循环控制的范围由缩进表达，

从次行开始连续的缩进比该行多的（前面的空白更长的）为循环包含的内容。

#### 思路

栈模拟其循环次数

```c++
#include<bits/stdc++.h>
string s;
stack<int> sk;
int main() {
  freopen("prog.txt", "r", stdin);
  int ci = 1;
  int res = 0;
  while(getline(cin, s)) {
    int pos = 0, len = s.size(), sj, mid;
    while(pos < len && s[pos] == ' ') ++pos;
    sj = pos / 4;
    while(sk.size() > sj) {
      ci /= sk.top();
      sk.pop();
    }
    if(s[pos] == 'R') {
      pos += 7;
      for(mid = 0; pos < len-1; ++pos) mid = mid * 10 + s[pos]-'0';
      sk.push(mid); ci *= mid;
    } else {
      pos += 8;
      for(mid = 0; pos < len; ++pos) mid = mid * 10 + s[pos]-'0';
      res += mid * ci;
    }
  }
  cout << res;
  return 0;
}
```

### E: 矩阵

#### 题目

【问题描述】

把 1 ∼ 2020 放在 2 × 1010 的矩阵里。要求同一行中右边的比左边大，同一

列中下边的比上边的大。一共有多少种方案？

答案很大，你只需要给出方案数除以 2020 的余数即可。

【答案提交】

这是一道结果填空题，你只需要算出结果后提交即可。本题的结果为一个

整数，在提交答案时只填写这个整数，填写多余的内容将无法得分。

#### 思路

深搜

```c++
f[0][0]=1;                                   
    for(int i=0;i<=1010;i++)
        for(int j=0;j<=1010;j++){
            if(i - 1 >= j) //上边一行的数要多于下边一行 才能往下边放                     
            	f[i][j] += f[i-1][j] % 2020;
            if(j)
            	f[i][j] += f[i][j-1] % 2020;
        }
```

### F: 整除序列

#### 题目

【问题描述】

有一个序列，序列的第一个数是 n，后面的每个数是前一个数整除 2，请输出这个序列中值为正数的项。

【输入格式】

输入一行包含一个整数 n。

【输出格式】

输出一行，包含多个整数，相邻的整数之间用一个空格分隔，表示答案。

【样例输入】

20

【样例输出】

20 10 5 2 1

【评测用例规模与约定】

对于 80% 的评测用例，1≤n≤109。1≤n≤109。

对于所有评测用例，1≤n≤1018。1≤n≤1018。

#### 思路

数据范围别出问题就好

```c++
#define ll unsigned long long
...
    vector<ll> a;
	while(n){
		a.push_back(n);
		n >>= 1;
	}
	
	for(int i = 0; i < a.size(); i++) if(a[i] > 0) cout << a[i] << " ";
```

