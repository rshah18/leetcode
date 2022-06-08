# Graph

## Types of Graph

#### Undirected graph

* An undirected graph is a graph in which edges have no orientation. The edge `(u,v)` is identical to the edge `(v,u)` 

#### Directed graphs

* A directed graph or digraph is a graph in which edges have orientations. for eg. `(u,v)` is the edge form node u to node v

#### weighted graphs

* Many graphs can have edges that contain a certain value such as cost, distance, and quantity. 
* An edge in weighted graph can be represented as `(u,v,w)` and specify whether graph is directed or undirected

#### Trees

* A tree is an undirected graph with no cycles.
* Equivalently, it is a connected graph with N nodes and N-1 edges.
* <img src="C:\ravi\LeetCode\img\trees6-3.png" alt="trees6-3" style="zoom:60%;" />

#### Rooted trees

* A rooted tree is a tree with a designated root node where every edge either points away from or towards the root node. 
* When edges point away from the root the graph is called an `arborescence (out-tree)` 
* otherwise `anti-aborescene (in-tree)` 
* <img src="C:\ravi\LeetCode\img\rootdtrees6-3.png" alt="rootdtrees6-3" style="zoom:60%;" />

#### Directed Acylic graph 

* Directed graphs with no cycles
* All out-trees are DAG but not all DAGs are out-trees
* Play an important role in representing structures with dependencies. 

<img src="C:\ravi\LeetCode\img\dag6-3.png" alt="dag6-3" style="zoom:60%;" />

#### Bipartite graph

* A bipartite graph is one whose vertices can be split into two independent groups `U,V` such that every edge connects between `U` and `V` 
* 

<img src="C:\ravi\LeetCode\img\bipartitie6.3.png" alt="bipartitie6.3" style="zoom:60%;" />

#### Complete Graphs

* A complete graph is one where there is a unique edge between every pair of nodes.
* A complete graph with a `n` vertices is denoted as graph `Kn`
* <img src="C:\ravi\LeetCode\img\completegraph6.3.png" alt="completegraph6.3" style="zoom:60%;" />

* Worse case possible graph for performance 

## Representing graphs

#### Adjacency matrix

* A adjacency matrix `m` is a very simple way to represent a graph. 
* The idea is that the cell `m[i][j]` represents the edge weight of going from node `i` to node `j`
* It is assumed that the edge of going from a node to itself has a cost of zero
* <img src="C:\ravi\LeetCode\img\adjacencymatrix6.3.png" alt="adjacencymatrix6.3" style="zoom:60%;" />

* Pros
  * Space efficient for representing dense graphs
  * Edge weight look is `O(1)` 
  * Simplest graph representation 
* Cons
  * Requires `O(v^2)` space
  * Iterating over all edges takes `O(v^2)` 

#### Adjacency List

* An adjacency list is a way to represent a graph as a map from nodes to lists of edges
* <img src="C:\ravi\LeetCode\img\adjacencylist6.3.png" alt="adjacencylist6.3" style="zoom:60%;" />

* Pros
  * Space efficient for representing sparse graphs 
  * Iterating over all edges is efficient 
* Cons
  * Less space efficient for denser graphs
  * Edge weight lookup is `O(E)`
  * Slightly more complex graph representation 

#### Edge list

* An edge list is a way to represent a graph simply as an unordered list of edges.
* Assume the notation for any triplet `(u,v,w)` means:
  * the cost from node `u` to node `v` is `w`
* <img src="C:\ravi\LeetCode\img\edgelist6-3.png" alt="edgelist6-3" style="zoom:60%;" />

* Pros
  * Space efficient for representing sparse graphs
  * Iterating over all edges is efficient 
  * Very simple structure
* Cons
  * Less space efficient for denser graphs
  * Edge weight lookup is `O(E)`

## Common graph theory problems

#### Things to think about

1. Is the graph **directed** or **undirected**

2. Are the edges of the graph weighted

3. Is the graph sparse or dense with edges

4. Should we use `Adjacency matrix` , `Adjacency list` or an `edge list` or other structure

### 1. Shortest path problem

* Given a graph, find the shortest path of edges from node A to node B
* <img src="C:\ravi\LeetCode\img\shortestpath6.3.png" alt="shortestpath6.3" style="zoom:60%;" />

* Algorithms
  * `BFS (unweighted graph)` 
  * `Dijkstra's`
  * `Bellman-Ford`
  * `Floyd-Warshall`
  * `A*`
  * `...`

