# 第一章 Flutter 学习与开发

## 1.1 学习 Dart 语言

Dart 基本就是 `JavaScript` 和 `Java` 的结合体，官网：https://dart.dev/。这里推荐阅读这篇专栏进行一个入门学习：https://juejin.cn/column/7002416628709195790



### 1.1.1 Dart 基础解析

**var、late、final 和 const**

- 参考文档一：https://juejin.cn/post/7003547549554442248
- 参考文档二：https://juejin.cn/post/6844903897123799054
- 关键字 var：声明一个可空变量，类型会自动推断
- 关键字 late：声明一个不可空的变量，并在声明后初始化，主要用途是延迟初始化变量
- 关键字 final：final 常量只能被赋值一次，不可被修改，**相当于 JS 里的 const**
- 关键字 const：在左边时作用是声明变量，并且必须在初始化时赋值，不可被修改。在右边时表示修饰符，它意味着对象的整个深度状态可以在编译时完全确定，并且对象将被冻结并且完全不可变

```dart
// const在右边可创建编译时常量对象，这样编译器可以对其进行优化，在编译时就分配好内存，而不是在运行时动态创建对象
Future<String> testFuture() {
  return Future<String>.delayed(const Duration(seconds: 2), () {
    return "Hello World";
  });
}
```

- 关键字 static：在类中声明一个静态属性，使得多个相同类型的类对象共享同一个成员变量的实例，并且类外不允许访问

```dart
// 通常声明变量时不用带类型，所以使用关键字 var、const 即可，但是直接用类型生成一个变量又可以省略关键字
vat n = 12.22;
int i = 12; // 等效与js代码就是const i: int = 12;
```



### 1.1.2 Dart 类型解析

主要介绍 Dart 内置对象的使用，常规的类型可以参考文档：https://juejin.cn/post/7003603047133741064

- `num`、`int`、`double`、`bool`、`String`：常见类型
- `Object`：所有 Dart 类的超类，除了 Null
- `Future和Stream`：用于异步支持
- `Iterable`：用于 for-in 循环和同步生成器函数中
- `Never`：表示表达式永远不能成功地完成求值，最常用于总是抛出异常的函数
- `dynamic`：关闭静态检查，通常你应该使用 Object 或 Object? 代替
- `void`：表示某个值从未被使用，通常用作返回类型



**dynamic 动态类型**

- 可以赋予任何类型的值，编译器不会对其进行静态类型检查。
- 用法相当于 TS 里面的 any 类型



**Lists 数组类型**

- 区分变量、编译时常量和变量的区别：https://juejin.cn/post/7003603047133741064#heading-4
- 使用扩展操作符：https://juejin.cn/post/7003603047133741064#heading-5



**Set、Map 类型**

- 三种创建 Set 变量的方式：`Set<String> names = {}`、`var names = <String>{}`、`var gifts = Set<String>()`
- Map 创建的方式也类似，并且是键值对形式，这里的 map 就类似于 js 的对象



### 1.1.3 Dart 函数解析

参考文档：https://juejin.cn/post/7003951983853830151



**函数定义**

- 标准函数写法：`isNumber(int index) { return list[index] != null; }`
- 当函数只有一条语句时可以使用箭头函数来简写：`bool isNumber(int index) => list[index] != null;`



**函数参数**

- 一共有三种类型的参数：普通参数、命名参数、位置参数

```dart
// 普通参数
void greet(String name, int age) {
  print("Hello, $name! You are $age years old.");
}
greet("Alice", 25);

// 命名参数
void greet({String name = "Guest", int age = 18, required int count}) {
  print("Hello, $name! You are $age years old.");
}
greet(name: "Alice", age: 25, count: 11);
  
// 位置参数
void greet(String name, [int? age, num count = 12]) {
  print("Hello, $name! ${age == null ? "How old are you?" : "You are $age years old."}");
}
greet('cocoon', 18)
```



**匿名函数**

- 匿名函数也称为 Lambda 表达式 或 Closure 闭包，可以赋值给一个变量然后使用它，或者作为函数的参数使用
- 参考文档：https://juejin.cn/post/7003951983853830151#heading-7



### 1.1.4 Dart 类解析

**构造函数**

- **普通构造函数**：定义一个和类名字一样的方法就定义了一个构造函数，给内置属性赋值时可以使用语法糖，直接通过 this 赋值并且函数体可以直接省略

```dart
// 给自身属性赋值
Point(this.x, this.y);
// 给父类属性赋值 
Circle(super.x, super.y);
// 通过常量构造函数和命名式入参赋值
const HttpStudy({super.key});
```

- **初始化列表**：它是一种在构造函数体执行之前初始化字段的方式，通常用于需要提前初始化的字段或者调用父类的构造函数

```dart
// 调用父类构造函数
Child(String name, this.age) : super(name);

// 通过初始化列表计算字段值
Circle(this.radius) : area = 3.14 * radius * radius;
```

- **super**：初始化父类构造函数使用 `super`,必须放在初始化列表里面去执行

```dart
Student(String name, int age, String gender, this.school) { super(name, age, gender) }
```

- **命名构造函数**：使用 类名.方法名 的形式定义，可以为类提供多个构造函数，更加灵活！

```dart
class MyClass {
  final int x;
  final int y;

  // 命名构造函数
  MyClass.zero() : x = 0, y = 0; // 初始化为(0, 0)
  MyClass.init() {
    ...
  }
}
```

- **工厂构造函数**：可以返回任意对象（包括子类或缓存实例），无法直接访问类的字段，下面是一个单例模式实例：

```dart
void main() {
  Logger logger1 = Logger();
  Logger logger2 = Logger();
  print(identical(logger1, logger2)); // true
}

class Logger {
  static Logger? _cache;
  static final Logger _instance = Logger._internal();
  Logger._internal() {
    print('Logger created');
  }
  factory Logger() {
    _cache ??= _instance;
    return _cache!;
  }
}
```



**常量构造函数**

在 Dart 中，要定义一个常量构造函数，必须满足以下条件：

1. 类的所有字段必须是 final 类型。
2. 构造函数不能有函数体。
3. 初始化列表中的值必须是编译时常量。
4. 如果继承父类，父类的构造函数也必须是常量构造函数。
5. 所有字段必须通过构造函数参数或初始化列表初始化。

之后就可以使用 const 构造函数创建高效的编译时常量对象。

```dart
class Base {
  final Key? key;
  const Base({this.key});
}

class Echo extends Base {
  final String data;
  const Echo({Key? key, required this.data}) : super(key: key); // 调用父类的常量构造函数
}

const e = Echo(data: 'cocoon')
```



**getter 和 setter**

- getter：是一个无需参数的方法，调用时像访问普通属性一样
- setter：是一个带有单个参数的方法，调用时像赋值操作一样

```dart
class Rectangle {
  double _width = 0;
  double _height = 0;

  // Setter
  set width(double value) {
    if (value > 0) {
      _width = value;
    } else {
      print("Width must be positive.");
    }
  }

  // Getter
  double get area => _width * _height;
}

void main() {
  final rect = Rectangle();
  rect.width = 10; // 调用 setter
  print("Rectangle area: ${rect.area}"); // 输出: Rectangle area: 50
}
```



**抽象类的继承与实现**

- **abstract**：抽象类是一种不能被直接实例化的类，通常用于定义子类的通用行为和接口。通过继承和实现抽象类，可以构建多态的、可扩展的代码结构。可以包含抽象方法（不带实现）和具体方法（带实现）

```dart
abstract class Animal {
  void eat(); // 抽象方法
  void sleep() {
    print("Sleeping...");
  } // 具体方法
}
```

- **抽象类的继承**：子类通过 extends 继承抽象类，可以继承其的具体方法和字段，并且子类必须实现抽象类中所有的抽象方法

```dart
abstract class Animal {
  void eat(); // 抽象方法
  void sleep() {
    print("Sleeping...");
  } // 具体方法
}

class Dog extends Animal {
  @override
  void eat() {
    print("Dog eats bones.");
  }
}
```

- **抽象类的实现**：抽象类也可以作为接口使用，子类使用 implements 来实现抽象类，实现类必须实现抽象类中的所有方法

```dart
abstract class Animal {
  void eat();
  void sleep() {
    print("Sleeping...");
  }
}

class Bird implements Animal {
  @override
  void eat() {
    print("Bird eats seeds.");
  }
  @override
  void sleep() {
    print("Bird sleeps in the nest.");
  }
}
```



**混合（mixin）**

由于之类只能继承一个父类，于是我们可以使用 mixin 将一组功能添加到多个类中，而无需使用继承。这种机制避免了单继承的限制，同时提供了一种灵活的代码共享方式。

```dart
mixin Flyer {
  void fly() {
    print("Flying");
  }
}
mixin Swimmer {
  void swim() {
    print("Swimming");
  }
}
class Duck with Flyer, Swimmer {}
void main() {
  Duck duck = Duck();
  duck.fly();  // 输出: Flying
  duck.swim(); // 输出: Swimming
}
```



