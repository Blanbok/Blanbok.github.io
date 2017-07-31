Objective-c Coding Standard

此次规范从当前的开发现状（风格各异）出发，奠基于当前的编码习惯，旨在规范大家的编程行为。
待到下次开会的时候，仍需依据自己的习惯，提出针对性的意见。后期将参考此次会上的意见进行修订。

> 最近大佬要规范下团队里的编码规范，作为狗腿子的咱自然是要响应下号召咯...顺带的自己也想把规范定下来，后面一步步的修订，方便代码更新迭代。
> 还是想着能让自己代码更加的简洁、明了、具有表达力的😁
> 希望下次谁谁看代码的时候，不用特意去对照界面就能了解这是个做什么的。

[TOC]

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
###### （2）驼峰式命名法

又叫小驼峰式命名法。 
第一个单词首字母小写，后面其他单词首字母大写。

```Objective-c
int myAge; 
char myName[10]; 
float manHeight;
```
###### （3）帕斯卡命名法

又叫大驼峰式命名法。 
每个单词的第一个字母都大写。

```Objective-c
int MyAge; 
char MyName[10]; 
float ManHeight;
```
<span id=underline></span>
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

#### （1）表达力 > 简洁

> 尽可能具有表达力和简洁是好的，但是表达力不应该因为简洁而受到影响。

代码|点评
---|---
insertObject:atIndex: | Good
insert:at: | 不清晰;要插⼊什么?“at”表⽰示什么?
removeObjectAtIndex: | Good
removeObject: | 不错,因为⽅法是⽤用来移除作为参数的对象
remove:|不清晰;要移除什么?

> 一般来说，不要缩写事物的名称。把它们拼出来，即使它们很长:

代码|点评
---|---
destinationSelection| Good
destSel | 不清晰
setBackgroundColor: | Good
setBkgdColor: | 不清晰

> 避免API名称中的歧义，例如可以用多种方法解释的方法名

代码|点评
---|---
sendPort| 它是发送端口还是返回?
displayName | 它是在用户界面中显示一个名称还是返回接收者的标题?

需要察看更多的规范，请前往[官方文档](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-BBCHBFAH)

## （二）、 实际规范

#### 1、变量命名

#####（1）一般变量命名

于小子个人而言，对于变量名使用更多的是下划线加驼峰式的命名，尽量用自然语言命名自己的变量
<span style="color:#F00">[小写类型前缀+`_`+介绍]的做法。<span>【介绍使用驼峰式,尽量用自然语言表达自己的意思。】

```Objective-c
@property (nonnull,nonatomic,strong) UIImageView *imageView_head;
```

##### （2）模型内的属性命名

当下后台属性命名方式：[<span style="color:lightGray">下划线命名</span>](#underline)
        
对于用于解析后台数据的模型，应尽量保持与后台命名方式一致，最好能命名完全一致
对于用于处理本地数据的模型，也应保持与后台命名方式一致。

<span style="color:#F00">**即应保证具有某一共同功能的类型命名方式一致。**</span>

#### 2、类命名

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

#### 4、宏命名

# 二、注释规范

### 类前注释
```
/*
 创建人：（标识创建）
 创建版本：创建类的版本（了解功能在哪一个版本添加或重构）
 功能描述：介绍类的主要功能（让读者一目了然）
 --修改人：（标识功能修改者）
 修改版本：类修改的版本（哪个版本有进行修订）
 修改描述：（修订某一功能）
 ···：重复【修改人 — 修改版本 — 修改描述】三列的介绍。"创建人"在之后的修改过程中也作为"修改人"
 */
```

# 三、逻辑规范

# 四、工具或SDK的使用规范

<span style="font-size:3rem">END</span>
# References
 [三种编程命名规范（匈牙利命名法、驼峰式命名法、帕斯卡命名法）](http://blog.csdn.net/f_zyj/article/details/51510085)
 
[编写让别人能够读懂的代码](http://www.cnblogs.com/richieyang/p/4840614.html)

[IOS开发（OC）中的命名规范](http://www.cnblogs.com/iOS-mt/p/5445284.html)

[Objective-C开发编码规范](http://www.cocoachina.com/ios/20150508/11780.html)

[iOS开发总结之代码规范](http://www.jianshu.com/p/414bb5a53139)

[iOS开发代码规范(通用)](http://www.cnblogs.com/gfxxbk/p/5469017.html)

[iOS中书写代码规范35条小建议](http://www.jianshu.com/p/71fdd1ae714c)

