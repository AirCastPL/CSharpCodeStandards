6. Language Usage
===============
以下章節將討論 C# 語言的特性應該如何有效的使用，限制部分可能被誤用的功能。而合理的功能限縮使用也是提高程式碼一致性的方法之一。

6.1 General
-----------
- **不要** 省略**存取修飾子 (Access Modifiers)**。明確使用適當的存取修飾子來定義所有的識別子(Identifiers)其存取性，而非使用預設模式。
    + 在 class 與在 interface 等之預設值皆不同。
    + 明確定義，減少人為誤判。
    
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
    + 減少 Memory Leak 或 Buffer Overflow 可能。
    + 獨立專案可以區分權責，當有錯誤發生時容易追查。
    + 通常只有底層才會需要使用 `unsafe` 程式碼。

- **避免** 組件(Assemblies) 交互參考。
    + 錯誤的相依性。
    + 混亂的建置順序。

- **不要** 使用 `using static` 指示詞。
    + 除 用於避免 擴充方法(Extension Method) 衝突 外。


6.2 Variables & Types
---------------------
- **嘗試** 使用 `this` 和 `base` 等 存取關鍵字(Access Keywords) 於型別中叫用成員，而非直接叫用。

- **嘗試** 於定義變數時一併初始化它 (給定值)。

- **總是** 選擇使用必要的、最簡單的資料型別、清單或物件。
    + 最小化需求。

- **嘗試** 於定義 識別子(Identifiers) 型別時，使用 介面型別 代取 實際型別。
    + 最大化彈性。
    
    ```csharp
        // **BAD**
        public Logger Logger { get; set; }
        
        // **GOOD**
        public ILogger Logger { get; set; }
    ```


- **總是** 使用 C# 內建型別別稱取代 .NET 型別。
    + 減少記憶型別。
    + 減少人為錯誤。
    
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


- **嘗試** 優先選擇 `int` 型別來存取任何非分數的數值 (且其定義域需與 `int` 數值相符)，即使為一正整數。
    + 當數值可能會大於 `int` 的定義域時，使用 `long` 型別。

- **嘗試** 優先選擇 `double` 型別來存取分數數值，以確保計算小數點時的精度。

- **避免** 使用 `float` 型別，除非你完全理解其計算方式與影響。
    + 而使用 `float` 型別存取的變數，將不會符合 `double` 及 `decimal` 型別。

- **嘗試** 使用 `decimal` 型別來存取須四捨五入至固定精度位數的分數值。常用於金錢方面。

- **避免** 使用 `sbyte`、`short`、`uint`、`ulong` 等型別。
    + 除 為叫用原生函式庫，與其相容 外。

- **避免** 將 列舉(Enum) 設為特殊的型別，使用預設的 int 型別。
    + 不需特別於程式中指定 int 型別。
    + 除 特殊需求使用到 long 型別 外。

- **避免** 使用 魔術數字(Magic Number)。
    + 使用 常數(Constants) 或 列舉(Enums) 取代。

- **減少** 宣告字串變數時直接給定字串內容。
    + 使用 資源檔(Resource)、常數(Constants)、設定檔(Configuration Files)、註冊表(Registry) 或由其他資料來源取得。

- 使用 `readonly` 或 `static readonly` 欄位來宣告較複雜的資料型別，替代常數。
    + 常數(Constants) 無法使用 `new` 初始化物件。
    + `readonly` 或 `static readonly` 欄位所儲存的資料是執行時期的定值。

- 使用 常數(Constants) 來宣告簡單的資料型別。
    + 常數 是一種欄位，其值是在編譯時期設定並且不能變更。
    + 常數 可提供有意義的名稱，用來取代意義不明的魔術數字或其他定值。

- 使用 `as` 運算子(Operator) 取代直接轉型，並檢查結果是否為 `null`。
    ```csharp
        // **BAD**
        object dataObject = LoadData();
        var ds = (DataSet)dataObject;
        …

        // **GOOD**
        object dataObject = LoadData();
        var ds = dataObject as DataSet;
        if (ds != null)
        {…}
    ```


- **避免** 實值型別發生 Boxing 與 Unboxing。
    + 嘗試使用 泛型 替代 `object` 型別的使用。

    ```csharp
        // **BAD**
        int count = 1;
        object refCount = count;  // Implicitly boxed.
        int newCount = (int)refCount; // Explicitly unboxed.
    ```


- 使用 `string.IsNullOrEmpty(str)` 或 `str.Length == 0` 來檢查字串是否有值。
    + **不要** 使用 `str == string.Empty` 來檢查。

