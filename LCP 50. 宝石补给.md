```python
class Solution:
    def giveGem(self, A: List[int], O: List[List[int]]) -> int:
        for x, y in O:
            A[y] += A[x] // 2
            A[x] -= A[x] // 2
        return max(A) - min(A)
```