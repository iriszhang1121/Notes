# 手把手教你刷Leetcode

原作者：爱学习的饲养员

视频：82个

来源：

https://www.youtube.com/watch?v=l7jCybGk1WA&list=PLVCBLinWsHYyYvQlZNAAy81s9z_OezZvl

https://www.bilibili.com/video/BV1sy4y1q79M/?spm_id_from=333.788.video.desc.click

[TOC]

# 0 视频介绍

知识点：数据结构、常用算法

<font color="blue">每个知识点 + leetcode算法练习（<4个，2 easy 2 medium）+ 对应练习题视频讲解（思路+伪代码，Java/Python代码文本）</font>

# 1 时间复杂度

https://www.youtube.com/watch?v=29SMQJt05wc&list=PLVCBLinWsHYyYvQlZNAAy81s9z_OezZvl&index=2

## 什么是时间复杂度

<font color="red">算法的执行效率，算法**执行时间** 和 输入的值之间的关系</font>

```python
def test(num):
    total = 0
    for i in range(num):
        total += i
    return total
```

以上案例的时间复杂度是O(N)

## 常用时间复杂度案例分析

主要看for/while循环，没有循环一般就是常量O(1)

$O(1)$ 执行时间和输入的num无关

```python
def O1(num):
    i = num
    j = num * 2
    return i + j
```

$O(logN)$

```python
def OlogN(num):
    i = 1
    while i < num:
        i *= 2
    return i
```

<img src="https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260225223804783_oTUtl4.png" alt="image-20260225223804783" style="zoom:50%;" />s

$O(N)$ 

```python
def ON(num):
    total = 0
    for i in range(num):
        total += i
    return total
```

$O(M+N)$

```python
    total = 0
    for i in range(num1):
        total += i
    for j in range(num2):
        total += j
    return total
```

$O(NlogN)$​

```python
def ONlogN(num1, num2):
    total = 0
    j = 0
    for i in range(num1):
        while j < num2:
            total += i + j
            j *= 2
    return total
```

$O(N^2)$​

```python
def ON2(num):
    total = 0
    for i in range(num):
        for j in range(num):
            total += i + j
    return total
```

## 常用时间复杂度对比

<img src="https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260225221500922_4N6Ca1.png" alt="image-20260225221500922" style="zoom:50%;" />

时间从短到长：$O(1) < O(logN) < O(N) < O(NlogN) < O(N^2) < O(2^N) < O(N!)$

$O(logN)$：二分查找法

$O(NlogN)$：排序

# 2 空间复杂度

https://www.youtube.com/watch?v=vxlHGg2KHuY&list=PLVCBLinWsHYyYvQlZNAAy81s9z_OezZvl&index=3

## 什么是空间复杂度

<font color="red">算法**存储空间** 与 输入值之间的关系 （占据空间要看**变量**个数）</font>

<img src="https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260225222004960_Scl0eU.png" alt="image-20260225222004960" style="zoom:50%;" />

左：

​	total永远是1个int，总体空间复杂度为$O(1)$

右：

​	看array长度，也就是nums长度，空间复杂度是$O(N)$

## 常用空间复杂度案例分析

常用空间复杂度

$O(1),   O(N), O(N^2)$ 常用

$O(logN),  O(NlogN)$ 用不上

**注意：变量、递归**

## 常用空间复杂度对比

空间复杂度：$O(1) <  O(N) < O(N^2)$ 

空间和时间只能二选一，工作当中一般时间>空间

# 3 数据结构-Array知识点讲解

https://www.bilibili.com/read/cv8568185/?spm_id_from=333.788.comment.all.click&opus_fallback=1

<font color="red">数组： **连续内存空间**中，存储一组 **相同类型** 的元素</font>

> 链表： 不连续内存空间，存储一组元素

区分：元素，索引

区分：数组访问access（通过索引进行访问元素），数组搜索search（通过元素进行查索引，或者看元素是否存在）

## 数组的时间复杂度

访问 access $O(1)$

搜索 search $O(N)$

插入 insert $O(N)$

删除 delete $O(N)$

<font color="red">适合读多 写少</font>

## 常用操作

1. 创建数组
2. 添加元素
3. 访问元素
4. 修改元素
5. 删除元素
6. 遍历数组
7. 查找元素
8. 数组长度
9. 数组排序（内置排序方法）

### 3.1 Python Array

https://www.youtube.com/watch?v=LTQRX_C7Gk4&list=PLVCBLinWsHYyYvQlZNAAy81s9z_OezZvl&index=5

