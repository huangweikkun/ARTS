# Algorithm

## LeetCode 160.Intersection of Two Linked Lists 

Write a program to find the node at which the intersection of two singly linked lists begins.

解析：找到两个单链表之间的交叉节点。交叉节点同一个节点，拥有相同的引用，两个单链表之间的交叉，我们只需要遍历第一个链表，将链表中所有节点的地址保存到一个set中，然后在遍历第二个链表，找到的第一个在set中出现的地址
就是两个链表交叉的节点。

```java

/**
 * @author jacken
 * @date 2019/11/03
 */
public class IntersectionOfTwoLinkedList {

  public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    if (headA == null || headB == null) {
      return null;
    }

    Set<String> addressSet = new HashSet<>();
    while (headA != null) {
      addressSet.add(headA.toString());
      headA = headA.next;
    }

    while (headB != null) {
      if (addressSet.contains(headB.toString())) {
        return headB;
      }

      headB = headB.next;
    }

    return null;

  }
}
  
```

# Review  
  
  ## item17 Favor composition over inheritance 
    更多使用组合而非继承
    
  有以下理由：
  1. 继承有时会导致子类的覆盖方法依赖于子类的实现，使得父类方法如果有变化，子类就会出现非预期的问题。
  2. 如果父类在迭代中新增了方法，但是在子类中却没有相关的对应的覆盖实现，就会导致一系列的问题。

# Tips

  
# Share
 [什么是事务](https://www.cnblogs.com/huangweikun/p/11735564.html) 
