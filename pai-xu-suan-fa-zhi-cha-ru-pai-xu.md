# 排序算法之插入排序

插入排序类似于我们平时抓扑克牌的模式。

![](http://images2015.cnblogs.com/blog/739525/201603/739525-20160329094816957-1860272498.jpg)

对于未排序的牌，在已排序的序列中从右到左向前扫描，找到相应的位置插入。

具体算法步骤如下：

1. 从第一个元素开始，该元素被认为已经排序
2. 取出下一个元素，在已经排序的元素位置从右向左扫描
3. 如果该元素\(已排序\)大于新的元素，则向右移动一个位置
4. 重复3步骤，知道该元素\(已排序\)小于或者等于新元素的位置
5. 将新元素插入该位置后
6. 重复步骤2-5，直至排序完成

```java
/**
 * Created by huangdaju on 17/7/27.
 */

public class InsertSort extends BubbleSort {

    public void insertSort(int[] data, MainActivity activity) {
        int n = data.length;
        int get;
        for (int i = 1; i < n; i++) {   //抓扑克牌
            get = data[i];  //右手抓到的牌

            for (int j = 0; j <= i - 1; j++) {      //拿在左手上的牌从0到i
                if (data[j] > get) {
                    exChange(data, i, j);
                    activity.onCallback();
                }
            }
        }
    }
}
```

## 插入排序之二分插入排序

对于插入排序，如果比较操作的代价与交换操作大的话，可以采用二分查找法来减少比较操作的次数。

代码如下：

```java
/**
 * Created by huangdaju on 17/8/2.
 */

public class MiddleInsertSort extends BubbleSort {

    public void middleInsertSort(int[] datas, MainActivity mainActivity) {
        int n = datas.length;
        int get;
        int left = 0, right = 0, j;

        for (int i = 0; i < datas.length; i++) {
            get = datas[i];
            left = 0;
            right = i - 1;
            while (left <= right) {
                int middle = (left + right) / 2;
                if (datas[middle] > get) {
                    left = middle + 1;
                } else {
                    right = middle - 1;
                }
            }

            for (j = i - 1; j >= left; j--) {
                {
                    datas[j + 1] = datas[j];
                }
                datas[left] = get;
                mainActivity.onCallback();
            }
        }
    }
}
```

当n较大的时候，二分插入排序的时间复杂度比直接插入排序最差的时间复杂度要好，但比直接插入排序最好时间复杂度要差；当以元素初始序列接近与升序，直接插入排序比二分插入排序的比较次数要少。

插入排序的更高效改进：希尔排序

