学习笔记

### 1、树、二叉树、二叉搜索树：  

#### 1.1、树(Tree)： 

元素的集合；树有多个节点(node)，用以储存元素。某些节点之间存在一定的关系，用连线表示，连线称为边(edge)。边的上端节点称为父节点，下端称为子节点。树像是一个不断分叉的树根。每个节点可以有多个子节点(children)，而该节点是相应子节点的父节点(parent)。树有一个没有父节点的节点，称为根节点(root)，没有子节点的节点称为叶节点(leaf)，树中节点的最大层次被称为深度（depth）。

#### 1.2、二叉树(binary)

二叉树(binary)是一种特殊的树。二叉树的每个节点最多只能有2个子节点。每个节点有一个左子节点(left children)和右子节点(right children)。左子节点是左子树的根节点，右子节点是右子树的根节点。

#### 1.3、二叉搜索树(binary search tree)

二叉搜索树要求：每个节点都不比它左子树的任意元素小，而且不比它的右子树的任意元素大。

二叉搜索树可以方便的实现搜索算法。在搜索元素x的时候，我们可以将x和根节点比较:

1. 如果x等于根节点，那么找到x，停止搜索 (终止条件)
2. 如果x小于根节点，那么搜索左子树
3. 如果x大于根节点，那么搜索右子树

二叉搜索树所需要进行的操作次数最多与树的深度相等。n个节点的二叉搜索树的深度最多为n，最少为log(n)。



高级：栈 stack、队列 queue、双端队列 deque、集合 set、映射 map(hash or map)、etc 

**数组（array）** 
**基础写法**：int a[100]； 
**优点**：直接访问时间复杂度都为O(1)，它可以随机访问任何一个元素，所以它的访问时间非常快 
**缺点**：增加（扩容）和删除数组元素的时候会移动数据，导致插入的操作不是常数级的，而是O（n）的复杂度。

**链表（Linked List）** 

​		为了优化或者是弥补数组的缺陷而设计的。 
**特点**：每个元素有Value、Next，next指向下一个元素，一般用class来定义，只有一个next指针叫单链表，有时		候往前一个指叫它的先前指针(previous)，是双向链表。头指针用head表示，尾指针用tail表示，最后一个元		素next指向空。如果tail指针可以指向head指针，就叫循环链表。 
**优点**：不管是增加还是删除节点，它都没有引起链表的群移操作，也不需要复制元素，挪动元素到新的位置，所以		它的移动和修改的效率非常高，为O（1） 

**缺点**：访问这个链表中的任何一个位置，需要的复杂度为O（n）。 

**跳表**：

​		为了优化或者是弥补链表的缺陷而设计的。 
**优化的中心思想**：升维，或者叫做空间换时间（将一维结构变为二维结构，不仅仅增加一个头指针和尾指针，再增		加一个中指针，可以在中间的中间增加指针。）。
**简单优化**：添加头中尾指针。 
**跳表的思想**：（提高链表线性查找的效率） 在跳表中查询任意数据的时间复杂度就是O(logn)，也就是从最朴素的		原始链表的O(n)的时间复杂度降到了log2n的时间复杂度。
​		增加或删除，导致索引跨度不一，而且维护成本相对较高，每增加或删除一个元素的时候，需要把它的索引都更新一遍。（时间复杂度为logn）。



### 2、堆、二叉堆、图：  

#### 2.1、堆、二叉堆

##### 2.1.1 堆：

堆通常是一个可以被看做一棵树。

**满足两个特性**：

1. 堆中任意节点的值总是不大于(不小于)其子节点的值。 
2. 堆总是一棵完全树。 将任意节点不大于其子节点的堆叫做最小堆或小根堆，而将任意节点不小于其子节点的堆叫做最大堆或大根堆。常见的堆有二叉堆、左倾堆、斜堆、二项堆、斐波那契堆等等。 

##### 2.1.2 二叉堆：

二叉堆是完全二叉树或者是近似完全二叉树。 

二叉堆满足二个特性： 

