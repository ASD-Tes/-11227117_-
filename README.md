##### 甲班11227117_吳彥霖
# CH1 
## 遞迴-Recursion
- 將大問題分解成更小的相同問題，**分而擊之**。
- 迭代的替代方案
- 用box trace視覺化遞迴函數的呼叫堆疊
 ### 遞迴的組成
  - **基本情況 (Base case)** : 問題簡化到最基本的形式，停止遞迴函數呼叫直接傳回一個結果。
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
  - 屬性 (Attributes)：每個類別的**變數(data member)**，代表類別的狀態或特徵。
  - 運算 (Behaviors)：操作在類別中的**函數 (member funtions) / 方法 (methods)**，定義物件的操作或計算，並且可以存取物件的屬性。
  - 建構子 (Constructor)：初始化新建立的物件。
  - 解構子 (Destructor)：清理物件佔用的資源。
- 物件 (Object)：
  - 包含屬性和行為的小單位，大物件是由小物件組成。
### 封裝 (Encapsulation)
將物件的屬性和運算封裝在一起並**隱藏內部實作細節**，使得外部無法直接訪問或修改物件的內部細節，從而限制對內部狀態的直接存取，只暴露必要的介面給外部使用。
- 通常會將data member設置為私有（private），只能透過member funtions進行訪問。
### 繼承 (Inheritance)：
類別可以從其他類別繼承屬性。已存在的類別可以被**重複使用**。
- 單一繼承：一個子類別只能繼承一個父類別（基底類別）。
- 多重繼承：一個子類別同時繼承多個父類別（菱形問題 : 一個類別透過兩個不同路徑繼承自同一個基底類別時，會出現二義性）。
### 多型 (Polymorphism)：
同一介面可以被不同類型的物件實現
- 方法重載 (Method Overloading)：函數同名但有不同的參數類型或數量。
- 方法覆蓋 (Method Overriding)：透過繼承和虛擬函數機制，使得在呼叫物件時會根據類型來讓子類別覆寫覆類別。
## 運算合約 (Operation Contracts)
- 用於程式碼文件化，尤其是**標頭檔案**。
- 紀錄方法的使用和侷限性 - 在分析階段開始撰寫契約，並在設計階段完成，包含目的、假設、輸入、輸出。
- 前置條件（Preconditions）：在執行操作前必須滿足的條件。
- 後置條件（Postconditions）：操作執行結束後系統應該滿足的狀態。
- 指定資料流 - 定義資料如何進入和流出的方法。
- **不指定**模組該如何執行任務 - 只專注於輸入和輸出的正確性。
- 不正常情況 - 例外狀況
## 程式設計中的關鍵問題 ：
- 可修改性 (Modifiability) ：程式設計應是設計給未來用的，應確保變更資料結構或功能時對其他程式碼的影響是最小。
- 風格 (Style) : 使用通用風格讓程式碼更易讀，結構清晰，有助於後續的團隊合作和程式維護。
- 易用性 (Ease of Use) ：設計得直觀，介面簡潔，以便於開發者快速理解和使用。
- 安全編程 (Fail-Safe Programming) ：設計應防止錯誤操作，並提供例外處理機制來避免程式崩潰或數據損壞。
- 除錯 (Debugging) ：需設置良好的除錯機制，以便開發者能夠輕鬆找到錯誤並修正。
= 測試 (Testing) ：需要經過嚴謹的測試，以確保功能正確、穩定，並在各種情況下都能正常運作。
# ADT(抽象資料類型)
- **定義了資料的行為和操作，而不關心其具體實現。**
## 模組化 (Modularity)
### 定義：透過系統化控制大型程式組件之間的互動，使大型程式的複雜性保持可控。
- **隔離錯誤 (Isolates errors)**
- **消除冗餘 (Eliminates redundancies)**
### 模組化程式的優點：
- 更容易撰寫 (Easier to write)
- 更容易閱讀 (Easier to read)
- 更容易修改 (Easier to modify)
- 拆解區塊分別管理，較方便管理、易於維護。
## 內聚性與耦合性：實現更好的解法
### 內聚性 (Cohesion)
- 定義：模組執行單個明確定義的任務。
- 設計：**高內聚**的模組 (Highly cohesive modules desired)
- 模組被視為單獨個體執行程度越高，內聚性越高。
- 模組需傳遞的參數較多且不是每次都會使用到。
### 耦合性 (Coupling)
- 定義：模組之間依賴的度量。
- 設計：**低耦合**的模組 (Loosely coupled modules desired)
- 與其他函式關聯性越低，耦合性越低。
- 每個函式只做一件事，大幅減少參數的傳遞。
## C++ class
- 物件是類別的**實例**
- class定義新的資料型別
- class包含**資料成員 (data mnmber)** 和 **方法 (method)** -（member funtions）
- 預設情況下，class中的所有成員預設都是**私有的**，但也可以將其指定為**公共 (public)**。
- 封裝隱藏了實作(implementation)細節
- class的定義通常放在**header file（標頭檔案，副檔名.h)** 中，class的方法實作放在**implementation file（實作檔案，副檔名.cpp)** 中。以此將介面與實作分離，增強程式碼組織、可維護性和可用性 
### 建構子 (constructors) : 向電腦請求記憶體來儲存資料
  - 建立並初始化類別的新實例 ：建構函數負責創建類別的實例並進行初始化。**在聲明類別實例時會自動調用建構函數。**
  - 與類別同名，且無返回型別：建構函數的名稱與類別名稱相同，並且沒有返回型別，甚至沒有 void。
  - 類別可以有多個建構函數：一個類別可以有多個建構函數（透過不同的參數來區分），這種特性稱為「建構函數重載」。
  - 預設建構函數：若建構函數沒有任何參數，則稱為預設建構函數。若類別中未定義任何建構函數，編譯器會自動生成一個預設建構函數。
  - 使用作用域解析運算子 (scope resolution operator) "::"。
  - 設置資料成員的初始值：建構函數的主要功能是為物件的資料成員設定初始值。在建構函數內可以直接設置這些成員，也可以使用初始化列表進行初始設置。
  - 使用初始化列表：初始化列表是一種直接在建構函數名稱後方、函數主體前使用的語法，可以更有效地初始化資料成員。
    ```cpp=
    Sphere::Sphere() : theRadius(1.0) { //預設初始值為1.0， 
    
    } // 預設建構函數
    ```
