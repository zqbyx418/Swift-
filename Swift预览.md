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

常量或者变量的类型必须和赋给它们的值的类型一样。但并不是每一次都能确定类型。当你创建常量或变量的同时赋值，那编译器就会推断它们的类型。上述例子中，编译器推断`myVariable`是整型，因为它的初始值是整型。

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

使用三个双引号来表示多行字符串，用三个双引号来结束，其中每行字符串最开始的缩进会被删除。例如：

```
let quotation = """
Even though there's whitespace to the left,
the actual lines aren't indented.
Except for this line.
Double quotes (") can appear without being escaped.

I still have \(apples + oranges) pieces of fruit.
"""
```
**不瞒你说，上述代码报错了，我真的没懂。。。**

用`[]`来创建数组和字典,在`[]`中写索引或者键来获取值，可以在最后一个元素后面写`,`。
```
var shoppingList = ["catfish","water","tulips","blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
		"Malcolm": "Captain",
		"Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

使用初始化语法来创建空数组或者空字典。
```
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```
当为变量设置新值或将参数传给函数时，如果类型信息可以被推导，可以写空数组`[]`和空字典[:]，如下所示。
```
shoppingList = []
occupations = [:]
```
###控制流程

使用`if`和`switch`来控制条件，使用`for-in`，`while`和`repeat-while`来控制循环。不必非得把条件和循环的表达式放在括号里面，但后面的花括号是必须的。
```
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
	if score > 50 {
		teamScore += 3
	} else {
	   teamScore += 1
	}
}
print(teamScore)
```
在`if`的条件中，表达式必须是`Boolean`类型，也就是说像`if 1 {...}`这样的写法，是错误的，不能隐式的和`0`比较。
可以用`if`和`let`的组合来处理可能为空的值。这些值表示为可选项，可选的意思就是要么有一个值，要么是nil。在类型后面用一个`?`来标记这是一个可选值。
```
var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
	greeting = "Hello, \(name)"
}
```
```
练习
把 optionalName 的值改为 nil 。 greeting 会是什么？在 if 后面加一个 else 如果 optionalName 是 nil 重写一个 greeting

答：
var optionalName: String? = "John Appleseed"
optionalName = nil
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)!"
} else {
    greeting = "Hello..."
}
// 输出else里面的东西
```
如果可选值是`nil`，条件就是`false`，代码就会跳过`true`那个花括号里面的语句。除此之外，可选值将会被解包，并赋值给let声明的常量，代码块类的解包值是可用的。

还有另外一种处理可选值的方法，就是提供一个默认值，使用`??`来操作。如果可选值是`nil`，这个默认值将会被用来替代它。
```
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)"
```
`Switch`支持任何种类的数据和比较操作——不仅仅是整型或者等式。
```
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
```
```
练习
把 default 去掉，会是什么错误？

答：
Switch must be exhaustive, consider adding a default clause
Switch 必须是有限的，添加一个 default 来处理其他情况
``` 
注意, 如何在模式中使用`let`来匹配该模式的值分配给常量
在执行完switch中对应的代码后，程序将跳出switch。不会继续执行switch中接下来的代码，所以不需要在对应的代码块结尾加上`break`

使用`for-in`，并且提供一个键值对来遍历字典中全部元素，字典是一个无序的集合，因此他们的健和值的迭代也是任意的。
```
let interestingNumbers = [
    "Prime": [2,3,5,7,11,13],
    "Fibonacci": [1,1,2,3,5,8],
    "Square": [1,4,9,16,25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
// largest = 25
```
```
练习
添加另一个变量来追踪，哪种numbers是最大的，以及最大的数字

答：
let interestingNumbers = [
    "Prime": [2,3,5,7,11,13],
    "Fibonacci": [1,1,2,3,5,8],
    "Square": [1,4,9,16,25],
]
var largest = 0
var kindString: String?
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
            kindString = kind
        }
    }
}
print(largest)
print(kindString ?? "没有找到")
```
使用`while`来重复代码块直到条件改变。循环的条件可以放在最后，来确保至少执行了一次代码块。
```
var n = 2
while n < 100 {
	n *= 2
}
print(n)

