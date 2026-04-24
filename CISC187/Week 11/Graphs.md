## Tasks
1. Explain with the help of an example __"Why Dijkstra's algorithm fails on negative weights".


To explain why Dijikstra's Algorithm fails, you can picture a graph in your head with A branching out to B and C. The edge to B from A is 100 and C from A is 1. Then C connects to D with 1 and B connects to D with a value of -101. Forming a rhombus.
Dijkstra's algorithm checks to find the shortest path to D. It checks both A to B and A to C. The starting value of 1 for A to C makes it check that path first and label it the fastest without checking the other. 
It ends up with a distance of 2 recorded for A > C >D, and cancels the search through A to B because 100 > 2. The reason this happens is because Dijkstra just assumes that once it finalizes a node, that distance isn't changing. 
This is obviously an oversight by the algorithm because a detailed check through A > B > D would have shown a total distance of -1 which is less than 2 making it the more efficient route. That would be why Dijkstra's algorithm would fail on negative weights.