```python
# 1 Create an array
a = []

# 2.1 Add element
# Time complexity: O(1) by default, but it could be O(N) 当执行添加元素后的当前内存区不足以存储全部元素，会重新找一块足够大的内存区，这是需要把原来的所有元素重新复制
a.append(1)
a.append(2)
a.append(3)
print(a) # [1, 2, 3]

# 2.2 Add element
# Time complexity: O(N) 
a.insert(2, 99);
print(a) # [1, 2, 99, 3]

# 3 Access element 用索引（下标）访问元素
# Time complexity: O(1) 
temp = a[2]
print(temp) # 99

# 4 Update element
# Time complexity: O(1)
a[2] = 88
print(a) # [ 1, 2, 88, 3]

# 5 Remove element 三种删除方法
# Time complexity: O(N) 
a.remove(88) #直接删除elment
print(a) # [1, 2, 3]

# Time complexity: O(N) 
a.pop(1) # 根据索引删除element
print(a) # [1, 3]

# Time complexity: O(1)
a.pop() # 直接删除最后一个element
print(a) # [1]

# 6 the length of array
size = len(a) # a = [1, 2, 3]
print(size) # 3

# 7 Iterate array 三种遍历方法
# Time complexity: O(N) 
for i in a:
    print(i)
for index, element in enumerate(a):
    print("Index at ", index, "is: ", element)
for i in range(0, len(a)):
    pprint("Index at ", i, " element is: ", a[i])
    
# 8 Find an element
# Time complexity: O(N) 
index = a.index(2) # a = [1, 2, 3]
print(index) # 1

# 9 Sort an array
# Time complexity: O(NlogN) 
a = [3, 1, 2]
a.sort()
print(a) # [1, 2, 3]

a.sort(reverse=True)
print(a) # [3, 2, 1]
```

### 3.2 Java Array

```java
// 1 创建数组的方式
// Four solutionss to create an array in Java
// Take [1, 2, 3] as an example
// Sol 1
int[] a = {1, 2, 3};
System.out.println("a: " + Arrays.toString(a));

// Sol 2
int[] b = new int[]{1, 2, 3};
System.out.println("b: " + Arrays.toString(b));

// Sol 3 常用
int[] c = new int[3]; //  c = [0, 0, 0]
for(int i = 0; i < a.length; i++) {
    c[i] = i + 1;
} // c = [1, 2, 3]
System.out.println("c: " + Arrays.toString(c));

//Sol 4 常用
ArrayList<Integer> arr = new AarrayList<>(); // 不需要指定长度和类型，需要import对应的package
for(int i = 0; i < 3; i++) {
    arr.add(i + 1);
}
System.out.println("arr: " + arr.toString());


// 2 添加元素 ArrayList方法
// Add element
// Time complexity: O(1) by default, but it could be O(N) 当执行添加元素后的当前内存区不足以存储全部元素，会重新找一块足够大的内存区，这是需要把原来的所有元素重新复制
arr.add(99);
System.out.println("arr: " + arr.toString()); // [1, 2, 3, 99]

// Insert element
// Time complexity: O(N)
arr.add(3, 88);
System.out.println("arr: " + arr.toString()); // [1, 2, 3, 88, 99]

// 3 Access element 通过索引访问
// Time complexity: O(1)
int c1 = c[1];
int arr1 = arr.get(1);
// 1
System.out.println("c1: " + c1);
System.out.println("arr1: " + arr1);

// 4 Update element
// Time complexity: O(1)
c[1] = 11;
arr.set(1, 11);
// 1 -> 11
System.out.println("c1: " + c[1]);
System.out.println("arr1: " + arr.get(1));

// 5 Remove element
// Time complexity: O(N)
arr.remove(3);
System.out.println("arr1: " + arr.get(1));

// 6 length of an array
// Time complexity: O(N)
int cSize = c.length;
int arrrSize = arr.size();
System.out.println("c length: " + cSize);
System.out.println("arr length: " + arrSize);

// 7 Iterate an array
// Time complexity: O(N)
// iterate c
for (int i = 0; i < c.length; i++) {
    int currrent = c[i];
    System.out.println("c at index " + i + ": " + current);
}
// iterate arr
for (int i = 0; i < arr.size(); i++) {
    int currrent = arr.get(i);
    System.out.println("arr at index " + i + ": " + current);
}

// 8 Find an element
// Time complexity: O(N)
// find an element in  c
for (int i = 0; i < c.length; i++) {
   if (c[i] == 99) {
     System.out.println("We found 99 in c");  
   }
}
// find an element in  arr
boolean is99 = arr.contains(99);
System.out.println("Are we found 99 in arr?" + is99); // True / False

// 9 Sort an array by built-in lib

c= new int[]{2, 3, 1};
arr = new ArrayList<>();
arr.add(2);
arr.add(3);
arr.add(1);
// [2, 3, 1]
System.out.println("c: " + Arrays.toString(c));
System.out.println("arrr: " + arr.toString());

// from small to big
// Time complexity: O(NlogN)
Arrays.sort(c); 
Collections.sort(arr);
// [1, 2, 3]
System.out.println("c: " + Arrays.toString(c));
System.out.println("arrr: " + arr.toString());

// from big to small
// Time complexity: O(NlogN)
// For c, you can read an array in reverse 方法1，把数组c从后往前读
// 		or Arrays.sort(T[], Collections.reverseOrder()); 方法2 把int[] c => Integer[] c
// For arr, 
Collections.sort(arr, Collections.reverseOrder());
// [3, 2, 1]
System.out.println("c: " + Arrays.toString(c));
System.out.println("arrr: " + arr.toString());
```

