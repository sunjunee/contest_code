1、一面

（1）如何做特征工程的？

    1）数据的可靠性：来源准确可靠，对样本的覆盖率要高

    2）线下抽取，分析特征重要性：a.互信息/相关系数；b.训练单特征的模型，看特征的效果；c.加入到lr/decision tree/rf等模型中，可以分析特征是否起到较大的作用；d.lr等模型中加l1正则，对特征进行选择，留下来的认为有效；

    3）上线测试，开ab实验，加入特征前后实验指标的变化。

（2）一个数组，找连续子序列的乘积最大值？

    写翻车了，只考虑了正数的情况。
    dp问题，每一步满足如下的转移公式：

    dp1[i]:以第i个数结尾的连续子序列最大乘积
    dp2[i]:以第i个数结尾的连续子序列最小乘积

    dp1[i]=max(data[i],dp1[i-1]*data[i],dp2[i-1]*data[i]);
    dp2[i]=min(data[i],dp1[i-1]*data[i],dp2[i-1]*data[i]);

```Python

    def maxValue(nums):
        lens = len(nums)

        if(lens == 0):
            return
        elif(lens == 1):
            return nums[0]

        dp1 = nums[0]
        dp2 = nums[0]

        for i in range(1, lens):
            dp1_tem = max([nums[i], dp1 * nums[i], dp2 * nums[i]])
            dp2_tem = min([nums[i], dp1 * nums[i], dp2 * nums[i]])

            dp1, dp2 = dp1_tem, dp2_tem

        return dp1

```


（3）k个链表合并？

    两两合并，说了思路，然后让写了两个链表合并的代码。


2、二面

（1）推导lr，梯度下降？

    李航书上有

（2）lr为什么用logistic？好处？

    一方面，sigmoid函数具有非常优良的性能，其导数和它自身存在一定的关系，利于后续利用梯度下降法进行求解，计算起来也会飞快；

    另一方面，sigmoid函数在两边变化缓慢，中间变化迅速，对于分类边界附近的点，应该具有更高的分辨能力。

（3）梯度下降法和牛顿法的区别？优缺点？

    参考：https://blog.csdn.net/xmu_jupiter/article/details/47402497

（4）svm的使用场景？

    1）如果Feature的数量很大，跟样本数量差不多，这时候选用LR或者是Linear Kernel的SVM
    2）如果Feature的数量比较小，样本数量一般，不算大也不算小，选用SVM+Gaussian Kernel
    3）如果Feature的数量比较小，而样本数量很多，需要手工添加一些feature变成第一种情况


（5）cnn如何不加全连接实现分类？

    面试官说可以用全卷积。。。并不懂

（6）不同大小的图片，输入cnn，怎么处理？

     面试官曰：hekaiming他们的论文解决了这个问题

（7）卷积算法底层如何实现快速运算的？

    答：分块并行计算
    问：边界怎么搞？
    答：分块的时候，留一点重叠

（8）cnn的参数主要集中在什么地方？

    卷积层输出到全连接

（9）推荐或广告的整体流程？

    大概讲了从特征构造，召回，精排的流程。

    然后讲了推荐和广告的不同。

    可以参考：https://mp.weixin.qq.com/s/lUP2BehOh7KczR3WRnOqFw

    https://mp.weixin.qq.com/s/9Fcj5lO-JPfFVnRSSM_56w

    https://mp.weixin.qq.com/s/izWqy9uNYcNKg7xJVv4SMQ

    第三个是实习的搜狗信息流的解决方案。

（10）用什么损失函数？讲一下交叉熵？为什么work？

    交叉熵

（11）怎么判断一个损失函数，是不是凸函数？

    https://blog.csdn.net/a7910932/article/details/44003775

（12）最近看过的论文？不足之处？

    正好前一天在头条分享过阿里妈妈团队做的TDM-attention召回模型，就讲了一下，贼爽。

    然后同事那天也提了一个问题，说这个模型并行实现不好做，然后就借用了一下～

（13）讲一讲word2vec或者embedding？

    参考：https://blog.csdn.net/baimafujinji/article/details/77836142


（14）dnn是怎么用来推荐召回的？

    讲了google做youtube视频推荐的dnn模型：http://cseweb.ucsd.edu/classes/fa17/cse291-b/reading/p191-covington.pdf

（15）推荐中，用户的特征怎么处理的？

    用户历史行为，做embedding

    category特征，做one-hot

    连续取值特征，分箱然后做one-hot

（16）为什么最后都做成ont-hot？

     可以平滑一些噪声的影响，对异常数据具有更强的鲁棒性；
     离散化将一个特征变为多个，特征的维度增加了，可以引入非线性，让样本更容易区分，模型更简单；


（17）讲一下信号处理里面的奈奎斯特采样定律？

  https://baike.baidu.com/item/%E5%A5%88%E5%A5%8E%E6%96%AF%E7%89%B9%E9%87%87%E6%A0%B7%E5%AE%9A%E5%BE%8B/16262017?fr=aladdin
