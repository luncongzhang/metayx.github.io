---
layout: post
title:  "36. 有效的数独"
categories: 算法
tags: leetcode 哈希表
---

* content
{:toc}

<!--more-->

判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

![](https://ws3.sinaimg.cn/large/006tKfTcgy1ftlbqxcqsrj306y06ydfp.jpg)

上图是一个部分填充的有效的数独。

数独部分空格内已填入了数字，空白格用 '.' 表示。

示例 1:

```
输入:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: true
```

示例 2:

```
输入:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: false
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。
     但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。
```
说明:

* 一个有效的数独（部分已被填充）不一定是可解的。
* 只需要根据以上规则，验证已经填入的数字是否有效即可。
* 给定数独序列只包含数字 1-9 和字符 '.' 。
* 给定数独永远是 9x9 形式的。

解1： 掌握核心科技,不过核心科技太难掌握。下面公式不知道哪个大神推导出来的，非常难。看解2。

```
x = (i / 3) * 3 + (k % 9) / 3;
y = j % 3 + ((k / 9) % 3) * 3;
```

```
public boolean isValidSudoku(char[][] board) {
        Set<Character> rowSet = new HashSet<>();
        Set<Character> lineSet = new HashSet<>();
        Set<Character> sudokuSet = new HashSet<>();

        int k = 0;
        int x = 0;
        int y = 0;

        for (int i = 0; i < 9; i++) {
            rowSet.clear();
            lineSet.clear();
            sudokuSet.clear();
            for (int j = 0; j < 9; j++) {
                //行
                if (board[i][j] != '.' && !rowSet.add(board[i][j])) {
                    return false;
                }

                //列
                if (board[j][i] != '.' && !lineSet.add(board[j][i])) {
                    return false;
                }

                x = (i / 3) * 3 + (k % 9) / 3;
                y = j % 3 + ((k / 9) % 3) * 3;
                //小格子
                if (board[x][y] != '.' && !sudokuSet.add(board[x][y])) {
                    return false;
                }
                k += 1;
            }
        }
        return true;
    }
```

解2：牺牲了一点时间，比较容易理解。

```
public boolean isValidSudoku(char[][] board) {
        Set<Character> rowSet = new HashSet<>();
        Set<Character> lineSet = new HashSet<>();
        Set<Character> sudokuSet = new HashSet<>();

        int m = board.length;
        int n = board[0].length;
        //行列
        for (int i = 0; i < m; i++) {
            rowSet.clear();
            lineSet.clear();
            for (int j = 0; j < n; j++) {
                //行
                if (board[i][j] != '.' && !rowSet.add(board[i][j])) {
                    return false;
                }
                //列
                if (board[j][i] != '.' && !lineSet.add(board[j][i])) {
                    return false;
                }
            }
        }
        //小格子
        for (int i = 0; i < m - 2; i = i + 3) {
            for (int j = 0; j < n - 2; j = j + 3) {
                //外面两个循环确定了小格子左上角第一个元素
                sudokuSet.clear();
                for (int a = i; a < i + 3; a++) {
                    for (int b = j; b < j + 3; b++) {
                        if (board[a][b] != '.' && !sudokuSet.add(board[a][b])) {
                            return false;
                        }
                    }

                }
            }
        }
        return true;
    }
```