# Algorithm Study_220417

## DFS & BFS

### 백준 1260 : DFS와 BFS

- 준구

  ```python
  ```

  

- 재현

  ```python
  ```

  

- 광휘

  ```python
  ```

  

- 승연

  ```python
  def dfs(start):
      stack = [start]
      while stack:
          v = stack.pop()
          if v not in d_visited:
              d_visited.append(v)
              for g in graph[v]:
                  stack.append(g)
      return d_visited
  
  def bfs(start):
      q = [start]
      b_visited[start] = 1
      result = list()
      while q:
          v = q.pop(0)
          result.append(v)
          graph[v].sort()
          for g in graph[v]:
              if b_visited[g] == 0:
                  q.append(g)
                  b_visited[g] = 1
      return result
  
  N, M, V = map(int, input().split())
  graph = [[] for _ in range(N+1)]
  for _ in range(M):
      s, f = map(int, input().split())
      graph[s].append(f)
      graph[f].append(s)
  b_visited = [0]*(N+1)
  bfs_result = bfs(V)
  for lst in graph:
      if lst:
          lst.sort(reverse=True)
  d_visited = list()
  dfs_result = dfs(V)
  print(dfs_result)
  print(bfs_result)
  ```

  

- 동훈

  ```python
  ```

  



### 백준 2606 : 바이러스

- 준구

  ```python
  ```

  

- 재현

  ```python
  ```

  

- 광휘

  ```python
  ```

  

- 승연

  ```python
  def dfs(start):
      global visited
      if graph[start]:
          visited[start] = 1
          for g in graph[start]:
              if visited[g] == 0:
                  dfs(g)
      else:
          return
  
  computers = int(input())
  n = int(input())
  graph = [[] for _ in range(computers+1)]
  for _ in range(n):
      tmp = tuple(map(int, input().split()))
      graph[tmp[0]].append(tmp[1])
      graph[tmp[1]].append(tmp[0])
  visited = [0]*(computers+1)
  dfs(1)
  ans = visited.count(1)
  print(ans-1)
  ```

  

- 동훈

  ```python
  ```

  



