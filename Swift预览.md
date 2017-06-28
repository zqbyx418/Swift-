# Swift预览

按照学习新语言的传统，第一个程序是打印"Hello, world!"。在`Swift`中，一行代码搞定：

`print("Hello, world!")`

如果你是用C或者Objective-C，应该比较熟悉这种写法。在`Swift`中，这行代码就是一个完整的程序。不需要为**输入/输出**或者**处理字符串**导入单独的库。全局作用域中的代码会被当做程序的入口，所以不需要`main()`函数，也不用在每个句子的后面加上`;`来分隔。

这个教程有足够的信息来教你如何用`Swift`实现各种编程任务。如何你暂时不懂其中一些东西，不要担心，后面会有详细解释，慢慢来，要学的还很多。

```
注意：
为了最好的体验，在Xcode中使用**playground**。它可以直接让你看到代码所产生的结果。
```

###简单值
`let`声明常量`var`表示变量。在编译时期不需要知道常量值，但是它只能被赋值一次。也就是说，你可以用常量来表示这样一个值：有且仅有一次赋值，多次使用。

```
var myVariable = 42
myVariable = 50
let myConstant = 42
```

常量或者变量的类型必须和赋给它们的值的类型一样。但并不是每一次都能确定类型。当你创建常量或变量的同时赋值，那编译器就会推断它们的类型。上述例子中，编译器推断`myVariable`是整形，因为它的初始值是整形。

如果初始值不能提供足够的信息（或没有初始值），在变量名后面指定类型，用`:`隔开

```
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```
```
练习
创建一个常量指定它的类型为 Float 并赋值为4

答：
let myConstant: Float = 4
```

值永远不会被隐式的转换成其他类型。如果需要把一个值转换成其他类型，**显示转换！**

```
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

```
练习
把最后一行代码中的 String 去掉，看看是什么错误？

答：
Binary operator '+' cannot be applied to operands of type 'String' and 'Int'
二元运算符'+' 不能用于'String'类型和'Int'类型相加这种操作
```

有一种更简单的方式把值转换成字符串：把值写到（）中，并且在（）前面加上一个\。例如：
```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

```
练习
用\()把一个浮点数转换成字符串，并加上某人的名字和他打个招呼。

答：
let name: String = "xxx"
var age: Float = 20.5
let greeting = "Hi \(age)岁的" + name
```

使用三个双引号来表示多行字符串，只要匹配结束的引号，每行字符串最开始的缩进会被删除。例如：

```
let quotation = """
Even though there's whitespace to the left,
the actual lines aren't indented.
Except for this line.
Double quotes (") can appear without being escaped.

I still have \(apples + oranges) pieces of fruit.
```
**不瞒你说，上述代码报错了，我真的没懂。。。**



