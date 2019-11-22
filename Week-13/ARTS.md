# Algorithm

## LeetCode 543.Diameter of Binary Tree

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

解析：找到一个二叉树的最长路径，要找到一个最长路径，最长路径得经过一个节点，我们只需要遍历所有的节点，算出每个节点的左右子树的路径，从而得到这个节点的路径，然后与最长路径比较，就可以找到一个二叉树的最长路径了。

```java

/**
 * @author jacken
 * @date 2019/11/21
 */
public class DiameterOfBinaryTree {

  private int maxLength = 0;

  public int diameterOfBinaryTree(TreeNode root) {
    if (root == null) {
      return maxLength;
    }

    getSubTreeLength(root);

    return maxLength;
  }

  private int getSubTreeLength(TreeNode root)   {
    if (root == null) {
      return 0;
    }

    int leftLength = getSubTreeLength(root.left);
    int rightLength = getSubTreeLength(root.right);

    int length = leftLength + rightLength;
    if (length > maxLength) {
      maxLength = length;
    }

    return leftLength > rightLength ? leftLength + 1 : rightLength + 1;
  }

}

```

# Review  
[The Greatest Shortcut for Leaders Is Reading Books](https://forge.medium.com/the-greatest-shortcut-for-leaders-is-reading-books-d1c7e8eb4ee5)

### 成为一个领导者的捷径是读书

成为一个领导者会让你面对很多你之前没有遇见过的问题，这意味着你需要花费很大的力气去解决，但是好消息是你是第一个碰到这些问题的人，因为在这么多年的历史中，有许多碰到过该问题的人碰到过这些问题并解决了它们，然后把它们记录下来，
你可以通过阅读去学习解决这些问题的办法。


# Tips

  
# Share
 [MySQL事务](https://www.cnblogs.com/huangweikun/p/11784768.html) 