### 1.1.5 Dart 场景应用

#### 1.1.5.1 JSON 转换

**Dart 实现 JSON 类型和 map 类型的转换**

- 通过引入内置库：dart:convert
- json.encode：将 Dart 的 Map 转换为 JSON 字符串
- json.decode：将 JSON 字符串解析为 Dart 的 Map

```dart
import 'dart:convert';

void main() {
  // JSON 字符串
  String jsonString = '{"name": "Dart", "version": 3.0, "isStable": true}';
  
  // 解析 JSON 字符串为 Map
  Map<String, dynamic> jsonMap = json.decode(jsonString);
  
  print(jsonMap); // 输出: {name: Dart, version: 3.0, isStable: true}
  print(jsonMap['name']); // 输出: Dart
}
```



**Dart 实现 JSON 类型和实体类的转换**

通过 JSON 转 Dart 实体类在线网站获取实体类代码：https://www.bejson.com/jsontool/jsonzhuandart/

```dart
class Data {
  int code;
  String method;
  String requestPrams;

  Data({this.code, this.method, this.requestPrams});

  Data.fromJson(Map<String, dynamic> json) {
    code = json['code'];
    method = json['method'];
    requestPrams = json['requestPrams'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = new Map<String, dynamic>();
    data['code'] = this.code;
    data['method'] = this.method;
    data['requestPrams'] = this.requestPrams;
    return data;
  }
}
```

- 通过调用实体类的 formJson 和 toJson 来进行相互转换

```dart
Data d = Data.fromJson({"code":0,"data":{"code":0,"method":"POST","requestPrams":"11"},"msg":"SUCCESS."});
String s = Data.toJson(d)
```



#### 1.1.5.2 定时器

https://juejin.cn/post/7006936349710221343

```dart
import 'dart:async';
Timer(Duration(seconds: 2), () => {print('这是一次性定时器,延迟2秒执行')});
```



#### 1.1.5.3 Future

理解上几乎和 Promise 一致，参考文档：https://juejin.cn/post/7403547816915795994

```dart
// async-await
void main() async{
  final str = await fetchData();
  final arr = await Future.wait([fetchData(), fetchData2()]);
  print("All done!");
}

Future<String> fetchData() async {
  await Future.delayed(const Duration(seconds: 5));
  return "fetchData";
}

Future<String> fetchData2() async {
  await Future.delayed(const Duration(seconds: 3));
  return "fetchData2";
}
```

```dart
Future<String> fetchData() async {
  Future.delayed(Duration(seconds: 2)).then((e) {
  setState(() {
    //重新构建列表
    _words.insertAll(
      _words.length - 1,
      //每次生成20个单词
      generateWordPairs().take(20).map((e) => e.asPascalCase).toList(),
    );
  });
});
}
```



#### 1.1.5.4 Dart 迭代器

在 Dart 中，许多集合方法会返回 Iterable 类型，特别是当你调用集合上的一些操作时，返回值是一个可以懒加载的迭代器对象，而不是具体的集合类型（如 List）。Iterable 类型是一个抽象集合接口，它允许你对其元素进行按需访问。将 Iterable 类型转换为 List 类型非常简单，你可以使用 Dart 中的 toList() 方法。这是 Iterable 类的一部分，它会将 Iterable 中的元素转换成一个新的 List，并返回这个 List。

```dart
List<int> numbers = [1, 2, 3, 4, 5];
Iterable<String> stringNumbers = numbers.map((n) => "Number: $n");
List<String> listOfStringNumbers = stringNumbers.toList();
print(listOfStringNumbers);  // 输出 ["Number: 1", "Number: 2", "Number: 3", "Number: 4", "Number: 5"]
```



**where**

**功能**：用于过滤集合，返回一个新的 Iterable，其中包含满足条件的元素。

```dart
List<int> numbers = [1, 2, 3, 4, 5];
Iterable<int> evenNumbers = numbers.where((n) => n.isEven);
print(evenNumbers); // 输出 (2, 4)
```



**map**

**功能**：将集合中的每个元素应用给定的函数，返回一个新的 Iterable，每个元素变换后的结果。

```dart
List<int> numbers = [1, 2, 3];
Iterable<String> stringNumbers = numbers.map((n) => "Number: $n");
print(stringNumbers); // 输出 (Number: 1, Number: 2, Number: 3)
```



**expand**

**功能**：将集合中的每个元素展开成多个元素，返回一个新的 Iterable，由多个展开的元素组成。

```dart
List<int> numbers = [1, 2, 3];
Iterable<int> expandedNumbers = numbers.expand((n) => [n, n * 2]);
print(expandedNumbers); // 输出 (1, 2, 2, 4, 3, 6)
```



**take**

**功能**：从集合的开头取出前 N 个元素，返回一个新的 Iterable。

```dart
List<int> numbers = [1, 2, 3, 4, 5];
Iterable<int> firstThreeNumbers = numbers.take(3);
print(firstThreeNumbers); // 输出 (1, 2, 3)
```



**skip**

**功能**：跳过集合的前 N 个元素，返回一个新的 Iterable。

```dart
List<int> numbers = [1, 2, 3, 4, 5];
Iterable<int> remainingNumbers = numbers.skip(2);
print(remainingNumbers); // 输出 (3, 4, 5)
```



**distinct**

**功能**：返回一个不重复的 Iterable，去除集合中的重复元素（需要导入 dart:collection）。

```dart
import 'dart:collection';

List<int> numbers = [1, 2, 2, 3, 4, 4];
Iterable<int> distinctNumbers = LinkedHashSet<int>.from(numbers);
print(distinctNumbers); // 输出 (1, 2, 3, 4)
```



**followedBy**

**功能**：将两个集合连接在一起，返回一个新的 Iterable，包含原集合的所有元素，后跟另一个集合的所有元素。

```dart
List<int> numbers1 = [1, 2];
List<int> numbers2 = [3, 4];
Iterable<int> combined = numbers1.followedBy(numbers2);
print(combined); // 输出 (1, 2, 3, 4)
```



**takeWhile**

**功能**：从集合的开头取出直到满足条件的元素，返回一个新的 Iterable，直到条件不再成立为止。

```dart
List<int> numbers = [1, 2, 3, 4, 5];
Iterable<int> taken = numbers.takeWhile((n) => n < 4);
print(taken); // 输出 (1, 2, 3)
```



**forEach()**

**功能**：对集合中的每个元素执行一个函数，虽然它不会返回一个新的 Iterable，但也通过迭代对每个元素进行操作。

```dart
List<int> numbers = [1, 2, 3];
numbers.forEach((number) {
  print(number);
}); 
```



## 1.2 Flutter 学习初步

### 1.2.1 开发环境搭建

**Flutter SDK**

- 先下载 Dart：brew install dart
- 下载 Flutter SDK，并配置环境变量：本地安装路径：/Users/cocoon/Applications/Flutter，export PATH=$HOME/Applications/Flutter/bin:$PATH
- 想要切换 SDK 版本只需要进入文件夹切换分支即可，通过 flutter doctor 命令查看环境是否都配置成功
- 如果没有开梯子则需要设置 Flutter 镜像：https://docs.flutter.cn/community/china



**Android Studio 和 Android SDK**

- 参考 Flutter 官网安卓开发配置：https://flutter.cn/docs/get-started/install/macos/mobile-android?tab=download

- 直接进入官网下载 IDE，进入 IDE 之前会要求你下载 Android SDK：https://developer.android.google.cn/studio?hl=zh-cn
- Android SDK 本地下载地址：/Users/cocoon/Applications/Android
- 除了 SDK，还下载了其他工具，进入设置 - 语言和框架 - Android SDK 中查看，并且还可以扩展下载
- 配置 Android 环境变量（主要用于 adb 命令）：https://blog.csdn.net/MirkoWug/article/details/126948260



**配置时遇到的问题**

- 需要获取安卓许可和下载好列表上的安卓模拟器运行工具：https://flutter.cn/docs/get-started/install/macos/mobile-android?tab=download#configure-your-target-android-device
- Android Studio 运行项目时卡在 Running gradle assembleDebug：需要外网环境，或者修改 SDK 和项目安卓目录的镜像源：https://blog.csdn.net/Yyongchao/article/details/136896379



**Xcode 和 IOS Simulator**

- 参考 Flutter 官网 IOS 开发配置：https://docs.flutter.cn/get-started/install/macos/mobile-ios
- 下载好Xcode 和 IOS Simulator 后，通过输入命令 open -a Simulator 运行即可
- 依然使用 Android Studio 将 Flutter 项目运行到 IOS Simulator 上面



**Flutter 开发与调试**

- 和 IDEA 编辑模式一致，编辑之后会自动保存文件，通过 opt + cmd + l 格式化代码
- 启动项目后每次修改完文件，可以按 cmd + s 或者手动点击闪电图标进行热更新
- 插件 FlutterSnippets 实现代码快捷生成

```md
stful -> 生成一个StatefulWidget
stless -> 生成一个StatelessWidget 
```



