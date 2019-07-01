# raywenderlich.com 官方代码风格指南中文版[长期维护项目]

### Updated for Swift 4.2

This style guide is different from others you may see, because the focus is centered on readability for print and the web. We created this style guide to keep the code in our books, tutorials, and starter kits nice and consistent — even though we have many different authors working on the books.

这篇代码风格指南可能不同于你看到的其他代码风格指南。因为它倾向于保证出版物和网页内容的可读性。我们创建这篇代码风格指南的初衷是为了让我们的书、教程和初学者指南中的代码，即使在有很多作者同时协作的情况下，也能保持质量与风格统一。

Our overarching goals are clarity, consistency and brevity, in that order.

总的来说，这份风格指南的目标依次是清晰、一致和简洁。

## 目录/Table of Contents

* [正确性/Correctness](##正确性/Correctness)
* [命名/Naming](##命名/Naming)
  * [在文章中正确引用代码/Prose](###在文章中引用代码/Prose)
  * [代理/Delegates](###代理/Delegates)
  * [使用上下文进行类型推断/Use Type Inferred Context](###使用上下文进行类型推断/Use-Type-Inferred-Context)
  * [通用类型参数/Generics](###泛型/Generics)
  * [类前缀/Class Prefixes](###类前缀/Class-Prefixes)
  * [语言/Language](###语言/Language)
* [代码组织/Code Organization](##代码组织/Code-Organization)
  * [协议一致性/Protocol Conformance](###协议一致性/Protocol-Conformance)
  * [无用代码/Unused Code](###无效代码/Unused-Code)
  * [简化引用/Minimal Imports](###简化引用/Minimal-Imports)
* [空格/Spacing](##空格/Spacing)
* [注释/Comments](##注释/Comments)
* [类与结构体/Classes and Structures](##类和结构体/Classes-and-Structures)
  * [Self 的使用/Use of Self](###Self-的使用/Use-of-Self)
  * [协议一致性/Protocol Conformance](###协议一致性/Protocol-Conformance)
  * [计算型属性/Computed Properties](###计算属性/Computed-Properties)
  * [FinaL 关键字/Final](###Final-关键字/Final)
* [函数声明/Function Declarations](##函数声明/Function-Declarations)
* [函数调用/Function Calls](##函数调用/Function-Calls)
* [闭包表达式/Closure Expressions](##闭包表达式/Closure-Expressions)
* [类型/Types](##类型/Types)
  * [常量/Constants](###常量/Constants)
  * [静态方法和可变类型属性/Static Methods and Variable Type Properties](###静态方法和可变类型属性/Static-Methods-and-Variable-Type-Properties)
  * [可选类型/Optionals](###可选类型/Optionals)
  * [延时初始化/Lazy Initialization](###延迟初始化/Lazy-Initialization)
  * [类型推断/Type Inference](###类型推断/Type-Inference)
  * [语法糖/Syntactic Sugar](###语法糖/Syntactic-Sugar)
* [函数与方法/Functions vs Methods](##函数-vs-方法/Functions-vs-Methods)
* [内存管理/Memory Management](##内存管理/Memory-Management)
  * [延长生命周期/Extending Lifetime](###延长对象的生命周期/Extending-object-lifetime)
* [访问控制/Access Control](##访问控制/Access-Control)
* [控制流/Control Flow](##控制流/Control-Flow)
  * [三元条件表达式/Ternary Operator](###三元条件表达式/Ternary-Operator)
* [黄金路径/Golden Path](##黄金路径/Golden-Path)
  * [失败防护/Failing Guards](###失败防护/Failing-Guards)
* [分号/Semicolons](##分号/Semicolons)
* [括号/Parentheses](##括号/Parentheses)
* [多行字符串字面量/Multi-line String Literals](##多行字符串字面量/Multi-line-String-Literals)
* [不要使用 Emoji/No Emoji](##不要使用-Emoji/No-Emoji)
* [组织名称和包标识/Organization and Bundle Identifier](##组织名称和包标识/Organization-and-Bundle-Identifier)
* [版权声明/Copyright Statement](##版权声明/Copyright-Statement)
* [笑脸/Smiley Face](##笑脸/Smiley-Face)
* [参考资料/References](##参考/References)

## 正确性/Correctness

Strive to make your code compile without warnings. This rule informs many style decisions such as using `#selector` types instead of string literals.

尽量保证代码在编译的过程中不会出现任何警告。这条规则左右了其他规则的制定，例如使用 `#selector` 类型而不是字符串字面量。

## 命名/Naming

Descriptive and consistent naming makes software easier to read and understand. Use the Swift naming conventions described in the [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/). Some key takeaways include:

具有描述性和一致性的命名能够让软件更易于阅读和理解。遵循 [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/) 中描述的命名规范。 下面展示了一些关键点：

* striving for clarity at the call site

* 在调用时力求意图清晰明确。

* prioritizing clarity over brevity

* 传达清晰的意图比文字的简洁更重要。

* using camel case (not snake case)

* 使用驼峰命名法（而不是蛇形命名法）。

  > 译者注：snake case 是指使用下划线的命名方法，[详情参考链接](https://fr.wikipedia.org/wiki/Snake_case)

* using uppercase for types (and protocols), lowercase for everything else

* 类型（和协议）使用首字母大写，其它都是首字母小写。

* including all needed words while omitting needless words

* 包含所有需要的单词，同时省略不必要的单词。

* using names based on roles, not types

* 基于作用命名，而不是类型。

* sometimes compensating for weak type information

* 必要时，为无明确意义的类型补充额外信息。

* striving for fluent usage
* 尽量保证使用上的流畅性

* beginning factory methods with `make`
* 工厂方法要以 `make` 开头

* naming methods for their side effects
* 依据方法的副作用进行命名

  * verb methods follow the -ed, -ing rule for the non-mutating version
  * 针对不可变的场景，动词描述的方法遵循紧跟 -ed, -ing 后缀

    >译者注：verb methods 是指恰好能够被一个动词描述的方法

  * noun methods follow the formX rule for the mutating version
  
  * 针对可变的场景，名词描述的方法遵循 formX 的规则

    > 译者注： formX 中的 X 指代对应的名词，例如 `y.formUnion()` 方法，X 指代 Union

  * boolean types should read like assertions

  * 布尔类型读起来像是断言的感觉

  * protocols that describe _what something is_ should read as nouns

  * _描述事物的_ 协议，读起来应该像名词

  * protocols that describe _a capability_ should end in _-able_ or _-ible_

  * _描述能力_ 的协议，应该使用后缀 _-able_，_ible_

* using terms that don't surprise experts or confuse beginners

* 使用术语的时候，不要让专家觉得惊讶，也不要让初学者感到困惑

* generally avoiding abbreviations

* 通常要避免缩写

* using precedent for names

* 命名可以遵循先例

* preferring methods and properties to free functions

* 优先选择方法或属性，而非全局函数。

> 译者注：free function 在这里翻译为全局函数，[详情请点击这里](https://en.wikipedia.org/wiki/Free_function)

* casing acronyms and initialisms uniformly up or down

* 首字母缩写的单词要根据惯例保持全大小或者全小写的方式

* giving the same base name to methods that share the same meaning

* 当某些方法的含义基本一致时，那么它们可以共享一个基础方法名。

* avoiding overloads on return type

* 避免“重载返回类型”

* choosing good parameter names that serve as documentation

* 选择具有说明作用的形参名，能够让文档注释质量更高

* preferring to name the first parameter instead of including its name in the method name, except as mentioned under Delegates

* 尽量为第一个参数设置参数标签，不要将此参数标签放在方法名中，在代理模式下的方法可以忽略此规定。

* labeling closure and tuple parameters

* 为闭包和元组参数设置标签

* taking advantage of default parameters

* 利用默认参数带来的优势

### 在文章中引用代码/Prose

When referring to methods in prose, being unambiguous is critical. To refer to a method name, use the simplest form possible.

在文章中引用方法时，含义明确是至关重要的。尽可能用最简单的形式引用方法。

1. Write the method name with no parameters.  **Example:** Next, you need to call `addTarget`.

* 写一个不带参数的方法。**例如**：下一步，你需要调用方法 `addTarget`。

2. Write the method name with argument labels.  **Example:** Next, you need to call `addTarget(_:action:)`.

* 写一个带参数标签的方法。**例如**：下一步，你需要调用方法 `addTarget(_:action:)`。

3. Write the full method name with argument labels and types. **Example:** Next, you need to call `addTarget(_: Any?, action: Selector?)`.

* 写一个带参数标签和参数类型的完整方法。**例如**：下一步, 你需要调用方法 `addTarget(_: Any?, action: Selector?)`。

For the above example using `UIGestureRecognizer`, 1 is unambiguous and preferred.

上面是一个使用 `UIGestureRecognizer` 的例子, 1 的表述简单明了，也是应当被首先采用的描述方式。

**Pro Tip:** You can use Xcode's jump bar to lookup methods with argument labels. If you’re particularly good at mashing lots of keys simultaneously, put the cursor in the method name and press **Shift-Control-Option-Command-C** (all 4 modifier keys) and Xcode will kindly put the signature on your clipboard.

**小提示：** 你可以使用 Xcode 的 jump bar 来查看方法的参数标签。如果你能够相对轻松的操作多个按键，那么可以尝试将光标放在方法名上，并同时按下  **Shift-Control-Option-Command-C** 键，此时 Xcode 会将此方法的签名复制到剪贴板上。

  > 译者注：与复制相关的快捷操作有三种，需要注意的是在 playground 中这些方法不生效
  >  
  > * **command+C** ：Copy（光标所在位置的单词）：`viewDidLoad`
  > * **control+shift+command+C**：Copy Symbol Name（光标所在位置的消息符号名称）：`viewDidLoad()`
  > * **option+control+shift+command+C**：Copy Qualified Symbol Name（光标所在位置的消息符号全名，带所属类名）：`ViewController.viewDidLoad()`

![Methods in Xcode jump bar](screens/xcode-jump-bar.png)

### 类前缀/Class Prefixes

Swift types are automatically namespaced by the module that contains them and you should not add a class prefix such as RW. If two names from different modules collide you can disambiguate by prefixing the type name with the module name. However, only specify the module name when there is possibility for confusion which should be rare.

Swift 里各种类型被其所处的模块自动分配了命名空间。不应该再添加类似于 RW 的类前缀。如果不同模块间的两个类型命名冲突，可以在类型名前添加模块名来消除歧义。无论如何，仅在少数可能引起混淆的情况下指明模块名。

```swift
import SomeModule

let myClass = MyModule.UsefulClass()
```

### 代理/Delegates

When creating custom delegate methods, an unnamed first parameter should be the delegate source. (UIKit contains numerous examples of this.)

当创建自定义的代理方法时，第一个未命名的参数应该是代理源。（ UIKit 包含很多类似的例子）

**推荐（Preferred）**:

```swift
func namePickerView(_ namePickerView: NamePickerView, didSelectName name: String)
func namePickerViewShouldReload(_ namePickerView: NamePickerView) -> Bool
```

**不推荐（Not Preferred）**:

```swift
func didSelectName(namePicker: NamePickerViewController, name: String)
func namePickerShouldReload() -> Bool
```

### 使用上下文进行类型推断/Use Type Inferred Context

Use compiler inferred context to write shorter, clear code.  (Also see [Type Inference](#type-inference).)

利用编译器根据上下文进行类型推断的能力，书写更简洁明了的代码。（你也可以阅读 [类型推断](#type-inference)。)

**推荐（Preferred）**:

```swift
let selector = #selector(viewDidLoad)
view.backgroundColor = .red
let toView = context.view(forKey: .to)
let view = UIView(frame: .zero)
```

**不推荐（Not Preferred）**:

```swift
let selector = #selector(ViewController.viewDidLoad)
view.backgroundColor = UIColor.red
let toView = context.view(forKey: UITransitionContextViewKey.to)
let view = UIView(frame: CGRect.zero)
```

### 泛型/Generics

Generic type parameters should be descriptive, upper camel case names. When a type name doesn't have a meaningful relationship or role, use a traditional single uppercase letter such as `T`, `U`, or `V`.

泛型的类型参数应该遵循大写驼峰法命名规则且具有较强的描述性。当类型参数与函数或泛型之间无明显任何有意义的关联时，通常使用单个大写字母来命名，例如 `T` 、`U` 或 `V`。

**推荐（Preferred）**:

```swift
struct Stack<Element> { ... }
func write<Target: OutputStream>(to target: inout Target)
func swap<T>(_ a: inout T, _ b: inout T)
```

**不推荐（Not Preferred）**:

```swift
struct Stack<T> { ... }
func write<target: OutputStream>(to target: inout target)
func swap<Thing>(_ a: inout Thing, _ b: inout Thing)
```

### 语言/Language

Use US English spelling to match Apple's API.

使用美式英语拼写来匹配 Apple 的 API。

**推荐（Preferred）**:

```swift
let color = "red"
```

**不推荐（Not Preferred）**:

```swift
let colour = "red"
```

## 代码组织/Code Organization

Use extensions to organize your code into logical blocks of functionality. Each extension should be set off with a `// MARK: -` comment to keep things well-organized.

利用扩展的特性将代码组织成各个不同的功能逻辑块。每个扩展都应该添加 `// MARK: -` 注释符号，以保证代码的结构清晰。

### 协议一致性/Protocol Conformance

In particular, when adding protocol conformance to a model, prefer adding a separate extension for the protocol methods. This keeps the related methods grouped together with the protocol and can simplify instructions to add a protocol to a class with its associated methods.

通常来说，当遵循某个协议后，推荐将与该协议相关的方法统一到某个单独的扩展中。这会让与协议相关的方法聚集在一起，也将简化整体的代码结构。

**推荐（Preferred）**:

```swift
class MyViewController: UIViewController {
  // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate methods
}
```

**不推荐（Not Preferred）**:

```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all methods
}
```

Since the compiler does not allow you to re-declare protocol conformance in a derived class, it is not always required to replicate the extension groups of the base class. This is especially true if the derived class is a terminal class and a small number of methods are being overridden. When to preserve the extension groups is left to the discretion of the author.

因为编译器不允许你在派生类中重新声明已经遵守的协议，所以你并不总需要重复基类扩展里的相关代码。这在派生类是一个终端类且只有很少的方法需要重写的情况下十分常见。何时保留扩展组将由开发者自行决定。

For UIKit view controllers, consider grouping lifecycle, custom accessors, and IBAction in separate class extensions.

对于 UIKit 中的视图控制器，可考虑将生命周期、自定义存取器和 IBAction 分组在单独的类扩展中。

### 无效代码/Unused Code

Unused (dead) code, including Xcode template code and placeholder comments should be removed. An exception is when your tutorial or book instructs the user to use the commented code.

像 Xcode 模板工程代码和占位注释这样的无用代码，应该被移除掉。但教程或书籍中用于指导用户使用的注释代码除外。

Aspirational methods not directly associated with the tutorial whose implementation simply calls the superclass should also be removed. This includes any empty/unused UIApplicationDelegate methods.

对于仅实现简单的调用父类，且与教程无直接关联的方法也应该被移除。这里包括任何为空的或无用的 UIApplicationDelegate 方法。

**推荐（Preferred）**:

```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  return Database.contacts.count
}
```

**不推荐（Not Preferred）**:

```swift
override func didReceiveMemoryWarning() {
  super.didReceiveMemoryWarning()
  // Dispose of any resources that can be recreated.
}

override func numberOfSections(in tableView: UITableView) -> Int {
  // #warning Incomplete implementation, return the number of sections
  return 1
}

override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  // #warning Incomplete implementation, return the number of rows
  return Database.contacts.count
}

```

### 简化引用/Minimal Imports

Import only the modules a source file requires. For example, don't import `UIKit` when importing `Foundation` will suffice. Likewise, don't import `Foundation` if you must import `UIKit`.

只引用必要的文件。举个例子，引用 `Foundation` 就足够的情况下不要再引用 `UIKit` 。同样，需要引用 `UIKit` 的时候，就不要引用 `Foundation`。

**推荐（Preferred）**:  

```swift
import UIKit
var view: UIView
var deviceModels: [String]
```

**推荐（Preferred）**:

```swift
import Foundation
var deviceModels: [String]
```

**不推荐（Not Preferred）**:

```swift
import UIKit
import Foundation
var view: UIView
var deviceModels: [String]
```

**不推荐（Not Preferred）**:

```swift
import UIKit
var deviceModels: [String]
```

## 空格/Spacing

* Indent using 2 spaces rather than tabs to conserve space and help prevent line wrapping. Be sure to set this preference in Xcode and in the Project settings as shown below:

* 用两个字符缩进比用制表符缩进更节省空间，同时能防止换行。务必在 Xcode 和项目中设置这个偏好，如下所示：

![Xcode indent settings](screens/indentation.png)

* Method braces and other braces (`if`/`else`/`switch`/`while` etc.) always open on the same line as the statement but close on a new line.

* 方法的大括号和其他大括号（ `if` / `else` / `switch` / `while` 等）总是在和语句相同的行写左括号，而在新行写右括号。

* Tip: You can re-indent by selecting some code (or **Command-A** to select all) and then **Control-I** (or **Editor ▸ Structure ▸ Re-Indent** in the menu). Some of the Xcode template code will have 4-space tabs hard coded, so this is a good way to fix that.

* 提示：你可以通过选中一些代码（或按 **Command-A** 选中全部）然后按 **Control-I** （或在目录中选择**Editor ▸ Structure ▸ Re-Indent**）的方式来重新缩进代码。一些 Xcode 模板代码会使用 4 个空格的制表符硬编码，这就是一个修正它的好方法。

**推荐（Preferred）**:

```swift
if user.isHappy {
  // Do something
} else {
  // Do something else
}
```

**不推荐（Not Preferred）**:

```swift
if user.isHappy
{
  // Do something
}
else {
  // Do something else
}
```

* There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but having too many sections in a method often means you should refactor into several methods.

* 方法之间应该只有一个空行，这样有助于视觉清晰和组织。方法中的空白应该按功能分隔代码，但在一个方法中有很多段意味着你应该将它们封装进不同的方法。

* There should be no blank lines after an opening brace or before a closing brace.
* 在左括号之后或者右括号之前没有独立的空行

* Colons always have no space on the left and one space on the right. Exceptions are the ternary operator `? :`, empty dictionary `[:]` and `#selector` syntax `addTarget(_:action:)`.

* 冒号总是在左边没有空格而右边有空格。比较特殊的是三元运算符 `? :`、空字典 `[:]` 和 `#selector` 语法里的方法名，例如 `addTarget(_:action:)` .

**推荐（Preferred）**:

```swift
class TestDatabase: Database {
  var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

**不推荐（Not Preferred）**:

```swift
class TestDatabase : Database {
  var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```

* Long lines should be wrapped at around 70 characters. A hard limit is intentionally not specified.
* 当一行的字符数达到 70 个左右的时候就应该换行，这里并非硬性限制，可自行调整。

* Avoid trailing whitespaces at the ends of lines.
* 避免在行结尾的地方附上空白。

* Add a single newline character at the end of each file.
* 在每个文件的结尾处增加一个单独的换行符。

## 注释/Comments

When they are needed, use comments to explain **why** a particular piece of code does something. Comments must be kept up-to-date or deleted.

需要的时候，用注释来解释**为什么**这个代码片段要做这些事情。注释如果不能保持最新的状态，就应当被删除。

Avoid block comments inline with code, as the code should be as self-documenting as possible. _Exception: This does not apply to those comments used to generate documentation._

避免在代码中出现大块的代码注释，代码应该尽可能自文档化。 _例外：这条规则不适用于那些被用于生成文档的注释。_

> 译者注：[详情见链接](https://github.com/raywenderlich/swift-style-guide/issues/310)

Avoid the use of C-style comments (`/* ... */`). Prefer the use of double- or triple-slash.

避免使用 C 风格的注释方式(`/* ... */`)，尽量使用2个或3个斜杠的方式进行注释。

## 类和结构体/Classes and Structures

### 如何选择/Which one to use?

Remember, structs have [value semantics](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_144). Use structs for things that do not have an identity. An array that contains [a, b, c] is really the same as another array that contains [a, b, c] and they are completely interchangeable. It doesn't matter whether you use the first array or the second, because they represent the exact same thing. That's why arrays are structs.

请记住，结构体有[值语义]((https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_144))。对没有标识的事物应用结构体。一个包含 [a, b, c] 的数组和另一个包含 [a, b, c] 的数组是完全一样的。他们是可以完全互换的。使用第一个数组还是第二个数组都无所谓，因为他们代表着完全相同的事物。这就是为什么数组是结构体。

Classes have [reference semantics](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_145). Use classes for things that do have an identity or a specific life cycle. You would model a person as a class because two person objects are two different things. Just because two people have the same name and birthdate, doesn't mean they are the same person. But the person's birthdate would be a struct because a date of 3 March 1950 is the same as any other date object for 3 March 1950. The date itself doesn't have an identity.

类有[引用语义](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_145)。对有标识或有具体生命周期的事物应用类。你需要将人建模为一个类，因为不同两个人对象是两个不同的事物。只是因为两个人拥有相同的名字和生日不意味着他们是同一个人。但是人的生日应该是一个结构体，因为 1950 年 3 月 3 日和任何其它的 1950 年 3 月 3 日日期对象是相同的。日期本身没有标识。

Sometimes, things should be structs but need to conform to `AnyObject` or are historically modeled as classes already (`NSDate`, `NSSet`). Try to follow these guidelines as closely as possible.

有时，事物本应该是结构体，但需要遵循 `AnyObject`，或由于历史原因已经被建模为类 （`NSDate` 、 `NSSet`）。不管怎样，都请尽可能遵循前面提到的原则。

### 示例/Example definition

Here's an example of a well-styled class definition:

下面是一个代码风格良好的类定义示例：

```swift
class Circle: Shape {
  var x: Int, y: Int
  var radius: Double
  var diameter: Double {
    get {
      return radius * 2
    }
    set {
      radius = newValue / 2
    }
  }

  init(x: Int, y: Int, radius: Double) {
    self.x = x
    self.y = y
    self.radius = radius
  }

  convenience init(x: Int, y: Int, diameter: Double) {
    self.init(x: x, y: y, radius: diameter / 2)
  }

  override func area() -> Double {
    return Double.pi * radius * radius
  }
}

extension Circle: CustomStringConvertible {
  var description: String {
    return "center = \(centerString) area = \(area())"
  }
  private var centerString: String {
    return "(\(x),\(y))"
  }
}
```

The example above demonstrates the following style guidelines:

上面的例子遵循了以下代码规范：

* Specify types for properties, variables, constants, argument declarations and other statements with a space after the colon but not before, e.g. `x: Int`, and `Circle: Shape`.

* 遵循冒号前有空格，冒号后无空格的规则，并应用在属性、变量、常量、参数声明和其它类型的语句中，例如：`x: Int` 和 `Circle: Shape`。

* Define multiple variables and structures on a single line if they share a common purpose / context.

* 如果多个变量和结构体共享一个共同的目的 / 上下文，则可以在同一行中定义。

* Indent getter and setter definitions and property observers.
* 缩进 getter、setter 的定义和属性观察器。

* Don't add modifiers such as `internal` when they're already the default. Similarly, don't repeat the access modifier when overriding a method.

* 不要将默认的修饰符重复添加到代码中，例如 `internal` 关键字。类似的，当重写一个方法时，不要再重复添加与访问权限相关的修饰符。

* Organize extra functionality (e.g. printing) in extensions.
* 在扩展中组织额外功能（例如打印）。

* Hide non-shared, implementation details such as `centerString` inside the extension using `private` access control.

* 隐藏非共享的实现细节，例如 `centerString` 在扩展中使用 `private` 级别的访问控制。

### Self 的使用/Use of Self

For conciseness, avoid using `self` since Swift does not require it to access an object's properties or invoke its methods.

为了简洁，请避免使用 `self` 关键词，Swift 不需要用它来访问一个对象属性或调用它的方法。

Use self only when required by the compiler (in `@escaping` closures, or in initializers to disambiguate properties from arguments). In other words, if it compiles without `self` then omit it.

仅在编译器需要时（在 `@escaping` 闭包或初始化函数中，消除参数与属性的歧义）才使用 self。换句话说，如果不需要 `self` 就能编译通过，则可以忽略它。

### 计算属性/Computed Properties

For conciseness, if a computed property is read-only, omit the get clause. The get clause is required only when a set clause is provided.

为了简洁，如果一个计算属性是只读的，则可以忽略 get 子句。仅在提供了 set 子句的情况下才需要 get 子句。

**推荐（Preferred）**:

```swift
var diameter: Double {
  return radius * 2
}
```

**不推荐（Not Preferred）**:

```swift
var diameter: Double {
  get {
    return radius * 2
  }
}
```

### Final 关键字/Final

Marking classes or members as `final` in tutorials can distract from the main topic and is not required. Nevertheless, use of `final` can sometimes clarify your intent and is worth the cost. In the below example, `Box` has a particular purpose and customization in a derived class is not intended. Marking it `final` makes that clear.

在教程中将类或成员标记为 `final` 会发散主题，且不是必需的。尽管如此，`final` 的使用有时可以明确你的意图，且值得你这样做。在下面的例子中，`Box`有特定的用途，且不打算在派生类中进行自定义。标记为 `final` 可以使它更清晰。

```swift
// Turn any generic type into a reference type using this Box class.
final class Box<T> {
  let value: T
  init(_ value: T) {
    self.value = value
  }
}
```

## 函数声明/Function Declarations

Keep short function declarations on one line including the opening brace:

保持函数的声明在一行以内，包括左括号：

```swift
func reticulateSplines(spline: [Double]) -> Bool {
  // reticulate code goes here
}
```

For functions with long signatures, put each parameter on a new line and add an extra indent on subsequent lines:

对于函数名较长的情况，则需要保证每个参数新起一行，且在该行的开始处添加一个换行符：

```swift
func reticulateSplines(
  spline: [Double],
  adjustmentFactor: Double,
  translateConstant: Int, comment: String
) -> Bool {
  // reticulate code goes here
}
```

Don't use `(Void)` to represent the lack of an input; simply use `()`. Use `Void` instead of `()` for closure and function outputs.

不要使用 `(Void)` 来表示入参为空的情况，用 `()` 即可。在 闭包和函数的输出参数为空的情况时，推荐使用 `Void`, 而不是 `()`

**推荐（Preferred）**:

```swift
func updateConstraints() -> Void {
  // magic happens here
}

typealias CompletionHandler = (result) -> Void
```

**不推荐（Not Preferred）**:

```swift
func updateConstraints() -> () {
  // magic happens here
}

typealias CompletionHandler = (result) -> ()
```

## 函数调用/Function Calls

Mirror the style of function declarations at call sites. Calls that fit on a single line should be written as such:

在调用时呈现出函数声明时的样式。如果调用函数只需要一行就可以完成，应当像下面一样组织代码。

```swift
let success = reticulateSplines(splines)
```

If the call site must be wrapped, put each parameter on a new line, indented one additional level:

当函数调用的时候必须换行的情况想，需要让每个参数新起一行并添加缩进。

```swift
let success = reticulateSplines(
  spline: splines,
  adjustmentFactor: 1.3,
  translateConstant: 2,
  comment: "normalize the display")
```

## 闭包表达式/Closure Expressions

Use trailing closure syntax only if there's a single closure expression parameter at the end of the argument list. Give the closure parameters descriptive names.

仅在参数列表最后有个单独的闭包表达式参数时，使用尾随闭包语法。给闭包参数定义一个描述性的命名。

**推荐（Preferred）**:

```swift
UIView.animate(withDuration: 1.0) {
  self.myView.alpha = 0
}

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}, completion: { finished in
  self.myView.removeFromSuperview()
})
```

**不推荐（Not Preferred）**:

```swift
UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
})

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}) { f in
  self.myView.removeFromSuperview()
}
```

For single-expression closures where the context is clear, use implicit returns:

对于上下文清晰的单独表达式闭包，使用隐式返回：

```swift
attendeeList.sort { a, b in
  a > b
}
```

Chained methods using trailing closures should be clear and easy to read in context. Decisions on spacing, line breaks, and when to use named versus anonymous arguments is left to the discretion of the author. Examples:

链式方法结合尾随闭包的使用场景应当保证代码清晰且可读性强。作者将自行抉择空格、换行、何时使用具名参数，还是匿名参数等问题。举例：

```swift
let value = numbers.map { $0 * 2 }.filter { $0 % 3 == 0 }.index(of: 90)

let value = numbers
  .map {$0 * 2}
  .filter {$0 > 50}
  .map {$0 + 10}
```

## 类型/Types

Always use Swift's native types and expressions when available. Swift offers bridging to Objective-C so you can still use the full set of methods as needed.

请尽可能多的使用 Swift 原生类型。 Swift 提供了 Objective-C 桥接，所以当你需要的时候你仍然可以使用对应的方法。

**推荐（Preferred）**:

```swift
let width = 120.0                                    // Double
let widthString = "\(width)"                         // String
```

**可接受（Less Preferred）**:

```swift
let width = 120.0                                    // Double
let widthString = (width as NSNumber).stringValue    // String
```

**不推荐（Not Preferred）**:

```swift
let width: NSNumber = 120.0                          // NSNumber
let widthString: NSString = width.stringValue        // NSString
```

In drawing code, use `CGFloat` if it makes the code more succinct by avoiding too many conversions.

在绘制相关的代码中，使用 `CGFloat` 可以避免代码频繁的转换，从而让你的代码更加简洁。

### 常量/Constants

Constants are defined using the `let` keyword and variables with the `var` keyword. Always use `let` instead of `var` if the value of the variable will not change.

使用 `let` 关键字来定义常量，使用 `var` 关键字来定义变量。如果变量的值不会改变，则要使用 `let` 来代替 `var` 。

**Tip:** A good technique is to define everything using `let` and only change it to `var` if the compiler complains!

**提示**: 一个比较好的技巧就是所有东西都优先使用 `let` , 当编译器警告的时候再改为 `var` 。

You can define constants on a type rather than on an instance of that type using type properties. To declare a type property as a constant simply use `static let`. Type properties declared in this way are generally preferred over global constants because they are easier to distinguish from instance properties. Example:

You can define constants on a type rather than on an instance of that type using type properties. 使用 `static let` 去声明一个类型属性作为常量。相比于全局变量声明常量的方式，更推荐用这种方式声明常量，因为这种方式更能和实例属性区分开。举例：

**推荐（Preferred）**:

```swift
enum Math {
  static let e = 2.718281828459045235360287
  static let root2 = 1.41421356237309504880168872
}

let hypotenuse = side * Math.root2

```

**Note:** The advantage of using a case-less enumeration is that it can't accidentally be instantiated and works as a pure namespace.

**注意：** 使用无枚举值的枚举类型时，它的一大优势就是不会被意外的实例化，而只是单纯的作为一个命名空间。

**不推荐（Not Preferred）**:

```swift
let e = 2.718281828459045235360287  // pollutes global namespace
let root2 = 1.41421356237309504880168872

let hypotenuse = side * root2 // what is root2?
```

### 静态方法和可变类型属性/Static Methods and Variable Type Properties

Static methods and type properties work similarly to global functions and global variables and should be used sparingly. They are useful when functionality is scoped to a particular type or when Objective-C interoperability is required.

静态方法和类型属性跟全局函数和全局变量的工作原理类似，应当谨慎使用。当功能的作用域是一个特定类型或需要与 Objective-C 交互时，它们非常有用。

### 可选类型/Optionals

Declare variables and function return types as optional with `?` where a `nil` value is acceptable.

在可接受 `nil` 值的情况下，使用 `?` 声明变量和函数返回类型为可选类型。

Use implicitly unwrapped types declared with `!` only for instance variables that you know will be initialized later before use, such as subviews that will be set up in `viewDidLoad()`. Prefer optional binding to implicitly unwrapped optionals in most other cases.

用 `!` 声明的隐式解包类型，适用于在使用前一定能被正确初始化的实例变量，比如子视图会在 `viewDidLoad` 中创建。大多数场景下，倾向使用可选绑定而不是隐式解包类型。

When accessing an optional value, use optional chaining if the value is only accessed once or if there are many optionals in the chain:

当访问一个可选值时，如果值仅被访问一次或在调用链中有许多值时，使用可选链：

```swift
textContainer?.textLabel?.setNeedsDisplay()
```

Use optional binding when it's more convenient to unwrap once and perform multiple operations:

when it's more convenient to unwrap once 且之后要执行多步操作的场景下，使用可选绑定：

```swift
if let textContainer = textContainer {
  // do many things with textContainer
}
```

When naming optional variables and properties, avoid naming them like `optionalString` or `maybeView` since their optional-ness is already in the type declaration.

在命名可选变量和属性时，需避免类似 `optionalString` 或 `maybeView` 这样的命名，因为他们的可选性已经体现在类型声明中了。

For optional binding, shadow the original name whenever possible rather than using names like `unwrappedView` or `actualLabel`.

对于可选绑定，适当时使用原始名称，而不是使用像 `unwrappedView` 或 `actualLabel` 这样的名称。

**推荐（Preferred）**:

```swift
var subview: UIView?
var volume: Double?

// later on...
if let subview = subview, let volume = volume {
  // do something with unwrapped subview and volume
}

// another example
UIView.animate(withDuration: 2.0) { [weak self] in
  guard let self = self else { return }
  self.alpha = 1.0
}
```

**不推荐（Not Preferred）**:

```swift
var optionalSubview: UIView?
var volume: Double?

if let unwrappedSubview = optionalSubview {
  if let realVolume = volume {
    // do something with unwrappedSubview and realVolume
  }
}

// another example
UIView.animate(withDuration: 2.0) { [weak self] in
  guard let strongSelf = self else { return }
  strongSelf.alpha = 1.0
}
```

### 延迟初始化/Lazy Initialization

Consider using lazy initialization for finer grained control over object lifetime. This is especially true for `UIViewController` that loads views lazily. You can either use a closure that is immediately called `{ }()` or call a private factory method. Example:

在更细粒度地控制对象声明周期时考虑使用延迟初始化。对于 `UIViewController` ，延迟初始化视图是非常正确的。你也可以直接调用 `{ }()` 的闭包或调用私有工厂方法。例如：

```swift
lazy var locationManager = makeLocationManager()

private func makeLocationManager() -> CLLocationManager {
  let manager = CLLocationManager()
  manager.desiredAccuracy = kCLLocationAccuracyBest
  manager.delegate = self
  manager.requestAlwaysAuthorization()
  return manager
}
```

**注意/Notes:**

* `[unowned self]` is not required here. A retain cycle is not created.

* 因为没有发生循环引用，所以这里不需要 `[unowned self]`。

* Location manager has a side-effect for popping up UI to ask the user for permission so fine grain control makes sense here.

* 位置管理器向用户申请权限时，有弹出 UI 界面的副作用，所以细颗粒地控制在这里是有意义的。

### 类型推断/Type Inference

Prefer compact code and let the compiler infer the type for constants or variables of single instances. Type inference is also appropriate for small, non-empty arrays and dictionaries. When required, specify the specific type such as `CGFloat` or `Int16`.

优先选择简洁紧凑的代码，让编译器为单个实例的常量或变量推断类型。类型推断也适合于小型的，非空的数组和字典。当数据是一些特殊类型，如 `CGFloat` 或 `Int16`时，请指明此特定类型。

**推荐（Preferred）**:

```swift
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5
```

**不推荐（Not Preferred）**:

```swift
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
var names = [String]()
```

#### 空数组和空字典的类型注释/Type Annotation for Empty Arrays and Dictionaries

For empty arrays and dictionaries, use type annotation. (For an array or dictionary assigned to a large, multi-line literal, use type annotation.)

为空数组和空字典使用类型注释。(适用于分配给大型的、多行字面量的数组和字典，使用类型注释。)

**推荐（Preferred）**:

```swift
var names: [String] = []
var lookup: [String: Int] = [:]
```

**不推荐（Not Preferred）**:

```swift
var names = [String]()
var lookup = [String: Int]()
```

**NOTE**: Following this guideline means picking descriptive names is even more important than before.

**注意**：遵循此原则意味着选择描述性命名比之前更重要。

### 语法糖/Syntactic Sugar

Prefer the shortcut versions of type declarations over the full generics syntax.

推荐使用简短版本的类型声明，而不是完整的泛型语法。

**推荐（Preferred）**:

```swift
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
```

**不推荐（Not Preferred）**:

```swift
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```

## 函数 vs 方法/Functions vs Methods

Free functions, which aren't attached to a class or type, should be used sparingly. When possible, prefer to use a method instead of a free function. This aids in readability and discoverability.

不附属于类或类型的全局函数应该被谨慎使用。可能的话，首选方法而不是全局函数。这有助于提升可读性，也更容易被检索到。

Free functions are most appropriate when they aren't associated with any particular type or instance.

全局函数最适用于它们与任何特定类或实例无关的情况。

**推荐（Preferred）**:

```swift
let sorted = items.mergeSorted()  // easily discoverable
rocket.launch()  // acts on the model
```

**不推荐（Not Preferred）**:

```swift
let sorted = mergeSort(items)  // hard to discover
launch(&rocket)
```

**适合全局函数的场景/Free Function Exceptions**

```swift
let tuples = zip(a, b)  // feels natural as a free function (symmetry)
let value = max(x, y, z)  // another free function that feels natural
```

## 内存管理/Memory Management

Code (even non-production, tutorial demo code) should not create reference cycles. Analyze your object graph and prevent strong cycles with `weak` and `unowned` references. Alternatively, use value types (`struct`, `enum`) to prevent cycles altogether.

代码（即使是非生产环境、教程演示的代码）都不应该出现循环引用。分析你的对象关系图并用 `weak` 和 `unowned` 来防止循环引用。或者使用值类型（ `struct`、`enum` ）来杜绝循环引用。

### 延长对象的生命周期/Extending object lifetime

Extend object lifetime using the `[weak self]` and `guard let self = self else { return }` idiom. `[weak self]` is preferred to `[unowned self]` where it is not immediately obvious that `self` outlives the closure. Explicitly extending lifetime is preferred to optional chaining.

使用惯用语法 `[weak self]` 和 `guard let self = self else { return }` 来延长对象的生命周期。 在 `self` 超出闭包生命周期不明显的状况下，优先使用 `[weak self]` 而不是 `[unowned self]`。 利用固定代码明确延长对象的生命周期优于可选链的书写方式。

**推荐（Preferred）**:

```swift
resource.request().onComplete { [weak self] response in
  guard let self = self else {
    return
  }
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**不推荐（Not Preferred）**:

```swift
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**不推荐（Not Preferred）**:

```swift
// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
  let model = self?.updateModel(response)
  self?.updateUI(model)
}
```

## 访问控制/Access Control

Full access control annotation in tutorials can distract from the main topic and is not required. Using `private` and `fileprivate` appropriately, however, adds clarity and promotes encapsulation. Prefer `private` to `fileprivate`; use `fileprivate` only when the compiler insists.

在教程中，完整的访问控制注释会分散主题且是不必要的。然而，适时地使用 `private` 和 `fileprivate` 会使代码更加清晰，也会有助于封装。 在合理情况下，`private` 要优于 `fileprivate`。 使用扩展可能会要求你使用 `fileprivate`。

Only explicitly use `open`, `public`, and `internal` when you require a full access control specification.

只有需要完整的访问控制规范时，才显式地使用 `open` 、 `public` 和 `internal`。

Use access control as the leading property specifier. The only things that should come before access control are the `static` specifier or attributes such as `@IBAction`, `@IBOutlet` and `@discardableResult`.

将访问控制用作前置属性说明符。仅有 `static` 说明符或诸如 `@IBAction` 、`@IBOutlet` 和 `@discardableResult` 标志应该放在访问控制符前面。

**推荐（Preferred）**:

```swift
private let message = "Great Scott!"

class TimeMachine {  
  private dynamic lazy var fluxCapacitor = FluxCapacitor()
}
```

**不推荐（Not Preferred）**:

```swift
fileprivate let message = "Great Scott!"

class TimeMachine {  
  lazy dynamic private var fluxCapacitor = FluxCapacitor()
}
```

## 控制流/Control Flow

Prefer the `for-in` style of `for` loop over the `while-condition-increment` style.

优先选择 `for` 循环的 `for-in` 格式而不是 `while-condition-increment` 风格的循环。

**推荐（Preferred）**:

```swift
for _ in 0..<3 {
  print("Hello three times")
}

for (index, person) in attendeeList.enumerated() {
  print("\(person) is at position #\(index)")
}

for index in stride(from: 0, to: items.count, by: 2) {
  print(index)
}

for index in (0...3).reversed() {
  print(index)
}
```

**不推荐（Not Preferred）**:

```swift
var i = 0
while i < 3 {
  print("Hello three times")
  i += 1
}


var i = 0
while i < attendeeList.count {
  let person = attendeeList[i]
  print("\(person) is at position #\(i)")
  i += 1
}
```

### 三元条件表达式/Ternary Operator

The Ternary operator, `?:` , should only be used when it increases clarity or code neatness. A single condition is usually all that should be evaluated. Evaluating multiple conditions is usually more understandable as an `if` statement or refactored into instance variables. In general, the best use of the ternary operator is during assignment of a variable and deciding which value to use.

当三元条件表达式能够让代码更清晰或者让代码更加整洁时，才被采用。即使是单个条件分支也需要进行判断。而在存在多个条件分支时，结合着 `if` 语句或者将相关代码重构为实例变量的方式，能够降低整体的理解难度。总体而言，使用三元条件表达式的最佳场景就是赋值变量并为变量选择值的时候。

**推荐（Preferred）**:

```swift
let value = 5
result = value != 0 ? x : y

let isHorizontal = true
result = isHorizontal ? x : y
```

**不推荐（Not Preferred）**:

```swift
result = a > b ? x = c > d ? c : d : y
```

## 黄金路径/Golden Path

When coding with conditionals, the left-hand margin of the code should be the "golden" or "happy" path. That is, don't nest `if` statements. Multiple return statements are OK. The `guard` statement is built for this.

当使用条件语句编码时，代码的左边距应该是“黄金”或“快乐”的路径。换句话说，就是不要嵌套 `if` 语句。多个返回语句是可以的。`guard` 语句就是因为避免这个问题而创建的。

**推荐（Preferred）**:

```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

  guard let context = context else {
    throw FFTError.noContext
  }
  guard let inputData = inputData else {
    throw FFTError.noInputData
  }

  // use context and input to compute the frequencies
  return frequencies
}
```

**不推荐（Not Preferred）**:

```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

  if let context = context {
    if let inputData = inputData {
      // use context and input to compute the frequencies

      return frequencies
    } else {
      throw FFTError.noInputData
    }
  } else {
    throw FFTError.noContext
  }
}
```

When multiple optionals are unwrapped either with `guard` or `if let`, minimize nesting by using the compound version when possible. In the compound version, place the `guard` on its own line, then indent each condition on its own line. The `else` clause is indented to match the conditions and the code is indented one additional level, as shown below. Example:

当用 `guard` 或 `if let` 解包多个可选值时，在条件允许的状态下，尽量使用混合的方式来简化嵌套。在混合的方式中，将 `guard` 关键字放在句子的最开始处，并缩进与此相关的条件分支。`else` 闭包的缩进与之前的条件分支一致，但闭包里面代码需要再缩进一级。就像下面的示例一样：

**推荐（Preferred）**:

```swift
guard
  let number1 = number1,
  let number2 = number2,
  let number3 = number3
  else {
    fatalError("impossible")
}
// do something with numbers
```

**不推荐（Not Preferred）**:

```swift
if let number1 = number1 {
  if let number2 = number2 {
    if let number3 = number3 {
      // do something with numbers
    } else {
      fatalError("impossible")
    }
  } else {
    fatalError("impossible")
  }
} else {
  fatalError("impossible")
}
```

### 失败防护/Failing Guards

Guard statements are required to exit in some way. Generally, this should be simple one line statement such as `return`, `throw`, `break`, `continue`, and `fatalError()`. Large code blocks should be avoided. If cleanup code is required for multiple exit points, consider using a `defer` block to avoid cleanup code duplication.

在某些退出代码的情况下，防护语句是必不可少的。一般地，它应该是一行简洁的语句，比如： `return`、`throw`、`break`、`continue` 和 `fatalError()`。应该避免大量的代码块。如果与清理相关的代码被用在多个退出点，则可以考虑用 `defer` 块来避免代码的重复。

## 分号/Semicolons

Swift does not require a semicolon after each statement in your code. They are only required if you wish to combine multiple statements on a single line.

在 Swift 中，每条代码语句后面都不需要加分号。只有在你希望在一行中结合多条语句，才需要加分号。

Do not write multiple statements on a single line separated with semicolons.

不要在用分号分隔的单行中写多条语句。

**推荐（Preferred）**:

```swift
let swift = "not a scripting language"
```

**不推荐（Not Preferred）**:

```swift
let swift = "not a scripting language";
```

**NOTE**: Swift is very different from JavaScript, where omitting semicolons is [generally considered unsafe](http://stackoverflow.com/questions/444080/do-you-recommend-using-semicolons-after-every-statement-in-javascript)

注：Swift 非常不同于 JavaScript。在 JavaScript 中忽略分号[一般被认为是不安全的](http://stackoverflow.com/questions/444080/do-you-recommend-using-semicolons-after-every-statement-in-javascript)。

## 括号/Parentheses

Parentheses around conditionals are not required and should be omitted.

条件周围的括号是不必要的，应该被忽略。

**推荐（Preferred）**:

```swift
if name == "Hello" {
  print("World")
}
```

**不推荐（Not Preferred）**:

```swift
if (name == "Hello") {
  print("World")
}
```

In larger expressions, optional parentheses can sometimes make code read more clearly.

在更大的表达式中，额外的括号有时可以让代码读起来更清晰。

**推荐（Preferred）**:

```swift
let playerMark = (player == current ? "X" : "O")
```

## 多行字符串字面量/Multi-line String Literals

When building a long string literal, you're encouraged to use the multi-line string literal syntax. Open the literal on the same line as the assignment but do not include text on that line. Indent the text block one additional level.

当创建一个较长的字符串字面量时，你可以使用多行字符串字面量的便利语法。在赋值语句处开始创建字符串字面量，但是不包含任何文字。文字将在第二行出现并缩进一个层级。

**推荐（Preferred）**:

```swift
let message = """
  You cannot charge the flux \
  capacitor with a 9V battery.
  You must use a super-charger \
  which costs 10 credits. You currently \
  have \(credits) credits available.
  """
```

**不推荐（Not Preferred）**:

```swift
let message = """You cannot charge the flux \
  capacitor with a 9V battery.
  You must use a super-charger \
  which costs 10 credits. You currently \
  have \(credits) credits available.
  """
```

**不推荐（Not Preferred）**:

```swift
let message = "You cannot charge the flux " +
  "capacitor with a 9V battery.\n" +
  "You must use a super-charger " +
  "which costs 10 credits. You currently " +
  "have \(credits) credits available."
```

## 不要使用 Emoji/No Emoji

Do not use emoji in your projects. For those readers who actually type in their code, it's an unnecessary source of friction. While it may be cute, it doesn't add to the learning and it interrupts the coding flow for these readers.

不要在工程里使用 Emoji。对于读者而言，输入这一类型的代码意义并不大。虽然看起来十分可爱，但它对于学习的帮助不大且会打乱输入代码的节奏。

## 组织名称和包标识/Organization and Bundle Identifier

Where an Xcode project is involved, the organization should be set to `Ray Wenderlich` and the Bundle Identifier set to `com.raywenderlich.TutorialName` where `TutorialName` is the name of the tutorial project.

涉及到 Xcode 项目的地方，组织应该被设置为 `Ray Wenderlich` 并且包标识符应该被设置为 `com.razeware.TutorialName` ，其中 `TutorialName` 是教程的名字。

![Xcode Project settings](screens/project_settings.png)

## 版权声明/Copyright Statement

The following copyright statement should be included at the top of every source file:

以下版权声明应该被包含在每个源文件的顶部：

```swift
/// Copyright (c) 2019 Razeware LLC
/// 
/// Permission is hereby granted, free of charge, to any person obtaining a copy
/// of this software and associated documentation files (the "Software"), to deal
/// in the Software without restriction, including without limitation the rights
/// to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
/// copies of the Software, and to permit persons to whom the Software is
/// furnished to do so, subject to the following conditions:
/// 
/// The above copyright notice and this permission notice shall be included in
/// all copies or substantial portions of the Software.
/// 
/// Notwithstanding the foregoing, you may not use, copy, modify, merge, publish,
/// distribute, sublicense, create a derivative work, and/or sell copies of the
/// Software in any work that is designed, intended, or marketed for pedagogical or
/// instructional purposes related to programming, coding, application development,
/// or information technology.  Permission for such use, copying, modification,
/// merger, publication, distribution, sublicensing, creation of derivative works,
/// or sale is expressly withheld.
/// 
/// THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
/// IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
/// FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
/// AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
/// LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
/// OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
/// THE SOFTWARE.
```

## 笑脸/Smiley Face

Smiley faces are a very prominent style feature of the [raywenderlich.com](https://www.raywenderlich.com/) site! It is very important to have the correct smile signifying the immense amount of happiness and excitement for the coding topic. The closing square bracket `]` is used because it represents the largest smile able to be captured using ASCII art. A closing parenthesis `)` creates a half-hearted smile, and thus is not preferred.

笑脸是[raywenderlich.com](https://www.raywenderlich.com/) 网站的一大特色！正确使用微笑来表达对编码主题的欢乐与兴奋是非常重要的。使用右方括号 `]` 是因为它代表 ASCII 中的最大笑容。右括号 `)` 表示笑脸就没有那么强烈了，因此不推荐使用。

**推荐（Preferred）**:

```swift
:]
```

**不推荐（Not Preferred）**:

```swift
:)
```

## 参考/References

* [The Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
* [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/index.html)
* [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html)
* [Swift Standard Library Reference](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/index.html)