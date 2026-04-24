## Tasks
1. Create a theoretical graph using a pen and paper OR electronically. **(2 points)**
<img width="1237" height="1600" alt="image" src="https://github.com/user-attachments/assets/64543dc5-a3f7-4ba9-83e0-00955ee29f96" />

##
2. Implement the graph created in step 1 and apply breadth and depth-first search algorithms using C++. **(6 points)**

```
#include <iostream>
#include <vector>
#include <queue>
#include <stack>

// 0 = great white , 1 = hammerhead , 2 = bull , 3 = tiger , 4 = whale , 5 = mako , 6 = nurse

int main() {

  std::vector<std::vector<int>> sharks(7);

  // great white and hammerhead
  sharks[0].push_back(1);
  sharks[1].push_back(0);

  // great white and bull
  sharks[0].push_back(2);
  sharks[2].push_back(0);

  // hammerhead and tiger
  sharks[1].push_back(3);
  sharks[3].push_back(1);

  // hammerhead and whale
  sharks[1].push_back(4);
  sharks[4].push_back(1);

  // bull and whale
  sharks[2].push_back(4);
  sharks[4].push_back(2);

  // bull and mako
  sharks[2].push_back(5);
  sharks[5].push_back(2);

  // tiger and nurse
  sharks[3].push_back(6);
  sharks[6].push_back(3);

  // whale and nurse
  sharks[4].push_back(6);
  sharks[6].push_back(4);

  // BFS
  std::cout << "BFS: " << "\n";
  std::queue<int> line;
  std::vector<bool> visited(7, false); // create list to show unvisited
  visited[0] = true; // mark first (great white) as visited
  line.push(0); // start great white at the top of the queue

  // loop to check list, remove them, then print them
  while (!line.empty()) {
    int current = line.front();
    line.pop();
    std::cout << current << "";

    // checking for neighbor of shark we removed and adding them to the line
    for (int x : sharks[current]) {
      if (!visited[x]) {
        visited[x] = true;
        line.push(x);
    
        }
    }
}

  // DFS
  std::cout << "\n" << "DFS: " << "\n";
  std::stack<int> stak;
  std::vector<bool> visitedsecond(7, false); // second list to show unvisited
  visitedsecond[0] = true; // mark great white visited
  stak.push(0); // start with great white

  // loop to check each part of the list, print them, then remove them from the stack
  while (!stak.empty()) {
    int current = stak.top();
    stak.pop();
    std::cout << current << "";

    // analyzes neighbors, marks visited, and moves them to the top of the stack
    for (int x : sharks[current]) {
      if (!visitedsecond[x]) {
        visitedsecond[x] = true;
        stak.push(x);
        }
    }
}

std::cout << "\n" << "Reference : 0 = great white , 1 = hammerhead , 2 = bull , 3 = tiger , 4 = whale , 5 = mako , 6 = nurse";
  return 0;
}


```

##
3. Compare both search algorithms in the context of Big O notations. **(2 points)**

Both DFS and BFS are reliant on the number of vertices and edges. These two factors dicatate the speed as it gets larger. This means that their Big O notation is the same : O(V+E). This means that the search algorithms don't differ in speed in the context of big O notation. The only difference between the two is how they go through the graph with BFS creating a queue and going level by level while DFS goes through the whole path.
##
