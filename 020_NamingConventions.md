2. Naming Conventions
=====================
Consistency is the key to maintainable code. This statement is most true for naming your projects, source files, and
identifiers including Fields, Variables, Properties, Methods, Parameters, Classes, Interfaces, and Namespaces.

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


- **不要** 使用全大寫或全小寫的名稱 (除非 單個小寫單詞 或 單個字母)。
    ```csharp
        // **BAD**
        var thisisabook = new Book();
        
        // **GOOD**
        var book = new Book();
    ```


- Do not create declarations of the same type (namespace, class, method, property, field, or parameter) and access modifier (protected, public, private, internal) that vary only by capitalization.
- 不要建立相同類型的宣告(包含namespace、class、method、property、field or parameter)與保留字

- **不要** 使用以數字開頭的名稱。
    + 實際上 C# 也不允許數字開頭之名稱。

- ~~Do add numeric suffixes to identifier names.~~
- ~~不要把數字加入變數的中綴詞~~

- 使用有意義、明確及具體的名稱。

- Always err on the side of verbosity not terseness.
- 如果簡潔的命名無法明確表達意義，使用較冗長的命名

- Variables and Properties should describe an entity not the type or size.
- 變數與屬性必須能夠描述他自己

- **避免** 使用縮寫，除非全名真的過長；且縮寫不應超過5個字。

- Any Abbreviations must be widely known and accepted.
- 任何的縮寫必須是為大家所知道的

- Use uppercase for two-letter abbreviations, and Pascal Case for longer abbreviations.
- 使用Pascal Case來設計比較長的縮寫變數

- Do not use C# reserved words as names.
- 不要使用C#保留字當做變數

- Avoid naming conflicts with existing .NET Framework namespaces, or types.
- 避免變數與.NET Framework namespace 和 型別衝突

- Avoid adding redundant or meaningless prefixes and suffixes to identifiers
- 避免增加無意義的前餟詞與中綴詞

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


- Append computational qualifiers to variable names like Average, Count, Sum, Min, and Max where appropriate.
- 加上 "Average" "Count" "Sum" "Min" "Max" 關鍵字在計量的變數上

- 定義 root namespace 時，使用產品或公司名字。


2.2 Name Usage & Syntax
-----------------------





