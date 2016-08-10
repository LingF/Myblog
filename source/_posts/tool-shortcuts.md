title: 工欲其善必先利其器
date: 2015-12-11 15:30:24
tags: [工具, 插件]
---

# 工具快捷键整理
## 总有原因的
工具永远是<del>人类</del>最好的伙伴，有了工具可以干许多事情不费力，腿脚利索了，牙齿也倍棒，当然很多好处举不胜数。工具用的好必须靠快捷键记得牢，按起来嗖嗖嗖地逼格绝对高，效率也是杠杠滴。
## 速查表
| 目的          | 描述          | 快捷键 |
| ------------- |:-------------:| -----: |
| 选择          | 选择一个选中项的下一个匹配项    | Ctrl + D (⌘ + D) |
|               | 选择一个选中项的所有匹配项      | Alt + F3 (CTRL + ⌘ + G) |
|               | 选择与光标关联的开始和结束标签  | Ctrl + Shift + ‘ (⌘ + ⇧ + K) |
|               | 选择容器内内容                  | Ctrl + Shift + A (CTRL + D) |
|               | 选择括号内的内容                | Ctrl + Shift + M (⌘ + ⇧ + Space) |
|               | 选择整行或多行                  | Ctrl + L () |
| 移动、操作行和文本 | 上移或下移行 | Ctrl + Shift + ↑ 或 ↓ (CTRL + ⌘ + ↑ 或 ↓) |
|                    | 复制 行或选中项 | Ctrl + Shift + d (⌘ + ⇧ + D) |
|                    | 增加和减少缩进  | Ctrl + [ 或 ] (⌘ + [ 或 ]) |
|                    | 插入新行        | Ctrl + Enter or Ctrl + Shift + Enter |
| 剪切和删除，复制和粘贴 | 剪切行或选中项 | Ctrl+x (⌘ + X) |
|                        | 粘贴并保持缩进 | Ctrl + Shift + V (⇧ + ⌘ + V) |
|                        | 用标签包裹行或选中项 | Alt + Shift + W (CTRL + ⇧ + W) |
|                        | 移除容器元素 | Ctrl + Shift + ; (⌘ + ’) |
| 文本和数字操作         | 计算数学表达式 | Ctrl + Shift + Y (⌘ + ⇧ + Y) |
|                        | 递增和递减 | Alt + Shift + ↑ 或 ↓，ctrl+ ↑ 或 ↓ (⇧ + OPTION + ↑ or ↓, OPTION + ↑ or ↓) |
|                        | 大写和小写 | Ctrl + K + U, Ctrl + K + L (⌘ + K then U, ⌘ + K then L) |
| 折叠和展开             | 折叠 | Ctrl + Shift + [ () |
|                        | 展开 | Ctrl + Shift + ]，Ctrl + K + 0 () |
|                        | 注释选中项/行 | Ctrl + / (⌘ + /) |
| _Emmet_ | | |
| 生成标签编号 | 正常序号 | ul>li.item$*3 |
|              | 多位数   | ul>li.item$$$*3 |
|              | 倒序     | ul>li.item$@-*3 |
|              | 指定开始(同样可以倒序) | ul>li.item$@2*3 |
| 生成文本内容 | 一般内容 | a[href=”xxx“]{内容} |
|              | 嵌套内容 | div>{内容}+a{标题} |
|              | 平行内容 | div{内容}+a{标题} |
|              | 随机大段文字(默认30个单次) | lorem (直接Tab) |
|              | 随机标题(限定单次数) | h2>lorem4 |
| 扩展缩写     | 基础 | h2>lorem4 / .page>h3{Title}+.content |
|              | 提供文本 | nav>ul.nav>li.nav-item$*>a |
|              | 去掉默认编号 | nav>ul.nav>li.nav-item$*>a(竖线)t |
|              | 文本复用 | ul>li[title= $# ]*>{ $# }+img[alt= $# ] |

## Sublime Text 快捷键

### 选择
<!-- <h3 id="st1"></h3> -->

#### 选择一个选中项的下一个匹配项
> Ctrl + D (⌘ + D)

![选择一个选中项的下一个匹配项](/uploads/i/1.gif "p1")

这里有个扩展需求：就是可能不想选择选中项或者某一项，那就在选中该项时按下 Ctrl + K，然后继续 Ctrl + D 就会跳过该项。

---
#### 选择一个选中项的所有匹配项
> Alt + F3 (CTRL + ⌘ + G)

![选择一个选中项的所有匹配项](/uploads/i/2.gif "p2")

---
#### 选择与光标关联的开始和结束标签
> Ctrl + Shift + ' [注意: ( ' ) 是回车边上的单引号那个键] (⌘ + ⇧ + K)

