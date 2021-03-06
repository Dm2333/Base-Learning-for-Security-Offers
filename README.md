# Base-Learning-for-Security-Offers
## 404notfound的知识体系，不断完善
![](https://i.imgur.com/ALXXcjc.png)

- [基础语言类](基础语言类)
  - [Java](#Java基础知识)
  - [Python](#Python基础知识)
- [四大科班基础课程类](四大科班基础课程类)
  - [数据结构](#数据结构)
  - [计算机网络]
  - [操作系统](#操作系统)
  - [计算机组成原理]
- [机器学习基础类](机器学习基础类)
  - [理论基础](#理论基础)
  - [算法原理](#算法原理)
  - [算法特性](#算法特性)
  - [算法比较](#算法比较)
  - [杂项](#杂项)
- [深度学习基础类](#深度学习基础类)
  - [知识体系](#知识体系)
  - [神经网络](#神经网络)
    - [CNN]
    - [RNN]
    - [LSTM]
    - [BiRNN]
- [网络空间安全基础类]
  - [网络安全]
  - [应用安全]
  - [系统安全]
- [安全算法类]

# 基础语言类 #
## Java基础知识 ##
- [(Java中)堆和栈的区别](https://www.cnblogs.com/zyj-bozhou/p/6723863.html)<br>
联系数据结构中、操作系统中、C++中、Java中堆和栈的区别

## Python基础知识 ##
* Python中基本数据类型元组tuple、列表list、字典dict、集合set之间的区别？<br>
答：列表的特点是：可重复，类型可不同，类型不同也是和数据最本质的区别了；元组：元组和列表在结构上没有什么区别，唯一的差异在于元组是只读的，不能修改，元组用“()”表示；字典定义了键和值之间一对一的关系，但它们是以无序的方式存储的，字典的值可以是任意数据类型，最大的价值是查询；集合是一个无序不重复元素集，基本功能包括关系测试和消除重复元素，和字典类似，也是一组不重复key的集合，但不存储value
* [Python中list是怎么实现的？](http://www.laurentluce.com/posts/python-list-implementation/)<br>
答：Python中底层的list是用C语言的结构体表示的，ob_item是用来表示保存元素的指针数组，allocated是ob_item预先分配的内存总容量，list的初始化，当初始化一个空的list的时候，非常重要的是要知道list申请内存空间allocated的大小和list实际存储元素所占空间的大小ob_size之间的关系，ob_size()的大小和len(L)是一样的，通常会看到allocated的值要比ob_size的值要大，这是为了避免每次有新元素加入list时都要调用realloc进行内存分配
* [Python中list的get是怎么实现的？](http://www.laurentluce.com/posts/python-list-implementation/)<br>
答：list常见的操作函数有append、insert、pop、remove。以append为例，追加一个整数append(1)看看内部发生了什么？调用了内部的C函数app1(),list_resize()会申请多余的空间以避免调用多次list_resize()函数，list增长的模型是0,4,8,16,25,46,58,72,88，开辟了四个内存空间来存放list中的元素，存放的第一个元素是1，剩余的内存空间申请了但是没有使用。pop函数调用了listpop()函数，list_resize()在函数listpop()内部被调用，如果这时ob_size小于内存空间allocated的一半，这时的内存空间将会缩小。
* [Python装饰器、迭代器、生成器原理及应用场景](https://www.jianshu.com/p/efaa19594cf4)<br>
* [Python进程、线程和协程的区别及应用场景](https://zhuanlan.zhihu.com/p/30980478)
* [Python扫描速度的优化到GIL锁的原理和优化](http://cenalulu.github.io/python/gil-in-python/)
* [masscan扫描和nmap扫描等端口探测的原理和方式](http://www.freebuf.com/articles/network/146087.html)<br>

# 四大科班基础课程类
## 数据结构
- 堆和栈的区别<br>
答：栈是一种具有后进先出性质的数据结构；堆是一种经过排序的树形数据结构，通常我们所说的堆的数据结构，是指二叉堆，堆的特点是根节点的值最小或最大，且根节点的两个子树也是一个堆，由于堆的这个特性，常用来实现优先队列，好比是书架，虽然书的摆放是有顺序的，但是我们想要取任意一本时，不必要像栈一样取出前面所有的书。

## 操作系统
- [堆和栈的区别？](https://www.zhihu.com/question/19729973)<br>
答：堆区(heap),一般由程序员分配释放，若程序员不释放，程序结束时可能由OS回收；栈区(stack)，由编译器自动分配释放，存放函数的参数值，局部变量的值，其操作方式类似于数据结构中的栈。<br>
**区别和联系**：<br>
**1、申请方式**<br>
堆是由程序员自己申请并指明大小，如在c中使用malloc函数，与数据结构中的堆是两码事，分配方式类似于链表。而对于面向对象程序来说，new出来的任何对象，无论是对象内部的成员变量，局部变量，类变量，他们指向的对象都存储在堆内存中（但指针本身存在栈中）；栈是由系统自动分配，如申明在一个函数中一个局部变量int b；系统自动在栈中为b开辟空间，存放函数的参数值，局部变量的值等<br>
**2、申请后系统的响应**<br>
栈：只要栈的剩余空间大于所申请空间，系统将为程序提供内存，否则将报异常提示栈溢出；堆：首先应该知道操作系统有一个记录空闲内存地址的链表，当系统收到程序的申请时，会遍历该链表，寻找第一个空间大于所申请空间的堆结点，然后将该结点从空闲结点链表中删除，并将该结点的空间分配给程序，另外对于大部分系统，会在这块内存空间中的首地址处记录本次分配的大小，这样，代码中的delete语句才能正确的释放本内存空间。由于找到的堆结点的大小不一定正好等于申请的大小，系统会自动的将多余的那部分重新放入空闲链表中。<br>
**3、申请大小的限制**<br>
栈：在Windows下,栈是向低地址扩展的数据结构，是一块连续的内存的区域。这句话的意思是栈顶的地址和栈的最大容量是系统预先规定好的，在WINDOWS下，栈的大小是2M（也有的说是1M，总之是 一个编译时就确定的常数），如果申请的空间超过栈的剩余空间时，将提示overflow。因此，能从栈获得的空间较小。  
堆：堆是向高地址扩展的数据结构，是不连续的内存区域。这是由于系统是用链表来存储的空闲内存地址的，自然是不连续的，而链表的遍历方向是由低地址向高地址。堆的大小受限于计算机系统中有效的虚拟内存。由此可见，堆获得的空间比较灵活，也比较大。<br>
**4、申请效率的比较**<br>
栈是系统自动分配，速度较快，但程序员是无法控制的；堆是由new分配的内存，一般速度比较慢，而且容易产生内存碎片，不过用起来很方便。<br>

# 机器学习基础类 #
## 理论基础 ##
- 怎么防止过拟合？<br>
答：a. 增加样本（data bias or small data的缘故），移除噪声。<br>
b. 减少特征，保留重要的特征（可以用PCA等对特征进行降维）。<br>
c. 对样本进行采样（类似bagging）。就是建树的时候，不是把所有的样本都作为输入，而是选择一个子集。<br>
d. 对特征进行采样。类似样本采样一样, 每次建树的时候，只对部分的特征进行切分。

- 机器学习里面的偏差和方差有什么区别？<br>
答：泛化误差可分解为偏差、方差与噪声之和。偏差度量了学习算法的期望预测与真实结果的偏离程度，即刻画了学习算法本身的拟合能力；方差度量了同样大小的训练集的变动所导致的学习性能的变化，即刻画了数据扰动所造成的影响；噪声则表达了在当前任务上任何学习算法所能达到的期望泛化误差的下界，即刻画了学习问题本身的难度。偏差-方差分解说明，泛化性能是由学习算法的能力、数据的充分性以及学习任务本身的难度所共同决定的。给定学习任务，为了取得好的泛化性能，则需使偏差较小，即能够充分拟合数据，并且使方差较小，即使得数据扰动产生的影响小。

- 样本类别不平衡怎么办？<br>
答：现有技术大体上有三类做法：假定正例少，负例多。第一类是直接对训练集的反类样例进行“欠采样”，即去除一个反例使得正、反例数目接近，然后再进行学习；第二类是对训练集里的正类样例进行“过采样”，即增加一些正例使得正、反例数目接近，然后再进行学习；第三类则是直接基于原始训练集进行学习，但在用训练好的分类器进行预测时，将“再缩放”嵌入到其决策过程中，称为“阈值移动”，但是实际操作却可能有问题，主要因为“训练集是真实样本总体的无偏采样”这个假设往往不成立，未必能有效的基于训练集观测几率来推断出真实几率。

- [L1和L2有什么区别？](https://www.zhihu.com/question/26485586)<br>
答：L0：计算非零个数，用于产生绝对的稀疏性；L1：计算绝对值之和，用于产生稀疏性，对于large-scale的问题来说，可以减少存储空间；L2：计算平方和再开根号，能够起到正则化的作用，L2范数更多的是防止过拟合，提高模型的泛化能力，并且让优化求解变得稳定快速，这是因为加入L2范数之和，满足了强凸。<br>
从最优化问题解的平滑性来看，L1范数的最优解相对于L2范数要少，但其往往是最优解，而L2的解很多，但更多的倾向于某种局部解。

- [为什么L1能得到稀疏解？](https://www.zhihu.com/question/37096933)<br>
答：L1、L2两种正则能不能把最优的x变成0，取决于原先的函数在0点处的导数。如果本来导数不为0，那么施加L2正则后导数依然不为0，最优的x也不会变成0；而施加L1正则时，只要正则项的系数C，大于原先函数在0点处的导数的绝对值，x=0就会变成一个极小值点。上面只分析了一个参数x，事实上L1正则会使许多参数的最优值变成0，这样模型就稀疏了。

- [梯度消失、爆炸是怎么回事？](https://blog.csdn.net/qq_25737169/article/details/78847691)<br>
答：梯度爆炸和梯度消失根源：深度神经网络和反向传播（sigmoid激活函数）。都是因为网络太深，网络权值更新不稳定造成的，本质上是因为梯度反向传播中的连乘效应。对于更普遍的梯度消失问题，可以考虑用ReLU激活函数取代sigmoid激活函数。另外，LSTM的结构设计也可以改善RNN中的梯度消失问题

## 算法原理 ##
- xgb的原理
- GBDT的原理
	- [GBDT迭代决策树算法的一些基本概念](https://zhuanlan.zhihu.com/p/30736738)
	- [GBDT的原理和应用](https://zhuanlan.zhihu.com/p/30339807)
	- [GBDT原理及利用GBDT构造新的特征-Python实现](https://blog.csdn.net/shine19930820/article/details/71713680)

## 算法特性 ##
- [lr怎么改善？](https://zhuanlan.zhihu.com/p/30339807)<br>
答：lr和gbdt相结合，用gbdt来学习组合特征，再结合lr固有的稀疏特征，组成新的特征向量

## 算法比较 ##
- [RF、GBDT和XGB比较](https://zhuanlan.zhihu.com/p/34679467)
- lgb和xgb有什么区别

## 杂项 ##
- 机器学习各种算法怎么调参？
	- [RF、GBDT是怎么调参的？哪些参数比较重要？一般选多少？](https://www.zhihu.com/question/34470160)<br>
	答：**思路：全程联系偏差和方差**。<br>
	**思路展开**：联系RF、GBDT对应到偏差、方差，具体来说，拆分RF、GBDT为多个单个树，再对应到偏差、方差，再联系单个树的特性和树之间的关联性，对应到两类参数：过程影响类参数和子模型影响类参数。<br>
	**具体描述**：对过程影响类参数进行调整，毕竟它们对整体模型性能的影响最大，然后依据经验，在子模型影响类参数中选择对整体模型性能影响最大的参数，进行下一步调参。联系RF、GBDT对应到Bagging和Boosting：正由于Bagging的训练过程旨在降低方差，而Boosting的训练过程旨在降低偏差，过程影响类的参数能够引起整体模型性能的大幅度变化。一般来说，在此前提下，我们继续微调子模型影响类的参数，从而进一步提高模型的性能。例如RF的过程影响类参数只有“子模型数”，而GBDT的过程影响类参数有“子模型数”和“学习率”，需要一起考虑调整，GBDT子模型影响参数有：最大叶节点数、最大树深度、分裂所需最小样本数、叶节点最小样本数、子采样率、分裂时考虑的最大特征数等。最大叶节点数、最大树深度等控制子模型结构的参数是与Random Forest一致的。类似“分裂时考虑的最大特征数”、“子采样率”，也会造成子模型间的关联度降低，整体模型的方差减小。

# 深度学习基础类
## 知识体系
![](https://i.imgur.com/z97OmHx.png)

## 神经网络

## 深度学习VS机器学习
- [深度学习与机器学习有什么区别？应用场景有哪些区别？哪些应用场景用机器学习？哪些场景用深度学习？为什么？]<br>
答：从**数据集角度**来说，目前深度学习表现比较好的领域主要是图像、语音、自然语言处理等领域，这些领域的一个共性是局部相关性。图像中像素组成物体，语音信号中音位组合成单词，文本数据中单词组合成句子，这些特征元素的组合一旦被打乱，表示的含义同时也被改变。对于没有这样的**局部相关性的数据集**，不适合用深度学习算法进行处理。举个例子：预测一个人的健康状况，相关的参数会有年龄、职业、收入、家庭状况等因素，将这种元素打乱，并不会影响相关的结果。这种情况就比较适合用机器学习来处理。（此处是从数据集的特性来说，如果从数据集的大小来说，深度学习不适合处理小数据集）

