---
title: "Objective-c Coding Standard"
date: 2017-08-01T08:43:28+08:00
---

此次规范从当前的开发现状（风格各异）出发，奠基于当前的编码习惯，旨在规范大家的编程行为。
待到下次开会的时候，仍需依据自己的习惯，提出针对性的意见。后期将参考此次会上的意见进行修订。

> 最近大佬要规范下团队里的编码规范，作为狗腿子的咱自然是要响应下号召咯...顺带的自己也想把规范定下来，后面一步步的修订，方便代码更新迭代。
> 还是想着能让自己代码更加的简洁、明了、具有表达力的😁
> 希望下次谁谁看代码的时候，不用特意去对照界面就能了解这是个做什么的。

-------
<!--[TOC]-->
# 一、命名规范

我们所写的代码主要是为了阅读，其次才是被机器执行。所以我们要写：

- 让别人能读懂的代码
- 可扩展的代码
- 可测试的代码(代码应该具备可测试性，对没有可测试性的代码写测试，是浪费生命的表现)

## （一）、相关参考

### 1、RC原则

> 可读性高(Readable)
> 防止命名冲突(Conflict Name prevention)

说到命名，就先来介绍下常用的命名方法：

##### 常用命名方法


###### （1）匈牙利命名：

开头字母用变量类型的缩写，其余部分用变量的英文或英文的缩写，要求单词第一个字母大写。

```Objective-c
int iMyAge; “i”是int类型的缩写； 
char cMyName[10]; “c”是char类型的缩写； 
float fManHeight; “f”是float类型的缩写；
```

<span id=named_02></span>
###### （2）驼峰式命名法

又叫小驼峰式命名法。 
第一个单词首字母小写，后面其他单词首字母大写。

```Objective-c
int myAge; 
char myName[10]; 
float manHeight;
```

<span id=named_03></span>
###### （3）帕斯卡命名法

又叫大驼峰式命名法。 
每个单词的第一个字母都大写。

```Objective-c
int MyAge; 
char MyName[10]; 
float ManHeight;
```
<span id=named_04></span>
###### （4）下划线命名法
在命名中添加下划线用以标识
一般Object-C中建议我们在命名前加`_`，用以区分成员变量与其它变量的
在命名后加`_`，通常用在宏命名中
其它情况下在，`_`添加在标识不同含义的单词块之间用以区分

```Objective-c
int _myage; 
char my_name[10]; 
__FILE__
```


### 2、TEDC原则
> 简洁(Terse)
> 具有表达力(Expressive)
> 只做一件事(Do one thing)

Objective-C 的命名通常都比较长, 名称遵循驼峰式命名法. 一个好的命名标准很简单, 就是做到在开发者一看到名字时, 就能够懂得它的含义和使用方法. 

有些时候这三者也会有起冲突的时候，怎么取舍呢？

借用官方的例子

<span id=TEDC_01></span>
#### 表达力 > 简洁
> 尽可能具有表达力和简洁是好的，但是表达力不应该因为简洁而受到影响。

代码|点评
---|---
insertObject:atIndex: | Good
insert:at: | 不清晰;要插⼊什么?“at”表⽰示什么?
removeObjectAtIndex: | Good
removeObject: | 不错,因为⽅法是⽤用来移除作为参数的对象
remove:|不清晰;要移除什么?

#### 清晰表达意思
> 一般来说，不要缩写事物的名称。把它们拼出来，即使它们很长:

代码|点评
---|---
destinationSelection| Good
destSel | 不清晰
setBackgroundColor: | Good
setBkgdColor: | 不清晰


#### 避免歧义
> 避免API名称中的歧义，例如可以用多种方法解释的方法名

代码|点评
---|---
sendPort| 它是发送端口还是返回?
displayName | 它是在用户界面中显示一个名称还是返回接收者的标题?

需要察看更多的规范，请前往[官方文档](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-BBCHBFAH)

## （二）、 实际规范

#### 1、变量命名

##### （1）一般变量命名

