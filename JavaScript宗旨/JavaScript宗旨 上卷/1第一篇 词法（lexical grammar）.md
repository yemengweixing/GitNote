JavaScript 的词法（lexical grammar）。
ECMAScript 源码文本会被从左到右扫描，并被转换为一系列的输入元素，包括 token、控制符、行终止符、注释和空白符。ECMAScript 定义了一些关键字、字面量以及行尾分号补全的规则。


 ECMAScript 程序的源文本首先转换成一个输入元素序列；tokens，行终结符，注释，空白构成输入元素序列。从左到右扫描源文本，反复获取作为下一个输入元素的尽可能长的字符序列。

 词法文法有两个目标符。InputElementDiv 目标符用在允许除法 (/) 或除赋值 (/=) 运算符开始的语法文法上下文中。InputElementRegExp 目标符用在其他语法文法上下文。

 没有允许除法或除赋值运算符开头，同时又允许 RegularExpressionLiteral 开头的语法文法上下文。这不会被分号插入（见 7.9）影响；如下面的例子：


a = b /hi/g.exec(c).map(d);
 其中 LineTerminator 后的第一个非空白，非注释字符是斜线（/），并且这个语法上下文允许除法或除赋值运算符，所以不会在这个 LineTerminator 位置插入分号。也就是说，上面的例子解释为：


a = b / hi / g.exec(c).map(d);
 语法：

InputElementDiv ::
WhiteSpace
LineTerminator
Comment
Token
DivPunctuator
InputElementRegExp ::
WhiteSpace
LineTerminator
Comment
Token
RegularExpressionLiteral

一
Unicode 格式控制字符
 Unicode 格式控制字符（即，Unicode 字符数据库中“Cf”分类里的字符，如“左至右符号 (left-to-right mark)”或“右至左符号 (left-to-right mark)”）是用来控制被更高层级协议（如标记语言）忽略的文本范围的格式的控制代码。

 允许在源文本中出现控制字符是有用的，以方便编辑和显示。所有格式控制字符可写入到注释，字符串字面量，正则表达式字面量中。

 在某些语言中和控制字符用于创建必要的的分隔符分割词或短语。在 ECMAScript 源文本里，和还可以用在一个标识符后的第一个字符。

 控制字符主要出现的文本的开头，标记它是 Unicode，并允许检测文本的编码和字节顺序。用于这一目的字符，有时也可能出现在文本开始的后面，例如，一个合并的文件。字符被视为空白字符（见 [7.2]）。

 表 1 总结了一些在注释，字符串字面量，正则表达式字面量之外被特殊对待的格式控制字符。

控制字符的使用
字符编码值	名称	正式名称	用途
\u200C	零宽非连接符	<ZWNJ>	IdentifierPart
\u200D	零宽连接符	<ZWJ>	IdentifierPart
\uFEFF	位序掩码	<BOM>	Whitespace
空白字符
 空白字符用来改善源文本的可读性和分割 tokens（不可分割的词法单位），此外就无关紧要。空白字符可以出现的两个 token 之间还可以出现在输入的开始或结束位置。空白字符，还可以出现在字符串 字面量 (StringLiteral) 或正则 表达式字面量 (RegularExpressionLiteral)( 在这里它表示组成字面量的字符 ) 或 注释 (Comment) 中，但是不能出现的其他任何 token 内。







二空白字符
 表 2 中列出了 ECMAScript 空白字符。


空白字符
字符编码值	名称	正式名称                说明                              转义序列
\u0009	制表符	<TAB>                      水平制表符                         \t
\u000B	纵向制表符	<VT>                   垂直制表符                          \v
\u000C	进纸符(分页符)	<FF>               分页符（Wikipedia）                 	\f
\u0020	空格	<SP>
\u00A0	非断空格	<NBSP>                 在该空格处不会换行
\uFEFF	位序掩码	<BOM>
Others 其它分类“Zs”	其它任何Unicode"空白分隔符"	<USP>
 ECMAScript 实现必须认可 Unicode 3.0 中定义的所有空白字符。后续版本的 Unicode 标准可能定义其他空白字符。ECMAScript 实现可以认可更高版本 Unicode 标准里的空白字符。

 语法：

WhiteSpace ::
<tab>
<vt>
<ff>
<sp>
<nbsp>
<bom>
<usp>




