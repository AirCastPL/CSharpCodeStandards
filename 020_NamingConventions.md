2. Naming Conventions
=====================
程式碼可維護性的關鍵是**一致性(Consistency)**。而一致性最重要的是 專案名稱、原始碼檔案 以及 修飾子 (包含欄位、屬性、變數、函式、參數、類別、介面、命名空間等) 的命名。

2.1 General Guidelines
----------------------

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


- ~~Do not create declarations of the same type (namespace, class, method, property, field, or parameter) and access modifier (protected, public, private, internal) that vary only by capitalization.~~

- **不要** 使用以數字開頭的名稱。
    + 實際上 C# 也不允許數字開頭之名稱。

- ~~Do add numeric suffixes to identifier names.~~

- 使用簡潔、有意義、明確、具體的名稱。

- ~~Always err on the side of verbosity not terseness.~~

- ~~Variables and Properties should describe an entity not the type or size.~~

- **避免** 使用 C# 保留字做為名稱。

- **避免** 命名與 `.NET Framework` 的命名空間(Namespaces) 或 型別(Types) 衝突。

- **避免** 使用縮寫，除非全名真的過長；且縮寫不應超過 5 個字母。

- 縮寫使用 帕斯卡命名法(Pascal Case)。

- 任何縮寫必須是為大家所熟悉且認同的。

- **避免** 於名稱中加入冗於、無意義的前餟或後綴詞。

- **避免** 屬性名稱中包含其所屬類別的名稱。

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


- 嘗試使用 "Can"、"Is"、"Has" 做為前綴詞，在 `bool` 型別的變數或屬性命名上。

    ```csharp
        // **GOOD**
        var isSunday = DateTime.Today.DayOfWeek == DayOfWeek.Sunday;

        // **GOOD**
        public bool HasEnoughMoney => user.GetMoney() >= cart.GetTotalMoney();
    ```


- 嘗試在適當的時機，為變數名稱附加上 "Average"、"Count"、"Sum"、"Min"、"Max" 等統計的修飾詞。

- 使用 產品名稱 或 公司名稱 做為 根命名空間(Root Namespace) 的名稱。


2.2 Name Usage & Syntax
-----------------------





