# The Official Kodeco SwiftLint Policy

The SwiftLint configuration in this repo is designed to ensure the work we create at Kodeco conforms with [The Official Kodeco Swift Style Guide](https://github.com/kodecocodes/swift-style-guide/blob/main/README.markdown).

本仓库中的 SwiftLint 配置旨在确保我们在 Kodeco 创建的工作符合 [The Official Kodeco Swift Style Guide](https://github.com/kodecocodes/swift-style-guide/blob/main/README.markdown)。

The focus of this style is to improve readability in our print and web publications. Therefore, this style may be different from others you've used, but the demands of print and online reading are different from other contexts.

本样式指南的重点是提高我们印刷和网页出版物的可读性。因此,本样式指南可能与您以前使用的其他样式指南有所不同,但印刷和在线阅读的需求与其他场景有所不同。

The policies described here have a goal of achieving consistency between all of our projects, which will also streamline the flow of content through our editing process. Some of the choices also aim to ensure we've removed as much of the burden from our readers as possible.

这里描述的策略旨在实现我们所有项目之间的一致性,这也会进一步提高我们的工作效率。某些选择也旨在确保我们尽可能减轻读者的负担。

These guides use SwiftLint as a standard. You can learn more about SwiftLint by visiting its [official documentation page](https://github.com/realm/SwiftLint).

这些指南以 SwiftLint 为标准。您可以通过访问其[官方文档页面]((https://github.com/realm/SwiftLint))了解更多关于 SwiftLint 的信息。


## Table of Contents

* [安装 SwiftLint/Installing SwiftLint](#installing-swiftlint)
* [使用配置文件/Using the Configuration File](#using-the-configuration-file)
* [Xcode 配置/Xcode Settings](#xcode-settings)
* [运行 SwiftLine/Running SwiftLint](#running-swiftlint)
* [处理异常规则/Handling Rule Exceptions](#handling-rule-exceptions)
* [预期中的异常/Approved Exceptions](#approved-exceptions)
	* [隐式解包/Implicitly Unwrapped Optionals](#implicitly-unwrapped-optionals)
	* [强制转换/Force Cast](#force-cast)
	* [强制解包/Force Unwrapping](#force-unwrapping)
	* [SwiftUI 和多尾随闭包/SwiftUI and Multiple Trailing Closures](#swiftui-and-multiple-trailing-closures)
	* [开源文件/Open-Source Files](#open-source-files)
* [其他注意事项/Other Notes](#other-notes)

## 安装 SwiftLint/Installing SwiftLint

We recommend that Kodeco team members install SwiftLint using Homebrew:

我们建议 Kodeco 团队成员使用 Homebrew 安装 SwiftLint:

```bash
brew install swiftlint
```

If you are unable to use Homebrew, you may use one of the other methods described in the [SwiftLint documentation](https://github.com/realm/SwiftLint).

如果您无法使用 Homebrew,可以使用 SwiftLint 文档中描述的其他方法之一。

**Do not** install SwiftLint as a CocoaPod in your project.

**不要**在您的项目中将 SwiftLint 作为 CocoaPod 的包进行安装。

## 使用配置文件/Using the Configuration File

**Do not** place the configuration file inside your project. We don't want to impose this style on readers without their express knowledge or understanding of what's going on. 

**不要**将配置文件放置在您的项目内部。我们不想在读者没有明确知晓或理解发生的情况下强加此样式给他们。

Download **com.raywenderlich.swiftlint.yml** from the [Swift Style Guide repo]([https://github.com/raywenderlich/swift-style-guide](https://github.com/kodecocodes/swift-style-guide/)) and place it your home directory: **~/com.raywenderlich.swiftlint.yml**.

从 [Swift Style Guide repo]([https://github.com/raywenderlich/swift-style-guide](https://github.com/kodecocodes/swift-style-guide/)) 下载 **com.raywenderlich.swiftlint.yml**,并将其放置在您的主目录中:**~/com.raywenderlich.swiftlint.yml**。


## Xcode 设置/Xcode Settings

You'll need to configure Xcode to remove trailing whitespace from all lines. This is not the default configuration.

您需要配置 Xcode 以删除所有行的尾随空白。这不是默认配置。

In Xcode's Preferences, select **Text Editing** ▸ **Editing** and check **Including whitespace-only lines**. 

在 Xcode 的首选项中,选择 **Text Editing ▸ Editing**,并勾选 **Including whitespace-only lines**。

![](screens/trailing-whitespace.png)

## 运行 SwiftLint/Running SwiftLint

To simplify the process for everyone in the content pipeline, you'll need to add the necessary instructions to your sample project to run SwiftLint automatically on each build. To do so:

为了简化工作流中每个人的流程,您需要为样例项目添加必要的说明,以便在每次构建时自动运行 SwiftLint。要做到这一点:

1. 在项目导航器中选择项目文档。 / Select the project document in the Project navigator.
1. 选择 **Build Phases** 选项卡。 / Select the **Build Phases** tab.
1. 点击 **+** 并选择 **New Run Script Phase**。/ Click **+** and choose **New Run Script Phase**.

![](screens/add-run-script.png)

4. 将新创建的阶段拖动到 **Compile Sources** 阶段之前。/ Drag the new phase before the **Compile Sources** phase.
4. 点击 **Run Script** 阶段的披露三角形,并确保 **Shell** 设置为 **/bin/sh**。/ Click the disclosure triangle on the **Run Script** phase and ensure **Shell** is set to **/bin/sh**.

![](screens/empty-run-script.png)

6. 添加以下脚本 / Add the following script:
```
PATH=/opt/homebrew/bin:$PATH
if [ -f ~/com.raywenderlich.swiftlint.yml ]; then
  if which swiftlint >/dev/null; then
    swiftlint --no-cache --config ~/com.raywenderlich.swiftlint.yml
  fi
fi
```

## 处理异常规则/Handling Rule Exceptions

Your sample project must compile without warnings — SwiftLint or otherwise. In general, you should change your code to eliminate all warnings where necessary. When it comes to SwiftLint, however, there will be times when this isn't possible. In these situations, you'll need to use in-line comments to temporarily disable rules. You can find appropriate syntax to do this in [the SwiftLint documentation](https://realm.github.io/SwiftLint/#disable-rules-in-code).

您的示例项目必须在没有警告的情况下进行编译 —— 不管是 SwiftLint 还是其他警告。通常,您应该根据需要更改代码以消除所有警告。但是,当涉及到 SwiftLint 时,有时这是不可能的。在这种情况下,您需要使用内联注释来临时禁用规则。您可以在 [the SwiftLint documentation](https://realm.github.io/SwiftLint/#disable-rules-in-code) 文档中找到合适的禁用规则的语法。

You may only disable a rule if it is on the list of approved exceptions listed below.

您只能禁用下面列出的经批准的异常规则列表中的规则。

Prefer the form that disables a rule only for the next line:

优先使用仅禁用下一行的规则的形式:

```
// swiftlint:disable:next implicitly_unwrapped_optional
var injectedValue: Data!
```

Or, similarly, for the previous line:

或者,对于前一行实施类似的规则:

```
var injectedValue: Data!
// swiftlint:disable:previous implicitly_unwrapped_optional
```

If there are several approved exceptions, group them together and disable the rule for that region. Be sure to enable the rule after that section. Do not leave a rule disabled throughout the source file.

如果有多个预期内的异常,请将其组合在一起,并对该区域禁用规则。一定要在该部分之后再启用规则。不要在整个源文件中保持规则被禁用状态。

```
// swiftlint:disable implicitly_unwrapped_optional
var injectedValue1: Data!
var injectedValue2: Data!
// swiftlint:enable implicitly_unwrapped_optional
```

If you must disable rules in your project, leave those in-line comments in the project for the benefit of your teammates in the editing pipeline.

如果您必须在项目中禁用规则,请为工作流中的队友留下这些内联注释。

Finally, if you're not sure which rule is triggering a warning, you can find the rule name in parentheses at the end of message:

最后,如果您不确定哪条规则触发了警告,可以在消息末尾的括号中找到规则名称:

![](screens/swiftlint-warning.png)

## 预期中的异常/Approved Exceptions

There are certain common idioms that violate SwiftLint's strict checking. If you are unable to work around them — and you've already tried to find a better way to structure your code — you may disable rules as described in this section.

有些常见的用法违反了 SwiftLint 的严格检查。如果您无法解决它们 - 并且您已经尝试找到重构代码的更好方法 - 您可以按本节所述禁用规则。

If you find that you're struggling with rules other than those described below, please reach out to your Team Lead with your specific example.

如果您发现除了下面描述的规则之外,您还在努力遵守其他规则,请随时与您的团队主管联系,提供您的具体例子。

### 隐式解包/Implicitly Unwrapped Optionals

It is sometimes common, in lieu of using dependency injection, to declare a child view controller's properties as Implicitly Unwrapped Optionals (IUO). If you're unable to structure your project to avoid this, you may disable the `implicitly_unwrapped_optional` rule for those dependency declarations. With the advent of `@IBSegueAction`, this should be rare.

有时,为了避免使用依赖注入,会将子视图控制器的属性声明为隐式解包可选项(IUO)。如果您无法对项目进行结构化以避免此情况,您可以对这些依赖关系声明禁用 `implicitly_unwrapped_optional` 规则。随着 `@IBSegueAction` 的出现,这种情况应该很少见。

### 强制转换/Force Cast

You may use force casting — and disable the `force_cast` rule — in the `UITableViewDataSource` and `UICollectionViewDataSource` methods that dequeue cells.

在 `UITableViewDataSource` 和 `UICollectionViewDataSource` 的相关方法中取出 Cell 时,您可以使用强制转换 - 并禁用 `force_cast` 规则。

### 强制解包/Force Unwrapping

You may use forced unwrapping — rule name `force_unwrap` — when returning a color from an asset catalog:

从资源目录获取颜色时,您可以使用强制解包 - 规则名称为 `force_unwrap`:

```
static var rwGreen: UIColor {
  // swiftlint:disable:next force_unwrapping
  UIColor(named: "rw-green")!
}
```

You may also use it in the same context as the force cast exception above, dequeuing cells in `UITableViewDataSource` and `UICollectionViewDataSource` methods.

在上面强制转换的上下文中,也即在 UITableViewDataSource 和 UICollectionViewDataSource 方法中取出 Cell 时,您也可以使用这个规则。

Although we prefer you to model appropriately defensive code for our readers, you may use force unwrapping to access resources that you _know_ are included in the app bundle.

虽然我们更喜欢您为读者编写适当的防御性代码,但是您可以使用强制解包访问您确定包含在应用程序 bundle 中的资源。

Finally, you may use force unwrapping when constructing a `URL` from a hard-coded, and guaranteed valid, URL string.

最后,在从硬编码且保证有效的 URL 字符串构造 `URL` 时,您可以使用强制解包。

### SwiftUI 和多个尾随闭包/SwiftUI and Multiple Trailing Closures

Idiomatic SwiftUI uses trailing closures to provide the view content for certain user interface elements. `Button` is a prime example; it has an initializer form that uses a closure to provide its `label`. It's common to write something like the following:

惯用的 SwiftUI 使用尾随闭包为某些用户界面元素提供视图内容。`Button` 就是一个很好的例子;它有一个使用闭包提供其 `label` 的初始化器形式。编写如下代码很常见:

```
Button(action: { self.isPresented.toggle() }) {
  Image(systemName: "plus")
}
```

This violates the rule that you should not use trailing closure syntax when a method accepts multiple closure parameters, so SwiftLint will flag it with a warning. 

这违反了当方法接受多个闭包参数时不应使用尾随闭包语法的规则,因此 SwiftLint 会发出警告。

You can work around this by extracting the `Button`'s action into a separate method. While this is frequently a better solution when the action requires several statements, it's an onerous requirement when the action is a single statement, as in the example above.

您可以通过将 `Button` 的 action 提取到一个单独的方法中来解决这个问题。虽然当 action 需要多个语句时这通常是更好的解决方案,但当 action 仅是一个语句时,就像上面的例子一样,这是一项艰巨的要求。

In these cases, you're permitted to disable this rule **for the declaration of a SwiftUI view** only. The rule name is `multiple_closures_with_trailing_closure`.

在这些情况下,您只能在**声明 SwiftUI 视图**时禁用此规则。规则名称是 `multiple_closures_with_trailing_closure`。

### 开源文件/Open-Source Files

Occasionally, you'll find it necessary to include an unmodified open-source file in the sample project. It's a virtual certainty that these files won't comply with our style guide. Our practice has always been to leave these files in their original state. In this situation, you should disable SwiftLint for the entire file:

有时候,在示例项目中包含未修改的开源文件是必要的。这些文件遵循我们的样式指南的可能性肯定微乎其微。我们的惯例一直是将这些文件保留在原始状态。在这种情况下,您应该为整个文件禁用 SwiftLint:

```
// swiftlint:disable all
```

## 其他注意事项/Other Notes

While SwiftLint goes a long way towards making your source code compliant with our style guide, it doesn't cover everything. For example, it won't catch or force you to correct the formatting for multi-condition `guard` statements. (See [Golden Path](https://github.com/raywenderlich/swift-style-guide#golden-path) for correct formatting.)

虽然 SwiftLint 在很大程度上使您的源代码符合我们的样式指南,但它并不能涵盖所有内容。例如,它不会捕获或强制您修正多条件 `guard` 语句的格式。(请参阅 [Golden Path](https://github.com/raywenderlich/swift-style-guide#golden-path) 以获取正确的格式。)

This configuration has been tested against several dozen of our most recent tutorials. A couple of rules, such as the line length limit or the limit on the length of a function, may need tweaking to fit our style. If you find yourself butting heads with SwiftLint, please reach out to the iOS Team Lead with details.

该配置已针对我们最近的几十个教程进行了测试。一些规则,比如行长度限制或函数长度限制,可能需要调整以符合我们的风格。如果您发现自己与 SwiftLint 发生冲突,请随时联系 iOS 团队负责人提供详细信息。
