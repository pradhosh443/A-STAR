<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: PRADHOSH K M </h3>
<h3>Register Number: 212224060192 </h3>

<H3>AIM</H3>
<p>To Implement A * Search algorithm for a Graph using Python 3.</p>
<H3>ALGORITHM</H3>

``````
1. Initialize OPEN list and CLOSED list.
2. Add the start node to the OPEN list.
3. Set g(start) = 0.
4. Compute h(start) using heuristic.
5. Compute f(start) = g(start) + h(start).

6. While OPEN list is not empty, do:
   a) Select the node with minimum f(n) from OPEN list. Call it q.
   b) Remove q from OPEN list.
   
   c) If q is the goal node:
      - Construct the path from start to goal.
      - Stop the algorithm.

   d) Generate all successors (neighbors) of q.

   e) For each successor:
      i) Compute g(successor) = g(q) + cost(q, successor)
     ii) Compute h(successor) using heuristic
    iii) Compute f(successor) = g + h

     iv) If successor is in OPEN with lower f value, skip it.
      v) If successor is in CLOSED with lower f value, skip it.
     vi) Otherwise:
         - Set parent of successor = q
         - Add successor to OPEN list

   f) Add q to CLOSED list.

7. If OPEN list becomes empty:
   - No solution found.

``````

<hr>
<h2>Sample Graph I</h2>
<hr>

<img width="800" height="517" alt="image" src="https://github.com/user-attachments/assets/e50c6122-a710-4136-9997-6e95911d4d63" />

<hr>
<h2>Sample Graph II</h2>
<hr>

<img width="854" height="501" alt="image" src="https://github.com/user-attachments/assets/5038fd63-ffba-4fbc-978d-382535c35165" />

### PROGRAM
```python
import heapq

def a_star(graph, heuristic, start, goal):
    open_list = []
    heapq.heappush(open_list, (0, start))

    g_cost = {node: float('inf') for node in graph}
    g_cost[start] = 0

    parent = {start: None}

    while open_list:
        current_f, current = heapq.heappop(open_list)

        if current == goal:
            path = []
            while current:
                path.append(current)
                current = parent[current]
            return path[::-1], g_cost[goal]

        for neighbor, cost in graph[current].items():
            new_g = g_cost[current] + cost

            if new_g < g_cost[neighbor]:
                g_cost[neighbor] = new_g
                f_cost = new_g + heuristic[neighbor]
                heapq.heappush(open_list, (f_cost, neighbor))
                parent[neighbor] = current

    return None, float('inf')


# 🔹 INPUT
n, e = map(int, input().split())

graph = {}

# Read edges
for _ in range(e):
    u, v, cost = input().split()
    cost = int(cost)

    if u not in graph:
        graph[u] = {}
    if v not in graph:
        graph[v] = {}

    graph[u][v] = cost

# Read heuristic
heuristic = {}
for _ in range(n):
    node, h = input().split()
    heuristic[node] = int(h)

# 🔹 Start and Goal (you can change if needed)
start = input("Enter start node: ")
goal = input("Enter goal node: ")

# 🔹 RUN
path, cost = a_star(graph, heuristic, start, goal)

# 🔹 OUTPUT15 
if path:
    print("Shortest Path:", " -> ".join(path))
    print("Total Cost:", cost)
else:
    print("No path found")
```
### OUTPUT
#### For sample 1
<img width="400" height="494" alt="image" src="https://github.com/user-attachments/assets/d05189d0-7e39-43ca-9e89-352892b1841b" />

#### For sample 2
<img width="343" height="273" alt="image" src="https://github.com/user-attachments/assets/2931ba83-70bf-4edd-81ac-5a2ad4376ec8" />

### RESULT
Thus , A* search algorithm is implemented for the given graph using python.
