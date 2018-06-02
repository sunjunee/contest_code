### 2018 0602 今日头条

#### T1

![image](https://github.com/sunjunee/contest_code/blob/master/toutiao/T1.jpg)


思路：实际上类似于滑动窗口，这一题有两个要点：

* 记录当前窗口内的0个数和位置，并在窗口内的0个数超过3的时候，更新窗口起点；
* 当窗口内数字之和小于0时，这些数字对后续的数字的和有负作用，需要更新窗口起点。

```python
# -*- coding: utf-8 -*-
"""
@ Author: Jun Sun {Python3}
@ E-mail: sunjunee@qq.com
@ Date:   2018-06-02 10:44:48
"""

n = 8
nums = [1,2,3,0,0,0,-2,7]

start, tem, resu = 0, nums[0], nums[0]      #start:窗口的起始位置
                                            #tem为当前窗口内的和，resu为最大的和
zeros = [] if tem != 0 else [0]             #当前窗口内0的index

for i in range(1, len(nums)):
    if(nums[i] == 0):       #如果新加入的数字是0，则将index加入zeros
        zeros.append(i)
    if(len(zeros) == 4):    #如果超过3个0，则需要将窗口开始位置移动到第一个0的未知
        new_start = zeros[0]
        del zeros[0]
        start = new_start
        tem = sum(nums[start:i])    #重新算tem
    
    tem += nums[i]          #计算tem
    if(tem <= 0):           #如果tem小于0，则前面的需要被舍弃
        start = i + 1
        tem = nums[i]
        
    if(tem > resu):         #更新最大值
        resu = tem
    
print(resu)
    
```

T2 

![image](https://github.com/sunjunee/contest_code/blob/master/toutiao/T2.jpg)

思路：



