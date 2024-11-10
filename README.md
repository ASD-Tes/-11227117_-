##### 甲班11227117_吳彥霖
# CH1 
### 遞迴-Recursion
- 將大問題分解成更小的相同問題，分而擊之。
- 迭代的替代方案
- 用box trace視覺化遞迴函數的呼叫堆疊
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


# 線性遞迴跟二元遞迴
### 線性遞迴 : 每一次都只處理一個子問題，然後將這個子問題再拆解成更小的部分，直到問題變得簡單到可以直接解決為止。
- 優點 : 實現簡單且易於理解。
  - 只適用於可以被分解成單一子問題的問題，不適合需要同時處理多個子問題的場景，例:迭代元素查找、階乘計算、簡單的數學計算
- 缺點 : 可能導致堆疊溢位和效率問題
  - 由於每次只處理一個問題所以在處理大型問題時可能會遇到效率低下、堆疊溢位和高記憶體使用。
 
 ### 二元遞迴 : 每次呼叫遞迴時，會分裂成兩個子問題產生兩個新的遞迴分支，只需選擇問題的其中一半去解決。
- 優點 : 高效處理分治問題，降低每次要解決問題的規模，
  - 能夠解決更複雜的問題，適合於需要同時處理多個子問題的情況，例如組合問題和樹結構遍歷。
- 缺點 : 效率低，可能會造成內存不足或堆疊溢位
  - 呼叫次數成指數增加，尤其是在輸入增大時，容易造成重複計算，占用額外的內存和堆疊空間。

# 遞迴函式
- Factorial - 階乘 
- GCD - 最大公因數
- Search in Array - 搜尋
- Tower of Hanoi - 河内塔
- Fibonacci series - 費氏數列
- Combinatorial numbers - 組合數
- Fractal - 碎形
  
# 實作
## Factorial
n !=n×( n−1 )×( n−2 )×…×3×2×1
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
gcd ( a ,b )=gcd ( b ,a mod b )
兩種做法
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
|           | gcd1           | gcd2  |
|:-----------:|:-------------:|:-----:|
| 檢查   | 檢查哪個數字作為呼叫自身的第一個參數 | 直接做輾轉相除法的計算，無需額外檢查 |
| 優點    | 無論輸入非0數字的大小順序如何，都可以正常計算。 |  更簡單、更有效率(輸入值須遵循特定條件) 。|
| 缺點    |   由於額外的檢查效率稍低。         |   輸入時需要有特定的輸入順序，不然會產生多餘遞迴堆疊。 |


## Binary search
1. 初始化邊界：分左半和右半
2. 計算中間位置 mid
3. 比較中間元素與目標值 array[mid], value 
```cpp=
int binarySearch(int Array[], int first, int last, int value) {
  // base case ：first > last，回傳-1表示目標值不在陣列中
  int index;
  if (first > last) {
    index = -1;
  // recursive case ：計算中間位置，比較中間元素與目標值
  } else {
    int mid = (first + last) / 2;
    if (value == Array[mid]) {
      index = mid;
    } else if {
      index = binarySearch(Array, first, mid-1, value);
    } else {
       index = binarySearch(Array, mid-1, last, value);
    }
  }
  return index;
} // end binarySearch
``` 
相關應用 : 找最大值、找第k小的值。
## Tower of Hanoi
```cpp=
void towers (numDisks, source, dest, auxilaiary) {
  if (numDisk == 1) {
    std::cout << "Move from " << source << "to " << dest << std::endl;
  } else {
    towers (numDisks - 1, source, auxilaiary, dest);
    towers (1, source, dest, auxilaiary);
    towers (numDisks - 1, auxilaiary, dest, source);
  }
}
```

## Fibonacci series
Fn = Fn−1 + Fn−2
兩種做法
```cpp=
int Fibonacci1(int n) {
  if (n <= 2) {
    return 1;
  } else {
    return Fibonacci1(n-1) + Fibonacci1(n-2);
  }
}
```
```cpp=
std::pair<int, int> Fibonacci2(int k) {
  // base case：若 k = 1，則回傳 (1, 0)，對應於 (F1, F0)
  if (k == 1) {
    return {1, 0};
  // recursive case：呼叫 Fibonacci2(k-1) 並返回 (F(k), F(k-1))
  } else {
    std::pair<int, int> previous = Fibonacci2(k - 1);
    // 透過前一對結果計算當前 Fibonacci 數列值 (F(k), F(k-1))
    return {previous.first + previous.second, previous.first};
  }
}
```
|           | Fibonacci1           | Fibonacci2  |
|:-----------:|:-------------:|:-----:|
| 呼叫次數   | 呼叫次數成指數成長 | 呼叫次數呈現性成長 |
| 優點    | 簡單直接的實施 |  在時間複雜度上更有效率。 |
| 缺點    |   由於子問題重複，對於值較大的數來說效率非常低。 |   在閱讀上稍微複雜一些。 |
## Combinatorial numbers
N選K的組合數
c(n,k) = c(n-1, k-1) + c(n-1, k)
```CPP=
int Combinatorial(int k, int n) {
  // base case：若 k = 0，不取，回傳1
  if (k == 0) {
    return 1;
  // base case：若 k = n，一次取全部，回傳1
  } else if (k == n) {
    return 1;
  // base case：若 k > n，無法取大於自己的數量，回傳0
  } else if (k > n) {
    return 0;
  // recursive case：0 < k < n
  } else {
    return  Combinatorial(n - 1, k - 1) +  Combinatorial(n - 1, k);
  }
}
```

#CH2

