4. Coding Style
===============
Coding style causes the most inconsistency and controversy between developers. Each developer has a preference, and
rarely are two the same. However, consistent layout, format, and organization are key to creating maintainable code.
The following sections describe the preferred way to implement C# source code in order to create readable, clear, and
consistent code that is easy to understand and maintain.

3.1 Formatting
--------------
1. Never declare more than 1 namespace per file.
2. Avoid putting multiple classes in a single file.
3. Always place curly braces ({ and }) on a new line.
4. Always use curly braces ({ and }) in conditional statements.
5. Always use a Tab & Indention size of 4.
6. Declare each variable independently ¡V not in the same statement.
7. Place namespace ¡§using¡¨ statements together at the top of file. Group .NET namespaces above custom namespaces.
8. Group internal class implementation by type in the following order:
    a. Member variables.
    b. Constructors & Finalizers.
    c. Nested Enums, Structs, and Classes.
    d. Properties
    e. Methods

9. Sequence declarations within type groups based upon access modifier and visibility:
    a. Public
    b. Protected
    c. Internal
    d. Private

10. Segregate interface Implementation by using #region statements.
11. Append folder-name to namespace for source files within sub-folders.
12. Recursively indent all code blocks contained within braces.
13. Use white space (CR/LF, Tabs, etc) liberally to separate and organize code.
14. Only declare related attribute declarations on a single line, otherwise stack each attribute as a separate declaration.
15. Place Assembly scope attribute declarations on a separate line.
16. Place Type scope attribute declarations on a separate line.
17. Place Method scope attribute declarations on a separate line.
18. Place Member scope attribute declarations on a separate line.
19. Place Parameter attribute declarations inline with the parameter.
20. If in doubt, always err on the side of clarity and consistency.
21. All comments should be written in the same language, be grammatically correct, and contain appropriate punctuation.
22. Use // or /// but never /* ¡K */
23. Do not ¡§flowerbox¡¨ comment blocks.
    Example:
    // ***************************************
    // Comment block
    // ***************************************

24. Use inline-comments to explain assumptions, known issues, and algorithm insights.
25. Do not use inline-comments to explain obvious code. Well written code is self documenting.
26. Only use comments for bad code to say ¡§fix this code¡¨ ¡V otherwise remove, or rewrite the code!
27. Include comments using Task-List keyword flags to allow comment-filtering.
    Example:
    // TODO: Place Database Code Here
    // UNDONE: Removed P\Invoke Call due to errors
    // HACK: Temporary fix until able to refactor

28. Always apply C# comment-blocks (///) to public, protected, and internal declarations.
29. Only use C# comment-blocks for documenting the API.
30. Always include <summary> comments. Include <param>, <return>, and <exception> comment sections where applicable.
31. Include <see cref=¡¨¡¨/> and <seeAlso cref=¡¨¡¨/> where possible.
32. Always add CDATA tags to comments containing code and other embedded markup in order to avoid encoding issues.
    Example:
    /// <example>
    /// Add the following key to the ¡§appSettings¡¨ section of your config:
    /// <code> <![CDATA[
    /// <configuration>
    /// <appSettings>
    /// <add key=¡¨mySetting¡¨ value=¡¨myValue¡¨/>
    /// </appSettings>
    /// </configuration>
    ///  ]]> ></code>
    /// </example>


