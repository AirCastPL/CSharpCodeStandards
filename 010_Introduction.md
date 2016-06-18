1. Introduction
===============
本文規範及建議如何使用 C# 語言來開發應用程式以及函式庫。希望透過訂定完整清楚的準則、統一程式編寫風格與格式，以減少開發時遇到陷阱或發生錯誤，提高程式碼維護性。

本文包含：
- 命名規則 (Naming Conventions)
- 檔案及目錄結構 (File Organization)
- 程式碼編寫風格 (Coding Style)
- 語言使用規範 (Language Usage)
- 物件模型設計 (Object Model Design)

等部分。


1.1 Scope
---------
本文僅適用於 **C# 語言**。但由於使用 C# 語言開發與 .NET Framework 息息相關，所以亦涵蓋部分 .NET Framework Class Library 之用法說明。


1.2 Terminology & Definitions
-----------------------------
下列為本文所使用術語之定義：

- **關鍵字 (Keyword)**  
    關鍵字是對編譯器有特殊意義而預先定義的保留識別子。  
    在 C# 中，關鍵字必須具有一個前置的 `@` 符號，才能做為程式中的識別子(Identifier)。例如，`@if` 是有效的識別子，但是 `if` 則不是，因為 `if` 是一個關鍵字。

    Reference: https://msdn.microsoft.com/en-us/library/x53a06bb(v=vs.140).aspx


- **存取修飾子 (Access Modifier)**  
    C# 以關鍵字 `public`、`protected`、`internal`、`private` 及 `protected internal` 定義 型別(Types) 與 成員(Members) 間的存取性，這些關鍵字稱為存取修飾子 (Access Modifier)。  
    在 C# 中，類別(Classes) 及其大部分的成員其存取修飾子預設值為 `private`，但 介面(Interfaces) 和 列舉(Enums) 則預設為 `public`。

    Reference: [Access Modifiers, C# Programming Guide, MSDN](https://msdn.microsoft.com/en-us/library/ms173121.aspx)


- **識別子 (Identifier)**  
    開發者所定義的唯一名稱，用來宣告類別、屬性、物件或實體等。

    *Example:*
    ```csharp
        public class MyClassNameIdentifier { … }
    ```


- **駝峰式命名法 (Camel Case)**  
    一種標示 識別子(Identifier) 的命名規則。  
    各單字之間不以空格斷開或連接號（-）、底線（_）連結，首字的第一個字母小寫，其後除每個單字的第一個母大寫其餘皆為小寫。

    *Example:*
    ```csharp
        customerName
        isYourBirthday
    ```
    Reference: [CamelCase, Wikipedia](https://en.wikipedia.org/wiki/CamelCase)


- **帕斯卡命名法 (Pascal Case)**  
    一種標示 識別子(Identifier) 的命名規則。  
    各單字之間不以空格斷開或連接號（-）、底線（_）連結，每個單字的首字母用大寫字母其餘字母為小寫。

    *Example:*
    ```csharp
        CustomerName
        IsYourBirthday
    ```
    Reference: [PascalCase, Wikipedia](https://en.wikipedia.org/wiki/PascalCase)

- **匈牙利命名法 (Hungarian Notation) **  
    一種標示 識別子(Identifier) 的命名規則。  
    由一個或多個小寫字母開始，這些字母用來表示特定類型(Type)或用途，而後再連接真正名稱，字母形式可以是帕斯卡命名法或其他。

    Reference: [Hungarian notation, Wikipedia](https://en.wikipedia.org/wiki/Hungarian_notation)


- **魔術數字 (Magic Number)**  
    任意的數值用於計算式(Expression)中或作為一變數的初始值，而無法令人了解其明確意義，稱之為魔術數字。

    *Example:*
    ```csharp
        sCustomerName
        dateIsYourBirthday
    ```

    Reference: [Magic number (programming), Wikipedia](https://en.wikipedia.org/wiki/Magic_number_(programming))


- **字面量 (Literal)**  
    用特定的符號或文字來指示特定 **型別(Type)** 與其 **值(Value)** 的表示法。

    *Example:*
    ```csharp
        var numberVar = 1985; // numberVar is a int and equals 1985.
        var booleanVar = true; // booleanVar is a bool and equals true.
        var ulongVar = 1000UL; // ulongVar is a ulong and equals 1000.
        var stringVar = "this is a string"; // stringVar is a string and equals "this is a string".
    ```


- **欄位 (Field)**  
    定義於類別中的一變數。


- **屬性 (Property)**  
    可透過 `get` 以及 `set` 指示詞，封裝邏輯層，取得或設定一數值。


- **特性 (Attribute)**  
    繼承 `System.Attribute` 的一類別，可用以標示與描述類別、欄位、屬性等其特定之特性，類似 Metadata 的概念。  
    常被翻譯為**屬性**，本文使用**特性**稱之，以與 **屬性 (Property)** 區隔。


1.3 References
--------------
本文參考、引用、並基於以下文章為基礎來編寫：
- https://weblogs.asp.net/lhunt/csharp-coding-standards
- https://msdn.microsoft.com/zh-tw/library/ms229042(v=vs.100).aspx
- https://github.com/dennisdoomen/CSharpGuidelines