var m = 2
repeat {
	m *= 2
} while m < 100
print(m)
```
可以通过`..<`创建索引范围来循环
```
var total = 0
for i in 0..<4 {
	total += i
}
print(total)
```
用`..<`创建一个省略其上限值的范围（相当于[n,m)），`...`来创建包含这两个值的范围（相当于[n,m]）。

###函数和闭包

用`func`来声明一个函数。通过函数名和括号中的一系列参数来调用。用`->`将参数名称、类型与函数的返回类型分开。
```
func greet(person: String, day: String) -> String {
	return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```
```
练习
去掉`day`这个参数，添加参数包括今天的午餐的特别问候

答：
func greet(person: String, lunch: String) -> String {
    return "Hello \(person), 今天中午的\(lunch)好吃吗?"
}
greet(person: "Bob", lunch: "猪")
```
默认，函数使用参数名来做为参数的标签，在参数名之前自定义参数标签或者用`_`省略参数标签。
```
func greet(_ person: String, on day: String) -> String {
	return "Hello \(person), today is \(day)."
}
greet("John",on: "Wednesday")
```
用元祖创建一个组合值，例如，从函数返回多个值。元祖的元素可以通过名称或者数字来引用。
```
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
	var min = scores[0]
	var max = scores[0]
	var sum = 0
	
	for score in scores {
		if score > max {
			max = score
		} else if score < min {
			min = score
		}
		sum += score
	}
	return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5,3,100,3,9])
print(statistics.sum)
print(statistics.2)
```
函数可以嵌套。嵌套函数可以用外层函数声明的变量。可以使用嵌套函数来组织长的或者复杂的函数代码。
```
func returnFifteen() -> Int {
	var y = 10
	func add() {
		y += 5
	}
	add()
	return y
}
```
函数是一等公民。这意味着一个函数可以返回另一个函数作为它的值。
```
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1+number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```
一个函数可以把另一个函数当做参数来使用
```
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}

func lessThanTen(number: Int) -> Bool {
    return number < 10
}

var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen(number:))
```
函数实际上是闭包的一种特殊形式：稍后可以被调用的代码块。闭包中的代码可以访问创建在闭包范围中可用的变量和函数，如你所看到的嵌套函数的示例，即使在执行闭包时，闭包也处于不同的范围。可以使用`({})`编写一个匿名闭包，用于将参数和返回类型与正文分开。
```
var numbers = [20,19,7,12]
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```
```
练习
重写闭包，所有奇数返回0

答：
var numbers = [20,19,7,12]
numbers.map({ (number: Int) -> Int in
    let result = number % 2 == 0 ? number : 0
    return result
})
```
有几种更简单的方式来写闭包。当已经知道闭包的类型，例如对应代理的回调，可以省略其参数的类型，其返回类型或者两者都省略。单条语句闭包隐式返回它唯一的语句的值。
```
var numbers = [20, 19, 7, 12]
let mappedNumbers = numbers.map({number in 3 * number})
print(mappedNumbers)
```

###对象和类

使用类名创建一个类。在类中声明属性就像声明常量和变量一样，只不过它在类的上下文中。同样，方法和函数的声明也和平时一样。
```
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```
```
练习
新增一个常量属性，新增一个带参数的方法