### 解構子 (destructors)
  - 銷毀物件實例：解構函數在物件的生命週期結束時自動調用，負責釋放物件使用的資源，並進行其他清理工作，以確保內存和資源被適當回收。
  - 每個類別僅有一個解構函數：每個類別只能有一個解構函數，且名稱為 ~ 加上類別名（例如 ~Sphere()），無需參數且無返回值。
  - 許多類別可省略解構函數：如果類別不包含動態分配的資源（如指標或外部資源），通常不必定義解構函數。編譯器會自動生成一個默認的解構函數，負責基本的資源釋放。 
  - 當前使用編譯器生成的解構函數：若沒有特定清理需求，可以直接使用編譯器自動生成的解構函數。
### 命名空間 (namespace)
- 命名空間的機制 : 將宣告和定義邏輯分組到共同的聲明區域中的機制。
  - 將相關的類別、函數、變數等放在同一區域內，以便組織程式碼、避免名稱衝突。
- 命名空間的內容可以由命名空間**內部**或**外部**的代碼存取。
- using 聲明：使用 using 聲明可以將命名空間中的元素名稱直接引入當前作用域，從而避免多次使用"::"。
- using namespace ：使用 using namespace 可以引入整個命名空間的所有成員，便於在當前作用域內直接使用命名空間的內容，但要小心名稱衝突。
### 例外狀況 (exceptions)
- 一種執行過程中處理錯誤的機制
- 拋出例外 (Throwing an Exception)：當函數或程式碼區段遇到錯誤情況時，可以用 throw 關鍵字來拋出例外，指示程式發生了異常。
- 捕獲和處理例外 (Handling an Exception) ：使用 try 和 catch 區塊來處理異常情況。
  - try 區塊 ：包含可能拋出例外的程式碼。
    - 如果發生例外，其餘語句將不再執行，會直接跳至相應的 catch 區塊進行處理。
      - 跳出例外後會在離開 try 區塊錢調用區塊內本地物件的解構函數，以確保資源被正確釋放。
  - catch 區塊 ：用於捕獲特定類型的例外，並提供處理邏輯
    - catch 區塊可以有多個，以處理不同類型的例外情況。
    - 當 catch 區塊執行完畢後，控制權將傳遞至該 try-catch 結構後面的第一條語句，繼續執行。
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
- head是唯一可以用程式找到，若後續串列其中一個位置遺失，後面的資料很如容易找不到。
- 相關應用 : 網路、樹狀圖
### 陣列跟鏈結串列在變動資料上的差別
- 陣列 : 陣列有**固定**大小，每次插入或是刪除資料，需要**移動**資料位置。
- 鏈結串列 : 鍊結串列的大小可以根據需要**增長**，每次插入或是刪除資料，不需要移動資料位置。

