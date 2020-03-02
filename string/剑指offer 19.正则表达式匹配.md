## 问题

## 思路
直接贴[牛客上的思路](https://www.nowcoder.com/questionTerminal/45327ae22b7b413ea21df13ee7d6429c?answerType=1&f=discussion)
```
首先，考虑特殊情况：
     1>两个字符串都为空，返回true
     2>当第一个字符串不空，而第二个字符串空了，返回false（因为这样，就无法
        匹配成功了,而如果第一个字符串空了，第二个字符串非空，还是可能匹配成
        功的，比如第二个字符串是“a*a*a*a*”,由于‘*’之前的元素可以出现0次，
        所以有可能匹配成功）
之后就开始匹配第一个字符，这里有两种可能：匹配成功或匹配失败。但考虑到pattern
下一个字符可能是‘*’， 这里我们分两种情况讨论：pattern下一个字符为‘*’或
不为‘*’：
      1>pattern下一个字符不为‘*’：这种情况比较简单，直接匹配当前字符。如果
        匹配成功，继续匹配下一个；如果匹配失败，直接返回false。注意这里的
        “匹配成功”，除了两个字符相同的情况外，还有一种情况，就是pattern的
        当前字符为‘.’,同时str的当前字符不为‘\0’。
      2>pattern下一个字符为‘*’时，稍微复杂一些，因为‘*’可以代表0个或多个。
        这里把这些情况都考虑到：
           a>当‘*’匹配0个字符时，str当前字符不变，pattern当前字符后移两位，
            跳过这个‘*’符号；
           b>当‘*’匹配1个或多个时，str当前字符移向下一个，pattern当前字符
            不变。（这里匹配1个或多个可以看成一种情况，因为：当匹配一个时，
            由于str移到了下一个字符，而pattern字符不变，就回到了上边的情况a；
```
原贴是C++，这里给个Python版。
```python
class Solution:
    # s, pattern都是字符串
    def match(self, s, pattern):
        if s is None or pattern is None:
            return False
        if s == '' and pattern == '':
            return True
        if s != '' and pattern == '':
            return False
        if len(pattern) > 1 and pattern[1] == '*':
            if len(s) > 0 and (pattern[0] == s[0] or pattern[0] == '.'):
                return self.match(s[1:], pattern) or self.match(s, pattern[2:])
            else:
                return self.match(s, pattern[2:])
        # if len(pattern) > 1 and pattern[1] != '*':
        if len(s) > 0 and (pattern[0] == s[0] or pattern[0] == '.'):
            return self.match(s[1:], pattern[1:])
        return False
```
