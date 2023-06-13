# 代码规范

**简体中文** | [繁體中文](./zh_hant_tw.md) | [English](./en_us.md)

此文档旨在对 HyPlayer 相关项目的代码贡献者进行代码规范的说明，以便于项目的维护和开发。

## 简介

此代码规范旨在统一代码风格，提高代码可读性，降低代码维护成本。如果你是一个新的贡献者，你应该阅读此文档以了解我们的代码规范。

此规范可能存在不完善的地方，如果你有任何建议，请参照 [修订规范](##修订规范) 的步骤进行修改。

该规范存在部分强制和建议内容, 按照 [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) 进行处理，提示词仅为提示强制性，如包含 **NOT**，依据所指建议的内容进行处理。

## 正文

### 对齐和缩进

#### 缩进

* [**MUST NOT**] 不使用制表符进行缩进
* [**RECOMMENDED**] 使用 4 个空格进行缩进
* [**RECOMMENDED**] 对嵌套语句不进行缩进
* [**RECOMMENDED**] 圆括号的缩进遵循 `K&R 样式`
* [**MUST**] 对 `#if` 等预处理程序指令不进行缩进

例外的: 对于 `#region`, `#endregion` 语句照常进行缩进。

* [**MUST**] 缩进 switch 语句的 case 和 default 语句
* [**RECOMMENDED**] 不对标签进行缩进
* [**MUST**] 缩进类型约束
* [**MUST**] 缩进语句条件内的大括号

#### 多行对齐
* [**MUST**] 如果行前存在运算符, 将运算符后的同等地位内容对齐, 并将运算符的末尾对齐

例如:
    
```csharp
var a =
    someOperand
  + operand2
  + operand3
  + operand4;
```

* [**MUST**] 方法参数(定义及调用)需要对齐
* [**MUST**] 基类和接口列表需要对齐
* [**MUST**] LINQ 查询需要对齐
* [**MUST**] 二元运算 (例如 +) 需要对齐
* [**MUST**] 链式方法调用需要对齐
* [**RECOMMENDED**] 数组,对象和集合初始值设定项需要对齐
* [**MUST**] switch 表达式需要对齐
* [**MUST**] 模式匹配 (Pattern Matching) 及二元匹配 (and/or) 需要对齐
* [**RECOMMENDED**] 列表模式匹配 (List patterns) 需要对齐
* [**SHOULD NOT**] 匿名方法体无需对齐
* [**MUST**] 元组组件需要对齐
* [**MUST**] 多个声明需要对齐
* [**OPTIONAL**] 如果声明内容前存在 Attribute, 可以将声明内容对齐
* [**SHOULD NOT**] 进行赋值时, 对于相似代码, 无需进行对齐
* [**SHOULD NOT**] 相同方法的调用, 无需进行对齐
* [**OPTIONAL**] 代码注释可以进行对齐
* [**OPTIONAL**] 对于 switch 语句的返回值可以进行对齐

### 命名规则

#### 命名要求

* [**MUST**] 使用英文而不是拼音进行命名
* [**MUST**] 使用有意义的名称
* [**SHOULD NOT**] 避免使用缩写缩写
* [**SHOULD NOT**] 避免使用数字进行命名, 若数字开头, 需要添加 `The`
* [**SHOULD NOT**] 避免使用下划线进行命名
* [**RECOMMENDED**] 对于相似元素应存在相似后缀
* [**SHOULD**] 对于异步方法, 应当以 `Async` 结尾

#### 大小写规则
* [**MUST**] 类型名称使用 `UpperPascalCase`
* [**MUST**] 方法名称使用 `UpperPascalCase`
* [**MUST**] 属性名称使用 `UpperPascalCase`
* [**MUST**] 命名空间名称使用 `UpperPascalCase`
* [**MUST**] 事件名称使用 `UpperPascalCase`
* [**MUST**] 非 private 字段名称使用 `UpperPascalCase`
* [**MUST**] 常量字段名称使用 `ALL_UPPERCASE_WITH_UNDERSCORES`
* [**MUST**] private 字段名称使用 `_lowerCamelCase`
* [**MUST**] 参数名称使用 `lowerCamelCase`
* [**MUST**] 局部变量名称使用 `lowerCamelCase`
* [**MUST**] 接口名称使用 `IUpperCamelCase`
* [**MUST**] 类型形参名称使用 `TUpperCamelCase`


#### 特例

* `Id` 作为单词, 例如 `UserId` 而不是 `UserID`
* `Guid` 作为单词, 例如 `GuidValue` 而不是 `GUIDValue`
* `Url` 作为单词, 例如 `UrlValue` 而不是 `URLValue`
* `Dto` 作为单词, 例如 `UserDto` 而不是 `UserDTO`
* `ViewModel` 作为两个单词, 例如 `UserViewModel` 而不是 `UserViewmodel`
* `Html` 作为单词, 例如 `HtmlValue` 而不是 `HTMLValue`
* `Xml` 作为单词, 例如 `XmlValue` 而不是 `XMLValue`
* `Json` 作为单词, 例如 `JsonValue` 而不是 `JSONValue`
* `Username` 作为单词
* `MD5`, `AES`, `DES`, `SHA` 需要全部大写
* 使用 `Email` 而不是 `Mail` 代表电子邮箱

其余单词按照微软的命名规则和品牌官方名进行处理, 例如 `GitHub` 而不是 `Github`。

### 语法样式

#### `var` 用法

* [**MUST**] 当变量类型明显来自赋值的右侧时，或者当精度类型不重要时，请使用 `var`
* [**MUST NOT**] 当类型并非明显来自赋值的右侧时，请勿使用 var
* [**SHOULD**] 使用隐式类型化来确定 `for` 循环中循环变量的类型
* [**SHOULD NOT**] 不要使用隐式类型化来确定 `foreach` 循环中循环变量的类型
* [**SHOULD**] 对析构变量首选单独的声明
* [**MUST NOT**] 对于丢弃不应使用 `var` 关键字

#### 内置类型

* [**MUST**] 对于内置类型, 首选关键字而不是 CLR 类型名称
* [**SHOULD**] 对于数字类型, 整数优先选择 `int`, 浮点数优先选择 `double`

#### `using` 指令

* [**RECOMMENDED**] 对于常用的命名空间, 建议使用 Global Using
* [**SHOULD**] Using 语句应当将 `System` 和 `Windows` 命名空间放在最前面, 其余按照字母顺序排列
* [**MUST**] 使用 File-scoped 命名空间

#### 修饰符

[**RECOMMENDED**] 建议的修饰符顺序如下

`public`, `private`, `protected`, `internal`, `file`, `static`, `extern`, `new`, `override`, `abstract`,`virtual`, `sealed`, `required` , `readonly`, `volatile`, `async`

* [**MUST**] 对于类型优先选择 `internal` 而不是 `public`
* [**MUST**] 对于字段优先选择 `private`

#### 圆括号

* [**RECOMMENDED**] 如果圆括号内只有一个表达式, 可以省略圆括号

例外的, 如果去除圆括号后会丢失语句的逻辑, 增加理解的复杂度, 或者表示计算的优先级, 应当加上圆括号, 比如:
```csharp
var foo = ((1+2)*5) + (userInputa + userInputb);
```


#### 花括号

* [**MUST**] 方法，if 等控制语句的花括号应当单独占据一行

例外的: 类的自动属性的花括号可以与类名同行。

* [**MUST**] 花括号应当与前置语句和其他分支保持一致的缩进
* [**RECOMMENDED**] 当花括号内只有一行语句时，可以省略花括号或使用 expression body

例外的: 对于局部函数, 构造函数应使用 block body。

* [**MUST**] 对 `do-while`, `using`, `lock`, `fixed` 语句的方法体, 必须使用花括号
* [**SHOULD**] 空大括号应在同一行中, 中间应存在空格
* [**SHOULD NOT**] 大括号后不应添加注释, 若要注释应在下一行添加
例外的: 当控制语句的其他分支存在花括号, 应当保留花括号。

将上述规范进行综合, 可得到如下示例:

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
#### 尾随逗号

[**RECOMMENDED**] 在多行列表新行前添加尾随逗号

#### 类型名称省略

* [**RECOMMENDED**] 对于类型创建, 可以省略 new 之后的创建类型
* [**RECOMMENDED**] 对于 default 关键字, 可以类型名称

#### 换行

* [**SHOULD**] 对于超过 120 字符的行应当进行换行
* [**MUST**] `else if` 应当在同一行
* [**MUST**] 逗号应当存在于上一行的末尾
* [**SHOULD**] 一行最多存在 4 个形参
* [**SHOULD**] 对于形参若需换行应对每个形参进行换行, 且第一个前需要换行
* [**SHOULD**] 对于类型约束若需换行应对每个约束进行换行, 且第一个前需要换行

#### 空格

* [**MUST**] 二元运算符两侧应当存在空格
* [**MUST NOT**] 一元运算符右侧不应当存在空格
* [**MUST**] 三元运算符前后应当存在空格
* [**MUST**] 若非行末, 逗号、分号、冒号后应当存在空格, 符号前无需空格
* [**MUST**] 语句的括号左侧应当存在空格, 内部不需要空格
* [**MUST**] 行注释前需要空格
* [**MUST**] lambda 箭头周围需要空格

### Null 检查

* [**MUST**] 所有项目必须启用 Nullable
* [**SHOULD**] 对于可为 Null 的对象, 应当使用 `?` 进行标记
* [**SHOULD**] 使用以下方式进行 Null 检查

```csharp
if (obja?.obj is null)
{
    // do something
}

if (obja?.objc is not null)
{
    // do something
}

```

### 文件规范

* [**RECOMMENDED**] 文件名应当与类名一致
* [**SHOULD**] 一个文件只能存放一个类, 若类过大, 应当考虑拆分
* [**RECOMMENDED**] 对类进行拆分时, 应当单独开启一个文件夹存放, 文件名采用 `类名.功能.cs`
* [**RECOMMENDED**] 文件名应当使用 PascalCase
* [**RECOMMENDED**] 文件名应当使用英文
* [**SHOULD**] 对于扩展方法, 应当将其放置在单独的 `Extensions` 文件夹中, 文件名采用 `类名Extensions.cs`

### 注释规范

* [**SHOULD**] 对于公开的方法, 属性, 字段, 构造函数, 应当添加注释
* [**RECOMMENDED**] 注释应当符合 XML 注释规范
* [**MUST**] 使用 `// TODO: <注释>` 标记未完成的代码
* [**SHOULD**] 对于装饰分割型注释, 应当使用 `/******** <注释> ********/` 进行标记, 并保证对齐, 使用不同的长度表示层级

### 异常处理

* [**SHOULD**] 对于异常处理, 应当使用 `try-catch` 进行处理
* [**MUST**] 若需要在 catch 中继续抛出异常, 请使用 `throw;` 而不是 `throw err;`
* [**RECOMMENDED**] 不建议使用引发异常代替错误返回, 这种情况下建议使用 Result 类型

### 资源释放

* [**SHOULD**] 对于需要释放的资源, 应当使用 `using` 进行释放
* [**SHOULD**] 若存在需要释放的内容, 应实现 `IDisposable` 接口
* [**SHOULD**] 在 try-catch 语句中存在需要释放的资源, 应当使用 `finally` 进行释放

### 其余规范

* [**SHOULD**] 对于枚举值, 第一个项应当为未知项
* [**SHOULD**] 使用 StringBuilder 进行长字符串拼接
* [**RECOMMENDED**] 使用 `ReadOnlySpan` 来减少对内存的占用
* [**SHOULD NOT**] 不建议使用 `struct`
* [**MUST NOT**] 对于重复使用的代码, 应当使用方法进行封装
* [**SHOULD**] 使用 `if (obj is BaseType foo)` 进行类型转换或者 `as` 运算符


## 修订规范

如果你想要修改此规范，请按照以下步骤进行：

1. 发起一个 Issue，简要描述你的修改内容
2. 创建项目 Fork
3. 在 Fork 中创建属于你的分支，分支名参照: `/draft/<你的名称>/<修订的简介，多个单词使用 - 分割>`
4. 将 Issue 连接到这个 Fork 的分支
5. 在新的分支中修改代码规范
6. 遵循提交模板进行 Pull Request
7. 等待审核