### 指標 (Pointer) : 指標包含記憶體空間的位置或記憶體中的位址。
- 宣告方式 :
  ```cpp
  int *p; //初始未定義，但不為 NULL
  ```
- 指標位址上內容 ：
  ```cpp
  *p //p指向的儲存空間
  p = &x; //p儲存x的位址，指向x的儲存空間。
  ```
  ### 動態配置
  配置記憶體 : 指定資料類型分​​配記憶體，並傳回指向該記憶體的指標。
  ```cpp==
  p = new int;
  ```
  釋放記憶體 : 釋放記憶體空間，將記憶體傳回給系統以供**重複使用**，使其可供其他進程使用並防止記憶體洩漏。
  - 一定要先 "delete" 變數再將變數設為 "NULL"，以防止記憶體洩漏 (memoery leak)
   ```cpp==
  delete p;
  p = NULL //設為NULL避免指標已釋放，指標本身仍然保存現在已釋放的記憶體的位址。
  ```

## 動態陣列配置

- 配置動態陣列 ：
  ```cpp
  int arraySize = 50;
  double *anArray = new double[arraySize];
  ```
- 陣列名是指向其第一個元素的指標 :
  ```cpp
  anArray[2] ≡ *(anArray + 2); //陣列名稱 = 指標
  ```
- 配置陣列大小 ：
  ```cpp
  double *oldArray = anArray;
  anArray = new double[3 * arraySize];
  delete[] oldArray;
  ```

### 指標鍊結串列
- 結構 : 每個節點包含節點資料跟指向下一個節點的指標
``` cpp=
struct Node {
  int item
  Node *next;
};
```
- 頭指標(head) : 指向整個鏈結串列的開頭，如果 **head = NULL** 代表鍊結串列為**空 (empty)**。
  - head 是訪問串列的唯一入口，所以在實作插入或是刪除時，走訪串列的過程需要用另一個指向 head 的指標去走訪，確保 head 指向的位置不會被更動。
### 複製建構子和解構子 (Constructors and Destructors)
  - 複製建構子主要負責在創建鏈結串列物件時初始化其成員變數，通常包括設定 size 和 head 的初始值。
  - 複製建構函式的預設行為執行淺層複製，這可能會在處理動態分配的記憶體時導致問題。為了避免這些問題，通常會實施深層複製。
    - 淺層複製和深層複製 (shallow copy and deep copy)
      - 淺層複製 ：只複製head指標跟串列大小，head是指向原鍊結串列，
        - 如果任一物件進行修改，另一物件也會受到影響。
      - 深層複製 ：複製整個鍊結串列，包括head、串列大小、整個鍊結串列內容。
        - 每個複製的鏈結串列都有其獨立的節點，相當於同樣內容但是存取在不同位址。需自訂義複製建構子。
  - 如果省略複製建構函數，編譯器會產生一個預設建構子，但它僅適用於使用**靜態分配陣列**的情況，不合適動態配置的鏈結串列。
  - 動態配置記憶體，需在解構時主動去釋放記憶體空間，因為系統無法預知物件的具體結構或管理方式，所以不會自動清除程式動態分配的記憶體。

## 比較基於陣列與基於指標的實作

- 大小 (Size)
  - 可調整大小的陣列在擴大時，可能會浪費儲存空間和時間。
  - **鏈結串列**會隨著需要動態增長或縮小。
