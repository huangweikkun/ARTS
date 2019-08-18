# Algorithm(LeetCode 617：Merge Two Binary Trees)
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

解析： 这是合并两个棵树的题目，合并后的新树是两个树同一节点的合，所以根据题目特点，可以使用递归算法进行合并，当当前节点两树的节点都不为空时，则当前节点等于两树节点相加，当前节点的左节点等于当前两树的左节点相加，右节点当前两树节点的
右子树节点相加，两个合并节点有一个为空时则直接返回不为空的节点，两个为空时则返回任意一个都可以。

  ```java

  /**
   * @author jacken
   * @date 2019/08/13
   */
  public class MergeTwoBinaryTrees {
  
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
      if (t2 == null) {
        return t1;
      } else if (t1 == null) {
        return t2;
      }
  
      TreeNode treeNode = new TreeNode(t1.getVal() + t2.getVal());
      treeNode.setLeft(mergeTrees(t1.getLeft(), t2.getLeft()));
      treeNode.setRight(mergeTrees(t1.getRight(), t2.getRight()));
  
      return treeNode;
    }
  
  }

  ```

# Review  
  Effective Java Item 6
  防止创建不必要的对象，包括一些不可变对象，不需要多次创建例如字符串，同时也需要防止无意的装箱，例子如下：
  
  ```java
  
  String s = new String("abc");

  Long sum = 0L；
  for(long i = 0; i <= Integer.Max_VALUE; i++) {
    sum += i;
  }

  ```
  
  Effective Java Item 7
  消除过时的对象引用，防止内存泄漏，当类对象管理自己内部的容器时，有可能导致内存泄漏，所以要及时清除不再用的对象引用，
  帮助垃圾回器回收废弃对象
  
  ```java
  
  public class Stack {
    private Object[] elements;
    
    public Object pop() {
      if (size == 0) {
        return null;
      }
      
      object result = elements[--size];
      elements[size] = null;
      return result;
    }
  }
  
  ```
 

# Tips
  
  这周学习到的是单元测试的小技巧，单元测试中如何模拟一个构造函数，需要注意点：
  @PrepareForTest(TestClass.class) 需要加上使用构造函数的所在的类
 
  
  实例如下：
  ```java
  
  /**
   * @author jacken
   * @date 2019/08/15
   */
  @RunWith(PowerMockRunner.class)
  @PrepareForTest(TestClass.class)
  public class MockConstructorDemo {
  
    @InjectMocks
    private TestClass testClass;
  
    @Test
    public void test() throws Exception {
      Instance instance = PowerMockito.mock(Instance.class);
      PowerMockito.whenNew(Instance.class).withAnyArguments()
          .thenReturn(instance);
      PowerMockito.when(instance.getName()).thenReturn("mockInstance");
      testClass.newInstance();
    }
  
  }
  
  class TestClass {
  
    public void newInstance() {
      Instance instance = new Instance("testClass");
      System.out.println(instance.getName());
    }
  
  }
  
  class Instance {
  
    private String name;
  
    public Instance(String name) {
      this.name = name;
    }
  
    public String getName() {
      return name;
    }
  
  }

  ```

  
# Share
  [技术人员如何通过了解业务获取晋升机会](https://mp.weixin.qq.com/s/o4CfgIcPibG_QxrsZ4x7sA)
  技术对业务的影响层次：
  1. 按时交付
  2. 通过技术手段优化产品的性能和体验，或者是研发的交付质量，帮助更好更快的产出业务。
  3. 通过技术去驱动业务，通过技术来解决业务的痛点问题。
  
  如何深入理解业务：
  1. 通过阅读相关的行业书籍和行业的分析报告
  2. 和运营沟通
  3. 实地走访，与用户沟通
  4. 分析行业中的数据
  
  通过了解所在做的业务，能够帮助我们提升我们对于产品的理解，在产品的开发中更好的去开发出适应和符合业务特点的产品，能让业务利用产品更好更快的实现业务增长。
  
  
