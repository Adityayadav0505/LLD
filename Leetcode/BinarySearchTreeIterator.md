## Binary Search Tree Iterator

Implement the `BSTIterator` class that represents an iterator over the in-order traversal of a binary search tree (BST):

- `BSTIterator(TreeNode root)` Initializes an object of the `BSTIterator` class. The root of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.
- `boolean hasNext()` Returns `true` if there exists a number in the traversal to the right of the pointer, otherwise returns `false`.
- `int next()` Moves the pointer to the right, then returns the number at the pointer.

Notice that by initializing the pointer to a non-existent smallest number, the first call to `next()` will return the smallest element in the BST.

You may assume that `next()` calls will always be valid. That is, there will be at least a next number in the in-order traversal when `next()` is called.

## Code (Java)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class BSTIterator {
    private int currIndex = 0;
    private List<Integer> val; 
    public BSTIterator(TreeNode root) {
        this.currIndex = 0;
        val = new ArrayList<>();
        inorderTraversal(root);
    }
    
    public int next() {
        return val.get(currIndex++);
    }
    
    public boolean hasNext() {
        if(currIndex > val.size()-1)
            return false;
        return true;
    }

    private void inorderTraversal(TreeNode root){
        TreeNode temp = root;
        if(temp == null)
            return;
        inorderTraversal(temp.left);
        val.add(temp.val);
        inorderTraversal(temp.right);
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```