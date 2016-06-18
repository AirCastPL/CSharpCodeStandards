5. Coding Style
===============
於程式開發者間，編寫風格是最容易產生歧異與爭執的。各開發者各有所好，鮮少有相同的。但一致性的排版、撰寫格式及程式碼組織是建立可維護性程式碼的關鍵。  
以下的章節將提出統一遵循的方針，來實作具可讀性、簡潔以及一致性的程式碼，以簡化維護作業。

5.1 Formatting
--------------
- **總是** 使用 UTF-8 做為檔案文件的編碼方式。

- **總是** 使用 `CR` + `LF` 字符做為換行符號，而非單一 `CR` 或 `LF` 字符。
    + `CR`：`0x0D`，用於 MacOS 系統。
    + `LF`：`0x0A`，用於 Unix 系統。
    + `CR` + `LF`：用於 Windows 系統。

- **不要** 使用 `Tab` 字符來縮排。以 4 個空白取代一個 `Tab` 字符。

- 自在的使用空格和換行符號來隔開與組織程式碼。
    + 適當的縮排能提高閱讀性。

- **總是** 在空行加入大括號 ("`{`"、"`}`")。
    + 除 自動屬性 (Auto-Implemented Properties) 外。
    + 除 集合初始化 (Collection initializers) 外。

- **總是** 將大括號 ("`{`"、"`}`") 中程式碼區塊縮排。

- **總是** 在條件判斷式的區段中加入大括號 ("`{`"、"`}`")。

- **總是** 使用 `var` 來宣告變數。
    + 除 編譯器無法自動推定型別 外。
    + 除 目標型別 非 來源型別 外。

    ```csharp
        // **BAD**
        User user = User.Get("Stephen Curry");
        OnlineLog log = WebManager.GetLogByUser(user);

        // **GOOD**
        var user = User.Get("Stephen Curry");
        var log = WebManager.GetLogByUser(user);

        // **GOOD**
        Func<int> randomNumberGenerator = () => new Random().Next(); 
        ILogger logger = null;
        IUser user = new Customer();
    ```


- **不要** 一次宣告多個變數，或將多個變數宣告寫在同一行。
    ```csharp
        // **BAD**
        int i, j, k = 99;
        var index = 10; var maxIndex = 1000;

        // **GOOD**
        int i;
        int j;
        var k = 99;
        var index = 10;
        var maxIndex = 1000;
    ```


- **總是** 依據下列順序排序 `using` 指示詞(Directive)：
    1. .NET Framework 的命名空間
    2. 其他的命名空間
    3. 命名空間或類別的別稱

    ```csharp
        // **BAD**
        using AirCast.Core;
        using Helper = AirCast.Data.DatabaseHelper;
        using System;
        using System.Text;

        // **GOOD**
        using System;
        using System.Text;
        using AirCast.Core;
        using Helper = AirCast.Data.DatabaseHelper;
    ```


- 依據下列次序，排序 類別(Class) 中的成員：
    1. 常數 (Constants)
    2. 欄位 (Fields)
    3. 建構式及解構式 (Constructors & Finalizers)
    4. 屬性 (Properties)
    5. 函式 (Methods)
    6. 巢狀列舉 (Nested Enums)
    7. 巢狀結構 (Nested Structs)
    7. 巢狀類別 (Nested Classes)

- 依據下列 存取修飾子(Access Modifier) 之次序，排序 宣告項目(Declarations)：
    1. `public`
    2. `internal`
    3. `internal protected`
    4. `protected`
    5. `private`

- **避免** 使用 `#region`。
    + 減少取消使用 `#region` 時造成的程式碼差異過大。
    + Visual Studio 預設為縮起內容，不好閱讀。
    + 自動產生之程式碼除外。

