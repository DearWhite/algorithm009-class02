学习笔记
### 1、一维数据结构：  
基础：数组 array(string)、链表 linked list 
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



### 2、盛水最多的容器、爬楼梯

#### 2.1、盛水最多的容器

容纳的水量是由两个指针指向的数字中较小值∗指针之间的距离决定，关键点：Math.min(height[l], height[r]) * (r - l)，ans = Math.max(ans, area)。 

#### 2.2、爬楼梯

爬楼梯问题转换为斐波那契数列问题f(n)=f(n-1)+f(n-2)



### 3、三数之和、爬楼梯

#### 3.1、三数之和

**解题思路**： 

- 暴力法搜索：三层循环。时间复杂度为 O(N^3)，可通过双指针动态消去无效解来优化效率。 
- 双指针法铺垫： 先将给定 nums 排序，复杂度为 O(NlogN)。 
- 双指针法思路： 固定 3 个指针中最左（最小）数字的指针 k，双指针 i，j 分设在数组索引 (k, len(nums))两端，通过双指针交替向中间移动，记录对于每个固定指针 k 的所有满足 nums[k] + nums[i] + nums[j] == 0 的 i,j 组合： 当 nums[k] &gt; 0 时直接break跳出：因为 nums[j] &gt;= nums[i] &gt;= nums[k] &gt; 0，即 3 个数字都大于 0 ，在此固定指针 k 之后不可能再找到结果了。 当 k &gt; 0且nums[k] == nums[k - 1]时即跳过此元素nums[k]：因为已经将 nums[k - 1] 的所有组合加入到结果中，本次双指针搜索只会得到重复组合。 i，j 分设在数组索引 (k, len(nums))两端，当i &lt; j时循环计算s = nums[k] + nums[i] + nums[j]，并按照以下规则执行双指针移动： 当s &lt; 0时，i += 1并跳过所有重复的nums[i]； 当s &gt; 0时，j -= 1并跳过所有重复的nums[j]； 当s == 0时，记录组合[k, i, j]至res，执行i += 1和j -= 1并跳过所有重复的nums[i]和nums[j]，防止记录到重复组合。 
  - 复杂度分析： 
    - 时间复杂度 O(N^2)：其中固定指针k循环复杂度 O(N)，双指针 i，j 复杂度 O(N)。 
    - 空间复杂度 O(1)：指针使用常数大小的额外空间。

#### 3.2、爬楼梯

假设你正在爬楼梯，需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶，你有多少种不同的方法可以爬到楼顶呢？

**解题思路**： 

1. 暴力法算法：

   将会把所有可能爬的阶数进行组合，也就是 1 和 2 。而在每一步中我们都会继续调用 climbStairsclimbStairs 这个函数模拟爬 11 阶和 22 阶的情形，并返回两个函数的返回值之和。
   $$
   climbStairs(i,n)=(i+1,n)+climbStairs(i+2,n)
   $$
   其中 i定义了当前阶数，而 n定义了目标阶数。

   ```
   public class Solution {
       public int climbStairs(int n) {
           climb_Stairs(0, n);
       }
       public int climb_Stairs(int i, int n) {
           if (i > n) {
               return 0;
           }
           if (i == n) {
               return 1;
           }
           return climb_Stairs(i + 1, n) + climb_Stairs(i + 2, n);
       }
   }
   ```

   **复杂度分析**

   - 时间复杂度：O(2^n)，树形递归的大小为 2^n 。
   - 空间复杂度：O(n)，递归树的深度可以达到 n。

2. 记忆化递归算法

   将每一步的结果存储在 memomemo 数组之中，每当函数再次被调用，我们就直接从 memomemo 数组返回结果。在 memomemo 数组的帮助下，我们得到了一个修复的递归树，其大小减少到 nn。

   ```
   public class Solution {
       public int climbStairs(int n) {
           int memo[] = new int[n + 1];
           return climb_Stairs(0, n, memo);
       }
       public int climb_Stairs(int i, int n, int memo[]) {
           if (i > n) {
               return 0;
           }
           if (i == n) {
               return 1;
           }
           if (memo[i] > 0) {
               return memo[i];
           }
           memo[i] = climb_Stairs(i + 1, n, memo) + climb_Stairs(i + 2, n, memo);
           return memo[i];
       }
   }
   ```

   **复杂度分析**

   - 时间复杂度：O(n)，树形递归的大小可以达到 n。

   - 空间复杂度：O(n)，递归树的深度可以达到 n。

     

