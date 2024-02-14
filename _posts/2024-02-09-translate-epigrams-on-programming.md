---
layout: post
title: "Epigrams on Programming"
tags: 翻译 科普
---


Author：Alan J. Perlis, Yale, September 1980

The phenomena surrounding computers are diverse and yield a surprisingly rich base for launching metaphors at individual and group activities. Conversely, classical human endeavors provide an inexhaustible source of metaphor for those of us who are in labor within computation. Such relationships between society and device are not new, but the incredible growth of the computer's influence (both real and implied) lends this symbiotic dependency a vitality like a gangly youth growing out of his clothes within an endless puberty.

围绕计算机的现象是多种多样的，并且个人和群体活动提供了丰富的抽象基础。相反，传统事业也为我们这些在计算机领域工作的人提供了不尽的抽象资源。这种社会与设备的辩证关系并不新鲜，不过计算机表面上和本质上的影响力增长附带的生命力，像一个瘦高迂笨的青年卡在他的衣服里不断发育。

The epigrams that follow attempt to capture some of the dimensions of this traffic in imagery that sharpens, focuses, clarifies, enlarges, and beclouds our view of this most remarkable of all mans' artifacts, the computer.

下面的警句试图捕捉这种流量的一些维度，加重、聚焦、清晰、扩展和模糊我们对人类智慧的结晶——计算机的看法。

1. One man's constant is another man's variable.  
一个人的常量是另一个人的变量。

1. Functions tend to delay binding; data structures tend to induce binding. Moral: Structure data late in the programming process.  
函数往往延迟绑定，数据结构往往引起绑定。寓意：编程后期再结构化数据。

1. Syntactic sugar causes cancer of the semi-colons.  
语法糖导致分号癌。  
语法糖：采用简洁的方式来表示复杂的过程。

1. Every program is a part of some other program and rarely fits perfectly.  
每个程序都是其他程序的一部分，不过很少能完美契合。

1. If a program manipulates a large amount of data, it does so in a small number of ways.  
如果程序操作大量数据，它必然只采取了少量方式。

1. Symmetry is a complexity reducing concept (co-routines include sub-routines); seek it everywhere.  
对称性是一个降低复杂度的概念（协程包括子例程）；无处不在。  
协程：相当于可以中断，可以继续的函数。  
子例程：函数。

1. It is easier to write an incorrect program than understand a correct one.  
编写错误的程序比理解正确的程序更容易。

1. A programming language in which the irrelevant is as portentious as the critical in programs is a low order language.  
低级语言意味着其编写的程序中无关紧要的部分非常重要。

1. It is better to have 100 functions operate on one data structure than 10 functions on 10 data structures.  
100 个函数对 1 种数据结构进行操作比 10 个函数对 10 个数据结构进行操作要好。

1. Get into a rut early: Do the same processes the same way. Accumulate idioms. Standardize. The only difference (!) between Shakespeare and you was the size of his idiom list - not the size of his vocabulary.  
尽早形成规矩：一仍旧贯。积累定式。走标准化。你和莎士比亚唯一的区别（！）是成语量，不是词汇量。

1. If you have a procedure with 10 parameters, you probably missed some.  
如果你的过程有 10 个参数，那么可能还遗漏了一些参数。  
过程：语言层面的概念，包括编程语言和现实语言，是一串操作的统称，可能有参数或返回值。

1. Recursion is at the root of computation since it trades description for time.  
递归是计算的根源，因为它用描述换取时间。

1. If two people write exactly the same program, each should be put in micro-code and then they certainly won't be the same.  
如果两个人写一个完全相同程序，那么在微码上必然有所不同。  
微码：一种比汇编更加底层的低级语言，一条汇编会对应一条或多条微代码。

1. In the long run every program becomes rococo -- then rubble.  
程序会变得洛可可，然后是瓦砾堆。  
洛可可：细腻且繁复、华丽但过时，暗讽过于精致。  
瓦砾堆：理解为废弃。

1. Everything should be built top-down, except the first time.  
一切应该自上而下，第一次除外。

1. Every program has (at least) two purposes: the one for which it was written and another for which it wasn't.  
任何程序（至少）有两个目的：一个是编写的目的，另一个不是编写的目的。

1. If a listener nods his head when you're explaining your program, wake him up.  
如果一个人在你解释程序时一直点头，请叫醒他。

1. A program without a loop and a structured variable isn't worth writing.  
没有循环和结构体的程序不值得写。

1. If a language doesn't affect the way you think about programming, it's not worth knowing.  
不影响编程思考方式的语言不值得了解。

1. Wherever there is modularity there is the potential for misunderstanding: Hiding information implies a need to check communication.  
模块引起误解：隐藏信息意味着检查通信。  

1. Optimization often delays evolution.  
优化延迟进化。  

1. A system is a collection of weakly interacting procedures that, in various combinations, perform a varietoy functions, in short, a system is a (general purpose?) computer. Hence the command language (order code) is critical. A good system can't have a weak command language.  
系统是弱交互过程的集合，这些过程相互组合执行各种功能，简而言之，系统是一台（通用？）计算机。因此命令行至关重要。好系统不会有差命令行。

1.  To understand a program you must become the machine that executes it, often the programs that process it.  
为了理解程序，你要成为执行它的机器，通常还要成为处理它的程序。

1. Perhaps if we wrote programs from childhood on, as adults we'd be able to read them. However, reading a program is not like reading a book, it is more like being a psychiatrist to a recumbent patient.  
如果我们从小开始写程序，长大后我们就能读懂它们。不过读懂程序不像读书，倒像精神科医生读卧着的病人。