### 2. Connectivity

* Does there exist a path between node A and node B
* Typical Solution
  * Use union find data structure 
  * Any search algorithm eg DFS
* <img src="C:\ravi\LeetCode\img\connectivity6.3.png" alt="connectivity6.3" style="zoom:60%;" />

### 3. Negative cycles in a directed graph

* Does my weighted digraph have any negative cycles. If so, where?
* <img src="C:\ravi\LeetCode\img\negative cycles 6.3.png" alt="negative cycles 6.3" style="zoom:60%;" />

* Algorithms
  * Bellman-ford
  * Flod0-warshall
* that is does any cycle when added all of its weight produce a negative number

### 4. Strongly connected components

* Strongly connected components  can be thought of as a `self-contained cycles` within a directed graph where every vertex in a given cycle can reach every other vertex in the same cycle
* <img src="C:\ravi\LeetCode\img\stronglyconnectedcomponents6.3.png" alt="stronglyconnectedcomponents6.3" style="zoom:60%;" />

* We are looking for self contained cycles within the graph where every vertex in the cycle should be able to reach every other vertex in that cycle
* Algorithms
  * `Tarjan's` 
  * `Kosaraju's`

### 5. Traveling salesman problem

* Given a list of cities and the distance between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city
* Algorithm
  * `Held-karp`
  * `Branch and bound`
  * `..`

### 6. Bridges

* A `bridge/cut edge` is any edge in a graph whose removal increases the number of connected components
* Bridges are important in graph theory because they often hint at weak points, bottlenecks or vulnerabilies in a graph.
* <img src="C:\ravi\LeetCode\img\bridges6.3.png" alt="bridges6.3" style="zoom:60%;" />

### 7. Articulation points

* An `articulation point/cut vertex` is any node in a graph whose removal increases the number of connected components
* <img src="C:\ravi\LeetCode\img\articulationpoints6.3.png" alt="articulationpoints6.3" style="zoom:60%;" />

* Articulation points are important in graph theory because they often hint at weak points, bottlenecks or vulnerabilities in a graph

### 8. Minimum Spanning Tree 

* A minimum spanning tree is a subset  of the edges of a connected, edge-weighted graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight. 
* A tree that has no cycles and spans the graph at minimal cost
* Algorithms:
  * `kruskal's ` 
  * `Prim's` 
* <img src="C:\ravi\LeetCode\img\mininumspanningtreea6.3.png" alt="mininumspanningtreea6.3" style="zoom:60%;" /><img src="C:\ravi\LeetCode\img\mininumspanningtreeb6.3.png" alt="mininumspanningtreeb6.3" style="zoom:60%;" />

* Minimum spanning trees on a graph are not always unique. 
* Applications
  * Designing a least cost network
  * circuit design 
  * Transportation network

### 9. Network flow: max flow

* With an infinite input source how much flow can we push through the network
* <img src="C:\ravi\LeetCode\img\networkflow6.3.png" alt="networkflow6.3" style="zoom:60%;" />

* Algorithms:
  * `Ford-Fulkerson`
  * `Edmonds-karp`
  * `Dinic's algorithm`

## DFS overview

* It runs with a time complexity of `O(V+E)` 
* By itself the dfs isn't all that useful, but when augmented to perform other tasks such as count connected components, determine connectivity between nodes, find bridges and articulation points

* A DFS plunges depth first into a graph without a regard for which edge it takes next until it cannot go any further at which point it backtracks and continues

* Backtrack when a node ends

* ```
  n = number of nodes in the graph
  g = adjacency list representating graph
  visited = [false..., false] # size n
  
  function dfs(at):
  	if visited[at]: return
  	visited[at] = true
  	
  	neighbours = graph[at]
  	for next in neighbours:
  		dfs(next)
      
      # start dfs at node zero
      start_node = 0
      dfs(start_node)
  ```

#### Connected components

* Assign an integer value to each group to be able to tell them apart

We can use DFS to identify components.	 	

#### dfs usage

* Compute a graph's minimum spanning tree
* Detect and find cycles in a graph
* Check if a graph is bipartite
* Find strongly connected components
* Topologically sort the nodes of a graph
* Find bridges and articulation points
* find augmenting paths in a flow network
* Generate mazes



## BFS overview

* Time complexity: `O(V+E)`

* Particularly useful for one thing: finding the shortest path on unweighted graphs