三
行终结符
 像空白字符一样，行终止字符用于改善源文本的可读性和分割 tokens（不可分割的词法单位）。然而，不像空白字符，行终结符对语法文法的行为有一定的影响。一般情况下，行终结符可以出现在任何两个 token 之间，但也有少数地方，语法文法禁止这样做。行终结符也影响自动插入分号过程（7.9）。行终结符不能出现在 StringLiteral 之外的任何 token 内。行终结符只能出现在作为 LineContinuation 一部分的 StringLiteral token 里。

 行终结符可以出现在 MultiLineComment（7.4）内，但不能出现在 SingleLineComment 内。

 正则表达式的 \s 类匹配的空白字符集中包含行终结符。

 表 3 列出了 ECMAScript 的行终止字符。

行终止字符
字符编码值	名称	正式名称                                         转义序列
\u000A	进行符	<LF>          在UNIX系统中起新行                     \n
\u000D	回车符	<CR>          在 Commodore 和早期的 Mac 系统中起新行  \r
\u2028	行分隔符	<LS>
\u2029	段分隔符	<PS>
 只有表 3 中的字符才被视为行终结符。其他新行或折行字符被视为空白，但不作为行终结符。字符序列 作一个行终结符。计算行数时它应该被视为一个字符。

 语法：


LineTerminator ::

LineTerminatorSequence ::
[lookahead ∉ ]


四        注释
 注释可以是单行或多行。多行注释不能嵌套。

 因为单行注释可以包含除了 LineTerminator 字符之外的任何字符，又因为有一般规则：一个 token 总是尽可能匹配更长，所以一个单行注释总是包含从 // 到行终结符之间的所有字符。然而，在该行末尾的 LineTerminator 不被看成是单行注释的一部分，它被词法文法识别成语法文法输入元素流的一部分。这一点非常重要，因为这意味着是否存在单行注释都不影响自动分号插入进程（见 7.9）。

 像空白一样，注释会被语法文法简单丢弃，除了 MultiLineComment 包含行终结符字符的情况，这种情况下整个注释会当作一个 LineTerminator 提供给语法文法解析。

 语法：

Comment ::
MultiLineComment
SingleLineComment

MultiLineComment ::
/* MultiLineCommentCharsopt*/
MultiLineCommentChars ::
MultiLineNotAsteriskChar MultiLineCommentCharsopt
* PostAsteriskCommentCharsopt
PostAsteriskCommentChars ::
MultiLineNotForwardSlashOrAsteriskChar MultiLineCommentCharsopt
* PostAsteriskCommentCharsopt

MultiLineNotAsteriskChar ::
SourceCharacter but not asterisk *

MultiLineNotForwardSlashOrAsteriskChar ::
SourceCharacter but not forward-slash / or asterisk *

SingleLineComment ::
// SingleLineCommentCharsopt

SingleLineCommentChars ::
SingleLineCommentChar SingleLineCommentCharsopt

SingleLineCommentChar ::
SourceCharacter but not LineTerminator

一种是单行注释（single-line comment），使用 //，会将该行中符号以后的文本都视为注释：
  // 这是单行注释

二种是多行注释（multiple-line comment），使用 /* */ ，这种方式更加灵活：
/* 单行注释 */
 /* 多行注释，
     直到终止符号才结束 */
块注释也可以用来屏蔽一段代码，只要将这段代码用块注释包裹起来就可以


Hashbang 注释节
A specialized third comment syntax, the hashbang comment, is in the process of being standardized in ECMAScript (see the Hashbang Grammar proposal).