- 儲存需求 (Storage Requirements)
  - 基於陣列的實作相比基於指標的實作，在抽象資料型別（ADT）的每個項目上**需要更少的記憶體**。
- 檢索 (Retrieval)
  - 基於陣列 ：存取第 i 個元素的時間是**常數 (Constant)**，與 i 無關。
  - 基於指標 ：存取第 i 個元素的時間**取決於 i**，需要從頭開始遍歷直到第 i 個節點。
- 插入和刪除 (Insertion and Deletion)
  - 基於陣列 ：需要**移動**資料，將變動資料位置之後的資料全部往後或是往前。
  - 基於指標 ：需要**遍歷** (traversal)，走訪到要變動資料得位置。

- 陣列 (Arrays) vs. 連結串列 (Linked Lists)
  - 基於陣列的列表使用**隱式 (implicit)** 排序方式，基於指標的列表使用 **顯式 (explicit)**排序方式。
  - 陣列允許直接存取 (direct access)元素，而鍊結串列需要遍歷 (traversal)。
  - **擴大陣列的大小需要複製**。

### 使用檔案儲存和恢復鏈結串列
- 使用**外部檔案**來保持列表在程式運行間的狀態。
- 只將**資料**寫入檔案，不存**指標**。- 指標當電腦關閉後就會重置。
- 透過將每個項目放置於鏈結串列的**末端**來重新創建列表，所以每一次重建的指標位置是不同的
  - 使用**尾端 (tail)**指標來促進將節點加入鏈結串列的末端。
  - 將第一次插入視為特殊情況，將尾端指標設為頭指標。  

### 鏈結串列的種類
1. **單向鏈結串列**：每個節點指向下一個節點。
2. **循環鏈結串列**：最後一個節點指回頭節點。
3. **雙向鏈結串列**：每個節點有指向前一個和下一個節點的指標。
  
## 圓形鍊結串列 (Circular Linked Lists)
- **最後一個節點指向第一個節點**，形成環狀結構。
- 每個節點都有**後繼節點 (successor)**。
- 循環連結串列中的節點不包含NULL，不會有指向空指標的情況。
- 存取最後一個節點需要遍歷整個鏈結串列。
- 讓**外部指標**指向**最後一個節點**，而非第一個節點。
  - 這樣可以在不遍歷整個列表的情況下，直接存取第一個和最後一個節點。
- 要變動資料仍需要從偷開始遍歷，無法直接透過索引存取元素。
- 可以從任意節點開始遍歷整個串列，適合需要循環存取的任務。
  
## 變形：虛擬頭節點 (Dummy Head Node)
- 總是存在，即使鍊結串列為空。
  - 它是新增在串列開頭的額外節點，不包含有效的資料只是用來簡化鏈結串列的操作，通常指向鍊結串列中的第一個實際資料節點。 
- 插入和刪除操作會將 *prev* 指標初始化為指向**head dummy node**，而不是 *NULL*。 
  - 消除判斷串列第一個元素的操作的**特殊情況**。
    - 由於有虛擬頭節點，插入或刪除操作不需要分別處理頭節點和其他節點，從而去除了例外狀況。  


## 變形：雙向連結串列 (Doubly Linked Lists)
- 每個節點都指向其前驅 (precede) 和後繼 (next)的指標。
- 插入和刪除操作比單向連結串列更複雜。
- 通常包含一個虛擬頭節點 (dummy head node)，以簡化程式消除處理特殊情況。
- 常用環狀 (circular) 結構來消除特殊情況。
- 雙向結構不僅具備環狀結構的優點，還能在任一方向進行遍歷，使我們更方便地刪除或插入節點。
- 因為需要紀錄前後節點位置，所需空間相對多。

# CH4
遞迴作為解決問題的技巧
## Defining Languages
- 規範使用者哪些東西是合法，在範圍內即是合法。
  - 語言提供了符號集合，而語法定義了如何將這些符號組合成合法的表達形式。 
    - 語言 (language)
      - 語言是一組由符號組成的字串集合，符合該語言的語法和規則。 
        - 形式語言 (formal languages)
        - 正則語言 (Regular Language)
    - 語法 (grammar)
      - 語法是用於構成語言中合法字串的規則集合。 
        - 分支 : 正規運算式/正規表示式 (regular Expresion)