## 练习题

### LC485 最大连续1的个数

一次遍历、动态规划

### LC283 移动零

stack / 单指针

### LC27 移除元素

stack, 双指针

# 4 链表linked list

https://www.bilibili.com/read/cv8585621/?opus_fallback=1

数组：在 连续的内存空间 存储相同类型的元素

**链表**：在 **不连续的内存空间** 存储元素

## 链表时间复杂度

**访问access $O(N)$ 需要从头到尾遍历**

**搜索search $O(N)$ 从头遍历到尾**

**插入insert $O(1)$**

**删除delete $O(1)$**

<font color="red">特点：写很快、读很慢 -》写多读少</font>

## 常用操作

### 4.1 Python linked list

1. 创建链表

	```python
	linkedlist = deque()
	```

2. 添加元素

	append $O(1)$

	insert  $O(N)$

	```python
	4# add element
	# time complexity O(1)
	linkedlist.append(1)
	linkedlist.append(2)
	linkedlist.append(3)
	# [1. 2, 3]
	print(linkedlist)
	
	# insert element
	# time complexity O(N)
	linkedlist.insert(2, 99)
	# [1, 2, 99, 3]
	print(linkedlist)
	```

3. 访问元素

	```python
	# access element
	# time complexity O(N)
	element = linkedlist[2]
	# 99
	print(element)
	```

4. 搜索元素

	```python
	# searrch element
	# time complexity O(N)
	index = linkedlist.index(99)
	# 2
	print(index)
	```

5. 更新元素

	```python
	# update element
	# time complexity O(N)
	linkedlist[2] = 88
	# [1, 2, 88, 3]
	print(linkedlist)
	```

6. 删除元素

	```python
	# delete element
	# time complexity O(N)
	linkedlist.remove(88) # delete by value
	# del linkedlist[2] delete by index
	# [1, 2, 3]
	print(linkedlist)
	```

7. 长度

	```python
	# length
	# time complexity O(1)
	length = len(linkedlist)
	# 3
	print(length)
	```

### 4.2 Java linked list

1. 创建链表

	```java
	// create a LinkedList
	LinkedList<Integer> list = new LinkedList<>();
	```

2. 添加元素

	append $O(1)$

	insert  $O(N)$

	```java
	// add element
	// time complexity O(1)
	list.add(1);
	list.add(2);
	list.add(3);
	// [1. 2, 3]
	System.out.println(list.toString());
	
	// insert element
	// time complexity O(N)
	list.add(2, 99)
	// [1, 2, 99, 3]
	System.out.println(list.toString());
	```

3. 访问元素

	```java
	// access element
	// time complexity O(N)
	int element = list.get(2);
	// 99
	System.out.println(element);
	```

4. 搜索元素

	```java
	// searrch element
	// time complexity O(N)
	int index = list.indexOf(99)
	// 2
	System.out.println(index);
	```

5. 更新元素

	```java
	// update element
	// time complexity O(N)
	list.set(2, 88);
	// [1, 2, 88, 3]
	System.out.println(list.toString());
	```

6. 删除元素

	```java
	// delete element
	// time complexity O(N)
	list.remove(2); // remove by index
	// [1, 2, 3]
	System.out.println(list.toString());
	```

7. 长度

	```java
	// length
	// time complexity O(1)
	int length = list.size();
	// 3
	System.out.println(length);
	```

## 练习题

### LC203 移除链表元素 remove linked list

引入dummy

### LC206 反转链表 reverse linked list

头插法

| dummy    |      | head  |      | Head.next    |      |            |      |      |      |
| -------- | ---- | ----- | ---- | ------------ | ---- | ---------- | ---- | ---- | ---- |
|          |      | dnext |      | hnext        |      | hnext.next |      |      |      |
|          |      | hnext |      | hnext.next   |      | dnext      |      |      |      |
|          |      |       |      |              |      |            |      |      |      |
| pre      |      | cur   |      | Nxt=cur.next |      |            |      |      |      |
|          |      |       |      |              |      |            |      |      |      |
| cur.next |      | pre   |      | Cur          |      |            |      |      |      |



# 5 队列Queue

特点：先进先出

单向队列：一个口进、另一个口出

双向队列：两个口都可以进/出

## 队列时间复杂度

