5. Language Usage
===============

5.1 General
-----------
- **請勿** 省略**存取修飾子 (Access Modifiers)**。明確使用適當的存取修飾子來定義所有的識別子(Identifiers)其存取性，而非使用預設模式。
    - 在 class 與在 interface 等等之預設值皆不同。
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
    
    ```csharp
        // **BAD**
        public Logger Logger { get; set; }
        
        // **GOOD**
        public ILogger Logger { get; set; }
    ```

- **總是** 使用 C# 內建型別取代 .NET 基礎型別
    - 減少記憶型別
    - 減少人為錯誤
    
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
    
    ```csharp
        // Example
        object dataObject = LoadData();
        DataSet ds = dataObject as DataSet;
        if(ds != null)
        {…}
    ```

- Always explicitly initialize arrays of reference types using a for loop.

- Avoid boxing and unboxing value types.
    
    ```csharp
        // Example
        int count = 1;
        object refCount = count;  // Implicitly boxed.
        int newCount = (int)refCount; // Explicitly unboxed.
    ```

- Floating point values should include at least one digit before the decimal place and one after.
    
    ```csharp
        // Example
        var totalPercent = 0.05;
    ```

- Try to use the “@” prefix for string literals instead of escaped strings.

- Prefer 'string.Format()' or 'StringBuilder' over string concatenation.

- Never concatenate strings inside a loop.

- ~~Do not compare strings to `string.Empty` or '“”' to check for empty strings. Instead, compare by using `string.Length == 0'.~~

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

Generics
--------
- Always prefer C# Generic collection types over standard or strong-typed collections.


Inferring Types
---------------

Dynamic Types
-------------

Flow Control
------------
- Avoid invoking methods within a conditional expression.
- Avoid creating recursive methods. Use loops or nested loops instead.
- Avoid using foreach to iterate over immutable value-type collections. E.g. String arrays.
- Do not modify enumerated items within a foreach statement.
- Use the ternary conditional operator only for trivial conditions. Avoid complex or compound ternary operations.
   
    ```csharp
        // Example
        var result = isValid ? 9 : 4;
    ```

- Avoid evaluating Boolean conditions against true or false.
   
    ```csharp
        // **BAD**
        if (isValid == true)
        {…}
        
        // **GOOD**
        if (isValid)
        {…}
    ```

- Avoid assignment within conditional statements.
   
    ```csharp
        // Example:
        if((i=2)==2) {…}
    ```

- Avoid compound conditional expressions – use Boolean variables to split parts into multiple manageable expressions.
   
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

- Prefer nested if/else over switch/case for short conditional sequences and complex conditions.

- Prefer polymorphism over switch/case to encapsulate and delegate complex operations.


Exceptions
----------
- Do not use try/catch blocks for flow-control.
- Only catch exceptions that you can handle.
- Never declare an empty catch block.
- Avoid nesting a try/catch within a catch block.
- Always catch the most derived exception via exception filters.
- Order exception filters from most to least derived exception type.
- Avoid re-throwing an exception. Allow it to bubble-up instead.
- If re-throwing an exception, preserve the original call stack by omitting the exception argument from the throw statement.

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

- Always use validation to avoid exceptions.

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
- Avoid defining custom exception classes. Use existing exception classes instead.
- When a custom exception is required;
    a.  Always derive from Exception not ApplicationException.
    b.  Always suffix exception class names with the word “Exception”.
    c.  Always add the SerializableAttribute to exception classes.
    d.  Always implement the standard “Exception Constructor Pattern”:

    ```csharp
        public MyCustomException ();
        public MyCustomException (string message);
        public MyCustomException (string message, Exception innerException);
    ```

    e.  Always implement the deserialization constructor:

    ```csharp
        protected MyCustomException(SerializationInfo info, StreamingContext contxt);
    ```

- Always set the appropriate HResult value on custom exception classes.

    (Note: the ApplicationException HResult = -2146232832)

-  When defining custom exception classes that contain additional properties:
    a.  Always override the Message property, ToString() method and the implicit operator string to include custom property values.
    b.  Always modify the deserialization constructor to retrieve custom property values.
    c.  Always override the GetObjectData(…) method to add custom properties to the serialization collection.


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
- Use the default EventHandler and EventArgs for most simple events.
- Always derive a custom EventArgs class to provide additional data.
- Use the existing CancelEventArgs class to allow the event subscriber to control events.

Anonymous Classes
-----------------


Anonymous Methods, Delegates & Lambda Expressions
-------------------------------------------------



The yield statement
-------------------


Threading
---------
- Always use the “lock” keyword instead of the Monitor type.
- Only lock on a private or private static object.

    ```csharp
		Example: lock(myVariable);
    ```

- Avoid locking on a Type.

    ```csharp
		Example: lock(typeof(MyClass));
    ```

- Avoid locking on the current object instance.

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