答：
class Shape {
    var numberOfSides = 0
    let name = "shape"
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
    func newFunction(name: String){
        print(name)
    }
}
```
通过类名加圆括号来创建一个实例。使用点语法访问实例的属性和方法。
```
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```
这个`Shape`版本缺失了一些重要的东西：构造器，用与在实例创建时来初始化类来。使用`init`来创建一个实例。
```
class NamedShape {
    var numberOfSides: Int = 0
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```
注意在初始化的时候使用`self`来区分`name`属性和`name`参数。创建类实例时，参数在初始化的时候将被像函数调用一样传递。每个属性都需要被赋值——在其声明中（如`numberOfSides`）或者构造器中（与名称一样）。

如果需要在销毁对象之前做一些清理操作，用`deinit`来创建析构器（deinitializer） 。

子类的类名后面跟上父类的类名，用`:`隔开。子类不需要继承任何标准的基类，因此可以根据需要添加或者省略父类。

子类要想重写父类方法，需要在方法实现前面加上`override`,不加的话，编译器会报错。编译器也会检测不带`override`的方法，这些方法不会覆盖父类中的任何方法。
```
class Square: NamedShape {
    var sideLength: Double
    
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }
    
    func area() -> Double {
        return sideLength * sideLength
    }
    
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}

let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```
```
练习
新建一个叫做 Circle 的类，继承自 NamedShape， 构造方法中有 radius 和 name 两个参数。 在 Circle类中实现 area() 和 simpleDescription() 方法。

答：
class Circle: NamedShape {
    var radius: Double
    
    init(radius: Double, name: String){
        self.radius = radius
        super.init(name: name)
    }
    
    func area() -> Double {
        return radius * radius * M_PI_2
    }
    
    override func simpleDescription() -> String {
        return "A \(name)"
    }
}

var circle = Circle(radius: 2, name: "circle")
circle.area()
circle.simpleDescription()
```
除了存储的简单属性之外，属性还有一个setter和getter。
```
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0
    
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }
    
    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        
        set {
            sideLength = newValue / 3.0
        }
    }
    
    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}

var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
triangle.perimeter = 9.9
print(triangle.sideLength)
```
在`perimeter`的setter方法中，传入的值默认叫`newValue`。你也可以在`set`后面加一个圆括号里面放入你想叫的名字来命名。

注意 `EquilateralTriangle`类的构造方法有三步：
1. 设置子类声明的属性值
2. 调用父类的构造器
3. 改变父类中定义的属性的值。此外，使用方法、getter方法、setter方法也能做到这一点

如果不需要计算属性，但仍需要提供在设置新值之前和之后运行的代码，请使用`willSet`和`didSet`。
在构造器之外，只要值改变，这个代码就会运行。例如，下面这个类，确保其三角形的边长总是和正方形的边长相等。
```
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}

var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
print(triangleAndSquare.triangle.sideLength)
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
print(triangleAndSquare.square.sideLength)
```
使用可选值时，在执行调方法、调属性或者下标操作之前，加上一个`?`。如果`?`前面这个值是`nil`，那么`?`后面的所有操作都会被忽略，所有值都是`nil`。如果不是空，这个可选值会被解包，用解包后的值来执行`?`后面的操作。在这两种情况下，整个表达式的值是可选的值。
```
let optionalSquare: Square? = Square(sideLength: 2.5, name: "iotional square")
let sideLength = optionalSquare?.sideLength
```

###枚举和结构体

使用`enum`来创建一个枚举。像类和其他所有类型一样，枚举可以有与他们相关联的方法
```
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```
```
练习
写一个函数来比较两个`Rank`的值，通过比较它们每一行的值。

答：
暂时不会
```

默认情况，Swift 会从零开始分配原始值，并每次增加一个，但可以通过显示指定值来改变这种行为。在上述例子中，`Ace`明确的给出了原始值1，其余的原始值按顺序分配。也可以使用字符串或者浮点型作为枚举的原始类型。使用`rawValue`属性访问枚举的值。

使用`init?(rawValue:)`构造器来初始化一个枚举实例,参数传行数。如果有就返回对应的值，没有就返回空。
```
if let convertedRank = Rank(rawValue: 3){
    let threeDescription = convertedRank.simpleDescription()
}
```


