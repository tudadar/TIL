<h1>큐</h1>

큐는 선입선출(FIFO, First In First Out) 방식으로 데이터를 저장하는 자료 구조입니다.<br/>
큐는 데이터를 줄을 서서 기다리는 것과 같은 구조를 가지고 있습니다.<br/>

<h2>큐의 특징</h2>

데이터는 선입선출 방식으로 저장됩니다.<br/>
데이터의 접근과 처리가 빠릅니다.<br/>
데이터의 크기가 가변적입니다.<br/>

<h2>큐의 종류</h2>

순수 큐: 큐의 데이터가 모두 같은 자료형인 경우를 말합니다.<br/>
일반 큐: 큐의 데이터가 서로 다른 자료형인 경우를 말합니다.<br/>

순수 큐 예시

```Python
# 순수 큐 클래스를 정의합니다.
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, data):
        self.queue.append(data)

    def dequeue(self):
        return self.queue.pop(0)

    def is_empty(self):
        return len(self.queue) == 0

# 큐를 생성합니다.
queue = Queue()

# 큐에 데이터를 삽입합니다.
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

# 큐에서 데이터를 꺼냅니다.
print(queue.dequeue()) # 1
print(queue.dequeue()) # 2
print(queue.dequeue()) # 3

# 큐가 비어 있는지 확인합니다.
print(queue.is_empty()) # True

```

일반 큐 예시

```Python
# 일반 큐 클래스를 정의합니다.
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, data):
        self.queue.append(data)

    def dequeue(self):
        return self.queue.pop(0)

    def is_empty(self):
        return len(self.queue) == 0

# 큐를 생성합니다.
queue = Queue()

# 큐에 데이터를 삽입합니다.
queue.enqueue(1)
queue.enqueue(2.0)
queue.enqueue("Hello")

# 큐에서 데이터를 꺼냅니다.
print(queue.dequeue()) # "Hello"
print(queue.dequeue()) # 2.0
print(queue.dequeue()) # 1

# 큐가 비어 있는지 확인합니다.
print(queue.is_empty()) # True
```

<h2>큐를 사용할때 주의사항</h2>

큐는 선입선출 방식으로 데이터를 저장하기 때문에, 데이터를 꺼내고 싶다면 항상 가장 먼저 삽입된 데이터를 꺼내야 합니다.</br>
큐의 크기가 가변적이기 때문에, 큐의 크기를 초과하여 데이터를 삽입하거나 꺼낼 수 있습니다.</br>