**访问access $O(N)$ 需要从头到尾遍历**

**搜索search $O(N)$ 从头遍历到尾**

**插入insert $O(1)$**

**删除delete $O(1)$**

## 队列常用操作

https://www.bilibili.com/read/cv8623247/?opus_fallback=1 

### 5.1 Python Queue

1. 创建队列

	```python
	# create a queue
	queue = deque()
	```

2. 添加元素

	```python
	# add elemment
	# time complexity: O(1)
	queue.append(1)
	queue.append(2)
	queue.append(3)
	# [1, 2, 3]
	print(queue)
	```

3. 获取即将出队的元素

	```python
	# get the head of the queue
	# time complexity: O(1)
	temp1 = queue[0]
	# 1
	print(temp1)
	```

4. 删除即将出队的元素

	```python
	# remove the head of the queue
	# time complexity: O(1)
	temp2 = queue.popleft() # popleft / popright 删除并返回值
	# 1
	print(temp2)
	# [2, 3]
	print(queue)
	```

5. 判断队列是否为空

	```python
	# queue is empty
	# time complexity: O(1)
	len(queue) == 0
	```

6. 队列长度

	```python
	len(queue)
	```

7. 遍历队列（一边删除一边遍历队列操作）

	```python
	# time complexity: O(N)
	while len(queue) != 0:
	    temp = queue.popleft()
	    print(temp)
	```

### 5.2 Java Queue

1. 创建队列

	<font color="red">LinkedList作为queue的数据结构，因为链表插入删除比较快（$O(1)$)，使用队列时经常边加数据边删除，所以用LinkedList实现queue。不用ArrayList是因为数组的特性，在进行插入删除时时间复杂度可能会变成$O(N)$。</font>

	```java
	// create a queue
	Queue<Integer> queue = new LinkedList<>();
	```

2. 添加元素

	```java
	// add element
	// time complexity: O(1)
	queue.add(1);
	queue.add(2);
	queue.add(3);
	// [1, 2, 3]
	System.out.println(queue.toString());
	```

3. 获取即将出队的元素

	```java
	// get the head of queue
	// time complexity: O(1)
	int temp1 = queue.peek();
	// 1
	System.out.println(temp1);
	```

4. 删除即将出队的元素

	```java
	// remove the head of queue
	// time complexity: O(1)
	int temp2 = queue.poll();
	// 1
	System.out.println(temp2);
	// [2, 3]
	System.out.println(queue.toString());
	```

5. 判断队列是否为空

	```java
	// queue is empty?
	// time complexity: O(1)
	// isEmpty yes-> true, no->false
	System.out.println(queue.isEmpty());
	```

6. 队列长度

	```java
	// the length of queue
	// time complexity: O(1)
	// 3
	System.out.println(queue.size());
	```

7. 遍历队列（一边删除一边遍历队列操作）

	```java
	// time complexity: O(N)
	while (!queue.isEmpty()) { // not empty
	    int temp = queue.poll();
	    System.out.println(temp);
	}
	```

## 练习题

### LC933 最近的请求次数 number of recent calls

https://www.bilibili.com/read/cv8623235/?from=articleDetail&opus_fallback=1

# 6 Stack

## stack时间复杂度

## 常用操作

### 6.1 Python stack

### 6.2 Java stack

## 练习题

### LC20

### LC496

# 7 HashTable

## 时间复杂度

## 常用操作

### 7.1 Python HashTable

### 7.2 Java HashTable

## 练习题

### LC217

### LC389

### LC496

# 8 集合Set

## 时间复杂度

## 常用操作

### 8.1 Python set

### 8.2 Java set

## 练习题

### LC217

### LC705

# 9 树Tree

# 10 堆Heap

## 时间复杂度

## heap常用操作

### 10.1 Python heap

### 10.2 Java heap

## 练习题

### LC215

### LC692

# 11 图graph

# 12 数据结构知识点回顾

# 13 双指针

## 练习题

### LC141

### LC881

# 14 二分查找法 Binary Search

## 练习题

### LC704

### LC35

### LC162

### LC74

# 15 滑动窗口Sliding Window

## 练习题

### LC209

### LC1456

# 16 递归Recursion

## 练习题

### LC509

### LC206

### LC344

# 17 分治法Divde & Partition

## 练习题

### LC169

### LC53

# 18 回溯法Backtracking

## 练习题

### LC22

### LC78

# 19 深度优先搜索DFS

## 练习题

### LC938

### LC200

# 20 广度优先搜索BFS

## 练习题

### LC102

### LC107

# 21 并查集 Union Find Set及其优化

# 22 贪心算法Greedy

# 23 记忆化搜索

# 24 动态规划

## 练习题

### LC509

### LC62

# 25 前缀树Trie

## 练习题

### LC720

# 26 完结-下一步刷题建议



## 

