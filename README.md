---
title: 内部排序算法
layout: post
categories: 
- 算法
- JAVA
tags:
- JAVA
---
<img src="https://picjumbo.com/wp-content/uploads/man-setting-up-a-drone-for-aerial-photography-in-mountains-2210x1473.jpg"  alt="生而无畏" align=center />

概要：本文首先介绍了基于比较模型的排序算法，即最坏复杂度都在Ω(nlgn)的排序算法，接着介绍了一些线性时间排序算法，这些排序算法虽然都在线性时间，但是都是在对输入数组有一定的约束的前提下才行。完整代码见文章尾。
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E6%8E%92%E5%BA%8F.jpg?raw=true"  alt="生而无畏" align=center />

## 直接插入排序

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;直接插入排序的基本思想是：把n个待排序的元素看成为一个有序表和一个无序表，开始时有序表中只包含一个元素，无序表中包含有n-1个元素，排序过程中每次从无序表中取出第一个元素，把它的排序码依次与有序表元素的排序码进行比较，将它插入到有序表中的适当位置，使之成为新的表。
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/(%E7%9B%B4%E6%8E%A5)%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />
**代码：**
```java
    public static void insertSort(int[] data) {
        System.out.println("开始排序");
        int arrayLength = data.length;
        for (int i = 1; i < arrayLength; i++) {
            int temp = data[i];
            if (data[i] - data[i - 1] < 0) {
                int j = i - 1;
                for (; j >= 0 && data[j] - temp > 0; j--) {
                    data[j + 1] = data[j];
                }
                data[j + 1] = temp;
            }
            System.out.println(java.util.Arrays.toString(data));
        }
    }
```
## 冒泡排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;冒泡排序的基本思想：通过对待排序序列从前向后，依次比较相邻元素的排序码，若发现逆序则交换，使排序码较大的元素逐渐从前部移向后部。因为排序的过程中，各元素不断接近自己的位置，如果一趟比较下来没有进行过交换，就说明序列有序，因此要在排序过程中设置一个标志swap判断元素是否进行过交换。从而减少不必要的比较。
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />
**代码：**
```java
    //方法一
    public static void bubbleSort1(int[] data){
        System.out.println("开始排序：\n");
        int arrayLength = data.length;
        for (int i = 0;i < arrayLength - 1; i++){
            for (int j = 0; j < arrayLength - 1 - j;j++){
                if (data[j] > data[j + 1]) {
                    int temp = data[j + 1];
                    data[j + 1] = data[j];
                    data[j] = temp;
                }
            }
            System.out.println(Arrays.toString(data));
        }
    }

    //方法二
    public static void bubbleSort2(int[] data) {
        System.out.println("开始排序：\n");
        int arrayLength = data.length;
        for (int i = 0; i < arrayLength - 1; i++) {
            boolean flag = false;                 //设置标志位 当按照排序排好时 停止循环
            for (int j = 0; j < arrayLength - j - 1; j++) {
                if (data[j] > data[j + 1]) {
                    int temp = data[j + 1];
                    data[j + 1] = data[j];
                    data[j] = temp;
                    flag = true;
                }
            }
            System.out.println(Arrays.toString(data));
            if (!flag) {
                break;
            }
        }
    }
```

## 快速排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;快速排序（Quick Sorting)是迄今为止所有内排序算法中速度最快的一种。它的基本思想是：任取待排序序列中的某个元素作为标准（也称为支点、界点，一般取第一个元素），通过一次划分，将待排元素分为左右两个子序列，左子序列元素的排序码均小于基准元素的排序码，右子序列的排序码则大于或等于基准元素的排序码，然后分别对两个子序列继续进行划分，直至每一个序列只有一
个元素为止。最后得到的序列便是有序序列。
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />
**代码：**
```java
    private static void swap(int[] data, int i, int j){
        int temp = data[i];
        data[i] = data[j];
        data[j] = temp;
    }

    public static void subSort(int[] data,int start,int end) {
        if (start < end) {
            int base = data[start];
            int low = start;
            int high = end + 1;
            while (true) {
                while (low < end && data[++low] - base <= 0)
                    ;
                while (high > start && data[--high] - base >= 0)
                    ;
                if (low < high) {
                    swap(data, low, high);
                } else {
                    break;
                }
            }
            swap(data, start, high);

            subSort(data, start, high - 1);//递归调用
            subSort(data, high + 1, end);
        }
    }

    public static void quickSort(int[] data){
        subSort(data,0,data.length-1);
    }
```

## 简单选择排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基本原理：将待排序的元素分为已排序（初始为空）和未排序两组，依次将未排序的？元素中值最小的元素放入已排序的组中。

