---
title: Graph Algorithms
date: 2018-12-11 16:26:47
tags: 
- graph
- data structure
- algorithm
categories: 
- programming
---

## 1. Graphs

### Composed by 

- vertices 

- edges

### Classified by

- undirected graph : all edges are undirected

- directed graph : all edges are directed

- mixed graph : otherwise

(* mixed graph can be represented by a directed graph where the undirected edge is divided to two directed edge)

### Concepts - part 1

- The two vertices joined by an edge are called **end vertices(endpoints)** of the edge. If the edge is directed, the first endpoint is **origin** and the other is the **destination** of the edge

- The two endpoints of an edge are said to be **adjacent**. 

- An edge is said to be **incident** to its endpoints.

- origin -> **outcoming edge**; destination <- **incoming edge**. 

- The number of incident edges of a vertex v is called its **degree**, denoted as deg(v).

- **in-degree** indeg(v); **out-degree** outdeg(v)

### Concepts - part 2

- The definition of a graph refers to the group of edges as a **collection** rather than a **set**. So two edges can have the same endpoints, which are called **parallel edges** or **multiple edges**. 

- If two vertices coincide we call the edge **self-loop**.

- Graphs that do not have parallel edges or self-loops are called **simple**. The edges of a simple graph are a **set** of vertex pairs. Usually we just assume a graph is simple.  



### Concepts - part 3

- A **path** is a sequence of alternating vertices and edges that starts at a vertex and ends at a vertex; a **cycle** is a path that starts and ends at the same vertex; we say a path (or cycle) is **simple** if each vertex in the cycle is distinct (except for the first and last one).

- **directed path** and **directed cycle**

### Concepts - part 4

- If there is a directed path from u to v, then we say u **reaches** v, or v is **reachable** from u. 

- In an undirected graph, the notion of **reachability** is symmetric. 

- A graph is **connected** if for any two vertices there is a path between them, and is **strongly connected** if for any two vertices one can reach the other.

- **subgraph**; **spanning subgraph**: a subgraph of G that contains all the vertices of G; **connected components**: the maximal connected subgraphs of G.

- **forest**: a graph without cycles. A **tree** is a connected forest. A **spanning tree** of a graph is a spanning subgraph that is a tree. 

### Propositions

- $$\sum_{v\ in\  V} deg(v) = 2m$$

- $$\sum_{v\ in \ V} indeg(v) = \sum_{v\ in\ V} outdeg(v) = m$$

- Graph G has n verticles and m edges, then if G is undirected, 
$$m \leq n(n-1)/2$$
else if G is directed, 
$$m \leq n(n-1)$$

- If G is connected, then $m\geq n-1$

- If G is a tree, then $m = n-1$

- If G is a forest, then $m \leq n-1$

### The Graph ADT

Three data types: Vertex, Edge, Graph

- Vertex:
    - element()
    
- Edge:
    
    - element()
    - endpoints()
    - opposite(v)

- Graph:
    - vertex_count()
    - vertices()
    - edge_count()
    - edges()
    - get_edge(u,v)
    - degree(v, out=True)
    - incident_edges(v, out=True)
    - insert_vertex(x=None)
    - insert_edge(u, v, x=None)
    - remove_vertex(v)
    - remove_edge(e)

## 2. Data Structures for Graphs

- **edge list**
- **adjacency list**
- **adjacency map**
- **adjacency matrix**

An implementation of graph with adjacency map:


