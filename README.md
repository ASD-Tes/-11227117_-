##### 甲班11227117_吳彥霖
# CH1 
### 遞迴-Recursion
- 將大問題分解成更小的相同問題，分而擊之。
- 迭代的替代方案
 ### 遞迴的組成
  - **終止情況 (Base case)** : 問題簡化到最基本的形式，停止遞迴函數呼叫直接傳回一個結果。
  - **遞迴情況 (Recursive case)** : 函數內部再次呼叫自身，以解決一個相同但較小或簡化的問題。
 ### 構建遞迴的問題與步驟
1. 如何用同類型但較小的問題來定義該問題？
   - **遞迴定義** - 找到問題可以拆解的部分。 
3. 每次遞迴呼叫要如何簡化問題？
   - **問題簡化** - 每次遞迴呼叫都將原問題簡化成較小的問題。
5. 什麼問題的實例可以作為基本案例？
   - **終止條件** - 問題最簡的基本情況。
7. 隨著問題簡化，是否會達到基本狀況？
   - **保證終止** - 確認一定會到達基本條件。

# 遞迴函式
- Factorial - 階乘 
- GCD - 最大公因數
- Search in Array - 搜尋
- Fibonacci series - 費氏數列
- Combinatorial numbers - 組合數
- Tower of Hanoi - 河内塔
- Fractal - 碎形
  
# 實作
## Factorial
```cpp=
int factorial(int n) {
  // base case ：如果n為0，回傳值為1
  if (n == 0) {
    return 1;
  }
  // recursive case ：n的階乘等於n乘以(n-1)的階乘
  else {
    return n * factorial(n - 1);
  }
} // end Factorial
```
## GCD
較多判斷，較慢
```cpp=
int gcd1(int x, int y) {
  // base case ：如果y為0，回傳值為x
  if (y == 0) {
    return x;
  }
  // recursive case ：x > y，gcd1(x ,y) = gcd1(y ,x % y)
  else if (y > x) {
    return gcd1(x, y % x);
  } else {
    return gcd1(y, x % y);
  }
} // end gcd1
```
較少判斷，較快
```cpp=
int gcd2(int x, int y) {
  // base case ：如果x % y為0，回傳值為y
  if (x % y == 0) {
    return y;
  }
  // recursive case ：gcd2(x ,y) = gcd2(y ,x % y)
  else {
    return gcd2(y, x % y);
  } 
} // end gcd2
```
## Binary search
1. 初始化邊界：分左半和右半
2. 計算中間位置
3. 比較中間元素與目標值
```cpp=
int binarySearch(int Array[], int first, int last, int value) {
  // base case ：first > last，回傳-1表示目標值不在陣列中
  int index;
  if (first > last) {
    index = -1;
  // recursive case ：計算中間位置，比較中間元素與目標值value
  } else {
    int mid = (first + last) / 2;
    if (value == Array[mid])
      index = mid;
    else if
      index = binarySearch(Array, first, mid-1, value);
    else
       index = binarySearch(Array, mid-1, last, value);
  }
  return index;
} // end binarySearch
```
### 