A hashbang comment behaves exactly like a single line-only (//) comment, but it instead begins with #! and is only valid at the absolute start of a script or module. Note also that no whitespace of any kind is permitted before the #!. The comment consists of all the characters after #! up to the end of the first line; only one such comment is permitted.

The hashbang comment specifies the path to a specific JavaScript interpreter
that you want to use to execute the script. An example is as follows:

#!/usr/bin/env node

console.log("Hello world");
注意：Hashbang comments in JavaScript mimic shebangs in Unix used to run files with proper interpreter.

Although BOM before hashbang comment will work in a browser it is not advised to use BOM in a script with hasbang. BOM will not work when you try to run the script in Unix/Linux. So use UTF-8 without BOM if you want to run scripts directly from shell.

You must only use the #! comment style to specify a JavaScript interpreter. In all other cases just use a // comment (or mulitiline comment).


五
Tokens
 语法：

Token ::
IdentifierName
Punctuator
NumericLiteral
StringLiteral
注: DivPunctuator 和 RegularExpressionLiteral 产生式定义 tokens ，但 Token 的产生式不包含它们。


六
标识符名(IdentifierName)和标识符(Identifier)

标识符用于 变量 常量 对象 函数及形参的命名

1 开头只能为 字母 $ 下划线（——） 

2 开头后的 可以由 字母 数字 $ 下划线（——）组成

3区分大小写

4不能 保留字


 标识符名是 tokens，Unicode 标准第 5 章的“标识符”节给出的文法加入了一些小的修改来解释它。Identifier 是一个 IdentifierName 但不是一个 ReservedWord( 见 7.6.1)。Unicode 标识符文法基于 Unicode 标准指出的 normative 和 informative 字符分类。所有符合 ECMAScript 的实现必须能够正确处理 Unicode 标准 3.0 版本中指定的分类里的字符的分类。

 本标准增加了个别字符：在 IdentifierName 的任何位置允许出现美元符（$）和下划线（_）。

 IdentifierName 还允许出现 Unicode 转义序列，它们被 UnicodeEscapeSequence 的 CV 计算成单个字符贡献给 IdentifierName（见 7.8.4）。UnicodeEscapeSequence 前面的 \ 不给IdentifierName 贡献字符。UnicodeEscapeSequence 不能提供单个字符给将要成为非法字符的 IdentifierName。换句话说，如果一个 \ UnicodeEscapeSequence 序列被UnicodeEscapeSequence 的 CV 替换，结果必须仍是有效的包含与原 IdentifierName 精确相同字符序列的 IdentifierName。本规范说明的所有标识符是根据它的实际字符，不管转义序列贡献特定字符与否。

 根据 Unicode 标准两个规范的 IdentifierName 相等，是说除非他们的代码单元序列准确相等，否则不同（换句话说，符合 ECMAScript 的实现只需要按位比较 IdentifierName 值）。其目的是为了传入编译器之前就把源文本转换为正常化形式 C。

 ECMAScript 实现可以识别后续版本 Unicode 标准定义的标识符字符。如果考虑可移植性，程序员应该只采用 Unicode 3.0 中定义的标识符字符。

 语法：


Identifier ::
IdentifierName but not ReservedWord
IdentifierName ::
IdentifierStart
IdentifierName IdentifierPart
IdentifierStart ::
UnicodeLetter
$
_
\ UnicodeEscapeSequence
IdentifierPart ::
IdentifierStart
UnicodeCombiningMark
UnicodeDigit
UnicodeConnectorPunctuation
 UnicodeLetter
any character in the Unicode categories
“Uppercase letter (Lu)”, “Lowercase letter (Ll)”,
“Titlecase letter (Lt)”, “Modifier letter (Lm)”,
“Other letter (Lo)”,or “Letter number (Nl)”.
 UnicodeCombiningMark
any character in the Unicode categories “Non-spacing mark (Mn)”\\\
or “Combining spacing mark (Mc)”

UnicodeDigit
any character in the Unicode category “Decimal number (Nd)”

UnicodeConnectorPunctuation
any character in the Unicode category “Connector punctuation (Pc)”

UnicodeEscapeSequence
see 7.8.4.

六。关键字和保留字

六。一
关键词
 下列 token 是 ECMAScript 的关键词，用于表示控制语句的开始或结束，或者用于执行特定操作等，不能用作 ECMAScript 程序的 Identifiers。

break
case
catch
class
const
continue
debugger
default
delete
do
else
export
extends
finally
for
function
if
import
in
instanceof
new
return
super
switch
this
throw
try
typeof
var
void
while
with
yield
 let	const

六。二
未来保留字
 下列词被用作建议扩展关键字，因此保留，以便未来可能采用这些扩展。
 6 2 1
这些关键字在严格模式和非严格模式中均不能使用。

enum
以下关键字只在严格模式中被当成保留关键字：

implements
interface
let
package
private
protected
public
static
 

以下关键字只在模块代码中被当成保留关键字：

await
之前标准中的保留关键字
这里是之前版本中的ECMAScript（1到3）中的保留关键字：

abstract
boolean
byte
char
double
final
float
goto
int
long
native
short
synchronized
transient
volatile
另外，直接量null、true和false同样不能被当成标识使用。



七
标点符号
 语法

 Punctuator :: one of
{ } ( ) [ ]
.  ; , < > <=
>= ==  != ===  !==
+ - *  % ++ --
<< >> >>> & | ^  ! ~ && ||  ?  :
= += -= *=  %= <<=
>>= >>>= &= |= ^=


DivPunctuator :: one of
/ /=



八
字面量(literal) 即直接量
字面量是变量的字符串表示形式。它不是一种值，而是一种变量记法。除去表达式,当给变量赋值时，等号右边都可以认为是字面量
//var a = null  　　//空值字面量

直接量：直接量也称为字面量，是JavaScript中一种对象的表示(或者说创建)方式，它可以通过直接给变量赋上JavaScript中原生对象值的方式从而转换为一个相应的对象。
直接使用的数据，没有进行特别的封装



有数字（Number）字面量 字符串（String）字面量  表达式字面量 数组（Array）字面量 对象（Object）字面量 函数（Function）字面量

标识符  变量 常量 函数 属性 的名字 和函数的参数
，变量用于存储数据值（存储信息的"容器"）    变量通常是可变的。字面量是一个恒定的值
8 1
空值字面量
 语法：

null

 语义：

 空值字面量的值 null，是 Null 类型的唯一值。

8 2
布尔值字面量
 语法：

true
false
 语义：

 布尔值字面量的值 true 是个布尔类型值 ，即 true。

 布尔值字面量的值 false 是个布尔类型值 ，即 false。

8 3
数值字面量

十进制
0123456789

// 最好不使用 0 开头的数值：
0888 // 转换为十进制 888
0666 // 转换为八进制 666，十进制 552
注意，十进制数值直接量可以以 0 开头，但是如果 0 以后的最高位比 8 小，数值将会被认为是八进制而不会报错

二进制
var FLT_SIGNBIT  = 0b10000000000000000000000000000000; // 2147483648
var FLT_EXPONENT = 0b01111111100000000000000000000000; // 2139095040

二进制表示为开头是0后接大写或小写的B（0b或者0B）。
这是ECMAScript 6中的新语法，可以参考下面的浏览器兼容性表格。如果0b之后有除了0或1以外的数字，将会抛出SyntaxError：“Missing binary digits after 0b”。


八进制
八进制表示为开头是0后接大写或小写的O（0o或0O）。这是ECMAScript 6中的新语法，可以参考下面的浏览器兼容性表格。如果有不在（01234567）中的数字，将会抛出SyntaxError：“Missing octal digits after 0o”。

var n = 0O755; // 493

十六进制
十六进制表示为开头是0后接大写或小写的X（0x或0X）。如果有不在（0123456789ABCDEF）中的数字，将会抛出SyntaxError：“Identifier starts immediately after numeric literal”。

0xFFFFFFFFFFFFFFFFF // 295147905179352830000



8 4
字符串字面量
 一个字符串字面量是关闭的单引号或双引号里的零个或多个字符。每个字符都可以用一个转义序列代表。除了闭合银行字符，反斜杠，回车，行分隔符，段落分隔符，换行符之外的所有字符都可以直接出现的字符串字面量里。任何字符都可以通过转移序列的形式出现。

 语法
'foo'

 语义

 一个字符串字面量代表一个 String 类型的值。字面量的字符串值 (SV) 由字符串字面量各部分贡献的字符值 (CV) 描述。作为这一过程的一部分，字符字面量里的某些字符字符会被解释成包含数学值 (MV)，如 7.8.3 和下面描述的。


 十六进制转义序列
'\xA9' // "©"

Unicode 转义序列
Unicode 转义序列要求在\u之后至少有四个字符
字符串单字符转义序列
转义序列	字符编码值	名称	符号
\b	\u0008	回格	<BS>
\t	\u0009	水平制表符	<HT>
\n	\u000A	进行（新行）	<LF>
\v	\u000B	竖直制表符	<VT>
\f	\u000C	进纸	<FF>
\r	\u000D	回车	<CR>
\"	\u0022	双引号	"
\'	\u0027	单引号	'
\\	\u005C	反斜杠	\
CharacterEscapeSequence :: NonEscapeCharacter 的 CV 是 NonEscapeCharacter 的 CV.
NonEscapeCharacter :: SourceCharacter but not EscapeCharacter or LineTerminator 的 CV 是 SourceCharacter 字符自身 .
HexEscapeSequence :: x HexDigit HexDigit 的 CV 是 ((16 乘第一个 HexDigit 的 MV) 加第二个 HexDigit 的 MV) 代码单元确定的字符。
UnicodeEscapeSequence :: u HexDigit HexDigit HexDigit HexDigit 的 CV 是 (4096 乘第一个 HexDigit 的 MV) 加 (256 乘第二个 HexDigit 的 MV) 加 (16 乘第三个 HexDigit 的 MV) 加 ( 第四个 HexDigit 的 MV) 代码单元确定的字符。
 符合标准的实现，在处理严格模式代码（见 10.1.1）时，按照 B.1.2 的描述，不得扩展 EscapeSequence 包含 OctalEscapeSequence 的语法。

 行终结符不能出现在字符串字面量里，除非它成为 LineContinuation 的一部分产生空字符序列。让字符串字面量的字符串值包含行终结符的正确方法是使用转义序列，如 \n或 \u000A。

八 五
对象直接量
更多信息可以参考 Object 和对象初始化器。

var o = { a: "foo", b: "bar", c: 42 };

// ES6中的简略表示方法
var a = "foo", b = "bar", c = 42;

八 五
数组直接量
更多信息可以参考 Array。

[1954, 1974, 1990, 2014]

八 五
正则表达式字面量
 正则表达式字面量是输入元素，每当字面量被评估时会转换为 RegExp 对象（见 15.10）。当一个程序中有两个正则表达式字面量评估成正则表达式对象，不能用 === 比较他们是否相等，即使两个字面量包含相同内容。RegExp 对象也可以在运行时使用 new RegExp（见 15.10.4）或以函数方式调用 RegExp 构造器来创建（见 15.10.3）。

 下面的产生式描述了正则表达式字面量的语法，输入元素扫描器还用它搜索正则表达式字面量的结束位置。RegularExpressionBody 和 RegularExpressionFlags 包含的字符组成的字符串会直接传递给正则表达式构造器，在那里用更严格文法进行解析。一个实现可以扩展正则表达式构造器的文法。但它不能扩展 RegularExpressionBody 和 RegularExpressionFlags 产生式或使用这些产生式的产生式。

 语法

 正则表达式字面量不能为空；并不是说正则表达式字面量不能代表空，字符 // 会启动一个单行注释。要指定一个空正则，使用：/(?:)/。

 语义

 正则表达式字面量会评估为一个 Object 类型值，它是标准内置构造器 RegExp 的一个实例。此值取决于两个步骤：首先，展开组成正则表达式产生式 RegularExpressionBody 和RegularExpressionFlags 的字符，将其以未解析形式分别存成两个字符串 Pattern 和 Flags。然后，在每次评估字面量时创建新对象，仿佛使用 new RegExp(Pattern, Flags) 一样，这里的 RegExp 是标准内置构造器名。新构造的对象将成为 RegularExpressionLiteral 的值。如果调用 new RegExp 会产生 15.10.4.1 指定的错误，那么必须把错误当作是早期错误 ( 见 第 16 章 )。

八 五
模板直接量(模板字符串直接量)
更多信息可以参考template strings。

`string text`

`string text line 1
 string text line 2`





九
自动分号插入
 必须用分号终止某些 ECMAScript 语句 ( 空语句 , 变量声明语句 , 表达式语句 , do-while 语句 , continue 语句 , break 语句 , return 语句 ,throw 语句 )。这些分号总是明确的显示在源文本里。然而，为了方便起见，某些情况下这些分号可以在源文本里省略。描述这种情况会说：这种情况下给源代码的 token 流自动插入分号。

空语句
let、const、变量声明
import、export、模块定义
表达式语句
debugger
continue、break、throw
return

自动分号插入规则
 分号插入有三个基本规则：
1
左到右解析程序，当遇到一个不符合任何文法产生式的 token（叫做 违规 token(offending token)），那么只要满足下面条件之一就在违规 token 前面自动插入分号。
（出现一个不允许的行终止符或“}”时，会在其之前插入一个分号）
至少一个 LineTerminator 分割了违规 token 和前一个 token。
违规 token 是 }。
2
左到右解析程序，tokens 输入流已经结束，当解析器无法将输入 token 流解析成单个完整 ECMAScript 程序 ，那么就在输入流的结束位置自动插入分号。
 当捕获到标识符输入流的结尾，并且无法将单个输入流转换为一个完整的程序时，将在结尾插入一个分号