![选择与光标关联的开始和结束标签](/uploads/i/3.gif "p3")

---
#### 选择容器内内容(需要Emmet插件)
把光标放在文本间，按下快捷键。
> Ctrl + Shift + A (CTRL + D)

![选择容器内内容(需要Emmet插件)](/uploads/i/4.gif "p4")

---
#### 选择括号内的内容(适用js/css)
> Ctrl + Shift + M (⌘ + ⇧ + Space)

![选择括号内的内容(适用js/css)](/uploads/i/5.gif "p5")

---
#### 选择整行或多行
选中整行，继续操作则继续选择下一行，效果同 Shift + ↓。
> Ctrl + L ()

---
### 移动行和文本
<!-- <h3 id="st2"></h3> -->

#### 上移或下移行
> Ctrl + Shift + ↑ 或 ↓ (CTRL + ⌘ + ↑ 或 ↓)

![上移或下移行](/uploads/i/6.gif "p6")

---
#### 复制 行或选中项
如果你已经选中了文本，它会复制你的选中项。否则会复制整行。
> Ctrl + Shift + d (⌘ + ⇧ + D)

![复制 行或选中项](/uploads/i/7.gif "p7")

---
#### 增加和减少缩进
> Ctrl + [ 或 ] (⌘ + [ 或 ])

![增加和减少缩进](/uploads/i/8.gif "p8")

---
#### 插入新行
上一行或下一行插入新行
> Ctrl + Enter or Ctrl + Shift + Enter

---
### 剪切和删除，复制和粘贴
<!-- <h3 id="st3"></h3> -->

#### 剪切行或选中项
> Ctrl+x (⌘ + X)

![剪切行或选中项](/uploads/i/9.gif "p9")

---
#### 粘贴并保持缩进
基本可以替代 Ctrl + V，保持复制时的缩进(观察gif中差异)。
> Ctrl + Shift + V (⇧ + ⌘ + V)

![粘贴并保持缩进](/uploads/i/10.gif "p10")

---
#### 用标签包裹行或选中项
> Alt + Shift + W (CTRL + ⇧ + W)

![用标签包裹行或选中项](/uploads/i/11.gif "p11")

---
#### 移除容器元素
> Ctrl + Shift + ; (⌘ + ’)

![移除容器元素](/uploads/i/12.gif "p12")


---
### 文本和数字操作
<!-- <h3 id="st4"></h3> -->

#### 计算数学表达式
> Ctrl + Shift + Y (⌘ + ⇧ + Y)

![计算数学表达式](/uploads/i/13.gif "p13")


---
#### 递增和递减
两种不同的方式，代表10或1两种不同的步长增减最近的数字(无空格)。
> Alt + Shift + ↑ 或 ↓，ctrl+ ↑ 或 ↓ (⇧ + OPTION + ↑ or ↓, OPTION + ↑ or ↓)

![递增和递减](/uploads/i/14.gif "p14")


---
#### 大写和小写
> Ctrl + K + U, Ctrl + K + L (⌘ + K then U, ⌘ + K then L)

![大写和小写](/uploads/i/15.gif "p15")


