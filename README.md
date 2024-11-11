##### 甲班11227117_吳彥霖
# CH1 
## 遞迴-Recursion
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
- 階乘(Factorial)
- 最大公因數(GCD)
- 搜尋(Search in Array) 
- 河内塔(Tower of Hanoi)
- 費氏數列(Fibonacci series)
- 組合數(Combinatorial numbers)
- 碎形(Fractal)
  
# 實作
## 階乘
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
## 最大公因數
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


## 二元搜尋 Binary search
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
## 河内塔
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

## 費氏數列
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
## 組合數
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

# CH2
## 資料抽象化 - Data Abstraction
- 將資料和操作隱藏於介面之後，透過介面與實作分離來簡化複雜性，使程式更安全且易於設計。
## 物件導向 oo(object-oriented)
- 類別 (Class)：
  - 屬性 (Attributes)：每個類別的變數(data member)，代表類別的狀態或特徵。
  - 運算 (Behaviors)：操作在類別中的函數(member funtions)，定義物件的操作或計算，並且可以存取物件的屬性。
  - 建構子 (Constructor)：初始化新建立的物件。
  - 解構子 (Destructor)：清理物件佔用的資源。
- 物件 (Object)：
  - 包含屬性和行為的小單位，大物件是由小物件組成。
### 封裝 (Encapsulation)
將物件的屬性和運算封裝在一起並隱藏內部實作細節，使得外部無法直接訪問或修改物件的內部細節，從而限制對內部狀態的直接存取，只暴露必要的介面給外部使用。
- 通常會將data member設置為私有（private），只能透過member funtions進行訪問。
### 繼承 (Inheritance)：
類別可以從其他類別繼承屬性。已存在的類別可以被重複使用。
- 單一繼承：一個子類別只能繼承一個父類別（基底類別）。
- 多重繼承：一個子類別同時繼承多個父類別（菱形問題 : 一個類別透過兩個不同路徑繼承自同一個基底類別時，會出現二義性）。
### 多型 (Polymorphism)：
同一介面可以被不同類型的物件實現
- 方法重載 (Method Overloading)：函數同名但有不同的參數類型或數量。
- 方法覆蓋 (Method Overriding)：透過繼承和虛擬函數機制，使得在呼叫物件時會根據類型來讓子類別覆寫覆類別。
## 運算合約 (Operation Contracts)
- 紀錄方法的使用和侷限性 - 包含目的、假設、輸入、輸出。
- 前置條件（Preconditions）：在執行操作前必須滿足的條件。
- 後置條件（Postconditions）：操作執行結束後系統應該滿足的狀態。
- 指定資料流 - 定義資料如何進入和流出的方法。
- 不指定模組該如何執行任務 - 只專注於輸入和輸出的正確性。
- 不正常情況 - 例外狀況
## 程式設計中的關鍵問題 ：
- 可修改性 (Modifiability) ：程式設計應是設計給未來用的，應確保變更資料結構或功能時對其他程式碼的影響是最小。
- 風格 (Style) : 使用通用風格讓程式碼更易讀，結構清晰，有助於後續的團隊合作和程式維護。
- 易用性 (Ease of Use) ：設計得直觀，介面簡潔，以便於開發者快速理解和使用。
- 安全編程 (Fail-Safe Programming) ：設計應防止錯誤操作，並提供例外處理機制來避免程式崩潰或數據損壞。
- 除錯 (Debugging) ：需設置良好的除錯機制，以便開發者能夠輕鬆找到錯誤並修正。
= 測試 (Testing) ：需要經過嚴謹的測試，以確保功能正確、穩定，並在各種情況下都能正常運作。
# ADT(抽象資料類型)
- 定義了資料的行為和操作，而不關心其具體實現。
## 模組化 (Modularity)
### 定義：透過系統化控制大型程式組件之間的互動，使大型程式的複雜性保持可控。
- 隔離錯誤 (Isolates errors)
- 消除冗餘 (Eliminates redundancies)
### 模組化程式的優點：
- 更容易撰寫 (Easier to write)
- 更容易閱讀 (Easier to read)
- 更容易修改 (Easier to modify)
- 拆解區塊分別管理，較方便管理、易於維護。
## 內聚性與耦合性：實現更好的解法
### 內聚性 (Cohesion)
- 定義：模組執行單個明確定義的任務。
- 設計：高度內聚的模組 (Highly cohesive modules desired)
- 模組被視為單獨個體執行程度越高，內聚性越高。
- 模組需傳遞的參數較多且不是每次都會使用到。
### 耦合性 (Coupling)
- 定義：模組之間依賴的度量。
- 設計：低耦合的模組 (Loosely coupled modules desired)
- 與其他函式關聯性越低，耦合性越低。
- 每個函式只做一件事，大幅減少參數的傳遞。
## C++ class
- 物件是類別的實例
- class定義新的資料型別
- class包含資料成員(data mnmber)和方法(method) -（member funtions）
- 預設情況下，class中的所有成員預設都是私有的，但也可以將其指定為公共
- 封裝隱藏了實作(implementation)細節
class的定義通常放在header file（標頭檔案，副檔名.h）中，class的方法實作放在implementation file（實作檔案，副檔名.cpp)中。以此將介面與實作分離，增強程式碼組織、可維護性和可用性

header file (.h) 介面的部分：包含類別的結構、資料成員、方法宣告，讓使用者知道有哪些功能可以使用而不需知道如何實作。
```cpp=
// @file Sphere.h
const double PI = 3.14159;
class Sphere {
private:
    double theRadius;
public:
    Sphere();
    Sphere(double initialRadius);
    void setRadius(double newRadius);
    double getRadius() const;
    // 其他成員函數宣告...
};
```

Implementation File (.cpp)類別的具體實作，即程式的運算邏輯與如何完成實作。

```cpp=
// @file Sphere.cpp
#include "Sphere.h"

Sphere::Sphere() : theRadius(1.0) {}

Sphere::Sphere(double initialRadius) {
  if (initialRadius > 0)
    theRadius = initialRadius;
  else
    theRadius = 1.0;
}

void Sphere::setRadius(double newRadius) {
  if (newRadius > 0)
    theRadius = newRadius;
   else
     theRadius = 1.0;
}

double Sphere::getRadius() const {
  return theRadius;
}
```
- 實現 ADT 的模組化：
  - 透過分離介面和實作，將功能定義於 header file、具體實作於 implementation file，讓使用者只需引用 header file 即可使用類別功能而不需了解內部實作。確保了即使修改實作也不會影響使用者，只要介面保持不變，其他程式無需重編譯。

# CH3
## 指標與鏈結串列 - Pointers and Linked lists
- 可以比較彈性的擴充，但是每個位置都是依據前一個位置的指標指著去找到後一個位置。
- head是唯一可以用程式找到地，若後續串列其中一個位置遺失，後面的資料很如容易找不到。
- 相關應用 : 網路、樹狀圖
### 陣列跟列節串列的差別
- 陣列 : 陣列大小有固定大小，每次插入或是刪除資料，需要移動資料
- 鏈結串列

