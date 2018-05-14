# ARM介绍

从现实生活中可以发现ARM处理器无处不在。在2008年底石阶上生产的机遇ARM处理器的设备大约100亿件；在2013年底发布的基于ARM处理器的设备已经超过520亿。本书的读者们大约人手一台基于包含了ARM处理器的设备——移动电话，平板设备，个人电脑，电视机甚至是汽车。让使用PC更多的程序员们惊奇的是按照微处理器出货总量来算，极其成功的X86架构处理器也仅仅占了非常小的一部分份额，也就刚刚超过三十亿台设备。

自从1985年第一个ARM1处理器开始，ARM体系结构就具有非常大的先天优势。ARM生产了一个处理器家族，他们共享指令集，编程模型，且在一定程度上向后兼容。

那么让我们开始简单了解一下ARM历史

###1.1 历史###

第一个ARM处理器，ARM1，是由索菲-威尔逊和史蒂夫-斐不尔领导的团队在Acorn计算机公司设计完成的，在1985年的四月生产了第一块硅片，并且运行良好。很快ARM1就被ARM2替代，它增加了乘法硬件，并且用在了真实的系统中，其中包括Acorn Archimedes个人电脑。

![图1-1 Acorn Archimedes](\image\Figure1-1-Acorn-Archimedes.jpg)

在1990年11月ARM才作为独立的公司在英国剑桥成立，即Advanced RISC Machines Ltd。它是苹果计算机，Acorn计算机以及VLSI科技联合出资成立，时至今日它的两个股东公司已经不复存在。最初的12名雇员来自于Acorn计算机公司的团队。之所以将ARM单独分离出来成立独立的公司，因为苹果计算机公司选择ARM的处理器作为它的Newton产品的CPU。

![图1-2 苹果 Newton](\image\Figure1-2-The-Apple-Newton.jpg)

新的公司很快就为他们的技术做出了最好的决策，即授权知识产权（IP）。ARM并不设计，制造和出售芯片，他们仅仅出售他们的设计给半导体公司。这些公司会将ARM处理器设计进他们自己的产品中，以合作伙伴地形式与ARM公司合作。IP授权业务依旧是ARM公司现在的主业。ARM已经与半导体生产商中第一阵营中的夏普，德州仪器和三星等建立和合作关系。在1998年，ARM登录伦敦股票交易市场和纳斯达克。在写本书的时候，ARM已经拥有了2000名雇员，已经极大地扩展了他们的原始处理器设计业务。ARM也授权物理知识产权——物理单元库（与非门，RAM等），图形视频加速器和软件开发产品（比如编译器，调试器和开发板）。

###1.2 片上系统（SoC）###

今天的设计者可以在计算机芯片上汇集十亿晶体管甚至更多。设计和验证这么复杂的电路已经变成十分困难的任务。对于这么复杂的系统，由一家公司完成系统各组件设计的情况也变得原来越少。相应地，ARM和其他的半导体知识产权公司往往共同设计和验证组件（所谓的IP块或处理器）。这些IP授权给半导体公司，它们在自己的设计中使用这些IP块，包括微处理器，DSP，3D图形和视频控制器，同时也包括许多其他的功能。

半导体生产厂商那这些授权的IP块，再加上其他的部分组件生产出基于芯片的完整系统，这就形成了System-on-Chip（SoC）。为了生产一个完整的系统，架构师必须选择适当的内核，内存控制器，片上内存，外围设备，互联总线和其他的逻辑设备（或许还包括模拟模块或射频组件）。

专用集成电路（ASIC）是这本书中用到的另外一个术语。它是用于特定应用的一种集成电路。一种ASIC需要具有一个ARM核心，内存和其他的组件。很明显，在ASIC和SoC之间有很多重叠的地方。术语SoC通常是指高度集成的设备，在一个单一设备上包含很多系统组件，可能包含模拟组件，混合信号处理组件或射频电路。

半导体公司投入百亿美元来构建这些设备，通常也会设备运行的软件上投入很多。生产了带有强力处理器的复杂硬件系统，却没有为它移植几个操作系统或编写外围设备驱动，这是很难以让人理解的。

当然了，像Linux这样的操作系统要求大量的内存才能够运行起来，在单一硅片设备上通常是做不到的。所以术语SoC并不那么准确，因为SoC通常并不包含整个系统。除了硅片面积的问题，还有一种情况就是系统许多有用的部分都要求专家级硅片生产工艺，防止他们在同一硅片上都出现问题。

###1.3 嵌入式系统###

嵌入式系统通常被定义为一片运行了执行特定任务软件一片计算机硬件。典型的系统如电视机顶盒，智能卡，路由器，磁盘驱动器，打印机，汽车引擎管理系统，MP3播放器或影印机。这些设备与通常意义上理解的计算机系统相区别，计算机系统特指运行通用目的软件，具有输入输出设备，比如键盘，某种图像显示设备。

这个界限变得越来越模糊。比如移动电话或手机，它的基本功能或许是打电话，但是现代的智能手机可以运行一个复杂的系统，在这个系统上可以下载成千上万个应用程序。

嵌入式系统可以是具有8位微处理器，比如Intel 8051或PIC微控制器，或者一些具有复杂的32位或64位处理器，比如本书中描述的ARM家族处理器。他们要求具有ARM处理器和一些非易失性存储设备，以便保存在系统中运行的应用程序。系统也总会有额外的一些外围设备，通常与设备的功能相关——典型地包括通用异步发送接收设备，中断控制器，定时器，通用输入输出控制器，但一些情况下也会有GPU或DMA控制器。

运行在这些系统上的软件分为两类：操作系统和运行在操作系统上的应用程序。本书中，我们主要讲解Linux中的例子。Linux的源码是开源的，读者随时可以查看源码，并且很多程序员对于Linux源码也非常熟悉。尽管这样，从Linux中学到的知识也可以对等地应用到其他的操作系统中。

**内存占用**: 在许多系统中，为了降低软硬件花费（和电能），内存尺寸都受到限制。这样就被迫考虑程序的尺寸，以及如何减少程序运行时的内存占用。

**实时行为**: 特定系统的功能对于外部事件的响应都有最终时间限制。这种要求可能是"硬要求"（比如汽车的刹车系统必须在规定时间内给出响应），或“软要求”（音频处理碧玺在确定的时间帧内完成，避免糟糕的用户体验。但是极少情况下的无法及时响应也并不能说明该系统不可用）。

**电源**: 在许多嵌入式系统中电能供应来自于电池，程序员和硬件设计师必须对降低系统总能耗给予足够的重视。例如可以通过降低处理器频率，减小电源电压或在没有任务需要处理时关闭处理器。

**系统花费**: 减少材料花费可以在系统设计上尽量减少开支。

**推向市场时间**: 在竞争市场环境下，开发可用产品的时间会对产品成功与否产生显著影响。
