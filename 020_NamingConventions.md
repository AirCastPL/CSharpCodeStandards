2. Naming Conventions
=====================
程式碼可維護性的關鍵是**一致性(Consistency)**。而我們將從 識別子(Identifiers) (包含欄位、屬性、變數、函式、參數、類別、介面、命名空間等) 的命名方式著手開始。


2.1 General Guidelines
----------------------
- 名稱 必須是 簡潔、有意義、具體、明確、不易混淆的。

- 使用 英文 命名。

- 使用 帕斯卡命名法(Pascal Case) 或 駝峰式命名法(Camel Case)。

- **不要** 使用匈牙利命名法。
    + 隨著開發工具進步，已不須透過名稱註記才能了解型態。
    + 不易重構。

    ```csharp
        // **BAD**
        var sUserName = user.GetName();
        
        // **GOOD**
        var userName = user.GetName();
    ```


- **不要** 使用全大寫或全小寫的名稱 (除非 單個小寫單字 或 單個小寫字母)。
    ```csharp
        // **BAD**
        var thisisabook = new Book();
        
        // **GOOD**
        var book = new Book();
    ```

    ```csharp
        // **BAD**
        const int MAX_DOG_NUMBERS = 99;
        
        // **GOOD**
        const int MaxDogNumbers = 99;
    ```


- **不要** 使用以數字開頭的名稱。
    + 實際上 C# 也不允許數字開頭之名稱。

- **避免** 使用 C# 保留字做為名稱。

- **避免** 命名與 `.NET Framework` 的命名空間(Namespaces) 或 型別(Types) 衝突。

- **避免** 使用縮寫，除非全名真的過長；且縮寫不應超過 5 個字母。

- 縮寫使用 帕斯卡命名法(Pascal Case)。

- 任何縮寫必須是為大家所熟悉且認同的。

- **避免** 於名稱中加入冗於、無意義的前餟或後綴詞。
    ```csharp
        // **BAD**
        private int m_userIndex;
    ```
 

2.2 Name Usage & Syntax
-----------------------
### 2.2.1 Namespace
- **總是** 使用 帕斯卡命名法(Pascal Case) 為 命名空間 命名。

- **總是** 使用 產品名稱 或 公司名稱 做為 根命名空間(Root Namespace) 的名稱。


### 2.2.2 Interface, Class, Struct, Enum
- **總是** 使用 帕斯卡命名法(Pascal Case) 為 介面 命名，並加上前綴詞 "I"。

- **總是** 使用 帕斯卡命名法(Pascal Case) 為 類別、結構、列舉 命名。

- **嘗試** 使用 名詞、名詞片語或形容詞片語 做為 類別、結構、列舉 的名稱。

- **嘗試** 使用 父類別名稱 做為 子類別名稱 的後綴詞 (結構亦同)。
    + 為自訂的 特性 (Attribute) 類別名稱後加上 "Attribute"。
    + 為自訂的 控制器 (Controller) 類別名稱後加上 "Controller"。

    ```csharp
        // **GOOD**
        internal class SpecializedAttribute : Attribute
        {…}

        public class CustomerCollection : CollectionBase
        {…}

        public class CustomEventArgs : EventArgs
        {…}
        
        private struct InsertParameters : IQueryParameters
        {…}
    ```

- **總是** 為自訂的 擴充類別 (Extension Class) 名稱後加上 "Extensions"。

- **不要** 將 類別、結構、列舉 名稱後加上 "Class"、"Struct"、"Enum" 等詞。
    ```csharp
        // **BAD**
        public enum GameTypeEnum
        {…}
    ```


- **總是** 使用 帕斯卡命名法(Pascal Case) 為非私有的 屬性 命名。
    + 避免使用 `private` 之屬性。

- **總是** 使用 駝峰式命名法(Camel Case) 為私有 欄位 命名，並加上前綴詞 "_"。
    + 避免使用非 `private` 之欄位。

- **總是** 使用 駝峰式命名法(Camel Case) 為 常數 及 靜態欄位 命名。

- **避免** 屬性名稱中包含其所屬 類別、結構、列舉 的名稱。
    ```csharp
        // **BAD**
        public class Customer {
            public string CustomerName { get; set; }
        }

        // **GOOD**
        public class Customer {
            public string Name { get; set; }
        }
    ```


- 嘗試在 `bool` 型別的變數或屬性命名上，使用 "Can"、"Is"、"Has" 做為前綴詞。
    ```csharp
        // **GOOD**
        var isSunday = DateTime.Today.DayOfWeek == DayOfWeek.Sunday;

        // **GOOD**
        public bool HasEnoughMoney => user.GetMoney() >= cart.GetTotalMoney();
    ```


### 2.3.3 Method
- **總是** 使用 帕斯卡命名法(Pascal Case) 為 函式 命名。

- **嘗試** 使用 動詞 或 動詞-對象 這樣的組合 做為函式的命名。

- **總是** 為 擴充函式(Extension Method) 名稱加上 "Ext" 前綴詞。
    ```csharp
        // **GOOD**
        public static string ExtToJson(this object)
        {…}
    ```


2.3 Summary
-----------
| 命名方式標記 | 說明                      |
|:----------:|--------------------------|
|            | 無此應用性                 |
| **c**      | 駝峰式命名法 (Camel Case)  |
| **P**      | 帕斯卡命名法 (Pascal Case) |
| **_**      | 添加底線做為前綴詞          |
| x          | 不使用                    |

| 識別子類型                | `public`      | `internal protected` | `internal` | `protected` | `private` |
|------------------------:|:-------------:|:--------------------:|:-----------:|:----------:|:---------:|
| Namespace               | **P**         |                      |            |             |           |
| Struct                  | **P**         | **P**                | **P**      | **P**       | **P**     |
| Enum                    | **P**         | **P**                | **P**      | **P**       | **P**     |
| Class                   | **P**         | **P**                | **P**      | **P**       | **P**     |
| Generic Type Parameter  | T**P**        |                      |            |             |           |
| Interface               | I**P**        | I**P**               | I**P**     | I**P**      | I**P**    |
| Method                  | **P**         | **P**                | **P**      | **P**       | **P**     |
| Parameter               |               |                      |            |             | **c**     |
| Delegate                | **P**         | **P**                | **P**      | **P**       | **P**     |
| Event                   | **P**         | **P**                | **P**      | **P**       | **P**     |
| Property                | **P**         | **P**                | **P**      | **P**       | x         |
| Field                   | x             | x                    | x          | x           | **_c**    |
| Static Field            | **P**         | **P**                | **P**      | **P**       | **P**     |
| Constant                | **P**         | **P**                | **P**      | **P**       | **P**     |
| Variable                |               |                      |            |             | **c**     |
| Anonymous Type Property | **P** / **c** |                      |            |             |           |

