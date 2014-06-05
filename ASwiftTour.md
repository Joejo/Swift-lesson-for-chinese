###简单值
Swift使用let关键字声明常量，var关键字声明变量。常量无需在编译时指定，但至少要被赋值一次。也就是说，赋值一次多次使用：
```
var myVariable = 42
myVariable = 50
let myConstant = 42
```
这里的常量赋值之后值不能更改，应该提高重用性。

　　一个常量或变量的值与类型必须是一致的。不过，你不需要指明它的类型，因为编译器会根据你所赋的值推断它的类型，在上面的例子中，编译器会判断到myVariable是一个整型（integer），因为它的初始值是一个整数。

　　如果初始值的信息不够明确（以至于类型不好判断），可以在变量名后用冒号写明类型：
```
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```
    练习：
    创建一个常量，类型为Float，值为4。
```
let implicitFloat: Float = 70
```
　　值永远不会隐含转换到其他类型。如果你需要转换一个值到其它不同类型，明确的构造一个所需类型的实例。
```
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```
<br>
    练习：
    试着删除String方法，你会得到什么错误？
<br>
还有一种更简单的字符串中含值的方式：把值放在小括号里面，并以反斜线开头，如：
<br>
```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit.
```
<br>
    练习：
    使用 \() 来包含一个浮点数计算到字符串，并包含某人的名字来问候。
<br>
```
let pie:Double = 3.14

let pin:Double = 3.15

let greetPie = "hello,\(pie + pin)"
```
<br>
用[]创建数组或字典，并使用下标或键名访问：
<br>
```
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"
var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
  ]
occupations["Jayne"] = "Public Relations”
```
<br>
创建一个空数组或字典，使用初始化赋值语句：
<br>
```
let emptyArray = String[]()
let emptyDictionary = Dictionary<String, Float>()
```
<br>
如果类型信息无法推断，你可以写空的数组-- "[]" 或空的字典--"[:]"，例如你为变量赋新值或为函数传参:
<br>
```
shoppingList = []   //Went shopping and bought everything.
```
<br>
###流程控制
<br>
Swift用if和switch编写条件控制语句，用for-in，for，while和do-while编写循环。条件控制语句和循环语句中，小括号是可选的，但花括号包住这个循环体是必须的：
<br>
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
 teamScore
```　
<br>
####If语句
<br>
在if语句中，条件必须是布尔值，也就是说，if score { ... }这个条件句是错误的，不是一个隐式地与0比较的条件。
<br>
你可以结合if和let来防止这种值的丢失状况。这些值意味着可选，这种可选值要么包含一个具体的值要么包含一个nil(空)来指示它的值是不存在的。在值的类型后面加上？号来表示它为可选即可：
<br>
```
var optionalString: String? = "Hello"
optionalString == nil
 
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```
    练习：
    将 optionalName 赋值为 nil 。会发生什么？添加一个 else 条件句在 optionalName 为 nil 时设置一个不同的值试试。
<br>
一旦可选值为nil，条件为false时，花括号里的代码块将被跳过，否则，可选值将是未封装的并赋值给一个常量，这会让未封装的值在代码块作用域中可见。
<br>
####Switch语句
<br>
Switch语句支持任何数据类型而且支持多种比较，不限于整型或相等测试：
<br>
```
 let vegetable = "red pepper"
 switch vegetable {
 case "celery":
     let vegetableComment = "Add some raisins and make ants on a log."
 case "cucumber", "watercress":
     let vegetableComment = "That would make a good tea sandwich."
 case let x where x.hasSuffix("pepper"):
     let vegetableComment = "Is it a spicy \(x)?"
 default:
     let vegetableComment = "Everything tastes good in soup."
 }
```
    练习：
    移除default语句，看看会报什么错？
<br>
执行满足条件的case语句后，程序自动跳出，所以，无需给每个case语句加上break。
<br>
####For-In语句
<br>
使用for-in循环在字典中遍历时，提供一对名字来使用字典中的每一个名值对（如下例的number--numbers）：
```
 let interestingNumbers = [
     "Prime": [2, 3, 5, 7, 11, 13],
     "Fibonacci": [1, 1, 2, 3, 5, 8],
     "Square": [1, 4, 9, 16, 25],
 ]
 var largest = 0
 for (kind, numbers) in interestingNumbers {
     for number in numbers {
         if number > largest {
            largest = number
       }
    }
}
 largest
```
<br>
  练习：
  在上例中，添加一个变量来跟踪哪一个number是最大的，即最大的值是？
<br>
####While语句
<br>
使用while语句来重复执行一个代码块直到条件改变。条件可以置于句末以便代码至少执行一次：

```
 var n = 2
 while n < 100 {
    n = n * 2
 }
 n

 var m = 2
 do {
    m = m * 2
 } while m < 100
 m
