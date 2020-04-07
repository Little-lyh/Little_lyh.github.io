---
layout: post
title: 五大基本算法之动态规划算法 DP-dynamic programming
date:  2020-4-7 11:34:15 +0800
categories: [DB]
tags: [data-struct, block-chain, sh]
published: true
---

## dynamic programming

动态规划(dynamic programming)是运筹学的一个分支，是求解决策过程(decision process)最优化的数学方法。

20世纪50年代初美国数学家R.E.Bellman等人在研究多阶段决策过程(multistep decision process)的优化问题时，提出了著名的最优化原理(principle of optimality)，吧多级阶段过程转化为了一些列单阶段问题，利用各个阶段之间的关系，逐个求解，创立了解决种类过程优化问题的新方法——动态规划。

并于1957年出版了他的名著《Dynamic Programming》，这也是该领域的第一本著作。



## 基本概念

动态规划是通过拆分问题，定义问题状态和状态之间的关系，使得问题能够以地推(或者说分治)的方法去解决。



## 基本思想

动态规划算法的基本思想和分治法类似，也是将待求解的问题分解为若干个子问题(阶段)，按照顺序求解子阶段，前一个子问题的解，为后裔子问题的求解提供了有用的信息。在求解任一子问题时，列出各种可能的局部解，通过决策保留哪些有可能达到最优的局部解依次解决各个子问题，最后一个子问题就是初始问题的解。

由于动态规划解决的问题多数有重叠子问题的特点，为了减少重复计算，对于每个子问题只解一次，将其不同阶段的不同状态保存在一个二维数组中。

与分治法最大的差别是：适合于用动态规划法求解的问题，经过分解得到的子问题往往不是互相独立的(即下一个子阶段的求解是建立在上一个子阶段的基础上，进行进一步的求解)。



## 适合的情况

能够采用动态规划求解的问题一般要具有3个性质：

+ 最优化原理：如果问题的最优解所包含的子问题的解也是最优的，就成该问题具有最优子结构，即满足最优化原理。
+ 无后效性：即某阶段状态一旦确定，就不收这个状态以后决策的影响。也就是说，某状态以后的过程不会影响以前的状态，只与当前状态有关。
+ 有重叠子问题：即子问题之间是不独立的，一个子问题在下一阶段决策中可能被多次使用到。



## 使用动态规划求解的基本步骤

上面的话如果没有动态规划的基础，很难看懂，但是也能看出一些基本的信息。

**首先是拆分问题**，我认为就是根据问题的可能性，把问题划分为一步一步这样就可以通过递推或者递归来实现。

> 这一步，我认为是比较重要的。动态规划中有一类问题就是从后往前推导，有时候我们很容易知道如果只有一种情况是，最佳的选择应该怎么做，然后根据这个最佳的选择往前一步一步进行倒推，到的前一步的最佳选择。

**然后就是定义问题状态和状态之间的关系**，我的理解是掐面拆分的步骤之间的关系，用一种量化的形式表现出来，类似于高中学的推导公式，因为这个式子很容易可以使用程序写出来，也可以说对程序比较亲和。

**最后两段我的理解是**：我们将最优解保存下来，为了往前倒推时能够使用前一步的最优解，在这个过程中难免有一些相比于最优解查的解，此时我们应该放弃，只保存最优解，这样我们每一次都把最优解保存下来，大大降低了实践复杂度。



## 动态规划与递归

动态规划是自底向上，递归树是自顶向下。



## 什么是[自定向下]

递归，一般来说是从上向下延伸，都是从一个规模较大的原问题比如说是f(20)，向下主键分解规模，直到f(1)和f(2)触底，然后珠层返回答案，这就叫[自顶向下]。

```cpp
int Fibonacci(size_t n){
	if(n==1||n==2){
        return 1;
    }
    return Fibonacci(n-1)+Fibonacci(n-2);
}
```

> 虽然递归看上起很简洁，实际上有很大的限制，计算的数值稍微大一点，基本就算不出来了。



## 什么是[自底向上]

反过来，我们直接从最下，最简单，问题规模最小的f(1)和f(2)开始网上推

，直到推导我们想要的答案f(20)，这就是动态规划的思路，这也是为什么动态规划一般都脱离了递归，而是由循环迭代来完成计算。

```cpp
int Fibonacci(int N){
    vector<int> db(N+1,0);
    dp[1]=dp[2]=1;
    for(int i=3;i<=N;i++){
        dp[i]=dp[i-1]+dp[i-2];
    }
    return dp[N];
}
```



