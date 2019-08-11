# Algorithm(LeetCode 15：Three Sum)
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

解析：这道题是two sum的升级，需要找出数组中三个相加唯一等于0的所有唯一组合，唯一组合我们怎么能找到呢，就是当一个数作为第一个数已经去做过组合之后，只有有其他的数和这个数相等去做组合的话则不需要
在去做多一次组合了。而且三数之和我们需要去转换成两数之和，然后在剩下的数字中找出能组合成两数之和的唯一组合跟第一个数做组合就是三数之和的唯一组合。

```java

package com.jacken.practice.leetcode;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
 * @author jacken
 * @date 2019/08/04
 */
public class ThreeSum {

  public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);

    List<List<Integer>> resultList = new ArrayList<>();
    for (int i = 0; i < nums.length - 2; i++) {
      int complement = 0 - nums[i];
      int low = i + 1;
      int high = nums.length - 1;
      while (low < high) {
        if (nums[low] + nums[high] == complement) {
          resultList.add(Arrays.asList(nums[i], nums[low], nums[high]));
          while (low < high && nums[low] == nums[low + 1]) {
            low ++;
          }
          while (low < high && nums[high] == nums[high - 1]) {
            high --;
          }
          low ++;
          high --;
        } else if (nums[low] + nums[high] < complement) {
          low ++;
        } else {
          high --;
        }
      }

      while (i < nums.length - 2 && nums[i] == nums[i + 1]) {
        i ++;
      }
    }

    return resultList;
  }

}

```

# Review  
  Effective Java Item 4
  使用一个私有的构造函数来强制不可实例化，在我们一些帮助类里面都是static方法，客户端可以直接通过类来调用这些静态函数。这些帮助类并不需要实例化，但是有些意外情况可能会导致这些帮助类
  实例化，但是这些类实例化出来并没有作用，反而是占用了一定的空间，所以为了让帮助类不可以在实例化，需要在将类的构造方法设置为private。并且可以在构造方法里面抛出异常，来防止内部实例化类。示例如下：
  
  ```java
  
  public class UtilityClass {
    private UtilityClass() {
      throw new AssertionError();
    }
  }
  
  ```
  
  Effective Java Item 5
  
  当依赖于一个底层资源，并且这个底层资源会变化，并且会影响到类对象的行为时，不要使用静态工具类或者是单例类，而是使用依赖注入的方式创建类实例对象，来保证灵活，复用这个类对象。
  
  ```java
  
  public class SpellChecker {
    private final Lexicon dictionary;
    
    public SpellChecker(Lexicon dictionary) {
      this. dictionary = Objects.requireNonNull(dictionary);
    }
  }
  
  ```
 

# Tips
  
  这周分享在工作中使用的idea重构技巧：
  1. 抽取方法，之前需要将一段逻辑封装成一个方法都是将方法剪切出来，然后写一个新方法去将代码复制到新的方法中，这样子就需要改动到在原有方法的代码逻辑，需要加一个方法调用和接收参数，之前都是手工
  做这些操作，最近使用idea的快捷抽取方法，选中代码，右键选择Refactor，然后选择Extract选择方法，然后修改方法签名和方法名，直接就能生成这些代码，而不用再自己去重新写一遍，省时省力。
  2. 之前修改类中某个变量名时都是直接使用替换快捷键替换掉对应的变量名，但是这个方法在你有变量同名的时候就会有问题，通过直接对一个变量选定，然后右键选择Refactor,然后选择Rename就可以直接对这个变量的所有引用都修改掉。

  
# Share
  [努力就会成功](https://coolshell.cn/articles/19271.html)
  
  这周分享来自CoolShell的文章，文章中讲到实际工作中某个团队通过996去赶项目，最终做出来的项目却因为项目质量不过关导致项目重做，最终项目的完成日期还比之前预估的慢了，而且项目也由此失败了。由此引发出一个疑问，努力就会成功吗？
  答案显然不是，努力的方向很重要，如果我们只是在劳动密集型的事情上一直努力，我们并不能有所收获。在工作我们要努力去提升自己的能力，从而让工作能够更好更快的被完成，而不是通过堆时间去重复一堆没有技术含量的
  工作，这样子我们的努力才是有收获的，才是能提升自己的能力的，
  在工作中拼的不是谁更努力，拼的是谁解决问题的能力更强。
  
  这篇文章对我的触动很大，因为自己最近入职一家新公司，导致最近经常加班，自己总结了一下最近加班的原因是因为不熟悉相关的新的技术栈和工具，还有公司一些流程，所以自己接下来需要做的改进是
  1. 在空闲时间去熟悉公司使用的相关技术栈和工具
  2. 总结工作中的一些流程，看是否能够将某些流程不再通过手工去完成，而是自动化完成
  
  
