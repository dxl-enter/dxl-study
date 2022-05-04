在软件开发的过程中，可以说调试是一项基本技能。调试的英文单词为 debug ，顾名思义，就是去除 bug 的意思。俗话说的好，编程就是制造 bug 的过程，所以 debug 的重要性毋庸置疑，如果能熟练掌握调试技能，也就可以很快的定位出代码中的 bug。要知道，看的懂代码不一定写的出代码，写的出代码不一定能调试好代码，为了能写出没有 bug 的代码，我们必须得掌握一些基本的调试技巧。

工欲善其事，必先利其器。无论你的开发工具是 IntelliJ IDEA 还是 Eclipse ，调试器都是标配。在遇到有问题的程序时，合理的利用调试器的跟踪和断点技巧，可以很快的定位出问题原因。虽然说合理利用日志也可以方便定位线上问题，但是日志并不是调试工具，不要在开发环境把 System.out.println 当作调试手段，掌握调试器自带的调试技能才是正道。

一、实战 IDEA 调试技巧

如果你是做 Java 开发的，相信你不会没有听过 IntelliJ IDEA ，和大多数 Java 开发者一样，我一开始的时候也是用 Eclipse 来进行开发，但是自从换了 IDEA 之后，就再也离不开它了，彻底变成了 IDEA 的忠实粉丝（不好意思，打一波广告。。）。
不得不说，JetBrains 这家来自捷克的软件公司真的是良心企业，所出产品皆是精品，除了 IDEA，还有 WebStorm，PhpStorm，PyCharm 等，风格都是很类似的，一些类似的快捷键包括调试技巧也是通用的。
打开 IDEA 的调试面板，如下图所示，可以大致的将其分成五个部分：
单步跟踪
断点管理
求值表达式
堆栈和线程
变量观察

1.1 单步跟踪
说起调试，估计很多人第一反应就是对程序进行一步一步的跟踪分析，其实 IDEA 提供了很多快捷键来帮助我们跟踪程序，大抵可以列出下面几个技巧：
Show Execution Point
调试时往往需要浏览代码，对代码进行分析，有时候在浏览若干个源文件之后就找不到当前执行到哪了，可能很多人会使用 Navigate Back 来返回，虽然也可以返回去，但可能需要点多次返回按钮，相对来说使用这个技巧快速定位到当前调试器正在执行的代码行要更简便。
Step Over
这是最基本的单步命令，每一次都是执行一行代码，如果该行代码有方法会直接跳过，可以说真的是一步一个脚印。
Step In / Force Step In
Step Over 会跳过方法的执行，可以观察方法的返回值，但如果需要进到方法里面，观察方法的执行细节，则需要使用 Step In 命令了。另外，Step In 命令也会跳过 jdk 自带的系统方法，如果要跟踪系统方法的执行细节，需要使用 Force Step In 命令。
关于单步的时候忽略哪些系统方法，可以在 IDEA 的配置项 Settings -> Build, Execution, Deployment -> Debugger -> Stepping 中进行配置，如下图所示。

Step Out
当使用 Step In 命令跟踪到一个方法的内部时，如果发现自己不想继续调这个方法了，可以直接把这个方法执行完，并停在调用该方法的下一行位置，这就是 Step Out 命令。
Drop to Frame
这一招可以说是调试器的一大杀器。在单步调试的时候，如果由于粗心导致单步过了头，没有看到关键代码的执行情况，譬如想定位下某个中间变量的值，这个时候如果能回到那行关键代码再执行一遍就好了，Drop to Frame 就提供了我们这个能力，它可以回到方法调用的地方（跟 Step Out 不一样，Step Out 是回到方法调用的下一行），让我们可以再调试一次这个方法，这一次可不要再粗心了。

Drop to frame 的原理其实也非常简单，顾名思义，它将堆栈的最上面一个栈帧删除（也就是当前正在执行的方法），让程序回到上一个栈帧（父方法），可以想见，这只会恢复堆栈中的局部变量，全局变量无法恢复，如果方法中有对全局变量进行操作的地方，是没有办法再来一遍的。
Run to Cursor / Force Run to Cursor
这两个命令在需要临时断点时非常有用，譬如已经知道自己想分析哪一行代码了，但又不需要下很多无谓的断点，可以直接使用该命令执行到某行，Force Run to Cursor 甚至可以无视所有断点，直接到达我们想分析的地方。
1.2 断点管理
断点是调试器的基础功能之一，可以让程序暂停在需要的地方，帮助我们进行分析程序的运行过程。在 IDEA 中断点管理如下图所示，合理使用断点技巧可以快速让程序停在我们想停的地方：

