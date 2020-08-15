### 链表基础

>链表（Linked List）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的指针（Pointer）。

```js

//链表 构造函数
function ListNode (value, next = null) {
    this.val = value;
    this.next = null;
}

//将链表转化为数组
function transListToArray (list) {
    if (!list) return false;
    let arr = [];
    while (list.next) {
        arr.push(list.val);
        list = list.next;
    }
    return arr;
}

//将数组转化为链表
function transArrayToList (arr) {
    let dummy = new ListNode();

    //pre表示前一个节点
    let pre = dummy;
    arr.forEach(element => {
        let node = new ListNode(element);
        pre.next = node;
        pre = node;
    });
    return dummy.next;
}

//复制链表
function copyList (list) {
    let dummy = new ListNode();

    //pre表示前一个节点
    let pre = dummy;

    while (list) {
        pre = pre.next = new ListNode(list.val);
        list = list.next
    }
    
    return dummy.next;
}

//将链表打印出来
function logList (list) {
    if (!list) return '';
    let res = 'list:';
    while (list.next) {
        res += list.val + '->';
        list = list.next;
    }
    res += 'end';
    console.log(res);
}

```