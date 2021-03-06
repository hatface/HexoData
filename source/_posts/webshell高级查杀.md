title: "webshell高级查杀"
id: 16
date: 2012-07-01 02:13:29
tags: 
- Return
- webshell
- 入侵
- 渗透
categories: 
- 技术文章
---


##很多人一直注重于攻击，而轻视于防御。

>攻击在于创新，防御在于全面。

>用计算机的术语来说，攻是个单线程任务，你单核cpu频率越高，则效果愈好。

>防则是个多线程任务，你cpu核心越多，则效果俞佳。

##下面说webshell的查杀

- 其实和pc一样，如安卓的恶意捆绑木马 和linux的恶意镜像源。一样的道路，web也要过一遍，pc端杀毒也是几个阶段。

- 从最初的专杀到特征码查杀再到基于行为的查杀（启发式查杀），再到最近炒得火热的云查杀。

- 说句题外话：所谓的云查杀更像是基于网络的特征码查杀。

- 同理：服务器上的webshell查杀也需要走特征码的路线，在现在硬件水平高于网络通信带宽的情况下，特征码还是非常必要的，接下来的就是讲webshell的特征码问题。
<!--more-->
- 依据pc端病毒特征码的原理：根据执行文件如PE文件，从各个段提出多个特征码进行多对一的映射定位（这个主要是为了防止类此myccl之类的过免杀），这种提取的方式有很多种，大部分高效的做法还是经验丰富的病毒分析师凭经验定位特征码。

- 如PC端病毒特征码类似，但又不尽相同，pc端的病毒是以执行文件存在的，提取特征码只是在机器码-反汇编代码的基础上进行定位的。

- 而webshell是以源码的形式进行定位。机器码是最底层的语言，定的很死，比如我们od中常用的int3 就是0cch一一对应，不会再变。

- 而webshell使用高级脚本语言，高级语言的写法是存在多样性，如php中的各种字符串操作函数，这无疑增加了定位特征码的难度。

- 其实，现实是这样的对于大马的查杀是相对容易的，无论php，asp,.net的大马，他们中调用的一些函数是普通脚本代码不会用到，所以可以以这些特殊函数为正则匹配规则，进行匹配。（大部分的服务器安全软件也是这样做的）当然这样做的结果，会出现误杀的情况，因此要借用多重特征码进行匹配。一些做免杀的朋友，可能就笑了，这太好过了，直接做下字符串拆分，然后在连接，或者写个加解密，再或者加混淆代码轻松就过了。


- 这样理论上是对的，但是实际中忽略了电脑硬件的能力，对于2^32的运算一般配置的电脑也不会超过10秒，对于各种字符串加解密我们可以对与加解密运算的字符进行匹配，然后查杀设计要加入语义分析，如果学过编译原理的应该熟悉，对匹配到的字符串加减操作进行还原进行最终的匹配。

- 对于一句话木马的查杀则比较麻烦，因为变异的一句话木马有些是用的web应用程序正常调用的函数，再加上些变形，查杀是比较棘手，这种查杀则需要进行大量的样本收集，对其进行特征码提取。

- 特征码的提取可采用统计学中的采样方法，取一定数量的样本（包括正常样本和网马样本），对其进行异样提取，再对各类样本进行同样提取，再通过出现概率在进行添加。最终生成特征码样本。

这样基本对已知存在的一句话木马匹配到。

对于特征码的匹配算法尚在测试中。

欢迎提供更多的webshell样本.

原创作者：livers   blog:   http://livers.sinaapp.com