可以将断点分成两种类型：行断点指的是在特定的某行代码上暂停下来，而全局断点是在某个条件满足时停下来，并不限于停在固定的某一行，譬如当出现异常时暂停程序。
1.2.1 行断点
Suspend (All / Thread)
Condition
条件断点。这应该也是每个使用调试器的开发者都应该掌握的一个技巧，当遇到遍历比较大的 List 或 Map 对象时，譬如有 1000 个 Person 对象，你不可能每个对象都调一遍，你可能只想在 person.name = 'Zhangsan' 的时候让断点断下来，就可以使用条件断点，如下图所示：

Log message to console
Evaluate and log
当看到上面的 Suspend 这个选项的时候有的人可能会感到奇怪，我下一个断点不就是为了让程序停下来吗？还需要这个选项干什么？是不是有点多余？难道你下个断点却不想让程序停下来？
在发现 Evaluate and log 这个技巧之前，我对这一点也感觉很奇怪，直到有一天我突然发现 Suspend Off + Evaluate and log 的配合真的是太有用了。前面有讲过，不要把 System.out.println 当作调试手段，因为你完全可以用这个技巧来打印所有你想打印的信息，而不需要修改你的源代码。
Remove once hit
一次性断点。上面介绍的 Run to Cursor 就是一次性断点的例子。
Instance filters
Class filters
Pass count
这几个我用的不是很多，但应该也是非常有用的技巧可以先记下来。在 IDEA 里每个对象都有一个实例ID，Instance filters 就是用于当断点处代码所处的实例和设定ID匹配则断下来。Pass count 则是在断点执行到第几次的时候暂停下来。
1.2.2 全局断点
Exception breakpoints
Method breakpoints
Field watchpoints
个人感觉这几个技巧都不是很常用，感兴趣的同学自己实验一把吧。
1.3 求值表达式
在一堆单步跟踪的按钮旁边，有一个不显眼的按钮，这个按钮就是 “求值表达式”。它在调试的时候很有用，可以查看某个变量的值，也可以计算某个表达式的值，甚至还可以计算自己的一段代码的值，这分别对应下面两种不同的模式：
表达式模式（Expression Mode）
代码片段模式（Code Fragment Mode）
这两个模式类似于 Eclipse 里面的 Expression View 和 Display View。在 Display View 里也可以编写一段代码来执行，确实非常强大，但是要注意的是，这里只能写代码片段，不能自定义方法，如下图：

1.4 堆栈和线程
这个没什么好说的，一个视图可以查看当前的所有线程，另一个视图可以查看当前的函数堆栈。在线程视图里可以进行 Thread dump，分析每个线程当前正在做什么；堆栈视图里可以切换栈帧，结合右边的变量观察区，可以方便的查看每个函数里的局部变量和参数。
线程视图
堆栈视图

1.5 变量观察
变量区和观察区可以合并在一起，也可以分开来显示（如下图所示），我比较喜欢分开来显示，这样局部变量、参数以及静态变量显示在变量区，要观察的表达式显示在观察区。
观察区类似于求值表达式中的 Expression mode，你可以添加需要观察的表达式，在调试的时候可以实时的看到表达式的值。变量区的内容相对是固定的，随着左边的栈帧调整，值也会变得不同。在这里还可以修改变量原有的值。


二、使用 jdb 命令行调试

相信很多人都听过 gdb，这可以说是调试界的鼻祖，以前在学习 C/C++ 的时候，就是使用它来调试程序的。和 gdb 一样，jdb 也是一个命令行版的调试器，用于调试 Java 程序。而且 jdb 不需要安装下载，它是 JDK 自带的工具（在 JDK 的 bin 目录中，JRE 中没有）。

每研究一项新技术，我总是会看看有没有命令行版本的工具可以替代，在命令行下进行操作给人一种踏实的感觉，每一个指令，每一个参数，都清清楚楚的摆在那里，这相比较于图形界面的工具，可以学习更深层的知识，而不是把技术细节隐藏在图形界面之后，你可以发现命令行下的每一个参数，每一个配置，都是可以学习的点。
2.1 jdb 基本命令
在 jdb 中调试 Java 程序如下图所示，直接使用 jdb Test 命令加载程序即可。

