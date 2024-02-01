```python
# 将元素变为中位数
from sortedcontainers import SortedList
class Magic:
    def __init__(self):
        self.L = SortedList() # 保存前 k 小值
        self.R = SortedList() # 保存其他值
        self.sum_l = 0 # 左边的和
        self.sum_r = 0 # 右边的和

    # 调整 L 和 R 的大小，保证调整后 L 和 R 长度相等或多 1
    def adjust(self):
        # 左边长度 > 右边长度 + 1
        while len(self.L) > len(self.R) + 1:
            x = self.L.pop()
            self.sum_l -= x
            self.sum_r += x
            self.R.add(x)

        # 左边长度 < 右边
        while len(self.L) < len(self.R):
            x = self.R.pop(0)
            self.sum_r -= x
            self.sum_l += x
            self.L.add(x)

    # 插入元素 x
    def add(self, x: int):
        if len(self.R) and x >= self.R[0]:
            self.R.add(x)
            self.sum_r += x
        else:
            self.L.add(x)
            self.sum_l += x
        self.adjust()

    # 删除元素 x
    def delete(self, x: int):
        if x in self.L:
            self.L.remove(x)
            self.sum_l -= x
        else:
            self.R.remove(x)
            self.sum_r -= x
        self.adjust()

    def get(self):
        if (len(self.L) + len(self.R)) % 2:
            return self.L[-1]
        return (self.L[-1] + self.R[0]) // 2

class Solution:
    def numsGame(self, A: List[int]) -> List[int]:
        MOD = 1_000_000_007
        magic = Magic()
        ans = [0] * len(A)
        for i, b in enumerate(A):
            b -= i
            magic.add(b)
            mid = magic.get()
            ans[i] = (mid * len(magic.L) - magic.sum_l + magic.sum_r - mid * len(magic.R)) % MOD
        return ans
```
