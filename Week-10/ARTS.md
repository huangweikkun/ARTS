# Algorithm

## LeetCode 226. Invert Binary Tree

Given a binary tree, invert the binary tree;

解析：这是一个二叉树，需要对于二叉树进行倒置。

```java

  /**
   * @author jacken
   * @date 2019/10/04
   */
  public class InvertBinaryTree {
  
    public TreeNode invertTree(TreeNode root) {
      if (root == null) {
        return null;
      }
  
      invertTree(root.left);
      invertTree(root.right);
  
      TreeNode temp = root.left;
      root.left = root.right;
      root.right = temp;
  
      return root;
    }
  
  }
  
```

# Review  
  
 ### Effective Java Item 15
   最小化类和属性的可访问性
   1. private：本类中可以访问
   2. package-private：同名包中的类可以进行访问
   3. protected：继承的类和同名包中的类可以访问
   4. public：所有的类都可以进行访问  
   
   
 ### Effective Java Item 16
   
   对外的类中使用访问方法而不是直接对外暴露相应的属性，因为在提供访问方法的时可以控制外部客户端代码对于属性的修改，而直接使用对外暴露属性则无法对此进行控制，如多线程对同一个变量的操作。
 
 

# Tips

 1. git跳过暂存直接提交命令：git commit -a 
 2. git删除误添加的不需要进行追踪的文件：git rm --cached README
 3. git显示最近提交的差异：git log -p 2显示最近两次提交的差异
  
  
  
# Share
  
  
  
  
  
  
