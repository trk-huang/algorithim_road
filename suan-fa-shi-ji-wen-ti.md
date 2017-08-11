# 最长回文字符串

回文串就是一个正读和反读都一样的字符串，比如“level”、“noon”等等的回文串。回文子串，即字符串中满足回文串的子字符串。比如“google”中的“goog”就是这个字符串中最长的回文子串。

1.问题的解决基本方法

分析：要判断一个字符串是不是对称，不是一件很难的事。我们可以先得到首尾字符，判断是不是相等的。如果不相等，则不是对称字符串；如果相等，判断里面的字符，以此类推。

```java
def longestPailindrome(str):
    n = len(str)
    maxL,maxR,max = 0,0,0
    for i in range(n):
        start = i
        end = i + 1
        while start >=0 and end < n:
            if str[start] == str[end]:
                if end - start > max:
                    max = end - start + 1
                    maxL = start
                    maxR= end
                start -= 1
                end += 1
            else:
                break
        start = i -1
        end = i+1
        while start >=0 and end < n:
                if str[start] == str[end]:
                    if end - start > max:
                        max = end - start + 1
                        maxL = start
                        maxR = end 
                    start -= 1
                    end += 1
                else:
                    break    
    print max
    return str[maxL:maxR+1]
```

java代码实现：

```java
private String longestPailindrome(String str) {
        char[] chars = str.toCharArray();
        int maxL = 0, maxR = 0, max = 0;
        int n = chars.length;
        for (int i = 0; i < n; i++) {
            int start = i;
            int end = i + 1;
            while (start >= 0 && end < n) {
                if (chars[start] == chars[end]) {
                    if (end - start > max) {
                        max = end - start;
                        maxL = start;
                        maxR = end;
                    }
                    start -= 1;
                    end += 1;
                } else {
                    break;
                }
            }
            start = i - 1;
            end = i + 1;
            while (start >= 0 && end < n) {
                if (chars[start] == chars[end]) {
                    if (end - start > max) {
                        max = end - start;
                        maxL = start;
                        maxR = end;
                    }
                    start -= 1;
                    end += 1;
                } else {
                    break;
                }
            }

        }

        if (maxL >= 0 && maxR < n) {
            return str.substring(maxL, maxR + 1);
        } else
            return null;
    }
```

#### Manacher's ALGORITHM: O\(n\)时间求字符串的最长回文子串

主要原理是把所有可能的奇数/偶数的回文字符串都转换成奇数长度：在每个字符的两边都插入一个特殊字符。比如“abba”，改为“\#a\#b\#b\#a\#”,"aba"改为"\#a\#b\#a\#"。为了防止数组越界，我们在改后的字符串中加入"$",改为”$\#a\#b\#b\#a\#",然后我们用一个数组p\[\],来记录已字符S\[i\]为中心的最长回文串。如下列:

```java
S = [#,a,#,b,#,b,#,a,#]
P = [1,2,1,2,5,2,1,2,1]
```

那么怎么算p\[i\]呢，该算法添加两个变量id,mx，其中id为已知的{右边界最大}的回文串中心，mx=id+p\[id\],也就是这个子串的右边界，然后我们可以得出一个非常神奇的结论：如果mx &gt; i,那么p\[i\]&gt;=Min\(p\[2\*id-1\],mx-i\):

```java
if(mx - i > p[j]){
    p[i] = p[j];
}else{
    p[i] = mx - i;

}
```

当然光看代码还是不够清晰的，还是要借助图来理解比较容易。

当mx - i &gt; p\[j\]的时候，以S\[j\]为中心的回文子串包含在以S\[id\]为中心的回文子串中，由于i和j对称，以S\[i\]为中心的回文子串必然包含在以S\[id\]为中心的回文子串中，所以必有P\[i\] = P\[j\]

```python
def manacher(s):
    #预处理
    s='#'+'#'.join(s)+'#'

    RL=[0]*len(s)
    MaxRight=0
    pos=0
    MaxLen=0
    for i in range(len(s)):
        if i<MaxRight:
            RL[i]=min(RL[2*pos-i], MaxRight-i)
        else:
            RL[i]=1
        #尝试扩展，注意处理边界
        while i-RL[i]>=0 and i+RL[i]<len(s) and s[i-RL[i]]==s[i+RL[i]]:
            RL[i]+=1
        #更新MaxRight,pos
        if RL[i]+i-1>MaxRight:
            MaxRight=RL[i]+i-1
            pos=i
        #更新最长回文串的长度
        MaxLen=max(MaxLen, RL[i])
    return MaxLen-1
```