1. 父结点的键值总是大于或等于（小于或等于）任何一个子节点的键值。 
2. 每个结点的左子树和右子树都是一个二叉堆（都是最大堆或最小堆）。 当父结点的键值总是大于或等于任何一个子节点的键值时为最大堆。当父结点的键值总是小于或等于任何一个子节点的键值时为最小堆。

#### 2.2、图

一种非线性的数据结构。

**图结构构成**

**1.顶点（vertex）：**图中的数据元素

**2.边（edge）：**图中连接这些顶点的线

​		所有的顶点构成一个顶点集合，所有的边构成边的集合，一个完整的图结构就是由顶点集合和边集合组成。图结构在数学上记为以下形式：G=（V,E） 或者 G=（V（G），E（G）），其中 V（G）表示图结构所有顶点的集合，顶点可以用不同的数字或者字母来表示。E（G）是图结构中所有边的集合，每条边由所连接的两个顶点来表示。

   	图结构中顶点集合V（G）不能为空，必须包含一个顶点，而图结构边集合可以为空，表示没有边。

**图的基本概念**

  **1.无向图（undirected graph）**：所有的边都没有方向性。

  **2.有向图（directed graph）**：边是有方向性的。无向图也可以理解成一个特殊的有向图，就是边互相指向对方节点，A指向B，B又指向A。

  **3.混合图（mixed graph）**：一个图结构中，边同时有的是有方向性有的是无方向型的图。在生活中混合图这种情况比较常见，比如城市道路中有些道路是单向通行，有的是双向通行。

 **4.顶点的度**：

​		连接顶点的边的数量称为该顶点的度。顶点的度在有向图和无向图中具有不同的表示。

- 对于无向图，一个顶点V的度比较简单，其是连接该顶点的边的数量，记为D(V)。
- 对于有向图，一个顶点的度有**入度**和**出度**之分。有向图中，一个顶点V的总度便是入度和出度之和，即D(V) = ID(V) + OD(V)。
  - 入度是以该顶点为端点的入边数量， 记为ID(V)。
  -  出度是以该顶点为端点的出边数量， 记为OD(V)。





### 3、最小的 k 个数

输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

示例 1：

输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
示例 2：

输入：arr = [0,1,2,1], k = 1
输出：[0]


限制：

0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000

#### 3.1、解法

1. 快速排序：利用快排思想的快速选择，通过快排切分排好第 K 小的数（下标为 K-1），那么它左边的数就是比它小的另外 K-1 个数。时间复杂度是 O(N)。

   ```
   class Solution {
       public int[] getLeastNumbers(int[] arr, int k) {
           if (k == 0 || arr.length == 0) {
               return new int[0];
           }
           // 最后一个参数表示我们要找的是下标为k-1的数
           return quickSearch(arr, 0, arr.length - 1, k - 1);
       }
   
       private int[] quickSearch(int[] nums, int lo, int hi, int k) {
           // 每快排切分1次，找到排序后下标为j的元素，如果j恰好等于k就返回j以及j左边所有的数；
           int j = partition(nums, lo, hi);
           if (j == k) {
               return Arrays.copyOf(nums, j + 1);
           }
           // 否则根据下标j与k的大小关系来决定继续切分左段还是右段。
           return j > k? quickSearch(nums, lo, j - 1, k): quickSearch(nums, j + 1, hi, k);
       }
   
       // 快排切分，返回下标j，使得比nums[j]小的数都在j的左边，比nums[j]大的数都在j的右边。
       private int partition(int[] nums, int lo, int hi) {
           int v = nums[lo];
           int i = lo, j = hi + 1;
           while (true) {
               while (++i <= hi && nums[i] < v);
               while (--j >= lo && nums[j] > v);
               if (i >= j) {
                   break;
               }
               int t = nums[j];
               nums[j] = nums[i];
               nums[i] = t;
           }
           nums[lo] = nums[j];
           nums[j] = v;
           return j;
       }
   }
   ```

   

