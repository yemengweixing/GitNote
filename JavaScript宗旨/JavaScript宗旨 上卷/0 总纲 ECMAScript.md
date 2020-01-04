JavaScript 是一门跨平台、面向对象的脚本语言。为动态类型、弱类型、基于原型的语言。
完整的JavaScript实现由三者组成：ECMAScript，文档对象模型，浏览器对象模型。










诞生于1995，由网景通信公司（Netscape Communications Corporation）的Brendan Eich设计（两周之内设计出）。
最初将其脚本语言命名为LiveScript。后来Netscape在与Sun合作之后将其改名为JavaScript（希望借Java的名气来推广，最初JavaScript是甲骨文公司的注册商标）。JavaScript最初受Java启发而开始设计的，目的之一就是“看上去像Java”，因此语法上有类似之处，一些名称和命名规范也借自Java。但JavaScript的主要设计原则源自Self和Scheme。


#ECMAScript 为规范
The specification defined in ECMA-262 中定义的标准，是用于创建通用目的脚本语言的

ECMAScript为Ecma国际（Ecma International前身为欧洲计算机制造商协会,英文名称是European Computer Manufacturers Association）通过ECMA-262标准化的脚本程序设计语言。往往被称为JavaScript或JScript。
**ECMA-262 傻Ecma 国际发布的标准 定义了名为 ECMAScript 的脚本语言的规范。**
**ECMA-262是标准的名称，它代表了脚本语言规范ECMAScript**

**JavaScript 为语言 实现了多数 ECMA-262 中描述的 ECMAScript 规范**
来历：
初期，并没有JavaScript的标准。
1995年Netscape公司发布的Netscape Navigator 2.0中使用与Sun联合开发的JavaScript 1.0，而后的3.0版本中发布了JavaScript1.1。而同时微软的IE 3.0使用JScript和CEnvi的ScriptEase。三种不同版本的客户端脚本语言同时存在。

1997年，JavaScript 1.1作为草案提交给欧洲计算机制造商协会（ECMA）
第三十九技术委员会（TC39）与由Netscape、Sun、微软、Borland等公司的参与组成的工作组 确定统一标准：ECMA-262。（因为JavaScript是网景的注册商标，所以不能起名JavaScript定为标准）

>此后的Javascript，JScript，ActionScript等脚本语言都是基于ECMAScript标准实现的。
>ECMAScript实际上是一种脚本在语法和语义上的标准。实际上JavaScript是由ECMAScript，DOM和BOM三者组成的。
#ECMAScript版本
由 ECMA（欧洲电脑制造商协会）通过 ECMAScript 实现语言的标准化。

年份	名称	描述
1997	ECMAScript 1	第一个版本

1998	ECMAScript 2	版本变更，基本没有加新功能

1999 2002年	ECMAScript 3	
添加正则表达式 成为JavaScript的通行标准，得到了广泛支持
添加 try/catch

 	ECMAScript 4	没有发布，部分功能被迁移到ES6中

2009	ECMAScript 5
增加很多功能：访问器属性，对象的反射创建和检查，属性属性的程序控制，附加的数组操作函数，对json对象编码格式，严格模式(use strict)

2011	ECMAScript 5.1	
成为国际标准iso / iec 16262：2011。发布ES5.1版本 同时被MCMA-262和ISO/IEC批准。

2015	ECMAScript 6(即ES2015 和 ECMAScript 2015)	
添加类和模块( ECMAScript 规范有着显著的变化和改进)
>也可称为ES2015 ，因为 Ecma 国际决定每年都对 ECMAScript 发布一次。即 Ecma 国际 也开始基于每年所发布的来命名新版本的 ECMAScript 规范

2016	ECMAScript 7	
增加指数运算符 (**)，增加 Array.prototype.includes


#附：关键字 保留字
ECMA-262定义了ECMAScript支持的一套关键字（keyword）
ECMAScript关键字的完整列表：

break
case
catch
continue
default
delete
do
else
finally
for
function
if
in
instanceof
new
return
switch
this
throw
try
typeof
var
void
while
with

关键字用作标识符，可能得到诸如“Identifier expected”（应该有标识符、期望标识符）这样的错误信息


ECMA-262定义了ECMAScript支持的一套保留字（reserved word）。在某种意义上是为了将来的而保留的单词。因此，保留字不能被用作变量名或函数名。
ECMA-262第3版中保留字的完整列表如下：

abstract
boolean
byte
char
class
const
debugger
double
enum
export
extends
final
float
goto
implements
import
int
interface
long
native
package
private
protected
public
short
static
super
synchronized
throws
transient
volatile

如果将保留字用作标识符，那么除非将来的浏览器实现了该保留字，否则很可能收不到任何错误消息。当浏览器将其实现后，该单词被看作关键字，如此将出现关键字错误。















