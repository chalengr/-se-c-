```c
#include <stdio.h>  // 引入标准输入输出库
#include <stdlib.h> // 引入标准库，用于常用的系统函数

#define MAXN 20  // 定义常量MAXN为20，表示棋盘的最大大小

int count = 0;  // 定义一个全局变量count，用于统计解的数量
int position[MAXN];  // 定义一个数组position，用于存储每一行皇后的列位置

// 检查在(row, col)位置放置皇后是否会导致攻击
int is_valid(int row, int col) {
    for (int i = 0; i < row; i++) {  // 遍历之前的所有行
        if (position[i] == col || abs(position[i] - col) == row - i) {
            return 0;  // 如果在同一列或对角线上发现另一个皇后，则不合法
        }
    }
    return 1;  // 如果没有冲突，返回合法
}

// 递归函数，用于在棋盘上放置皇后
void solve(int row, int n) {
    if (row == n) {  // 如果已经成功放置了n个皇后
        count++;  // 增加解的计数
        return;  // 返回上一层递归
    }
    for (int col = 0; col < n; col++) {  // 尝试在当前行的每一列放置皇后
        if (is_valid(row, col)) {  // 检查放置是否合法
            position[row] = col;  // 记录当前行皇后的位置
            solve(row + 1, n);  // 递归处理下一行
        }
    }
}

// 程序的主入口点
int main() {
    int n;  // 定义一个变量n，用于存储棋盘大小
    scanf("%d", &n);  // 从用户输入读取棋盘大小
    if (n == 2 || n == 3) {  // 如果棋盘大小为2或3
        printf("无解\n");  // 输出无解，因为2x2和3x3棋盘无法安排皇后互不攻击
        return 0;  // 结束程序
    }
    solve(0, n);  // 从第0行开始求解N皇后问题
    printf("%d\n", count);  // 打印出找到的解的数量
    return 0;  // 程序正常结束
}
```

![image-20231218160431618](C:\Users\xwh1544123230\AppData\Roaming\Typora\typora-user-images\image-20231218160431618.png)