```python
class Vertex:
    
    __slots__ = '_elements'
    
    def __init__(self,x):
        self._element = x
        
    def element(self):
        return self.element
    
    def __hash__(self):
        return hash(id(self))
    
class Edge:
    
    __slots__ = '_origin', '_destination', '_element'
    
    def __init__(self, u, v, x):
        self._origin = u
        self._destination = v
        self._element = x
        
    def endpoints(self):
        return (self._orgin, self._destination)
    
    def opposite(self, v):
        return self._destination if v is self._origin else self._origin
    
    def element(self):
        return self._element
    
    def __hash__(self):
        return hash((self._origin, self._destination))
    
class Graph:
    
    def __init__(self, directed= False):
        self._outgoing = {}
        self._incoming = {} if directed else self._outgoing
    
    def is_directed(self):
        return self._incoming is not self._outgoing
    
    def vertex_count(self):
        return len(self._outgoing)
    
    def vertices(self):
        return self._outgoing.keys()
    
    def edge_count(self):
        total = sum(len(self_outgoing[v]) for v in self._outgoing)
        return total if self.is_directed() else total//2
    
    def edges(self):
        result = set()
        for secondary_map in self._outgoing.values():
            result.update(secondary_map.values())
        return result
    
    def get_edge(self, u, v):
        return self._outgoing[u].get(v)
    
    def degree(self, v, outgoing=True):
        adj = self._outgoing if outgoing else self._incoming
        return len(adj[v])
    
    def incident_edges(self, v, outgoing=True):
        adj = self._outgoing if outgoing else self._incoming
        for edge in adj[v].values():
            yield edge
            
    def insert_vertex(self, x=None):
        v = self.Vertex(x)
        self._outgoing[v] = {}
        if self.is_directed():
            self._incoming[v] = {}
        return v
    
    def insert_edges(self, u, v, x=None):
        e = self.Edge(x)
        self._outgoing[u][v] = e
        self._incoming[v][u] = e
    
    def remove_vertex(self, v):
        for edge in self.incident_edges(v, outgoing=True):
            self._incoming[edge.opposite(v)].pop(v)
        self._outgoing.pop(v)
        
        if self.is_directed():
            for edge in self.incident_edges(v, outgoing=False):
                self._outgoing[edge.opposite(v)].pop(v)
            self._incoming.pop(v)       
        
    def remove_edge(self, e):
        u, v = e.endpoints()
        self._outgoing[u].pop(v)
        self._incoming[v].pop(u)
```

## 3. Graph Traversals

Problems for undirected graph G:
    
- Computing a path from u to v or report no such path exists.

- Give na vertex s, for every vertex v of G, a path with the minimum number of edges bewteen s and v, or reporting that no such path exists.

- Testing whether G is connected.

- Computing a spanning tree of G if G is connected.

- Computing a cycle in G, or reporting that G has no cycles.

Problems for directed graph G:

- Computing a directed path from vertex to vertex v, or reporting no such path exists. 

- Finding all the vertices of G that are reachablefrom a given vertex s.

- Determine whether G is acyclic.

- Determine whther G is strongly connected. 

### 3.1 Depth-First Search (DFS)

**Algorithm** DFS(G,u): {We assume u has already been marked as visited}

   **Input:** A graph G and a vertex u of G
    
   **Output:** A collection of vertices reachable from u, with their discovery edges
    
   **for** each outgoing edge e = (u,v) of u **do**
        
   - **if** vertex v has not been visited **then**
       
       - Mark vertex v as visited (via edge e).
           
       - Recursively call DFS(G,v).

#### Classifying Graph Edges with DFS:

  
- **discovery edge (tree edge):** an edge is used to discover a new vertex v during the DFS algorithm  

- **nontree edge:** an edge that is not a tree edge during the excution of DFS

For undirected graph:

   - **back edge:** nontree edge which connect a vertex to ana ancestor in the DFS tree
   
For directed graph:

   - **back edge:** nontree edge which connect a vertex to ana ancestor in the DFS tree
   
   - **forward edge:** nontree edge which connect a vertex to a descendant in the DFS tree
   
   - **cross edge:** nontree edge which connect a vertex that is neither its ancestor nor its descendant

#### Properties of a DFS:

Propositions:

- DFS traversal visits all vertices in the connected component of starting vertex s, and the discovery edges form a spanning tree of the connected component of s.

- Let G be a directed graph. DFS on G starting starting at a vertex s visits all vertices of G that are reachable from s. Also, the DFS tree contains directed paths from s to every vertex reachable from s. 

#### Running Time of DFS:

If G is directed, O(n+m) for: 

- DFS traversal

- Computing a path bewtween two given vertices of G if one exists. 

- Computing a soanning tree of G if G is connected.

- Computing the connected components of G.

- Computing a cycle in G, or reporting that there is no cycles.

If G is undirected, O(n+m) for:

- DFS traversal

- Computing a directed path between two given vertices of G, if one exists.

- Computing the set of vertices of G that are reachable from a given vertex s. 

- Testing whether G is strongly connected.

- Computing a directed cycle in G or reporting G is acyclic.

- Computing the **transitive closure** of G.

### 3.2 DFS Implementation and Extensions


```python
def DFS(g,u,discovered):
    for e in g.incident_edges(u):
        v = e.opposite(u)
        if v not in discovered:
            discovered[v] = e
            DFS(g,v,discovered)
```

The caller should start as follows:


