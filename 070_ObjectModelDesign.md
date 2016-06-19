7. Object Model Design
======================

General
-------
- **總是** 將 **欄位(Fields)** 其存取性宣告為 **private**；而 **屬性(Properties)** 則用 **public**、**protected**、**internal** 或 **protected internal** 來宣告。
    - 屬性常用於封裝欄位，成為公開介面。
    - 屬性是可以繼承，而欄位不能。


- 明確的指定 namespace，不要使用預設 `global` namespace。

- Avoid overuse of the public access modifier. Typically fewer than 10% of your types and members will be part of a public API, unless you are writing a class library.
- 避免濫用public修飾詞.一般來說應該少於10%。

- Consider using internal or private access modifiers for types and members unless you intend to support them as part of a public API.
- 優先考慮使用 `internal` 或 `private` 修飾詞。

- Never use the protected access modifier within sealed classes unless overriding a protected member of an inherited type.
- 在 `sealed` 類別，不要使用 `protected`。除非是可繼承的類別


- 方法避免使用超過5個參數.若超過,考慮重構它吧。

- Try to replace large parameter-sets (> than 5 parameters) with one or more class or struct parameters – especially when used in multiple method signatures.
- 試著使用class或struct取代大量參數.尤其是在多個方法簽名都會使用情況下。

- 不要使用 `new` 來隱藏衍生類別的成員。


- Only use the “base” keyword when invoking a base class constructor or base implementation within an override.
- 只在建構式或覆寫時，使用”base”關鍵字。

- Consider using method overloading instead of the params attribute (but be careful not to break CLS Compliance of your API’s).
- 考慮使用方法多載取代”params”。

- Always validate an enumeration variable or parameter value before consuming it. They may contain any value that the underlying Enum type (default int) supports.
- 在使用列舉變數或參數前，必須先驗證列舉是否定義。有可能是Enum的基底的型別(預設是int)。

        // Example
        public void Test(BookCategory cat)
        {
        if (Enum.IsDefined(typeof(BookCategory), cat))
        {…}
        }

- 考慮覆寫 struct 的Equals()方法。

- 當覆寫Equals()方法時，必須覆寫Equality Operator (==)。

- 當覆寫ToString()方法時，必須覆寫String Implicit Operator。

- 當類別有提供Close() or Dispose()時，請呼叫它。

- Wrap instantiation of IDisposable objects with a “using” statement to ensure that Dispose() is automatically called.
- 用”using”來包裝IDisposable介面來確保Dispose()會被自動呼叫。

        // Example
        using(SqlConnection cn = new SqlConnection(_connectionString))
        {…}

- 實作IDisposable介面當類別有參考外部資源時。

- 避免實作Finalizer，不要定義Finalize(),而是使用C#解構式。

- 優先使用聚合而非繼承。

- 避免 '(過早抽象) Premature Generalization'。當清楚意圖時，再建立抽象。

- 使用最簡單的方法，當需要時再重構。

- Always make object-behavior transparent to API consumers.
- 必須讓使用者清楚物件具備的行為。

- 在屬性、方法、建構式執行時，避免非預期的副作用。

- 將呈現層和商業邏輯層明確分開。

- 優先使用介面而不是抽象類別。

- 使用設計模式的名稱 `Bridge`、`Adapter` 或 `Factory` 來作為類別的後綴詞。

- Only make members virtual if they are designed and tested for extensibility.
- 只有在需要擴充時才使用 `virtual`。

- 經常重構！





Enum 
Add the FlagsAttribute to bit-mask multiple options. 


Attributes
----------

Exceptions
----------

Generics
--------

Co- and Contra-variance
-----------------------

Events
------

Delegate
--------


Partial Classes
---------------

Extension Methods
-----------------
