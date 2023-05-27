## 问题

写一个函数 StrToInt，实现把字符串转换成整数这个功能。不能使用 atoi 或者其他类似的库函数。

 

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。



## 示例

```
输入: "4193 with words"
输出: 4193

输入: "words and 987"
输出: 0
```





## 代码

考虑四种字符

1. 首部空格：删除

2. 符号位：“+”、“-”、“无符号"；新建变量保存符号位

3. 非数字：首次遇到，返回

4. 数字符号：拼接公式

   设当前字符 <i>c</i>，当前数字 <i>x</i>，数字结果 <i>res</i>，则拼接公式为：

   ```matlab
   res = 10 * res + x
   x = ascii(c) - ascii('0')
   ```

结果越界处理

返回结果的数值范围应在[-2^31, 2^31 - 1].若越界，要始终爆出 <i>res</i>在int类型的取值范围内。

​	在数字拼接前，判断 <i>res</i> 拼接后是否超过2147483647，设数字拼接边界bndry = 2147483647 // 10 = 214748364,则

+ res > bndry              拼接 10 * res ≥ 2147483647 越界
+ res = bndry, x > 7    拼接后是2147483648 、 2147483649



```java
class Solution {
    public int strToInt(String str) {
        char[] ch = str.trim().toCharArray();
        if(ch.length == 0) return 0;
        int res = 0, bndry = Integer.MAX_VALUE / 10;
        int i = 1, sign = 1;
        
        if(ch[0] == '-') sign = -1;
        else if(ch[0] != '+') i = 0;
        for(int j = i; j < ch.length; j++) {
            if(ch[j] < '0' || ch[j] > '9') break;
            if(res > bndry || res == bndry && ch[j] > '7') return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            res = res * 10 + (ch[j] - '0');
        }
        
        return sign * res;
    }
}
```

