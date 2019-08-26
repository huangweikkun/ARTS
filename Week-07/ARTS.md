# Algorithm(LeetCode 136：Single Number)
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

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
  
  idea Debug技巧：
  1. 断点调试时可以通过设置断点Evaluate and log来执行到达断点行需要执行的命令和记录日志。
  2. 可以设置condition来指定当到达某个条件后断点才触发。
  ![截图](./20190826-230012.png)
  3. 可以添加由某个异常而触发的断点，断点会在异常触发代码行停止。
  ![截图](./20190826-231036.png)
  4. 一行代码有好几个方法，可以通过Shift + F7键智能步入，选择需要debug进入的方法。
  5. 多线程调试时，设置断点为ALL会导致阻塞其他线程的运行，可以选择Thread阻塞级别。
  ![截图](./20190826-231801.png)
  6. 当需要回退到某一个断点执行时，可以在debug的调用栈里面右键选择需要回退的调用栈选择Drop Frame便可以回退到该断点，该断点回退只能重新走一下流程，无法回退已经修改的变量和状态。
  ![截图](./20190826-232144.png)
  
# Share
  
  
