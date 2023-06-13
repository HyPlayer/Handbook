# Code Specification

[简体中文](./zh_hans_cn.md) | [繁體中文](./zh_hant_tw.md) | **English**

This document aims to explain code specifications to code contributors of HyPlayer-related projects, so as to facilitate project maintenance and development.

## Introduction

This code specification aims to unify the code style, improve code readability, and reduce code maintenance costs. If you're a new contributor, you should read this document to understand our code guidelines.

There may be imperfections in this specification, if you have any suggestions, please refer to the steps of [Revised Specification](##Revised Specification) to modify.

There are some mandatory and recommended contents in this specification, which are processed according to [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119), and the prompt words are only mandatory, such as **NOT**, Proceed with the content of the suggested suggestion.

## Content

### Alignment and indentation

#### Indentation

* [**MUST NOT**] do not use tabs for indentation
* [**RECOMMENDED**] Use 4 spaces for indentation
* [**RECOMMENDED**] Do not indent nested statements
* [**RECOMMENDED**] Indentation of parentheses follows `K&R style`
* [**MUST**] Do not indent preprocessor directives such as `#if`

Exception: For `#region`, `#endregion` statements are indented as normal.

* [**MUST**] indent switch statement's case and default statements
* [**RECOMMENDED**] do not indent tags
* [**MUST**] Indent type constraints
* [**MUST**] Indent curly braces inside statement conditions

#### Multi-line alignment
* [**MUST**] If there is an operator before the line, align the content of the same position after the operator, and align the end of the operator

For example:
    
```csharp
var a =
     someOperand
   + operand2
   + operand3
   + operand4;
```

* [**MUST**] Method parameters (definition and call) need to be aligned
* [**MUST**] Base class and interface lists need to be aligned
* [**MUST**] LINQ query requires alignment
* [**MUST**] Binary operations (such as +) require alignment
* [**MUST**] Chained method calls require alignment
* [**RECOMMENDED**] array, object and collection initializers require alignment
* [**MUST**] switch expressions need to be aligned
* [**MUST**] pattern matching (Pattern Matching) and binary matching (and/or) need to be aligned
* [**RECOMMENDED**] List patterns need alignment
* [**SHOULD NOT**] Anonymous method body does not need to be aligned
* [**MUST**] Tuple components need to be aligned
* [**MUST**] Multiple declarations need to be aligned
* [**OPTIONAL**] If there is an Attribute before the declaration content, the declaration content can be aligned
* [**SHOULD NOT**] When assigning values, for similar codes, no alignment is required
* [**SHOULD NOT**] Calls of the same method without alignment
* [**OPTIONAL**] Code comments can be aligned
* [**OPTIONAL**] The return value of the switch statement can be aligned

### Naming rules

#### Naming Requirements

* [**MUST**] Use English instead of Pinyin for naming
* [**MUST**] Use meaningful names
* [**SHOULD NOT**] Avoid shorthand abbreviations
* [**SHOULD NOT**] Avoid using numbers for naming, if the number starts, you need to add `The`
* [**SHOULD NOT**] Avoid underscores in names
* [**RECOMMENDED**] Similar suffixes should exist for similar elements
* [**SHOULD**] For asynchronous methods, should end with `Async`

#### Case rules
* [**MUST**] Use `UpperPascalCase` for type names
* [**MUST**] Use `UpperPascalCase` for method names
* [**MUST**] Use `UpperPascalCase` for attribute names
* [**MUST**] Use `UpperPascalCase` for namespace names
* [**MUST**] Use `UpperPascalCase` for event names
* [**MUST**] Use `UpperPascalCase` for non-private field names
* [**MUST**] Use `ALL_UPPERCASE_WITH_UNDERSCORES` for constant field names
* [**MUST**] Private field names use `_lowerCamelCase`
* [**MUST**] Parameter names use `lowerCamelCase`
* [**MUST**] Use `lowerCamelCase` for local variable names
* [**MUST**] Use `IUpperCamelCase` for interface names
* [**MUST**] Use `TUpperCamelCase` for type parameter names


#### Special Cases

* `Id` as a word, e.g. `UserId` instead of `UserID`
* `Guid` as a word, e.g. `GuidValue` instead of `GUIDValue`
* `Url` as a word, eg `UrlValue` instead of `URLValue`
* `Dto` as word, eg `UserDto` instead of `UserDTO`
* `ViewModel` as two words, eg `UserViewModel` instead of `UserViewmodel`
* `Html` as a word, eg `HtmlValue` instead of `HTMLValue`
* `Xml` as a word, e.g. `XmlValue` instead of `XMLValue`
* `Json` as word, e.g. `JsonValue` instead of `JSONValue`
* `Username` as a word
* `MD5`, `AES`, `DES`, `SHA` need to be all uppercase
* Use `Email` instead of `Mail` for email

The remaining words are handled according to Microsoft's naming rules and official brand names, such as `GitHub` instead of `Github`.

### Grammar style

#### `var` Usage

* [**MUST**] Use `var` when the variable type is clearly from the right-hand side of the assignment, or when the precision type is unimportant
* [**MUST NOT**] Do not use var when the type is not obvious from the right side of the assignment
* [**SHOULD**] Use implicit typing to determine the type of the loop variable in a `for` loop
* [**SHOULD NOT**] Do not use implicit typing to determine the type of a loop variable in a `foreach` loop
* [**SHOULD**] Prefer separate declarations for destructor variables
* [**MUST NOT**] The `var` keyword should not be used for discarding

#### Built-in types

* [**MUST**] For built-in types, prefer keywords over CLR type names
* [**SHOULD**] For numeric types, prefer `int` for integers, `double` for floating point numbers

#### `using` Directives

* [**RECOMMENDED**] For commonly used namespaces, it is recommended to use Global Using
* [**SHOULD**] Using statements should put the `System` and `Windows` namespaces first, and the rest in alphabetical order
* [**MUST**] use the File-scoped namespace

#### Modifiers

[**RECOMMENDED**] The recommended modifier order is as follows

`public`, `private`, `protected`, `internal`, `file`, `static`, `extern`, `new`, `override`, `abstract`, `virtual`, `sealed`, `required ` , `readonly`, `volatile`, `async`

* [**MUST**] Prefer `internal` over `public` for types
* [**MUST**] Prefer `private` for fields

#### Parentheses

* [**RECOMMENDED**] If there is only one expression inside the parentheses, the parentheses can be omitted

As an exception, if the logic of the statement will be lost after removing the parentheses, which increases the complexity of understanding, or indicates the priority of calculation, parentheses should be added, for example:
```csharp
var foo = ((1+2)*5) + (userInputa + userInputb);
```


#### curly braces

* [**MUST**] method, curly braces of if and other control statements should occupy a single line

Exception: curly braces for automatic properties of a class may accompany the class name.

* [**MUST**] Curly braces should be indented consistently with preceding statements and other branches
* [**RECOMMENDED**] When there is only one line of statement inside the curly braces, you can omit the curly braces or use expression body

Exception: For local functions, constructors should use a block body.

* [**MUST**] Curly braces must be used for the body of `do-while`, `using`, `lock`, `fixed` statements
* [**SHOULD**] empty curly braces should be on the same line, there should be spaces in between
* [**SHOULD NOT**] Comments should not be added after curly braces, and comments should be added on the next line
Exception: When braces exist for other branches of a control statement, the braces should be preserved.

Combining the above specifications, the following example can be obtained:

```csharp
public class Foo {
     public int Bar { get; set; }
     public int Baz()
     {
         if (Bar == 0)
         {
             // comment
             return 5;
         }
         else if (Bar == 1)
         {
             Bar = 2;
             return Bar;
         }

         if (Bar == 2)
             return 3;

         return 5;
     }
}
```
#### trailing comma

[**RECOMMENDED**] Add trailing commas before newlines in multiline lists

#### type name omitted

* [**RECOMMENDED**] For type creation, the created type after new can be omitted
* [**RECOMMENDED**] For default keyword, can type name

#### Newline

* [**SHOULD**] Lines longer than 120 characters should be wrapped
* [**MUST**] `else if` should be on the same line
* [**MUST**] A comma should exist at the end of the previous line
* [**SHOULD**] There can be at most 4 parameters per line
* [**SHOULD**] For formal parameters, if newlines are required, each formal parameter should be newlined, and a newline is required before the first one
* [**SHOULD**] For type constraints, if newlines are required, each constraint should be newlined, and a newline is required before the first one

#### spaces

* [**MUST**] Binary operators should have spaces around them
* [**MUST NOT**] There should be no spaces on the right side of the unary operator
* [**MUST**] There should be spaces before and after the ternary operator
* [**MUST**] If it is not the end of the line, there should be a space after the comma, semicolon, and colon, and no space before the symbol
* [**MUST**] The left side of the parentheses of the statement should have a space, no spaces are required inside
* [**MUST**] Spaces are required before line comments
* [**MUST**] spaces are required around lambda arrows

### Null checks

* [**MUST**] All projects must have Nullable enabled
* [**SHOULD**] Nullable objects should be marked with `?`
* [**SHOULD**] Null checks using

```csharp
if (obja?. obj is null)
{
     // do something
}

if (obja?. objc is not null)
{
     // do something
}

```

### Document specification

* [**RECOMMENDED**] The file name should match the class name
* [**SHOULD**] A file can only store one class, if the class is too large, you should consider splitting it
* [**RECOMMENDED**] When splitting a class, a separate folder should be opened for storage, and the file name should be `class name.function.cs`
* [**RECOMMENDED**] Filenames should use PascalCase
* [**RECOMMENDED**] Filenames should be in English
* [**SHOULD**] For extension methods, they should be placed in a separate `Extensions` folder, and the file name uses `class name Extensions.cs`

### Annotation specification

* [**SHOULD**] Comments should be added to public methods, properties, fields, and constructors
* [**RECOMMENDED**] Comments should conform to the XML Comments specification
* [**MUST**] Use `// TODO: <comment>` to mark incomplete code
* [**SHOULD**] For decorative split comments, you should use `/******** <comment>********/` to mark, and ensure alignment, using different lengths presentation level

### exception handling

* [**SHOULD**] For exception handling, `try-catch` should be used for handling
* [**MUST**] If you need to continue throwing exceptions in catch, please use `throw;` instead of `throw err;`
* [**RECOMMENDED**] It is not recommended to use throwing an exception instead of returning an error, in this case it is recommended to use the Result type

### Resource release

* [**SHOULD**] For resources that need to be released, `using` should be used to release
* [**SHOULD**] If there is content that needs to be released, it should implement the `IDisposable` interface
* [**SHOULD**] There are resources that need to be released in the try-catch statement, and `finally` should be used to release them

### Other Specifications

* [**SHOULD**] For enumeration values, the first item should be unknown
* [**SHOULD**] Use StringBuilder for long string concatenation
* [**RECOMMENDED**] Use `ReadOnlySpan` to reduce memory usage
* [**SHOULD NOT**] `struct` is deprecated
* [**MUST NOT**] For reusable code, methods should be used for encapsulation
* [**SHOULD**] Use `if (obj is BaseType foo)` for type conversion or `as` operator


## Revision specification

If you want to modify this specification, please follow the steps below:

1. Initiate an Issue and briefly describe your modification
2. Create a project fork
3. Create your own branch in Fork, refer to the branch name: `/draft/<your name>/<revised introduction, use multiple words - split>`
4. Connect the Issue to the branch of this Fork
5. Modify the code specification in the new branch
6. Follow the submission template for Pull Request
7. Waiting for review