### 1.2.2 项目应用层功能

#### 1.2.2.1 Http 接口联调

依赖 Http 库: https://pub.dev/packages/http

```dart
import 'package:http/http.dart' as http;

_doGet() async {
  var uri =
      Uri.parse('https://api.geekailab.com/uapi/test/test?requestPrams=11');
  var response = await http.get(uri);
  if (response.statusCode == 200) {
    setState(() {
      resultShow = response.body;
    });
  } else {
    setState(() {
      resultShow = "请求失败：code: ${response.statusCode} body:${response.body}";
    });
  }
}

_doPost() async {
  var uri = Uri.parse('https://api.geekailab.com/uapi/test/test');
  var response = await http.post(uri, body: {'requestPrams': '11'});
  if (response.statusCode == 200) {
    setState(() {
      resultShow = response.body;
    });
  } else {
    setState(() {
      resultShow = "请求失败：code: ${response.statusCode} body:${response.body}";
    });
  }
}
```



#### 1.2.2.2 数据缓存方案

依赖 shared_preferences 库: https://pub.dev/packages/shared_preferences

```dart
import 'package:shared_preferences/shared_preferences.dart';

Future<void> saveData() async {
  final preferences = await SharedPreferences.getInstance();
  await preferences.setString('name', '张三');
}

Future<void> getData() async {
  final preferences = await SharedPreferences.getInstance();
  final namePre = preferences.getString('name');
  setState(() {
    name = namePre ?? '';
  });
  print('name: $name');
}
```



#### 1.2.2.3 布局问题方案

 **使用 Row 和 Column 时子 widget 超出屏幕范围溢出错误**

- 使用 Expanded：可以使子组件自定义分配空间，避免它们超出屏幕范围

- 使用 SingleChildScrollView：超出屏幕范围时，滚动查看所有内容
- 使用 Wrap：Wrap 会根据父容器的尺寸自动换行或换列，避免溢出错误
- 限制子组件的尺寸：使用 SizedBox 或 ConstrainedBox 来限制子组件的尺寸



### 1.2.3 认识基础 Widget

#### 1.2.3.1 Text 文本

参考文档：https://book.flutterchina.club/chapter3/text.html#_3-1-1-text

一个 Text Widget 特性是宽度就是它的内容宽度，宽度最大为父级容器的宽度，如果内容超出则默认换行展示，下面是它的一些属性：

```dart
Text("Hello world! I'm Jack. "*4,
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
  textAlign: TextAlign.left,
  textScaleFactor: 1.5, // 最新版已弃用
  textScaler: const TextScaler.linear(5),   
);
```

一个 Text Widget 只能有一个文本样式并且通过 TextStyle 生成：

```dart
Text("Hello world",
  style: TextStyle(
    color: Colors.blue,
    fontSize: 18.0,
    height: 1.2, // 行高 
    fontFamily: "Courier",
    background: Paint()..color=Colors.yellow,
    decoration:TextDecoration.underline,
    decorationStyle: TextDecorationStyle.dashed
  ),
);
```

如果想在一个 Text Widget 中实现多个样式的文本，则可以使用下面的方式 Text.rich + TextSpan 组合 ：

```dart
Text.rich(TextSpan(
  children: [
   TextSpan(
     text: "Home: "
   ),
   TextSpan(
     text: "https://flutterchina.club",
     style: TextStyle(color: Colors.blue)
   ),
  ]
))
```

导入字体方案

参考文档：https://book.flutterchina.club/chapter3/text.html#_3-1-5-%E5%AD%97%E4%BD%93，在根目录下新建 fonts 文件夹存储字体，在 pubspec.yaml 添加以下配置

```yaml
flutter:
  fonts:
    - family: PlaywriteIN
      fonts:
        - asset: fonts/PlaywriteIN-Thin.ttf
```

```dart
const Text(
  "Login with username",
  style: TextStyle(color: Colors.white, fontSize: 30, fontFamily: 'PlaywriteIN'),
)
```



#### 1.2.3.2 ElevatedButton

按钮组件比较简单，就一个 Text 和 onPress 回调函数，如果没有传入回调函数则按钮为禁用状态，另外有一个`icon` 构造函数，通过它可以轻松创建带图标的按钮，参考文档：https://book.flutterchina.club/chapter3/buttons.html#_3-2-1-elevatedbutton



#### 1.2.3.3 Image、Icon

Flutter 里面支持 Image 和 Icon，使用文档：https://book.flutterchina.club/chapter3/img_and_icon.html

```dart
const Image({
  ...
  this.width, //图片的宽
  this.height, //图片高度
  this.color, //图片的混合色值
  this.colorBlendMode, //混合模式
  this.fit,//缩放模式
  this.alignment = Alignment.center, //对齐方式
  this.repeat = ImageRepeat.noRepeat, //重复方式
  ...
})
```



#### 1.2.3.4 Form Widget

TextField：文本输入框：https://book.flutterchina.club/chapter3/input_and_form.html#_3-5-1-textfield

Checkbox、Switch：https://book.flutterchina.club/chapter3/radio_and_checkbox.html



### 1.2.4 认识布局 Widget

#### 1.2.4.1 ConstrainedBox

参考：https://book.flutterchina.club/chapter4/constraints.html

`ConstrainedBox` 组件用于对子组件添加额外的约束，通过添加 BoxConstraints 条件来实现

```dart
// 定义了一个最小宽度100%，最小高度30px的红色盒子
Widget redBox = ConstrainedBox(
  constraints: const BoxConstraints(minHeight: 30, minWidth: double.infinity),
  child: const DecoratedBox(decoration: BoxDecoration(color: Colors.red)),
);
```

```dart
// BoxConstraints 默认的构造函数
const BoxConstraints({
  this.minWidth = 0.0, //最小宽度
  this.maxWidth = double.infinity, //最大宽度
  this.minHeight = 0.0, //最小高度
  this.maxHeight = double.infinity //最大高度
})
```

> 当有多重限制时（多层级都添加了 BoxConstraints 条件），对于 `minWidth` 和 `minHeight` 来说，是取层级中相应数值较大的。实际上，只有这样才能保证父限制与子限制不冲突。



`SizedBox` 用于给子元素指定固定的宽高，类似与 `ConstrainedBox` 的语法糖

```dart
SizedBox(
  width: 80.0,
  height: 80.0,
  child: redBox
);
// 等效于
ConstrainedBox(
  constraints: BoxConstraints.tightFor(width: 80.0,height: 80.0),
  // 等效于 constraints: BoxConstraints(minHeight: 80.0,maxHeight: 80.0,minWidth: 80.0,maxWidth: 80.0)
  child: redBox, 
);
```



BoxConstraints 拥有多个构造函数以便于快速生成高宽度模板，例如：

1. `BoxConstraints.expand()`：高宽度占满，等效于都为百分之百
2. `BoxConstraints.tightFor(width: 80.0,height: 80.0)`：指定高宽度



#### 1.2.4.2 Row、Column

参考：https://book.flutterchina.club/chapter4/row_and_column.html

`Row`、`Column` 都是基于 `Flex` 的封装，形成了高效的横纵线性布局组件，对于线性布局，有主轴和纵轴之分，如果布局是沿水平方向，那么主轴就是指水平方向，而纵轴即垂直方向；如果布局沿垂直方向，那么主轴就是指垂直方向，而纵轴就是水平方向。

`MainAxisAlignment` 决定主轴，`CrossAxisAlignment` 决定纵轴。

实际上，`Row` 和 `Column` 都只会在主轴方向占用尽可能大的空间，而纵轴的长度则取决于他们最大子元素的长度。



Row，主轴默认是水平方向，水平方向默认左对齐，垂直方向默认顶端对齐

```dart
Row({
  // 这两个属性搭配决定横轴的子元素排列
  MainAxisSize mainAxisSize = MainAxisSize.max, // Row在横轴所占用的空间   
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, // Row子元素的水平排列方式

  // 这两个属性搭配决定纵轴的子元素排列
  // Row子元素在纵轴是从下到上开始看，还是从上到下，作为crossAxisAlignment的参考系 
  VerticalDirection verticalDirection = VerticalDirection.down, 
  // 如果Row子元素在纵轴是从下到上开始看，那么设置CrossAxisAlignment.start时，子元素在垂直方向上是顶部对齐
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
  
  List<Widget> children = const <Widget>[],
})
```

```dart
Row(
  verticalDirection: VerticalDirection.up,
  crossAxisAlignment: CrossAxisAlignment.start,  
  children: <Widget>[
    Text(" hello world ", style: TextStyle(fontSize: 30.0),),
    Text(" I am Jack "),
  ], // 实现了垂直反向底部对齐，水平方向左端对齐
);
```



Column，主轴默认是垂直方向，水平方向默认左对齐，垂直方向默认顶端对齐

```dart
Column(
  crossAxisAlignment: CrossAxisAlignment.center,
  children: <Widget>[
    Text("hi"),
    Text("world"),
  ], // 实现了垂直方向顶部对齐，水平方向居中对齐
);
```