1. One can only display complex information in the mind. Like seeing, movement or flow or alteration of view is more important than the static picture, no matter how lovely.  
思维才能呈现复杂信息。就像视觉中，物体转移、景观流动、视角改变都比静态的优美图片更重要。

1. There will always be things we wish to say in our programs that in all languages can only be said poorly.  
程序中总有一些我们想表达但难以表达的。

1. Once you understand how to write a program get someone else to write it.  
如果理解如何编写一个程序，不妨让别人来编写它。

1. Around computers it is difficult to find the correct grain of time to measure progress. Some cathedrals took a century to complete. Can you imagine the grandeur and scope of a program that would take as long?  
很难找到正确的时间尺度来衡量计算机相关的进展。有的教堂建了一个世纪。你能想象一个写了一个世纪的程序的壮丽宏大吗？

1. For systems, the analogue of a face-lift is to add to the control graph an edge that creates a cycle, not just toan additional node.  
系统的整容是流程图上加一条创造循环的边，不是加一个点。

1. In programming, everything we do is a special case of something more general -- and we often know it too quickly.  
编程中，我们常常过早了解到，我们所做的都是普遍情况的特例。

1. Simplicity does not precede complexity, but follows it.  
先呈现复杂性，再体现简洁性。

1. Good Programmers are not so much to be measured by their ingenuity and their logic as the completeness of their case analysis.  
优秀的程序员不能用优秀的才智和逻辑衡量，而是用分析问题的完整性。

1. The 11th commandment was "Thou Shalt Compute" or "Thou Shalt Not Compute" -- I forget which.  
第十一诫是「你应该计算」或「你不应该计算」——我忘了是哪个了。
《圣经》十诫，这里作者弄了第十一诫。  

1. The string is a stark data structure and everywhere it is passed there is much duplication of process. It is a perfect vehicle for hiding information.  
字符串是缓慢的数据结构，传递它的过程中有很多重复的过程。字符串是隐藏信息的完美工具。  
两句话无关吧？

1. Everyone can be taught to sculpt: Michelangelo would have had to be taught how not to. So it is with the great programmers.  
所有人学习雕刻：米开朗基罗必须学习如何不雕刻，优秀的程序员也是。

1. The use of a program to prove the 4-color theorem will not change mathematics -- it merely demonstrates that the theorem, a challenge for a century, is probably not important to mathematics.  
使用程序证明四色定理不会改变数学——只证明了这个百年未解的数学难题实际上对数学并不重要。

1. The most important computer is the one that rages in our skulls and ever seeks that satisfactory external emulator. The standardization of real computers would be a disaster -- and so it probably won't happen.  
最重要的计算机是在我们脑海中蔓延的，寻找令人满意的外部模拟的计算机。现实中这种计算机的标准化是场灾难，所以这不会发生。

1. Structured Programming supports the law of the excluded muddle.  
结构化编程支持排乱律。  
排中律：所有命题非真即假。排乱律：非整齐即更加混乱？

1. Re graphics: A picture is worth 10K words -- but only those to describe the picture. Hardly any sets of 10K words can be adequately described with pictures.  
关于图形：一张图片抵得上 10K 的单词，但仅限描述图片的单词。几乎没有 10K 的单词的集合可以用图片充分描述。

1. There are two ways to write error-free programs; only the third one works.  
有两种方法能编写无错误程序：只有第三种有效。

1. Some programming languages manage to absorb change, but withstand progress.

1. You can measure a programmer's perspective by noting his attitude on the continuing vitality of FORTRAN.  
你可以通过一个程序员对延续 FORTRAN 的态度衡量他的观点。

1. In software systems it is often the early bird that makes the worm.  
在软件系统中，往往是早起的鸟儿产生虫子。

1. Sometimes I think the only universal in the computing field is the fetch-execute cycle.  
有时我认为计算机领域唯一通用的是「取址-执行」循环

1. The goal of computation is the emulation of our synthetic abilities, not the understanding of our analytic ones.  
计算的目标是对综合能力的模拟，而不是对分析能力的理解。  
分析是把事物分解为各个部分、侧面、属性，分别加以研究。是认识事物整体的必要阶段。综合是把事物各个部分、侧面、属性按内在联系有机地统一为整体，以掌握事物的本质和规律。

1. Like punning, programming is a play on words.  
就像双关游戏一样，编程也是文字游戏。

1. As Will Rogers would have said, "There is no such thing as a free variable."  
正如 Will Rogers 所说：「不存在自由变量。」

1. The best book on programming for the layman is "Alice in Wonderland"; but that's because it's the best book.  
对于外行人来说最好的编程书是《爱丽丝漫游仙境》，不过那是因为这是最好的书。

1. Giving up on assembly language was the apple in our Garden of Eden: Languages whose use squanders machine cycles are sinful. The LISP machine now permits LISP programmers to abandon bra and fig-leaf.  
放弃汇编是伊甸园的苹果：使用汇编的

1. When we understand knowledge-based systems, it will be as before -- except our finger-tips will have be singed.  

1. Bringing computers into the home won't change either one, but may revitalize the corner saloon.

1. Systems have sub-systems and sub-systems have sub-systems and so on ad finitum -- which is why we're always starting over.  
系统有子系统，子系统有孙系统，子子孙孙无穷尽也——这也是为什么我们总是从头开始。

1. So many good ideas are never heard from again once they embark in a voyage on the semantic gulf.  
许多好的想法一旦踏入语义的深渊，就销声匿迹了。

1. Beware of the Turing tar-pit in which everything is possible but nothing of interest is easy.  
当心图灵焦油坑，虽然它能做到一切，但没有一件有趣的事是简单的。  
图灵焦油坑：图灵完备的阴间语言，如 brainfuck，COW，Whitespace。

缓更……