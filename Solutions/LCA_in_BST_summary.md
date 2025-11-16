## Solution Summary: Lowest Common Ancestor (LCA) in a Binary Search Tree (BST)

### 1. Problem Question

The problem is to find the **Lowest Common Ancestor (LCA)** of two given nodes, `p` and `q`, in a Binary Search Tree (BST).

*   **Ancestor:** A node `A` is an ancestor of `B` if `A` is `B` itself or an ancestor of `B`'s parent.
*   **Common Ancestor:** A node `C` is a common ancestor of `p` and `q` if `C` is an ancestor of both `p` and `q`.
*   **Lowest Common Ancestor (LCA):** Among all common ancestors of `p` and `q`, the LCA is the one that is deepest in the tree (farthest from the root).

### 2. Intuition

The key to efficiently finding the LCA in a BST lies in its defining property:

*   All values in a node's left subtree are less than the node's value.
*   All values in a node's right subtree are greater than the node's value.

This property allows us to determine the relative positions of `p` and `q` with respect to any current node we are examining, starting from the root.

**The core idea is an iterative traversal:**

1.  **Start at the root.**
2.  **Compare `p` and `q` with the `current` node's value:**
    *   **Case 1: Both `p` and `q` are smaller than `current`:** This means both nodes must be in the `current` node's **left subtree**. Therefore, the LCA must also be in the left subtree. We move `current` to its left child.
    *   **Case 2: Both `p` and `q` are larger than `current`:** This means both nodes must be in the `current` node's **right subtree**. Therefore, the LCA must also be in the right subtree. We move `current` to its right child.
    *   **Case 3: `p` and `q` are on opposite sides of `current` (one smaller, one larger), or one of them is equal to `current`:** In this scenario, `current` must be the LCA.
        *   If `p` is less than `current` and `q` is greater than `current` (or vice-versa), then `current` is the divergence point and thus the LCA.
        *   If `p` (or `q`) is equal to `current`, and the other node is in `current`'s subtree, then `current` itself is the LCA. This is because `current` is an ancestor of the other node, and it's the lowest one.

We continue this process until we find a `current` node that satisfies Case 3, which is our LCA.

### 3. Code

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

def lowestCommonAncestor(root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
    """
    Finds the lowest common ancestor (LCA) of two given nodes in a Binary Search Tree (BST).

    Args:
        root: The root of the BST.
        p: One of the nodes to find the LCA for.
        q: The other node to find the LCA for.

    Returns:
        The lowest common ancestor node.
    """
    current = root

    while current:
        # If both p and q are smaller than the current node,
        # then the LCA must be in the left subtree.
        if p.val < current.val and q.val < current.val:
            current = current.left
        # If both p and q are larger than the current node,
        # then the LCA must be in the right subtree.
        elif p.val > current.val and q.val > current.val:
            current = current.right
        # Otherwise, the current node is the LCA.
        # This happens when:
        # 1. p is on one side and q is on the other side of current.
        # 2. One of the nodes (p or q) is equal to current.
        else:
            return current
    
    # This line should ideally not be reached if p and q are guaranteed to be in the tree.
    # It's good practice for robustness in case they might not be.
    return None

```

### 4. Space and Time Complexity

*   **Time Complexity: O(h)**, where `h` is the height of the BST.
    *   In the worst case (a skewed tree, resembling a linked list), `h` can be `N` (number of nodes), leading to **O(N)**.
    *   In the best case (a balanced BST), `h` is `log N`, leading to **O(log N)**.
    *   The algorithm performs a single traversal from the root down to the LCA, doing constant work at each step.
*   **Space Complexity: O(1)**
    *   The iterative solution uses only a few pointers (`current`, `p`, `q`, `root`), requiring a constant amount of extra space, irrespective of the tree's size.

### 5. Similar Problems

*   **Lowest Common Ancestor of a Binary Tree:** This is a more general version where the tree is not necessarily a BST. The solution typically involves recursion or storing parent pointers.
*   **Search in a Binary Search Tree:** A simpler problem where you just need to find if a given value exists in the BST.
*   **Insert into a Binary Search Tree:** Adding a new node while maintaining the BST property.
*   **Delete Node in a BST:** Removing a node while maintaining the BST property, which is more complex due to handling nodes with one or two children.
*   **Validate Binary Search Tree:** Checking if a given binary tree adheres to the BST properties.
*   **Inorder Successor/Predecessor in a BST:** Finding the next smallest/largest element in the BST relative to a given node.
*   **Balanced BSTs (AVL Trees, Red-Black Trees):** These data structures are extensions of BSTs that automatically maintain balance to guarantee O(log N) time complexity for most operations, including LCA.
