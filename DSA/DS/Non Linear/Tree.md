
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


- binary tree ke lie preorder, postorder jaruri h
- bst ke lie inorder jaruri h (  **+ inorder stack se kese hota h - ye bhi**)


### 1. Top Down Approach - (PreOrder)
1. solves / process current node and call child nodes ( by passing info )
2. used when you determine answer for a node using parameter before visiting it's children.
   ( **Very IMPORTANT** )
3. [513. Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value/) ( get top down intuition from this problem )
4. [112. Path Sum](https://leetcode.com/problems/path-sum/) 


### 2. Bottom Up Approach - (PostOrder)
1. solves / process child and returns answer to parent ( parent get solved result )
2. then solve parent using returned results form child
3. used when node's answer depends on children answer
4. https://www.geeksforgeeks.org/problems/remove-half-nodes/1 ( get bottom up intuition )
5. [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) ( get bottom up intuition )
6. [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) 


### Good Revision -
- [2196. Create Binary Tree From Descriptions](https://leetcode.com/problems/create-binary-tree-from-descriptions/) 
- [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)  
- [Ceil in BST](https://www.geeksforgeeks.org/problems/implementing-ceil-in-bst/1) 
- [450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - fit karde



### Must Learn CONCEPTS - (important**)
- [987. Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)     - map of maps
- [662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/)     - level order numbering
- [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)   - parent pointer
- [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) - remember to make a unique binary tree - you need inorder with either pre or post order.
- [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) - node return se khel, bool nahi



- [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - har node ki ek value domain range hoti h ( IMPORTANT BST CONCEPT ) 
- [1008. Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/) { **uper wala concept** }
- [Predecessor and Successor](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1) { bro -- simply know, pred. left ka rightmost and succ. right ka leftmost hota h ----------------- very tripppppy   brrooooo}


- [653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/) { inorder traversal stack se }
- [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/) { ^^ same }

