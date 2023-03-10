# MIT6.006
一点一点学习Algorithm中，记录学习的过程

2023/1/5
今天完成了ps1中的代码部分的作业，主要是练习双向链表doble_linked_list的一些基本操作
特别需要注意的点是在链表为特殊情况下的处理，比如链表为空，链表只有一个节点等情况下，删除，插入会需要注意head和tail的处理；以及插入删除时节点的next,prev的变化处理。

2023/1/6
lec03 video 
sorting,用递归的方法实现的选择排序selection-sort,插入排序insertion-sort,归并排序merge-sort

lec04 notes
Direct-Access-Array 
Hashing (smaller dynamic direct access array)(还未深入理解，有待继续学习）


2023/1/22
ps2  Problem 2-2 Sorting Sorts   selection-sort insert-sort merge-sort

(a)Selection-sort:因为在a情况下，数据结构D支持的set_at(i,x)操作在最坏情况下花费Θ(nlogn)的时间，而get_at(i)操作在最坏情况下只花费Θ(1)的时间，
因而在排序的时候set_at(i,x)操作是影响运行时间的关键项，所以需要选择一个执行set_at(i,x)操作最少的排序算法。
在选择排序、插入排序、归并排序三种排序算法中，选择排序所执行的set_at(i,x)操作是最少的。因为它确认好每一轮排序时的最大值（或最小值）的位置后，
对这个最大值（或最小值）只执行一次set_at(i,x)操作,与这个值交换位置的值也只执行一次set_at(i,x)操作，即每一轮排序时在最坏情况下执行Ο(1)次set_at(i,x)操作;
因而选择排序在最坏情况下执行Ο(n)次set_at(i,x)操作;则选择排序下，D排好序所需时间为Θ(n^2*logn)
而其他两种排序算法:插入排序在每一轮排序时执行2i次set_at(i,x)操作，因而选择排序在最坏情况下执行Ο(n^2)次set_at(i,x)操作，则选择排序下D排好序所需时间为Θ(n^3*logn);
归并排序在每一轮排序中最坏情况下执行Ο(n)次set_at(i,x)操作，共有logn轮排序，因而选择排序在最坏情况下执行Ο(nlogn)次set_at(i,x)操作，则归并排序下D排好序所需时间为Θ((nlogn)^2);
综上，选择 选择排序，执行时间为Θ(n^2*logn)。

(b)由题意可得，需要选择一个执行比较操作最少的算法。
选择排序和插入排序都需要执行Ο(n^2)比较操作，而归并排序需要执行Ο(nlogn)次比较操作；
因而选择 归并排序，执行时间为Θ(n(logn)^2)

(c)由题意可得，A是有部分值出于排好序的状态，需要选择一个执行交换操作最少且能够利用部分数据已排好序的特点的算法。
假设A有i个数据被打乱顺序，剩余n-i个数据没有被打乱顺序。则选择排序需要执行Ο(n)次交换操作，插入排序需要执行Ο(n^2)次
交换操作,归并排序需要执行Ο(nlogn)次交换操作,与A的有序度无关。
综上，选择 选择排序，执行时间为Θ(nloglogn)


2023/1/25
Ps2-3 Friend Finder


算法：
第一步：Πcard先跳到岛的中心，如果Datum恰好在这个位置，则找到Datum,结束寻找；否则用tracking device 判断Datum的方位，N or S，执行第二步；

第二步：根据第一步的方位判断，Πcard跳到岛相应方位的端头（比如如果第一步方位判断为N，则跳到岛的最北端；为S，则跳到岛的最南端），执行第三步；

第三步：在岛的一端，比如N端，如果Datum恰好在这个位置，则找到Datum,结束寻找；如果Datum不在，那么一开始tracking device的方位提示肯定是指向岛的另一端S，根据tracking device的这个方位提示下按0,1,2,4,8,16…… 底为2的指数增长去跳到相应的位置；然后执行第四步；

第四步：如果Datum恰好在这些2的指数位置被找到，则找到Datum,结束寻找；否则直到tracking device的方位提示又再次指示为N端，此时Datum所在的离最近的岛的N端的k km位置在2^(logk(向下取整)) ~ 2^((logk(向下取整))+1) 之间，在从岛的N端到tracking device再次提示为N端时访问的位置之间所访问的位置的数量为(logk(向下取整)+1)（对数底为2），然后执行第五步；

第五步：此时确定k在2^(logk(向下取整)) ~ 2^((logk(向下取整))+1) 之间，然后使用二分查找法，找到Datum,结束查找；使用二分查找确定Datum所在的k位置需要访问（log(2^(logk(向下取整)))）+1个位置，即(logk(向下取整))+1个位置；

综上，这个算法所需要访问的位置的个数最坏情况为2+((logk)(向下取整)+1)+ ((logk)(向下取整)+1),即4+2*((logk)(向下取整))，即O(log k) locations。

2023/1/26
ps2-4  MixBookTube.tv Chat 

这道题暂时只想了一下思路，具体的结果还没有再继续思考下去
（因为发现6.006对于初学者来说还是不太适合作为数据结构与算法的入门课，它更偏向于算法，大多数题主要考察算法思路，实际动手写代码的部分并不多，
而我基础的数据结构代码部分本来就练习得少，并且对于代码部分非常不熟练，所以还是转而选择CS61B作为数据结构与算法的入门课，希望它给我的学习体验会好些吧）

思路部分：
viewers 需要一个数据结构体，

typedef struct viewer
{

  int ID;
  bool banned;
  
}viewer

ID代表viewer，banned 代表viewer是否被ban;

messages
typedef struct message
{

  time t;
  
  int ID;
  
  string m;  
  
}message
t代表message被发送时的时间，ID代表message是被哪个viewer所发送的，m代表message的内容；


chat room，The chat consists of a linear stream of messages；
也就是说chat room是由线性的messages流组成的，初步设想chat room 所需的数据结构应该是一个链表（link list）型的结构，
因为它是线性的，且需要实时插入新的被发送的messages,或者实时删除被ban的viewer所发送的messages;


对于screen所显示的k条messages，即recent(k),从chat room 中获取 the k most recent not-deleted messages;


以上就是暂时关于ps2-4的一点思考。