* A BFS starts at some arbitrary node of a graph and explores the neighbour nodes first, before moving to the next level neighbours  

*  The BFS algorithm uses a queue data structure to track which node to visit next. 

* Upon reaching a new node the algorithm adds it to the queue to visit it later.

* ```
  function solve(s):
      q  = queue data structure with enqueue and dequeue 
      q.enqueue(s)
      
      visited = [false,.... false]
      visited[s] = true
      
      prev = [null, ,,,, null]
      while !q.isEmpty(); 
      node = q.dequeue()
      neighoours = q.get(node)
      
      for(next: neighbours):
      	if !visited[next]:
      		q.enqueue(next)
      		visited[next] = true
      		prev[next] = node
      		
      return prev; 
  ```

### BFS shortest path on a grid

* Grids are a form of implicit graph bacause we can determine a node's neighbours based on our location within the grid

#### Approach

* A Common approach to solving graph theory problems on grids is to first convert the grid to a familiar format such as an adjacency list/matrix
* First label the cells in the grid with numbers `[0,n)` where `n=#rows x #columsn`
* Initialize an adjacency list or adjacency matrix
* <img src="C:\ravi\LeetCode\img\gridproblems6.3.png" alt="gridproblems6.3" style="zoom:60%;" />

* Transformations between graph representations can usually be avoided due to the structure of a grid
* <img src="C:\ravi\LeetCode\img\directionvectors6.3.png" alt="directionvectors6.3" style="zoom:60%;" />

* <img src="C:\ravi\LeetCode\img\diagonal6.3.png" alt="diagonal6.3" style="zoom:60%;" />

#### Direction vector

* ```
  # Define the direction vectors for 
  # north, south, east and west
  
  dr = [-1, +1, 0, 0 ]
  dc = [0, 0, +1, -1 ]
  
  for( i = 0; i < 4; i++ ):
  	rr = r + dr[i];
  	cc = c + dc[i];
  	
  	# skip invalid cells Assume R and C for the number of rows and columns
  	
  	if rr < 0 or cc < 0: continue
  	if rr >= R or cc >= C: continue
  	
  ```

## Dungeon Problem statement

* You are trapped in a 2D dungeon and need to find the quickest way out! The dungeon is composed of unit cubes which may or may not be filled with rock.

* It takes one minute to move one unit north, south, east, west. You cannot move diagonally and the maze is surrounded by solid rock on all sides

* Is an escape possible if so how long will it take?

* The dungeon has a size of `RxC` and you start at cell `S` and there's an exit at cell `E` 

* A cell full of rock is indicated by a `#` and empty cells are represented by a `.`

* <img src="C:\ravi\LeetCode\img\dungeons.png" alt="dungeons" style="zoom:60%;" />

* <img src="C:\ravi\LeetCode\img\dungeons6.3b.png" alt="dungeons6.3b" style="zoom:60%;" />

* Breadth first search from `S` to `E` 

* ```
  #Global/class scope variables
  
  R, C = ... # R = num rows, c = num Cols
  m = .. # input character matrix of size RXC
  sr, sc = # 'S' symbol row and column values
  rq, cq = # Empty row queue (RQ) and Column queue (CQ)
  
  # Variables used to track the number of steps taken
  move_count = 0
  nodes_left_int_layer = 1
  nodes_in_next_layer = 0
  
  # Variable used to track whether the `E` character ever gets reached during the BFS
  reached_end = false
  
  # R X C matrix of false values used to track whether the node at position `(i,j)` has been visited
  visited = ..
  
  #North, south, east, west diretion vectors
  
  dr = [-1, +1, 0, 0]
  dc = [0, 0, +1, -1]
  
  Function solve():
  	rq.enqueue(sr)
  	cq.enqeuue(sc)
  	visited[sr][sc] = true
  	
  	while rq.size() > 0:
  		r = rq.dequeu()
  		c = rq.dequeue()
  		
  		if m[r][c] == 'E';
  			reached_end = true
  			break
      explore_neighbours(r,c)
      nodes_left_in_layer--
      if nodes_left_in_layer == 0 :
      	nodes_in_next_layer = nodes_in_next_layer
      	nodes_in_next_layer = 0
      	move_count++
      if reached_end:
      	return move_count
      return -1
      
      
  ```

## 174. Dungeon Game

Hard

The demons had captured the princess and imprisoned her in **the bottom-right corner** of a `dungeon`. The `dungeon` consists of `m x n` rooms laid out in a 2D grid. Our valiant knight was initially positioned in **the top-left room** and must fight his way through `dungeon` to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to `0` or below, he dies immediately.

