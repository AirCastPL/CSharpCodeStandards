6. Language Usage
===============

6.1 General
-----------
- **不要** 省略**存取修飾子 (Access Modifiers)**。明確使用適當的存取修飾子來定義所有的識別子(Identifiers)其存取性，而非使用預設模式。
    - 在 class 與在 interface 等之預設值皆不同。
    - 明確定義，減少人為誤判。
    
    ```csharp
        // **BAD**
        Void WriteEvent(string message)
        {…}
        
        // **GOOD**
        private Void WriteEvent(string message)
        {…}
    ```
    
    ```csharp
        // **BAD**
        ILogger Logger { get; set; }
        
        // **GOOD**
        public ILogger Logger { get; set; }
    ```


- **避免** 使用 `unsafe` 程式碼，若因特別因素考量使用，則盡可能獨立放置一特別專案中。
    - 減少 Memory Leak 或 Buffer Overflow 可能。
    - 獨立專案可以區分權責，當有錯誤發生時容易追查。
    - 通常只有底層才會需要使用 `unsafe` 程式碼。

- **避免** 組件(Assemblies) 交互參考。
    - 錯誤的相依性。
    - 混亂的建置順序。


6.2 Variables & Types
---------------------
- **嘗試** 於定義變數時一併初始化它 (給定值)。

- **總是** 選擇使用必要的、最簡單的資料型別、清單或物件。
    - 最小化需求。

- **嘗試** 於定義 識別子(Identifiers) 型別時，使用 介面型別 代取 實際型別。
    - 最大化彈性。
    
    ```csharp
        // **BAD**
        public Logger Logger { get; set; }
        
        // **GOOD**
        public ILogger Logger { get; set; }
    ```


- **總是** 使用 C# 內建型別別稱取代 .NET 型別。
    - 減少記憶型別。
    - 減少人為錯誤。
    
    ```csharp
        // **BAD**
        public Int32 Index { get; set; }
        
        // **GOOD**
        public int Index { get; set; }
    ```

    ```csharp
        // **BAD**
        protected String ErrorMessage { get; private set; }
        
        // **GOOD**
        protected string ErrorMessage { get; private set; }
    ```


- 嘗試 優先選擇 `int` 型別來存取任何非分數的數值 (且其定義域需與 `int` 數值相符)，即使為一正整數。
    + 當數值可能會大於 `int` 的定義域時，使用 `long` 型別。

- 嘗試 優先選擇 `double` 型別來存取分數數值，以確保計算小數點時的精度。

- **避免** 使用 `float` 型別，除非你完全理解其計算方式與影響。
    + 而使用 `float` 型別存取的變數，將不會符合 `double` 及 `decimal` 型別。

- 嘗試 使用 `decimal` 型別來存取須四捨五入至固定精度位數的分數值。常用於金錢方面。

- **避免** 使用 `sbyte`、`short`、`uint`、`ulong` 等型別。
    + 除 為叫用原生函式庫，與其相容 外。

- Avoid specifying the type for an enum - use the default of int unless you have an explicit need for long (very uncommon).
- 避免在enum使用特殊型別，使用預設的int，除非你必須使用long

- **避免** 使用 魔術數字(Magic Number)。使用 常數 (Constant) 或 列舉 (Enum) 取代。

- Avoid declaring string literals inline. Instead use Resources, Constants, Configuration Files, Registry or other data sources.
- 避免在函式中宣告內嵌式字串變數，使用Resource、Constants、Configuration Files、Registry 或其他data source

- Declare readonly or static readonly variables instead of constants for complex types.
- 使用readonly或static readonly來宣告複雜的型別

- Only declare constants for simple types.
- 使用Constants來宣告簡單型別

- Avoid direct casts. Instead, use the “as” operator and check for null.
- 避免直接轉型，使用 as 來轉型，並檢查是否為null
    ```csharp
        // Example
        object dataObject = LoadData();
        DataSet ds = dataObject as DataSet;
        if(ds != null)
        {…}
    ```


- **避免** 實值型別發生 boxing 與 unboxing。
    ```csharp
        // **BAD**
        int count = 1;
        object refCount = count;  // Implicitly boxed.
        int newCount = (int)refCount; // Explicitly unboxed.
    ```



- Try to use the “@” prefix for string literals instead of escaped strings.
- 在字串變數中，使用@取代逃逸字元