## 状态转移方程

这里，引出「状态转移方程」这个名词，实际上就是描述问题结构的数学形式：

可见列出「状态转移方程」的重要性，它是解决问题的核心。

很容易发现，其实状态转移方程直接代表着暴力解法。

千万不要看不起暴力破解，动态规划问题最困难的就是写出状态转移方程。



## 便于理解的例子

### 题目

![这里写图片描述](https://img-blog.csdn.net/20170715221117648?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzMwOTg3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](https://img-blog.csdn.net/20170715222316773?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzMwOTg3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](https://img-blog.csdn.net/20170715222600560?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzMwOTg3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](https://img-blog.csdn.net/20170715222733332?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzMwOTg3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 采用递归方法求解

```cpp
int cut(int []p,int n){
    if(n==0){
        return 0;
    }
    int q=Interger.MIN_VALUE;
    for(int i=1;i<=n;i++){
        q=Math.max(q,p[i-1]+cut(p,n-i));
    }
    return q;
}
```

递归的思路其实和回溯法是一样的，遍历所有解空间但是这里和上面斐波那契数列的不同之处在于，在每一层都进行了一次最优解的选择，q=Math.max(1,p[i-1]+cut(p,n-i));这个端语句就是最优解选择，这里上一层的最优解和下一层的最优解相关。



#### 采用备忘录版本求解[自顶向下]

```cpp
int cutMemo(int[] p){
    int []r=new int[p.length+1];
    for(int i=0;i<p.length;i++){
        r[i]=-1;
    }
    return cut(p,p.length,r);
}
int cut(int []p,int n,int []r){
    int q=-1;
    if(r[n]>=0){
        return r[n];
    }
    if(n==0){
        q=0;
    }else{
        for(int i=0;i<=n;i++){
            q=Math.max(q,cut(p,n-i,r)+p[i-1]);
        }
    }
    r[n]=q;
    
    reurn q;
}
```



#### 自底向上的动态规划求解

```cpp
int buttom_up_cut(int []p){
    int []r=new int[p.length+1];
    for(int i=1;i<=p.length;i++){
        int q=-1;
        for(int j=1;j<=i;j++)
            q=Math.max(q, p[j-1]+r[i-j]);
        r[i]=q;
    }
    return r[p.length];
}
```





### 题目二

> 7
>
> 3	8
>
> 8	1	0
>
> 2	7	4	4
>
> 4	5	2	6	5

从上到下选择一条路，使得经过的数字之和最大，路径上的每一步只能王坐下或者右下走。



#### 递归解法

我们在这个题目可以看出每走第n行第m列时有两种后续：向下或者向右下。

由于最后一行我们是确定的，当做边界条件，所以我们自然而然想到递归求解

```cpp
int getMax(){
    vector<vector<int>> D;
    int n;
    int i=0;
    int j=0;
    int maxSum=getMaxSum(D,n,i,j);
    return maxSum;
}
int getMaxSum(vector<vector<int>> D,int n,int i,int j){
    if(i==n){
        return D[i][j];
    }
    int x=getMaxSum(D,n,i+1,j);
    int y=getMaxSum(D,n,i+1,j+1);
    return max(x,y)+D[i][j];
}
```

> 存在问题：
>
> 仔细观察，上面的解答过程时间复杂度相当大，因为他对于有的数字的解进行了多次的重复计算。
>
> ```
> 7
> 3	8
> 8	1(2)	0
> 2	7(3)	4(3)	4
> 4	5(4)	2(6)	6(4)	5
> ```

所以我们便是自然想到是都可以吧每次结果保存下来，那么复杂度就会打大大降低。那么这就是**动态规划的最核心的思想**。



#### 动态规划解法

```cpp
for(int i=n-1;i>=1;i--){
    for(int j=1;j<i;j++){
        maxSum[i][j]=Math.max(maxSum[i+1][j],maxSum[i+1][j+1]);
    }
}
```



## 分类

动态规划一般可以划分为线性动态规划、区域动态规划、树形动态规划、背包动态规划。

举例：

**线性动态规划：**拦截导弹，合唱队形，挖地雷，建学校，剑客对决等

**区域动态规划：**式子合并，加分二叉树，统计单词个数，炮兵布阵等

**树形动态规划：**贪吃的九头龙，二分查找树，聚会的欢乐，数字三角形等；

**背包动态规划：**01背包问题，完全背包问题，分组背包问题，二维背包问题，装箱问题，挤牛奶等。



**应用实例**：

最短路径问题，项目管理，网络流优化等。