### 백준 2667 : 단지번호 붙이기

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def bfs(i, j):
      q = list()
      q.append((i, j))
      visited[i][j] = 1
      cnt = 1
      while q:
          v = q.pop(0)
          for di, dj in ((-1, 0), (0, 1), (1, 0), (0, -1)):
              ni, nj = v[0] + di, v[1] + dj
              if 0 <= ni < n and 0 <= nj < n and arr[ni][nj] == 1 and visited[ni][nj] == 0:
                  cnt += 1
                  q.append((ni, nj))
                  visited[ni][nj] = 1
      return cnt
  
  n = int(input())
  arr = [0]*n
  for _ in range(n):
      arr[_] = list(map(int, input()))
  print(arr)
  danji = list()
  visited = [[0]*n for _ in range(n)]
  for r in range(n):
      for c in range(n):
          if arr[r][c] == 1 and visited[r][c] == 0:
              num = bfs(r, c)
              danji.append(num)
  danji.sort()
  print(len(danji))
  for a in danji:
      print(a)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 1012 : 유기농 배추

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def bfs(i, j):
      q = list()
      q.append((i, j))
      visited[i][j] = 1
      while q:
          v = q.pop(0)
          for di, dj in ((-1, 0), (0, 1), (1, 0), (0, -1)):
              ni, nj = v[0] + di, v[1] + dj
              if 0 <= ni < N and 0 <= nj < M and arr[ni][nj] == 1 and visited[ni][nj] == 0:
                  q.append((ni, nj))
                  visited[ni][nj] = 1
  
  T = int(input())
  for tc in range(T):
      M, N, K = map(int, input().split())
      arr = [[0]*M for _ in range(N)]
      for k in range(K):
          x, y = map(int, input().split())
          arr[y][x] = 1
  
      cnt = 0
      visited = [[0]*M for _ in range(N)]
      for r in range(N):
          for c in range(M):
              if arr[r][c] == 1 and visited[r][c] == 0:
                  cnt += 1
                  bfs(r, c)
      print(cnt)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 2178 : 미로 탐색

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def bfs():
      q = [(0, 0, 1)]
      front = -1
      visited[0][0] = 1
      while q:
          front += 1
          v = q[front]
          if v[0] == N-1 and v[1] == M-1:
              return v[2]
          cnt = v[2] + 1
          for di, dj in ((-1, 0), (0, 1), (1, 0), (0, -1)):
              ni, nj = v[0] + di, v[1] + dj
              if 0 <= ni < N and 0 <= nj < M and arr[ni][nj] == 1 and visited[ni][nj] == 0:
                  q.append((ni, nj, cnt))
                  visited[ni][nj] = 1
  
  N, M = map(int, input().split())
  arr = [0]*N
  for _ in range(N):
      arr[_] = list(map(int, input()))
  visited = [[0]*M for _ in range(N)]
  road = bfs()
  print(road)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 7576 : 토마토

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def tomato(q):
      global visited
      while q:
          v = q.pop(0)
          cnt = visited[v[0]][v[1]]
          for dr, dc in ((-1, 0), (0, 1), (1, 0), (0, -1)):
              nr, nc = v[0] + dr, v[1] + dc
              if 0 <= nr < N and 0 <= nc < M and visited[nr][nc] == 0:
                  q.append((nr, nc))
                  visited[nr][nc] = cnt + 1
      for r in range(N):
          if 0 in visited[r]:
              return -1
      result = max(map(max, visited))
      return result - 1
  
  
  M, N = map(int, input().split())
  arr = [0]*N
  rot = list()
  visited = [[0]*M for _ in range(N)]
  already = 0
  for i in range(N):
      arr[i] = list(map(int, input().split()))
      for j in range(M):
          if arr[i][j] == 1:
              rot.append((i, j))
              visited[i][j] = 1
          if arr[i][j] == -1:
              visited[i][j] = 1
      if 0 not in arr[i]:
          already += 1
  if already == N:
      day = 0
  else:
      day = tomato(rot)
  print(day)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 7569 : 토마토(3차원)

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 1697 : 숨바꼭질

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def find(n):
      global visited
      q = [(n, 0)]
      while q:
          v = q.pop(0)
          if v[0] == k:
              return v[1]
          else:
              cnt = v[1] + 1
              if 0 <= v[0]-1 <= 100000 and v[0]-1 not in visited and v[0]-1 != n:
                  q.append((v[0]-1, cnt))
                  visited.append(v[0]-1)
              if 0 <= v[0]+1 <= 100000 and v[0]+1 not in visited and v[0]+1 != n:
                  q.append((v[0]+1, cnt))
                  visited.append(v[0]+1)
              if 0 <= 2*v[0] <= 100000 and 2*v[0] not in visited and v[0]*2 != n:
                  q.append((2*v[0], cnt))
                  visited.append(2*v[0])
  
  n, k = map(int, input().split())
  visited = list()
  ans = find(n)
  print(ans)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 2206 : 벽 부수고 이동하기

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def bfs():
      q = [(0, 0, 1, 0)]
      visited.append((0, 0, 1, 0))
      while q:
          v = q.pop(0)
          if (v[0], v[1]) == (N-1, M-1):
              return v[2]
          cnt = v[2]+1
          wall = v[3]
          for dr, dc in ((-1, 0), (0, 1), (1, 0), (0, -1)):
              nr, nc = v[0] + dr, v[1] + dc
              if 0 <= nr < N and 0 <= nc < M:
                  if arr[nr][nc] == 0 and (nr, nc, cnt, wall) not in visited:
                      q.append((nr, nc, cnt, wall))
                      visited.append((nr, nc, cnt, wall))
                  elif arr[nr][nc] == 1 and wall == 0 and (nr, nc, cnt, 1) not in visited:
                      q.append((nr, nc, cnt, 1))
                      visited.append((nr, nc, cnt, 1))
      return -1
  
  
  N, M = map(int, input().split())
  arr = [0]*N
  for _ in range(N):
      arr[_] = list(map(int, input()))
  visited = list()
  ans = bfs()
  print(ans)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 7562 : 나이트의 이동

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def bfs(start):
      q = [(start[0], start[1], 0)]
      cnt = 0
      visited[start[0]][start[1]] = 1
      while q:
          v = q.pop(0)
          if (v[0], v[1]) == goal:
              return v[2]
          cnt = v[2] + 1
          for dr, dc in ((-2, 1), (-1, 2), (1, 2), (2, 1), (2, -1), (1, -2), (-1, -2), (-2, -1)):
              nr, nc = v[0] + dr, v[1] + dc
              if 0 <= nr < pan and 0 <= nc < pan and visited[nr][nc] == 0:
                  q.append((nr, nc, cnt))
                  visited[nr][nc] = 1
  
  
  T = int(input())
  for tc in range(T):
      pan = int(input())
      now = tuple(map(int, input().split()))
      goal = tuple(map(int, input().split()))
      visited = [[0]*pan for _ in range(pan)]
      ans = bfs(now)
      print(ans)
  ```

  

- 동훈

  ```python
  
  ```

  



### 백준 1707 : 이분 그래프

- 준구

  ```python
  
  ```

  

- 재현

  ```python
  
  ```

  

- 광휘

  ```python
  
  ```

  

- 승연

  ```python
  def bfs():
      q = [1]
      visited[1] = 1
      while q:
          v = q.pop(0)
          for g in graph[v]:
              if visited[g] == 1:
                  return 'NO'
              else:
                  q.append(g)
                  visited[g] = 1
      return 'YES'
  
  K = int(input())
  for tc in range(K):
      V, E = map(int, input().split())
      graph = [[] for _ in range(V+1)]
      for _ in range(E):
          u, v = map(int, input().split())
          graph[u].append(v)
      visited = [0]*(V+1)
      ans = bfs()
      print(ans)
  ```

  

- 동훈

  ```python
  
  ```

  