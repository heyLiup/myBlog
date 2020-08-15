
### 141.环形链表

```js

//解法一，判断是否遍历过
var hasCycle = function(head) {
    let map = {};
    while (head) {
        if (head[head.val] !== undefined) {
            return true;
        } else {
            head[head.val] = true;
        }
        head = head.next
    }
    return false;
};

//解法二： 追及
var hasCycle = function(head) {
    if (!head || !head.next) return false;
    let slow = head;
    let fast = head.next;
    
    //因为下面fast.next.next，所以需判断fast.next是否存在
    while (fast && fast.next) {
    if (slow == fast) {
        return true;
    }
    slow = slow.next;
    fast = fast.next.next;
    }
    return false
}

```