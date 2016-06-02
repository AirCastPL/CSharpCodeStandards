6. Object Model Design
======================

General
-------
- **總是** 將 **欄位(Fields)** 其存取性宣告為 **private**；而 **屬性(Properties)** 則用 **public**、**protected**、**internal** 或 **protected internal** 來宣告。
    - 屬性常用於封裝欄位，成為公開介面。
    - 屬性是可以繼承，而欄位不能。


- Always declare types explicitly within a namespace. Do not use the default “{global}” namespace.

- Avoid overuse of the public access modifier. Typically fewer than 10% of your types and members will be part of a public API, unless you are writing a class library.

- Consider using internal or private access modifiers for types and members unless you intend to support them as part of a public API.

- Never use the protected access modifier within sealed classes unless overriding a protected member of an inherited type.

- Avoid declaring methods with more than 5 parameters. Consider refactoring this code.

- Try to replace large parameter-sets (> than 5 parameters) with one or more class or struct parameters – especially when used in multiple method signatures.

- Do not use the “new” keyword on method and property declarations to hide members of a derived type.

- Only use the “base” keyword when invoking a base class constructor or base implementation 
within an override.

- Consider using method overloading instead of the params attribute (but be careful not to break CLS Compliance of your API’s).

- Always validate an enumeration variable or parameter value before consuming it. They may contain any value that the underlying Enum type (default int) supports.

		// Example
		public void Test(BookCategory cat)
		{
		if (Enum.IsDefined(typeof(BookCategory), cat))
		{…}
		}

- Consider overriding Equals() on a struct.

- Always override the Equality Operator (==) when overriding the Equals() method.

- Always override the String Implicit Operator when overriding the ToString() method.

- Always call Close() or Dispose() on classes that offer it.

- Wrap instantiation of IDisposable objects with a “using” statement to ensure that Dispose() is automatically called.

		// Example
		using(SqlConnection cn = new SqlConnection(_connectionString))
		{…}




- Always prefer aggregation over inheritance.

- Avoid “Premature Generalization”. Create abstractions only when the intent is understood.

- Do the simplest thing that works, then refactor when necessary.

- Always make object-behavior transparent to API consumers.

- Avoid unexpected side-affects when properties, methods, and constructors are invoked.

- Always separate presentation layer from business logic.

- Always prefer interfaces over abstract classes.

- Try to include the design-pattern names such as “Bridge”, “Adapter”, or “Factory” as a suffix to class names where appropriate.

- Only make members virtual if they are designed and tested for extensibility.

- Refactor often!


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
