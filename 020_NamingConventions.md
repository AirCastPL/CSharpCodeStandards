2. Naming Conventions
=====================
程式碼可維護性的關鍵是**一致性(Consistency)**。而我們將從 識別子(Identifiers) (包含欄位、屬性、變數、函式、參數、類別、介面、命名空間等) 的命名方式著手開始。


2.1 General Guidelines
----------------------
- 使用簡潔、有意義、明確、具體的名稱。

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


2.2 Name Usage & Syntax
-----------------------
###2.2.1 Namespace###
- 使用 帕斯卡命名法(Pascal Case) 為 命名空間 命名。

- 使用 產品名稱 或 公司名稱 做為 根命名空間(Root Namespace) 的名稱。


###2.2.2 Enum###
- 使用 帕斯卡命名法(Pascal Case) 為 列舉 命名。

- 嘗試使用 名詞 或 名詞片語 做為 列舉 的名稱。

- **不要** 將 列舉 名稱加上 "Enum" 的後綴詞。
    ```csharp
        // **BAD**
        public enum GameTypeEnum
        {…}
    ```


###2.2.3 Interface###
- 使用 帕斯卡命名法(Pascal Case) 為 介面 命名，並加上前綴詞 "I"。


###2.2.4 Class, Struct###
- 使用 帕斯卡命名法(Pascal Case) 為 類別 及 結構 命名。

- 嘗試使用 名詞 或 名詞片語 做為 類別 及 結構 的名稱。

- 嘗試使用 父類別 名稱此類別名稱的作為後綴詞。
    + 為自訂的 擴充類別 (Extension Class) 名稱加上 "Extensions" 後綴詞。
    + 為自訂的 特性 (Attribute) 類別名稱加上 "Attribute" 後綴詞。
    + 為自訂的 控制器 (Controller) 類別名稱加上 "Controller" 後綴詞。

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


- 使用 帕斯卡命名法(Pascal Case) 為非私有的 屬性 命名。
    + 避免使用 `private` 之屬性。

- 使用 駝峰式命名法(Camel Case) 為私有 欄位 命名，並加上前綴詞 "_"。
    + 避免使用非 `private` 之欄位。

- 使用 駝峰式命名法(Camel Case) 為 常數 及 靜態欄位 命名。

- **避免** 屬性名稱中包含其所屬 類別 或 結構 的名稱。
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
| Method Parameter        |               |                      |            |             | **c**     |
| Delegate                | **P**         | **P**                | **P**      | **P**       | **P**     |
| Event                   | **P**         | **P**                | **P**      | **P**       | **P**     |
| Property                | **P**         | **P**                | **P**      | **P**       | x         |
| Field                   | x             | x                    | x          | x           | **_c**    |
| Static Field            | **P**         | **P**                | **P**      | **P**       | **P**     |
| Constant                | **P**         | **P**                | **P**      | **P**       | **P**     |
| Variable                |               |                      |            |             | **c**     |
| Anonymous Type Property | **P** / **c** |                      |            |             |           |

