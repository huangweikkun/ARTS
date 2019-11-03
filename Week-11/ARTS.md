# Algorithm

## LeetCode 83. Remove Duplicates from Sorted List

Given a binary tree, invert the binary tree;

解析：移除一个排序单链表中的重复元素，根据这是排序的特点，可以得出相同的元素是相邻的，我们只需要取第一个就可以了，所以遍历的时候如果遇到相同的节点就跳过，遇到不同的节点就把节点添加到链表中，实现代码如下：

```java

/**
* @author jacken
* @date 2019/10/18
*/
public class DeleteDuplicates {

  public ListNode deleteDuplicates(ListNode head) {
    ListNode currentNode = head;
    while (currentNode != null && currentNode.next != null) {
      if (currentNode.val == currentNode.next.val) {
        currentNode.next = currentNode.next.next;
      } else {
        currentNode = currentNode.next;
      }
    }

    return head;
  }
}
  
```

# Review  
  
  ## item17 Minimize mutability 最小化可变性
  一个对象保持实例变量的不可变性，能够简化我们的编程的难度和减少在多线程中出问题的概率，遵从以下几点保证类的不可变性
  
  1. 不要提供方法改变对象的状态
  2. 确保类是不可以被继承的
  3. 让所有的变量是final的
  4. 让所有的变量是private的，客户端不可直接访问
  5. 确保客户端无法拿到一个可变引用组件的引用，让客户端拿到的是拷贝对象或者是只读对象，不能修改引用对象的状态。

# Tips

 ### docker相关概念
 
 1. image: 是一个包含docker分层信息的一个模板文件，相当于面向对象中的类
 2. container: 由image启动的一个进程应用

 ### docker基础使用命令
 1. docker command --help 查看容器命令的使用手册
 2. docker pull ${containerName}拉取对应的镜像
 3. docker image ls 查看相关镜像的信息
 4. docker run -d ${containerId} ${command} 在后台启动容器在容器内执行对应的指令
 5. docker stop 停止容器
 6. docker ps 查看正在执行中的容器
 7. docker exec -it ${containerId} /bin/bash 连接到某个容器的内部
 
  
  
  
# Share
  
  ## 架构设计的目的
    
  架构设计是为了解决软件系统复杂度带来的问题
  
  ## 架构设计复杂度来源
  
  ### 高性能：在业务快速拓展的时候，如何能够以最小代价的方式去提高整体系统的性能
  
  ### 高可用：系统不间断执行的能力
  
  ### 可扩展性：在业务的发展过程中，如何能够让系统不用修改或者是少量修改就可以满足业务的需求。
  
  ### 安全性：功能安全，架构安全
  
  ### 低成本：如何设计能够让整个架构的成本降下来
  
  ### 规模：系统的规模不断增大，系统的复杂度在上升
  
  
  
   
  
  
  
