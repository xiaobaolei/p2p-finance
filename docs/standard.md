#PHP编码规范
##前言
###适用范围
适用PHP5.4+，基于psr-1，psr-2，prs-4， 主要参考了[Yii2][1]、[Symfony2][2]、[ZendFramework2][3]、[PEAR][4]
###语气说明
必须 - MUST、REQUIRED、SHALL  
不允许 - MUST NOT  
推荐 - SHOULD、RECOMMENDED  
不推荐 - SHOULD NOT 
可选(建议) - OPTIONAL、MAY  

###术语表和参考引用
首字母大写驼峰： StudlyCaps = CamelCase = Pascal
首字母小写驼峰： camelCase
全小写下划线分割：lowercase_underscore
全小写短横线峰：lowercase-dash
##基础规范
 - 文件编码**必须**使用UTF-8无BOM。
 - **必须**使用`LF`(`\n`)做为换行符，而不是(`CRLF`)`\r\n`。
 - **必须**使用`<?php ?>`或者`<?= ?>`，如果文件仅包含纯PHP代码，**不允许**结束标签`?>`。(防止`include`文件不期望的空白符或换行符输出）
 - 文件最后一行**必须**有一个空行。
 - 代码行的长度不做硬性规定，但**推荐**不超过120，最好控制在80以下。
 - 在非必要情况下**不推荐**直接使用`include/require/require_once/include_once`，由psr-4实现。

##命名规范
###关键字
 - 关键字**必须**为小写，如`if` `for` `function` ...。  
###全局常量###
 - 使用大写字母命名，使用划线来分隔单词。如有模块名/包名带上前缀。
 - PHP内置常量 `true`、`false`、`null`**必须**小写。
 - 自定义常量**推荐**使用 `const`关键字来定义，而不是`define()`，除了必须使用`define()`的情况（如if语句结构中）。 
```php
const MODULE_MY_CONST = true;
if (false) {
    define('MODULE_MY_ANOTHER_CONST', false);
}

```
###全局变量
 - **不推荐**使用，如果使用，**建议**遵从以下规则：
 - 全小写，如果模块/包名为`CamelCase`，则必须有```$camel_case```前缀。
 - 模块名或包名作为前缀，单词之间用下划线分割。
 例如：`$module_var`、`$package_var`。
 - 如果作用域仅在本模块中则加下划线前缀。
 例如：`$_module_var`。

###全局函数
 - **不推荐**使用，**推荐**封装成Helper或Until类且**建议**遵从以下规则：
 - 全小写，如果模块/包名为CamelCase，则写成camel_case。
 - 模块名或包名作为前缀，单词之间用下划线分割。
 例如：`module_func`、`package_func`。
 - 如果作用域仅在本模块中调用则加下划线前缀。
 例如：`_module_func`。

 - ~~TODO如何对内置PHP函数改进？~~
 - ~~TODO如何对内置PHP函数包裹？~~

###函数参数
 - **推荐**使用camelCase。
###局部变量
 - **推荐**使用camelCase。

###命名空间
 - **必须**使用CamelCase。

###命名空间别名
 - **必须**使用CamelCase。

###类
 - **必须**使用CamelCase。
 - 异常类**必须**以Exception作为后缀。

###抽象类
 - **必须**使用CamelCase，以Abstract作为前缀。

###类常量
 - **必须**使用大写字母命名，使用划线来分隔单词。无需带上模块/包名前缀。

###类属性
 - **推荐**使用camelCase，用public、protected、private修饰都是如此。

###方法
 - **推荐**使用camelCase，用public、protected、private修饰都是如此。

###静态属性
 - **推荐**使用camelCase，用public、protected、private修饰都是如此。

###静态函数
 - **推荐**使用camelCase，用public、protected、private修饰都是如此。

###接口
 - **必须**使用CamelCase，并且用Interface作为后缀。

###trait
 - **必须**使用CamelCase， 并且用Trait作为后缀。

###目录名
 - 如果是遵从了psr-4的自动加载，**必须**为CamelCase。
 - 其他情况皆**必须**小写且用短横线`-`分割单词（尽量使用一个单词），可以为复数形式。

###文件名
 - 文档文件全部大写，后缀小写。如README.txt, INSTALL.txt, TODO.txt, CHANGELOG.txt
 - 纯PHP代码文件，如果仅包含一个类（接口、trait）遵从psr-4，则**必须**使用`CamelCase`，其他情况则**必须**全小写且用`下划线`(`_`)分割单词。例如：`config_development.php`。
 - 混合了PHP代码的视图文件，则全小写且用`短横线`(`-`)分割单词。例如：`clomun3-right.php`。

##书写规范

###缩进Indenting
 - **必须**使用4个空格代替Tab
###操作符Operators
 - 一元操作符 ++、--、!、~与操作数之间**不允许**空格。
 例如：`$i++;`
 - 二元操作符 =、. 、+= 、.=等 两边**必须**有空格。
 例如：`$a > $b;`
 - 三元操作符?:与操作数之间**必须**有空格。
 例如：`$a = isset($b) ? $b : '';`
```php
//综合示例
//变量名过长换行的情况，新行应该缩进，操作符应该顶头
$sum = $loooooooooooongVariable1
    + $loooooooooooongVariable2
    + $loooooooooooongVariable3
;
//字符串太长
$sql = "SELECT `id`, `name` "
    . "FROM `people` "
    . "WHERE `name` = 'Susan' "
    . "ORDER BY `name` ASC "
;
//三元表达式 条件太长
$foo = $longCondition1 && $longCondition2
    ? $foo : $bar
;
//三元表达式变量名太长
$foo = empty($shortCondition)
    ? $longVariableName1
    : $longVariableName2
;

```
###数组定义
 - **推荐**使用`[]`定义数组，而不是`array()`;
 - 单行的情况下每个元素用逗号空格`,　`分割，最后一个元素无需逗号；多行的情况下用逗号换行符分割，最后一个元素也应该有一个逗号`,`。
 - 多行的情况下，`[`或者`array(`后**不允许**跟数组元素。
 - 关联数组，多行情况下，多个key name相似的情况下，**建议**对齐赋值符`=>`。
```php
//一般形式
$sampleArray = array('hello', 'world', 'foo' => 'bar');
//多行，列表数组参数很多
$sampleArray = array(
    1, 2, 3,
    $a, $b, $c,
);
//多行，关联数组参数很多
$sampleArray = array(
    'foo' => 'bar',
    'spam' => 'ham',
);
//多行，关联数组如有相似的键名，则建议对齐
$sampleArray = array(
    'foo1'   => '1',
    'foo22'  => '22',
    'foo333' => '333',
    'spam' => '4444',
);
```
###字符串定义及单引号与双引号
 - 当字符串是普通文字(不包含变量、转义字符、单引号)，**必须**用单引号，否则使用双引号。
 - 变量替换**推荐**使用{\$var}形式，**不允许**\${var}
```php
$greeting = "Hello {$name}, welcome back!";
```
###强制类型转换Casting
 - 类型与变量之间**推荐**有个空格。(int) $mynumber
###流程控制语句Control Structure
 - 关键字之后**必须**有一个空格。 例如: `if ()...`
 - 左圆括号`(`之后不能有空格，右圆括号`)`之前**不允许**有空格。例如:`if ($exp)`
 - 右圆括号`)`与左花括号`{`之间**必须**有一个空格。 
 - 右圆括号`)`与左花括号`{`**必须**在同一行。
 - 结构主体**必须**缩进一次。
 - 任何情况下都**必须**使用花括号`{}`包裹，无论有多少条语句。
 - 如果右花括号`}`为语句结束行，**必须**独占一行。
 - 在PHP视图文件中**推荐**使用if-endif、switch-endswitch、while-endwhile、for-endfor、foreach-endforeach结构。

#### if，elseif，else
 - 推荐使用`elseif`，而不是`else if`。
```php
//一般形式
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
//表达式较长
if (
    ($condition1 || $condition2)
    && $condition3
    && $condition4
) {
    //code here
}
```
####switch，case
 - `case`后面没有`break`语句**必须**注释说明。
```php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```
####for
```php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```
####foreach
```php
foreach ($iterable as $key => $value) {
    // foreach body
}
```
####while
```php
while ($expr) {
    // structure body
}
```
####do while
```php
do {
    // structure body;
} while ($expr);
```
####try catch
```php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```
####break
 - 独占一行。
####continue
 - 独占一行。
####return
 - 独占一行，如果在函数最后一行，在它前面还应插入一个空行。
```php
function foo() {
    //function body

    return $bar;
}
```
####视图文件中的流程控制语句
```
<?php if ($expression == true): ?>
  This will show if the expression is true.
<?php else: ?>
  Otherwise this will show.
<?php endif; ?>
```
###函数
####函数定义
 - 函数名与左圆括号`(`不允许有空格。
 - 函数参数之间用逗号`,`空格分隔。
 - 左圆括号`(`之后，右圆括号`)`之前不允许有空格。
 - 左花括号`{`另起一行，右花括号`}`另起一行。
```php
function foo($arg1, &$arg2, $arg3 = []) {
    // method body
   
    return true;
}
```
####函数调用
 - 函数名与左圆括号`(`不允许有空格。
 - 函数参数之间用逗号空格`,　`分隔。
```php
//一般形式
$val = foo($bar, $biz);
//参数列表过多，参数名过长，推荐的换行形式
foo(
    $longArgument,
    $longerArgument,
    $muchLongerArgument ,
    [
        'key1' => 'value1',
    ]
);
//参数过长
foo(
    [
        'key1' => 'value1',    
    ],
    $longArgument,
    [
        'x1' => 'y1',
    ]
);
//最后一个参数为数组，函数名与([在同一行，则以])结束
foo($var, [
    'key1' => 'value1',    
]);
//最后一个参数为数组, 函数名与(array(在同一行，则以))结束
foo($var, array(
    'key1' => 'value1',    
));
//最后一个参数为闭包时的特殊情况，函数名与(...{在同一行，则以})结束
foo(function ($arg2) use ($var1) {
    // body
});
//参数也为函数调用
fun1(
    fun2(
        fun3(
            'Help me!',
            array(
                'foo' => 'bar',
                'spam' => 'eggs',
            ),
            23
        ),
        fun3()
    ),
    fun4(12)
);
```
###类
####类定义
 - 必须有一个命名空间，命名空间与类之间应该有一空白行。
 - `extends` 和 `implements`关键字必须在同一行。
 - 花括号应当从类名下一行开始
 - 类中所有代码必需用四个空格的缩进。
 - 每个 PHP 文件中只有一个类。
 - 先定义类的常量，再定义类的属性，再定义类的方法。
 - 每个属性独占一行。
 - 推荐 按照`public`>`protected`>`privated`先后顺序去定义属性和方法。
 - 属性或者方法的定义之间推荐增加一个空白行。
 - 不推荐protected、private之后的属性或方法名使用一个underscore前缀。
 - `abstract`、`final`修饰符在 可视性修饰（public、protected、privated）之前，而 `static`修饰符在可视性修饰符之后。
```php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

abstract class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
    public $foo = null;
   
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
   
    final public static function bar()
    {
        // method body
    }
    
    abstract protected function zim();
}
```
####类实例化
 - 必须有括号，无论构造函数是否带参。
```php 
$foo = new MyClassName();
```
####类静态成员调用
 - 无
####类属性调用
 - 无
####类静态函数调用
 - 无

####类方法调用
```php
//一般形式与全局函数调用类似，见上

//链式操作，推荐多行
$someObject->someFunction("some", "parameter")
    ->someOtherFunc(23, 42)
    ->andAThirdFunction()
;
```
###闭包Closures
 - 关键词`function`与左圆括号`(`之间必须有一个空格，`use`关键字两边必须有一个空格。
```php
//最后一个参数为闭包时的特殊情况，函数名与(...{在同一行，以})结束
foo->bar(function ($arg2) use ($var1) {
    // body
});
//为参数
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);

$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

```
### ~~TODO文档注解，需要完善
 - 现在写有写纸上谈兵的感觉，而且文档的撰写必须费脑细胞，对于快速迭代有一定干扰~~
 - 所有文档块必须兼容phpDocumentor，语法参考：http://phpdoc.org/
 - 所有的类文件在起始处必须包含一个"文件级"的文档块，"类级"文档块下面立即为类申明

####文件
 - 所有包含的PHP代码的文件在起始处**必须**有一个文档块，它至少包含下面几个标签:
```php
/**
 * @link http://www.yiiframework.com/
 * @copyright Copyright (c) 2008 Yii Software LLC
 * @license http://www.yiiframework.com/license/
 */
```
####类
```php
/**
 * Component is the base class that provides the *property*, *event* and *behavior* features.
 *
 * @include @yii/docs/base-Component.md
 *
 * @author Qiang Xue <qiang.xue@gmail.com>
 * @since 2.0
 */
class Component extends \yii\base\Object
```

####函数/方法
 - 在没有返回值的情况下**推荐** `@return void`
```php
/**
 * Returns the list of attached event handlers for an event.
 * You may manipulate the returned [[Vector]] object by adding or removing handlers.
 * For example,
 *
 * ~~~
 * $component->getEventHandlers($eventName)->insertAt(0, $eventHandler);
 * ~~~
 *
 * @param string $name the event name
 * @return Vector list of attached event handlers for the event
 * @throws Exception if the event is not defined
 */
public function getEventHandlers($name)
{
    if (!isset($this->_e[$name])) {
        $this->_e[$name] = new Vector;
    }
    $this->ensureBehaviors();
    return $this->_e[$name];
}
```


  [1]: https://github.com/yiisoft/yii2/blob/master/docs/internals/core-code-style.md
  [2]: http://symfony.com/doc/current/contributing/code/standards.html
  [3]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
  [4]: http://pear.php.net/manual/en/standards.php