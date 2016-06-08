4. Coding Style
===============
Coding style causes the most inconsistency and controversy between developers. Each developer has a preference, and
rarely are two the same. However, consistent layout, format, and organization are key to creating maintainable code.
The following sections describe the preferred way to implement C# source code in order to create readable, clear, and
consistent code that is easy to understand and maintain.

4.1 Formatting
--------------
- 在一個檔案中不要宣告超過一個namespace

- 避免放置太多class在同一個檔案

- Always place curly braces ({ and }) on a new line.
- 在新行加入 { }

- 在條件判斷式的區段加入 { }

- Always use a Tab & Indention size of 4.
- Tab空行的標準為4

- 每一個變數獨立宣告，不要寫在同一行

- ~~Place namespace “using” statements together at the top of file. Group .NET namespaces above custom namespaces.~~
- ~~using namespace 敘述放置檔案的最頂端，外部的using在.NET Framework之下~~
- 外部的 using 在.NET Framework之下

- Group internal class implementation by type in the following order:
- 類別(Class)中的排序
    a. Member variables.
    b. Constructors & Finalizers.
    c. Nested Enums, Structs, and Classes.
    d. Properties
    e. Methods

- 修飾子(Access Modifier) 的排序
- Sequence declarations within type groups based upon access modifier and visibility:
    a. Public
    b. Protected
    c. Internal
    d. Private


- ~~Segregate interface Implementation by using #region statements.~~
- ~~使用#region區分不同程式區塊~~


- Append folder-name to namespace for source files within sub-folders.
- 在namespace加上資料夾名稱

- Recursively indent all code blocks contained within braces.
- 所有的程式區塊都要縮進 { } 中

- Use white space (CR/LF, Tabs, etc) liberally to separate and organize code.
- 用空格隔開跟組織程式碼

- Only declare related attribute declarations on a single line, otherwise stack each attribute as a separate declaration.
- 宣告屬性時，相關的屬性擺在同一行，不相關的屬性分開行寫

- Place Assembly scope attribute declarations on a separate line.
- Place Type scope attribute declarations on a separate line.
- Place Method scope attribute declarations on a separate line.
- Place Member scope attribute declarations on a separate line.
- Place Parameter attribute declarations inline with the parameter.
- Assembly、Type、Method、Field、Parameter範圍的Attribute，放置不同行

- If in doubt, always err on the side of clarity and consistency.
- 程式碼撰寫時，盡量保持連續性與簡潔

- All comments should be written in the same language, be grammatically correct, and contain appropriate punctuation.
- 所有的註解必須使用相同語言，並且語法正確，使用標點符號。

- 使用 // 或 /// 不要使用 /* ... */

- Do not “flowerbox” comment blocks.
- 不要使用 井字號包住註解區塊

    Example:
    // ***************************************
    // Comment block
    // ***************************************

- Use inline-comments to explain assumptions, known issues, and algorithm insights.
- 使用在行內的註解，來解釋假設、已知的Issue、和演算法

- Do not use inline-comments to explain obvious code. Well written code is self documenting.

- Only use comments for bad code to say “fix this code” – otherwise remove, or rewrite the code!
- 對設計不良的程式碼來說，唯一使用註解就是 "fix this code"，否則移除或是重寫程式碼

- Include comments using Task-List keyword flags to allow comment-filtering.
- 註解使用Task-List，內含關鍵字，這可以讓註解被篩選

    Example:
    // TODO: Place Database Code Here
    // UNDONE: Removed P\Invoke Call due to errors
    // HACK: Temporary fix until able to refactor

- Always apply C# comment-blocks (///) to public, protected, and internal declarations.
- 在public protected internal 的宣告使用 /// 來產生 Summary 註解區塊

- Only use C# comment-blocks for documenting the API.


- Always include <summary> comments. Include <param>, <return>, and <exception> comment sections where applicable.
- Summary註解區塊最好都包含 <param>,<return> <exception>

- 如果可以的話，加上 <see cref=””/> 與 <seeAlso cref=””/>

- Always add CDATA tags to comments containing code and other embedded markup in order to avoid encoding issues.
- 在註解中增加CDATA，避免編碼問題

    Example:
    /// <example>
    /// Add the following key to the “appSettings” section of your config:
    /// <code> <![CDATA[
    /// <configuration>
    /// <appSettings>
    /// <add key=”mySetting” value=”myValue”/>
    /// </appSettings>
    /// </configuration>
    ///  ]]> ></code>
    /// </example>

