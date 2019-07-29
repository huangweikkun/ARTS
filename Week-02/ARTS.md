# Algorithm(LeetCode 94：Binary Tree Inorder Traversal)
Given a binary tree, return the inorder traversal of its nodes' values.

解析：这是二叉树中序遍历的题目，使用递归可以很方便快捷的解决问题，但是如果树的规模比较大，递归会有栈溢出的风险，所以我们可以使用非递归的方法去解决它。
中序遍历的规则是先遍历左节点，在遍历父节点，最后遍历右节点，解决思路就是在遍历节点的时候把树的根节点和对应的左节点入栈，直到对应的节点的左节点不存在了，
就弹出当前的节点，当前节点加入到遍历的序列中，然后把当前节点的右节点入栈，重复该过程。 以下是Java语言的解法，以下解法的使用了一个map来做遍历标记，
空间复杂度较高，应该有更少空间复杂度的解法，有待之后优化。

```java

package com.jacken.practice.leetcode;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Stack;

/**
 * @author jacken
 * @date 2019/07/28
 */
public class BinaryTreeInorderTraversal {

  public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> inorderList = new ArrayList<>();
    if (root == null) {
      return inorderList;
    }

    Map<TreeNode, Boolean> traverseFlagMap = new HashMap<>();
    Stack<TreeNode> integerStack = new Stack<>();
    integerStack.push(root);
    while (!integerStack.isEmpty()) {
      TreeNode treeNode = integerStack.pop();

      if ((traverseFlagMap.get(treeNode) != null && traverseFlagMap.get(treeNode)) || treeNode.getLeft() == null) {
        inorderList.add(treeNode.getVal());
        if (treeNode.getRight() != null) {
          integerStack.push(treeNode.getRight());
        }
      } else {
        integerStack.push(treeNode);
        if (treeNode.getLeft() != null) {
          integerStack.push(treeNode.getLeft());
        }
      }

      traverseFlagMap.put(treeNode, true);
    }

    return inorderList;
  }

}

/**
 * 二叉树节点
 */
class TreeNode {

  private int val;
  private TreeNode left;
  private TreeNode right;

  public TreeNode(int x) {
    this.val = x;
  }

  public int getVal() {
    return val;
  }

  public void setVal(int val) {
    this.val = val;
  }

  public TreeNode getLeft() {
    return left;
  }

  public void setLeft(TreeNode left) {
    this.left = left;
  }

  public TreeNode getRight() {
    return right;
  }

  public void setRight(TreeNode right) {
    this.right = right;
  }

}


```

# Review
 [“What Makes a Better Programmer” by Alicia Liu](https://medium.com/better-programming/what-makes-a-better-programmer-89093be66cf4)  
 这是一篇关于如何成为一个更好的程序员，目前网上充斥着大量如何在某些编程语言方面如何更为精进，但是编程语言会过期，
 谁都不知道过几年流行的语言又是什么了，所以作者总结了在编程领域三十年甚至五十年都不会变和需要我们去学习的技术，
 有如下几门书相关技术在经历过几十年的变迁依然在编程领域被奉为经典之作：
 
 1. 企业应用架构模式：介绍了关于企业级web应用的架构设计和相关模式。
 2. 重构：讲解了关于如何重构，什么时候进行重构，怎么做扩展性重构。
 3. 设计模式：关于面向对象设计的模式，帮助设计高内聚低耦合的软件。
 4. 人月神话：介绍了如何进行大型软件项目的管理
 5. 计算机程序设计心理学：该书籍他同样讲解如何管理项目，但是是从人的视角去看的，该书认为我们几乎不会去寻求一个最好的应用程序，甚至很少去寻求一个好的应用程序，
 而是在寻求一个符合需求的应用程序。并且认为一个程序最重要的是正确的，而不是程序运行很快但却不能处理所有的输入，即便正确的程序是更丑陋和更慢的。软件开发最初的是
 正确的结果，其次是按时交付，然后是代码健壮性，最后才是程序的效率。当然其中的顺序也要视情况而定。
   
     最后作者认为软件开发的最终目标是delivering working software that achieves its purpose（提供能满足需求的工作软件）
 

# Tip
  
  本周分享关于写单元测试的一些关注点和技巧
  
  ## 一般原则
  - 测试任何可能失败的地方
  - 测试任何已经失败的地方
  - 对于新加的代码，在被证明
  正确之前都是可能有问题的
  - 针对每次编译做局部测试
  - 签入代码之前做全局测试
  
  ## 单元测试要求
  1. 要足够小
  2. 针对一个行为一个单元测试
  
  ## 单元测试内容（Right-BICEP）
  
  ### Right
   结果是否正确
  
  ### B
  边界条件，包含以下条件：  
  
  - 不一致的输入数据
  - 格式错误的数据
  - 空值或者是不完整的值
  - 与现实情况相比不合理的值
  - 不符合要求的输入数据
  - 数据的顺序与期望不符合
  
  #### CORRECT
  
  - Conformance: 值是否与预期一致
  - Ordering：值是否是有序的
  - Range：值是否位于合理的最大最小值之间
  - Reference：代码是否引用了不在代码本身控制范围之内的资源
  - Existence：值是否存在
  - Cardinality：是否恰好有足够的值，在0，1，n的问题上
  - Time：所有事情的发生是否是有序的，是否是在正确的时刻
  
  ### I
  检查反向关联，使用结果的反向推理进行检查，如插入数据后查询数据进行检查
  
  ### C
  使用其他手段进行交叉检查，使用多个算法进行检查结果
  
  ### E
  强制产出 错误条件
  
  ### P
  性能
  
  ## 要回答的问题
  1. 我如何知道代码是否正确呢
  2. 我要如何对他进行测试
  3. 还有哪些方面可能会发生错误
  4. 这个问题是否会在其他地方出现
    
  ## 单元测试原则（A-TRIP）
  
  ### 自动化(Automatic)
  
  ### 彻底的(Thorough)
  
  ### 可重复的(Repeatable)
  
  ### 独立的(Independent)
  
  ### 专业的(Professional)
  
 #### 参考文献
 - [1] [单元测试之道](https://book.douban.com/subject/1239651/)

  
# Share
  [如何在工作中快速成长](https://mp.weixin.qq.com/s/wqb_Vwv-r6Aj-LEm_EWJXQ)
  认知升级，思维中改变反映到行动的改变
  
  1. 思考脑 VS 反射脑
  2. 习惯 VS 习以为常
  3. 时间管理：三八理论
  4. 最重要的财富：注意力
  5. 拿结果手段：执行力
  6. 贵人
  7. 会议
  8. 跳出舒适区
  9. 职业规划
  10. 时间换空间
  
