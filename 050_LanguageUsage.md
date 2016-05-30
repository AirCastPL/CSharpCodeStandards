5. Language Usage
===============

General
-------
1. **請勿** 省略**存取修飾子 (Access Modifiers)**。明確使用適當的存取修飾子來定義所有的識別子(Identifiers)其存取性，而非使用預設模式。
    - 在 class 與在 interface 等等之預設值皆不同。
    - 明確定義，減少人為誤判。
    
    // **BAD**
    Void WriteEvent(string message)
    {…}
    
    // **GOOD**
    **private** Void WriteEvent(string message)
    {…}
    
    // **BAD**
    ILogger Logger { get; set; }
    
    // **GOOD**
    **public** ILogger Logger { get; set; }

2. **避免** 使用 unsafe 程式碼，若因特別因素考量使用，則盡可能獨立放置一特別專案中。
    - 減少 Memory Leak 或 Buffer Overflow 可能。
    - 獨立專案可以區分權責，當有錯誤發生時容易追查。
    - 通常只有底層才會需要使用 unsafe 程式碼。

3. **避免** 組件(Assemblies) 交互參考。
    - 錯誤的相依性。
    - 混亂的建置順序。

Variables & Types
-----------------
1. **總是** 只使用必要的、夠簡單的資料型別、清單或物件。
    - 最小化需求

2. **盡可能** 於定義識別子(Identifiers)型別時，使用介面型別代取實際型別。
    - 最大化彈性
    
    // **BAD**
    public **Logger** Logger { get; set; }
    
    // **GOOD**
    public **ILogger** Logger { get; set; }

3. **總是** 使用 C# 內建型別取代 .NET 基礎型別
    - 減少記憶型別
    - 減少人為錯誤
    
    // **BAD**
    public **Int32** Index { get; set; }
    
    // **GOOD**
    public **int** Index { get; set; }
    
    // **BAD**
    protected **String** ErrorMessage { get; private set; }
    
    // **GOOD**
    protected **string** ErrorMessage { get; private set; }
    
    
The yield statement
-------------------


Inferring Types
---------------

Dynamic Types
-------------

Anonymous Objects
-----------------

Anonymous Methods
-----------------

Lambda Expressions
------------------


Flow Control
------------


Reflection
----------

Threading
---------


Task Parallel Library
---------------------

Testing
-------
Microsoft.VisualStudio.TestTools.UnitTesting.Assert
public static void AreEqual<T>(T expected, T actual)

NUnit.Framework.Assert
public static void AreEqual(object expected, object actual)

Xunit.Assert
public static void Equal<T>(T expected, T actual)
