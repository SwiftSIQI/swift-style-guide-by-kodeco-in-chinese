# The Official raywenderlich.com Swift Style Guide.

### Updated for Swift 4.2

This style guide is different from others you may see, because the focus is centered on readability for print and the web. We created this style guide to keep the code in our books, tutorials, and starter kits nice and consistent — even though we have many different authors working on the books.

这篇代码风格指南可能不同于你看到的其他代码风格指南。因为它倾向于保证出版物和网页内容的可读性。我们创建这篇代码风格指南的初衷是为了让我们的书、教程和初学者指南中的代码，即使在有很多作者同时协作的情况下，也能保持能高质量与风格统一。

Our overarching goals are clarity, consistency and brevity, in that order.

总体的目标依次排列是清晰、一致和简洁。

## Table of Contents

* [正确性 Correctness](#correctness)
* [命名 Naming](#naming)
  * [在文章中正确引用代码 Prose](#prose)
  * [代理 Delegates](#delegates)
  * [使用上下文进行类型推断 Use Type Inferred Context](#use-type-inferred-context)
  * [通用类型参数 Generics](#generics)
  * [类前缀 Class Prefixes](#class-prefixes)
  * [语言 Language](#language)
* [代码组织 Code Organization](#code-organization)
  * [协议一致性 Protocol Conformance](#protocol-conformance)
  * [无用代码 Unused Code](#unused-code)
  * [简化引用 Minimal Imports](#minimal-imports)
* [空格 Spacing](#spacing)
* [注释 Comments](#comments)
* [类与结构体 Classes and Structures](#classes-and-structures)
  * [Self 的使用 Use of Self](#use-of-self)
  * [协议一致性 Protocol Conformance](#protocol-conformance)
  * [计算型属性 Computed Properties](#computed-properties)
  * [FinaL 关键字 Final](#final)
* [方法声明 Function Declarations](#function-declarations)
* [方法调用 Function Calls](#function-calls)
* [闭包表达式 Closure Expressions](#closure-expressions)
* [类型 Types](#types)
  * [常量 Constants](#constants)
  * [静态方法和可变类型属性 Static Methods and Variable Type Properties](#static-methods-and-variable-type-properties)
  * [可选类型 Optionals](#optionals)
  * [延时初始化 Lazy Initialization](#lazy-initialization)
  * [类型推断 Type Inference](#type-inference)
  * [语法糖 Syntactic Sugar](#syntactic-sugar)
* [函数与方法 Functions vs Methods](#functions-vs-methods)
* [内存管理 Memory Management](#memory-management)
  * [延长生命周期 Extending Lifetime](#extending-lifetime)
* [访问控制 Access Control](#access-control)
* [控制流 Control Flow](#control-flow)
  * [三元运算符 Ternary Operator](#ternary-operator)
* [黄金路径 Golden Path](#golden-path)
  * [失败防护 Failing Guards](#failing-guards)
* [分号 Semicolons](#semicolons)
* [圆括号 Parentheses](#parentheses)
* [多行字符串字面量 Multi-line String Literals](#multi-line-string-literals)
* [不要使用 Emoji No Emoji](#no-emoji)
* [组织名称和包标识 Organization and Bundle Identifier](#organization-and-bundle-identifier)
* [版权声明 Copyright Statement](#copyright-statement)
* [笑脸 Smiley Face](#smiley-face)
* [参考资料 References](#references)

## Correctness

Strive to make your code compile without warnings. This rule informs many style decisions such as using `#selector` types instead of string literals.

尽量保证代码在编译的过程中不会出现任何警告。这条规则左右了其他规则的制定，例如使用 `#selector` 类型而不是字符串字面量这条规则。

## Naming

Descriptive and consistent naming makes software easier to read and understand. Use the Swift naming conventions described in the [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/). Some key takeaways include:

具有描述性和一致性的命名能够让软件更易于阅读和理解。遵循 [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/) 中描述的命名规范。 一些关键点包括如下：

* striving for clarity at the call site

* 在调用时力求意图清晰明确。

* prioritizing clarity over brevity

* 传达清晰的意图比文字的简洁更重要。

* using camel case (not snake case)

* 使用驼峰命名法（而不是蛇形命名法）

  > 译者注：snake case 是指使用下划线的命名方法，[详情参考链接](https://fr.wikipedia.org/wiki/Snake_case)

* using uppercase for types (and protocols), lowercase for everything else

* 类型（和协议）使用首字母大写，其它都是首字母小写

* including all needed words while omitting needless words

* 包含所有需要的单词，同时省略不必要的单词

* using names based on roles, not types

* 基于作用命名，而不是类型

* sometimes compensating for weak type information

* 必要时，为弱类型补充额外的信息

* striving for fluent usage
* 尽量保证使用上的流畅性

* beginning factory methods with `make`
* 工厂方法要以 `make` 开头

* naming methods for their side effects
* 依据方法的副作用进行命名

  * verb methods follow the -ed, -ing rule for the non-mutating version
  * 对于不可变方法，动词描述的方法遵循紧跟 -ed, -ing 后缀

    >译者注：verb methods 是指恰好能够被一个动词描述的方法

  * noun methods follow the formX rule for the mutating version
  
  * 对于可变方法，名词描述的方法遵循 formX 的规则

    > 译者注： formX 中的 X 指代对应的名词，例如 `y.formUnion()` 方法，X 指代 Union

  * boolean types should read like assertions

  * 布尔类型读起来应该像是对被调用对象的断言

  * protocols that describe _what something is_ should read as nouns

  * _描述事物的_ 协议，读起来应该像名词

  * protocols that describe _a capability_ should end in _-able_ or _-ible_

  * _描述能力_ 的协议，应该使用后缀 _-able_，_ible_

* using terms that don't surprise experts or confuse beginners

* 使用术语的时候，不要让专家觉得惊讶，也不要让初学者感到困惑

* generally avoiding abbreviations

* 通常要避免缩写

* using precedent for names

* 遵循名称的先例

* preferring methods and properties to free functions
* 优先选择方法或属性，而非全局函数。

* casing acronyms and initialisms uniformly up or down
* 首字母缩写的单词要根据惯例全大小或者全小写

* giving the same base name to methods that share the same meaning
* 当某些方法的含义基本一致时，那么它们可以共享一个基础方法名。

* avoiding overloads on return type
* 避免“重载返回类型”

* choosing good parameter names that serve as documentation
* 选择具有说明作用的形参名，能够让文档注释质量更高

* preferring to name the first parameter instead of including its name in the method name, except as mentioned under Delegates
* 尽量为第一个设置参数标签并避免在方法中包含第一个参数名，代理模式下的方法可以忽略此规定。

* labeling closure and tuple parameters

* 为闭包和元组参数设置标签

* taking advantage of default parameters

* 利用默认参数带来的优势

### 在文章中引用代码（Prose）

When referring to methods in prose, being unambiguous is critical. To refer to a method name, use the simplest form possible.

在文章中引用方法时，含义明确是至关重要的。尽可能用最简单的形式引用方法。

1. Write the method name with no parameters.  **Example:** Next, you need to call `addTarget`.

* 写一个不带参数的方法。**例如**：下一步，你需要调用方法 `addTarget`。

2. Write the method name with argument labels.  **Example:** Next, you need to call `addTarget(_:action:)`.

* 写一个带参数标签的方法。**例如**：下一步，你需要调用方法 `addTarget(_:action:)`。

3. Write the full method name with argument labels and types. **Example:** Next, you need to call `addTarget(_: Any?, action: Selector?)`.

* 写一个带参数标签和类型的完整方法。**例如**：下一步, 你需要调用方法 `addTarget(_: Any?, action: Selector?)`。

For the above example using `UIGestureRecognizer`, 1 is unambiguous and preferred.

上面是一个使用 `UIGestureRecognizer` 的例子, 1 的表述明确，也是应当被首先采用的描述方式。

**Pro Tip:** You can use Xcode's jump bar to lookup methods with argument labels. If you’re particularly good at mashing lots of keys simultaneously, put the cursor in the method name and press **Shift-Control-Option-Command-C** (all 4 modifier keys) and Xcode will kindly put the signature on your clipboard.

**小提示：** 你可以使用 Xcode 的 jump bar 来查看方法的参数标签。如果你能够相对轻松的操作多个按键，那么可以尝试将光标放在方法名上，并同时按下  **Shift-Control-Option-Command-C** 键，这些 Xcode 会将此方法的签名复制到剪贴板上。

  > 译者注：与复制相关的快捷操作有三种，需要注意的是在 playground 中这些方法不生效
  >  
  > * **command+C** ：Copy（光标所在位置的单词）：`viewDidLoad`
  > * **control+shift+command+C**：Copy Symbol Name（光标所在位置的消息符号名称）：`viewDidLoad()`
  > * **option+control+shift+command+C**：Copy Qualified Symbol Name（光标所在位置的消息符号全名，带所属类名）：`ViewController.viewDidLoad()`

![Methods in Xcode jump bar](screens/xcode-jump-bar.png)

### 类前缀（Class Prefixes）

Swift types are automatically namespaced by the module that contains them and you should not add a class prefix such as RW. If two names from different modules collide you can disambiguate by prefixing the type name with the module name. However, only specify the module name when there is possibility for confusion which should be rare.

Swift 里各种类型被其所处的模块自动分配了命名空间。不应该再添加类似于 RW 的类前缀。如果不同模块间的两个类型命名冲突，可以在类型名前添加模块名来消除歧义。无论如何，仅在少数可能引起混淆的情况下指明模块名。

```swift
import SomeModule

let myClass = MyModule.UsefulClass()
```

### 代理（Delegates）

When creating custom delegate methods, an unnamed first parameter should be the delegate source. (UIKit contains numerous examples of this.)

当创建自定义代理方法的时候，第一个未命名的参数应该是代理源。（ UIKit 包含很多类似的例子）

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

### 使用上下文进行类型推断（Use Type Inferred Context）

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

### 泛型 (Generics)

Generic type parameters should be descriptive, upper camel case names. When a type name doesn't have a meaningful relationship or role, use a traditional single uppercase letter such as `T`, `U`, or `V`.

泛型的类型参数应该遵循大写驼峰法命名规则且具有较强的描述性。当类型参数与函数或这泛型之间无明显任何有意义的关联时，通常使用单个大写字母来命名，例如 `T` 、`U` 或 `V`。

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

### 语言(Language)

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

## Code Organization

Use extensions to organize your code into logical blocks of functionality. Each extension should be set off with a `// MARK: -` comment to keep things well-organized.

### Protocol Conformance

In particular, when adding protocol conformance to a model, prefer adding a separate extension for the protocol methods. This keeps the related methods grouped together with the protocol and can simplify instructions to add a protocol to a class with its associated methods.

**Preferred**:
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

**Not Preferred**:
```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all methods
}
```

Since the compiler does not allow you to re-declare protocol conformance in a derived class, it is not always required to replicate the extension groups of the base class. This is especially true if the derived class is a terminal class and a small number of methods are being overridden. When to preserve the extension groups is left to the discretion of the author.

For UIKit view controllers, consider grouping lifecycle, custom accessors, and IBAction in separate class extensions.

### Unused Code

Unused (dead) code, including Xcode template code and placeholder comments should be removed. An exception is when your tutorial or book instructs the user to use the commented code.

Aspirational methods not directly associated with the tutorial whose implementation simply calls the superclass should also be removed. This includes any empty/unused UIApplicationDelegate methods.

**Preferred**:
```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  return Database.contacts.count
}
```

**Not Preferred**:
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
### Minimal Imports

Import only the modules a source file requires. For example, don't import `UIKit` when importing `Foundation` will suffice. Likewise, don't import `Foundation` if you must import `UIKit`.

**Preferred**:
```
import UIKit
var view: UIView
var deviceModels: [String]
```

**Preferred**:
```
import Foundation
var deviceModels: [String]
```

**Not Preferred**:
```
import UIKit
import Foundation
var view: UIView
var deviceModels: [String]
```

**Not Preferred**:
```
import UIKit
var deviceModels: [String]
```

## Spacing

* Indent using 2 spaces rather than tabs to conserve space and help prevent line wrapping. Be sure to set this preference in Xcode and in the Project settings as shown below:

![Xcode indent settings](screens/indentation.png)

* Method braces and other braces (`if`/`else`/`switch`/`while` etc.) always open on the same line as the statement but close on a new line.
* Tip: You can re-indent by selecting some code (or **Command-A** to select all) and then **Control-I** (or **Editor ▸ Structure ▸ Re-Indent** in the menu). Some of the Xcode template code will have 4-space tabs hard coded, so this is a good way to fix that.

**Preferred**:
```swift
if user.isHappy {
  // Do something
} else {
  // Do something else
}
```

**Not Preferred**:
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

* There should be no blank lines after an opening brace or before a closing brace.

* Colons always have no space on the left and one space on the right. Exceptions are the ternary operator `? :`, empty dictionary `[:]` and `#selector` syntax `addTarget(_:action:)`.

**Preferred**:
```swift
class TestDatabase: Database {
  var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

**Not Preferred**:
```swift
class TestDatabase : Database {
  var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```

* Long lines should be wrapped at around 70 characters. A hard limit is intentionally not specified.

* Avoid trailing whitespaces at the ends of lines.

* Add a single newline character at the end of each file.

## Comments

When they are needed, use comments to explain **why** a particular piece of code does something. Comments must be kept up-to-date or deleted.

Avoid block comments inline with code, as the code should be as self-documenting as possible. _Exception: This does not apply to those comments used to generate documentation._

Avoid the use of C-style comments (`/* ... */`). Prefer the use of double- or triple-slash.

## Classes and Structures

### Which one to use?

Remember, structs have [value semantics](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_144). Use structs for things that do not have an identity. An array that contains [a, b, c] is really the same as another array that contains [a, b, c] and they are completely interchangeable. It doesn't matter whether you use the first array or the second, because they represent the exact same thing. That's why arrays are structs.

Classes have [reference semantics](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_145). Use classes for things that do have an identity or a specific life cycle. You would model a person as a class because two person objects are two different things. Just because two people have the same name and birthdate, doesn't mean they are the same person. But the person's birthdate would be a struct because a date of 3 March 1950 is the same as any other date object for 3 March 1950. The date itself doesn't have an identity.

Sometimes, things should be structs but need to conform to `AnyObject` or are historically modeled as classes already (`NSDate`, `NSSet`). Try to follow these guidelines as closely as possible.

### Example definition

Here's an example of a well-styled class definition:

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

 + Specify types for properties, variables, constants, argument declarations and other statements with a space after the colon but not before, e.g. `x: Int`, and `Circle: Shape`.
 + Define multiple variables and structures on a single line if they share a common purpose / context.
 + Indent getter and setter definitions and property observers.
 + Don't add modifiers such as `internal` when they're already the default. Similarly, don't repeat the access modifier when overriding a method.
 + Organize extra functionality (e.g. printing) in extensions.
 + Hide non-shared, implementation details such as `centerString` inside the extension using `private` access control.

### Use of Self

For conciseness, avoid using `self` since Swift does not require it to access an object's properties or invoke its methods.

Use self only when required by the compiler (in `@escaping` closures, or in initializers to disambiguate properties from arguments). In other words, if it compiles without `self` then omit it.


### Computed Properties

For conciseness, if a computed property is read-only, omit the get clause. The get clause is required only when a set clause is provided.

**Preferred**:
```swift
var diameter: Double {
  return radius * 2
}
```

**Not Preferred**:
```swift
var diameter: Double {
  get {
    return radius * 2
  }
}
```

### Final

Marking classes or members as `final` in tutorials can distract from the main topic and is not required. Nevertheless, use of `final` can sometimes clarify your intent and is worth the cost. In the below example, `Box` has a particular purpose and customization in a derived class is not intended. Marking it `final` makes that clear.

```swift
// Turn any generic type into a reference type using this Box class.
final class Box<T> {
  let value: T
  init(_ value: T) {
    self.value = value
  }
}
```

## Function Declarations

Keep short function declarations on one line including the opening brace:

```swift
func reticulateSplines(spline: [Double]) -> Bool {
  // reticulate code goes here
}
```

For functions with long signatures, put each parameter on a new line and add an extra indent on subsequent lines:

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

**Preferred**:

```swift
func updateConstraints() -> Void {
  // magic happens here
}

typealias CompletionHandler = (result) -> Void
```

**Not Preferred**:

```swift
func updateConstraints() -> () {
  // magic happens here
}

typealias CompletionHandler = (result) -> ()
```

## Function Calls

Mirror the style of function declarations at call sites. Calls that fit on a single line should be written as such:

```swift
let success = reticulateSplines(splines)
```

If the call site must be wrapped, put each parameter on a new line, indented one additional level:

```swift
let success = reticulateSplines(
  spline: splines,
  adjustmentFactor: 1.3,
  translateConstant: 2,
  comment: "normalize the display")
```

## Closure Expressions

Use trailing closure syntax only if there's a single closure expression parameter at the end of the argument list. Give the closure parameters descriptive names.

**Preferred**:
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

**Not Preferred**:
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

```swift
attendeeList.sort { a, b in
  a > b
}
```

Chained methods using trailing closures should be clear and easy to read in context. Decisions on spacing, line breaks, and when to use named versus anonymous arguments is left to the discretion of the author. Examples:

```swift
let value = numbers.map { $0 * 2 }.filter { $0 % 3 == 0 }.index(of: 90)

let value = numbers
  .map {$0 * 2}
  .filter {$0 > 50}
  .map {$0 + 10}
```

## Types

Always use Swift's native types and expressions when available. Swift offers bridging to Objective-C so you can still use the full set of methods as needed.

**Preferred**:
```swift
let width = 120.0                                    // Double
let widthString = "\(width)"                         // String
```

**Less Preferred**:
```swift
let width = 120.0                                    // Double
let widthString = (width as NSNumber).stringValue    // String
```

**Not Preferred**:
```swift
let width: NSNumber = 120.0                          // NSNumber
let widthString: NSString = width.stringValue        // NSString
```

In drawing code, use `CGFloat` if it makes the code more succinct by avoiding too many conversions.

### Constants

Constants are defined using the `let` keyword and variables with the `var` keyword. Always use `let` instead of `var` if the value of the variable will not change.

**Tip:** A good technique is to define everything using `let` and only change it to `var` if the compiler complains!

You can define constants on a type rather than on an instance of that type using type properties. To declare a type property as a constant simply use `static let`. Type properties declared in this way are generally preferred over global constants because they are easier to distinguish from instance properties. Example:

**Preferred**:
```swift
enum Math {
  static let e = 2.718281828459045235360287
  static let root2 = 1.41421356237309504880168872
}

let hypotenuse = side * Math.root2

```
**Note:** The advantage of using a case-less enumeration is that it can't accidentally be instantiated and works as a pure namespace.

**Not Preferred**:
```swift
let e = 2.718281828459045235360287  // pollutes global namespace
let root2 = 1.41421356237309504880168872

let hypotenuse = side * root2 // what is root2?
```

### Static Methods and Variable Type Properties

Static methods and type properties work similarly to global functions and global variables and should be used sparingly. They are useful when functionality is scoped to a particular type or when Objective-C interoperability is required.

### Optionals

Declare variables and function return types as optional with `?` where a `nil` value is acceptable.

Use implicitly unwrapped types declared with `!` only for instance variables that you know will be initialized later before use, such as subviews that will be set up in `viewDidLoad()`. Prefer optional binding to implicitly unwrapped optionals in most other cases.

When accessing an optional value, use optional chaining if the value is only accessed once or if there are many optionals in the chain:

```swift
textContainer?.textLabel?.setNeedsDisplay()
```

Use optional binding when it's more convenient to unwrap once and perform multiple operations:

```swift
if let textContainer = textContainer {
  // do many things with textContainer
}
```

When naming optional variables and properties, avoid naming them like `optionalString` or `maybeView` since their optional-ness is already in the type declaration.

For optional binding, shadow the original name whenever possible rather than using names like `unwrappedView` or `actualLabel`.

**Preferred**:
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

**Not Preferred**:
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

### Lazy Initialization

Consider using lazy initialization for finer grained control over object lifetime. This is especially true for `UIViewController` that loads views lazily. You can either use a closure that is immediately called `{ }()` or call a private factory method. Example:

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

**Notes:**
  - `[unowned self]` is not required here. A retain cycle is not created.
  - Location manager has a side-effect for popping up UI to ask the user for permission so fine grain control makes sense here.


### Type Inference

Prefer compact code and let the compiler infer the type for constants or variables of single instances. Type inference is also appropriate for small, non-empty arrays and dictionaries. When required, specify the specific type such as `CGFloat` or `Int16`.

**Preferred**:
```swift
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5
```

**Not Preferred**:
```swift
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
var names = [String]()
```

#### Type Annotation for Empty Arrays and Dictionaries

For empty arrays and dictionaries, use type annotation. (For an array or dictionary assigned to a large, multi-line literal, use type annotation.)

**Preferred**:
```swift
var names: [String] = []
var lookup: [String: Int] = [:]
```

**Not Preferred**:
```swift
var names = [String]()
var lookup = [String: Int]()
```

**NOTE**: Following this guideline means picking descriptive names is even more important than before.


### Syntactic Sugar

Prefer the shortcut versions of type declarations over the full generics syntax.

**Preferred**:
```swift
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
```

**Not Preferred**:
```swift
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```

## Functions vs Methods

Free functions, which aren't attached to a class or type, should be used sparingly. When possible, prefer to use a method instead of a free function. This aids in readability and discoverability.

Free functions are most appropriate when they aren't associated with any particular type or instance.

**Preferred**
```swift
let sorted = items.mergeSorted()  // easily discoverable
rocket.launch()  // acts on the model
```

**Not Preferred**
```swift
let sorted = mergeSort(items)  // hard to discover
launch(&rocket)
```

**Free Function Exceptions**
```swift
let tuples = zip(a, b)  // feels natural as a free function (symmetry)
let value = max(x, y, z)  // another free function that feels natural
```

## Memory Management

Code (even non-production, tutorial demo code) should not create reference cycles. Analyze your object graph and prevent strong cycles with `weak` and `unowned` references. Alternatively, use value types (`struct`, `enum`) to prevent cycles altogether.

### Extending object lifetime

Extend object lifetime using the `[weak self]` and `guard let self = self else { return }` idiom. `[weak self]` is preferred to `[unowned self]` where it is not immediately obvious that `self` outlives the closure. Explicitly extending lifetime is preferred to optional chaining.

**Preferred**
```swift
resource.request().onComplete { [weak self] response in
  guard let self = self else {
    return
  }
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**Not Preferred**
```swift
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**Not Preferred**
```swift
// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
  let model = self?.updateModel(response)
  self?.updateUI(model)
}
```

## Access Control

Full access control annotation in tutorials can distract from the main topic and is not required. Using `private` and `fileprivate` appropriately, however, adds clarity and promotes encapsulation. Prefer `private` to `fileprivate`; use `fileprivate` only when the compiler insists.

Only explicitly use `open`, `public`, and `internal` when you require a full access control specification.

Use access control as the leading property specifier. The only things that should come before access control are the `static` specifier or attributes such as `@IBAction`, `@IBOutlet` and `@discardableResult`.

**Preferred**:
```swift
private let message = "Great Scott!"

class TimeMachine {  
  private dynamic lazy var fluxCapacitor = FluxCapacitor()
}
```

**Not Preferred**:
```swift
fileprivate let message = "Great Scott!"

class TimeMachine {  
  lazy dynamic private var fluxCapacitor = FluxCapacitor()
}
```

## Control Flow

Prefer the `for-in` style of `for` loop over the `while-condition-increment` style.

**Preferred**:
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

**Not Preferred**:
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

### Ternary Operator

The Ternary operator, `?:` , should only be used when it increases clarity or code neatness. A single condition is usually all that should be evaluated. Evaluating multiple conditions is usually more understandable as an `if` statement or refactored into instance variables. In general, the best use of the ternary operator is during assignment of a variable and deciding which value to use.

**Preferred**:

```swift
let value = 5
result = value != 0 ? x : y

let isHorizontal = true
result = isHorizontal ? x : y
```

**Not Preferred**:

```swift
result = a > b ? x = c > d ? c : d : y
```

## Golden Path

When coding with conditionals, the left-hand margin of the code should be the "golden" or "happy" path. That is, don't nest `if` statements. Multiple return statements are OK. The `guard` statement is built for this.

**Preferred**:
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

**Not Preferred**:
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

**Preferred**:
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

**Not Preferred**:
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

### Failing Guards

Guard statements are required to exit in some way. Generally, this should be simple one line statement such as `return`, `throw`, `break`, `continue`, and `fatalError()`. Large code blocks should be avoided. If cleanup code is required for multiple exit points, consider using a `defer` block to avoid cleanup code duplication.

## Semicolons

Swift does not require a semicolon after each statement in your code. They are only required if you wish to combine multiple statements on a single line.

Do not write multiple statements on a single line separated with semicolons.

**Preferred**:
```swift
let swift = "not a scripting language"
```

**Not Preferred**:
```swift
let swift = "not a scripting language";
```

**NOTE**: Swift is very different from JavaScript, where omitting semicolons is [generally considered unsafe](http://stackoverflow.com/questions/444080/do-you-recommend-using-semicolons-after-every-statement-in-javascript)

## Parentheses

Parentheses around conditionals are not required and should be omitted.

**Preferred**:
```swift
if name == "Hello" {
  print("World")
}
```

**Not Preferred**:
```swift
if (name == "Hello") {
  print("World")
}
```

In larger expressions, optional parentheses can sometimes make code read more clearly.

**Preferred**:
```swift
let playerMark = (player == current ? "X" : "O")
```

## Multi-line String Literals

When building a long string literal, you're encouraged to use the multi-line string literal syntax. Open the literal on the same line as the assignment but do not include text on that line. Indent the text block one additional level.

**Preferred**:

```swift
let message = """
  You cannot charge the flux \
  capacitor with a 9V battery.
  You must use a super-charger \
  which costs 10 credits. You currently \
  have \(credits) credits available.
  """
```

**Not Preferred**:

```swift
let message = """You cannot charge the flux \
  capacitor with a 9V battery.
  You must use a super-charger \
  which costs 10 credits. You currently \
  have \(credits) credits available.
  """
```

**Not Preferred**:

```swift
let message = "You cannot charge the flux " +
  "capacitor with a 9V battery.\n" +
  "You must use a super-charger " +
  "which costs 10 credits. You currently " +
  "have \(credits) credits available."
```

## No Emoji

Do not use emoji in your projects. For those readers who actually type in their code, it's an unnecessary source of friction. While it may be cute, it doesn't add to the learning and it interrupts the coding flow for these readers.

## Organization and Bundle Identifier

Where an Xcode project is involved, the organization should be set to `Ray Wenderlich` and the Bundle Identifier set to `com.raywenderlich.TutorialName` where `TutorialName` is the name of the tutorial project.

![Xcode Project settings](screens/project_settings.png)

## Copyright Statement

The following copyright statement should be included at the top of every source
file:

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

## Smiley Face

Smiley faces are a very prominent style feature of the [raywenderlich.com](https://www.raywenderlich.com/) site! It is very important to have the correct smile signifying the immense amount of happiness and excitement for the coding topic. The closing square bracket `]` is used because it represents the largest smile able to be captured using ASCII art. A closing parenthesis `)` creates a half-hearted smile, and thus is not preferred.

**Preferred**:
```
:]
```

**Not Preferred**:
```
:)
```

## References

* [The Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
* [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/index.html)
* [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html)
* [Swift Standard Library Reference](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/index.html)