**简单选择排序的基本过程为：**
>在一组元素R[i]到R[n]中选择具有最小关键码的元素
若它不是这组元素中的第一个元素，则将它与这组元素中的第一个元素对调。
除去具有最小关键字的元素，在剩下的元素中重复第（1）、（2）步，直到剩余元素只有一个止。

<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/(%E7%AE%80%E5%8D%95)%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />
**代码：**
```java
    public static void selectSort(int[] data) {
        System.out.println("开始排序");
        int arrayLength = data.length;
        for (int i = 0; i < arrayLength - 1; i++) {
            for (int j = i + 1; j < arrayLength; j++) {
                if (data[i] - data[j] > 0) {
                    int temp = data[i];
                    data[i] = data[j];
                    data[j] = temp;
                }
            }
            System.out.println(java.util.Arrays.toString(data));
        }
    }
```

## 堆排序

**（1)建初始堆**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;将排序码k，k,ka,.…，k,表示成一棵完全二叉树，然后从第Ln/2]个排序码（即树的最后一个非终端结点）开始筛选，使由该结点作根结点组成的子二叉树符合堆的定义，然后从第筑n/2J-1个排序码重复刚才操作，直到第一个排序码止。这时候，该二叉树符合堆的定义，初始堆已经建立。
**（2）堆排序**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;将堆中第一个结点（二叉树根结点）和最后一个结点的数据进行交换（k与k。），再将k,~koa重新建堆，然后k，和k。1交换，再将k,~k。,重新建堆，然后k，和k。,交换，如此重复下去，每次重新建堆的元素个数不断减1，直到重新建堆的元素个数仅剩一个为止。这时堆排序已经完成，则排序码k，k2,ks，…，k已排成一个有序序列。
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E5%A0%86%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />
**代码：**
```java
    public static void bucketSort(int[] data, int min, int max) {
        System.out.println("开始排序");
        int arrayLength = data.length;
        int[] temp = new int[arrayLength];
        int[] buckets = new int[max - min];
        for (int i = 0; i < arrayLength; i++) {
            buckets[data[i] - min]++;
        }
        System.out.println(Arrays.toString(buckets));
        for (int i = 1; i < max - min; i++) {
            buckets[i] = buckets[i] + buckets[i - 1];
        }
        System.out.println(Arrays.toString(buckets));
        System.arraycopy(data, 0, temp, 0, arrayLength);
        for (int k = arrayLength - 1; k >= 0; k--) {
            data[--buckets[temp[k] - min]] = temp[k];
        }
    }
```

## 希尔排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;希尔排序的基本思想：先将整个待排元素序列分割成若干个子序列（由相隔某个“增量”的元素组成的）分别进行直接插入排序，待整个序列中的元素基本有序（增量足够小）时，再对全体元素进行一次直接插入排序。因为直接插入排序在元素基本有序的情况下（接近最好情况），效率是很高的，因此希尔排序在时间效率上有较大提高。
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />

**代码：**
```java
    public static void ShellSort(int[] data) {
        System.out.println("开始排序");
        int arrayLength = data.length;

        int h = 1;
        while (h <= arrayLength / 3) {
            h = h * 3 + 1;
        }
        while (h > 0) {
            System.out.println("===h的值：" + h + "===");
            for (int i = h; i < arrayLength; i++) {
                int temp = data[i];
                if (data[i] - data[i - h] < 0) {
                    int j = i - h;
                    for (; j >= 0 && data[j] - temp > 0; j -= h) {
                        data[j + h] = data[j];
                    }
                    data[j + h] = temp;
                }
                System.out.println(java.util.Arrays.toString(data));
            }
            h = (h - 1) / 3;
        }
    }
```

## 桶排序

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;桶排序思想：用空间复杂度换取时间复杂度的经典例子，简单来说桶排序就是将要排序的集合划分为多个顺序的子集，再对每个子集排序，最后合并各个顺序的子集。如上面引用所诉，在多数场景下是可以用桶排序提高时间效率的。桶排序的应用场景主要是：1.key范围不大，2.各子集分布平均。桶排序的思想还适用于对不同key的个数统计，比如统计高考分数分布。（为每个可能的高考分数创建一个桶，统计每个桶内的记录个数即可）

<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E6%A1%B6%E6%8E%92%E5%BA%8F.png?raw=true"  alt="生而无畏" align=center />

**代码：**
```java
    public static void bucketSort(int[] data, int min, int max) {
        System.out.println("开始排序");
        int arrayLength = data.length;
        int[] temp = new int[arrayLength];
        int[] buckets = new int[max - min];
        for (int i = 0; i < arrayLength; i++) {
            buckets[data[i] - min]++;
        }
        System.out.println(Arrays.toString(buckets));
        for (int i = 1; i < max - min; i++) {
            buckets[i] = buckets[i] + buckets[i - 1];
        }
        System.out.println(Arrays.toString(buckets));
        System.arraycopy(data, 0, temp, 0, arrayLength);
        for (int k = arrayLength - 1; k >= 0; k--) {
            data[--buckets[temp[k] - min]] = temp[k];
        }
    }
```

