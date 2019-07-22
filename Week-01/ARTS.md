# Algorithm(LeetCode 20)
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.

解析：这是一道关于栈相关的题目，验证输入的字符串是不是一个合法的开闭左右符号，从题目的要求中我们可以分析出，在进行字符串验证的时候，遇到左边的符号就入栈，遇到右边的符号就出栈，最后栈中的元素为空的话就是一个合法的字符串，否则就不是一个合法字符串。
下面是这道题的Java的一个解法：

```java
package com.jacken.practice.leetcode;

import java.util.HashMap;
import java.util.Map;
import java.util.Stack;

/**
 * @author jacken
 * @date 2019/07/21
 */
public class ValidParentheses {

  private static Map<Character, Character> map = new HashMap<>();

  static {
    map.put(')', '(');
    map.put('}', '{');
    map.put(']', '[');
  }

  public boolean isValid(String s) {
    if (s == null) {
      throw new IllegalArgumentException("s can not be null");
    }

    Stack<Character> stringStack = new Stack<>();
    char[] ss = s.toCharArray();
    for (char c : ss) {
      if (map.containsKey(c)) {
        Character var = stringStack.isEmpty() ? ' ' : stringStack.peek();
        if (!var.equals(map.get(c))) {
          return false;
        }

        stringStack.pop();
      } else {
        stringStack.push(c);
      }
    }

    return stringStack.isEmpty();
  }

}


```


#Review


#Tip
  
  idea中的lombok插件在使用@Builder注解后如果需要在程序中使用无参数构造函数会导致运行时报无法通过无参构造器构造对象，因为不存在对应的无参构造器，原因是@Builder注解在会在对象中加入一个全参构造器，导致无参构造器无法使用，而如果添加@NoArgsConstructor会报编译错误无法将类xxx中的构造器xxx应用到给定类型,
  解决方案是在类中添加对应的无参构造器，并且添加@Tolerate注解，让编译器不编译该方法
  ```java
  @Tolerate
  public xxx() {
  
  }
  ```
  
#Share
  分享陈皓的关于登月相关的文章：https://coolshell.cn/articles/19612.html，读完后感觉现在人写程序对于程序的健壮性似乎要求的太低了，看看登月的程序在写好后两天就上生产，精确控制执行发射去到月球，并且当时的电脑在内存中使用绕线进行编程，竟然能完成如此伟大的工程，真是让人感叹那代人的工匠精神的对于技术的一丝不苟的投入。