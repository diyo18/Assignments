# stack.h - Stack class definition

```cpp
struct Node
{
    int data;
    Node* next;
};

class Stack
{
private:
    Node* head;

public:
    Stack();

    void push(int value);
    void pop();
    int peek();
    bool isEmpty();
    void display();
};
```

---

# stack.cpp - Stack implementation


```cpp
Stack::Stack()
{
    head = nullptr;
}

void Stack::push(int value)
{
  Node* newNode = new Node;
  newNode->data = value;
  newNode->next = head;
  head = newNode;
}

void Stack::pop()
{
  if(isEmpty())
    {
      cout << "Stack Underflow" << endl;
      return;
    }
    Node* temp = head;
    head = head ->next;
    delete temp;
}

int Stack::peek()
{
  if (isEmpty())
  {
    cout << "Stack Empty" << endl;
    return -1;
  }
  return head->data;
}

bool Stack::isEmpty()
{
    return head == nullptr;
}

void Stack::display()
{
  if (isEmpty())
  {
    cout << "Stack Empty" << endl;
    return;
  }
  cout << "Stack Elements: " << endl;
  node* current = head;
  while (current != nullptr)
  {
    cout << current->data << endl;
    current = current->next;
  }
}
```

---

# main.cpp - 	Test program


```cpp
int main()
{
  Stack s;
 
  s.push(10);
  s.push(20);
  s.push(30);
  s.push(40);
 
  s.display();
  cout << endl;
 
  s.pop();
 
  cout << "Top element: " << s.peek() << endl;
  cout << endl;
 
  s.display();
  cout << endl;
 
  s.pop();
  s.pop();
  s.pop();
  s.pop();
 
  return 0;
}
```

---

# Entire Program

```cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node* next;
};

class Stack
{
private:
    Node* head;

public:
    Stack();

    void push(int value);
    void pop();
    int peek();
    bool isEmpty();
    void display();
};

Stack::Stack()
{
    head = nullptr;
}

void Stack::push(int value)
{
  Node* newNode = new Node;
  newNode->data = value;
  newNode->next = head;
  head = newNode;
}

void Stack::pop()
{
  if(isEmpty())
    {
      cout << "Stack Underflow" << endl;
      return;
    }
    Node* temp = head;
    head = head ->next;
    delete temp;
}

int Stack::peek()
{
  if (isEmpty())
  {
    cout << "Stack Empty" << endl;
    return -1;
  }
  return head->data;
}

bool Stack::isEmpty()
{
    return head == nullptr;
}

void Stack::display()
{
  if (isEmpty())
  {
    cout << "Stack Empty" << endl;
    return;
  }
  cout << "Stack Elements: " << endl;
  Node* current = head;
  while (current != nullptr)
  {
    cout << current->data << endl;
    current = current->next;
  }
}

int main()
{
  Stack s;
 
  s.push(10);
  s.push(20);
  s.push(30);
  s.push(40);
 
  s.display();
  cout << endl;
 
  s.pop();
 
  cout << "Top element: " << s.peek() << endl;
  cout << endl;
 
  s.display();
  cout << endl;
 
  s.pop();
  s.pop();
  s.pop();
  s.pop();
 
  return 0;
}
```

---
# Result


<img width="612" height="336" alt="image" src="https://github.com/user-attachments/assets/e58322f3-581f-4f72-a6f1-172e15480a13" />

---