运行完 jdb Test 命令之后，程序这时并没有运行起来，而是停在那里等待进一步的命令。这个时候我们可以想好在哪里下个断点，譬如在 main() 函数处下个断点，然后再使用 run 命令运行程序：
> stop in Test.main正在延迟断点Test.main。将在加载类后设置。> run运行Test设置未捕获的 java.lang.Throwable设置延迟的未捕获的 java.lang.Throwable>VM 已启动：设置延迟的断点：Test.main
可以看出在执行 run 命令之前，程序都还没有开始运行，这个时候的断点叫做“延迟断点”，当程序真正运行起来时，也就是 JVM 启动的时候，才将断点设置上。除了 stop in Class.Method 命令，还可以使用 stop at Class:LineNumber 的方式来设置断点。
main[1] stop at Test:25
在 jdb 中下断点，就没有 IDEA 中那么多名堂了，什么条件断点，什么 Instance filters 都不支持，只能乖乖的一步一步来。在断点处，可以使用 list 命令查看断点附近的代码，或者用 step 命令单步执行，print 或者 dump 打印变量或表达式的值，locals 命令查看当前方法中的所有变量，cont 命令继续执行代码。
还有一些其他的命令就不多做介绍了，可以使用 help 查看所有的命令清单，或者参考 jdb 的官方文档。
2.2 探索 class 文件结构
在 jdb 中调试 Java 程序时，有可能源代码文件和 class 文件不在一起，这个时候需要指定源码位置：
# jdb -sourcepath path/to/source Test
如果不指定源码位置，在使用 list 命令时会提示找不到源码文件，如果真的没有源码文件，那么在 jdb 里完全就是瞎调了。我们知道 Java 代码在执行的时候，是以字节码的形式运行在 JVM 里的，可以猜测到，class 文件中必然有着和源码相关联的一些信息，类似于 C/C++ 语言的 obj 文件一样，要不然 list 命令怎么可以显示出当前正在执行的代码是哪一行呢？我们可以使用开源的 jclasslib 软件查看 class 文件里的内容，一个标准的 class 文件包含了下面这些信息：
基本信息
常量池
接口
属性
父类
字段
方法
Code 属性
行号属性
局部变量表
如下图所示，其中最重要的一个部分就是 Code 属性，Code 属性下面有行号属性 LineNumberTable，这个 LineNumberTable 就是调试器用来关联字节码和源代码的关键。关于 class 文件，可以参考:
http://ginobefunny.com/post/deep_in_jvm_notes_part4/

题外话：没有源码时如何调试？
如果没有源码，虽然在 jdb 里也可以用 step 来单步，但是没有办法显示当前正在运行的代码，这简直就是盲调。这个时候只能使用字节码调试工具了，常见的字节码调试器有：Bytecode Visualizer、JSwat Debugger、Java ByteCode Debugger (JBCD) 等等，参考:
https://reverseengineering.stackexchange.com/questions/7991/java-class-bytecode-debugger

三、关于远程调试

通过对 jdb 的学习，我们已经越来越接近 Java 调试器的真相了，但是还差最后一步。让我们先看看 Java 程序在 IDEA 里是如何被调试的，如果你有很强的好奇心，那么在 IDEA 里调试程序的时候可能已经发现了下面的秘密：

或者在调试 tomcat 的时候，也有类似的一串仿佛魔咒一般的参数：

这串魔咒般的参数像下面这样，一旦你理解了这串参数，你也就打破了 Java 调试器的魔咒，然后才能认识到 Java 调试器真正的面目：
"C:\Program Files\Java\jdk1.8.0_111\bin\java" -agentlib:jdwp=transport=dt_socket,address=127.0.0.1:20060,suspend=y,server=n FooConnected to the target VM, address: '127.0.0.1:20060', transport: 'socket'
这里面有两个关键点：
Java 程序在运行的时候带着 -agentlib 参数，这个参数用于指示 JVM 在启动时额外加载的动态库文件，-agentlib 参数和 -javaagent 不一样，这个库文件应该是由 C/C++ 编写的原生程序（JNI），类似于这里的 jdwp，在 Windows 上对应一个 jdwp.dll 库文件，在 Linux 上对应 jdwp.so 文件。那么这个 jdwp 库文件到底是做什么的呢？它后面的一串参数又是什么意思？
jdwp 的参数里貌似提到了 socket，并有 address=127.0.0.1:20060 这样的 IP 地址和端口号，而且下面的 Connected to the target VM 也似乎表示调试器连接到了这么一个网络地址，那么这个地址到底是什么呢？由于这里是本地调试，所以 IP 地址是 127.0.0.1 ，那么如果是远程调试的话，是不是这里也是支持的呢？
在 IDEA 的 Run/Debug Configuration 配置页面，你也可以添加一个远程调试，界面如下图，可以发现上面那串魔咒参数又出现了：

