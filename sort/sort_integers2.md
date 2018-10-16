[题目链接](https://www.lintcode.com/problem/sort-integers-ii/description)

# Description
```
Given an integer array, sort it in ascending order. Use quick sort, merge sort, heap sort or any O(nlogn) algorithm.
Have you met this question in a real interview?  
Example
Given [3, 2, 1, 4, 5], return [1, 2, 3, 4, 5].
重点：快速排序、归并排序、堆排序（面试问排序基本就是这三个，理解并背熟）
用快速排序、归并排序、堆排序都实现一遍
```
# 快速排序：
```
快速排序算法是一种基于交换的高效的排序算法，它采用了 分治法 的思想：
从数列中取出一个数作为基准数（枢轴，pivot）。
将数组进行划分(partition)，将比基准数大的元素都移至枢轴右边，将小于等于基准数的元素都移至枢轴左边。
再对左右的子区间重复第二步的划分操作，直至每个子区间只有一个元素。
```
![](https://github.com/only-you/-/blob/master/picture/quicksort.png)

# 归并排序
[blog](https://blog.csdn.net/jianyuerensheng/article/details/51262984)
```
（1）申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列
（2）设定两个指针，最初位置分别为两个已经排序序列的起始位置
（3）比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置
（4）重复步骤3直到某一指针达到序列尾
（5）将另一序列剩下的所有元素直接复制到合并序列尾
一趟归并需要将数组 a[]中相邻的长度为h的有序序列进行两两归并.并将结果放到temp[]中，这需要将待排序列中的所有记录扫描一遍，因此耗费O(n)，而又完全二叉树的深度可知，整个归并排序需要进行（log2n）次，因此总的时间复杂度为O(nlogn)，而且这是归并排序算法中最好、最坏、平均的时间性能。
由于归并排序在归并过程中需要与原始序列同样数量的存储空间存放归并结果以及递归时深度为log2n的栈空间，因此空间复杂度为O(n+logn).
另外，对代码进行仔细研究，发现merge函数中有if (a[i] < a[j]) 的语句，说明它需要两两比较，不存在跳跃，因此归并排序是一种稳定的排序算法。
也就是说，归并排序是一种比较占内存，但却效率高且稳定的算法。
```

![](https://github.com/only-you/-/blob/master/picture/mergesort.png)


# 堆排序
[blog](https://www.cnblogs.com/chengxiao/p/6129630.html)
```
堆排序利用了大根堆（或小根堆）堆顶记录的关键字最大（或最小）这一特征，使得在当前无序区中选取最大（或最小）关键字的记录变得简单。
（1）用大根堆排序的基本思想
① 先将初始文件R[1..n]建成一个大根堆，此堆为初始的无序区
② 再将关键字最大的记录R[1]（即堆顶）和无序区的最后一个记录R[n]交换，由此得到新的无序区R[1..n-1]和有序区R[n]，且满足R[1..n-1].keys≤R[n].key
③由于交换后新的根R[1]可能违反堆性质，故应将当前无序区R[1..n-1]调整为堆。然后再次将R[1..n-1]中关键字最大的记录R[1]和该区间的最后一个记录R[n-1]交换，由此得到新的无序区R[1..n-2]和有序区R[n-1..n]，且仍满足关系R[1..n-2].keys≤R[n-1..n].keys，同样要将R[1..n-2]调整为堆。
……
直到无序区只有一个元素为止。

（2）大根堆排序算法的基本操作：
①建堆，建堆是不断调整堆的过程，从len/2处开始调整，一直到第一个节点，此处len是堆中元素的个数。建堆的过程是线性的过程，从len/2到0处一直调用调整堆的过程，相当于o(h1)+o(h2)…+o(hlen/2) 其中h表示节点的深度，len/2表示节点的个数，这是一个求和的过程，结果是线性的O(n)。
②调整堆：调整堆在构建堆的过程中会用到，而且在堆排序过程中也会用到。利用的思想是比较节点i和它的孩子节点left(i),right(i)，选出三者最大(或者最小)者，如果最大（小）值不是节点i而是它的一个孩子节点，那边交互节点i和该节点，然后再调用调整堆过程，这是一个递归的过程。调整堆的过程时间复杂度与堆的深度有关系，是lgn的操作，因为是沿着深度方向进行调整的。
③堆排序：堆排序是利用上面的两个过程来进行的。首先是根据元素构建堆。然后将堆的根节点取出(一般是与最后一个节点进行交换)，将前面len-1个节点继续进行堆调整的过程，然后再将根节点取出，这样一直到所有节点都取出。堆排序过程的时间复杂度是O(nlgn)。因为建堆的时间复杂度是O(n)（调用一次）；调整堆的时间复杂度是lgn，调用了n-1次，所以堆排序的时间复杂度是O(nlgn) [2] 

　堆排序是一种选择排序，整体主要由构建初始堆+交换堆顶元素和末尾元素并重建堆两部分组成。其中构建初始堆经推导复杂度为O(n)，在交换并重建堆的过程中，需交换n-1次，而重建堆的过程中，根据完全二叉树的性质，[log2(n-1),log2(n-2)...1]逐步递减，近似为nlogn。所以堆排序时间复杂度一般认为就是O(nlogn)级。
```
![](https://github.com/only-you/-/blob/master/picture/heapsort.png)
