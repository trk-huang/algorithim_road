排序算法之冒泡算法

冒泡算法是一种非常简单的排序算法，也是我入门学习的第一个算法。它的原理是：从第一个数开始，重复走过要排序的数，一次比较相邻的两个数，如果顺序错误就把他们调换过来，直到没有元素要调换，才算完成。算法步骤如下：

1. 比较相邻的元素，如果前一个比后一个大，就调换位置
2. 对每一对相邻的元素做同样的工作，从第一个元素到最后一个元素。这样最后一个元素才是最大的数
3. 针对所有元素重复做以上两个步骤，除了最后一个

冒泡排序算法的代码如下：

```java
/**
 * Created by huangdaju on 17/7/25.
 */
public class BubbleSort {

    /**
     * 位置交换
     *
     * @param data
     * @param i
     * @param j
     */
    public void exChange(int[] data, int i, int j) {
        int temp = data[i];
        data[i] = data[j];
        data[j] = temp;

    }

    /**
     * 冒泡排序
     *
     * @param data
     */
    public int[] sort(final int[] data, final MainActivity activity) {
        int n = data.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - 1 - i; j++) { //比较两个数
                if (data[j] > data[j + 1]) {
                    exChange(data, j, j + 1);
                }
            }
        }
        return data;
    }
}
```

尽管冒泡排序是最容易了解和实现的排序算法之一，但它对于少数元素之外的数列排序是很没有效率的。

## 改进型算法：鸡尾酒排序算法

鸡尾酒排序，也叫**定向冒泡排序**，是冒泡排序的一种改进。此算法与冒泡排序的不同处在于**从低到高然后从高到低**，而冒泡排序则仅从低到高去比较序列里的每个元素。他可以得到比冒泡排序稍微好一点的效能。

```java
/**
 * Created by huangdaju on 17/7/25.
 */

public class CocksailSort extends BubbleSort {

    public void cocksailSort(final int[] data, final MainActivity activity) {
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

以序列\(2,3,4,5,1\)为例，鸡尾酒排序只需要访问一次序列就可以完成排序，但如果使用冒泡排序则需要四次。但是在乱数序列的状态下，鸡尾酒排序与冒泡排序的效率都很差劲.

