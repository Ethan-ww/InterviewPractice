# Data Structures

## Array

### Sort

####Time complexity 

<img src="/Users/ethan/Desktop/InterviewPractice/images/Complexity.png" alt="Complexity" style="zoom:67%;" />

#### Merge sort

时间复杂性稳定，但是占用空间大，空间换效率

```java
void merge(int arr[], int l, int m, int r) 
{ 
    // Find sizes of two subarrays to be merged 
    int n1 = m - l + 1; 
    int n2 = r - m; 

    /* Create temp arrays */
    int L[] = new int[n1]; 
    int R[] = new int[n2]; 

    /*Copy data to temp arrays*/
    for (int i = 0; i < n1; ++i) 
        L[i] = arr[l + i]; 
    for (int j = 0; j < n2; ++j) 
        R[j] = arr[m + 1 + j]; 

    /* Merge the temp arrays */

    // Initial indexes of first and second subarrays 
    int i = 0, j = 0; 

    // Initial index of merged subarry array 
    int k = l; 
    // 轮流放入原array
    while (i < n1 && j < n2) { 
        if (L[i] <= R[j]) { 
            arr[k] = L[i]; 
            i++; 
        } 
        else { 
            arr[k] = R[j]; 
            j++; 
        } 
        k++; 
    } 

    /* Copy remaining elements of L[] if any */
    while (i < n1) { 
        arr[k] = L[i]; 
        i++; 
        k++; 
    } 

    /* Copy remaining elements of R[] if any */
    while (j < n2) { 
        arr[k] = R[j]; 
        j++; 
        k++; 
    } 
} 

// Main function that sorts arr[l..r] using 
// merge() 
void sort(int arr[], int l, int r) 
{ 
    if (l < r) { 
        // Find the middle point 
        int m = (l + r) / 2; 

        // Sort first and second halves 
        sort(arr, l, m); 
        sort(arr, m + 1, r); 

        // Merge the sorted halves 
        merge(arr, l, m, r); 
    } 
} 
```

#### Quick sort

每次寻找一个pivot，将比pivot小的划至左侧，大的划至右侧。对左右侧依次分割排序。

```java
// Java program for implementation of QuickSort 
class QuickSort 
{ 
    /* This function takes last element as pivot, 
       places the pivot element at its correct 
       position in sorted array, and places all 
       smaller (smaller than pivot) to left of 
       pivot and all greater elements to right 
       of pivot */
    int partition(int arr[], int low, int high) 
    { 
        int pivot = arr[high];  
        int i = (low-1); // index of smaller element 
        for (int j=low; j<high; j++) 
        { 
            // If current element is smaller than the pivot 
            if (arr[j] < pivot) 
            { 
                i++; 
  
                // swap arr[i] and arr[j] 
                int temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
        } 
  
        // swap arr[i+1] and arr[high] (or pivot) 
        int temp = arr[i+1]; 
        arr[i+1] = arr[high]; 
        arr[high] = temp; 
  
        return i+1; 
    } 
  
  
    /* The main function that implements QuickSort() 
      arr[] --> Array to be sorted, 
      low  --> Starting index, 
      high  --> Ending index */
    void sort(int arr[], int low, int high) 
    { 
        if (low < high) 
        { 
            /* pi is partitioning index, arr[pi] is  
              now at right place */
            int pi = partition(arr, low, high); 
  
            // Recursively sort elements before 
            // partition and after partition 
            sort(arr, low, pi-1); 
            sort(arr, pi+1, high); 
        } 
    } 
  
    /* A utility function to print array of size n */
    static void printArray(int arr[]) 
    { 
        int n = arr.length; 
        for (int i=0; i<n; ++i) 
            System.out.print(arr[i]+" "); 
        System.out.println(); 
    } 
  
    // Driver program 
    public static void main(String args[]) 
    { 
        int arr[] = {10, 7, 8, 9, 1, 5}; 
        int n = arr.length; 
  
        QuickSort ob = new QuickSort(); 
        ob.sort(arr, 0, n-1); 
  
        System.out.println("sorted array"); 
        printArray(arr); 
    } 
} 
/*This code is contributed by Rajat Mishra */
```

#### Tim sort

java 内置的排序算法，调用方法为Arrays.sort(arr)。

如需传入自定义比较方式可创建一个继承自Comparator 的类

```java
// 创建一个comparator类
class NumComparator implements Comparator<NameTag> {
    public int compare (NameTag left,NameTag right) {
        return(left.getNumber() - right.getNumber());
    }
}
// 调用如下
Arrays.sort(tags, new NumComparator());
```



## LinkedList

快慢指针能解决很多问题

## Tree

通常tree类的题目会使用很多的递归，做题时要想好返回条件，遍历顺序。

