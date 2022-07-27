# 🎥백준 15591번 - MooTube(silver)

[문제출처](https://www.acmicpc.net/problem/15591)

___

15591_MooTube

### 목표 :

- 주어진 MooTube 그래프(영상과 유사도)를 기반으로, 
  주어지는 인풋 k(최소 유사도)와 v(현재 영상)일 때 추천되는 영상 개수 반환.

<br>

### 풀이 :

- USADO(유사도)로 연결된 동영상(노드)의 그래프를 bfs순회.
  K(최소 유사도) 보다 높은곳을 방문.
- K > 유사도인 경우 어차피 다음 경로로 이동 불가능, 고로 이동 경로상의 유사도의 최솟값 갱신 필요 x
- 중복되는 쌍의 노드가 발생하지 않기때문에 싸이클 형성이 없으니 (노드개수 - 1).
  고로, 굳이 union-find 알고리즘을 활용하여 상호 배타적 집합(Disjoint-set)을 찾음으로써
  노드의 싸이클 형성을 방지할 필요 x.

- ```python
  import sys
  from collections import deque, defaultdict
  sys.stdin = open('input.txt')
  
  
  def bfs(K, current_n):
      visited = [0] * (N+1)       # 농부의 질문마다 방문 값 초기화
      visited[current_n] = 1      # 현재 노드 위치 방문 처리
      Q = deque()
      Q.append((current_n, 99999999))
      cnt = 0                     # 추천되는 동영상 개수 축적
  
      while Q:
          current_n, temp_relevance = Q.popleft()
          for goal_n, relevance in graph[current_n]:
              if relevance >= K and not visited[goal_n]:  # 유사도 & 방문 검증
                  visited[goal_n] = 1
                  cnt += 1        # 추천 되는 비디오 개수 추가
                  Q.append((goal_n, relevance))
      return cnt                  # 정답
  
  
  N, Q = map(int, input().split())
  graph = defaultdict(list)   # key: 현재노드, val: (연결된 노드, 유사도)
  print(graph)
  
  for i in range(N-1):        # 그래프 생성
      p, q, r = map(int, input().split())
      graph[p].append((q, r))
      graph[q].append((p, r))
  print(graph)
  
  for i in range(Q):			# 각 인풋 값 k, v 순회 시작
      k, v = map(int, input().split())
      print(bfs(k, v))
  ```