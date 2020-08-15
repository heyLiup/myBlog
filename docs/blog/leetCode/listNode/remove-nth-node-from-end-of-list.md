
### 19.删除链表的倒数第N个节点

```text

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？

[链接]：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list

```

解法一

通过第一次循环算出链表总长度  
计算出下一次需要循环的次数  
再次循环找到目标节点


```js
var removeNthFromEnd = function(head, n) {
    var dummy = new ListNode();
    dummy.next = head;
    
    let length = 0;
    let first = head;
    while (first) {
        length++;
        first = first.next;
    }
    
    length -= n;
    
    let second = dummy;
    while (length > 0) {
        length--;
        second = second.next
    }
    second.next = second.next.next;
    return dummy.next;
};


```



解法二

先构造两个链表对象listA，listB。listA用于遍历所有节点，listB用于计算出 期望删除节点的前一个

```js

var removeNthFromEnd = function(head, n) {
    var dummy = new ListNode();
    dummy.next = head;
    
    let listA = dummy;
    let listB = dummy;
    let count = 0;
    
    while (listA) {

        //同时出发，让listA先走，等到listA和listB相距n时，listA和listB一起往后走，
        //listA停时，listB指向的就是目标节点
        if (n < count) {
            listB = listB.next;
        } 
        count++
        listA = listA.next;
    }
    
    listB.next = listB.next.next;
    return dummy.next;
    
};

```