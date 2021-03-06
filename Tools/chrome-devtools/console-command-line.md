---
tags: ['命令手册']
---

# 控制台命令API

## 简介

Chrome开发者工具中的**命令行工具**的命令手册

Command Line API 包含一个用于执行以下常见任务的便捷函数集合：选择和检查 DOM 元素，以可读格式显示数据，停止和启动分析器，以及监控 DOM 事件。

注：此 API 仅能通过**控制台**本身获取。您无法通过网页上的脚本访问 Command Line API。

## 命令详细

### $_

`$_` 返回最近评估的表达式的值。

`$_` 在评估新命令时更改

### $0 - $4

$0、$1、$2、$3 和 $4 命令用作在 Elements 面板中检查的最后五个 DOM 元素或在 Profiles 面板中选择的最后五个 JavaScript 堆对象的历史参考。$0 返回最近一次选择的元素或 JavaScript 对象，$1 返回仅在最近一次之前选择的元素或对象，依此类推。

### $(selector)

`$(selector)` 返回带有指定的 CSS 选择器的第一个 DOM 元素的引用。此函数等同`document.querySelector()` 函数。

右键点击返回的结果并选择“Reveal in Elements Panel”以在 DOM 中查找它，或选择“Scroll in to View”以在页面上显示它。

注：如果您在使用库，例如，使用 $ 的 jQuery，则此功能将被覆盖， $ 将与该库的实现对应。

### $\$(selector)

<code>$\$(selector)</code> 返回与给定 CSS 选择器匹配的元素数组。此命令等同于调用 `document.querySelectorAll()`。

以下示例使用 <code>$\$()</code> 在当前文档中创建一个所有 `<img>` 元素的数组，并显示每个元素的 src 属性值：

```javascript
var images = $$('img');
for (each in images) {
console.log(images[each].src);
}
```

注：在控制台中按 Shift + Enter 以开始一个新行，无需执行脚本。

### $x(path)

`$x(path)` 返回一个与给定 XPath 表达式匹配的 DOM 元素数组。

例如，以下命令返回页面上的所有 `<p>` 元素：

```
$x("//p")
```

以下示例返回包含 `<a>` 元素的所有 `<p>` 元素：

```
$x("//p[a]")
```

### clear()

`clear()` 清除其历史记录的控制台。

```
clear();
```

### copy(object)

`copy(object)` 将指定对象的字符串表示形式复制到剪贴板。

```
copy($0);
```

### debug(function)

调用指定的函数时，将触发调试程序，并在 Sources 面板上使函数内部中断，从而允许逐行执行代码并进行调试。

```
debug(getData);
```

使用 `undebug(fn)` 停止函数中断，或使用 UI 停用所有断点。

### dir(object)

`dir(object)` 显示所有指定对象的属性的对象样式列表。此方法等同于 Console API 的 `console.dir()` 方法。

以下示例显示在命令行中直接评估 `document.body` 和使用 `dir()` 显示相同元素之间的差异：

```
document.body;
dir(document.body);
```

### dirxml(object)

dirxml(object) 输出以 XML 形式表示的指定对象，如 Elements 标签中所示。此方法等同于 console.dirxml() 方法。

### inspect(object/function)

`inspect(object/function)` 在相应的面板中打开并选择指定的元素或对象：针对 DOM 元素使用 Elements 面板，或针对 JavaScript 堆对象使用 Profiles 面板。

以下是在“Elements”面板中打开 `document.body` 的示例：

```
inspect(document.body);
```

当传递要检查的函数时，此函数在 Sources 面板中打开文档以供您检查。

### getEventListeners(object)

`getEventListeners(object)` 返回在指定对象上注册的事件侦听器。

返回值是一个对象，其包含每个注册的事件类型（例如，“click”或“keydown”）数组。每个数组的成员是描述为每个类型注册的侦听器的对象。

例如，下面列出了在文档对象上注册的所有事件侦听器：

```
getEventListeners(document);
```

### keys(object)

`keys(object)` 返回一个包含属于指定对象的属性名称的数组。

如需获取相同属性的关联值，请使用 `values()`。

### monitor(function)

调用指定函数时，系统会向控制台记录一条消息，其中指明函数名称及在调用时传递到该函数的参数。

使用 `unmonitor(function)` 停止监控。

### monitorEvents(object[, events])

当在指定对象上发生一个指定事件时，将 Event 对象记录到控制台。您可以指定一个要监控的单独事件、一个事件数组或一个映射到预定义事件集合的常规事件“类型”。请参阅以下示例。

以下命令监控 `window` 对象上的所有 resize 事件。

monitorEvents(window, "resize");

下面定义一个在 `window` 对象上同时监控“resize”和“scroll”事件的数组：

monitorEvents(window, ["resize", "scroll"])

您还可以指定一个可用的事件“类型”、映射到预定义事件集的字符串。

下表列出了可用的事件类型及其相关的事件映射：

事件类型 | 对应的已映射事件
:--- | :---
mouse | "mousedown", "mouseup", "click", "dblclick", "mousemove", "mouseover","mouseout", "mousewheel"
key | "keydown", "keyup", "keypress", "textInput"
touch | "touchstart", "touchmove", "touchend", "touchcancel"
control | "resize", "scroll", "zoom", "focus", "blur", "select", "change", "submit", "reset"

例如，以下示例为 Elements 面板上当前选择的输入文本字段上的所有对应 key 事件使用使用“key”事件类型。

```
monitorEvents($0, "key");
```

### profile([name]) and profileEnd([name])

profile() 使用可选的名称启动一个 JavaScript CPU 分析会话。profileEnd() 在 Profile 面板中完成分析，并显示结果。（另请参阅加速 JavaScript 执行。）

开始分析：

```
profile("My profile")
```

在“Profiles”面板中停止分析并显示结果：

```
profileEnd("My profile")
```

也可以嵌入配置文件。例如，这在任意顺序下都起作用：

```
profile('A');
profile('B');
profileEnd('A');
profileEnd('B');
```

注：一次可运行多个 CPU 配置文件，不需要您按创建顺序结束它们。

### table(data[, columns])

通过传入含可选列标题的数据对象记录具有表格格式的对象数据。例如，要在控制台中显示使用 table 的名称列表，您需要执行：

```
var names = {
0: { firstName: "John", lastName: "Smith" },
1: { firstName: "Jane", lastName: "Doe" }
};
table(names);
```

### undebug(function)

`undebug(function)` 可停止调试指定函数，以便在调用函数时，不再调用调试程序。

```
undebug(getData);
```

### unmonitor(function)

`unmonitor(function)` 可停止监控指定函数。它可与 `monitor(fn)` 结合使用。

```
unmonitor(getData);
```

### unmonitorEvents(object[, events])

unmonitorEvents(object[, events]) 可停止针对指定对象和事件的事件监控。例如，以下命令可停止 window 对象上的所有事件监控：

```
unmonitorEvents(window);
```

您也可以有选择性地停止监控某个对象上的特定事件。

例如，以下代码可开始对当前所选元素上所有鼠标事件的监控，然后停止监控“mousemove”事件（可能会减少控制台输出的噪音）：

```
monitorEvents($0, "mouse");
unmonitorEvents($0, "mousemove");
```

### values(object)

values(object) 返回一个包含属于指定对象的所有属性值的数组。

```
values(object);
```
