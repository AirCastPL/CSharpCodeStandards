5. Language Usage
===============

5.1 General
-----------
- **請勿** 省略**存取修飾子 (Access Modifiers)**。明確使用適當的存取修飾子來定義所有的識別子(Identifiers)其存取性，而非使用預設模式。
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

- ~~Do not use the default (“1.0.*”) versioning scheme. Increment the AssemblyVersionAttribute value manually.~~

- ~~Set the ComVisibleAttribute to false for all assemblies.~~

- ~~Only selectively enable the ComVisibleAttribute for individual classes when needed.~~

- **避免** 使用 unsafe 程式碼，若因特別因素考量使用，則盡可能獨立放置一特別專案中。
    - 減少 Memory Leak 或 Buffer Overflow 可能。
    - 獨立專案可以區分權責，當有錯誤發生時容易追查。
    - 通常只有底層才會需要使用 unsafe 程式碼。

- **避免** 組件(Assemblies) 交互參考。
    - 錯誤的相依性。
    - 混亂的建置順序。

5.2 Variables & Types
---------------------
- ~~Try to initialize variables where you declare them.~~

- **總是** 只使用必要的、夠簡單的資料型別、清單或物件。
    - 最小化需求

- **盡可能** 於定義識別子(Identifiers)型別時，使用介面型別代取實際型別。
    - 最大化彈性
    
    // **BAD**
    public **Logger** Logger { get; set; }
    
    // **GOOD**
    public **ILogger** Logger { get; set; }

- **總是** 使用 C# 內建型別取代 .NET 基礎型別
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
    
- Try to use int for any non-fractional numeric values that will fit the int datatype - even variables for non-negative numbers.
- Only use long for variables potentially containing values too large for an int.
- Try to use double for fractional numbers to ensure decimal precision in calculations.
- Only use float for fractional numbers that will not fit double or decimal.
- Avoid using float unless you fully understand the implications upon any calculations.
- Try to use decimal when fractional numbers must be rounded to a fixed precision for calculations. Typically this will involve money.
- Avoid using sbyte, short, uint, and ulong unless it is for interop (P/Invoke) with native libraries.
- Avoid specifying the type for an enum - use the default of int unless you have an explicit need for long (very uncommon).
- Avoid using inline numeric literals (magic numbers). Instead, use a Constant or Enum.
- Avoid declaring string literals inline. Instead use Resources, Constants, Configuration Files, Registry or other data sources.
- Declare readonly or static readonly variables instead of constants for complex types.
- Only declare constants for simple types.
- Avoid direct casts. Instead, use the “as” operator and check for null.

    Example:
    object dataObject = LoadData();
    DataSet ds = dataObject as DataSet;
    if(ds != null)
    {…}

- Always explicitly initialize arrays of reference types using a for loop.
- Avoid boxing and unboxing value types.

    Example:
    int count = 1;
    object refCount = count;  // Implicitly boxed.
    int newCount = (int)refCount; // Explicitly unboxed.

- Floating point values should include at least one digit before the decimal place and one after.

    Example: totalPercent = 0.05;

- Try to use the “@” prefix for string literals instead of escaped strings.
- Prefer String.Format() or StringBuilder over string concatenation.
- Never concatenate strings inside a loop.
- ~~Do not compare strings to `string.Empty` or “” to check for empty strings. Instead, compare by using `string.Length` == 0.~~

- Avoid hidden string allocations within a loop. Use `string.Compare()` for case-sensitive

    Example:
    (ToLower() creates a temp string)

Generics
--------
- Always prefer C# Generic collection types over standard or strong-typed collections.


Inferring Types
---------------

Dynamic Types
-------------

Flow Control
------------

Anonymous Objects
-----------------

Anonymous Methods
-----------------

Lambda Expressions
------------------



The yield statement
-------------------


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
