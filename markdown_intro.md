

## 更新

### 怎么调整表格

* 用style标签  没用
* 用html，比较麻烦

```html
<table>
    <tr>
        <th style="width:100px">名称</th>
        <th>值</th>
        <th>备注</th>
    </tr>
    <tr>
        <th>hellp</th>
    </tr>
</table>

```

<table>
    <tr>
        <th style="width:100px">名称</th>
        <th>值</th>
        <th>备注</th>
    </tr>
    <tr>
        <th>hell0</th>
        <th>oooooooooooooooo</th>
        <th>d</th>
    </tr>
</table>

* 还是用暴力方法吧

  加空格符：&nbsp; &nbsp; &nbsp; "&nbsp"&nbsp;








## 标题

**使用 # 号标记**

使用 **#** 号可表示 1-6 级标题，一级标题对应一个 **#** 号，二级标题对应两个 **#** 号。

```markdown
# 一级标题
## 二级标题
### 三级标题
```



## 字体

```markdown
*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___
```



## 段落格式

### 分隔线

可以在一行中用三个以上的星号、减号、底线来建立一个分隔线

```markdown
****
----
___
```

***

---

____

### 删除线

在文字的两端加上两个波浪线 **~~** 

```markdown
hello
~~hello~~
```

### 下划线

可以通过 HTML 的 **<u>** 标签来实现

```markdown
hello
<u>hello</u>
```

<u>hello</u>



### 脚注

```markdown
脚注[^hello]
[^hello]:内容
```

脚注[^hello]

[^hello]:内容



## 列表

### 无序列表

无序列表使用星号(*****)、加号(**+**)或是减号(**-**)作为列表标记

```markdown
* 第一
* 第二
```

* 第一
* 第二

### 有序列表

有序列表使用数字并加上 **.** 号来表示

```markdown
1.first
2.second
```

### 列表嵌套

列表嵌套只需在子列表中的选项添加四个空格即可

```
1. 第一项：
	* 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
```

1. 第一项：
	* 第一项嵌套的第一个元素
   
    - 第一项嵌套的第二个元素



## 区块

在段落开头使用 **>** 符号 ，然后后面紧跟一个**空格**符号：

```
> 这是一个区块
> 这是一个区块
> > 嵌套区块1
> > 嵌套区块1
```

> 这是一个区块
> 这是一个区块
> > 嵌套区块1
> > 嵌套区块1

### 列表中使用区块

如果要在列表项目内放进区块，那么就需要在 **>** 前添加四个空格的缩进

* 列表

  > 区块
  >
  > 



## 代码

### 代码片段

反引号把它包起来（**`**）

```
函数`print("hello")`
```

函数`print("hello")`

### 代码块

**使用（```)**

```
​```python
R = input('>')
print(R)
```

效果如下：

```python
R = input('>')
print(R)
```



## 链接

```
[链接名称](链接地址)
or
<链接地址>
```

百度链接：[百度](www.baidu.com)

<www.baidu.com>

### 高级链接

```markdown
链接也可以用变量来代替，文档末尾附带变量地址：
这个链接用 1 作为网址变量 [Google][1]
这个链接用 b 作为网址变量 [baidu][b]
然后在文档的结尾为变量赋值（网址）

  [1]: http://www.google.com/
  [b]:www.baidu.com
```

链接也可以用变量来代替，文档末尾附带变量地址：
这个链接用 1 作为网址变量 [Google][1]
这个链接用 b 作为网址变量 [baidu][b]
然后在文档的结尾为变量赋值（网址）

[1]: http://www.google.com/
[b]:www.baidu.com



## 图片

Markdown 图片语法格式如下：

```markdown
![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")
```

- 开头一个感叹号 !
- 接着一个方括号，里面放上图片的替代文字
- 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的 'title' 属性的文字。



```markdown
![Google 图标](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png  "helo")
```

![Google 图标](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png"helo")

[谷歌图标][2]

[2]:https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png

### 指定图片大小

```
<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="10%" >
```

<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="10%">

### 给图片加上链接

```markdown
[![Google 图标](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)](www.google.com)
```

[![Google 图标](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)](www.google.com)



## 表格

制作表格使用 **|** 来分隔不同的单元格，使用 **-** 来分隔表头和其他行。

```markdown
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

| 表头   | 表头   |
| ------ | ------ |
| 单元格 | 单元格 |
| 单元格 | 单元格 |



### 对齐方式

- **-:** 设置内容和标题栏居右对齐。
- **:-** 设置内容和标题栏居左对齐。
- **:-:** 设置内容和标题栏居中对齐。

```
| 左对齐 | 居中对齐 | 右对齐 |
| :----- | :------: | -----: |
| hello  |  hello   |  hello |
```

| 左对齐 | 居中对齐 | 右对齐 |
| :----- | :------: | -----: |
| hello  |  hello   |  hello |



## 高级技巧

### 支持的 HTML 元素

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。

目前支持的 HTML 元素有：` <b> <i> <em> <sup> <sub> <br>`等

```markdown
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
<b>hello</b>
```

使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
<b>hello</b>



### 转义

使用反斜杠转义特殊字符

```markdown
* 列表
\*
```

* 列表
\*

### 公式

当你需要在编辑器中插入数学公式时，可以使用两个美元符 $$ 包裹 TeX 或 LaTeX 格式的数学公式来实现。提交后，问答和文章页会根据需要加载 Mathjax 对数学公式进行渲染。

```latex
$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
$$
```

$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$