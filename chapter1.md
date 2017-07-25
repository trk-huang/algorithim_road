# 排序算法之冒泡算法

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
    private void exChange(int[] data, int i, int j) {
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