#### 1.2.4.3 Flex、Expanded

参考：https://book.flutterchina.club/chapter4/flex.html

**Flex 作为 Row、Column 的基类**，搭配 Expanded 实现了底层弹性布局。弹性布局允许子组件按照一定比例来分配父容器空间：

```dart
//Flex的两个子widget按1：2来占据水平空间  
Flex(
  direction: Axis.horizontal,
  children: <Widget>[
    Expanded(
      flex: 1,
      child: Container(
        height: 30.0,
        color: Colors.red,
      ),
    ),
    Expanded(
      flex: 2,
      child: Container(
        height: 30.0,
        color: Colors.green,
      ),
    ),
  ],
);
```



#### 1.2.4.4 Wrap、Flow

参考：https://book.flutterchina.club/chapter4/wrap_and_flow.html

Wrap 作为 Row、Column 的再进阶版本，首先支持子元素排序超出后自动换行，其次还可以给主轴或纵轴的子元素添加间距。

```dart
Wrap({
  this.direction = Axis.horizontal, // 主轴排列方向
  this.alignment = WrapAlignment.start, // 主轴对齐方式
  this.spacing = 0.0, // 主轴方向子元素之间的间距
  this.runAlignment = WrapAlignment.start, // 纵轴方向的对齐方式
  this.runSpacing = 0.0, // 纵轴方向子元素之间的间距
  List<Widget> children = const <Widget>[],
})
```



Flow 主要用于子元素的自定义排序，稍微有点复杂，并且使用率极低因此在这里不做笔记。



#### 1.2.4.5 Stack、Positioned

要使用绝对定位就必须要用到 Stack、Positioned 进行搭配。Stack 允许子组件堆叠，而 Positioned 用于根据 Stack 的四个角来确定子组件的位置。**层叠布局允许子组件按照代码中声明的顺序堆叠起来。**

Stack 构造函数如下：

```dart
Stack({
  this.alignment = AlignmentDirectional.topStart, // 当Positioned元素在某个方向上没有设置位置时则采用这个放置方式
  this.fit = StackFit.loose, // 此参数用于确定没有定位的子组件如何去适应Stack的大小
  this.clipBehavior = Clip.hardEdge, // 此属性决定对超出Stack显示空间的部分如何剪裁
  List<Widget> children = const <Widget>[],
})
```

```dart
// Stack的子组件默认实现相对定位，对齐方式由alignment决定
Stack(
  alignment: Alignment.center,
  children: <Widget>[
    ListView.builder(
      itemCount: 100,
      itemExtent: 50.0,
      itemBuilder: (context, index) => ListTile(title: Text("$index")),
    ),
    CircleAvatar(
      radius: 30.0,
      child: Text(_progress),
      backgroundColor: Colors.black54,
    )
  ],
)
```



Positioned 组件实现子组件自定义相对定位的位置，默认构造函数如下：

```dart
const Positioned({
  Key? key,
  this.left, 
  this.top,
  this.right,
  this.bottom,
  this.width,
  this.height,
  required Widget child,
})
```

> 举个例子，在水平方向时，你只能指定`left`、`right`、`width`三个属性中的两个，如指定`left`和`width`后，`right`会自动算出(`left`+`width`)



Stack 和 Positioned 搭配实现层叠布局的一个例子：

```dart
//通过ConstrainedBox来确保Stack占满屏幕
ConstrainedBox(
  constraints: BoxConstraints.expand(),
  child: Stack(
    alignment:Alignment.center , //指定未定位或部分定位widget的对齐方式
    children: <Widget>[
      Container(
        child: Text("Hello world",style: TextStyle(color: Colors.white)),
        color: Colors.red,
      ),
      Positioned(
        left: 18.0,
        child: Text("I am Jack"),
      ),
      Positioned(
        top: 18.0,
        child: Text("Your friend"),
      )        
    ],
  ),
);
```



#### 1.2.4.6 Align、Center

参考：https://book.flutterchina.club/chapter4/alignment.html

Align 只有一个子元素，根据确定的坐标原点直接在 Align 决定子元素的位置，它的定义如下：

```dart
Align({
  Key key,
  this.alignment = Alignment.center, // 子组件在父组件中的起始位置
  // widthFactor和heightFactor是用于确定Align组件本身宽高的属性
  // 它们是两个缩放因子，会分别乘以子元素的宽、高，最终的结果就是Align组件的宽高
  // 如果值为null，则组件的宽高将会占用尽可能多的空间，比如占满上一层元素的空间
  this.widthFactor,
  this.heightFactor,
  Widget child,
})
```



`alignment` 属性： 需要一个 AlignmentGeometry 类型的值，AlignmentGeometry 是一个抽象类，它有两个常用的子类：Alignment 和 FractionalOffset，它们的偏移量有一定的公式用于计算，这里不深入做笔记。

```dart
Container(
  height: 120.0,
  width: 120.0,
  color: Colors.blue.shade50,
  child: Align(
    alignment: Alignment.topRight,
    child: FlutterLogo(
      size: 60,
    ),
  ),
)
```



Center 继承自 Align，它比 Align 只少了一个 `alignment` 参数；由于 Align 的构造函数中`alignment` 值为 `Alignment.center`，所以我们可以认为  Center 组件其实是对齐方式确定居中的 Align。

```dart
DecoratedBox(
  decoration: BoxDecoration(color: Colors.red),
  child: Center( // 高宽度默认占满父元素
    child: Text("xxx"),
  ),
),
```



### 1.2.5 认识容器 Widget

#### 1.2.5.1 Padding

参考：https://book.flutterchina.club/chapter5/padding.html

一个组件想要添加空白间距可以使用 Padding 来包裹， Padding 中的 EdgeInsets 定义了一些设置空白填充的便捷方法：

```dart
Padding(
  //左边添加8像素补白
  padding: EdgeInsets.only(left: 8),
  child: Text("Hello world"),
),
```

```markdown
EdgeInsets提供的便捷方法：
fromLTRB(double left, double top, double right, double bottom)：分别指定四个方向的填充。
all(double value) : 所有方向均使用相同数值的填充。
only({left, top, right ,bottom })：可以设置具体某个方向的填充(可以同时指定多个方向)。
symmetric({ vertical, horizontal })：用于设置对称方向的填充，vertical指top和bottom，horizontal指left和right。
```



#### 1.2.5.2 DecoratedBox

参考：https://book.flutterchina.club/chapter5/decoratedbox.html

`DecoratedBox` 可以在其子组件绘制前后绘制一些装饰（Decoration），如背景、边框、渐变等：

```dart
const DecoratedBox({
  Decoration decoration,
  DecorationPosition position = DecorationPosition.background,
  Widget? child
})
```

decoration 通常使用 BoxDecoration 来进行封装：

```dart
BoxDecoration({
  Color color, //颜色
  DecorationImage image,//图片
  BoxBorder border, //边框
  BorderRadiusGeometry borderRadius, //圆角
  List<BoxShadow> boxShadow, //阴影,可以指定多个
  Gradient gradient, //渐变
  BlendMode backgroundBlendMode, //背景混合模式
  BoxShape shape = BoxShape.rectangle, //形状
})
```

下面实现一个自定义按钮样式：

```dart
DecoratedBox(
   decoration: BoxDecoration(
     gradient: LinearGradient(colors:[Colors.red,Colors.orange.shade700]), //背景渐变
     borderRadius: BorderRadius.circular(3.0), //3像素圆角
     boxShadow: [ //阴影
       BoxShadow(
         color:Colors.black54,
         offset: Offset(2.0,2.0),
         blurRadius: 4.0
       )
     ]
   ),
  child: Padding(
    padding: EdgeInsets.symmetric(horizontal: 80.0, vertical: 18.0),
    child: Text("Login", style: TextStyle(color: Colors.white),),
  )
)
```



#### 1.2.5.3 Transform

参考：https://book.flutterchina.club/chapter5/transform.html

Transform 可以在绘制阶段对一个组件进行平移、旋转或 3D等变换，但是在布局阶段这个组件的位置、大小已经确定了。实现效果是 Transform 包裹的组件相对于其初始位置进行变换（初始位置可以当做是把 Transform 去掉）

使用 Matrix4：

```dart
Container(
  color: Colors.black,
  child: Transform(
    alignment: Alignment.topRight, // 相对于坐标系原点的对齐方式
    transform: Matrix4.skewY(0.3), // 沿Y轴倾斜0.3弧度
    child: Container(
      padding: const EdgeInsets.all(8.0),
      color: Colors.deepOrange,
      child: const Text('Apartment for rent!'),
    ),
  ),
)
```



使用平移、缩放、旋转

```dart
DecoratedBox(
  decoration:BoxDecoration(color: Colors.red),
  //默认原点为左上角，左移20像素，向上平移5像素  
  child: Transform.translate(
    offset: Offset(-20.0, -5.0),
    child: Text("Hello world"),
  ),
);

DecoratedBox(
  decoration:BoxDecoration(color: Colors.red),
  child: Transform.scale(
    scale: 1.5, //放大到1.5倍
    child: Text("Hello world")
  )
);

DecoratedBox(
  decoration:BoxDecoration(color: Colors.red),
  child: Transform.rotate(
    //旋转90度
    angle:math.pi/2 ,
    child: Text("Hello world"),
  ),
);
```



