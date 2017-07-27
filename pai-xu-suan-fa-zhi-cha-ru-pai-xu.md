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