### 語法的基本概念
- 語法中使用的符號 : 用符號描述規範。
- x | y：表示 "x or y" ，表示字串可以是 x 或 y。
- x y 或 x • y：表示 x 之後接 y，也就是 x 和 y 按順序組合而成。
  - •（連接符號）：表示連接或追加，即將兩個符號或字串串接在一起，形成更長的字串。
- <word>：這種表示法表示**任何符合 word 定義的實例**，即泛指該詞所代表的結構或形式。
- 實作 : 遞迴，基本情況就是剩餘一個字元時，判斷是否符合語法 
  ```plaintext
  - <addtion> = <number> + <addtion> | <number>
  - <number> = <number><digit> | <digit>
  - <digit> = 0|1|2|3|4|5|6|7|8|9
  ```
### 代數表達式 (Algebraic Expressions)
中序 (infix)、前序 (prefix)、後續 (postfix)，指的是運算子的位置。  
  - **中序表示法 (Infix expressions)**：
    - 運算子出現在操作數之間，這是最常見的表達式形式，人類易於閱讀。
    - 範例 ："a + b"
    - 加上括號來明確運算順序，而不是依賴運算符的優先級來判斷順序。
      - 程式是一個一個讀，所以若是沒設先後條件會不知道哪個要先做。 
      ```plaintext
      <infix> : <identifier> | (<infix><operator><infix>)
      <operator> : + | - | * | /
      <identifier> : a | b | ... | z
      ```
  - **前序表示法 (Prefix expressions)**：
    - 運算子出現在操作數之前，相對於中序，是把運算子移到其相對應左括號標記的位置，把括號去除。
    - 範例 ："+ a b"
    - 一個前序式後面再接上**非空字串**一定不是前序式。
      ```plaintext
      <prefix> : <identifier> | <operator> <prefix> <prefix>
      <operator> : + | - | * | /
      <identifier> : a | b | ... | z
      ```

  - **後序表示法 (Postfix expressions)**：
    - 運算子出現在操作數之後，相對於中序，是把運算子移到其相對應右括號標記的位置，把括號去除。
    - 範例 ："a b +"
      ```plaintext
      <postfix> :<identifier> | <postfix> <postfix> <operator>
      <operator> : + | - | * | /
      <identifier> : a | b | ... | z
      ```
   - 相較於中序式，前序式跟後續式的優點 :
      - 無優先級規則 (No precedence rules) : 不用擔心讀的順序，因為讀的順序義唯一的。
      - 無結合律規則 (No association rules)：
      - 無括號 (No parentheses)：
      - 簡單語法 (Simple grammars)：
      - 直觀的識別和求值算法

## 回溯法 (Backtracking)
- 回溯法是一種通過猜測解決方案並在遇到僵局/死巷時退回的策略。
- **遞迴 (Recursion)** 與 **回溯法**結合使用以解決問題，尤其是需要探索所有可能解或查找最優解的問題。
  - 例 : 八后問題、迷宮探索、數獨，最短路徑等。

## 八后問題 (Eight-Queens Problem)
- 削減不必要組合的觀察法則 (Pruning Observation) : 先用規則排除不可能，減少範圍。
- 將八個皇后放置在棋盤上，使得任意兩個皇后不會互相攻擊。
1. **基本情況 (Base case)**：
   - 如果已經沒有更多列需要考慮，
2. **遞迴情況 (Recursive step)**：
   - 如果能**成功地**在當前列放置一個皇后。
     - 繼續考慮下一列。
   - 如果**無法在當前列放置皇后**
     - 需要**回溯 (backtrack)**，探索其他位置。
## 遞迴和數學歸納法 (Recursion and Mathematical Induction)
- 遞迴和數學歸納法都使用基本情況來解決問題。
- 兩者都是將問題分解成更小的問題逐步解決。
  - 遞迴通過將問題分解為規模更小的相同問題，逐層遞迴來構建完整解答。
  - 數學歸納法則通過假設小規模問題成立（即「歸納假設」），然後證明更大規模的問題也成立。
- 可以用數學歸納法來證明遞迴算法的正確性/特性。
- 歸納法可用來分析遞迴算法的時間複雜度，證明寫法需要花多少時間/空間。 







  