#### 1.2.5.4 Container

最常用的组件，将前面的容器以及样式组件进行了整合：https://book.flutterchina.club/chapter5/container.html

```dart
Container({
  this.alignment, // 文字对齐方式
  this.padding, //容器内补白，属于decoration的装饰范围
  Color color, // 背景色，与decoration不能共用
  Decoration decoration, // 背景装饰
  Decoration foregroundDecoration, //前景装饰
  double width,//容器的宽度
  double height, //容器的高度
  BoxConstraints constraints, //容器大小的限制条件
  this.margin,//容器外补白，不属于decoration的装饰范围
  this.transform, //变换
  this.child,
  ...
})
```

> 容器的大小可以通过`width`、`height`属性来指定，也可以通过`constraints`来指定；如果它们同时存在时，`width`、`height`优先。实际上Container内部会根据`width`、`height`来生成一个`constraints`。



下面是一个使用的例子：

```dart
Container(
  margin: EdgeInsets.only(top: 50.0, left: 120.0),
  constraints: BoxConstraints.tightFor(width: 200.0, height: 150.0),//卡片大小
  decoration: BoxDecoration(  //背景装饰
    gradient: RadialGradient( //背景径向渐变
      colors: [Colors.red, Colors.orange],
      center: Alignment.topLeft,
      radius: .98,
    ),
    boxShadow: [
      //卡片阴影
      BoxShadow(
        color: Colors.black54,
        offset: Offset(2.0, 2.0),
        blurRadius: 4.0,
      )
    ],
  ),
  transform: Matrix4.rotationZ(.2),//卡片倾斜变换
  alignment: Alignment.center, //卡片内文字居中
  child: Text(
    //卡片文字
    "5.20", style: TextStyle(color: Colors.white, fontSize: 40.0),
  ),
 )
```



#### 1.2.5.5 Clip、FittedBox

Flutter 中提供了一些剪裁组件，用于对组件进行剪裁：https://book.flutterchina.club/chapter5/clip.html

| 剪裁Widget | 默认行为                                                     |
| ---------- | ------------------------------------------------------------ |
| ClipOval   | 子组件为正方形时剪裁成内贴圆形；为矩形时，剪裁成内贴椭圆     |
| ClipRRect  | 将子组件剪裁为圆角矩形，`borderRadius: BorderRadius.circular(5.0),` |
| ClipRect   | 默认剪裁掉子组件布局空间之外的绘制内容（溢出部分剪裁）       |
| ClipPath   | 按照自定义的路径剪裁                                         |



Flutter 提供了一个 FittedBox 组件，使子组件适配父组件空间，组件本身通过缩放或者裁剪子组件来使得子组件不会溢出到父组件

https://book.flutterchina.club/chapter5/fittedbox.html

```dart
const FittedBox({
  Key? key,
  this.fit = BoxFit.contain, // 适配方式
  this.alignment = Alignment.center, //对齐方式
  this.clipBehavior = Clip.none, //是否剪裁
  Widget? child,
})
```

> 关于 BoxFit 的各种适配规则和 Image 的 fix 属性指定是一样的，在介绍 Image 组件时有关于各种适配规则对应的效果
>
> **FittedBox 自身还是要遵守其父组件传递的约束**，因此这一层组件不会溢出父组件



### 1.2.6 认识滚动 Widget

#### 1.2.6.1 SingleChildScrollView

当内容元素超出屏幕范围时显示滚动效果：https://book.flutterchina.club/chapter6/single_child_scrollview.html

> 需要注意的是，**通常`SingleChildScrollView`只应在期望的内容不会超过屏幕太多时使用**，这是因为`SingleChildScrollView`不支持基于 Sliver 的延迟加载模型，所以如果预计视口可能包含超出屏幕尺寸太多的内容时，那么使用`SingleChildScrollView`将会非常昂贵（性能差），此时应该使用一些支持Sliver延迟加载的可滚动组件，如`ListView`。

```dart
SingleChildScrollView({
  this.scrollDirection = Axis.vertical, //滚动方向，默认是垂直方向
  this.reverse = false, 
  this.padding, 
  bool primary, 
  this.physics, 
  this.controller,
  this.child,
})
```

```dart
class SingleChildScrollViewTestRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    return Scrollbar( // 显示进度条
      child: SingleChildScrollView(
        padding: EdgeInsets.all(16.0),
        child: Center(
          child: Column( 
            //动态创建一个List<Widget>  
            children: str.split("") 
                //每一个字母都用一个Text显示,字体为原来的两倍
                .map((c) => Text(c, textScaleFactor: 2.0,)) 
                .toList(),
          ),
        ),
      ),
    );
  }
}
```



#### 1.2.6.2 ListView

可滚动组件简介：https://book.flutterchina.club/chapter6/intro.html

认识 ListView 之前先了解一下滚动组件的核心构成：**Scrollable**  负责处理滑动手势和偏移、**Viewport**定义可视区域、**Sliver**进行具体内容的按需构建与渲染。另外 **Scrollbar **是一个 Material 风格的滚动指示器（滚动条），如果要给可滚动组件添加滚动条，只需将它作为可滚动组件的任意一个父级组件即可：

```dart
Scrollbar(
  controller: _controller,
  child: ListView.builder(
      controller: _controller,
      itemCount: 100,
      itemExtent: 50.0,
      itemBuilder: (context, index) {
        return ListTile(title: Text("$index"),);
      }
  ),
)
```




ListView 学习文档：https://book.flutterchina.club/chapter6/listview.html

ListView 是 Flutter 中用于显示滚动列表的基础小部件之一，通常用于显示具有相同布局的多个项。它是一个非常常用的 UI 组件，可以在移动应用中用于展示数据列表。它常用的使用方式如下：

**ListView**：是 Flutter 中最基本的列表组件，支持垂直滚动。构造函数如下：

```dart
ListView({
  ...  
  //可滚动widget公共参数
  Axis scrollDirection = Axis.vertical,
  bool reverse = false,
  ScrollController? controller,
  bool? primary,
  ScrollPhysics? physics,
  EdgeInsetsGeometry? padding,
  
  //ListView各个构造函数的共同参数  
  double? itemExtent,
  Widget? prototypeItem, //列表项原型，后面解释
  bool shrinkWrap = false,
  bool addAutomaticKeepAlives = true,
  bool addRepaintBoundaries = true,
  double? cacheExtent, // 预渲染区域长度
    
  //子widget列表
  List<Widget> children = const <Widget>[],
})
```

```dart
ListView(
  shrinkWrap: true, // 该属性表示是否根据子组件的总长度来设置ListView的长度
  padding: const EdgeInsets.all(20.0),
  children: <Widget>[
    const Text('I\'m dedicating every day to you'),
    const Text('Domestic life was never quite my style'),
    const Text('When you smile, you knock me out, I fall apart'),
    const Text('And I thought I was so smart'),
  ],
);
```



**ListView.builder**：适用于动态生成大量列表项，并提供高性能。ListTile 组件可用于用于自定义每个列表项的外观。

```dart
ListView.builder(
  itemCount: 100,
  itemExtent: 50.0, //强制高度为50.0
  itemBuilder: (BuildContext context, int index) {
    return ListTile(title: Text("$index"));
  }
);
```



**ListView.separated**：用于在列表项之间添加分隔符，通过 separatorBuilder 属性构造分割线。

```dart
class ListView3 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //下划线widget预定义以供复用。  
    Widget divider1=Divider(color: Colors.blue,);
    Widget divider2=Divider(color: Colors.green);
    return ListView.separated(
      itemCount: 100,
      //列表项构造器
      itemBuilder: (BuildContext context, int index) {
        return ListTile(title: Text("$index"));
      },
      //分割器构造器
      separatorBuilder: (BuildContext context, int index) {
        return index%2==0?divider1:divider2;
      },
    );
  }
}
```



#### 1.2.6.3 ScrollController

可以通过 ScrollController 控制滚动位置。参考：https://book.flutterchina.club/chapter6/scroll_controller.html

`ScrollController` 构造函数如下， _scrollController 存在多个属性和方法来实现滚动控制：

- _scrollController.offset：获取绑定的滚动组件当前的滚动位置
- _scrollController.jumpTo(double offset)：直接跳转到指定位置
- _scrollController.animateTo(double offset,...)：动画跳转到指定位置
- _scrollController.addListener()：`ScrollController` 间接继承自 `Listenable`，因此我们可以监听滚动事件

```dart
const _scrollController = ScrollController({
  double initialScrollOffset = 0.0, //初始滚动位置
  this.keepScrollOffset = true,//是否保存滚动位置
  ...
});
```

