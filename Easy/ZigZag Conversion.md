## 题目

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## 分析

- `nRows=3`

```
1   5   9
2 4 6 8 10
3   7   11
```

- `nRow=4`

```
1     7        13
2   6 8     12 14
3 5   9  11    15
4     10       16
```

假设某列的每个位置都有数据的话，称呼该列为满列。以由上可看出满列的最小间隔为`2(nRows-1)`。则第i行（除首位两行）的每两个数之间的间隔以`2(nRows-1)-2i`、`2i`交替出现。

## 程序

```javascript
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    if(numRows===1) {
            return s;
        }
    let gapMax = 2*(numRows-1) // 两个满列列之间最小的距离
    let result = '' // 最终结果
    for(let i=0; i<numRows; i++) {
        let index = i // s的下标
        let arr = []; // 每行的数据都以数组来存储
        let flag = 0 // 数组arr的下标
        if(i===0 || i===numRows-1) {
            while(s.charAt(index) !== ''){
                arr.push(s.charAt(index))
                index += gapMax
            }
        }
        // 如果不是第一行或最后一行，则奇数列和偶数列的值诉算法不同
        while(s.charAt(index) !== '') {
            if(flag%2 === 0) {
                // 如果是偶数列
                arr.push(s.charAt(index))
                index += (gapMax-2*i)
                flag++
            } else {
                // 奇数列
                arr.push(s.charAt(index))
                index += (2*i)
                flag++
            }
        }
        result += arr.join("")
    }
    return result;
};


```

