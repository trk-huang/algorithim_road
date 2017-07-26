# 排序算法之选择排序

选择排序算法的工作原理：

1. 初始时选择最小\(大\)元素，放到序列的起始位置作为已排序元素
2. 再从剩余未排序的元素中寻找最小\(大\)的元素，放到已排序元素的末尾
3. 以此类推，直到所有元素都排序完毕

选择排序和冒泡排序的区别：

1. 冒泡排序通过依次交换相邻两个不合法的元素，从而将当前最小\(大\)元素放到合适位置
2. 选择排序每遍历一次序列都记住了最小\(大\)元素的位置，最后仅需一次交换操作就能将元素放到合适的位置

```java

/**
 * Created by huangdaju on 17/7/25.
 */

public class CocksailSort extends BubbleSort {

    public void cocksailSort(final int[] data,  MainActivity activity) {
        int right = data.length - 1;
        int left = 0;
        while (left < right) {
            for (int i = left; i < right; i++) {
                if (data[i] > data[i + 1]) {
                    exChange(data, i, i + 1);
                    activity.onCallback();
                }
            }
            right--;
            for (int i = right; i > left; i--) {
                if (data[i - 1] > data[i]) {
                    exChange(data, i - 1, i);
                    activity.onCallback();
                }
            }
            left++;
        }
    }
}
```

**选择排序是不稳定的排序算法，不稳定发生在最小元素与A\[i\]交换的时刻。**

比如序列：{5, 8,5,2, 9 }，一次选择的最小元素是2，然后把2和第一个5进行交换，从而改变了两个元素5的相对次序。