---
### 折叠和展开
<!-- <h3 id="st5"></h3> -->
#### 折叠
> Ctrl + Shift + [ ()

---
#### 展开
前者展开当前折叠，后者展开所有折叠
> Ctrl + Shift + ]，Ctrl + K + 0 ()


---
#### 注释选中项/行
> Ctrl + / (⌘ + /)

![注释选中项/行](/uploads/i/16.gif "p16")


---
### 扩展
<!-- <h3 id="st6"></h3> -->
#### AlignTab自定义快捷键
安装 AlignTab, ,添加自定义绑定到您的自定义键绑定文件中,选择一些代码,并点击CTRL + ⇧ + . 或 ; 或 =

![AlignTab自定义快捷键](/uploads/i/17.gif "p17")

---

---
## Emmet 技巧

### 生成标签编号
#### 正常序号
> ul>li.item$*3

    <ul>
      <li class="item1"></li>
      <li class="item2"></li>
      <li class="item3"></li>
    </ul>

#### 多位数
> ul>li.item$$$*3

    <ul>
      <li class="item001"></li>
      <li class="item002"></li>
      <li class="item003"></li>
    </ul>

#### 倒序
> ul>li.item$@-*3

    <ul>
      <li class="item3"></li>
      <li class="item2"></li>
      <li class="item1"></li>
    </ul>

#### 指定开始(同样可以倒序)
> ul>li.item$@2*3

    <ul>
      <li class="item2"></li>
      <li class="item3"></li>
      <li class="item4"></li>
    </ul>

---
### 生成文本内容
#### 一般内容
> a[href=" http: //www.baidu.com "]{点击这里到 百度}

    <a href="http://www.baidu.com">点击这里到 百度</a>

#### 嵌套内容
> div>{内容}+a{标题}

    <div>内容<a href="">标题</a></div>

#### 平行内容
> div{内容}+a{标题}

    <div>内容</div>
    <a href="">标题</a>

#### 随机大段文字(默认30个单次)
> lorem (直接Tab)

#### 随机标题(限定单次数)
> h2>lorem4

    <h2>Lorem ipsum dolor sit.</h2>

> p*3>lorem4

    <p>Lorem ipsum dolor sit.</p>
    <p>Ratione accusantium minus ullam.</p>
    <p>Nisi ex assumenda totam.</p>

---
### 扩展缩写
#### 基础
光标在下面的P上按下Shift + Ctrl + G

    <div id="view">
      <p>Hello world</p>
    </div>

> .page>h3{Title}+.content

    <div id="view">
      <div class="page">
        <h3>Title</h3>
        <div class="content">
          <p>Hello world</p>
        </div>
      </div>
    </div>

#### 提供文本
> nav>ul.nav>li.nav-item$*>a

    首页
    公司简介
    公司动态
    关于我们
    联系我们

转换 ↓

    <nav>
      <ul class="nav">
        <li class="nav-item1"><a href="">首页</a></li>
        <li class="nav-item2"><a href="">公司简介</a></li>
        <li class="nav-item3"><a href="">公司动态</a></li>
        <li class="nav-item4"><a href="">关于我们</a></li>
        <li class="nav-item5"><a href="">联系我</a></li>
      </ul>
    </nav>
注意，导航中有5个菜单，这里不需要在li标签后面使用\*5，只需使用单独的操作符\*就可以

#### 去掉默认编号
添加 |t 就可以删除文本中的标记
> nav>ul.nav>li.nav-item$*>a|t

#### 文本复用
使用 $# 操作符Emmet可以将文本输出到多个元素中，需将 $# 放在属性值 [ ] 或文本 { } 操作符中
> ul>li[title= $# ]*>{ $# }+img[alt= $# ]

    <ul>
      <li title="首页">首页<img src="" alt="首页"></li>
      <li title="公司简介">公司简介<img src="" alt="公司简介"></li>
      <li title="公司动态">公司动态<img src="" alt="公司动态"></li>
      <li title="关于我们">关于我们<img src="" alt="关于我们"></li>
      <li title="联系我们">联系我们<img src="" alt="联系我们"></li>
    </ul>