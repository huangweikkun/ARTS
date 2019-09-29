# Algorithm

## LeetCode 104. Maximum Depth of Binary Tree

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.


解析：求解一个二叉树的最大深度，此题可通过递归思路进行解题，递归条件为：一个节点的深度等于左右子节点的较大深度加1，停止条件为：一个节点为叶子节点时深度为1；

  ```java
  
  /**
   * @author jacken
   * @date 2019/09/28
   */
  public class MaximumDepthOfBinaryTree {
  
  
    public int maxDepth(TreeNode treeNode) {
  
      if (treeNode == null) {
        return 0;
      }
  
      int leftDepth = maxDepth(treeNode.left);
      int rightDepth = maxDepth(treeNode.right);
  
      return leftDepth > rightDepth ? leftDepth + 1 : rightDepth + 1;
    }
  }

  ```
  
## LeetCode 70. Climbing Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

解析：这是一个典型的递归问题，也是一个斐波那契数列，递归条件为：当前所在楼梯的的攀爬方案等于上一次攀爬两个阶梯和一个阶梯的方案数量，终止条件为：当楼梯数为1时方案数量为1，当楼梯数为2时方案数量为2。

```java

  /**
   * @author jacken
   * @date 2019/09/28
   */
  public class ClimbStairs {
  
  
    private Map<Integer, Integer> solutionMap = new HashMap<>();
  
    public int climbStairs(int n) {
      if (n == 2) {
        return 2;
      }
  
      if (n == 1) {
        return 1;
      }
  
      if (solutionMap.get(n) != null) {
        return solutionMap.get(n);
      }
  
      int solution = climbStairs(n - 1) + climbStairs(n - 2);
      solutionMap.put(n, solution);
      return solution;
    }
    
    public int climbStairs2(int n) {
      if (n == 1) {
        return 1;
      }
  
      int first = 1;
      int second = 2;
  
      for (int i = 3; i <= n; i++) {
        int third = first + second;
        first = second;
        second = third;
      }
  
      return second;
    }
  }

```

# Review  
  
  [5个软技能帮助你的程序生涯更加出色](https://medium.com/sololearn/these-five-essential-soft-skills-will-help-your-programing-career-flourish-9260c6a7e43e)
  
  1. 团队协作能力，与团队成员一起协作完成一个共同的目标，
  2. 交流能力，采用不同的方式与不同人的沟通，如何让沟通更加顺畅。
  3. 压力管理能力，在工作上和生活上难免有许多的压力，如何去处理压力，能让自己不受压力的困扰，持续的高效为团队做贡献
  4. 自学能力，软件的技能更新非常快，需要保持持续学习的能力，从而不会被时代的潮流所抛弃
  5. 分享知识和教学他人的能力，如何将自己擅长的东西教会给团队里面的人，帮助团队成员共同成长。
 
 

# Tips
  
  
  
  
# Share

  [如何写好复杂业务代码](https://mp.weixin.qq.com/s/pdjlf9I73sXDr30t-5KewA)
  
  在一些复杂的业务场景中，有一些业务流程会涉及复杂繁琐的逻辑，如何写好其中的业务代码(自上而下的结构化分解和自下而上的面向对象分析)
  1. 梳理其中的业务流程,分析问题。
  2. 按照过程进行分解，即将业务处理分治成不同的逻辑模块进行处理
  3. 采用对象模型对分解后的逻辑模块进行整合，将领域具有的能力进行封装，提高整个设计的领域表达能力
  4. 不需要一次性设计出所有的Domain的能力，在设计迭代程中将Domain能力逐步循序渐进下沉到Domain层
  
  
  
  
  
  