2. #### 大根堆(前 K 小) / 小根堆（前 K 大)，使用PriorityQueue

   时间复杂度：*O*(*N**l**o**g**K*)

   ```
   // 保持堆的大小为K，然后遍历数组中的数字，遍历的时候做如下判断：
   // 1. 若目前堆的大小小于K，将当前数字放入堆中。
   // 2. 否则判断当前数字与大根堆堆顶元素的大小关系，如果当前数字比大根堆堆顶还大，这个数就直接跳过；
   //    反之如果当前数字比大根堆堆顶小，先poll掉堆顶，再将该数字放入堆中。
   class Solution {
       public int[] getLeastNumbers(int[] arr, int k) {
           if (k == 0 || arr.length == 0) {
               return new int[0];
           }
           // 默认是小根堆，实现大根堆需要重写一下比较器。
           Queue<Integer> pq = new PriorityQueue<>((v1, v2) -> v2 - v1);
           for (int num: arr) {
               if (pq.size() < k) {
                   pq.offer(num);
               } else if (num < pq.peek()) {
                   pq.poll();
                   pq.offer(num);
               }
           }
           return pq.stream().mapToInt(Integer::intValue).toArray();
       }
   }
   ```

   

3. #### 二叉搜索树也可以 O(NlogK)解决 TopK 问题

   TreeMap的key 是数字，value 是该数字的个数。
   我们遍历数组中的数字，维护一个数字总个数为 K 的 TreeMap：
   1.若目前 map 中数字个数小于 K，则将 map 中当前数字对应的个数 +1；
   2.否则，判断当前数字与 map 中最大的数字的大小关系：若当前数字大于等于 map 中的最大数字，就直接跳过该数字；若当前数字小于 map 中的最大数字，则将 map 中当前数字对应的个数 +1，并将 map 中最大数字对应的个数减 1。

   ```
   class Solution {
       public int[] getLeastNumbers(int[] arr, int k) {
           if (k == 0 || arr.length == 0) {
               return new int[0];
           }
           // TreeMap的key是数字, value是该数字的个数。
           // cnt表示当前map总共存了多少个数字。
           TreeMap<Integer, Integer> map = new TreeMap<>();
           int cnt = 0;
           for (int num: arr) {
               // 1. 遍历数组，若当前map中的数字个数小于k，则map中当前数字对应个数+1
               if (cnt < k) {
                   map.put(num, map.getOrDefault(num, 0) + 1);
                   cnt++;
                   continue;
               } 
               // 2. 否则，取出map中最大的Key（即最大的数字), 判断当前数字与map中最大数字的大小关系：
               //    若当前数字比map中最大的数字还大，就直接忽略；
               //    若当前数字比map中最大的数字小，则将当前数字加入map中，并将map中的最大数字的个数-1。
               Map.Entry<Integer, Integer> entry = map.lastEntry();
               if (entry.getKey() > num) {
                   map.put(num, map.getOrDefault(num, 0) + 1);
                   if (entry.getValue() == 1) {
                       map.pollLastEntry();
                   } else {
                       map.put(entry.getKey(), entry.getValue() - 1);
                   }
               }
               
           }
   
           // 最后返回map中的元素
           int[] res = new int[k];
           int idx = 0;
           for (Map.Entry<Integer, Integer> entry: map.entrySet()) {
               int freq = entry.getValue();
               while (freq-- > 0) {
                   res[idx++] = entry.getKey();
               }
           }
           return res;
       }
   }
   ```

### 4、Hash总结

HashMap基于hashing原理，我们通过put()和get()方法储存和获取对象。当我们将键值对传递给put()方法时，它调用键对象的hashCode()方法来计算hashcode，让后找到bucket位置来储存值对象。当获取对象时，通过键对象的equals()方法找到正确的键值对，然后返回值对象。HashMap使用LinkedList来解决碰撞问题，当发生碰撞了，对象将会储存在LinkedList的下一个节点中。 HashMap在每个LinkedList节点中储存键值对对象。

HashMap可以接受null键值和值。HashMap是非synchronized。

