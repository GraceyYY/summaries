JavaScript基本数据类型小结：

JavaScript中数据类型分为两类，原始类型（primitive types）和对象类型（object types）。

* 原始类型包含Boolean，Number，String，Undefined，Null，Symbol （ES6）。原始类型的数据是不可变的（immutable）。

  1. Boolean：Boolean类型的字面值只有两个，true和false（大小写敏感，全部为小写才是Boolean值，其他大小写混合的形式都不是Boolean值，而是标识符）。`Boolean()`为转型函数，可以对任何数据类型的值调用`Boolean()`函数，且总会返回一个Boolean值。`Boolean()`函数对不同类型数据有着自己的转换规则，这些转换规则对理解控制流语句（如if语句）自动执行的相应转换非常重要。

  2. Number：使用IEEE754格式来表示整数和浮点数值。

     * 整型直接量： 可用十进制和十六进制字面值表示。八进制在严格模式下无效。
     * 浮点型直接量：可用实数写法（整数部分+小数点+小数部分）和科学计数法表示。
     * 最大值为1.7976931348623157e+308，可以通过`Number.MAX_VALUE`查看。超过最大值的数字将被显示为`Infinity`。
     * 最小值为5e-324，可以通过`Number.MIN_VALUE`查看。小于最小值的数字将被显示为`-Infinity`。
     * `Infinity`和`-Infinity`是Number类型中的特殊值，它们无法参与下次计算。为了避免`Infinity`和`-Infinity`影响运算，可以通过`isFinite()`函数进行判断该值是否是`Infinity/-Infinity`。
     * `NaN`（not a number）也是Number类型中的一个特殊值，用来表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误了）。它有以下两个特点：
       1. 任何涉及`NaN`的操作，都会返回`NaN`。
       2. `NaN`与任何数值都不相等，包括它自己。`NaN != NaN; //true`
          * 可以通过isNaN()函数去判断某个值是否是NaN，然而这个函数有一个bug，就是当该值不为数值时（例如string），返回值也会是true（因为这个函数检查该值是否不是`NaN`，也不是数字）。因此在判断某个值是否为`NaN`时，建议使用ES6的`Number.isNaN()`或者利用它不等于自己的特点`n != n`。

     * 将其他类型的数值转换为Number有三个函数：`Number()`，`parsInt()`,和`parseFloat()`。三个函数的转换规则不同，常用的为`parsInt()`。

  3. String：用于表示由零个或多个16位unicode字符组成的字符序列，即字符串。
     * 字符串可以由双引号或单引号表示，但是必须要前后对应。
     * 字符串是不可变的，一旦创建，它们的值就不能改变，要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用一个新值填充该变量。
     * 转义字符：反斜线`\`加一个字符即构成转义字符，字符不再表示其原本的含义。例如`\n`代表换行。
     * 有两种方式可以将其他类型的数据转型为String：
       1. `toString()`方法，例如`age.toString();`一般情况下不用传参。
       2. `String()`转型函数。

  4. Undefined：表示变量已经声明，但未初始化。未被初始化的变量会自动被赋值undefined。而当直接使用未被声明的变量时，则会报错。

     * undefined是该类型的唯一成员。

     ```javascript
     var a;
     console.log(a);//undefined
     console.log(b);//Uncaught ReferenceError: a is not defined
     ```

  5. Null：表示空对象指针。null指向了一个空对象，这也从某些角度解释了下面这个bug出现的原理`typeOf null; //object`。

     * null是该类型的唯一成员。

     * 只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存null值。

* 对象类型：除了原始值以外的其他值都是object。对象是属性（property）的结合，属性由键值对组成，值可以为原始值，也可以为对象。

  * 普通对象：普通对象是键值对的无序集合。

  * 特殊对象：

    1. Array —有专用的语法，并且拥有一些和普通对象不同的特有行为特征。

          2. Function —含义有可执行代码，调用函数来运行可执行可执行代码，并返回运算结果。也拥有一些和普通对象不同的特有行为特征。

             * 用来初始化类（class）的函数称为构造函数。

             * 类可以看作是object的子类型。

             * JS定义了三个类：Date（日期），RegExp（正则），Error（错误）。

  * 对象可以转换为原始值。对象继承了两个方法，`toString()`和`valueOf()`。

* JavaScript可以自由地进行数据类型的转换（遵循相应的转换规则）。
* 在实际编程的过程中，可以用`typeof`操作符判断变量的数据类型。