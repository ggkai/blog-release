---
title: markdown常用技巧
date: 2018-10-16 22:20:59
tags: 工作
---
记录一下markdown用到的语法
<!-- more -->

# 一、标题
>#一级标题  
##二级标题  
###三级标题  
####四级标题  
#####五级标题  
######六级标题  

# 二、换行
>文字后面两个空格表示换行

# 三、列表
无序列表
>-空格 
- 无序列表 
- 无序列表
- 无序列表

有序列表
>数字加点（.）空格
1. 你好
2. 你好
3. 你好

嵌套列表
>下级缩进3个空格，-和+都可以

- 你好   
   + 你好
   + 你好
      + 你好
# 四、分割线
>换行---分割线

# 五、引用
>\>一层引用
>>\>>二层嵌套引用
>>>\>>>三层嵌套引用

# 六、转义
>\反斜杠转义

# 七、文字
斜体
>\*内容\*

*斜体举例*

粗体
>\*\*内容\*\*

**粗体举例**


# 八、链接
超链接
>\[名字](URL)

[百度](www.baidu.com)

图片
>\！[名字｝(URL）

![markdown](https://justyy.com/wp-content/uploads/2016/01/markdown-syntax-language.png)

自动链接
>\<链接>

<wwww.baidu.com>

参考链接
>内容：[链接文字][数字标记]  
空一行  
参考：[数字标记]:链接地址

[百度][1]

[1]: www.baidu.com

# 九、目录
>\[TOC] 独占一行

# 十、其他
1、表格  
http://www.ituring.com.cn/article/3452

2、锚点  
首先是建立一个跳转的连接，然后标记要跳转到什么位置即可，文字颜色可随意设置。

<a href="#jump" target="_self">说明文字</a>

<span id = "jump"><font color="red">跳转到这里</font></span>

3、代码块
tab缩进，即4个空格  
shift+tab，反缩进