```python
result = {u : None} # u trivally discovered
DFS(g, u, result)
```

### Reconstructing a Path from u to v


```python
def constrcuct_path(u,v,discovered):
    path = []
    if v in discovered:
        path.append(v)
        walk = v
        while walk is not u:
            e = discovered[walk]
            parent = e.opposite(v)
            path.append(parent)
            walk = parent
        path.reverse()
    return path
```

### Testing for connectivity

- **connected:** check for an arbitrary vertex if len(discovered) = n.

- **strongly connected:** for an arbitrary vertex s, do DFS traversal and loops through all incoming edges and all outgoing edges. If for these two traversals every vertex in the graph can reach s and is reachable from s, then G is strongly connected. This method runs in O(n+m) time. 

### Computing all connected components

When a graph is not connected, the next goal we may have is to identify all of the **connected components** of an undirected graph, or the **strongly connected components** of a directed graph.


```python
def DFS_complete(g):
    forest = {}
    for u in g.vertices():
        if u not in forest:
            forest[u] = None
            DFS(g, u, forest)
    return forest
```

This function runs in O(n+m) time

### Detecting cycles wih DFS

## 3.3 Breadth-First Search (BFS)

BFS proceeds in rounds and subdivides the vertices into **levels**. 


```python
def BFS(g, s, discovered):
    level = [s]
    while len(level) > 0:
        next_level = []
        for u in level:
            for e in g.incident_edges(u):
                v = e.opposite(u)
                if v not in discovered:
                    discovered[v] = e
                    next_level.append(v)
        level = next_level
```

For BFS on an undirected graph, all nontree edges are cross edges, and for BFS on a directed graph, all nontree edges are either back edges or cross edges.

### Properties of BFS

- A path in a BFS tree rooted at vertex s to any other vertex v is guaranteed to be the shortest path.

- The traversal visits all vertices of G that are reachable from s.

- For each vertex v at level i, the path of the BFS tree T between s and v has i edges, and any other path of G from s to v has at least i edges. (same as shortest path property).

- If (u,v) is an edge that is not in the BFS tree, then the level number of v can be at most 1 greater than the level number of u.

- BFS takes O(n+m) time.

### DFS vs. BFS

BFS guarantees that those paths use as few edges as possible; DFS is suited for certain tasks such as finding a directed cycle in the graph or in identifying the strongly connected components. 

# 4. Transitive Closure

The **transitive closure** of a directed graph G is a directed graph G*, such that the vertices of G* are the same vertices of G, and whenever G has a path from u to v, G* has an edge (u,v).

**Proposition:** For i=1,2,...,n, directed graph $G_k$ has an edge $(v_i, v_j)$ if and only if directed graph $G$ has a directed path from $v_i$ to $v_j$, whose intermediate vertices (if any) are in the set $\{v_1, ..., v_k\}$

### Floyd-Warshall Algorithm

An algorithm that computes transitive closure of a graph in $O(n^3)$ time. Well suited in an adjacency matrix. 


```python
def floyd_warshall(g):
    
    closure = deepcopy(g)
    verts =list(closure.vertices())
    n = len(verts)
    for k in range(n):
        for i in range(n):
            if i!=k and closure.get_edge(verts[i], verts[k]) is not None:
                for j in range(n):
                    if i!=j!=k and closure.get_edge(verts[k], verts[j]) is not None:
                        if closure.get_edge(vers[i], verts[j]) is not None:
                            closure.insert_edges(verts[i], verts[j])
    return closure
```

# 5. Directed Acyclic Graphs (DAG)

## 5.1 Topological Ordering

**topologival ordering** is an ordering such that any directed path in G traverses vertices in increasing order. A directed graph may have more than one topological ordering. 

**Proposition**: G has a topological ordering if and only if it is acyclic.

The algorithm for computing a topological ordering of a directed graph which we call **topological sorting**. 


```python
def topological_sort(g):
    
    topo = []
    ready = []
    incount = {}
    for u in g.vertices():
        incount[u] = g.degree(u, False)
        if incount[u] == 0: # if u has no incoming edges
            ready.append(u)
    while len(ready)>0:
        u = ready.pop()
        topo.append(u)
        for e in g.incident_edges(u):
            v = e.opposite(u)
            incount[v] -= 1
            if incount[v] == 0:
                ready.append(v)
    return topo
```

it runs in O(n+m) time and using O(n) auxiliary space. 

# 6. Shortest Paths

(to be continue ...)