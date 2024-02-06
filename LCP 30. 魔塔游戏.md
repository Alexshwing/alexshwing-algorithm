```python
class Solution:
    def magicTower(self, A: List[int]) -> int:
        if sum(A) < 0: return -1
        ans, hp, pq = 0, 1, []
        for x in A:
            if x < 0: heappush(pq, x)
            hp += x
            if hp <= 0:
                hp -= heappop(pq)
                ans += 1
        return ans
```
