# Xcode查找和替换技巧
### 举例说明
替换以下代码

```
***{ [unowned self] *****
//code
}
```
为

```
***{ [weak self] *****
guard let `self` = self else {return}
//code
}
```
正则表达式一栏就要这样写

```
(\[unowned self\])(.*)([\s]+)
```
替换那一栏就要这样写

```
[weak self]$2$3guard let `self` = self else {return}$3
```
##### 解释

正则表达式一栏中`\[unowned self\]`表示匹配字符串`[unowned self]`，其中`[]`需要转义，`.*`表示匹配出 **换行符** 以外的字符，`[\s]+`表示匹配至少一个空字符，贪婪模式，直到遇到非空字符。分别加括号表示变量，变量下标从 **1** 开始。替换那一栏`[weak self]`字符串加上变量 **2** （就是`(.*)`)匹配到的部分，再加上变量 **3** （就是`([\s]+)`)匹配到的部分，再加上自己的语句`guard let `self` = self else {return}`，最后再加上变量 **3** （就是`([\s]+)`)匹配到的部分。最后加一次是为了让代码对齐。


