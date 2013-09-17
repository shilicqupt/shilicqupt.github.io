---
layout: post
title: IBM HeapAnalyzer
---

{{ page.title }}
================

<p class="meta">2013-9-17 - HZ China</p>
今天学习到了如何使用IBM HeapAnalyzer这个分析工具来对dump处的堆栈，从而去分析内存打满的原因。
首先需要了解IBM HeapAnalyzer这个工具的作用
    * 它可以解析堆栈文件，分解出其中的对象元素。
    * 可以根据解析出信息来生成图
    * 可以根据生成图来生成对象树
    * 可以使用java heap 泄露检查引擎来显示可疑的java heap泄露区域

-----------------------------

其次是具体操作步骤和分析过程 假设/path/xxx.bin为我们dump出的项目堆栈文件
    * 启动IBM HeapAnalyzer，一般堆栈文件都很大需要使用参数-Xmx调大启动的java heap空间，否则会出现OOM错误
    * 点击file标签，open我们的/path/xxx.bin导入堆栈信息，这是HeapAnalyzer就开始解析文件了
    * 解析完毕后可以下观察Console窗口来空heap总数
    * 可以点击Analysis标签来下面的选项来看具体哪些对象存在内存，占用比例，可以点击节点来看具体对象的信息
    * 可以右键点击节点选择Locate a leak suspect来看提示是否有内存泄露

-----------------------------------

  上面就是具体查找步骤了，其实最重要就是找到占用内存最多的对象实例，以及它所存放的对象实例，然后再具体程序中去Search用到容器或者对象的具体文件中去进行定位，因为HeapAnalyszer是无法帮助我们来进行定位具体的程序，只会告诉可能发生内存泄露的对象


[Discuss this post on Hacker News](http://news.ycombinator.com/item?id=3267432)
