## 1.  无重复字符的最长子串

```
/**
 * @param {string} s
 * @return {number}
 */
 var lengthOfLongestSubstring = function(s) {
    s = s.replace(/\s/g, "︹"); // 这里对空格的处理，暂时用键盘上没存在的特殊符号代替；
    const len = s.length;
    
    let value = '';

    for (let i = 0; i < len; i++) {

      let forValue = ''; // 当前循环集合到的字符串

      forValue = s[i]; // 当前提取的字符串；

      const for_Num = len - (i + 1); // 获取字符串剩余需要循环的几次
      if (len === 1) {
        value = forValue
      }
      for (let j = 0; j < for_Num; j++) {
        const for_J = len - (for_Num - j);
        const j_current = s[for_J]; // 二次循环提取的字符串；

        if (forValue.indexOf(j_current) === -1) {
          forValue += j_current;
        } else {
          if (!value || value.length < forValue.length) {
            value = forValue;
          }   
          break;
        }

      }
      
      if (value.length < forValue.length) {
        value = forValue
      }

    }
    return value.length;
};
```

## 2.最长回文子串

```
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  const len = s.length;

  if (len < 2) return s;

  // begin: 开始位置
  // maxLen: 目前截取到的字符串的长度
  let begin = 0, maxLen = 1;

  // 循环开始与结束位置
  const validateLocation = (left, right) => {
    while (left < right) {
      if (s.charAt(left) !== s.charAt(right)) {
        return false
      }
      left++;
      right--;
    }
    return true
  }

  for(let i = 0; i < len - 1; i++) {

    for (let j = i + 1; j < len; j++) {
      // j - 1 + 1 当前开始位置与结束位置，是否比目前已截取的长度 长 （减少不必要的赋值）
      if (j - i + 1 > maxLen && validateLocation(i, j)) {
        begin = i;
        maxLen = j - i + 1;
      }
    }

  }

  return s.slice(begin, begin + maxLen);
};

console.log(longestPalindrome('babad')) // bab
console.log(longestPalindrome('cbbd')) // bb
console.log(longestPalindrome('cbbddbbc')) // cbbddbbc
```

## 3.快乐数

```
/**
 * @param {number} n
 * @return {boolean}
 */
var isHappy = function(n) {
  const flag = validateNumberIsOne(n);

  return flag;
};

function validateNumberIsOne (n) {
  n = isString(n) ? n : n.toString();
  const nArr = n.split("");

  if (nArr.length === 1) {
    const data = nArr[0]
    const num = isString(data) ? Number(data) : data
    return [1, 7].includes(num)
  }

  const number = nArr.reduce((pre, cur) =>{
    cur = Number(cur)
    return pre + (cur * cur)
  }, 0)


  if ([1, 7].includes(number)) return true

  return validateNumberIsOne(number);

}

//校验是否为字符串
function isString (s) {
  return typeof s === 'string'
}
```



