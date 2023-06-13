# 程式碼規範

[简体中文](./zh_hans_cn.md) | **繁體中文** | [English](./en_us.md)

此文件旨在對 HyPlayer 相關專案的程式碼貢獻者進行程式碼規範的說明，以便於專案的維護和開發。

## 簡介

此程式碼規範旨在統一程式碼風格，提高程式碼可讀性，降低程式碼維護成本。如果你是一個新的貢獻者，你應該閱讀此文件以瞭解我們的程式碼規範。

此規範可能存在不完善的地方，如果你有任何建議，請參照 [修訂規範](##修訂規範) 的步驟進行修改。

該規範存在部分強制和建議內容, 按照 [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) 進行處理，提示詞僅為提示強制性，如包含 **NOT**，依據所指建議的內容進行處理。

## 正文

### 對齊和縮排

#### 縮排

* [**MUST NOT**] 不使用製表符進行縮排
* [**RECOMMENDED**] 使用 4 個空格進行縮排
* [**RECOMMENDED**] 對巢狀語句不進行縮排
* [**RECOMMENDED**] 圓括號的縮排遵循 `K&R 樣式`
* [**MUST**] 對 `#if` 等預處理程式指令不進行縮排

例外的: 對於 `#region`, `#endregion` 語句照常進行縮排。

* [**MUST**] 縮排 switch 語句的 case 和 default 語句
* [**RECOMMENDED**] 不對標籤進行縮排
* [**MUST**] 縮排型別約束
* [**MUST**] 縮排語句條件內的大括號

#### 多行對齊
* [**MUST**] 如果行前存在運算子, 將運算子後的同等地位內容對齊, 並將運算子的末尾對齊

例如:
    
```csharp
var a =
    someOperand
  + operand2
  + operand3
  + operand4;
```

* [**MUST**] 方法引數(定義及呼叫)需要對齊
* [**MUST**] 基類和介面列表需要對齊
* [**MUST**] LINQ 查詢需要對齊
* [**MUST**] 二元運算 (例如 +) 需要對齊
* [**MUST**] 鏈式方法呼叫需要對齊
* [**RECOMMENDED**] 陣列,物件和集合初始值設定項需要對齊
* [**MUST**] switch 表示式需要對齊
* [**MUST**] 模式匹配 (Pattern Matching) 及二元匹配 (and/or) 需要對齊
* [**RECOMMENDED**] 列表模式匹配 (List patterns) 需要對齊
* [**SHOULD NOT**] 匿名方法體無需對齊
* [**MUST**] 元組元件需要對齊
* [**MUST**] 多個宣告需要對齊
* [**OPTIONAL**] 如果宣告內容前存在 Attribute, 可以將宣告內容對齊
* [**SHOULD NOT**] 進行賦值時, 對於相似程式碼, 無需進行對齊
* [**SHOULD NOT**] 相同方法的呼叫, 無需進行對齊
* [**OPTIONAL**] 程式碼註釋可以進行對齊
* [**OPTIONAL**] 對於 switch 語句的返回值可以進行對齊

### 命名規則

#### 命名要求

* [**MUST**] 使用英文而不是拼音進行命名
* [**MUST**] 使用有意義的名稱
* [**SHOULD NOT**] 避免使用縮寫縮寫
* [**SHOULD NOT**] 避免使用數字進行命名, 若數字開頭, 需要新增 `The`
* [**SHOULD NOT**] 避免使用下劃線進行命名
* [**RECOMMENDED**] 對於相似元素應存在相似字尾
* [**SHOULD**] 對於非同步方法, 應當以 `Async` 結尾

#### 大小寫規則
* [**MUST**] 型別名稱使用 `UpperPascalCase`
* [**MUST**] 方法名稱使用 `UpperPascalCase`
* [**MUST**] 屬性名稱使用 `UpperPascalCase`
* [**MUST**] 名稱空間名稱使用 `UpperPascalCase`
* [**MUST**] 事件名稱使用 `UpperPascalCase`
* [**MUST**] 非 private 欄位名稱使用 `UpperPascalCase`
* [**MUST**] 常量欄位名稱使用 `ALL_UPPERCASE_WITH_UNDERSCORES`
* [**MUST**] private 欄位名稱使用 `_lowerCamelCase`
* [**MUST**] 引數名稱使用 `lowerCamelCase`
* [**MUST**] 區域性變數名稱使用 `lowerCamelCase`
* [**MUST**] 介面名稱使用 `IUpperCamelCase`
* [**MUST**] 型別形參名稱使用 `TUpperCamelCase`


#### 特例

* `Id` 作為單詞, 例如 `UserId` 而不是 `UserID`
* `Guid` 作為單詞, 例如 `GuidValue` 而不是 `GUIDValue`
* `Url` 作為單詞, 例如 `UrlValue` 而不是 `URLValue`
* `Dto` 作為單詞, 例如 `UserDto` 而不是 `UserDTO`
* `ViewModel` 作為兩個單詞, 例如 `UserViewModel` 而不是 `UserViewmodel`
* `Html` 作為單詞, 例如 `HtmlValue` 而不是 `HTMLValue`
* `Xml` 作為單詞, 例如 `XmlValue` 而不是 `XMLValue`
* `Json` 作為單詞, 例如 `JsonValue` 而不是 `JSONValue`
* `Username` 作為單詞
* `MD5`, `AES`, `DES`, `SHA` 需要全部大寫
* 使用 `Email` 而不是 `Mail` 代表電子郵箱

其餘單詞按照微軟的命名規則和品牌官方名進行處理, 例如 `GitHub` 而不是 `Github`。

### 語法樣式

#### `var` 用法

* [**MUST**] 當變數型別明顯來自賦值的右側時，或者當精度型別不重要時，請使用 `var`
* [**MUST NOT**] 當型別並非明顯來自賦值的右側時，請勿使用 var
* [**SHOULD**] 使用隱式型別化來確定 `for` 迴圈中迴圈變數的型別
* [**SHOULD NOT**] 不要使用隱式型別化來確定 `foreach` 迴圈中迴圈變數的型別
* [**SHOULD**] 對析構變數首選單獨的宣告
* [**MUST NOT**] 對於丟棄不應使用 `var` 關鍵字

#### 內建型別

* [**MUST**] 對於內建型別, 首選關鍵字而不是 CLR 型別名稱
* [**SHOULD**] 對於數字型別, 整數優先選擇 `int`, 浮點數優先選擇 `double`

#### `using` 指令

* [**RECOMMENDED**] 對於常用的名稱空間, 建議使用 Global Using
* [**SHOULD**] Using 語句應當將 `System` 和 `Windows` 名稱空間放在最前面, 其餘按照字母順序排列
* [**MUST**] 使用 File-scoped 名稱空間

#### 修飾符

[**RECOMMENDED**] 建議的修飾符順序如下

`public`, `private`, `protected`, `internal`, `file`, `static`, `extern`, `new`, `override`, `abstract`,`virtual`, `sealed`, `required` , `readonly`, `volatile`, `async`

* [**MUST**] 對於型別優先選擇 `internal` 而不是 `public`
* [**MUST**] 對於欄位優先選擇 `private`

#### 圓括號

* [**RECOMMENDED**] 如果圓括號內只有一個表示式, 可以省略圓括號

例外的, 如果去除圓括號後會丟失語句的邏輯, 增加理解的複雜度, 或者表示計算的優先順序, 應當加上圓括號, 比如:
```csharp
var foo = ((1+2)*5) + (userInputa + userInputb);
```


#### 花括號

* [**MUST**] 方法，if 等控制語句的花括號應當單獨佔據一行

例外的: 類的自動屬性的花括號可以與類名同行。

* [**MUST**] 花括號應當與前置語句和其他分支保持一致的縮排
* [**RECOMMENDED**] 當花括號內只有一行語句時，可以省略花括號或使用 expression body

例外的: 對於區域性函式, 建構函式應使用 block body。

* [**MUST**] 對 `do-while`, `using`, `lock`, `fixed` 語句的方法體, 必須使用花括號
* [**SHOULD**] 空大括號應在同一行中, 中間應存在空格
* [**SHOULD NOT**] 大括號後不應新增註釋, 若要註釋應在下一行新增
例外的: 當控制語句的其他分支存在花括號, 應當保留花括號。

將上述規範進行綜合, 可得到如下示例:

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
#### 尾隨逗號

[**RECOMMENDED**] 在多行列表新行前新增尾隨逗號

#### 型別名稱省略

* [**RECOMMENDED**] 對於型別建立, 可以省略 new 之後的建立型別
* [**RECOMMENDED**] 對於 default 關鍵字, 可以型別名稱

#### 換行

* [**SHOULD**] 對於超過 120 字元的行應當進行換行
* [**MUST**] `else if` 應當在同一行
* [**MUST**] 逗號應當存在於上一行的末尾
* [**SHOULD**] 一行最多存在 4 個形參
* [**SHOULD**] 對於形參若需換行應對每個形參進行換行, 且第一個前需要換行
* [**SHOULD**] 對於型別約束若需換行應對每個約束進行換行, 且第一個前需要換行

#### 空格

* [**MUST**] 二元運算子兩側應當存在空格
* [**MUST NOT**] 一元運算子右側不應當存在空格
* [**MUST**] 三元運算子前後應當存在空格
* [**MUST**] 若非行末, 逗號、分號、冒號後應當存在空格, 符號前無需空格
* [**MUST**] 語句的括號左側應當存在空格, 內部不需要空格
* [**MUST**] 行註釋前需要空格
* [**MUST**] lambda 箭頭周圍需要空格

### Null 檢查

* [**MUST**] 所有專案必須啟用 Nullable
* [**SHOULD**] 對於可為 Null 的物件, 應當使用 `?` 進行標記
* [**SHOULD**] 使用以下方式進行 Null 檢查

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

### 檔案規範

* [**RECOMMENDED**] 檔名應當與類名一致
* [**SHOULD**] 一個檔案只能存放一個類, 若類過大, 應當考慮拆分
* [**RECOMMENDED**] 對類進行拆分時, 應當單獨開啟一個資料夾存放, 檔名採用 `類名.功能.cs`
* [**RECOMMENDED**] 檔名應當使用 PascalCase
* [**RECOMMENDED**] 檔名應當使用英文
* [**SHOULD**] 對於擴充套件方法, 應當將其放置在單獨的 `Extensions` 資料夾中, 檔名採用 `類名Extensions.cs`

### 註釋規範

* [**SHOULD**] 對於公開的方法, 屬性, 欄位, 建構函式, 應當新增註釋
* [**RECOMMENDED**] 註釋應當符合 XML 註釋規範
* [**MUST**] 使用 `// TODO: <註釋>` 標記未完成的程式碼
* [**SHOULD**] 對於裝飾分割型註釋, 應當使用 `/******** <註釋> ********/` 進行標記, 並保證對齊, 使用不同的長度表示層級

### 異常處理

* [**SHOULD**] 對於異常處理, 應當使用 `try-catch` 進行處理
* [**MUST**] 若需要在 catch 中繼續丟擲異常, 請使用 `throw;` 而不是 `throw err;`
* [**RECOMMENDED**] 不建議使用引發異常代替錯誤返回, 這種情況下建議使用 Result 型別

### 資源釋放

* [**SHOULD**] 對於需要釋放的資源, 應當使用 `using` 進行釋放
* [**SHOULD**] 若存在需要釋放的內容, 應實現 `IDisposable` 介面
* [**SHOULD**] 在 try-catch 語句中存在需要釋放的資源, 應當使用 `finally` 進行釋放

### 其餘規範

* [**SHOULD**] 對於列舉值, 第一個項應當為未知項
* [**SHOULD**] 使用 StringBuilder 進行長字串拼接
* [**RECOMMENDED**] 使用 `ReadOnlySpan` 來減少對記憶體的佔用
* [**SHOULD NOT**] 不建議使用 `struct`
* [**MUST NOT**] 對於重複使用的程式碼, 應當使用方法進行封裝
* [**SHOULD**] 使用 `if (obj is BaseType foo)` 進行型別轉換或者 `as` 運算子


## 修訂規範

如果你想要修改此規範，請按照以下步驟進行：

1. 發起一個 Issue，簡要描述你的修改內容
2. 建立專案 Fork
3. 在 Fork 中建立屬於你的分支，分支名參照: `/draft/<你的名稱>/<修訂的簡介，多個單詞使用 - 分割>`
4. 將 Issue 連線到這個 Fork 的分支
5. 在新的分支中修改程式碼規範
6. 遵循提交模板進行 Pull Request
7. 等待稽覈