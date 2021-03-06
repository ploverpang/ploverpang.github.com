---
title: 重构感悟——写出皮实可靠的工业代码
date: 2017-09-1 00:00:00
categories: 技术博文
tags: [reading]
---

本来计划半个月的软件代码重构，昨天终于结束，发布了2.0-beta版本的ADAS，整整最终多用了一倍的时间。软件就像孕育在我们肚子里的婴儿，我们知道还没有发育好，甚至有些畸形，出生没准就会直接夭折，但时间到了还是得努力生出来。一直大着个肚子，什么都不能干，毕竟不爽。生下来的咱们有病治病，没病就抚养它不断成长。

对比V1.2.1版本的结果，还是明显能看出改善了不少。物体检测误检低了许多，跟踪稳定了一些，测距的精度也提高了。回头头看，不枉费团队几个人一个月的辛苦。这一个月，check in了不少代码：算法方面改进是一方面，代码的优化/抽象/精简，写新的工具代码，也花费了一些时间。

<!-- more -->

最大的收获，就是对软件开发多了一些理解。以前在学校时，没有参与大型系统开发的经验，对程序的理解只停留在讲授语法的代码片段和解决ACM算法题目的小程序上，加上自己不是计算机科班出身，连软件工程课这种熏陶都没有。年少无知，觉得设计数据结构和算法，并实现出来，写就是软件开发的全部。当时听工作的前辈总结：一个软件工作者，coding的时间，可能只占到总共工作时间的10%。当时一方面不理解，觉得写软件的，不**写**软件，还有别的事情做吗？另一方面，猜测这些人一定是不务正业，或者水平不高，才导致效率这么低。

工作中接触了真正的系统开发，渐渐理解了，古人诚不欺我也。程序开发中，有需求分析，设计，代码构建，单元测试，集成，测试，发布，维护，重构等种种步骤。代码构建，或者说coding，只是整个过程的其中一环，而算法又只是代码构建中的一部分。虽然算法和数据结构可以说是软件的灵魂，但灵魂也需要一个附着在一个强健的肉身。软件开发的其他环节，就是这肉身。把没有肉身不健全的的灵魂交付出去，用户会经常破口大骂：这什么玩意！见鬼！

单就代码构建来说，这次重构，自己也小有领悟。最重要的领悟就是：如何写健壮的代码。接着上面的比喻，如果每个算法或者每个功能函数，都是一个灵魂，如何打造一副健壮的肉身。

以前写代码时，丝毫没有代码健壮性的概念，不管代码封装好不好，可读性怎么样，能不能复用，哗哗哗往下实现算法，写完之后编译运行，程序恰好能运行就好，运行失败再去看哪里写错了。这种方式开发速度的确很快，但之后经常碰到各种bug，花在调bug的时间可能更多。更不要说代码无法复用，违反DRY原则，维护起来不方便，需要浪费更多时间。

吃一堑长一智，与其之后调试bug花更多时间，为什么不把代码写好一些呢。对输入参数进行合理的检查，对异常进行错误处理，打上适当的log，关键步骤有断言进行检查，有恰好好处的单元测试。这些步骤会让代码数量膨胀许多，程序远远没有纯粹的算法优美。但是这才是工业上需要的代码，皮实可靠，久经考验。

代码习惯上的改变背后，其实更重要的程序思维的改变：从”恰好运行“式编程，到”防御式“编程的转变。

“‘恰好运行’式编程”这个名词是我发明的，但我敢肯定这种风格，或者这种态度，肯定不是我发明的。曾经的我就是这样写代码的，成功运行“一次就好“，之后“我陪你去看天荒地老”是这种风格的slogan。

“防御式编程”，这个名词不是我发明的，我最早看到是在《程序员自我修炼》那本书里。现在的我非常认同这种编程风格。我愿意宣言：“比起编译器，人类更有可能出错，尤其自己最有可能出错”。

更相信机器编译和运行的结果，让我在实现代码时，把可能出错的地方都在代码中体现出来。低三下四地用蹩脚的编程语言询问编译器，“编大爷，我写的对吗？“。编大爷说对，我继续往前走，编大爷说错了，我得毕恭毕敬地把编大爷说的话记下来，从中寻找我出错的蛛丝马迹。改正之后，继续询问编大爷：“我这么修改，您还满意吗？”，直到编大爷满意。之后再进行合理的测试，都是依靠机器来做一些检查。

这种对人类智力的不自信，带来的是自己对所写的程序的自信。正因为自己足够小心，充分自我怀疑，才会让可能出现问题的时候尽可能的小，并且考虑在异常时也能正确处理。前期对机器的信赖，其实换回的是部署之后程序命运掌握在自己手中的安定感，不再战战兢兢，祈求上天让程序运行顺利。

这种编程方式要增加很多工作量，所以很重要的一点告诫自己：一定要区分，现在写的代码，是在造狗窝，还是在建高楼。

建高楼需要稳定的根基，稍微一些小小的错误就会导致巨大的错误，并且难以察觉，整个系统的稳定性取决于一点一滴小函数的稳定性，所以必须有谨慎甚至谦卑的态度。但如果只是造狗窝，写一个原型或者临时使用的小工具，完成主要功能就好，如果花很多时间设计和打牢固的根基，也非常不合适。

当自己有了对工业代码的好坏有自己的判断，有灵敏的鼻子嗅出坏代码的味道，其实更容易犯第二个错误：用建高楼的方式去建造狗窝。看狗窝总是觉得简陋，松散，不够人性化。但其实那就是个狗窝，要人性化干嘛。我可以给狗窝造的和高楼一样牢固，但那多累啊。而一天可能要造好几个狗窝，而且狗住一天可能就不住了。

我在CV领域很大的体会：尺度很重要。写代码也一样，甚至做人也一样：要分清自己现在是在哪个层次上，用合适的scale来做事。scale太大或者太小，都不会有好的结果。
