
## DFS-BFS -
```cpp
DFS -
    void dfs(int i,int j,vector<vector<char>>&board,vector<vector<bool>>&vis,
    int& n,int& m){

        vis[i][j] = true; // yaha vis mark karo

        int row[4] = {0,0,1,-1}, col[4] = {1,-1,0,0};

        for(int idx=0;idx<4;idx++){  

            int r = i + row[idx], c = j + col[idx];
            if(r<0 || r>=n || c<0 || c>=m || vis[r][c] || board[r][c] != 'O')
                continue;
                
            dfs(r,c,board,vis,n,m);
        }
    }
```


```cpp
BFS -
- queue initialise karne ke lie push karo tab usko vis mark karo
- ab inside loop, whenever, push karo q me to vis mark kardo
```


---



## Cycle detection in Undirected -
1. if already vis.
2. and not parent node


---


## Cycle detection in Directed -

### DFS -
- carry an extra pathVis with standard approach.
- if any node is already vis and also pathVis

### BFS (Topo Sort) -
- if size of final topo sort vector is not equal to total nodes


---

[802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/) 
## Print cycle nodes in Directed G -

### DFS -
- bas jese hi loop milne ki condition true - dfs unfold karke return (basically exact same code of cycle detection in directed G with no change)
- pathVis array ki state hold karke rakhenge
- at the end, jo pathVis true nodes hai, vo hi cycle nodes h


### BFS -
- graph edges reverse kardo
- now apply same kahn's topo bfs
- every node jo pop karra hu, are not part of loop
- store this info in a vis bool array, end m jo bhi false hai -> vo nodes are cycle nodes

---


## Topo Sort -
- if `u->v` then topo ordeing m `u`, `v` se pehle ana chahiye

### DFS -

- vis array maintain
- Post-push: curNode p khada hoke ---> sare nodes (dfs calls) process karne k baad, curNode ko ds m push

### BFS (Kahn's algo)-
- inorder array maintain only
- if inorder 0 hai to q me push initial
- whenever i reach a node, uska inorder -1 kar dunga
- repeat 2-3


---


## DSU -
- why dsu ? -> in dynamic graphs (where the graph config constantly changes), telling if any two nodes belong to same component or not in constant time.
- without dsu, dfs or bfs will be required each time for find operation.

### Union -
```cpp
why path compression ? -> so har node ka parent pure set the most senior most parent se update kar de else recursive calls karke pochna padta hai

why rank based union ? -> so min height graph bane
what is rank ? -> parent banane ki priority

vector<int> parent;
vector<int> rank;

int find (int x) {
    if (x == parent[x]) 
        return x;

    return parent[x] = find(parent[x]); // this is path compression
}

void Union (int x, int y) {
    int x_parent = find(x);
    int y_parent = find(y);

    if (x_parent == y_parent) 
        return;
 
    if(rank[x_parent] > rank[y_parent]) {    // jyada rank wale ko papa
        parent[y_parent] = x_parent;
    } else if(rank[x_parent] < rank[y_parent]) {  
        parent[x_parent] = y_parent;
    } else {  
        parent[x_parent] = y_parent;      // if rank is same - kisi ko bhi papa
        rank[y_parent]++;                 // and papa ka rank++
    }
}


Time complexity :
both operations : O(4 alpha) ~ constant ( as alpha is close to 1)
```


---


## Dijkstra Algo -
```cpp      
        priority_queue<pi,vector<pi>,greater<pi>>pq;    //min-heap
        set<pi>st;
        
        vector<int>distance(V,INT_MAX);
        
        distance[src] = 0;
        
        pq.push({0,src});
        st.insert({0,src});
        
        while(!pq.empty()){
        
            auto it = pq.top();
            auto& it = *st.begin()
            
            pq.pop();
            st.erase(it);
            
            int curNode = it.second;
            int curDist = it.first;
            
            if(curDist > distance[curNode]) continue;
            
            for(auto& itr : adj[curNode]){
                int node = itr.first;
                int wt = itr.second;
                
                if(curDist + wt < distance[node]){
                
	                if(distance[node] != INT_MAX) 
		                st.erase({distance[node],node});
                    
                    distance[node] = curDist + wt;
                    pq.push({distance[node], node});
                }
            }
        }
```

### Keywords in problem (agar y h) -
1. source given hai
2. shortest path chahiye
3. edge wt constant ya variable (kuch bhi)

### BFS lagega agar -
1. shortest path
2. edge wt constant h

### Important -
if edge wt constant h ---- to priority queue ki need nhi h, normal queue same kaam karega