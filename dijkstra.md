# Solution class to implement Dijkstra's Algorithm
```
class Solution {

    // Function to find the shortest distance of all the vertices from the source vertex S
    public int[] dijkstra(int V, ArrayList<int[]>[] adj, int S) {
        // Create a priority queue to store the nodes as a pair {dist, node}
        // The queue will always return the node with the smallest distance first
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);

        // Initialising dist array with a large number to indicate the nodes are unvisited initially
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);

        // Source initialised with dist = 0
        dist[S] = 0;
        pq.offer(new int[]{0, S});

        // Traverse the graph using the priority queue
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int dis = curr[0];  // Distance of the current node
            int node = curr[1];  // Current node

            // Traverse all the adjacent nodes
            for (int[] edge : adj[node]) {
                int adjNode = edge[0];  // Adjacent node
                int weight = edge[1];   // Weight of the edge

                // If the new calculated distance is smaller, update it
                if (dis + weight < dist[adjNode]) {
                    dist[adjNode] = dis + weight;
                    pq.offer(new int[]{dist[adjNode], adjNode});
                }
            }
        }

        return dist;
    }
}

// Main class to test the Solution class
public class Main {
    public static void main(String[] args) {
        // Number of vertices and edges
        int V = 3, E = 3, S = 2;

        // Create adjacency list to represent the graph
        ArrayList<int[]>[] adj = new ArrayList[V];
        for (int i = 0; i < V; i++) {
            adj[i] = new ArrayList<>();
        }

        // Add edges to the graph
        adj[0].add(new int[]{1, 1});
        adj[0].add(new int[]{2, 6});
        adj[1].add(new int[]{2, 3});
        adj[1].add(new int[]{0, 1});
        adj[2].add(new int[]{1, 3});
        adj[2].add(new int[]{0, 6});

        Solution obj = new Solution();
        // Call dijkstra function and store the result
        int[] res = obj.dijkstra(V, adj, S);

        // Output the shortest distance from source to all nodes
        for (int i = 0; i < V; i++) {
            System.out.print(res[i] + " ");
        }
        System.out.println();
    }
}
```
