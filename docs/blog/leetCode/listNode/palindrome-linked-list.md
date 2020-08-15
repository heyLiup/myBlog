### 234.回文链表

解法一：转化成数组后判断是否是回文数组

解法二：将链表反转，依次比较每个值是否一致
```js

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var isPalindrome = function(head) {
    let list = head;
    if (!head || !head.next) return true 
    let pre = null;
    
    let newList = new ListNode();

    //paster 会在下面的循环中时刻变动，为临时变量
    let paster = newList;
    while (list) {
        //得到链表的复制 newList
        paster = paster.next = new ListNode(list.val);

        //得到链表的反转 pre
        let temp = list.next;
        list.next = pre;
        pre = list;
        list = temp;    
    }

    //对比正反链表是否一致
    while (pre.next) {
        if (pre.val !== newList.next.val) {
            return false 
        }
        pre = pre.next;
        newList = newList.next;
    }
    return true;
};

```