- **總是** 將各個 特性(Attribute) 置於不同行。
    + 除 用於 參數(Parameter) 的 特性(Attribute) 外。

    ```csharp
        // **BAD**
        [JsonProperty("name"), Required, Display(Name="User Name")]
        public string Name {get; set;}

        [JsonProperty("birthday")][Display(Name="Birthday")][DisplayFormat(DataFormatString = "{0:dd/MM/yyyy}")]
        public DateTime BirthDate {get; set;}

        // **GOOD**
        [JsonProperty("name")]
        [Required]
        [Display(Name="User Name")]
        public string Name {get; set;}

        [JsonProperty("birthday")]
        [Display(Name="Birthday")]
        [DisplayFormat(DataFormatString = "{0:dd/MM/yyyy}")]
        public DateTime BirthDate {get; set;}
    ```

- **總是** 將用於 Assembly、Type、Method、Field、Parameter 的 特性(Attribute) 放置於與宣告對象不同的一行。
    ```csharp
        // **GOOD**
        [JsonObject(MemberSerialization.OptIn)]
        public class User
        {
            public int Id {get; set;}

            [JsonProperty]
            public string Name {get; set;}

            [JsonProperty]
            [JsonConverter(typeof(JavaScriptDateTimeConverter))]
            public DateTime BirthDate {get; set;}
        }
    ```


- **總是** 將用於 參數(Parameter) 的 特性(Attribute) 放置於與其宣告對象同一行。
    ```csharp
        // **GOOD**
        public int GetMember([NotNull]string name)
        {…}
    ```
    ```csharp
        // **GOOD**
        public IEnumerable<User> UserList(
            [WithKey(nameof(User))]IProvider provider,
            [WithKey(nameof(User))]IFilter filter,
            ILogger logger)
        {…}
    ```


- 所有的註解盡量使用相同語言撰寫，且語意、文法正確並包含適當的標點符號。

- **不要** 使用 多行註解 (/* ... */)。
    + 使用 單行註解(Inline-comments)(//) 或 註解區塊(Comment-blocks) (///) 取代。

- **不要** 使用 單行註解(Inline-comments) 來解釋明顯的程式碼。
    + 良好編寫風格的程式碼具有自敘性 (Well written code is self documenting)。
    + 使用 單行註解(Inline-comments) 來解釋假設(Assumptions)、已知問題、演算法等。

- 可在 單行註解(Inline-comments) 中加入 工作清單(Task List) 的工作語彙基元 (Token) (如：TODO、UNDONE 等)，來建立工作清單註解。
    ```csharp
        // TODO: Place Database Code Here
        // UNDONE: Removed P\Invoke Call due to errors
        // HACK: Temporary fix until able to refactor
    ```


- 總是對非私用的 宣告項目(Declarations) 加上 註解區塊(Comment-blocks)。
    + 私用的宣告項目也可以附加註解區塊。

- **總是** 於 註解區塊(Comment-blocks) 中，使用 `<summary>`、`<param>`、`<returns>` 和 `<exception>` 註解區段，若所說明的程式碼包含這些部分的話。
    + 並盡可能使用 `<see cref="member"/>` 與 `<seeAlso cref="member"/>`。

- **總是** 於 註解區塊(Comment-blocks) 中，為在註解中添加的 程式碼 或 其他嵌入標記 使用 `CDATA` 標籤以避免編碼問題。
    ```csharp
        /// <example>
        /// Add the following key to the “appSettings” section of your config:
        /// <code><![CDATA[
        ///     <configuration>
        ///         <appSettings>
        ///             <add key=”mySetting” value=”myValue”/>
        ///         </appSettings>
        ///     </configuration>
        /// ]]></code>
        /// </example>
    ```


Excluded
--------
- ~~Only use comments for bad code to say “fix this code” – otherwise remove, or rewrite the code!~~
- ~~If in doubt, always err on the side of clarity and consistency.~~
- ~~Only use C# comment-blocks for documenting the API.~~
- ~~Do not “flowerbox” comment blocks.~~
- ~~Place namespace “using” statements together at the top of file. Group .NET namespaces above custom namespaces.~~
- ~~Segregate interface Implementation by using #region statements.~~
