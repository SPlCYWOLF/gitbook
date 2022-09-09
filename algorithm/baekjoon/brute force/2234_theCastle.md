# 🍸백준 2234번 - The Castle

[문제출처](https://www.acmicpc.net/problem/2234)

---

### 목표 :

- 주어진 성의 지도를 입력받아서 아래 3가지를 구하라 :
  1. 이 성에 있는 방의 개수
  2. 가장 넓은 방의 넓이
  3. 하나의 벽을 제거하여 얻을 수 있는 가장 넓은 방의 크기
- 벽에 대한 정보는 한 정수로 주어지고 각 방향의 값을 더한 값이 주어진다 :
  1. 서쪽에 벽이 있을 때는 1
  2. 북쪽에 벽이 있을 때는 2
  3. 동쪽에 벽이 있을 때는 4
  4. 남쪽에 벽이 있을 때는 8

<br>

### 풀이 :

- bfs돌면서 가장 넓은 방 저장
  bfs다 돌면 방 개수 + 1
  bfs돌면서 room_record 2차원 리스트에 방 번호 기록
- bfs 돌면서 벽을 판단하는 방법 :
  - 16비트 2진수 표시법을 활용하면 벽의 표시 기준인 [남: 1, 동: 2, 북: 4, 서: 8] 마다
    해당 비트 위치의 2진수가 0 혹은 1임에 따라 벽의 유무를 판단 가능하다.
    예시 : bin(11) => 1011 => 동쪽만 벽이 없음
- 각 방의 넓이는 area_record = dict() 에 저장해 놓음
- 추후 room_record 돌면서 각 방의 우측 & 아래 탐색하며 다른 방 찾으면, 두 방 넓이의 최대 합 갱신.

- ```python
  from collections import deque
  import sys
  sys.stdin = open('input.txt')
  
  
  # 남 동 북 서 (하-> 우-> 상-> 좌)
  dr = (1, 0, -1, 0)
  dc = (0, 1, 0, -1)
  
  def bfs(r, c, room_num):
      global room_record
      Q = deque()
      Q.append((r, c))
      area = 1
      while Q:
          r, c = Q.popleft()
  
          walls = bin(castle[r][c])[2::]  # 2진수로 변환 후
          while len(walls) < 4:           # 16비트 모양을 (str 네개) 맞춰주기 위한 작업
              walls = "0" + walls
  
          for k in range(4):
              if walls[k] == "0":
                  nr, nc = r + dr[k], c + dc[k]
                  if not visited[nr][nc]:
                      visited[nr][nc] = 1
                      room_record[nr][nc] = room_num
                      area += 1
                      Q.append((nr, nc))
      return area						# 해당 방의 넓이 반환
  
  
  M, N = map(int, input().split())
  castle = tuple(tuple(map(int, input().split())) for _ in range(N))
  
  room_record = [[0] * M for _ in range(N)]
  area_record = dict()
  
  visited = [[0] * M for _ in range(N)]
  room_num = 0
  for i in range(N):                      # 각 방의 넓이 bfs
      for j in range(M):
          if not visited[i][j]:
              room_num += 1
              visited[i][j] = 1
              room_record[i][j] = room_num
              area_record[room_num] = bfs(i, j, room_num)
  
  largest_area = max(area_record.values())        # 최대 넓이
  
  double_largest_area = 0
  for i in range(N):                      # 두개의 방 더하며 최대 넓이의 합 탐색
      for j in range(M):
          cur_room_num = room_record[i][j]
          for k in range(2):
              nr, nc = i + dr[k], j + dc[k]
              if 0 <= nr < N and 0 < nc < M:
                  next_room_num = room_record[nr][nc]
                  if cur_room_num != next_room_num:
                      room_sum = area_record[cur_room_num] + area_record[next_room_num]
                      double_largest_area = max(double_largest_area, room_sum)
  
  print(room_num)
  print(largest_area)
  print(double_largest_area)
  ```