在真正开始远程调试之前，我们不妨带着这些疑问，来学习 Java 调试器的基本原理。

四、Java 调试原理及 JPDA 简介

在武侠世界里，天下武功可以分为两种：一种讲究招式新奇，出招时能出其不意，善于利用兵器的特性和自身的高妙手法攻敌不备；另一种讲究内功心法，就算是最最普通的招式，结合自身的深厚内力，出招时也能有雷霆之势。其实在技术的世界里，武功也可以分为两种：技巧和原理。
上面讲的那么多，无论你是掌握了 IDEA 的所有调试技巧也好，还是记熟了 jdb 的所有命令也好，都只是招式上的变化，万变不离其宗，我们接下来就看看调试器的内功心法。
4.1 JPDA
我们知道，Java 程序都是运行在 JVM 上的，我们要调试 Java 程序，事实上就需要向 JVM 请求当前运行态的状态，并对 JVM 发出一定的指令，或者接受 JVM 的回调。为了实现 Java 程序的调试，JVM 提供了一整套用于调试的工具和接口，这套接口合在一起我们就把它叫做 JPDA（Java Platform Debugger Architecture，Java 平台调试体系）。
这个体系为开发人员提供了一整套用于调试 Java 程序的 API，是一套用于开发 Java 调试工具的接口和协议。本质上说，它是我们通向虚拟机，考察虚拟机运行态的一个通道，一套工具。
JPDA 由三个相对独立的层次共同组成，而且规定了它们三者之间的交互方式。这三个层次由低到高分别是 Java 虚拟机工具接口（JVMTI），Java 调试线协议（JDWP）以及 Java 调试接口（JDI），如下图所示（图片来自 IBM developerWorks）：

这三个模块把调试过程分解成几个很自然的概念：调试者（debugger）和被调试者（debuggee），以及他们中间的通信器。被调试者运行于我们想调试的 Java 虚拟机之上，它可以通过 JVMTI 这个标准接口，监控当前虚拟机的信息；调试者定义了用户可使用的调试接口，通过这些接口，用户可以对被调试虚拟机发送调试命令，同时调试者接受并显示调试结果。

