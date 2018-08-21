# 高频题

### 1、top k问题

从100w个数字中，找出最大的k个数。

解法：使用前k个数，构造一个k个数的最小堆，堆顶元素是堆中元素的最小值，对于后面的每个数，依次与堆顶元素比较，如果小于堆顶元素，则跳过考虑下一个；如果当前数大于堆顶元素，则用当前数字替换堆顶元素，然后调整堆结构。

实际复杂度：构造堆 klogk；比较和调整堆最多n*logk，所以时间复杂度是nlogk

```python
#构造一个最小堆：从右到左，从下到上调整每个数的位置：
def build_min_heap(nums):
    lens = len(nums)
    
    start = lens // 2
    for i in range(start - 1, -1, -1):
        make_change_min(nums, lens - 1, i) 
    
def make_change_min(nums, imax, index):
    left = 2 * index + 1
    right = 2 * (index + 1)
    
    if(left > imax):
        return
    
    if(right > imax):
        if(nums[left] < nums[index]):
            nums[left], nums[index] = nums[index], nums[left]
    else:
        if(nums[left] < nums[index] and nums[left] < nums[right]):
            nums[left], nums[index] = nums[index], nums[left]
            make_change_min(nums, imax, left)
        elif(nums[right] < nums[index] and nums[right] < nums[left]):
            nums[right], nums[index] = nums[index], nums[right]
            make_change_min(nums, imax, right)

if __name__ == "__main__":
    nums = [random.randint(-100000, 10000000) for i in range(1000000)]
    
    # 从1M个数中取top 10:
    # 构造一个10个结点的最小堆
    k = 7
    
    tem = nums[0:k]
    build_min_heap(tem)
    
    for i in range(k, len(nums)):
        if(nums[i] > tem[0]):
            tem[0] = nums[i]
            make_change_min(tem, k-1, 0)
    
    print(tem)
```
