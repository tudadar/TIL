<h1>연결 리스트</h1>

연결 리스트는 데이터를 노드로 연결하여 저장하는 자료 구조입니다.<br/>
연결 리스트는 데이터의 순서와 관계없이 데이터를 저장할 수 있다는 장점이 있습니다.<br/>

<h2>연결 리스트의 특징</h2>

데이터의 순서와 관계없이 저장됩니다.<br/>
데이터의 크기가 가변적입니다.<br/>
데이터의 접근과 처리가 배열보다 느릴 수 있습니다.<br/>

<h2>연결 리스트의 종류</h2>

단일 연결 리스트: 각 노드가 다음 노드의 주소만 저장하는 연결 리스트입니다.<br/>
이중 연결 리스트: 각 노드가 이전 노드와 다음 노드의 주소를 모두 저장하는 연결 리스트입니다.<br/>

단일 연결 리스트 예시

```Python
# 단일 연결 리스트의 노드 클래스를 정의합니다.
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# 단일 연결 리스트를 생성합니다.
head = Node(1)
head.next = Node(2)
head.next.next = Node(3)

# 단일 연결 리스트에서 데이터를 읽어옵니다.
print(head.data) # 1
print(head.next.data) # 2
print(head.next.next.data) # 3

```

이중 연결 리스트 예시

```Python
# 이중 연결 리스트의 노드 클래스를 정의합니다.
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

# 이중 연결 리스트를 생성합니다.
head = Node(1)
head.prev = None
head.next = Node(2)
head.next.prev = head
head.next.next = Node(3)
head.next.next.prev = head.next

# 이중 연결 리스트에서 데이터를 읽어옵니다.
print(head.data) # 1
print(head.next.data) # 2
print(head.next.next.data) # 3
```

<h2>연결 리스트 사용시 주의사항</h2>

연결 리스트의 노드를 삭제할 때는 이전 노드의 다음 노드 주소를 변경해야 합니다.<br/>
연결 리스트의 노드를 삽입할 때는 이전 노드의 다음 노드 주소를 변경해야 합니다.<br/>