- 使用 `string.Format()` 與 `StringBulider` 來串接字串。
  
- 使用 `string.IsNullOrEmpty()` 來檢查字串是否有值。

- 避免字串隱性配置，使用String.Compare() 來判別大小寫    
- Avoid hidden string allocations within a loop. Use `string.Compare()` for case-sensitive
    
    ```csharp
        // **BAD**
        var id = -1;
        var name = “lance hunt”;
        for(int i=0; i < customerList.Count; i++)
        {
            if(customerList[i].Name. ToLower() == name)
            {
                id = customerList[i].ID;
            }
        }
        
        // **GOOD**
        var id = -1;
        var name = “lance hunt”;
        for(int i = 0; i < customerList.Count; i++)
        {
            // The “ignoreCase = true” argument performs a
            // case-insensitive compare without new allocation.
            if(string.Compare(customerList[i].Name, name,  true) == 0)
            {
                id = customerList[i].ID;
            }
        }
    ```





Enum 
Add the FlagsAttribute to bit-mask multiple options. 






Generics
--------
- Always prefer C# Generic collection types over standard or strong-typed collections.
- 優先考慮泛型類別


Inferring Types
---------------

Dynamic Types
-------------

Flow Control
------------

- Avoid invoking methods within a conditional expression.
- 條件判斷式避免使用Methods

- Avoid creating recursive methods. Use loops or nested loops instead.
- 避免使用遞迴，使用迴圈

- Avoid using foreach to iterate over immutable value-type collections. E.g. String arrays.
- 避免使用foreach在實值型別的集合

- Do not modify enumerated items within a foreach statement.
- 在foreach陳述式中，不要修改列舉的項目

- Use the ternary conditional operator only for trivial conditions. Avoid complex or compound ternary operations.
- 使用三元運算式，但是避免綜合多個三元運算式使用
   
    ```csharp
        // Example
        var result = isValid ? 9 : 4;
    ```


- Avoid evaluating Boolean conditions against true or false.
- 避免解析true 或 false 在if條件式
   
    ```csharp
        // **BAD**
        if (isValid == true)
        {…}
        
        // **GOOD**
        if (isValid)
        {…}
    ```


- Avoid assignment within conditional statements.
- 避免在if條件式中給予變數值

    ```csharp
        // Example:
        if((i=2)==2) {…}
    ```


- Avoid compound conditional expressions – use Boolean variables to split parts into multiple manageable expressions.
- 避免在if條件式使用太複雜的判斷式，使用boolean變數，將他們分成好管理的陳述式

    ```csharp
        // **BAD**
        if (((value > _highScore) && (value != _highScore)) && (value < _maxScore))
        {…}
        
        // **GOOD**
        var isHighScore = (value >= _highScore);
        var isTiedHigh = (value == _highScore);
        var isValid = (value < _maxValue);
        if ((isHighScore && ! isTiedHigh) && isValid)
        {…}
    ```


- Avoid explicit Boolean tests in conditionals.
   
    ```csharp
        // **BAD**
        if(IsValid == true)
        {…};
        
        // **GOOD**
        if(IsValid)
        {…}
    ```

- Only use switch/case statements for simple operations with parallel conditional logic.
- 只有在簡單的運算中考慮使用switch/case

- Prefer nested if/else over switch/case for short conditional sequences and complex conditions.
- 優先考慮使用 if else 條件式

- Prefer polymorphism over switch/case to encapsulate and delegate complex operations.


Exceptions
----------
- Do not use try/catch blocks for flow-control.
- 不要使用try/catch 來做流程控制

- Only catch exceptions that you can handle.
- 只catch可以處理的例外

- Never declare an empty catch block.
- 不要建立一個空的catch區塊

- Avoid nesting a try/catch within a catch block.
- 避免在catch區塊中建立巢狀的try/catch

- Always catch the most derived exception via exception filters.
- 盡量利用衍生的Exception來篩選catch明確的exception

- Order exception filters from most to least derived exception type.
- 篩選Exception順序從最高級的到最低的。

- Avoid re-throwing an exception. Allow it to bubble-up instead.
- 避免再丟出Exception

- If re-throwing an exception, preserve the original call stack by omitting the exception argument from the throw statement.
- 如果再丟出Exception,忽略exception參數可以維持原本的call stack。

    ```csharp
        // Bad!
        catch(Exception ex)
        {
            Log(ex);
            throw ex;
        }
        
        // Good!
        catch(Exception ex)
        {
            Log(ex);
            throw;
        }
    ```


