
### All in one Traversal -
```cpp
void allinone(TreeNode* root){
    if (!root) return; // Edge case check

    stack<pair<TreeNode*,int>> s;
    vector<int> pre;
    vector<int> in;
    vector<int> post;

    s.push({root, 1});

    while(!s.empty()){
        auto& it = s.top(); // Use reference to modify the state in the stack
        auto node = it.first;
        int status = it.second;

// for pre,   left daal
        if(status == 1){
            it.second++; // Move to state 2 for next time
            pre.emplace_back(node->val);
            if(node->left) s.push({node->left, 1});
        }
        
// for in,   right daal
        else if(status == 2){
            it.second++; // Move to state 3 for next time
            in.emplace_back(node->val);
            if(node->right) s.push({node->right, 1});
        }
        
// for post,  pop
        else{
            post.emplace_back(node->val);
            s.pop(); // Done processing, pop from stack
        }
    }
}
```



### 1. Top Down Approach - (PreOrder)
1. solves / process current node and call child nodes ( by passing info )
2. used when you determine answer for a node using parameter before visiting it's children.
   ( **Very IMPORTANT** )
3. [513. Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value/) ( get top down intuition from this problem )


### 2. Bottom Up Approach - (PostOrder)
1. solves / process child and returns answer to parent ( parent get solved result )
2. then solve parent using returned results form child
3. used when node's answer depends on children answer
4. https://www.geeksforgeeks.org/problems/remove-half-nodes/1 ( get bottom up intuition )
5. [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) ( get bottom up intuition )



### Revision -
- [2196. Create Binary Tree From Descriptions](https://leetcode.com/problems/create-binary-tree-from-descriptions/) 