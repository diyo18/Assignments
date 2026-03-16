## Task
1. Using Figure 17 as a model, in the book [Data Structures in C++](https://d-khan.github.io/ds), illustrate the result of each operation in the sequence PUSH(S,4), PUSH(S,1), PUSH(S,3), POP(S), PUSH(S,8), and POP(S) on an initially empty stack $S$ stored in array $S[1..6]$.

Answer in Week 6 Folder (issue prevented me from uploading directly into this document)
##
2. Using Figure 18 as a model, in the book [Data Structures in C++](https://d-khan.github.io/ds), illustrate the result of each operation in the sequence ENQUEUE(Q,4), ENQUEUE(Q,1), ENQUEUE(Q,3), DEQUEUE(Q), ENQUEUE(Q,8), and DEQUEUE(Q) on an initially empty queue $Q$ stored in array $Q[1..6]$. ***Code is not required.*** **3 pts**

Answer in Week 6 Folder (issue prevented me from uploading directly into this document)
##
3. Rewrite ENQUEUE and DEQUEUE to detect ***underflow*** and ***overflow*** of a queue. (see Listings 4 & 5 in the book). ***Code is not required.*** **1 pt**

Enqueue

```
if Q.head == Q.tail + 1
  error "overflow"
Q[Q.tail] = x
if Q.tail == Q.length
    Q.tail = 1
else Q.tail = Q.tail + 1
```
Dequeue

```
if Q.head == Q.tail
  error "underflow"
x = Q[Q.head]
if Q.head == Q.length
    Q.head = 1
else Q.head = Q.head + 1
return x
```
##
4. A stack allows insertion and deletion of elements at only end, and a queue allows insertion at one end and deletion at the other end, a **deque** (double-ended queue) allows insertion and deletion at both ends. Write four $O(1)$-time procedures to insert elements into and delete elements from both ends of a deque implemented by an array. ***Code is not required.*** **3 pts**

Insert Front
```
Q.head = Q.head - 1
Q[Q.head] = x
```
Insert Rear
```
Q[Q.tail] = x
Q.tail = Q.tail + 1
```
Delete Front
```
x = Q[Q.head]
Q.head = Q.head + 1
return x
```
Delete Rear
```
Q.tail = Q.tail - 1
x = Q[Q.tail]
return x
```