- Only use the finally block to release resources from a try statement.
- finally區塊只用來釋放try區塊使用的資源

- Always use validation to avoid exceptions.
- 盡量用驗證，避免exception

    ```csharp
        // Bad!
        try
        {
            conn.Close();
        }
        Catch(Exception ex)
        {
            // handle exception if already closed!
        }
        
        // Good!
        if(conn.State != ConnectionState.Closed)
        {
            conn.Close();
        }
    ```


- Always set the innerException property on thrown exceptions so the exception chain & call stack are maintained.
- 盡可能設定innerException,如此可維持exception chain & call stack

- Avoid defining custom exception classes. Use existing exception classes instead.
- 避免定義客制的Exception,盡量使用現存的Excepiton取代

- When a custom exception is required;
- 當客制的Excepiton是必須時。
    a. Always derive from Exception not ApplicationException.
    a. 繼承Exception 而不是ApplicationException

    b. Always suffix exception class names with the word “Exception”.
    b. 類別名稱使用”Exception”當後綴詞

    c. Always add the SerializableAttribute to exception classes.
    c. 必須加入serialzableAttribute

    d. Always implement the standard “Exception Constructor Pattern”:
    d. 必須實作標準的建構式

    ```csharp
        public MyCustomException ();
        public MyCustomException (string message);
        public MyCustomException (string message, Exception innerException);
    ```


    e. Always implement the deserialization constructor:
    e. 必須實作反序列化的建構式

    ```csharp
        protected MyCustomException(SerializationInfo info, StreamingContext contxt);
    ```


- Always set the appropriate HResult value on custom exception classes.
- 客制的Exception請給定適當的HResult

    (Note: the ApplicationException HResult = -2146232832)

-  When defining custom exception classes that contain additional properties:
- 當定義客制Excepiton時，需注意以下屬性
    a. Always override the Message property, ToString() method and the implicit operator string to include custom property values.
    a. override Message(property) ToString()(method) implicit operator string

    b. Always modify the deserialization constructor to retrieve custom property values.
    b. 必須修改反序例化的建構式，這樣才能取回客制的屬性值

    c. Always override the GetObjectData(…) method to add custom properties to the serialization collection.
    c. 必須覆寫GetObjectData(…)加入客制的屬性到序列化的集合

    ```csharp
        public override void GetObjectData(SerializationInfo info,
        StreamingContext context)
        {
            base.GetObjectData (info, context);
            info.AddValue("MyValue", _myValue);
        }
    ```


Events
------
- Always check Event & Delegate instances for null before invoking.
- 在執行前先確認實體是否是null

- Use the default EventHandler and EventArgs for most simple events.
- 大多數簡單情況，使用預設的EventHandler/EventArgs

- Always derive a custom EventArgs class to provide additional data.
- 繼承EventArgs來客制額外需要的資料

- Use the existing CancelEventArgs class to allow the event subscriber to control events.
- 使用現存的CancelEventArgs來讓事件訂閱者控制事件


Anonymous Classes
-----------------


Anonymous Methods, Delegates & Lambda Expressions
-------------------------------------------------



The yield statement
-------------------


Threading
---------
- Always use the “lock” keyword instead of the Monitor type.
- 使用“lock”取代Monitor類別

- Only lock on a private or private static object.
- 只lock private 或private static物件

    ```csharp
        Example: lock(myVariable);
    ```


- Avoid locking on a Type.
- 避免lock Type

    ```csharp
        Example: lock(typeof(MyClass));
    ```


- Avoid locking on the current object instance.
- 避免lock目前的實體

    ```csharp
        Example: lock(this);
    ```


Task Parallel Library
---------------------


Reflection
----------

Testing
-------


```csharp
    // Microsoft.VisualStudio.TestTools.UnitTesting.Assert
    public static void AreEqual<T>(T expected, T actual)
```

```csharp
    // NUnit.Framework.Assert
    public static void AreEqual(object expected, object actual)
```

```csharp
    // Xunit.Assert
    public static void Equal<T>(T expected, T actual)
```













Excluded
---------
- ~~Floating point values should include at least one digit before the decimal place and one after.~~
- ~~Never concatenate strings inside a loop.~~
- ~~Always explicitly initialize arrays of reference types using a for loop.~~
