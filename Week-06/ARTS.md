# Algorithm(LeetCode 53：Maximum Subarray)
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

解析：从一个数组中解析出其中相加最大的一个子数组，暴力的方法是把数组中所有的组合都算出来，然后取其中最大的一个便可，这种方法的时间复杂度为O(n^2)，然而有一种方法可以让我们在O(n)的时间复杂度内得到和最大的一个子数组，遍历我们的数组，然后把当前最大的和加上
当前的遍历元素，看是否当前累加的和比当前遍历的元素大，是的话当前的最大和为累加和，否则的话就为当前的遍历元素。

  ```java

  /**
   * @author jacken
   * @date 2019/08/20
   */
  public class MaximumSubarray {
    
    public static int maxSubArray(int[] nums) {
        int maxSoFar = nums[0], maxEndingHere = nums[0];
        for (int i = 1; i < nums.length; ++i) {
          maxEndingHere = Math.max(maxEndingHere + nums[i], nums[i]);
          maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
      }
  }

  ```

# Review  
  Effective Java Item 8
  避免使用finalizers和cleaners，理由如下：
  1. 无法保证finalizer和cleaner是一定会被执行，而且也不知道何时会被执行，对于一些或许有时序性要求的程序来说显然是会有问题的。
  2. 执行期间一个未被捕获的异常会被忽略
  3. 会有严重的性能问题
  4. 会有一系列安全性问题
  
  
  Effective Java Item 9
  使用try-with-resources而不是try-finally,因为使用try-finally有可能在try块和finally同时报错而finally会有异常堆栈打出来，而try中的异常没有信息，将无法进行追踪而我们更多的是希望看到try中的异常。而使用try-with-resource
  模块将可以看到第一个调用异常，而接下来的异常将会被压制，可以通过Throwable的getSuppressed方法拿到被压制的异常。try-with-resource块中的对象资源需要实现AutoCloseable接口
 

# Tips
  
  这周学习的到的技巧是sonar扫描覆盖率的时候可以在设置中排除掉一些包，被排除的包不需要被扫描计算对应的单元测试覆盖率，我们可以把项目中的POJO类对应的包给排除掉，因为POJO类不存在逻辑，但是GET/SET方法会计算测试覆盖率，导致单元测试覆盖率不是那么准确，
  而又没有必要专门为POJO增加对应的单元测试。
  
# Share
  最近在通过极客时间专栏学习Tomcat源码，从中总结了一些学习源码的方法：
  1. 学习源码之前要弄清楚该框架有哪些功能，怎么进行使用。
  2. 学习使用了框架的功能后要再去学习框架的整体架构，对于框架的组件架构有一定的认识。
  3. 然后才是开始学习源码，学习源码时要结合框架的整体的架构从架构的上层到底层逻辑一步步深入学习，首先先去分析出整体框架构的重点类，抓住其中的重点类逻辑进行学习，不要陷入一些细枝末节中，本末倒置，把重点逻辑弄清楚后基本就对于整体源码有了一个基本的认识，
  再去看那些细枝末节就能很轻松的进行学习。
  
  