### Binary search tree





# Algorithms

## Graph

### BFS

把遍历的node加入一个**queue**，first in first out。

可以用一个while-loop来实现

###DFS

访问的node加入一个stack，first in last out。

可以用while-loop加上stack实现或者递归。



# Network

## 时延

总时延 = 排队时延 + 处理时延 + 传输时延 + 传播时延

###排队时延

分组在路由器的输入队列和输出队列中排队等待的时间，取决于网络当前的通信量。

###处理时延

主机或路由器收到分组时进行处理所需要的时间，例如分析首部、从分组中提取数据、进行差错检验或查找适当的路由等。

###传输时延

主机或路由器传输数据帧所需要的时间。

$delay=\frac{l}{v}$

其中 l 表示数据帧的长度，v 表示传输速率。

###传播时延

电磁波在信道中传播所需要花费的时间，电磁波传播的速度接近光速。

其中 l 表示信道长度，v 表示电磁波在信道上的传播速度。

## 网络结构

![network layers](/Users/ethan/Desktop/InterviewPractice/images/network layers.png)

###1. 五层协议

- **应用层** ：为**特定应用程序**提供数据传输服务，例如 HTTP、DNS 等协议。数据单位为**报文**。
- **传输层** ：为**进程**提供通用数据传输服务。由于应用层协议很多，定义通用的传输层协议就可以支持不断增多的应用层协议。运输层包括两种协议：传输控制协议 TCP，提供面向连接、可靠的数据传输服务，数据单位为**报文段**；用户数据报协议 UDP，提供无连接、尽最大努力的数据传输服务，数据单位为用户数据报。TCP 主要提供完整性服务，UDP 主要提供及时性服务。
- **网络层** ：为**主机**提供数据传输服务。而传输层协议是为主机中的进程提供数据传输服务。网络层把传输层传递下来的报文段或者用户数据报**封装成分组**。
- **数据链路层** ：网络层针对的还是主机之间的数据传输服务，而主机之间可以有很多链路，链路层协议就是为同一链路的主机提供数据传输服务。数据链路层把网络层传下来的分组**封装成帧**。
- **物理层** ：考虑的是怎样在传输媒体上传输数据比特流，而不是指具体的传输媒体。物理层的作用是尽可能屏蔽传输媒体和通信手段的差异，使数据链路层感觉不到这些差异。

#### 数据链接层

#####信道复用技术

* 频分复用： 相同时间占用不同频率的带宽资源
* 时分复用： 不同时间占用相同的频率带宽资源
* 统计时分复用： 不固定时分复用帧的位置，有数据就集中一组发送

#####MAC

固定的机器编码，用与交换机的机器对端口映射

交换机会自学习，更新翻译表

#### 网络层

##### VPN

VPN 使用公用的互联网作为本机构各专用网之间的通信载体。专用指机构内的主机只与本机构内的其它主机通信；虚拟指好像是，而实际上并不是，它有经过公用的互联网。

（场所A）-- （路由A）-- 【互联网/隧道】-- （路由B）-- （场所B）

##### NAT

将内网ip+端口转化为外网ip+端口，内网主机公用一个外网ip，使用不同端口来转发不同内网ip

##### 路由协议

1. RIP 
   1. 两个路由之间的跳跃数计做开销，最多跳跃15次
   2. 周期性与相邻路由器更新路由表，最终知道到达每一个网络内路由的距离以及下一跳的路由
   3. 实现简单但是限制网络规模
2. OSPF
   1. 向所有路由广播自己的链接状态（仅在链接变化时广播）。最终所有路由都具有全网的拓扑结构
   2. 路径计算使用Dijkstra的最短路径算法
   3. OSPF收敛速度比RIP快
3. BGP
   1. 每个AS之间选用比较好的路由尽心通信
   2. 可以限制其他AS通过自己转发
   3. 必须配置BGP发言人来进行路由信息交换

###2. OSI

其中表示层和会话层用途如下：

- **表示层** ：数据压缩、加密以及数据描述，这使得应用程序不必关心在各台主机中数据内部格式不同的问题。
- **会话层** ：建立及管理会话。

五层协议没有表示层和会话层，而是将这些功能留给应用程序开发者处理。

###3. TCP/IP

它只有四层，相当于五层协议中数据链路层和物理层合并为网络接口层。

**TCP/IP 体系结构不严格遵循 OSI 分层概念**，应用层可能会直接使用 IP 层或者网络接口层。

###4. 数据在各层之间的传递过程

在向下的过程中，需要添加下层协议所需要的首部或者尾部，而在向上的过程中不断拆开首部和尾部。

**路由器只有下面三层协议**，因为路由器位于网络核心中，不需要为进程或者应用程序提供服务，因此也就不需要传输层和应用层。

