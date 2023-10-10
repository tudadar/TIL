<h1>트리</h1>

트리는 계층적인 구조로 데이터를 저장하는 자료 구조입니다.<br/>
트리는 데이터를 노드로 연결하여 저장하기 때문에, 데이터의 계층 관계를 표현하기에 적합합니다.<br/>

<h2>트리의 특징</h2>

데이터는 계층적인 구조로 저장됩니다.<br/>
데이터의 접근과 처리가 빠릅니다.<br/>
데이터의 크기가 가변적입니다.<br/>

<h2>트리의 종류</h2>

이진 트리: 각 노드가 최대 2개의 자식 노드를 가지고 있는 트리입니다.<br/>
일반 트리: 각 노드가 임의의 개수의 자식 노드를 가지고 있는 트리입니다.<br/>

이진 트리 예시

```Python
# 이진 트리의 노드 클래스를 정의합니다.
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# 이진 트리를 생성합니다.
root = Node(1)
root.left = Node(2)
root.right = Node(3)

# 이진 트리에서 데이터를 읽어옵니다.
print(root.data) # 1
print(root.left.data) # 2
print(root.right.data) # 3
```

일반 트리 예시

```Python
# 일반 트리의 노드 클래스를 정의합니다.
class Node:
    def __init__(self, data):
        self.data = data
        self.children = []

# 일반 트리를 생성합니다.
root = Node(1)
root.children.append(Node(2))
root.children.append(Node(3))
root.children[0].children.append(Node(4))
root.children[0].children.append(Node(5))

# 일반 트리에서 데이터를 읽어옵니다.
print(root.data) # 1
print(root.children[0].data) # 2
print(root.children[1].data) # 3
print(root.children[0].children[0].data) # 4
print(root.children[0].children[1].data) # 5
```

<h2>트리 사용시 주의점</h2>
트리의 깊이가 깊어질수록 데이터의 접근과 처리가 느려집니다.<br/>
트리의 균형이 맞지 않으면, 데이터의 접근과 처리가 비효율적일 수 있습니다.<br/>
