
### 21.合并两个有序链表

解法1：转化为数组合并后在转回链表
```js

//链表转化为数组
function transListToArray (list) {
    let arr = [];
    while (list) {
        arr.push(list.val);
        list = list.next;
    }
    return arr;
}

//数组转为链表
function transArrayToList (array) {
    let dummy = new ListNode();
    let pre = dummy;
    for (let i = 0; i < array.length; i++) {
        pre = pre.next = new ListNode(array[i])
    }
    return dummy.next;
}

//快速排序
function quickSort (arr) {
    let temp = arr[0];
    let pre = [];
    let next = [];
    
    if (arr.length <= 1) return arr;
    
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > temp) {
            next.push(arr[i])
        } else if (arr[i] <= temp) {
            pre.push(arr[i])
        }
    }
    return quickSort(pre).concat([temp], quickSort(next));
    
}
var mergeTwoLists = function(l1, l2) {
    let arr1 = transListToArray(l1);
    let arr2 = transListToArray(l2);
    let arr = quickSort(arr1.concat(arr2));
    console.log(arr);
    return transArrayToList(arr)
};


```

解法2：新建链表，依次比较两个有序链表的值，插入到新建的链表后

```js

var mergeTwoLists = function(l1, l2) {
    let pre = new ListNode();
    let node = pre;

    if (!l1 || !l2) return l1 || l2
        
    while (l1) {       
        if (l1.val > l2.val) {
            node = node.next = new ListNode(l2.val)
            l2 = l2.next;
        } else {
            node = node.next = new ListNode(l1.val)
            l1 = l1.next;
        }
        
        if (!l2 || !l1) {           
            node.next = l1 || l2;
            break;
        }
    }    
    return pre.next;
};

```

解法3：利用递归

```js

var mergeTwoLists = function(l1, l2) {
    if (!l1 || !l2) return l1 || l2;
    if (l1.val < l2.val) {

        //假设l1为[3], l2为[5]， 
        //mergeTwoLists参数为(null, [5])，mergeTwoLists执行返回 l2
        //所以l1.next 等于 l2，然后直接return即可，反之一样
        l1.next = mergeTwoLists(l1.next, l2);    
        return l1;
    } else {
        l2.next = mergeTwoLists(l1, l2.next);    
        return l2;
    }
};


```