```dart
@override
void initState() {
  super.initState();
  //监听滚动事件，打印滚动位置
  _controller.addListener(() {
    print(_controller.offset); //打印滚动位置
    if (_controller.offset < 1000 && showToTopBtn) {
      setState(() {
        showToTopBtn = false;
      });
    } else if (_controller.offset >= 1000 && showToTopBtn == false) {
      setState(() {
        showToTopBtn = true;
      });
    }
  });
}
```

```dart
Scrollbar(
  controller: _controller,
  child: ListView.builder(
      controller: _controller,
      itemCount: 100,
      itemExtent: 50.0, //列表项高度固定时，显式指定高度是一个好习惯(性能消耗小)
      itemBuilder: (context, index) {
        return ListTile(title: Text("$index"),);
      }
  ),
),
```

```dart
//返回到顶部时执行动画
_controller.animateTo(
  .0,
  duration: Duration(milliseconds: 200),
  curve: Curves.ease,
);
```



#### 1.2.6.4 GirdView

网格布局是一种常见的布局类型，GridView 组件正是实现了网格布局的组件。GridView 在实现滚动的基础上再对其子组件布局进行排列：https://book.flutterchina.club/chapter6/gridview.html

其构造函数如下，大部分属性和 ListView 一致，关键属性是 gridDelegate：

```dart
GridView({
  Key? key,
  Axis scrollDirection = Axis.vertical,
  bool reverse = false,
  ScrollController? controller,
  bool? primary,
  ScrollPhysics? physics,
  bool shrinkWrap = false,
  EdgeInsetsGeometry? padding,
  required this.gridDelegate,  //下面解释
  bool addAutomaticKeepAlives = true,
  bool addRepaintBoundaries = true,
  double? cacheExtent, 
  List<Widget> children = const <Widget>[],
  ...
})
```



**GridView.count：实现一个横轴为固定数量子元素的 layout 算法**

```dart
SliverGridDelegateWithFixedCrossAxisCount({
  @required double crossAxisCount, 
  double mainAxisSpacing = 0.0,
  double crossAxisSpacing = 0.0,
  double childAspectRatio = 1.0,
})
```

> - `crossAxisCount`：横轴子元素的数量。此属性值确定后子元素在横轴的长度就确定了，即ViewPort横轴长度除以它的商。
> - `mainAxisSpacing`：主轴方向的间距。
> - `crossAxisSpacing`：横轴方向子元素的间距。
> - `childAspectRatio`：子元素在横轴长度和主轴长度的比例。由于`crossAxisCount`指定后，子元素横轴长度就确定了，然后通过此参数值就可以确定子元素在主轴的长度。

```dart
// 固定横轴三个子组件，因此确定了宽度
// 设置宽高比是1，因此确定了高度
GridView(
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
      crossAxisCount: 3, //横轴三个子widget
      childAspectRatio: 1.0 //宽高比为1时，子widget
  ),
  children:<Widget>[
    Icon(Icons.ac_unit),
    Icon(Icons.airport_shuttle),
    Icon(Icons.all_inclusive),
    Icon(Icons.beach_access),
    Icon(Icons.cake),
    Icon(Icons.free_breakfast)
  ]
);

// 以下是GridView.count作为上面代码的语法糖
GridView.count( 
  crossAxisCount: 3,
  childAspectRatio: 1.0,
  children: <Widget>[
    Icon(Icons.ac_unit),
    Icon(Icons.airport_shuttle),
    Icon(Icons.all_inclusive),
    Icon(Icons.beach_access),
    Icon(Icons.cake),
    Icon(Icons.free_breakfast),
  ],
);
```



**GridView.extent：实现一个横轴子元素为固定最大长度的 layout 算法**

```dart
SliverGridDelegateWithMaxCrossAxisExtent({
  double maxCrossAxisExtent,
  double mainAxisSpacing = 0.0,
  double crossAxisSpacing = 0.0,
  double childAspectRatio = 1.0,
})
```

> `maxCrossAxisExtent`为子元素在横轴上的最大长度，之所以是“最大”长度，是**因为横轴方向每个子元素的长度设定是等分的**

```dart
// 宽度等分，最大宽度为120
GridView(
  padding: EdgeInsets.zero,
  gridDelegate: SliverGridDelegateWithMaxCrossAxisExtent(
      maxCrossAxisExtent: 120.0,
      childAspectRatio: 2.0 //宽高比为2
  ),
  children: <Widget>[
    Icon(Icons.ac_unit),
    Icon(Icons.airport_shuttle),
    Icon(Icons.all_inclusive),
    Icon(Icons.beach_access),
    Icon(Icons.cake),
    Icon(Icons.free_breakfast),
  ],
);

GridView.extent(
   maxCrossAxisExtent: 120.0,
   childAspectRatio: 2.0,
   children: <Widget>[
     Icon(Icons.ac_unit),
     Icon(Icons.airport_shuttle),
     Icon(Icons.all_inclusive),
     Icon(Icons.beach_access),
     Icon(Icons.cake),
     Icon(Icons.free_breakfast),
   ],
 );
```



**动态构建 GridView 使用 GridView.builder**，使用方式和 ListView 一致

```dart
GridView.builder(
 ...
 itemCount,
 required SliverGridDelegate gridDelegate, 
 required IndexedWidgetBuilder itemBuilder,
)
```



#### 1.2.6.5 PageView



# 第二章 ReactNative 开发

## 2.1 ReactNative 环境搭建

1. 和 Flutter 一样需要 Java SDK、Android SDK、Android Studio 等配置和环境变量，这里就不再赘述了
2. RN 环境就是前端开发环境，全局 node 版本得 18 及以上，另外的下一个 工具 brew install watchman
3. 通过命令 npx react-native@version init AwesomeProject 初始化一个 RN 项目，最好下载稳定版本
4. 进入 vscode 打开项目，终端启动模拟器：emulator -avd Pixel_6_API_34，启动项目：yarn start，直接启动安卓：yarn android
5. 项目启动好后进入 Android Studio 打开 android 文件夹，安卓项目会自动被 gradle 构建，还需要点击右上角 Sync Gradle 一下



## 2.2 核心组件与样式学习

这一章主要介绍 ReactNative 的基础知识与核心组件，还有常用样式的定义。组件开发和一些原生事件和 Web 的开发还是有所不同的，但是 React 的开发模式是一样的



### 2.2.1 样式开发指南

**样式定义**

官方建议使用 StyleSheet 构建组件样式进行统一管理，但是还是可以使用内联样式的。这些样式名基本上是遵循了 web 上的 CSS 的命名，只是按照 JS 的语法要求使用了驼峰命名法。最基础的 View 组件没有任何样式，其他组件可能自带样式

```tsx
import { StyleSheet } from 'react-native'
(<SafeAreaView style={[styles.sectionContainer, styles.sectionTitle, {backgroundColor: '#30303060'}]} />)
const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: '600',
  },
});
```



**布局样式**

定义一个组件的宽高规范：https://www.reactnative.cn/docs/height-and-width，通过宽高样式定义，通过 flex 布局占比定义，或者通过百分比占父类盒子比例定义

React Native 中固定使用 flexbox 规则来指定某个组件的子元素的布局，默认布局为 column。下面是常用的几个样式介绍：https://www.reactnative.cn/docs/flexbox

更多布局样式参考：https://www.reactnative.cn/docs/layout-props



**Transform 样式**

我们可以使用 Transform 样式类似与 web 中的移动属性进行 2D 或 3D 变换修改组件的外观和位置，https://www.reactnative.cn/docs/transforms

```tsx
container: {
  transform: [{scale: 1.5}, {rotate: '30deg'}],
},
```





### 2.2.2 基础核心组件使用

**View**

View 就是一个视图组件，用来承载多个子组件和支持样式以实现页面布局。和 Web 中 div 盒子组件不同的是无法直接写入文本，只能通过嵌套 Text 组件写入文本，并规范一些字体属性



**Text**

文本组件，可写入文本并规定文本样式



**Image**

图像组件，类似与 Web 的 Img 标签，支持网络图片、静态资源、临时的本地图片、以及本地磁盘上的图片等



**ImageBackground**

Image 和 View 组件的结合，类似于 Web 上给 div 添加背景图片，然后再嵌套其他组件



**TextInput**

输入框组件，可受控并提供了多种特性的配置



**TouchableOpacity**

移动端独一无二的组件，这是一个用于触发用户触摸行为的组件。该组件的触摸 API 继承于 TouchableWithoutFeedback 组件。该组件提供了触摸时视觉上的反馈，即包裹区域透明度会发生变化。常用属性有 `activeOpacity`、`onPress`

- https://www.reactnative.cn/docs/touchablewithoutfeedback
- https://www.reactnative.cn/docs/touchableopacity



**Button**

按钮组件，和前面的 Touchable 组件不同点在于这个组件已经固定为按钮样式（无内联 style）了，并提供了其他特殊配置。



**Pressable**

更加强大的提供触摸反馈的组件，它可以检测到任意子组件的不同阶段的按压交互情况。