## 归并排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;归并排序 (merge sort) 是一类与插入排序、交换排序、选择排序不同的另一种排序方法。归并的含义是将两个或两个以上的有序表合并成一个新的有序表。

<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />

**代码：**
```java
    public static void mergeSort(int[] data) {
        // 归并排序
        sort(data, 0, data.length - 1);
    }

    // 将索引从left到right范围的数组元素进行归并排序
    private static void sort(int[] data, int left, int right) {
        if(left < right){
            //找出中间索引
            int center = (left + right)/2;
            sort(data,left,center);
            sort(data,center+1,right);
            //合并
            merge(data,left,center,right);
        }
    }

    // 将两个数组进行归并，归并前两个数组已经有序，归并后依然有序
    private static void merge(int[] data, int left, int center, int right) {
        int[] tempArr = new int[data.length];
        int mid = center + 1;
        int third = left;
        int temp = left;
        while (left <= center && mid <= right) {
            if (data[left] - data[mid] <= 0) {
                tempArr[third++] = data[left++];
            } else {
                tempArr[third++] = data[mid++];
            }
        }
        while (mid <= right) {
            tempArr[third++] = data[mid++];
        }
        while (left <= center) {
            tempArr[third++] = data[left++];
        }
        while (temp <= right) {
            data[temp] = tempArr[temp++];
        }
    }

```

## 基数排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基数排序（radix sort）属于“分配式排序”（distribution sort），又称“桶子法”（bucket sort）或bin sort，顾名思义，它是透过键值的部份资讯，将要排序的元素分配至某些“桶”中，藉以达到排序的作用，基数排序法是属于稳定性的排序，其时间复杂度为O (nlog(r)m)，其中r为所采取的基数，而m为堆数，在某些时候，基数排序法的效率高于其它的稳定性排序法。

<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E5%9F%BA%E6%95%B0%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />

**代码：**
```java
    public static void radixSort(int[] data, int radix, int d) {
        System.out.println("开始排序：");
        int arrayLength = data.length;
        int[] temp = new int[arrayLength];
        int[] buckets = new int[radix];
        for (int i = 0, rate = 1; i < d; i++) {
            // 重置count数组，开始统计第二个关键字
            Arrays.fill(buckets, 0);
            // 当data数组的元素复制到temp数组中进行缓存
            System.arraycopy(data, 0, temp, 0, arrayLength);
            for (int j = 0; j < arrayLength; j++) {
                int subKey = (temp[j] / rate) % radix;
                buckets[subKey]++;
            }
            for (int j = 1; j < radix; j++) {
                buckets[j] = buckets[j] + buckets[j - 1];
            }
            for (int m = arrayLength - 1; m >= 0; m--) {
                int subKey = (temp[m] / rate) % radix;
                data[--buckets[subKey]] = temp[m];
            }
            System.out.println("对" + rate + "位上子关键字排序："
                    + java.util.Arrays.toString(data));
            rate *= radix;
        }
    }

```
## 计数排序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;计数排序是一个非基于比较的排序算法，该算法于1954年由 Harold H. Seward 提出。它的优势在于在对一定范围内的整数排序时，它的复杂度为Ο(n+k)（其中k是整数的范围），快于任何比较排序算法。 [1-2]  当然这是一种牺牲空间换取时间的做法，而且当O(k)>O(n*log(n))的时候其效率反而不如基于比较的排序（基于比较的排序的时间复杂度在理论上的下限是O(n*log(n)), 如归并排序，堆排序）
<img src="https://github.com/leslieAIbin/leslieAIbin.github.io/blob/master/img/%E5%86%85%E9%83%A8%E6%8E%92%E5%BA%8F/%E8%AE%A1%E6%95%B0%E6%8E%92%E5%BA%8F.gif?raw=true"  alt="生而无畏" align=center />

**代码：**
```java
    public static void binaryInsertSort(int[] data) {
        System.out.println("开始排序");
        int arrayLength = data.length;
        for (int i = 1; i < arrayLength; i++) {
            int temp = data[i];
            int low = 0;
            int high = i - 1;
            while (low <= high) {
                int mid = (low + high) / 2;
                if (temp > data[mid]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
            for (int j = i; j > low; j--) {
                data[j] = data[j - 1];
            }
            data[low] = temp;
            System.out.println(java.util.Arrays.toString(data));
        }

    }

```

[完整代码](https://github.com/leslieAIbin/sort)