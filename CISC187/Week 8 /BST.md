## Binary Search Trees Tasks
1. Imagine you were to take an empty binary search tree and insert the following sequence of numbers in this order: [1, 5, 9, 2, 4, 10, 6, 3, 8]. Draw a diagram showing what the binary search tree would look like. Remember, the numbers are being inserted in the order presented here. **(2 points)**
<img width="603" height="674" alt="image" src="https://github.com/user-attachments/assets/6caf66ea-cbea-427f-91bd-164742dda2d7" />

##
2. If a well-balanced binary search tree contains 1,000 values, what is the maximum number of steps it would take to search for a value within it? **(1 point)**

Max number of steps is equal to the height of the tree which is calculated by base 2 logarithm, so Log2(1000) = which would be 10 steps max it would take to search for a value within that BST.
##
3. Write an algorithm that finds the greatest value within a binary search tree. **2 points)**

```
function GreatestValue(node)
  if node has no right child:
    return node.value
  else:
    return GreatestValue(right child of node)
```

##
4. Write a code in C++ using the same array mentioned in #1 and implement a binary search tree. Only insertion operation is required. **(5 points)**


```cpp
#include <iostream>
using namespace std;

struct BstNode {
int value; // number stored in node
BstNode* left; // pointer to left child
BstNode* right; // pointer to right child
};

//builds new node and returns pointer to new node
BstNode* createBstNode(int value) {
BstNode* newNode = new BstNode();
  newNode->value = value;
  newNode->left = nullptr;
    newNode->right = nullptr;
return newNode;
}

//takes current node and number that is being inserted
BstNode* insertNode(BstNode* root, int value) {
  //sees if there is a pointer, if not, it creates a new node so it can be assigned
  if (root == nullptr) {
    return createBstNode(value);
}
  // if smaller go left
  if (value < root->value) {
      root->left = insertNode(root->left, value);
  }
    // if bigger go right
    else if (value > root->value) {
    root->right = insertNode(root->right, value);
    }

return root;
}

int main() {
// shows that root is a pointer to the node I created
BstNode* root = nullptr;

//inserting values from array into nodes
root = insertNode(root, 1);
root = insertNode(root, 5);
root = insertNode(root, 9);
root = insertNode(root, 2);
root = insertNode(root, 4);
root = insertNode(root, 10);
root = insertNode(root, 6);
root = insertNode(root, 3);
root = insertNode(root, 8);

  return 0;
}
```
