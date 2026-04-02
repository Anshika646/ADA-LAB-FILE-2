# ADA-LAB-FILE-2
def create_matrix(n):
    graph = [[0]*n for i in range(n)]
    edges = [(0,1),(0,2),(1,2),(2,3)]
    for u,v in edges:
        graph[u][v] = 1
        graph[v][u] = 1
    return graph

g = create_matrix(4)
for i in g:
    print(i)
    def create_list():
    graph = {
        0:[1,2],
        1:[0,2],
        2:[0,1,3],
        3:[2]
    }
    return graph
print(create_list())


from collections import deque
def bfs(graph, start):
    visited = set()
    q = deque([start])
      while q:
        node = q.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            for i in graph[node]:
                q.append(i)
graph = create_list()
bfs(graph, 0)




def topo_sort(graph):
    visited = set()
    stack = []
    def dfs(v):
        visited.add(v)
        for i in graph[v]:
            if i not in visited:
                dfs(i)
        stack.append(v)
    for i in graph:
        if i not in visited:
            dfs(i)
    print(stack[::-1])
graph = {
    0:[1,2],
    1:[3],
    2:[3],
    3:[]
}
topo_sort(graph)



import heapq

def dijkstra(graph, start):
    dist = {i:float('inf') for i in graph}
    dist[start] = 0
    pq = [(0,start)]
    while pq:
        d,u = heapq.heappop(pq)
        for v,w in graph[u]:
            if dist[v] > d + w:
                dist[v] = d + w
                heapq.heappush(pq,(dist[v],v))
    return dist
graph = {
    0:[(1,4),(2,1)],
    1:[(3,1)],
    2:[(1,2),(3,5)],
    3:[]
}

print(dijkstra(graph,0))





def bellman_ford(edges, n, start):
    dist = [float('inf')]*n
    dist[start] = 0
    for _ in range(n-1):
        for u,v,w in edges:
            if dist[u] + w < dist[v]:
                dist[v] = dist[u] + w
    return dist

edges = [(0,1,4),(0,2,1),(2,1,-2),(1,3,1),(2,3,5)]
print(bellman_ford(edges,4,0))


import heapq

def prim(graph):
    visited = set()
    pq = [(0,0)]
    cost = 0 
    while pq:
        w,u = heapq.heappop(pq)
        if u not in visited:
            visited.add(u)
            cost += w
            for v,wt in graph[u]:
                if v not in visited:
                    heapq.heappush(pq,(wt,v))
    return cost

graph = {
    0:[(1,4),(2,3)],
    1:[(0,4),(2,1),(3,2)],
    2:[(0,3),(1,1),(3,4)],
    3:[(1,2),(2,4)]
}

print(prim(graph))





def find(parent,x):
    if parent[x]!=x:
        parent[x]=find(parent,parent[x])
    return parent[x]

def union(parent,rank,x,y):
    px = find(parent,x)
    py = find(parent,y)
    
    if rank[px]<rank[py]:
        parent[px]=py
    else:
        parent[py]=px
        if rank[px]==rank[py]:
            rank[px]+=1

def kruskal(edges,n):
    edges.sort(key=lambda x:x[2])
    parent = list(range(n))
    rank = [0]*n
    cost = 0
    for u,v,w in edges:
        if find(parent,u)!=find(parent,v):
            union(parent,rank,u,v)
            cost += w
    return cost

edges = [(0,1,4),(0,2,3),(1,2,1),(1,3,2),(2,3,4)]
print(kruskal(edges,4))



import matplotlib.pyplot as plt

# Nodes and edges
edges = [(0,1),(0,2),(1,2),(2,3)]

# Draw manually
for u,v in edges:
    plt.plot([u,v],[u,v])

plt.scatter([0,1,2,3],[0,1,2,3])

plt.title("Simple Graph Visualization")
plt.show()





import matplotlib.pyplot as plt

# Node positions (manual)
positions = {
    0: (0, 0),
    1: (1, 1),
    2: (2, 0),
    3: (3, 1)
}

edges = [(0,1),(0,2),(1,2),(2,3)]

# Draw edges
for u, v in edges:
    x = [positions[u][0], positions[v][0]]
    y = [positions[u][1], positions[v][1]]
    plt.plot(x, y)

# Draw nodes
for node, (x, y) in positions.items():
    plt.scatter(x, y)
    plt.text(x, y, str(node))

plt.title("Graph Representation ")
plt.show()




import matplotlib.pyplot as plt

# Node positions (manual)
positions = {
    0: (0, 0),
    1: (1, 1),
    2: (2, 0),
    3: (3, 1)
}

edges = [(0,1),(0,2),(1,2),(2,3)]

# Draw edges
for u, v in edges:
    x = [positions[u][0], positions[v][0]]
    y = [positions[u][1], positions[v][1]]
    plt.plot(x, y)

# Draw nodes
for node, (x, y) in positions.items():
    plt.scatter(x, y)
    plt.text(x, y, str(node))

plt.title("Graph Representation ")
plt.show()