3. 动态规划算法

   第 i 阶可以由以下两种方法得到：在第 (i-1)(i−1) 阶后向上爬1阶。在第 (i-2)(i−2) 阶后向上爬 2阶。所以到达第 i阶的方法总数就是到第 (i−1) 阶和第(i−2) 阶的方法数之和。

   ​		令 dp[i]dp[i] 表示能到达第 ii 阶的方法总数：dp[i]=dp[i-1]+dp[i-2]

   ```
   public class Solution {
       public int climbStairs(int n) {
           if (n == 1) {
               return 1;
           }
           int[] dp = new int[n + 1];
           dp[1] = 1;
           dp[2] = 2;
           for (int i = 3; i <= n; i++) {
               dp[i] = dp[i - 1] + dp[i - 2];
           }
           return dp[n];
       }
   }
   ```

   **复杂度分析**

   - 时间复杂度：O(n)*O*(*n*)，单循环到 n*n* 。

   - 空间复杂度：O(n)*O*(*n*)，dp*d**p* 数组用了 n*n* 的空间。

     

4. 斐波那契数算法

   ​		*F**i**b*(*n*)=*F**i**b*(*n*−1)+*F**i**b*(*n*−2)

   以 11 和 22 作为第一项和第二项的斐波那契数列中的第 n*n* 个数，也就是说 Fib(1)=1*F**i**b*(1)=1 且 Fib(2)=2*F**i**b*(2)=2。

   ```
   public class Solution {
       public int climbStairs(int n) {
           if (n == 1) {
               return 1;
           }
           int first = 1;
           int second = 2;
           for (int i = 3; i <= n; i++) {
               int third = first + second;
               first = second;
               second = third;
           }
           return second;
       }
   }
   ```

   **复杂度分析**

   - 时间复杂度：O(n)*O*(*n*)，单循环到 n*n*，需要计算第 n*n* 个斐波那契数。
   - 空间复杂度：O(1)*O*(1)，使用常量级空间。

   ​		

### 4、栈、队列、优先队列、双端队列

#### 4.1、栈和队列的实现与特性

##### 4.1.1、栈

一种先进后出的线性表。

**栈的常用操作：**

- 判断栈是否为空、是否已满
- 入栈、出栈操作
- 获取栈顶元素
- 获取栈的大小

**栈的使用场景**

- 表达式计算
- 递归（斐波那契数列）
- 括号匹配

##### 4.1.2、队列

​			**队列（queue）是只允许在一端进行插入操作，而在另一端进行删除操作的线性表。是一种先进先出（First in First Out）的线性表，简称FIFO。允许插入的一端称为队尾，允许删除的一端称为队头。**

队头(Front)：允许删除的一端，又称为队首。

队尾(Rear)：允许插入的一端。

空队列：不含任何元素的空表。

**常用操作：**

- InitQueue(Q)：初始化队列，构造一个空队列Q。
- QueueEmpty(Q)：判队列空，若队列Q为空返回true，否则返回false。
- EnQueue(Q, x)：入队，若队列Q未满，将x加入，使之成为新的队尾。
- DeQueue(Q, x)：出队，若队列Q非空，删除队头元素，并用x返回。
- GetHead(Q, x)：读队头元素，若队列Q非空，则将队头元素赋值给X。

**队列类型**	

1. 顺序队列（基于数组实现）

   （1）队头不动，出队列时队头后的所有元素向前移动。缺陷：操作是如果出队列比较多，要搬移大量元素。

   （2）队头移动，出队列时队头向后移动一个位置。

   ​		如果还有新元素进行入队列容易造成假溢出。

   ​		假溢出：顺序队列因多次入队列和出队列操作后出现的尚有存储空间但不能进行入队列操作的溢出。
   ​		真溢出：顺序队列的最大存储空间已经存满二又要求进行入队列操作所引起的溢出。

2. 循环队列

   **把队列的这种头尾相接的顺序存储结构称为循环队列。**

   如何判断此时的队列究竟是空还是满呢？

   - 设置一个标致变量flag，当front==rear，且flag=0时时为队列空，当front==rear，且flag=1时为队列满。
   - 当队列空时没条件就是front=rear，当队列满时，我们修改其条件，保留一个元素空间。

3. 链式队列（基于单链表实现）

   特殊的单链表，只在单链表上进行头删尾插的操作

   

##### 4.1.3、优先队列

**优先队列**的基础是最大堆/最小堆，是用来维护一组元素构成的集合S的数据结构，每一个元素都有一个相关的值，称之为`key`。基于二叉堆实现，优先指的是按某种优先级优先出列而不是先入先出。

**最大优先队列，无论入队顺序，当前最大的元素优先出队。**

**最小优先队列，无论入队顺序，当前最小的元素优先出队。**

一个最大优先队列支持如下操作：

- **MAXIMUM(pQueue)**：得到pQueue里面key值最大的元素
- **EXTRACT-MAX(pQueue)**：得到pQueue里面key值最大的元素，并将这个元素从优先队列里面删除
- **INSERT**(pQueue , E)：在pQueue里面插入一个新的元素E
- **INCRESED-KEY(pQueue , POS , NEWKEY)**：将pQueue里面位置POS的元素key值设为NEWKEY

