2. Naming Conventions
=====================
Consistency is the key to maintainable code. This statement is most true for naming your projects, source files, and
identifiers including Fields, Variables, Properties, Methods, Parameters, Classes, Interfaces, and Namespaces.

2.1 General Guidelines
----------------------
-  Always use Camel Case or Pascal Case names.
-  使用Pascal Case 或是 Camel Case 

-  Avoid ALL CAPS and all lowercase names. Single lowercase words or letters are acceptable.
-  避免全大寫或全小寫的名稱。單個小寫單詞或字母是可以接受的

-  Do not create declarations of the same type (namespace, class, method, property, field, or parameter) and access modifier (protected, public, private, internal) that vary only by capitalization.
-  不要建立相同類型的宣告(包含namespace、class、method、property、field or parameter)與保留字

-  Do not use names that begin with a numeric character.
-  不要以數字當做變數命名開頭

-  Do add numeric suffixes to identifier names.
-  不要把數字加入變數的中綴詞

-  Always choose meaningful and specific names.
-  使用有意義的名詞當做變數

-  Always err on the side of verbosity not terseness.
-  如果簡潔的命名無法明確表達意義，使用較冗長的命名

-  Variables and Properties should describe an entity not the type or size.
-  變數與屬性必須能夠描述他自己

-  Do not use Hungarian Notation!
-  不要使用匈牙利命名法
    Example: strName or iCount

- Avoid using abbreviations unless the full name is excessive.
- 避免使用縮寫，除非全名真的過長

- Avoid abbreviations longer than 5 characters.
- 避免縮寫超過5個字

- Any Abbreviations must be widely known and accepted.
- 任何的縮寫必須是為大家所知道的

- Use uppercase for two-letter abbreviations, and Pascal Case for longer abbreviations.
- 使用Pascal Case來設計比較長的縮寫變數

- Do not use C# reserved words as names.
- 不要使用C#保留字當做變數

- Avoid naming conflicts with existing .NET Framework namespaces, or types.
- 避免變數與.NET Framework namespace 和 型別衝突

- Avoid adding redundant or meaningless prefixes and suffixes to identifiers
- 避免增加無意義的前餟詞與中綴詞

- Do not include the parent class name within a property name.
- 屬性名稱命名時，不要包含父類別名稱

    Example: Customer.Name NOT Customer.CustomerName

- Try to prefix Boolean variables and properties with “Can”, “Is” or “Has”.
- 嘗試使用 "Can" "Is" "Has" 在Boolean的命名上

- Append computational qualifiers to variable names like Average, Count, Sum, Min, and Max where appropriate.
- 加上 "Average" "Count" "Sum" "Min" "Max" 關鍵字在計量的變數上

- When defining a root namespace, use a Product, Company, or Developer Name as the root.
- 定義root namespace時，使用產品、公司 或開發者名字


2.2 Name Usage & Syntax
-----------------------





