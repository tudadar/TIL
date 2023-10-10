<h1>스택</h1>

스택은 후입선출(LIFO, Last In First Out) 방식으로 데이터를 저장하는 자료 구조입니다.<br/>
스택은 데이터를 쌓아놓은 것과 같은 구조를 가지고 있습니다.

<h2>스택의 특징</h2>

데이터는 후입선출 방식으로 저장됩니다.<br/>
데이터의 접근과 처리가 빠릅니다.<br/>
데이터의 크기가 가변적입니다.<br/>

<h2>스택의 종류</h2>

순수 스택: 스택의 데이터가 모두 같은 자료형인 경우를 말합니다.<br/>
일반 스택: 스택의 데이터가 서로 다른 자료형인 경우를 말합니다.<br/>

순수 스택 예시

```Python
# 순수 스택 클래스를 정의합니다.
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, data):
        self.stack.append(data)

    def pop(self):
        return self.stack.pop()

    def peek(self):
        return self.stack[-1]

    def is_empty(self):
        return len(self.stack) == 0

# 스택을 생성합니다.
stack = Stack()

# 스택에 데이터를 삽입합니다.
stack.push(1)
stack.push(2)
stack.push(3)

# 스택에서 데이터를 꺼냅니다.
print(stack.pop()) # 3
print(stack.pop()) # 2
print(stack.pop()) # 1

# 스택이 비어 있는지 확인합니다.
print(stack.is_empty()) # True

```

일반 스택 예시

```Python
# 일반 스택 클래스를 정의합니다.
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, data):
        self.stack.append(data)

    def pop(self):
        return self.stack.pop()

    def peek(self):
        return self.stack[-1]

    def is_empty(self):
        return len(self.stack) == 0

# 스택을 생성합니다.
stack = Stack()

# 스택에 데이터를 삽입합니다.
stack.push(1)
stack.push(2.0)
stack.push("Hello")

# 스택에서 데이터를 꺼냅니다.
print(stack.pop()) # "Hello"
print(stack.pop()) # 2.0
print(stack.pop()) # 1

# 스택이 비어 있는지 확인합니다.
print(stack.is_empty()) # True

```

<h2>스택 사용시 주의사항</h2>

스택은 후입선출 방식으로 데이터를 저장하기 때문에, 데이터를 꺼내고 싶다면 항상 가장 마지막에 삽입된 데이터를 꺼내야 합니다.<br/>
스택의 크기가 가변적이기 때문에, 스택의 크기를 초과하여 데이터를 삽입하거나 꺼낼 수 있습니다.<br/>