最小优先队列支持如下操作：

- **MINIMUM(pQueue)**：得到pQueue里面key值最小的元素
- **EXTRACt-MIN(pQueue)**：得到pQueue里面key值最小的元素，并将这个元素从优先队列里面删除
- **INSERT(pQueue , E)**：在pQueue里面插入一个新的元素E
- **DECRESED-KEY(pQueue , POS , NEWKEY)**：将pQueue里面位置POS的元素key值设为NEWKEY

##### 4.1.4、双端队列Double-ended queue

双端队列 Double-ended queue，简称为Deque，和队列的操作方式出列同名。双端队列(缩写为deque) 是一种抽象数据类型，它概括了一个队列，其中的元素可以从前(头) 或后(尾) 添加或删除（前端与后端都支持插入和删除操作的队列）。因此也经常被称为首尾链表。

**常用方法 ：**

| 方法                                    | 描述                                                         |
| :-------------------------------------- | :----------------------------------------------------------- |
| boolean add(object)                     | 此方法在此双端队列的末尾插入指定的元素。                     |
| void addFirst(E e)                      | 此方法将指定的元素插入此双端队列的前面。                     |
| void addLast(E e)                       | 此方法在此双端队列的末尾插入指定的元素。                     |
| void clear()                            | 此方法从此双端队列中删除所有元素。                           |
| ArrayDeque clone()                      | 此方法返回此双端队列的副本。                                 |
| boolean contains(Object o)              | 如果此双端队列包含指定的元素，则此方法返回true。             |
| Iterator descendingIterator()           | 此方法以相反的顺序返回此双端队列中的元素的迭代器。           |
| E element()                             | 此方法检索但不删除此双端队列代表的队列的头部。               |
| E getFirst()                            | 此方法检索但不删除此双端队列的第一个元素。                   |
| E getLast()                             | 此方法检索但不删除此双端队列的最后一个元素。                 |
| boolean isEmpty()                       | 如果此双端队列不包含任何元素，则此方法返回true。             |
| Iterator iterator()                     | 此方法返回此双端队列中的元素的迭代器。                       |
| boolean offer(E e)                      | 此方法在此双端队列的末尾插入指定的元素。                     |
| boolean offerFirst(E e)                 | 此方法将指定的元素插入此双端队列的前面。                     |
| boolean offerLast(E e)                  | 此方法在此双端队列的末尾插入指定的元素。                     |
| E peek()                                | 此方法检索但不删除此双端队列表示的队列的头部，如果此双端队列为空，则返回null。 |
| E peekFirst()                           | 此方法检索但不删除此双端队列的第一个元素，如果此双端队列为空，则返回null。 |
| E peekLast()                            | 此方法检索但不删除此双端队列的最后一个元素，如果此双端队列为空，则返回null。 |
| E poll()                                | 此方法检索并删除此双端队列表示的队列的头部，如果此双端队列为空，则返回null。 |
| E pollFirst()                           | 此方法检索并删除此双端队列的第一个元素，如果此双端队列为空，则返回null。 |
| E pollLast()                            | 此方法检索并删除此双端队列的最后一个元素，如果此双端队列为空，则返回null。 |
| E pop()                                 | 此方法从此双端队列表示的堆栈中弹出一个元素。                 |
| void push(E e)                          | 此方法将元素压入此双端队列表示的堆栈上。                     |
| E remove()                              | 此方法检索并删除此双端队列代表的队列的头部。                 |
| boolean remove(Object o)                | 此方法从此双端队列删除指定元素的单个实例。                   |
| E removeFirst()                         | 此方法检索并删除此双端队列的第一个元素。                     |
| boolean removeFirstOccurrence(Object o) | 此方法删除此双端队列中指定元素的首次出现。                   |
| E removeLast()                          | 此方法检索并删除此双端队列的最后一个元素。                   |
| boolean removeLastOccurrence(Object o)  | 此方法删除此双端队列中最后一次出现的指定元素。               |
| int size()                              | 此方法返回此双端队列的元素数。                               |
| Object[\] toArray()                     | 此方法以适当的顺序返回一个数组，其中包含此双端队列中的所有元素。 |



#### 4.2、有效的括号、最小栈等问题

##### 4.2.1、有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

**解法**

​		使用栈来实现：初始化栈 S。 一次处理表达式的每个括号。 如果遇到开括号，我们只需将其推到栈上即可。这意味着我们将稍后处理它，让我们简单地转到前面的 子表达式。 如果我们遇到一个闭括号，那么我们检查栈顶的元素。如果栈顶的元素是一个 相同类型的 左括号，那么我们将它从栈中弹出并继续处理。否则，这意味着表达式无效。 如果到最后我们剩下的栈中仍然有元素，那么这意味着表达式无效。

