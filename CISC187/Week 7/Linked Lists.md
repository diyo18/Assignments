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

struct Node // given in instructions
{
    int data;
    Node* next;
};

// given in instructions
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

// given in instructions
Stack::Stack()
{
    head = nullptr;
}
// push function which creates a new node and places it at the front (head)
void Stack::push(int value)
{
  Node* newNode = new Node;
  newNode->data = value;
  newNode->next = head;
  head = newNode;
}
// removes the node at the head
void Stack::pop()
{
  if(isEmpty()) // if empty, lets us know we can't pop from empty stack
    {
      cout << "Stack Underflow" << endl;
      return;
    }
    Node* temp = head; // saving current head
    head = head ->next; // move head down to the next node
    delete temp; // free up the memory of the old uneeded head
}
// observes and returns value without removing from the head
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

// function to print all elements
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

// inserting elements into stack by calling previous functions
int main()
{
  Stack s;
 
  s.push(10);
  s.push(20);
  s.push(30);
  s.push(40);
 
  s.display();
  cout << endl;
 
  s.pop(); // remove top
 
  cout << "Top element: " << s.peek() << endl; // show new top
  cout << endl;
 
  s.display(); // show new stack
  cout << endl;

// remove rest of elements including triggering the underflow to test
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