1. 点按一次回调函数触发顺序：onPressIn、onPress、onPressOut
2. 长按一次回调函数触发顺序：onPressIn、onLongPress、onPressOut

```tsx
<Pressable
  onPressIn={() => console.log('press in')}
  onLongPress={() => console.log('long press')}
  onPressOut={() => console.log('press out')}
  onPress={() => console.log('press')}>
  {({pressed}) => <Text style={styles.container}>{pressed}</Text>}
</Pressable>
```



**ScrollView**

RN 中想要实现滚动不能使用 overflow: scroll，而是必须使用 ScrollView 组件包裹一下，并且必须指定一个确切的高度，可以自己定义或者继承父类的高度。组件还提供了实例方法 scrollTo、scrollToEnd 等



**FlatList & SectionList**

FlatList 强大的滚动列表渲染组件，通过提供 data、renderItem 等属性实现列表渲染。SectionList 分组列表组件。

1. onEndReached：滚动到底部时触发，一般用于上拉加载
2. onEndReachedThreshold：距离底部还是多少时就触发 onEndReached



**RefreshControl**

为滚动组件：ScrollView、FlatList、SectionList 提供下拉刷新，通过 onRefresh 属性触发下拉刷新

```tsx
<ScrollView
  contentContainerStyle={styles.scrollView}
  refreshControl={
    <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
  }
>
  <Text>Pull down to see RefreshControl indicator</Text>
</ScrollView>
```



**Modal**

Modal 组件是一种简单的覆盖在其他视图之上显示内容的方式，相当于建立了一个顶级图层并且占满了整个屏幕

1. visible：控制组件的显示与隐藏
2. onRequestClose：当安卓点击返回键的时候就会触发这个回调函数，ios 则不需要传入
3. statusBarTranslucent：使弹层组件不覆盖状态栏
4. onShow、onDismiss：展示和关闭的回调
5. transparent：将图层设置为透明以便可以看到底层图层，否则背景为白色

```tsx
<View style={viewStyle}>
  <Button title="打开弹窗" onPress={() => setVisible(!visible)} />
  <Modal
    transparent={true}
    visible={visible}
    animationType="slide"
    onRequestClose={() => setVisible(false)}>
    <View style={styles.modalContainer}>
      <View style={styles.modalContent} />
    </View>
  </Modal>
</View>

const styles = StyleSheet.create({
  viewContainer: {
    flex: 1,
  },
  tranBgc: {
    backgroundColor: '#30303060',
  },
  modalContainer: {
    flex: 1,
    backgroundColor: 'transparent',
    justifyContent: 'flex-end',
  },
  modalContent: {
    height: '40%',
    backgroundColor: '#fff',
    borderTopLeftRadius: 20,
    borderTopRightRadius: 20,
  },
});
```



**KeyboardAvoidingView**

本组件用于解决一个常见的尴尬问题：手机上弹出的键盘常常会挡住当前的视图。本组件可以自动根据键盘的高度，调整自身的 height 或底部的 padding，以避免被遮挡。实测 behavior 属性设置为 padding 是没问题的



### 2.2.3 核心 API 的使用

**useWindowDimensions & Dimensions**

获取设备屏幕的宽高，https://www.reactnative.cn/docs/dimensions



**Platform**

获取平台以及版本信息，https://www.reactnative.cn/docs/platform



**Linking**

用于跳转链接或者跳转应用，https://www.reactnative.cn/docs/linking



**PixelRatio**

这个属性可以获取到设备的像素密度和字体缩放比，https://www.reactnative.cn/docs/pixelratio

getPixelSizeForLayoutSize：将一个布局尺寸(dp)转换为像素尺寸(px)，例如指定一图片大小为 20，如果设备的 pixelratio 为 2，那么所需要的图片像素大小就为 40px

```tsx
const image = getImage({
  url,
  width: PixelRatio.getPixelSizeForLayoutSize(200),
  height: PixelRatio.getPixelSizeForLayoutSize(100),
});
<Image source={image} style={{width: 200, height: 100}} />
```



**BackHandler**

用于监听设备上的后退按钮事件，可以调用你自己的函数来处理后退行为，回调函数返回 false 则会执行回退行为

使用 @react-native-community/hooks 下的 useBackHandler 可以简化使用，https://www.reactnative.cn/docs/backhandler

```tsx
useEffect(() => {
  const backAction = () => {
    Alert.alert('Hold on!', 'Are you sure you want to go back?', [
      {
        text: 'Cancel',
        onPress: () => null,
        style: 'cancel',
      },
      {text: 'YES', onPress: () => BackHandler.exitApp()},
    ]);
    return true;
  };

  const backHandler = BackHandler.addEventListener(
    'hardwareBackPress',
    backAction,
  );

  return () => backHandler.remove();
}, []);
```

```tsx
useBackHandler(() => {
  if (shouldBeHandledHere) {
    // handle it
    return true
  }
  // let the default thing happen
  return false
})
```



**Vibration**

一个使设备振动的 API，https://www.reactnative.cn/docs/vibration



**PermissionsAndroid**

通过次 API 来申请动态权限， 每次使用的时候都得动态申请一次，https://www.reactnative.cn/docs/permissionsandroid

```tsx
const onPress = async () => {
  const permission = await PermissionsAndroid.check(
    PermissionsAndroid.PERMISSIONS.GET_ACCOUNTS,
  );
  console.log('permission', permission);
  if (!permission) {
    const res = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.GET_ACCOUNTS,
      {
        title: 'Cool Photo App Camera Permission',
        message:
          'Cool Photo App needs access to your camera ' +
          'so you can take awesome pictures.',
        buttonNeutral: 'Ask Me Later',
        buttonNegative: 'Cancel',
        buttonPositive: 'OK',
      },
    );
    console.log('res', res);
    if (res === PermissionsAndroid.RESULTS.GRANTED) {
      // 用户同意授权
      console.log('用户同意授权');
    } else if (res === PermissionsAndroid.RESULTS.DENIED) {
      // 用户拒绝授权
      console.log('用户拒绝授权');
    } else if (res === PermissionsAndroid.RESULTS.NEVER_ASK_AGAIN) {
      // 用户永久拒绝授权
      console.log('用户永久拒绝授权');
    }
  }
};
```



**Keyboard**

用来控制键盘相关的事件，监听键盘的打开和关闭事件，以及 Keyboard.dismiss 控制键盘的关闭

```tsx
useEffect(() => {
  const showSubscription = Keyboard.addListener('keyboardDidShow', () => {
    setKeyboardStatus('Keyboard Shown');
  });
  const hideSubscription = Keyboard.addListener('keyboardDidHide', () => {
    setKeyboardStatus('Keyboard Hidden');
  });

  return () => {
    showSubscription.remove();
    hideSubscription.remove();
  };
}, []);
```



**Alert**

启动一个提示对话框，支持传入标题、信息和按钮，https://www.reactnative.cn/docs/next/alert

```tsx
Alert.alert(
  "Alert Title",
  "My Alert Msg",
  [
    {
      text: "Ask me later",
      onPress: () => console.log("Ask me later pressed")
    },
    {
      text: "Cancel",
      onPress: () => console.log("Cancel Pressed"),
      style: "cancel"
    },
    { text: "OK", onPress: () => console.log("OK Pressed") }
  ]
);
```



## 2.3 Animated 动画库使用

Animated 使得开发者可以简洁地实现各种各样的动画和交互方式，并且具备极高的性能。Animated 旨在以声明的形式来定义动画的输入与输出，在其中建立一个可配置的变化函数，然后使用 start/stop 方法来控制动画按顺序执行。使用 useRef 将一个 Animated.value 保持组件周期内渲染时不更新，仅通过 Animated 库来控制，https://www.reactnative.cn/docs/animations

```tsx
const AnimatedDemo = () => {
  const marginLeftValue = useRef(new Animated.Value(0)).current;

  const onPress = () => {
    Animated.timing(marginLeftValue, {
      toValue: 200,
      duration: 1000,
      useNativeDriver: false,
    }).start();
  };

  return (
    <View>
      <Button title="start" onPress={() => onPress()} />
      <Animated.View
        style={{
          width: 100,
          height: 100,
          backgroundColor: 'red',
          marginLeft: marginLeftValue,
        }}
      />
    </View>
  );
};
```



组件必须经过特殊处理才能用于动画。所谓的特殊处理主要是指把动画值绑定到属性上，并且在一帧帧执行动画时避免 react 重新渲染和重新调和的开销。此外还得在组件卸载时做一些清理工作，使得这些组件在使用时是安全的。`Animated` 中默认导出了以下这些可以直接使用的动画组件：

- `Animated.Image`
- `Animated.ScrollView`
- `Animated.Text`
- `Animated.View`
- `Animated.FlatList`
- `Animated.SectionList`



### 2.3.1 动画的构建与启动

当我们想要创建一个动画时，Animated 提供了三种动画类型。每种动画类型都提供了特定的函数曲线，用于控制动画值从初始值变化到最终值的变化过程，比如初始值为 0，我想要初始值增加到 10 的过程中使用何种动画类型（变化效果）

