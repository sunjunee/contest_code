1、一面

（1）两个队列实现一个栈
（2）两个栈实现一个队列

```Python
class baseStack():
    def __init__(self):
        self.val = []

    def pop(self):
        return self.val.pop()

    def push(self, x):
        self.val.append(x)

    def lens(self):
        return len(self.val)

class baseQueue():
    def __init__(self):
        self.val = []

    def pop(self):
        if(self.val == []):
            return

        x = self.val[0]
        del self.val[0]

        return x

    def push(self, x):
        self.val.append(x)

    def lens(self):
        return len(self.val)


class Stack():
    def __init__(self):
        self.queue_1 = baseQueue()
        self.queue_2 = baseQueue()

    def pop(self):
        if(self.queue_1.lens() == 0):
            return

        while(self.queue_1.lens() != 1):
            self.queue_2.push(self.queue_1.pop())

        self.queue_1, self.queue_2 = self.queue_2, self.queue_1
        return self.queue_2.pop()

    def push(self, x):
        self.queue_1.push(x)


class Queue():
    def __init__(self):
        self.stack_1 = baseStack()
        self.stack_2 = baseStack()

    def pop(self):
        if(self.stack_2.lens() != 0):
            return self.stack_2.pop()

        for i in range(self.stack_1.lens()):
            self.stack_2.push(self.stack_1.pop())

        return self.stack_2.pop()

    def push(self, x):
        self.stack_1.push(x)

```


（3）一个字符串数组，连续空格合并成一个空格


```Python

def removeBlanks(strs):
    lens = len(strs)
    if lens == 0:
        return

    i = 1
    while(i < len(strs)):
        if(strs[i] == strs[i-1] and strs[i] == " "):
            del strs[i]
        else:
            i += 1

    return  "".join(strs)

def removeBlanks1(strs):
    return " ".join(strs.split())

if __name__ == "__main__":
    print(removeBlanks(list("wo shi  hao  ren     a ")))
    print(removeBlanks1("wo shi  hao  ren     a "))
```

（4）二叉树中序非递归

```Python
def cenTravelNoRecur(root):
    if(root == None):
        return

    stack = [root]
    node = root.left

    while(True):
        while(node != None):
            stack.append(node)
            node = node.left

        if(stack == []):
            break

        node = stack.pop()
        print(node.x, end=" ")
        node = node.right
```

（5）二叉树找公共父节点

```Python
def getCommonFather(root, p1, p2):
    if(root == p1 or root == p2 or root == None):
        return root

    left = getCommonFather(root.left, p1, p2)
    right = getCommonFather(root.right, p1, p2)

    if(left != None and right != None):
        return root
    elif(left != None):
        return left
    else:
        return right
```


（6）把ipv4地址转换成一个int

```Python
def transIPv4(strs):
    nums = [int(s) for s in strs.split(".")]

    return nums[0] * (256**3) + nums[1] * (256 ** 2) + nums[2] * (256 ** 1) + nums[3] * (256 ** 0)
```


（7）浏览器中输入www.baidu.com到显示页面，经过了哪些过程？

    https://www.cnblogs.com/kongxy/p/4615226.html

2、

（1）推svm公式，线性svm，对偶形式

（2）svm的缺点

     不适合在大数据量下使用，SVM是借助二次规划来求解支持向量，而求解二次规划将涉及m阶矩阵的计算（m为样本的个数），当m数目很大时该矩阵的存储和计算将耗费大量的机器内存和运算时间。

     只能用于二分类问题，多分类需要多个二分类组合。

（3）lr和svm的区别

     Logistic回归、perception都是线性分类器，而SVM在引入kernel方法之后，变成了非线性的模型。
     优化的目标不一样，Logistic回归是基于概率的模型，其最优化的目标是最大化模型的对数似然函数，一般用梯度下降或者牛顿法求解；SVM和perception可以认为都是基于几何的模型，特别是SVM，它优化的目标都是期望误差，即经验风险，SVM是合页损失函数，而Perception就是分类的损失函数。Perception基于样本在分类面的两边的位置来分类，而SVM则将分类的边界拉大，用间隔之外的位置用于分类。
     Logistic回归中，每个点对分类面都不会有影响，点对分类面的影响会随着距离的增大而指数衰减；Perception中每个点都影响分类，但每个点对于分类面的影响，可以认为和距离无关；而SVM中，对分类面有影响的只有边界附近的支持向量。
     LR可以拓展为多分类，而SVM和Perception不行。


（4）设计一个商品召回的系统流程

  每个汽车商品给你一个价值，是区间或者一个给定值，如：20万-30万，35万。根据用户的浏览历史，设计一个汽车商品的召回系统。

    按照亚马逊item-cf的思路，设计了这样的流程：

    1）根据价格，预先计算汽车商品之间的相似度：
      计算方法：价值都取平均，或者给定值变成一个范围，然后两两求举例。

    2）根据用户的历史浏览的每个汽车商品，去已有商品中找和它相似度最高的k个商品；

    3）对召回的所有商品，按照相似度排序。

面试官问：

    1）你觉得哪些地方可以改进？
      相似度计算的方法，不一定合理，比如10万的车和20万的车，以及100万的车和110万的车，这两组，他们之间的相似度，实际上应该不太一样，但是上面的算法会认为差不多。

      同时排序的过程也可以优化

（5）knn快速算法

    之前看过kd-tree/ball-tree算法

    https://baike.baidu.com/item/kd-tree/2302515?fr=aladdin

（6）1000w商品选相似度top k

    说了两种：
      构建堆：时间复杂度太大，o(nlogn)
      堆商品分partion，然后分别取top k，最后取top k

3、

（1）9键输入数字，提示候选英文单词：字典树

    1 - abc, 2-def ...

    输入12，再输入3，怎么给出候选单词

    https://baike.baidu.com/item/%E5%AD%97%E5%85%B8%E6%A0%91/9825209

    http://www.cnblogs.com/gaochundong/p/trie_tree.html

然后基本全程在聊天。。。

百度凤巢广告算法
