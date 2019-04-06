---
title: vim搜索中的正则表达式
date: 2019-01-24 15:55:45
desc: vim搜索中的正则表达式
tags: vim, regexp
---

最近使用vim的搜索替换， 发现只是不够用，特意学习了下。

<!-- more -->

### vim中有个·magic·的东西

当然快速查看帮助： `help magic`

```bash
    magic (\m)：除了$ . * ^ 之外其他元字符都要加反斜杠。
    nomagic (\M)：除了 $ ^ 之外其他元字符都要加反斜杠。
    very magic (\v)：都必须加上反斜杠
    very nomagic (\V)：都不加反斜杠
```

help中拿过来的例子：

```bash

      $       $        $         \$        匹配行尾
      .       .        \.         \.        匹配任何字符
      *       *        \*         \*        前面匹配原的任意次重复
      ()       \(\)     \(\)     \(\)    组成为单个匹配原
      |       \|        \|         \|        分隔可选分支
      \a       \a        \a         \a        字母字符
      \\       \\        \\         \\        反斜杠 (按本义)
      \.       \.        .         .        英文句号 (按本义)
      \{       {        {         {        '{'  (按本义)
      a       a        a         a        'a'  (按本义)

```


默认设置的 `magic`

### 一些常用的量词， 元字符

这些量词，元字符需要自己记下。没办法，👐


量词：

```bash
*  匹配0个或多个(匹配优先)
\+ 匹配1个或多个(匹配优先)
\?或\= 0个或1个(匹配优先)，\?不能在 ? 命令（逆向查找）中使用
\{n,m} 匹配n个到m个(匹配优先),如\d{1, 3}可以匹配1到3个数字,类似1, 12, 123
\{n,} 最少n个(匹配优先)
\{,m} 最多m个(匹配优先
\{n} 恰好n个

```

元字符：

```bash
*  匹配任意一个字符
[abc] 匹配方括号中的1个字
[a-zA-Z0-9] 匹配所有大小写字母和数字
[^abc] 不匹配方括号中字符
\d 匹配数字 [0-9] 
\D 匹配非数字 [^0-9] 
\x 匹配16进制字符[0-9A-Fa-f] 
\w 匹配单个字符[a-zA-Z0-9] 
\W 匹配非单个字符 [^a-zA-Z0-9] 
\t 下写字符 [a-z] 
\L 非小写字符[^a-z] 
\u 大写字符 [A-Z]
\U 非大写的字符[^A-Z]
```



### 一些实用的例子

查找替换 `:%s/luo/wen/g` 全局把luo替换成wen `:%s/luo/wen/gc` 替换前每次询问

反向应用demo ` :%s/\(luo\) or \(wen\)/\2 or \1/ ` 将luo 和wen 相互交换

贪婪和非贪婪

```bash

demo: luowenoh

`:%s/\(l.\{-}o\)/hello(\1)/g` => hello(luo)wenoh

`:%s/\(l.*o\)/hello(\1)/g` => hello(luoweno)h

```