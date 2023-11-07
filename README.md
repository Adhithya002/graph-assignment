# graph-assignment

2685. Count the Number of Complete Components

You are given an integer n. There is an undirected graph with n vertices, numbered from 0 to n - 1. You are given a 2D integer array edges where edges[i] = [ai, bi] denotes that there exists an undirected edge connecting vertices ai and bi.

Return the number of complete connected components of the graph.

A connected component is a subgraph of a graph in which there exists a path between any two vertices, and no vertex of the subgraph shares an edge with a vertex outside of the subgraph.

A connected component is said to be complete if there exists an edge between every pair of its vertices.

class Solution {
    Set<Integer> vis = new HashSet<>();
    Map<Integer, Set<Integer>> nodes;
    public int countCompleteComponents(int n, int[][] edges) {
        //build graph to store all neighbors of each node, by loop the edge.
        nodes = buidGraph(edges);
        //Do BFS and check for each islands, res++ if complete.
        int result = 0;
        for (int i = 0; i < n; i++) {
            if (vis.contains(i)) continue;
            if (bfs(i)) result++;
        }
        return result;
    }

    private Map<Integer, Set<Integer>> buidGraph(int[][] edges) {
        Map<Integer, Set<Integer>> nodes = new HashMap<>();
        for (int[] e : edges) {
            nodes.putIfAbsent(e[0], new HashSet<>());
            nodes.putIfAbsent(e[1], new HashSet<>());
            nodes.get(e[0]).add(e[1]);
            nodes.get(e[1]).add(e[0]);
        }
        return nodes;
    }

    private boolean bfs(int i) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(i);
        vis.add(i);
        int cntOfNeighs = nodes.getOrDefault(i, new HashSet<>()).size(), numOfNodes = 0;
        boolean result = true;
        while (!q.isEmpty()) {
            int curr = q.poll();
            numOfNodes++;
            if (nodes.getOrDefault(curr, new HashSet<>()).size() != cntOfNeighs) result = false;
            for (int neig : nodes.getOrDefault(curr, new HashSet<>())) {
                if (vis.contains(neig)) continue;
                vis.add(neig);
                q.offer(neig);
            }
        }
        return result && cntOfNeighs == numOfNodes - 1;
    }
} 


Given an undirected graph with V vertices. We say two vertices u and v belong to a single province if there is a path from u to v or v to u. Your task is to find the number of provinces.



//Back-end complete function Template for Java

class Solution {
    
    //Function to perform Depth First Search (DFS) traversal on the adjacency list.
    void dfs(ArrayList<ArrayList<Integer>> M, int[] visited, int i)
    {
        //Iterating through each element in the adjacency list.
        for (int j = 0; j < M.size(); j++)
        {
            //Checking if the element is not the current element being visited, 
            //and if it is connected to current element and is not visited before.
            if (i!=j && M.get(i).get(j) == 1 && visited[j] == 0)
            {
                //Marking the element as visited.
                visited[j] = 1;
                //Recursively calling DFS on the connected element.
                dfs(M, visited, j);
            }
        }
    }
    
    //Function to count the number of provinces using DFS.
    int numProvinces(ArrayList<ArrayList<Integer>> adj, int V) {
        
        //Creating an array to keep track of visited elements.
        int[] visited = new int[adj.size()];
        //Initializing count of provinces to 0.
        int count = 0;
        
        //Iterating through each element in the adjacency list.
        for (int i = 0; i < adj.size(); i++)
        {
            //If the element is not visited, perform DFS on that element and increase count of provinces.
            if (visited[i] == 0)
            {
                //Marking the element as visited.
                dfs(adj, visited, i);
                //Increasing count of provinces.
                count++;
            }
        }
        
        //Returning the count of provinces.
        return count;
    }
};


Given an undirected graph with V nodes and E edges, create and return an adjacency list of the graph. 0-based indexing is followed everywhere.

/Back-end complete function Template for Java
class Solution {
    public List<List<Integer>> printGraph(int V, int edges[][]) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            graph.add(new ArrayList<>());
        }
        for (int i[] : edges) {
            graph.get(i[0]).add(i[1]);
            graph.get(i[1]).add(i[0]);
        }
        return graph;
    }
}


Given a directed graph. The task is to do Breadth First Traversal of this graph starting from 0.


class Solution {
    // Function to return Breadth First Traversal of given graph.
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // boolean list to mark all the vertices as not visited.
        boolean visited[] = new boolean[V];

        int s = 0;
        // initially we mark first vertex as visited(true).
        visited[s] = true;

        ArrayList<Integer> res = new ArrayList<>();

        // creating a queue for BFS and pushing first vertex in queue.
        LinkedList<Integer> q = new LinkedList<Integer>();
        q.add(s);

        while (q.size() != 0) {
            // adding front element in output list and popping it from queue.
            s = q.poll();
            res.add(s);

            // traversing over all the connected components of front element.
            Iterator<Integer> i = adj.get(s).listIterator();
            while (i.hasNext()) {
                int n = i.next();
                // if they aren't visited, we mark them visited and add to
                // queue.
                if (!visited[n]) {
                    visited[n] = true;
                    q.add(n);
                }
            }
        }
        // returning the output list.
        return res;
    }
}
