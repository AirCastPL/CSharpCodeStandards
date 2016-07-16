7. Object Model Design
======================

General
-------
- **總是** 將 **欄位(Fields)** 其存取性宣告為 **private**；而 **屬性(Properties)** 則用 **public**、**protected**、**internal** 或 **protected internal** 來宣告。
    + 屬性常用於封裝欄位，成為公開介面。
    + 屬性是可以繼承，而欄位不能。

- 明確的指定命名空間，不要使用預設 `global` 命名空間。

- **避免** 濫用 `public` 修飾詞於型別或成員定義。對於一個公開的 API 來說，通常會少於10%。
    + 模型(Model) 類別例外。

- 優先考慮使用 `internal` 或 `private` 修飾詞於型別或成員定義，除非你想開放他們成為公開 API 的一部分。

- **不要** 在 `sealed` 類別中使用 `protected` 修飾詞。除非是由父類別繼承來的。

- **避免** 函式超過 5 個參數。若超過，請考慮重構它吧。

- 試著使用一個或多個 類別 或 結構 來取代大量參數，尤其是會用於多個 函式簽名(Method Signature) 中的情況下。

- **不要** 使用 `new` 來隱藏衍生類別的成員。

- 只在叫用 父類別建構式 或 父類別實作 時，使用 `base` 關鍵字。

- ~~Consider using method overloading instead of the params attribute (but be careful not to break CLS Compliance of your API’s).~~
- ~~考慮使用方法多載取代”params”。~~

- Always validate an enumeration variable or parameter value before consuming it. They may contain any value that the underlying Enum type (default int) supports.
- 在使用列舉變數或參數前，必須先驗證列舉是否定義。有可能是Enum的基底的型別(預設是int)。

        // Example
        public void Test(BookCategory cat)
        {
        if (Enum.IsDefined(typeof(BookCategory), cat))
        {…}
        }

- 考慮覆寫 結構 的 `Equals()` 函式。

- 當覆寫 `Equals()` 函式時，必須覆寫 等號運算子(Equality Operator, ==)。

- 當覆寫 `ToString()` 函式時，必須覆寫 字串隱性轉型運算子(String Implicit Operator)。

- 當類別有提供 `Close()` / `Dispose()` 時，請使用它。

- 使用 `using` 陳述式來初始、設定一實作 `IDisposable` 介面的物件，以確保物件使用完畢後 `Dispose()` 函式會被自動呼叫。

    ```csharp
        // **GOOD**
        using(var conn = new SqlConnection(this._connectionString))
        {…}
    ```


- 當類別有參考外部資源時，實作 `IDisposable` 介面。

- **避免** 實作 `Finalizer`，不要定義 `Finalize()` 函式，而是使用 C# 的解構式。

- 優先使用 聚合 而非 繼承。

- 避免 過早抽象(Premature Generalization)。當清楚意圖時，再建立抽象。

- 使用最簡單的方法實作，當需要時再重構。

- **總是** 讓物件的行為能清楚的被 API 使用者所了解。

- ~~在屬性、方法、建構式執行時，避免非預期的副作用。~~

- 將 呈現層 和 商業邏輯層 明確分開。

- 優先使用介面而不是抽象類別。

- 使用設計模式的名稱，如 `Bridge`、`Adapter` 或 `Factory`，來作為類別的後綴詞。

- 只有在需要擴充時才使用 `virtual`。
    + 如因設計需求或測試需求時。

- 對於需要多選(或位元遮罩運算) 的 列舉(Enum)，加上 `FlagsAttribute` 特性修飾，並指定每個成員的數值。

- 經常重構！


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
