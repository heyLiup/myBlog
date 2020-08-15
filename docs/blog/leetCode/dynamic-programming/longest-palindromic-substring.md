### 最长回文字符串

```html

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
示例 2：

输入: "cbbd"
输出: "bb"

链接：https://leetcode-cn.com/problems/longest-palindromic-substring

```


```js

/**
 * @param {string} 
 * @return {string}
 */
 var calc = function (str, startIndex, lastIndex) {
    if (!str[startIndex - 1] || !str[lastIndex + 1] 
        || (str[startIndex] !== str[lastIndex ])
        || (str[startIndex - 1] !== str[lastIndex + 1])) {
        if (str[startIndex] === str[lastIndex]) {

            //slice是左开右闭，在截取时右边需要加一
            return str.slice(startIndex, ++lastIndex)
        } else {
            return str[startIndex]
        }
    } else {
        return calc(str, --startIndex, ++lastIndex)
    }
}


var longestPalindrome = function(s) {
    let maxStr = s[0];
    if (s.length < 2) return s;
    for (let i = 0; i < s.length; i++) {
        let temp = calc(s, i, i);
        let tempSpace = calc(s, i, i + 1);
        maxStr = maxStr.length < temp.length ? temp : maxStr;
        maxStr = maxStr.length < tempSpace.length ? tempSpace : maxStr;
    }
    return maxStr;
}; 


```