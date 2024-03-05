```python
class Solution:
    def conveyorBelt(self, A: List[str], start: List[int], end: List[int]) -> int:
        n, m = len(A), len(A[0])
        dist = [[inf] * m for _ in range(n)]
        dist[start[0]][start[1]] = 0
        dq = deque([(start[0], start[1])])
        while dq:
            x, y = dq.popleft()
            for nx, ny, op in (x + 1, y, 'v'), (x - 1, y, '^'), (x, y + 1, '>'), (x, y - 1, '<'):
                if 0 <= nx < n and 0 <= ny < m:
                    g = A[x][y]
                    if dist[x][y] + (g != op) < dist[nx][ny]:
                        dist[nx][ny] = dist[x][y] + (g != op)
                        if g == op: dq.appendleft((nx, ny))
                        else: dq.append((nx, ny))
        return dist[end[0]][end[1]]
```