<span style="color:#F00">命名方式</span>：[小写类型前缀+`_`+介绍[小驼峰式](named_02)]的做法。【介绍尽量用自然语言表达自己的意思。】

于个人而言，变量名使用更多的是下划线加驼峰式的命名，尽量用自然语言命名自己的变量

```Objective-c
@property (nonnull,nonatomic,strong) UIImageView *imageView_head;
```

##### （2）模型内的属性命名

<span style="color:#F00">命名方式</span>：[下划线命名](#named_04)

坚持<span style="color:#F00">一致性</span>的原则

当下后台属性命名方式：[下划线命名](#named_04)
        
对于用于解析后台数据的模型，应尽量保持与后台命名方式一致，最好能命名完全一致
对于用于处理本地数据的模型，也应保持与后台命名方式一致。

<span style="color:#F00">**即应保证具有某一共同功能的类型命名方式一致。**</span>

#### 2、类命名

<span style="color:#F00">命名方式</span>：[大驼峰式命名法](#named_03)

对于一般的类，通常是使用大驼峰式的命名方式
类名的拼写方式一般采用<span style="color:#F00">[标识 + 模块名称+功能介绍+类型]</span>
**标识**用于区分其它第三方的类，一般为开发者或者开发公司的标识
**模块名称**标识当前类在界面中所处模块名称
**功能介绍**标识当前类在当前模块中的作用
**类型**标识当前类的类型

其中最有争议的应该是**模块名称**

位置|模块名称
---|---
根控制器|`Base`
一般控制器|其根控制器的**功能介绍**
一般视图|下一级响应者（父视图或是其所属的控制器）的**功能介绍**
通用控制器（例如：登陆、注册或者是好几个`TabBar`分栏都会跳转的控制器）|`public`
通用视图（用于多个界面的视图）| `public`

对控制器而言，模块名称即其根视图的**功能介绍**，若当前控制器即根控制器，则当前控制器的模块标识为`Base`

对于类名，小子是按其在界面中的层次进行命名
对于处于界面第一级的视图 将它的 上一级功能名称的 拼接字段定为`Base`
如`JYBaseHomeViewController` 表示首页的根控制器
其中

标识 |上一级功能 | 功能介绍 | 类型
--- | ---|---|---
`JY` |`Base`|`Home` |`ViewController`

#### 3、方法命名

<span style="color:#F00">命名方式</span>：[小驼峰式命名法](#named_02)

方法名应遵守小驼峰原则，首字母小写，其他单词首字母大写,每个空格分割的名称以动词开头。执行性的方法应该以动词开头，小写字母开头，返回性的方法应该以返回的内容开头，但之前不要加get。

方法名应具备以下特征
##### （1）表达力、简洁

方法名应该是简洁并具有表达力，去除参数之后能形成可读的自然语言
当这二者需要取舍，应该[着重强调表达力](#TEDC_01)

例如：

使用`insertObject:(NSObject*)object  atIndex: (NSInteger)index `

比`insert:(NSObject*)object at: (NSInteger)index`更合适

给它们去掉参数，变成自然语言即 “<span style="color:#F00">insert Object at Index</span>”对“<span style="color:#F00">insert at</span>”，孰优孰劣一目了然

##### （2）只做一件事

当你无法为你的方法起一个准确的名称时，很可能你的方法不止做了一件事，违反了(Do one thing)。特别是你想在方法名中加入：And，Or，If等词时

```Objective-c
- (void)RegisterUser:(User*) user SendEmail:(bool)sendEmail
{
    
}
```

此时，应该将执行不同逻辑操作的方法分开，构成两个不同的方法来执行

```Objective-c
- (void)RegisterUser:(User*)user
{

}

- (void)SendEmail:(User*)user
{

}
```

##### （3） 尽可能少的参数

过多的参数让读者难以抓住代码的意图，同时过多的参数将会影响方法的稳定性。另外也预示着参数应该聚合为一个`Model`

参数为<span style="color:#F00">1-2</span>个最合适  

```Objective-c
- (void) RegisterUserName:(NSString*)userName Password:(NSString*) password Email:(NSString*) email  Phone:(NSString*)phone
{

}
```
此时参数超过3个，可以聚合成为一个模型，以增强可读性

```Objective-c
- (void) RegisterUser:(User*)user
{

}
```

#### 4、类别命名

<span style="color:#F00">命名方式</span>：[类名+标识+扩展（[大驼峰式](named_03)）]

例：如果我们想要创建一个基于`NSString`的类别用于判断字符串类型，我们应该把类别放到名字是`NSString+JYJudgmentType`的文件里。`NSString`为要扩展的类名，`JY`为标识，`JudgmentType`为扩展的功能。

#### 5、枚举的命名

<span style="color:#F00">命名方式</span>：[标识+功能（[大驼峰式](named_03)）]

类型命名：[枚举名+特征]

下面我们列举一组用于判断字符串类型的枚举

```Objective-c
typedef NS_ENUM(NSInteger,JYJudgmentType){
    ///数字
    JYJudgmentTypeNumberCharacters             = 1,
    ///英文
    JYJudgmentTypeOrdinaryEnglishCharacters    = 1 << 1,
    ///中文
    JYJudgmentTypeChineseCharacters            = 1 << 2,
    ///电话
    JYJudgmentTypeMobile               = 1 << 3,
    ///身份证
    JYJudgmentTypeIDCard               = 1 << 4,
    ///银行卡
    JYJudgmentTypeBankCard             = 1 << 5,
    ///邮箱
    JYJudgmentTypeEmail             = 1 << 6,
};
```

我们就以`JYJudgmentTypeNumberCharacters`为例

`JY`为标识，`JudgmentType`为该枚举的功能，`NumberCharacters`为当前类型的特征

#### 6、const常量

<span style="color:#F00">命名方式</span>：[大驼峰式](named_03)

如果一定想要和其它变量区分开来，也可以给他一个标识

最明显的例子就是我们常用的`ReuseIdentifier`

#### 7、宏命名

<span style="color:#F00">命名方式</span>：[下划线命名](named_04)+全部字母大写
毕竟官方推荐命名方式
例如系统的宏`__FILE__`
我们也可以加上自己的标识用以和系统的宏区分开来`JY__FILE__`
如果还要标识宏隶属于某一模块的话，还可以更进一步的加上模块的标识`JY__SQL__FILE__`

# 二、注释规范

> 关于注释，虽说是有很大一份人认为优秀的代码可以完全替代注释，然而在实际上，英语这么强的还是很少的🤦‍♂️。而且对我们来说，用尽可能低的标准来要求别人，项目可维护性。（唔，连中文注释都看不懂那就无解了😒）
> 注释不用做得太夸张，由于开发中阅读注释大部分都只是为了关联或者了解某项功能，所以我们只需在关键点添加注释即可。

### 1、类前的注释
类的 `.h`文件中添加一段标识注释，用以解释当前类的用法

```
/*
 创建人：（标识创建）
 创建版本：创建类的版本（了解功能在哪一个版本添加或重构）
 功能描述：介绍类的主要功能（让读者一目了然）
 --修改人：（标识功能修改者）
 修改版本：类修改的版本（哪个版本有进行修订）
 修改描述：（修订某一功能）
 ···：重复【修改人 — 修改版本 — 修改描述】三列的介绍。"创建人"在之后的修改过程中也将作为"修改人"
 */
```

### 2、接口注释
推荐使用 `option`+`command`+`/`快捷注释命令
对类的接口处的属性、方法进行介绍

属性：

```objective-C
/**
 介绍属性
 */
@property (nonnull,nonatomic,strong) NSObject *object;
```

方法：

```objective-C
/**
 介绍方法功能

 @param obj 参数介绍
 */
- (void)RegisterUser:(User*)user;
```

# 三、逻辑规范

### （一）视图类的公有方法

对于封装的视图类，常会用到的方法有三类：

- 添加子视图
- 设置子视图在父视图中的位置
- 人机交互事件的设置

基于此，希望至少在这一种类型封装上能形成规范，当然，能约定俗成是最好的了😄

我就先抛砖引玉了：

<span style="color:#F00">首先</span> 重写系统初始化方法，下面是把将普通的init方法和可视化的初始化方法重写，然后调用我们自己的初始化方法`- (void)commInit`

```objective-C
//以frame初始化的方法
- (instancetype)initWithFrame:(CGRect)frame
{
    if (self = [super initWithFrame:frame]) {
        [self commInit];
    }
    return self;
}

//以可视化控件初始化的方法
- (instancetype)initWithCoder:(NSCoder *)aDecoder
{
    if (self = [super initWithCoder:aDecoder]) {
        [self commInit];
    }
    return self;
}

//自己的初始化方法
- (void)commInit
{

}

```

之后在我们的初始化方法中调用需要的操作，这里我们使用了，子视图添加、约束设置和交互设置三个方法

```objective-C
//初始化方法
- (void)commInit
{
    [self theSubViewAdd];
    [self theLayoutSet];
    [self theInterfaceEventSet];
}

//添加子视图
- (void)theSubViewAdd
{

}

//设置约束
- (void)theLayoutSet
{
    
}

//设置交互
- (void)theInterfaceEventSet
{
    
}
```

### （二）代码的重构规范

> 重构是一种对软件进行修改的行为，但它并不改变软件的功能特征，而是通过让软件程序更清晰，更简洁和更条理来改进软件的质量。

代码架构最初的设计也是经过精心的设计，具有良好架构的。但是随着时间的推移、需求的剧增，必须不断的修改原有的功能、追加新的功能，还免不了有一些缺陷需要修改。为了实现变更，不可避免的要违反最初的设计构架。经过一段时间以后，软件的架构就千疮百孔了。bug越来越多，越来越难维护，新的需求越来越难实现，最初的代码构架对新的需求渐渐的失去支持能力，而是成为一种制约。最后新需求的开发成本会超过开发一个新的软件的成本，这就使这个app的生命走到了尽头。

#### 1、目的

（1）持续偏纠和改进软件设计 

（2）使代码更被其他人所理解 

（3）帮助发现隐藏的代码缺陷

（4）从长远来看，有助于提高编程效率，增加项目进度（进度是质量的敌人，质量是进度的朋友） 

#### 2、不适用

（1）逻辑看起来过于复杂，没时间去分析梳理。

（2）不理解为什么前任程序员要这样编写。 

（3）负责的是一个很重要的系统，而且时间很紧。 

#### 3、方式
##### （1）权限分离

对一些“臃肿的类”，应当将其中分属其它类的处理逻辑，应当及时抽离出去。

就以经典`MVC`模式下的赋值为例

有些时候我们会将`Model`层的数据处理逻辑拿到`View`或`Controller`中来用，仅把`Model`层作为一个快速解析、调用数据的工具。

```objective-C
    NSString *money = [NSString stringWithFormat:@"总价%@万",_money];
    self.label_money.text = money;
```

而从其各自的业务上来说，数据处理的功能也应放在`Model`层上才是

```objective-C
- (NSString *)money
{
    return [NSString stringWithFormat:@"总价%@万",self->_money];
}
```

##### （2）提取类/方法

适用于以下类：

❶ 与其它类能共用相同的逻辑

❷ 与其它类在架构上一定的相似性

对于这些类可以提取出<span style="color:#F00">专门处理公有逻辑的新类</span>或<span style="color:#F00">架构相似的父类</span>为其减负。

##### （3 ）利用好第三方代码托管平台

对于某一类在项目间通用性更强的功能模块，更好的使用方式应该是放在第三方托管平台进行托管。做好`Pod`集成和`Carthage`集成的配置

以便 当前功能模块的维护更新以及在下一个项目的快速导入。

# 四、工具（类）的使用规范

### （一）手写代码 和 Xib的取舍

关于这个问题相信很多同学都有困惑，参考了国内iOS界的大神[唐巧](http://blog.devtang.com/2015/03/22/ios-dev-controversy-2/)和[喵神](https://onevcat.com/2013/12/code-vs-xib-vs-storyboard/)，结合自己在实际开发中的习惯，也就确立之后对于二者的使用了：

- 对于复杂的、动态生成的界面，建议使用手工编写界面。
- 对于需要统一风格的按钮或UI控件，建议使用手工用代码来构造。方便之后的修改和复用。
- 对于需要有继承或组合关系的 UIView 类或 UIViewController 类，建议用代码手工编写界面。
- 对于那些简单的、静态的、非核心功能界面，可以考虑使用 xib 或 storyboard 来完成。

### （二）工具类的使用规范

#### 1、UI调试工具

对于UI的调试，据我所知的有两种：

[Reveal](https://revealapp.com)和[UIDebuggingInformationOverlay](http://ryanipete.com/blog/ios/swift/objective-c/uidebugginginformationoverlay/)

二者的用法同等便利，但[Reveal](https://revealapp.com)比起[UIDebuggingInformationOverlay](http://ryanipete.com/blog/ios/swift/objective-c/uidebugginginformationoverlay/)来功能无疑是丰富许多。

[UIDebuggingInformationOverlay](http://ryanipete.com/blog/ios/swift/objective-c/uidebugginginformationoverlay/)现有的功能：

1. 列出界面层次、视图位置、从属关系
2. 对比设计图与APP运行时界面
3. 获取界面上的目标约束

[Reveal](https://revealapp.com)仅咱现在用到的功能在[UIDebuggingInformationOverlay](http://ryanipete.com/blog/ios/swift/objective-c/uidebugginginformationoverlay/)功能的基础上多了：
1. 使用可视化的图来展示界面的层次
2. GUI 上动态改变约束可以直接应用到APP上，实时展示改变效果（个人感觉这一点对后期UI的优化还是有点帮助的）
3. 对于越狱的机器，可以用Reveal来”调试“其它应用界面

所以说哟，能使用[Reveal](https://revealapp.com)还是用它为好，[UIDebuggingInformationOverlay](http://ryanipete.com/blog/ios/swift/objective-c/uidebugginginformationoverlay/)更多是在懒得使用或者实在用不了[Reveal](https://revealapp.com)的时候再用好了😦

#### 2、图片添加工具

说起来APPIcon，用得上的图片算起来也有8张了，没什么反人类的要求的话，图片内容基本一致，也仅是尺寸不一样，如果设计那边没什么便利的工具的话，那倒是可以使用下  [Asset Catalog Creator](https://itunes.apple.com/cn/app/asset-catalog-creator-free/id866571115?mt=12)，

一键设置Icon，直接添加到系统资源库,简单粗暴。

#### 3、项目优化工具

会用Xcode那对Intrument一定不会陌生了，也不多说，要优化就尽量多用吧。

#### 4、第三方代码托管

终归还是[Github](https://github.com/)最通用


<span style="font-size:3rem">END</span>

# References
 [三种编程命名规范（匈牙利命名法、驼峰式命名法、帕斯卡命名法）](http://blog.csdn.net/f_zyj/article/details/51510085)
 
[编写让别人能够读懂的代码](http://www.cnblogs.com/richieyang/p/4840614.html)

[IOS开发（OC）中的命名规范](http://www.cnblogs.com/iOS-mt/p/5445284.html)

[Objective-C开发编码规范](http://www.cocoachina.com/ios/20150508/11780.html)

[iOS开发总结之代码规范](http://www.jianshu.com/p/414bb5a53139)

[iOS开发代码规范(通用)](http://www.cnblogs.com/gfxxbk/p/5469017.html)

[iOS中书写代码规范35条小建议](http://www.jianshu.com/p/71fdd1ae714c)


[iOS 开发中的争议（二）](http://blog.devtang.com/2015/03/22/ios-dev-controversy-2/)

[代码手写UI，xib和StoryBoard间的博弈，以及Interface Builder的一些小技巧](https://onevcat.com/2013/12/code-vs-xib-vs-storyboard/)


[iOS项目重构周记（一）](http://www.jianshu.com/p/395700466a7b)

[代码重构意义和方法](http://blog.csdn.net/justinjing0612/article/details/41311577)


