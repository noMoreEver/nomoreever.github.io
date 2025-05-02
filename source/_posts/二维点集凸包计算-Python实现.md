---
title: 二维点集凸包计算 -- Python实现
date: 2025-05-02 17:51:08
tags: ['图形算法']
---

# 二维点集凸包计算 -- Python实现
> 代码地址https://github.com/noMoreEver/computational-geometry
> 参考：《计算几何-算法与应用》第一章

## 问题定义
**二维凸包定义**: 平面的一个子集S被称为是“凸”的，当且仅当对于任意两点p, q ∈ S，线段 pq 都完全属于S。
凸包问题可以转换为：
给定平面点集 P = { p1, …, pn }，通过计算从 P 中选出若干点，它们沿顺时针方向依次
对应于 CH(P)的各个顶点。
input = 平面上一组点：p1, p2, p3, p4, p5, p6, p7, p8, p9
output = 凸包的表示：p4, p5, p8, p2, p9

![](1746102980.png)

## 代码思路
如何判断三个点P1, P2, P3是否为凸包：对向量(P2 - P1)和向量(P3 - P1)进行<u>向量叉乘</u>
伪代码如下所示：
```
算法 CONVEXHULL(P)
输入：平面点集 P
输出：由 CH(P)的所有顶点沿顺时针方向组成的一个列表
1. 根据 x-坐标，对所有点进行排序，得到序列 p1, …, pn
2. 在 Lupper 中加入 p1和 p2（p1在前）
3. for (i← 3 to n)
4. do在 Lupper 中加入 pi
5. while (Lupper中至少还有三个点，而且最末尾的三个点所构成的不是一个右拐)
6. do将倒数第二个顶点从 Lupper 中删去
7. 在 Llower中加入 pn和 pn-1（pn在前）
8. for (i← n-2 downto 1)
9. do在 Llower中加入 pi
10. while (Llower中至少还有三个点，而且最末尾的三个点所构成的不是一个右拐) 
11. do将倒数第二个顶点从 Llower中删去
12. 将第一个和最后一个点从 Llower中删去
（以免在上凸包与下凸包联接之后，出现重复顶点）
13. 将 Llower联接到 Lupper 后面（将由此得到的列表记为 L）
14. return(L)
```
## 运行结果
该算法复杂度为O(nlogn), 实现可见https://github.com/noMoreEver/computational-geometry。

![](1746093955.png)

性能测试如下：
| Point Num |       Time Usage      |
| - | -|
|     20    | 0.0025811195373535156 |
|    200    |  0.025527238845825195 |
|    2000   |   0.301830530166626   |
|   20000   |   2.6785905361175537  |