在调试者和被调试者之间，调试命令和调试结果，都是通过 JDWP 的通讯协议传输的。所有的命令被封装成 JDWP 命令包，通过传输层发送给被调试者，被调试者接收到 JDWP 命令包后，解析这个命令并转化为 JVMTI 的调用，在被调试者上运行。类似的，JVMTI 的运行结果，被格式化成 JDWP 数据包，发送给调试者并返回给 JDI 调用。而调试器开发人员就是通过 JDI 得到数据，发出指令。
详细的内容，可以参考
https://www.ibm.com/developerworks/cn/java/j-lo-jpda1/index.html
4.2 Connectors & Transport
到这里，我们已经知道了 jdwp 是调试器和被调试程序之间的一种通信协议。不过命令行参数 -agentlib:jdwp=transport=dt_socket,address=127.0.0.1:20060,suspend=y,server=n 中的 jdwp 貌似还不止于此。
事实上，这个地方上 jdwp.dll 库文件把 JDI，JDWP，JVMTI 三部分串联成了一个整体，它不仅能调用本地 JVMTI 提供的调试能力，还实现了 JDWP 通信协议来满足 JVMTI 与 JDI 之间的通信。
想要完全理解这串参数的意思，我们还需要学习两个概念：Connectors（连接器）和 Transport（传输）。
常见的连接器有下面 5 种，它指的是 JDWP 建立连接的方式：
Socket-attaching connector
Shared-memory attaching connector
Socket-listening connector
Shared-memory listening connector
Command-line launching connector
其中 attaching connector 和 listening connector 的区别在于到底是调试器作为服务端，还是被调试程序作为服务端。
传输指的是 JDWP 的通信方式，一旦调试器和被调试程序之间建立起了连接，他们之间就需要开始通信，目前有两种通信方式：Socket（套接字） 和 Shared-memory（共享内存，只用在 Windows 平台）。
4.3 实战远程调试
通过上面的学习我们了解到，Java 调试器和被调试程序是以 C/S 架构的形式运行的，首先必须有一端以服务器的形式启动起来，然后另一段以客户端连接上去。如果被调试程序以服务端运行，必须加上下面的命令行参数：
# java -agentlib:jdwp=transport=dt_socket,server=y,address=5005 Test# java -agentlib:jdwp=transport=dt_shmem,server=y,address=javadebug Test
第一句是以 socket 通信方式 来启动程序，第二句是以 共享内存 的方式来启动程序，socket 方式需要指定一个端口号，调试器通过该端口号来连接它，共享内存方式需要指定一个连接名，而不是端口号。
在程序运行起来之后，可以使用 jdb 的 -attach 参数将调试器和被调试程序连接起来：
# jdb -attach 5005# jdb -attach javadebug
在 Windows 平台上，第一条命令会报这样的错：java.io.IOException: shmemBase_attach failed: The system cannot find the file specified，这是由于 jdb -attach 使用系统默认的传输来建立连接，而在 Windows 上默认的传输是 共享内存 。要想在 Windows 上使用 socket 方式来连接，要使用 jdb -connect 命令，只是命令的参数在写法上不太好记忆：
# jdb -connect com.sun.jdi.SocketAttach:hostname=localhost,port=5005# jdb -connect com.sun.jdi.SharedMemoryAttach:name=javadebug
如果反过来，想让调试器以服务端运行，执行下面的命令：
# jdb -listen javadebug
然后 Java 程序通过下面的参数来连接调试器：
# java -agentlib:jdwp=transport=dt_shmem,address=javadebug, suspend=y Test# java -agentlib:jdwp=transport=dt_socket,address=127.0.0.1:5005,suspend=y,server=n
最后我们再回过头来看一看 IDEA 打印出来的这串魔咒参数，可以大胆的猜测，IDEA 在调试的时候，首先以服务器形式启动调试器，并在 20060 端口监听，然后 Java 程序以 socket 通信方式连接该端口，并将 JVM 暂停等待调试。
"C:\Program Files\Java\jdk1.8.0_111\bin\java" -agentlib:jdwp=transport=dt_socket,address=127.0.0.1:20060,suspend=y,server=n FooConnected to the target VM, address: '127.0.0.1:20060', transport: 'socket'
如果在 IDEA 下进行远程调试，可以参考 IBM developerWorks 上的另一篇与调试相关的主题：使用 Eclipse 远程调试 Java 应用程序。

总结

这篇文章首先介绍了 IDEA 的一些常用调试技巧，然后通过使用 jdb 进行 Java 程序的调试，学习了 jdb 的常用命令，最后通过远程调试引出调试器原理的话题，对 JPDA、JVMTI、JDWP、JDI 等概念有了一个初步的认识。从招式到心法，由技巧到原理，逐步揭开了 Java 调试器的神秘面纱。

对于开发人员来说，如果只懂招式，只会一些奇淫技巧，那么他只是把工具用得更得心应手而已，很难在技术上得到质的突破；而如果只懂心法，只沉浸于基本原理和理论，那么他只能做一个眼高手低的学院派，空有满腹大道理却无用武之地。我们更应该内外兼修，把招式和心法结合起来，融会贯通，方能成正果。

最后的最后，关于调试的话题不得不补充一句：调试程序是一个费时费力的过程，一旦需要调试来定位问题，说明代码的逻辑性和清晰性有问题，最好的代码是不需要调试的。所以，少一点调试，多一点单元测试，多一点重构，将代码写的更清晰才是最好的编程方式。更多IDEA使用技巧，Java知音公众号内回复“IDEA聚合”，送你一份完整教程

番外篇：关于调试器的测不准效应

在量子物理学中，有一个名词叫 测不准原理，又叫 不确定性原理，讲的是粒子的位置与动量不可同时被确定，位置的不确定性越小，则动量的不确定性越大，反之亦然。
说白点就是，你如果要很准确的测量粒子的位置，那么就不能准确的测量粒子的动量；如果要很准确的测量粒子的动量，那么粒子的位置就测不准；正是由于测量本身，会导致系统受影响。
把这个现象套在调试器领域里，也有着类似的效果。由于调试器本身的干扰，程序已经不是以前的程序了。所以问题来了，在调试器下运行出来的结果，真的可信吗？
下面是我想出来的一个有趣的例子，假设我们在第 4 行下一个断点，程序最后输出结果会是什么呢？
