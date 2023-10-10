<h1>그래프</h1>

그래프는 두 개 이상의 정점(vertex)을 간선(edge)으로 연결한 자료 구조입니다.<br/>
그래프는 데이터의 관계를 표현하는 데 적합합니다.<br/>

<h2>그래프의 특징</h2>

데이터의 관계를 표현하는 데 사용됩니다.<br/>
데이터의 접근과 처리가 상대적으로 느릴 수 있습니다.<br/>
데이터의 크기가 가변적입니다.<br/>

<h2>그래프의 종류</h2>

무방향 그래프: 두 정점을 연결하는 간선의 방향이 없는 그래프입니다.<br/>
방향 그래프: 두 정점을 연결하는 간선의 방향이 있는 그래프입니다.<br/>

무방향 그래프 예시

```Python
# 무방향 그래프의 노드 클래스를 정의합니다.
class Node:
    def __init__(self, data):
        self.data = data
        self.neighbors = []

# 무방향 그래프를 생성합니다.
graph = Graph()

# 그래프에 노드를 추가합니다.
graph.add_node(Node(1))
graph.add_node(Node(2))
graph.add_node(Node(3))

# 그래프에 간선을 추가합니다.
graph.add_edge(1, 2)
graph.add_edge(2, 3)
graph.add_edge(3, 1)

# 그래프에서 데이터를 읽어옵니다.
print(graph.nodes[0].data) # 1
print(graph.nodes[1].data) # 2
print(graph.nodes[2].data) # 3
print(graph.edges[0]) # (1, 2)
print(graph.edges[1]) # (2, 3)
print(graph.edges[2]) # (3, 1)
```

방향 그래프 예시

```Python
# 방향 그래프의 노드 클래스를 정의합니다.
class Node:
    def __init__(self, data):
        self.data = data
        self.neighbors = []

# 방향 그래프를 생성합니다.
graph = Graph()

# 그래프에 노드를 추가합니다.
graph.add_node(Node(1))
graph.add_node(Node(2))
graph.add_node(Node(3))

# 그래프에 간선을 추가합니다.
graph.add_directed_edge(1, 2)
graph.add_directed_edge(2, 3)
graph.add_directed_edge(3, 1)

# 그래프에서 데이터를 읽어옵니다.
print(graph.nodes[0].data) # 1
print(graph.nodes[1].data) # 2
print(graph.nodes[2].data) # 3
print(graph.edges[0]) # (1, 2)
print(graph.edges[1]) # (2, 3)
print(graph.edges[2]) # (3, 1)
```

<h2>그래프를 사용시 주의사항</h2>

그래프의 크기가 커질수록 데이터의 접근과 처리가 느려질 수 있습니다.<br/>
그래프의 구조가 복잡할수록 데이터의 접근과 처리가 어려울 수 있습니다.<br/>