```
<br>
####For语句
<br>
for循环中可以使用索引值，利用..（两个点）或者明确声明一个初始值，条件句或增量来限制索引的范围，下面的两个循环意思一样：
<br>
```
 var firstForLoop = 0
 for i in 0..3 {
    firstForLoop += i
 }
 firstForLoop
 var secondForLoop = 0
 for var i = 0; i < 3; ++i {
    secondForLoop += 1
}
secondForLoop
```
<br>
使用 ..(两个点)限制索引的范围并忽略最高值，而用 ...(三个点) 构造的范围则包含两个值。
<br>
###函数与闭包
<br>
###Function 函数

Swift使用func关键字来声明函数，函数通过函数名加小括号内的参数列表来调用。使用->来区分参数名和返回值的类型：
```
1 func greet(name: String, day: String) -> String {
2     return "Hello \(name), today is \(day)."
3 }
4 greet("Bob", "Tuesday")
```
    练习：
    remove day参数，增加一个参数，比如：今天的午餐特色菜~
```
1 func greet(name:String, day:String) -> String{
2 
3 　　return "Hello \(name), today is \(day)."  //第二章说过用\()来内嵌变量
4 
5 }
6 
7 greet('Joe', '菩提玉斋')
```

 

函数使用元组(tuple)来返回多个值：
```
1 func getGasPrices() -> (Double, Double, Double) {
2     return (3.59, 3.69, 3.79)
3 }
4 getGasPrices()
```
函数还可以接收可变的参数个数，将这些参数收集在数组里面：
```
1 func sumOf(numbers: Int...) -> Int {
2     var sum = 0
3     for number in numbers {
4         sum += number
5     }
6     return sum
7 }
8 sumOf()
9 sumOf(42, 597, 12)
```
    练习：
    编写一个函数并求出其参数的平均值。

函数是可以嵌套的，嵌套过的函数可以访问到外部函数声明过的变量，使用函数嵌套可以便于你组织过长或复杂的函数：
```
1 func returnFifteen() -> Int {
2     var y = 10
3     func add() {
4         y += 5
5     }
6     add()
7     return y
8 }
9 returnFifteen()
```

在Swift中，函数是第一等类型，这意味着一个函数可以将另外一个函数作为它的返回值：
```
1 func makeIncrementer() -> (Int -> Int) {
2     func addOne(number: Int) -> Int {
3         return 1 + number
4     }
5     return addOne
6 }
7 var increment = makeIncrementer()
8 increment(7)
```

函数还能接收其它函数作为它的参数：
```
 1 func hasAnyMatches(list: Int[], condition: Int -> Bool) -> Bool {
 2     for item in list {
 3         if condition(item) {
 4             return true
 5         }
 6     }
 7     return false
 8 }
 9 func lessThanTen(number: Int) -> Bool {
10     return number < 10
11 }
12 var numbers = [20, 19, 7, 12]
13 hasAnyMatches(numbers, lessThanTen)
```　　
####Closure 闭包

　　
函数其实是一种闭包的特殊情况，你可以写一个用花括号{}包裹的匿名闭包，用in来区分参数与主体的返回类型：
```
1 numbers.map({
2     (number: Int) -> Int in
3     let result = 3 * number
4     return result
5     })
```
    练习：
    重写这个闭包来对所有奇数返回0

 

闭包有多种简洁的写法。当返回值类型已知时，比如委托回调，你就可以省略它的参数类型，它的返回值类选，或者二者都略去，单行语句的闭包可以直接隐式地返回此一语句的值：

1 numbers.map({ number in 3 * number })
 

你可以通过数字而不是名字来引用一个参数，这对于很短的闭包非常有用。一个闭包通过圆括号传递其最后一个参数到函数能立即生效：
```
1 sort([1, 5, 3, 12, 2]) { $0 > $1 }
```
<br>
###对象和类
<br>
####Class 类

 

在Swift中可以用class关键字后跟类名创建一个类。在类里，一个属性的声明写法同一个常量或变量的声明写法一样，除非这个属性是在类的上下文里面，否则，方法和函数的写法也是这样：
```
1 class Shape {
2     var numberOfSides = 0
3     func simpleDescription() -> String {
4         return "A shape with \(numberOfSides) sides."
5     }
6 }
```
    练习：
    用let关键字添加一个常量属性，添加另一个方法用来接收参数。

 

在类名后面加小括号来创建类的实例化，使用.（点号连接符）来访问实例的方法和属性：
```
1 var shape = Shape()
2 shape.numberOfSides = 7
3 var shapeDescription = shape.simpleDescription()
```

这个版本的Shape类缺少一个重要的东西：构造器--类被创建后的设置。可以使用init来创建一个：
```
 1 class NamedShape {
 2     var numberOfSides: Int = 0
 3     var name: String
 4     
 5     init(name: String) {
 6         self.name = name
 7     }
 8     
 9     func simpleDescription() -> String {
10         return "A shape with \(numberOfSides) sides."
11     }
12 }
```
注意，此处的self是用来区分构造器内的name参数和name属性的。创建类的实例时，构造器里的参数传递和函数的参数传递形式是一样的。每个属性都需要为其指定一个值，无论是在声明中（如nameOfSides），或是在构造器内（如name）。

使用 deinit 来创建一个析构器，来执行对象销毁时的清理工作。

 

####继承和多态

 

子类可以加冒号后直接跟超类名，子类声明时并不需要非得制定任何标准基类，所以子类后的超类可以被忽略。

子类的方法覆盖或重载超类中的实现要加上override标记，否则，编译器会报错，编译器也会检测被标记为override的重载方法到底有没有覆盖到超类。

 
```
 1 class Square: NamedShape {//接上一例，NamedShape为超类
 2     var sideLength: Double
 3     
 4     init(sideLength: Double, name: String) {
 5         self.sideLength = sideLength
 6         super.init(name: name)
 7         numberOfSides = 4
 8     }
 9     
10     func area() ->  Double {
11         return sideLength * sideLength
12     }
13     
14     override func simpleDescription() -> String {//在此处用override重载了上一例中超类NameSpace的方法simpleDescription
15         return "A square with sides of length \(sideLength)."
16     }
17 }
18 let test = Square(sideLength: 5.2, name: "my test square")
19 test.area()
20 test.simpleDescription()
```

    练习：
    编写另一个NamedShape的子类：Circle ，传入半径和名字作为参数到其构造器，并在Circle类中实现area和describe方法。

此外，声明过的属性通常还有一个get和一个set方法：
```
 1 class EquilateralTriangle: NamedShape {
 2     var sideLength: Double = 0.0
 3     
 4     init(sideLength: Double, name: String) {
 5         self.sideLength = sideLength
 6         super.init(name: name)
 7         numberOfSides = 3
 8     }
 9     
10     var perimeter: Double {
11     get {
12         return 3.0 * sideLength
13     }
14     set {
15         sideLength = newValue / 3.0
16     }
17     }
18     
19     override func simpleDescription() -> String {
20         return "An equilateral triagle with sides of length \(sideLength)."
21     }
22 }
23 var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
24 triangle.perimeter
25 triangle.perimeter = 9.9
26 triangle.sideLength
```　

上例中，perimeter的set中值的默认名是newValue，你可以再set后面以小括号的方式为其指定其它的名字。

请注意， EquilateralTriangle类的构造器有三个不同的步骤：

    第一步，设置子类各个属性的值；
    第二步，调用超类的构造器；
    第三步，改变超类中定义的属性的值，其它的方法，get，set等都可以在此一步骤实行。

如果你不需要计算属性的值，但是想在设置属性值之前或之后执行代码，那么你可以使用willset(之前)和didset(之后)。如下例中的类--确保三角形的边长始终与矩形边长相等：
```
 1 class TriangleAndSquare {
 2     var triangle: EquilateralTriangle {
 3     willSet {
 4         square.sideLength = newValue.sideLength
 5     }
 6     }
 7     var square: Square {
 8     willSet {
 9         triangle.sideLength = newValue.sideLength
10     }
11     }
12     init(size: Double, name: String) {
13         square = Square(sideLength: size, name: name)
14         triangle = EquilateralTriangle(sideLength: size, name: name)
15     }
16 }
17 var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
18 triangleAndSquare.square.sideLength
19 triangleAndSquare.triangle.sideLength
20 triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
21 triangleAndSquare.triangle.sideLength
``` 

类的方法与函数有一个重要的区别：函数的参数名仅作用于此函数内，而方法的参数名可以用于调用方法（第一个参数除外）。缺省时，一个方法有一个同名的参数，调用时就是方法本身。你可以指定第二个名字，在方法内部使用：
```
1 class Counter {
2     var count: Int = 0
3     func incrementBy(amount: Int, numberOfTimes times: Int) {
4         count += amount * times
5     }
6 }
7 var counter = Counter()
8 counter.incrementBy(2, numberOfTimes: 7)
```

当与可选值（详见第三章的If语句介绍）一起工作时，你可以在方法或属性前写 "?" 操作符。如果值在"?"之前就已经是 nil ，所有在 "?" 之后的都会自动忽略，而整个表达式是 nil 。另外，可选值是未封装的，所有 "?" 之后的都作为未封装的值。在这两种情况中，整个表达式的值是可选值：
```
1 let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")//?可选值的介绍详见第三章的If语句部分
2 let sideLength = optionalSquare?.sideLength
```


###Enumerations 枚举

 

使用 enum 来创建一个枚举。跟Classes(类)和其他类型的命名方式一样，枚举也可以有Method(方法)。
```
 1 enum Rank: Int {
 2     case Ace = 1
 3     case Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten
 4     case Jack, Queen, King
 5     func simpleDescription() -> String {
 6         switch self {
 7         case .Ace:
 8             return "ace"
 9         case .Jack:
10             return "jack"
11         case .Queen:
12             return "queen"
13         case .King:
14             return "king"
15         default:
16             return String(self.toRaw())
17         }
18     }
19 }
20 let ace = Rank.Ace
21 let aceRawValue = ace.toRaw()
```
    练习：
    创建一个函数，通过原始值的类比来比较两个rank的值。

在上例中，原始值的类型是 Int ，所以你可以只指定第一个原始值就可以了，因为后面的原始值都是按照顺序赋值的。你还也可以使用字符串或浮点数作为枚举的原始值。

使用toRaw和fromRaw函数可以实现原始值和枚举值间的转换：
```
1 if let convertedRank = Rank.fromRaw(3) {
2     let threeDescription = convertedRank.simpleDescription()
3 }
```
枚举出来的值就是实际值，而不是其他方式写的原始值。（这句话的意思应该就是说枚举值和原始值没有必然的关联性）为了防止枚举无意义的原始值，你不需要特意提供一个原始值：
```
 1 enum Suit {
 2     case Spades, Hearts, Diamonds, Clubs
 3     func simpleDescription() -> String {
 4         switch self {
 5         case .Spades:
 6             return "spades"
 7         case .Hearts:
 8             return "hearts"
 9         case .Diamonds:
10             return "diamonds"
11         case .Clubs:
12             return "clubs"
13         }
14     }
15 }
16 let hearts = Suit.Hearts
17 let heartsDescription = hearts.simpleDescription()
```
    练习：
    给枚举Suit创建一个名为color的方法，让Spades和Clubs返回“black”，让Hearts和Diamonds返回“red”。

请注意上例中引用Hearts成员的两种方式：当给常量Hearts赋值时，Suit.Hearts是全名引用，因为此时的常量Hearts没有一个明确的类型。而在switch内部，枚举通过缩略形式：.Hearts来引用，因为 self 的值对于枚举成员是已知的。当值的类型已知时，你可以随时使用缩略形式(去引用)。

 

###Structures 结构

 

使用struct关键字创建来创建结构。结构体支持类（Classes）的许多行为：如，方法（methods）和构造器(initializers)。结构体与类最重要的区别是，在代码中，结构体通过拷贝（copy）来实现值的传递，而类则是通过引用（reference）：
```
1 struct Card {
2     var rank: Rank
3     var suit: Suit
4     func simpleDescription() -> String {
5         return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
6     }
7 }
8 let threeOfSpades = Card(rank: .Three, suit: .Spades)
9 let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```
    练习：
    添加一个Card方法来创建一副纸牌，每一张牌都含有一个Rank和Suit的组合。

一个枚举成员的实例可以拥有实例的值。相同枚举成员的实例可以有不同的值。你在创建实例时可以给它指定一个值。指定值和原始值的区别在于：枚举的原始值与所有实例相同，原始值是你在定义枚举时提供的。

例如：有一个场景，需要你从服务器中请求太阳升起和降落的时间，服务器可以响应给你相应的信息，也能给你返回错误的信息：
```
 1 enum ServerResponse {
 2     case Result(String, String)
 3     case Error(String)
 4 }
 5  
 6 let success = ServerResponse.Result("6:00 am", "8:09 pm")
 7 let failure = ServerResponse.Error("Out of cheese.")
 8  
 9 switch success {
10 case let .Result(sunrise, sunset):
11     let serverResponse = "Sunrise is at \(sunrise) and sunset is at \(sunset)."
12 case let .Error(error)://请求错误时返回的信息--Joe.Huang
13     let serverResponse = "Failure...  \(error)"
14 }
```
    练习：
    在switch语句里给ServerResponse添加第三种情况（case）。

请注意：（上例中）ServerResponse所返回的日出与日落时间是switch中所匹配的情况（case）。