Some of the rooms are guarded by demons (represented by negative integers), so the knight loses health upon entering these rooms; other rooms are either empty (represented as 0) or contain magic orbs that increase the knight's health (represented by positive integers).

To reach the princess as quickly as possible, the knight decides to move only **rightward** or **downward** in each step.

Return *the knight's minimum initial health so that he can rescue the princess*.

**Note** that any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/13/dungeon-grid-1.jpg)

```
Input: dungeon = [[-2,-3,3],[-5,-10,1],[10,30,-5]]
Output: 7
Explanation: The initial health of the knight must be at least 7 if he follows the optimal path: RIGHT-> RIGHT -> DOWN -> DOWN.
```

```cpp
class Solution {
public:
    int calculateMinimumHP(vector<vector<int>>& dungeon) {

      if(dungeon.size() == 1 || dungeon[0].size() == 1){
        int wgt = dungeon[0][0];
        return wgt < 1? abs(wgt)+1 : wgt;  // not sure about this part 
      }
      
      queue<pair<int,int>> q;
      q.push(make_pair(0,0));

      int lastHp = 0;

      while(!q.empty()){
        int max_wgt = INT_MIN;
        pair<int,int> max_value_pair;

        int Qsize = q.size();

        // Find the pair with highest health point
        for(int i = 0; i < Qsize; i++){
          auto current = q.front(); q.pop();
          int wgt = dungeon[current.first][current.second];

          if(wgt > max_wgt){
            max_wgt = wgt;
            max_value_pair = current;
          } // if

        } // for loop

        if(max_value_pair.first + 1 < dungeon.size()){
          q.push(make_pair(max_value_pair.first +1, max_value_pair.second));
        }

        if(max_value_pair.second+1 < dungeon[max_value_pair.first].size()){
          q.push(make_pair(max_value_pair.first, max_value_pair.second+1));
        }

        lastHp += max_wgt;

      }// while loop


      return lastHp < 1 ? abs(lastHp)+1 : lastHp;  
    }
};

```

## Topological sort

* Many real world situations can be modelled as a graph with directed edges where some events must occur before others
  * School class prerequisites
  * Program dependencies 
  * Event scheduling 
  * etc
* A topological ordering is an ordering of the nodes in a directed graph where for each directed graph from node A to node B, node A appears before node B in the ordering. 
* The topological sort algorithm can find a topological ordering in `O(V+E)` time
* Topological orderings are not NOT unique
* <img src="C:\ravi\LeetCode\img\topologicalordering6.4.png" alt="topologicalordering6.4" style="zoom:60%;" />

* Not every graph can have a topological ordering. A graph which contains a cycle cannot a valid ordering 
* The only type of graph which has a valid topological ordering is a `Directed Acyclic Graph (DAG)` These are graphs with directed edges and no cycles.

* Not contain a directed cycle?
  * One method is to use Tarjan's strongly connected component algorithm which can be used to find these cycles

* By Definition, all rooted trees have a topological ordering since they do not contain any cycles

#### Topological sort algorithm

* Pick an unvisited node
* Beginning with the selected node, do a Depth first search exploring only unvisited nodes
* On the recursive callback of the DFS, add the current node to the topological ordering in reverse order.
*  Steps
  * Pick an unvisited node
  * recursive dfs calls
  * keep exploring until end node if it an end node push it in reverse order to the table
  * explore further
  * When you at node whose adjacent nodes have already been visited you now backtrack from that node adding it to the table
  * once all node are visited by the one that was picked 
  * Pick another and repeat

* ```
  #Assumption: graph is stored as adjacency list
  
  function topSort(graph):
  	N = graph.numberofnodes() # length N
  	v = [false....false]; # length N
  	i = N -1  # index for odering Array
  	
  	for( at = 0; at < N; at++):
  		if V[at] == false:
  			visitedNodes = []
  			for nodeId in visitedNodes:
  				ordering[i] = nodeId
  				i--; 
          return ordering 	
  ```



* Topological sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering. 
* Topological Sorting for a graph is not possible if the graph is not a DAG.
* steps
  * When unvisited neighbours of graph is found push it to the stack





## Dijkstra's algorithm

* Single source shortest path problem
* for a weighted graph find shortest path from some starting vertex to all other vertices 
* Optimization problems can be solved using greedy method
*  







# merge sort