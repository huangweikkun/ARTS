# Algorithm(LeetCode 617：Merge Two Binary Trees)
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

解析：这道题是two sum的升级，需要找出数组中三个相加唯一等于0的所有唯一组合，唯一组合我们怎么能找到呢，就是当一个数作为第一个数已经去做过组合之后，只有有其他的数和这个数相等去做组合的话则不需要
在去做多一次组合了。而且三数之和我们需要去转换成两数之和，然后在剩下的数字中找出能组合成两数之和的唯一组合跟第一个数做组合就是三数之和的唯一组合。

```java


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
  
  
  
