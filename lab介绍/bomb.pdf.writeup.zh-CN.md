**15-213 秋季 20xx**
**实验任务 L2：拆除二进制炸弹**
**分配日期：9月13日，截止日期：9月22日星期五**
**本实验的负责人是 Harry Bovik (bovik@cs.cmu.edu)。**

### 1. 介绍

邪恶的 Dr. Evil 在我们的课堂机器上布下了一系列“二进制炸弹”。二进制炸弹是由一系列阶段组成的程序。每个阶段需要你在标准输入上输入特定的字符串。如果你输入了正确的字符串，那么该阶段就被拆除，炸弹将进入下一阶段。否则，炸弹会爆炸，打印“BOOM!!!”然后终止。所有阶段都被拆除后，炸弹就会被成功拆除。

炸弹数量太多，我们无法全部处理，因此我们给每个学生分配一个炸弹来拆除。你的任务（没有选择的余地）是要在截止日期前拆除你的炸弹。祝你好运，欢迎加入拆弹小组！

### 第一步：获取你的炸弹

你可以通过指向以下网址的浏览器来获取你的炸弹：
```
http://$Bomblab::SERVER_NAME:$Bomblab::REQUESTD_PORT/
```
这将显示一个二进制炸弹请求表单，供你填写。输入你的用户名和电子邮件地址，然后点击提交按钮。服务器将生成你的炸弹，并将其以名为 `bombk.tar` 的 tar 文件返回到你的浏览器，其中 `k` 是你的炸弹的唯一编号。

将 `bombk.tar` 文件保存到你计划进行工作的（受保护的）目录中。然后执行命令：`tar -xvf bombk.tar`。这将创建一个名为 `./bombk` 的目录，包含以下文件：
- **README**：标识炸弹及其所有者。
- **bomb**：可执行的二进制炸弹。
- **bomb.c**：包含炸弹主要例程和 Dr. Evil 的友好问候的源文件。
- **writeup.{pdf,ps}**：实验说明书。

如果你由于某种原因请求了多个炸弹，这不是问题。选择一个炸弹进行工作，删除其余的。

### 第二步：拆除你的炸弹

你在这个实验中的任务是拆除你的炸弹。

你必须在课堂机器上完成这个任务。事实上，有传言说 Dr. Evil 真的很邪恶，如果在其他地方运行，炸弹会总是爆炸。我们听说炸弹还内置了几种防篡改装置。

你可以使用许多工具来帮助你拆除炸弹。请查看提示部分以获取一些建议和想法。最佳方式是使用你最喜欢的调试器逐步执行反汇编的二进制文件。

每次你的炸弹爆炸时，它会通知 bomblab 服务器，你的实验最终得分会减少 1/2 分（最多扣除 20 分）。所以炸弹爆炸是有后果的。你必须小心！

前四个阶段每个阶段值 10 分。阶段 5 和 6 略微困难一些，每个阶段值 15 分。最高得分为 70 分。

尽管各阶段逐渐变难，但你在从一个阶段到另一个阶段时获得的经验应该能够弥补这种难度。然而，最后一个阶段将对最优秀的学生构成挑战，因此请不要等到最后一刻才开始。

炸弹会忽略空白输入行。如果你运行炸弹时使用了命令行参数，例如：
```
linux> ./bomb psol.txt
```
它会从 `psol.txt` 中读取输入行，直到到达文件末尾（EOF），然后切换到标准输入。在一时的软弱中，Dr. Evil 添加了这个功能，这样你就不必反复输入已拆除阶段的解决方案。

为了避免意外引爆炸弹，你需要学习如何单步执行汇编代码以及如何设置断点。你还需要学习如何检查寄存器和内存状态。做这个实验的一个好处是，你将变得非常擅长使用调试器。这是一个关键技能，在你的职业生涯中将带来巨大的回报。

### 后勤

这是一个个人项目。所有交付都是电子化的。课程留言板上将发布澄清和更正。

### 提交

没有明确的提交方式。炸弹将自动通知你的指导老师你在拆除过程中的进展。你可以通过查看以下网址的课程记分板来跟踪你的进展：
```
http://$Bomblab::SERVER_NAME:$Bomblab::REQUESTD_PORT/scoreboard
```
这个网页会持续更新，以显示每个炸弹的进度。

### 提示（请阅读！）

有很多方法可以拆除你的炸弹。你可以在不运行程序的情况下详细检查它，并准确地弄清它的工作原理。这是一种有用的技术，但并不总是容易做到。你还可以在调试器下运行它，逐步查看它的工作过程，并利用这些信息来拆除它。这可能是拆除它最快的方法。

我们有一个请求，请不要使用蛮力方法！你可以编写一个程序，尝试所有可能的密钥来找到正确的密钥。但这没有什么好处，原因如下：
- 每次你猜错时，炸弹爆炸，你的实验最终得分会减少 1/2 分（最多扣除 20 分）。
- 每次你猜错时，一条消息会发送到 bomblab 服务器。你可能很快会用这些消息使网络饱和，并导致系统管理员撤销你的计算机访问权限。
- 我们没有告诉你字符串的长度，也没有告诉你其中包含的字符。即使你假设（不正确）它们都少于 80 个字符，并且只包含字母，你也需要为每个阶段进行 26^80 次猜测。这将花费很长时间，你在截止日期前不会得到答案。

有许多工具旨在帮助你了解程序的工作原理以及当它们不工作时的问题。以下是一些你可能会在分析炸弹时发现有用的工具，以及一些使用它们的提示。
- **gdb**
  GNU 调试器，这是一个命令行调试工具，几乎在每个平台上都可用。你可以逐行跟踪程序，检查内存和寄存器，查看源代码和汇编代码（我们没有给你大部分炸弹的源代码），设置断点，设置内存监视点，编写脚本。

  CS:APP 网站 [http://csapp.cs.cmu.edu/public/students.html](http://csapp.cs.cmu.edu/public/students.html) 有一个非常方便的单页 gdb 摘要，可以打印出来作为参考。以下是一些使用 gdb 的其他提示：
    - 为了防止每次输入错误时炸弹爆炸，你需要学习如何设置断点。
    - 在线文档，可以在 gdb 命令提示符下键入“help”，或在 Unix 提示符下键入“man gdb”或“info gdb”。有些人还喜欢在 emacs 的 gdb 模式下运行 gdb。

- **objdump -t**
  这将打印出炸弹的符号表。符号表包括炸弹中所有函数和全局变量的名称、炸弹调用的所有函数的名称及其地址。通过查看函数名称，你可能会学到一些东西！

- **objdump -d**
  使用此命令可以反汇编炸弹中的所有代码。你也可以只查看单个函数。阅读汇编代码可以告诉你炸弹是如何工作的。

  尽管 objdump -d 提供了很多信息，但它并没有告诉你全部内容。对系统级函数的调用以一种隐晦的形式显示。例如，对 `sscanf` 的调用可能会显示为：
  ```
  8048c36: e8 99 fc ff ff call 80488d4 <_init+0x1a0>
  ```
  要确定调用的是 `sscanf`，你需要在 gdb 中进行反汇编。

- **strings**
  此实用程序将显示炸弹中可打印的字符串。

在寻找特定工具吗？需要文档吗？别忘了，命令 `apropos`、`man` 和 `info` 是你的朋友。特别是，`man ascii` 可能会派上用场。`info gas` 会给你更多关于 GNU 汇编程序的信息。网络也可能是信息的宝库。如果你遇到困难，随时可以向你的导师求助。