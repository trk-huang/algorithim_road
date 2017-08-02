# 希尔排序

希尔排序一种更高效的插入排序相比较与二分插入排序来说。它也叫递减增量排序，是一种不稳定排序。

希尔排序针对于插入排序的两大性质进行的改进：

* 插入排序在对几乎排好序的数据操作时，效率高，即可以达到线性排序的效率
* 插入排序一般来说是低效的，因为插入排序每次只能将数据移动一位

希尔排序通过将比较的全部元素分为几个区域来提升插入排序的性能。这样可以让一个元素可以一次性得朝着最终位置前进一大步。然后算法取越来越小的步长进行排序，算法的最后一步就是普通的插入排序。但是到了这一步，排序已经基本完成，此时插入排序相对较快了。

代码实例：

```java
/**
 * Created by huangdaju on 17/8/2.
 */

public class ShellSort extends BubbleSort {

    public void shellSort(int[] data, MainActivity mainActivity) {
        int n = data.length;
        int gap = n;
        while (gap >= 1) {
            gap = gap / 2;
            int get;
            for (int i = 1; i < n; i += gap) {
                get = data[i];
                for (int j = 0; j <= i - 1; j++) {
                    if (data[j] > get) {
                        exChange(data, i, j);
                        mainActivity.onCallback();
                    }
                }
            }
        }
    }
}

```



