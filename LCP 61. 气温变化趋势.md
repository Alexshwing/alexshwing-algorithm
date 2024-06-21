```python
class Solution:
    def temperatureTrend(self, A: List[int], B: List[int]) -> int:
        ans = c = 0
        for (a1, b1), (a2, b2) in pairwise(zip(A, B)):
            x, y = a2 - a1, b2 - b1
            if x == y == 0 or x * y > 0: ans = max(ans, (c := c + 1))
            else: c = 0
        return ans

```
