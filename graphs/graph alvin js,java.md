# Graphs - alvin

## Graphs

* `graph = nodes + edges`
* `nodes (or vertex) = circles with data inside them`
* `edges = connection between nodes`
*  

<img src="C:\ravi\programming_notes\img\g1.png" alt="g1" style="zoom:80%;" />

* `Neighbor node` : accessible directly through any node in direction of the edge 

### Graph representation 

#### Adjacency List

* <img src="C:\ravi\programming_notes\img\g2.png" alt="g2" style="zoom:80%;" />

* A key value pair mapping data structure is used to represent adjacency list 
* unorderedmap in C++/java
* Every node in graphs appears as a key in the list whether it has adjacent nodes or not

#### Depth first traversal

* 

<img src="C:\ravi\programming_notes\img\g3.png" alt="g3" style="zoom:80%;" />

* Depth Search uses a `stack`
* Breadth first uses a `queue` 

 ```java
 package com.sw.graphex;
 
 import java.util.Collections;
 import java.util.HashMap;
 import java.util.List;
 import java.util.Map;
 import java.util.Stack;
 
 public class GraphDS {
 
     public static Map<String, List<String>> graph = new HashMap<>();
 
     public static void addData(String source, List<String> list) {
         // graph.put("a", List.of(new String[] { "b", "c" }));
         graph.put(source, list);
     }
 
     public static void printData() {
         graph.entrySet().forEach(d -> {
             System.out.println(d.getKey() + " => " + d.getValue());
         });
     }
 
     public static void depthFirstPrint(String source) {
         Stack<String> stack = new Stack<>();
         stack.push(source);
 
         while (!stack.empty()) {
             String current = stack.pop();
             System.out.println("visit: " + current);
 
             graph.get(current).forEach(neighbor -> {
                 System.out.println("pushing:  " + neighbor);
                 stack.push(neighbor);
             });
         }
     }
 
     public static void depthFirstRecPrint(String source){
         System.out.println("visiting: "+ source);
         graph.get(source).forEach(neighbor ->{
             depthFirstRecPrint(neighbor);
         });
     }
 
     public static void main(String[] arg) {
 
         addData("a", List.of("c", "b"));
         addData("b", List.of("d"));
         addData("c", List.of("e"));
         addData("d", List.of("f"));
         addData("e", Collections.emptyList());
         addData("f", Collections.emptyList());
 
         //printData();
         //depthFirstPrint("a");
         depthFirstRecPrint("a");
 
     }
 }
 
 ```

* javascript

```js

const depthFirstPrint = (_graph, source) => {
    const stack = [source];
    console.log(_graph);

    // while 
    while (stack.length > 0) {
        // 1. take one out 
        let current = stack.pop();
        // 2. process that node only 
        console.log(current);
        // 3. push all its neighbor to be next in line to be processed 
        for (let neighbor of _graph[current]) {
            stack.push(neighbor);
        }
        // only one neighbor is processed while all of its neighbor is pushed to stack
    }
}

const depthFirstPrintRrc = (_graph, source) => {
    console.log(source);
    // every neighbor branches out as further out as possible and processed on return
    for (let neighbor of graph[source]) {
        depthFirstPrintRrc(_graph, neighbor);
    }
}


const graph = {
    a: ['b', 'c'],
    b: ['d'],
    c: ['e'],
    d: ['f'],
    e: [],
    f: []
};

//depthFirstPrint(graph, 'a');
depthFirstPrintRrc(graph, 'a');
```

#### Breadth first search 

```java
package com.sw.graphex;

import java.util.Collections;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Queue;
import java.util.Stack;
import java.util.concurrent.ConcurrentLinkedQueue;

public class GraphDS {

    public static Map<String, List<String>> graph = new HashMap<>();

    public static void addData(String source, List<String> list) {
        // graph.put("a", List.of(new String[] { "b", "c" }));
        graph.put(source, list);
    }

    public static void printData() {
        graph.entrySet().forEach(d -> {
            System.out.println(d.getKey() + " => " + d.getValue());
        });
    }

    public static void breadthFirst(String source) {
        Queue<String> queue = new LinkedList<>();
        queue.add(source);

        while (!queue.isEmpty()) {
            String current = queue.poll();
            System.out.println(current);
            graph.get(current).forEach(neighbor -> {
                queue.add(neighbor);
            });
        }
    }

    public static void main(String[] arg) {

        addData("a", List.of("c", "b"));
        addData("b", List.of("d"));
        addData("c", List.of("e"));
        addData("d", List.of("f"));
        addData("e", Collections.emptyList());
        addData("f", Collections.emptyList());

        // printData();
        // depthFirstPrint("a");
        // depthFirstRecPrint("a");
        breadthFirst("a");

    }
}

```

* javascript

```js

const breadthFirstPrint = (_graph, source) => {
    let queue = [source];
    //shift removes first element 
    // push adds to last 

    while (queue.length > 0) {
        //1. get the current in queue
        let current = queue.shift();

        // 2. visit that element 
        console.log(current);

        // 3. add each of its neights to queue 
        for (let neighbor of _graph[current]) {
            queue.push(neighbor);
        }

    }
}




const graph = {
    a: ['b', 'c'],
    b: ['d'],
    c: ['e'],
    d: ['f'],
    e: [],
    f: []
};

//depthFirstPrint(graph, 'a');
breadthFirstPrint(graph, 'a');
```

