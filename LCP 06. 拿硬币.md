```python
class Solution:
    def minCount(self, A: List[int]) -> int:
        return sum((x + 1) // 2 for x in A)
```