3
左到右解析程序，遇到一个某些文法产生式允许的 token，但是此产生式是受限产生式，受限产生式的里紧跟在 no LineTerminator here 后的第一个终结符或非终结符的 token 叫做受限的 token，当至少一个 LineTerminator 分割了受限的 token 和前一个 token，那么就在受限 token 前面自动插入分号。
 然而，上述规则有一个附加的优先条件：如果插入分号后解析结果是空语句，或如果插入分号后它成为 for 语句头部的两个分号之一（见 12.6.3），那么不会自动插入分号。

 当语句中包含语法中的限制产品后跟一个行终止符的时候，将会在结尾插入一个分号。带“这里没有行终止符”规则的语句有：

后置运算符（++ 和 --）
continue
break
return
yield、yield*
module
--------------------------------------------------------------------------------

 文法里的受限产生式只限以下：

PostfixExpression :
LeftHandSideExpression [no LineTerminator here] ++
LeftHandSideExpression [no LineTerminator here] --

ContinueStatement :
continue [no LineTerminator here] Identifier;

BreakStatement :
break [no LineTerminator here] Identifier;

ReturnStatement :
return [no LineTerminator here] Expression;

ThrowStatement :
throw [no LineTerminator here] Expression;
 这些受限产生式的实际效果如下：

 当遇到的 ++ 或 --token 将要被解析器当作一个后缀运算符，并且至少有一个 LineTerminator 出现 ++ 或 --token 和它之前的 token 之间，那么在 ++ 或 --token 前面自动插入一个分号。

 当遇到 continue, break, return, throw token，并且在下一个 token 前面遇到 LineTerminator，那么在 continue, break, return, throw token 后面自动插入一个分号。

 这对 ECMAScript 程序员的实际影响是：

 后缀运算符 ++ 或 -- 和它的操作数应该出现在同一行。

 return 或 throw 语句的表达式开始位置应该和 return 或 throw token 同一行。

 break 或 continue 语句的标示符应该和 break 或 continue token 同一行。

