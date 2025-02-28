# Dijkstra's Algorithm in C++

## Overview
Dijkstra's Algorithm is a popular shortest path algorithm used to find the shortest path from a source node to all other nodes in a weighted graph. It works for graphs with non-negative weights.

## Algorithm Explanation
1. Initialize distances from the source to all nodes as infinity, except the source itself, which is set to 0.
2. Use a priority queue (min-heap) to select the node with the smallest known distance.
3. Update the distance of all adjacent nodes if a shorter path is found.
4. Repeat until all nodes are visited or the shortest path to all nodes is determined.

## Code Implementation
```cpp
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9;
vector<pair<int, int>> adj[1005];
vector<int> dist(1005, INF);

void dijkstra(int src) {
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, src});
    dist[src] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d > dist[u]) continue;

        for (auto edge : adj[u]) {
            int v = edge.first;
            int weight = edge.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m;

    for (int i = 0; i < m; i++) {
        int u, v, w;
        cin >> u >> v >> w;
        adj[u].push_back({v, w});
        adj[v].push_back({u, w}); // Remove for directed graph
    }

    int source;
    cin >> source;
    dijkstra(source);

    for (int i = 1; i <= n; i++) {
        cout << "Distance from " << source << " to " << i << " is " << dist[i] << endl;
    }
    return 0;
}
```

## Time and Space Complexity
- **Time Complexity**: 
  - Using a **priority queue (min-heap)**, the time complexity is **O((V + E) log V)**, where **V** is the number of vertices and **E** is the number of edges.
  - Each vertex is processed once, and the priority queue operations take **log V** time.
  - The adjacency list traversal takes **O(E)** time.
- **Space Complexity**: 
  - The adjacency list requires **O(V + E)** space.
  - The distance array and priority queue together use **O(V)** space.
  - Total space complexity: **O(V + E)**.

## How to Run
1. Compile the C++ program using `g++`:
   ```sh
   g++ dijkstra.cpp -o dijkstra
   ```
2. Run the executable:
   ```sh
   ./dijkstra
   ```
3. Provide input:
   - Number of nodes and edges
   - Edges in the format: `u v w` (where `u` and `v` are nodes and `w` is weight)
   - Source node

## Applications of Dijkstra's Algorithm
- Network Routing Protocols
- GPS Navigation Systems
- AI Pathfinding (e.g., game development)
- Traffic and Road Optimization


## License
This project is licensed under the MIT License.