- Animated.decay：以指定的初始速度开始变化，然后变化速度越来越慢直至停下
- Animated.spring：提供了一个基础的弹簧物理模型，配置稍微有点复杂
- Animated.timing：使用 easing 函数让数值随时间动起来

大多数情况下我们应该使用 timing。默认情况下，它会将对象逐渐加速到全速，然后通过逐渐减速停止结束。



**Animated.decay**

该动画类型是推动一个值以一个初始的速度和一个衰减系数逐渐变为 0，因此这段过程增加的距离或者终点不可以直接指定。

具体配置参考：https://www.reactnative.cn/docs/animated#decay

```tsx
Animated.decay(marginLeftValue, {
  velocity: 1,
  deceleration: 0.995,
  useNativeDriver: false,
}).start();
```



**Animated.spring**

实现一个弹簧动画，具体配置参考：https://www.reactnative.cn/docs/animated#spring

```tsx
Animated.spring(marginLeftValue, {
  toValue: 200,
  useNativeDriver: false,
  speed: 10,
  bounciness: 10,
}).start();
```



**Animated.timing**

主要配置为：toValue、duration、easing、delay，其中 Easing 模块定义了一大堆曲线，https://www.reactnative.cn/docs/easing

用于实现一些常见的动画缓动函数，具体配置参考：https://www.reactnative.cn/docs/animated#timing

```tsx
Animated.timing(marginLeftValue, {
  toValue: 200,
  duration: 1000,
  easing: Easing.linear,
  useNativeDriver: false,
}).start();
```



**animated.start**

通过在动画上调用 start 来启动动画。 它接受一个完成回调函数，当动画完成或因在它完成之前调用 stop 而结束时将被调用。如果动画是因为调用了 stop 而结束（例如，因为它被手势或其他动画中断），则它会收到 `{finished：false}`

```tsx
animated.start(({finished}) => {})
```



**animated.stop**

停止所有正在运行的动画



**animated.reset**

停止所有正在运行的动画并将其值重置为初始值




### 2.3.2 Animated.Value

驱动动画的一维标量值，搭配 React 中的 useRef 进行初始化创建：`useRef(new Animated.Value(0)).current`

该对象被取值时会调用 `getValue` 返回 `number` 类型的变量，其他常用方法参考：https://www.reactnative.cn/docs/animatedvalue



**Animated.ValueXY**

实现 x、y 两路复用的 Animated.Value，使用方法几乎一致：`useRef(new Animated.Value({x: 0, y: 0})).current`

具体参考：https://www.reactnative.cn/docs/animatedvaluexy



**setValue**

直接赋值。注意这会导致正在运行的动画中断而直接更新到新值。



**addListener**

给动画值添加一个异步监听器，以便您可以观察动画值的更新。返回一个作为监听器标识符的字符串。

```tsx
useEffect(() => {
  const id = marginLeftValue.addListener(({value}) => {
    console.log('value', value);
  });
  return () => {
    marginLeftValue.removeListener(id);
  };
}, [marginLeftValue, interpolateValue]);
```



**interpolate**

将原始值映射为需要展示的类型

```tsx
const rotateValue = useRef(new Animated.Value(0)).current;
const rotate = rotateValue.interpolate({
  inputRange: [0, 360],
  outputRange: ['0deg', '360deg'],
});
```



**合成动画值**

由于我们每一个动画值都是 Animated.Value 对象，因此不能直接进行加减乘除的运算。那么则可以使用加减乘除以及取余等运算来把两个动画值合成为一个新的动画值：

- [`Animated.add()`](https://www.reactnative.cn/docs/animated#add)
- [`Animated.subtract()`](https://www.reactnative.cn/docs/animated#subtract)
- [`Animated.divide()`](https://www.reactnative.cn/docs/animated#divide)
- [`Animated.modulo()`](https://www.reactnative.cn/docs/animated#modulo)
- [`Animated.multiply()`](https://www.reactnative.cn/docs/animated#multiply)



### 2.3.3 组合动画的使用

当我们创建了多个动画之后，动画还可以使用组合函数以复杂的方式进行组合：https://www.reactnative.cn/docs/animated#%E7%BB%84%E5%90%88%E5%8A%A8%E7%94%BB



**Animated.parallel**

将多个动画同时进行，https://www.reactnative.cn/docs/animated#parallel

```ts
Animated.parallel([moveX, moveY, scaleAnim]).start();
```



**Animated.sequence**

将多个动画依次进行，https://www.reactnative.cn/docs/animated#sequence

```tsx
Animated.sequence([moveX, moveY, scaleAnim]).start();
```



**Animated.stagger**

每个动画间指定一定的延迟依次执行，https://www.reactnative.cn/docs/animated#stagger

```tsx
Animated.stagger(1500, [moveX, moveY, scaleAnim]).start();
```



 **Animated.delay**

设置一个自定义的动画延迟，搭配 Animated.sequence 使用

```tsx
Animated.sequence([
    moveX,
    Animated.delay(1000),
    moveY,
    Animated.delay(500),
    scaleAnim,
]).start();
```



### 2.3.4 LayoutAnimation

当布局变化时，自动将视图运动到它们新的位置上，一个常用的调用此 API 的办法是在状态更新前调用。

参考文档：https://www.reactnative.cn/docs/layoutanimation

注意如果要在 **Android **上使用此动画，则需要在代码中启用：

```tsx
import { UIManager } from 'react-native';

if (Platform.OS === 'android') {
  if (UIManager.setLayoutAnimationEnabledExperimental) {
    UIManager.setLayoutAnimationEnabledExperimental(true);
  }
}
```



控制一个组件的显示与隐藏，直接在状态改变时启用即可

```tsx
const LayoutAnimationDemo = () => {
  const [show, setShow] = useState(false);
  return (
    <View>
      <Button
        title="show"
        onPress={() => {
          // LayoutAnimation.linear();
          LayoutAnimation.configureNext(LayoutAnimation.Presets.easeInEaseOut);
          setShow(true);
        }}
      />
      {show && <View style={{width: 100, height: 100, backgroundColor: 'red'}} />}
    </View>
  );
};
```



## 2.4 原生模块构建与使用

这一节主要介绍如何在安卓项目创建一个原生模块，作为安卓项目与RN 项目的一个桥梁。想象一下，您想在 React Native 应用程序内的 JavaScript 中访问 iOS/Android 原生日历 API，以创建日历事件。React Native 没有公开与原生日历库通信的 JavaScript API。然而，通过原生模块，您可以编写与原生日历 API 通信的原生代码。然后您可以在 React Native 应用程序中的 JavaScript 里调用该原生代码。

具体怎么创建和桥接原生模块直接看官方文档即可，参考文档：https://www.reactnative.cn/docs/native-modules-android



### 2.4.1 使用原生模块方法

在安卓原生项目中创建完成桥接原生模块之后，我们先实现在 RN 项目中调用原生模块方法

安卓项目，除了普通类型，其他复杂类型都得用 RN 提供的已序列化化好的类：WritableNativeMap、WritableNativeArray

`AppModule.java`

```java
@Override
public Map<String, Object> getConstants() {
    final Map<String, Object> constants = new HashMap<>();
    constants.put("DEFAULT_EVENT_NAME", "New Event");
    return constants;
}

@ReactMethod
public void createCallbackEvent(String name, Callback callback) {
    // 传递普通类型、对象类型、数组类型
    int id = 2020210832;
    boolean isTrue = false;

    WritableMap map = new WritableNativeMap();
    map.putString("name", "cocoon");
    map.putBoolean("isTrue", isTrue);
    map.putInt("id", id);

    WritableArray array = new WritableNativeArray();
    array.pushBoolean(isTrue);
    array.pushInt(id);

    callback.invoke(id, map, array);
}

@ReactMethod
public void createLogEvent(String name, String location) {
    Log.d("CalendarModule", "Create event called with name: " + name
            + " and location: " + location);
}

@ReactMethod
public void createPromiseEvent(String name, Promise promise) {
    try {
        String str = name + ": cocoon";
        WritableArray array = new WritableNativeArray();
		    array.pushBoolean(isTrue);
  		  array.pushInt(id);
        promise.resolve(array);
    } catch(Exception e) {
        promise.reject("Create Event Error", e);
    }
}
```



RN 项目

```java
onPress={async () => {
  // 获取原生模块的常量
  const constants = AppModule?.getConstants();
  console.log('constants', constants);

  // 调用原生模块的方法，打印安卓日志
  AppModule?.createLogEvent('testName', 'testLocation');

  // 在原生模块方法中调用回调函数
  AppModule?.createCallbackEvent(
    'name',
    (id: number, map: Record<string, any>, array: any[]) => {
      console.log('id', id);
      console.log('map', map);
      console.log('array', array);
    },
  );

  // 通过promise获取原生模块方法的返回值
  try {
    const res = await AppModule?.createPromiseEvent('name');
    console.log('res', res);
  } catch (error) {
    console.error(error);
  }
}}
```