自动分号插入的例子
 源代码：


{ 1 2 } 3
 即使在自动分号插入规则下，它也不符合 ECMAScript 文法。做为对比，源代码：


{ 1 2 } 3
 它还是不符合 ECMAScript 文法，但是它会被自动分号插入成为一下形式：


{ 1  ;2 ;} 3;
 这符合 ECMAScript 文法。

 源代码：


for (a; b )
 不符合 ECMAScript 文法，并且不会被自动分号插入所更改，因为 for 语句头部需要分号。自动分号插入从来不会插入成 for 语句头部的两个分号之一。

 源代码：


return a + b
 会被自动分号插入转换成以下形式：


return; a + b;
 表达式 a + b 不会被当做是 return 语句要返回的值，因为有一个 LineTerminator 分割了它和 return token。

 源代码：


a = b ++c
 会被自动分号插入转换成以下形式：


a = b; ++c;
 ++token 不会被当做应用于变量 b 的后缀运算符，因为 b 和 ++ 之间出现了一个 LineTerminator。

 源代码：


if (a > b) else c = d
 它不符合 ECMAScript 文法 ，else token 前面不会被自动分号插入改变，即使没有文法产生式适用这一位置，因为自动插入分号后会解析成空语句。

 源代码：


a = b + c (d + e).print()
 它不会被自动分号插入改变，因为第二行开始位置的括号表达式可以解释成函数调用的参数列表：


a = b + c(d + e).print()
 在赋值语句必须用左括号开头的情况下，程序员在前面语句的结束位置明确的提供一个分号是个好主意，而不是依赖于自动分号插入。