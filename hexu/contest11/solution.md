#A 题
===================

>题意：给你一个n*m的矩阵（1<=N,M<=50），我们称这个矩阵为合法矩阵当且仅当这个矩阵的所有的非0元素都可以由同行的一个元素加上同列的一个元素的和构成。问
当前给你的矩阵是否为合法矩阵。

>题解：我们可以用4重循环暴力枚举，复杂度O(N^4).

#B 题
===================

>题意:给你一个m和一个b，代表直线y=-1/M + B。（1<=M<=1000，1<=B<=10000). </P>
      现在要你在线上选一个点，假设这个点的坐标是（X,Y），把这个点，原点（0,0），X轴上的（X,0),y轴上的（Y,0） 一起构成一个矩阵，要你求出矩阵内部所有节
      点的价值。</P>
      PS:点（X,Y）的价值为X+Y。

>题解：因为y轴最大为1000，所以o（b^2）枚举起点和终点，根据直线算出矩形的长，前缀和计算贡献，维护最大值。 

#C 题
====================

>题意：两个操作，add：往栈里push一个数。</p>
      两个操作，add：往栈里push一个数。remove。移除栈顶元素。</p>
      现在要求将数字按1-n顺序移除. 问你需要改动多少次后满足。</p>
      改动：当遇到不满足时，可以将栈内元素排序。</p>

>题解：因为数据太大，所以我们不可能真的去排序，所以当遇到reomve操作，但是栈顶的数不满足要求时，我们就假装我们排了序，++ans，top=0，没了。

#D 题
=====================

>题意:有一张n*m的图，初始有k个地方是灯亮着的，你可以在初始亮灯的地方花费一金币使得任意一行或一列的灯全部点亮，但当你要再次点亮的时候，需要站在原来亮的点
 把上次点亮的那行或列点暗（初始亮的也会暗），求能从左上角到右下角只走亮的点的最小花费
 
>题解：很明显，0,0这个点是不需要花钱的，然后我们从0,0出发，枚举其他的点，当这两个点之间行列差的绝对值小于等于1时，我们可以不花钱就走到。</P>
      当这两个点的差等于2时就要花1金币了。然后我们用迪杰斯特拉来模拟这个松弛过程就可以啦。

#E 题
====================

>题意： 给你一个n条平行于x轴的线段，终点坐标(k,0)，满足l[i]=r[i-1],k∈[l[n],r[n]],</P>
每次可以向右下，右，右上移动且在任何时刻都不能超过包含x坐标的线段的y值,而且也不能走到X轴的下面去，求（0,0）走到（K,0）的方案数。

>题解：事实上，如果不是线段长度太大，我们可以很轻松的写出状态转移方程，但是线段长度太大了，注意到线段的高度是小于等于16的，而且同一条线段下面的
方程转移有共同之处，考虑到这个因素，我们可以用矩阵快速幂来加速这个过程。没了。
        
                                                                 