- 嘗試 於 字串字面量(String Literals) 前加上 "`@`" 符號，來代取使用逃逸字元。
    + 關於 C# 的逃逸字元可參考：[Escaping in C#: characters, strings, string formats, keywords, identifiers](http://www.codeproject.com/Articles/371232/Escaping-in-Csharp-characters-strings-string-forma)。

    ```csharp
        // **BAD**
        var path1    = "\\\\server\\share\\file.txt";  // \\server\share\file.txt
        var message1 = "Joe said \"Hello\" to me";     // Joe said "Hello" to me

        // **GOOD**
        var path2    = @"\\server\share\file.txt";     // \\server\share\file.txt
        var message2 = @"Joe said ""Hello"" to me";    // Joe said "Hello" to me
    ```


- 使用 字串插值(String Interpolation)、`string.Format()` 和 `StringBulider` 來串接字串。
  
- **避免** 在 字串插值(String Interpolation) 中使用運算式或叫用函式。
    + 可使用變數、屬性、欄位。

    ```csharp
        // **BAD**
        var message = $"{webManager.GetPage(pageIndex).Name} throw an exception.";

        // **GOOD**
        var page = webManager.GetPage(pageIndex);
        var message = $"{page.Name} throw an exception.";
    ```

- **嘗試** 使用 `string.Compare()` 與 `string.Equals()` 來比對兩字串是否相等。
    + 可消除大小寫之差異。
    + **避免** 使用 `==` 運算子(Operator) 來比對字串。

    ```csharp
        // **BAD**
        if (str1 == str2)
        {…}

        // **GOOD**
        if (string.Compare(str1, str2, true) == 0)
        {…}

        // **GOOD**
        if (string.Equals(str1, str2, CultureInfo.InvariantCulture))
        {…}

        // **GOOD**
        if (str1.Equals(str2, CultureInfo.InvariantCulture))
        {…}
    ```

- **嘗試** 使用 `using` 陳述式 來宣告繼承 `IDisposable` 介面的變數。
    - 系統會在使用完畢後自動叫用 `IDisposable.Dispose()` 函式。


6.3 Generics & LINQ
-------------------
- **總是** 優先考慮使用泛型的集合型別取代 一般集合型別 或 強集合型別。

- **減少** 使用 `IEnumerable` 型別，除非能完全了解 延遲執行(Delayed Execution) 所產生的邊際效益。
    + 使用 `T[]` 或 `IList<T>` 取代。

- **不要** 使用 LINQ 的 查詢語法(Query Syntax)，使用 函式語法(Method Syntax) 代替。
    ```csharp
        // **BAD**
        // Query syntax:
        var numQuery1 = 
            from num in numbers
            where num % 2 == 0
            orderby num
            select num;
        
        // **GOOD**
        // Method syntax:
        var numQuery2 = numbers
            .Where(num => num % 2 == 0)
            .OrderBy(n => n);
    ```

- **嘗試** 於確定 LINQ 已完成查詢後，使用 `ToArray()` 或 `ToList()` 函式強制執行查詢。 


6.4 Flow Control
----------------
- **避免** 於 選擇陳述式(Selection Statements) 及 反覆運算陳述式(Iteration Statements) 中使用複雜的 運算式 和 函式叫用。

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


- **不要** 於 選擇陳述式(Selection Statements) 及 反覆運算陳述式(Iteration Statements) 中使用 LINQ 查詢表達式(Query Expression)。

- **避免** 使用遞迴，使用迴圈或巢狀迴圈代替。

- **不要** 在 `foreach` 區段中 中修改集合內容，比如新增或刪除項目。

- **不要** 串接多個 三元運算式(Ternary Conditional Operator)。
    ```csharp
        // **BAD**
        var result = isValid1 ? isValid2 ? 1 : isValid3 ? 2 : 3 : 4;
    ```


- **不要** 於陳述式中 將一 `bool` 型別的變數或運算式結果 再與 `true`、`false` 比對。 
    ```csharp
        // **BAD**
        if (isValid == true)
        {…}
        
        // **GOOD**
        if (isValid)
        {…}
    ```
   
    ```csharp
        // **BAD**
        if ((age > 10) == true)
        {…}
        
        // **GOOD**
        if (age > 10)
        {…}
    ```


- **避免** 在 選擇陳述式(Selection Statements) 中指定數值給變數。
    ```csharp
        // **BAD**
        if ((i = 2) + j == 2)
        {…}
    ```
    ```csharp
        // **BAD**
        switch (type = User.GetType())
        {…}
    ```


- 面對 複雜的判斷式 或 多個簡短的判斷式 應優先考慮使用 `if`/`else` 而非 `switch`/`case`。

- 當使用 `switch`/`case` 時，應考量是否可能重構為使用多型來封裝與委派運算。


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


Anonymous Types
---------------


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
- ~~Avoid using foreach to iterate over immutable value-type collections. E.g. String arrays.~~
- ~~Only use switch/case statements for simple operations with parallel conditional logic.~~