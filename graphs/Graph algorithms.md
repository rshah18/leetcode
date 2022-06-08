# Graph algorithms

#### Algorithms

1. BFS
2. DFS
3. Topological sort
4. Shortest/Longest path on a DAG
5. Dijkstra's shortest path
6. Bellman Ford 
7. Floyd Warshall
8. Bridges and Articulation points
9. Tarjans strongly connected Components
10. Travelling Salesman problems
11. Eulerian Path
12. Prim's 
13. Ford fulkerson
14. Unweighted Bipartite matching
15. Edmonds karp
16. Dinic Algorithm

#### Problem patterns

1. BFS on Graphs
2. DFS on Graphs
3. BFS or DFS
4. Shortest Path

Matrix as Graph

1. Matrix as Graph
2. Flood fill
3. Number of islands
4. Knight Minimum moves
5. Walls and gates

Implicit graph

1. Open the lock
2. Word ladder
3. Slidding puzzle

Directed graph/ topological sort

1. Task Scheduling 
2. Reconstructing Sequence 
3. Alien Dictionary 
4. Course schedule

Weighted graph

1. Dijsktra's algorithm 
2. Uniform cost search

Minimum Spanning trees

1. Minimum spanning tree/forests



 

## Topological sort

* Visited al the nodes/vertices in depth first search manner and push to the stack upon returning from it
* The element at bottom of stack has no other nodes to visit after it. The element at top of the stack has all the elements under it 

```cpp
class Graph{
    private:
        int vertex_count; 
        vector<int> * adjList;
        
    public:

        Graph(int size){
            vertex_count = size; 
            adjList = new vector<int>[size]; 
        }

        void addEdge(int src, int des){
            adjList[src].push_back(des); 
        }

        void dfs(int start_vertex){
            static vector<bool> visited(vertex_count, false); 
            cout << start_vertex << " "; 
            visited[start_vertex] = true; 
           
            for(auto a: adjList[start_vertex]){
                if(visited[a] == false){
                    dfs(a); 
                }
            }
        }

        void bfs(int start_vertex){
            vector<bool> visited(vertex_count, false); 
            queue<int> q; 
            q.push(start_vertex);
            visited[start_vertex] = true; 

            while(!q.empty()){
                auto current_vertex = q.front(); q.pop();
                cout << current_vertex << " "; 
                
                for(auto a: adjList[current_vertex]){
                    if(visited[a] == false){
                        q.push(a); 
                        visited[a] = true; 
                    }
                }
                
            }

        }

        void dfsTS(int vertex, stack<int> &stk, vector<bool> &visited){
            visited[vertex] = true; 
            for(auto a: adjList[vertex]){
                if(!visited[a]){
                    dfsTS(a, stk, visited);
                } 
            }
            
            stk.push(vertex); 
            
            
        }

        void topologicalSort(){
            vector<bool> visited(vertex_count, false);   
            stack<int>stk; 
            
            for(int i = 0; i < vertex_count; i++){
                if(!visited[i]){
                    dfsTS(i, stk, visited); 
                }
            }
            
            while(!stk.empty()){
                cout << stk.top() << endl; 
                stk.pop(); 
            }

        }
};

```



* 