```
class Solution {

  // Hash table that takes care of the mappings.
  private HashMap<Character, Character> mappings;

  // Initialize hash map with mappings. This simply makes the code easier to read.
  public Solution() {
    this.mappings = new HashMap<Character, Character>();
    this.mappings.put(')', '(');
    this.mappings.put('}', '{');
    this.mappings.put(']', '[');
  }

  public boolean isValid(String s) {

    // Initialize a stack to be used in the algorithm.
    Stack<Character> stack = new Stack<Character>();

    for (int i = 0; i < s.length(); i++) {
      char c = s.charAt(i);

      // If the current character is a closing bracket.
      if (this.mappings.containsKey(c)) {

     	// Get the top element of the stack. 
     	//If the stack is empty, set a dummy value of '#'
        char topElement = stack.empty() ? '#' : stack.pop();

        // If the mapping for this bracket doesn't match the stack's top element, 
        // return false.
        if (topElement != this.mappings.get(c)) {
          return false;
        }
      } else {
        // If it was an opening bracket, push to the stack.
        stack.push(c);
      }
    }

    // If the stack still contains elements, then it is an invalid expression.
    return stack.isEmpty();
  }
}
```

**复杂度分析**

- 时间复杂度：O(n)*O*(*n*)，因为我们一次只遍历给定的字符串中的一个字符并在栈上进行 O(1)*O*(1) 的推入和弹出操作
- 空间复杂度：O(n)*O*(*n*)，当我们将所有的开括号都推到栈上时以及在最糟糕的情况下，我们最终要把所有括号推到栈上。例如 `((((((((((`。

##### 4.2.2、最小栈

设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) —— 将元素 x 推入栈中。
pop() —— 删除栈顶的元素。
top() —— 获取栈顶元素。
getMin() —— 检索栈中的最小元素。

解法：

**使用辅助栈：**对于栈来说，如果一个元素 a 在入栈时，栈里有其它的元素 b, c, d，那么无论这个栈在之后经历了什么操作，只要 a 在栈中，b, c, d 就一定在栈中，因为在 a 被弹出之前，b, c, d 不会被弹出。因此，在操作过程中的任意一个时刻，只要栈顶的元素是 a，那么我们就可以确定栈里面现在的元素一定是 a, b, c, d。那么，我们可以在每个元素 a 入栈时把当前栈的最小值 m 存储起来。在这之后无论何时，如果栈顶元素是 a，我们就可以直接返回存储的最小值 m。

**算法**：设计一个数据结构，使得每个元素 a 与其相应的最小值 m 时刻保持一一对应。因此我们可以使用一个辅助栈，与元素栈同步插入与删除，用于存储与每个元素对应的最小值。

- 当一个元素要入栈时，我们取当前辅助栈的栈顶存储的最小值，与当前元素比较得出最小值，将这个最小值插入辅助栈中；
- 当一个元素要出栈时，我们把辅助栈的栈顶元素也一并弹出；
- 在任意一个时刻，栈内元素的最小值就存储在辅助栈的栈顶元素中。

```
import java.util.Stack;

public class MinStack {

    // 数据栈
    private Stack<Integer> data;
    // 辅助栈
    private Stack<Integer> helper;

    /**
     * initialize your data structure here.
     */
    public MinStack() {
        data = new Stack<>();
        helper = new Stack<>();
    }

    // 思路 2：辅助栈和数据栈不同步
    // 关键 1：辅助栈的元素空的时候，必须放入新进来的数
    // 关键 2：新来的数小于或者等于辅助栈栈顶元素的时候，才放入（特别注意这里等于要考虑进去）
    // 关键 3：出栈的时候，辅助栈的栈顶元素等于数据栈的栈顶元素，才出栈，即"出栈保持同步"就可以了

    public void push(int x) {
        // 辅助栈在必要的时候才增加
        data.add(x);
        // 关键 1 和 关键 2
        if (helper.isEmpty() || helper.peek() >= x) {
            helper.add(x);
        }
    }

    public void pop() {
        // 关键 3：data 一定得 pop()
        if (!data.isEmpty()) {
            // 注意：声明成 int 类型，这里完成了自动拆箱，从 Integer 转成了 int，
            // 因此下面的比较可以使用 "==" 运算符
            // 如果把 top 变量声明成 Integer 类型，下面的比较就得使用 equals 方法
            int top = data.pop();
            if(top == helper.peek()){
                helper.pop();
            }
        }
    }

    public int top() {
        if(!data.isEmpty()){
            return data.peek();
        }
        throw new RuntimeException("栈中元素为空，此操作非法");
    }

    public int getMin() {
        if(!helper.isEmpty()){
            return helper.peek();
        }
        throw new RuntimeException("栈中元素为空，此操作非法");
    }

}
```

