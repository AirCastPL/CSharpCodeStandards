1. Introduction
============
本文規範及建議如何使用 C# 語言來開發應用程式以及函式庫。希望透過訂定完整清楚的準則、統一程式編寫風格與格式，以減少開發時遇到陷阱或發生錯誤，提高程式碼維護性。

本文包含**命名規則 (Naming Conventions)**、**程式碼編寫風格 (Coding Style)**、**語言使用規範 (Language Usage)**、**物件模型設計 (Object Model Design)**等部分。


1.1 Scope
--------------
本文僅適用於 **C# 語言**。但由於使用 C# 語言開發與 .NET Framework 息息相關，所以亦涵蓋部分 .NET Framework Class Library 之用法說明。


1.2 Terminology & Definitions 
------------------------------------------
以下為本文所參使用到的術語定義：
 
**存取修飾子 (Access Modifier)**
> C# 以關鍵字 `public`、`protected`、`internal`、`private` 及 `protected internal` 定義型別(Types) 與成員(Members) 間的存取性，這些關鍵字稱為存取修飾子 (Access Modifier)。類別(Classes) 及其大部分的成員其存取修飾子預設值為 `private`，但介面(Interfaces)和列舉(Enums) 則預設為 `public`。 
>
> [Access Modifiers, C# Programming Guide, MSDN](https://msdn.microsoft.com/en-us/library/ms173121.aspx)

**駝峰式命名 (Camel Case)**
>首字的第一個字母小寫，其後除每個單字的第一個母大寫其餘皆為小寫，的一種命名形式。
>
>***Example***
>
    customerName
    isYourBirthday
>		
>[CamelCase, Wikipedia](https://en.wikipedia.org/wiki/CamelCase)

**Common Type System** 	 
The .NET Framework common type system (CTS) defines how types are declared, used, and managed.  All native C# types are based upon the CTS to ensure support for cross-language integration.  
https://msdn.microsoft.com/en-us/library/zcx1eb1e(v=vs.100).aspx

**識別符號(Identifier)**
A developer defined token used to uniquely name a declared object or object instance. 
	 	Example: public class MyClassNameIdentifier { … } 

**Magic Number**
Any numeric literal used within an expression (or to initialize a variable) that does not have an obvious or wellknown meaning.  This usually excludes the integers 0 or 1 and any other numeric equivalent precision that evaluates as zero. 

**Pascal Case**
A word with the first letter capitalized, and the first letter of each subsequent word-part capitalized.   
	 	Example: CustomerName 

**Field** 
**Property**
**Attribute**

**關鍵字(Keyword)**
**字面量(Literal)**
**運算子(Operator)**

https://msdn.microsoft.com/en-us/library/ff926074.aspx
https://msdn.microsoft.com/en-us/library/ms229042.aspx
https://github.com/dennisdoomen/CSharpGuidelines