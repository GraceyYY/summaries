## JavaScript对象基础总结

对象可以看做是属性的无序集合，每个属性都是一个名/值对。属性名是字符串，属性的值可以是任意的，例如：字符串，数字，数组，函数等等。因此我们可以把对象看成是从字符串到值的映射。

#### 创建对象的常用方法

1. 对象直接量/字面量表示法

   对象直接量是由若干名/值对组成的映射表，名/值对之间用逗号分隔，整个映射表用花括号括起来。属性名可以是JavaScript标识符也可以是字符串直接量。属性的值可以是任意类型的JavaScript表达式，表达式的值（可以是原始值也可以是对象值）就是这个属性的值。

   ```javascript
   let book = {
       "main title": "JavaScript",
       "sub title": "Object",
       "price": 139,
       author: {
           firstname: "David",
           surname: "Flanagan"
       }
   };
   ```


1. 通过`new`关键字创建对象

   `new`运算符创建并初始化一个新对象。关键字`new`后跟随一个函数调用（构造函数-constructor）。构造函数用以初始化一个新创建的对象。

   ```javascript
   let arr = new Array();
   
   //构造函数Cat
   function Cat(name, age){
       this.name = name;
       this.age = age;
       this.food = ['chicken','beef','tuna'],
       this.greet = function (){
           console.log('meow meow');
       }
   }
   //通过new关键字创建Cat的一个实例对象
   let myCat = new Cat('baozi', 4);
   console.log(myCat); //Cat {name: "baozi", age: 4, food: Array(3), greet: ƒ}
   ```


#### 属性的查询和设置

1. 点表示法：对象的名字表现为一个命名空间，必须写在第一位，然后是一个点，紧接着是你想访问的项目，标识可以是简单属性的名字（name），或数组属性的一个子元素，又或者是对象的方法调用。

   ```javascript
   myCat.name; // 'baozi'
   myCat.greet(); // 'meow meow'
   myCat.food[1]; // 'beef'
   ```


1. 括号表示法：与点表示法类似，只是将属性名字的字符串放在方括号内来查询该属性。

   ```javascript
   book['main title']; //"JavaScript"
   ```


1. 需要修改或创建新属性时，只需使用点表示法/括号表示法写出查询该属性的表达式，并将新的值赋给该表达式即可。

   ```javascript
   book.pages = 1004; //添加新的属性‘pages’，并设置它的值为1004
   book.price = 130; //修改‘price’属性的值为130
   ```


括号表示法的优势在于：

1. 它可以动态地使用函数添加属性

2. 当使用多个单词作为属性名时，只能用`[]`

3. `[]`内可以使用表达式来计算属性名（ES6）


#### 删除属性

`delete`运算符可以删除对象的属性。它的操作数应当是一个属性访问表达式。

`delete`只是断开属性和宿主对象的关系，而不会去操作属性中的属性。

`delete`运算符只能删除自有属性，不能删除继承属性。

```javascript
delete book.price; //返回true，删除成功
```

#### 检测属性

`in`运算符可以用来判断某个属性是否存在于某个对象中。`in`运算符的左侧是属性名（字符串），右侧是对象。如果对象的自由属性或继承属性中包含这个属性则返回`true`。

```javascript
'name' in myCat; //返回true
```

对象的`hasOwnProperty()`方法用来检测给定的名字是否是对象的自有属性。对于继承属性它将返回false。

```javascript
myCat.hasOwnProperty('eat'); //返回false
myCat.hasOwnProperty('food'); //返回true
```

#### 枚举属性

for/in循环可以在循环体中遍历对象中所有可枚举的属性（包括自有属性和继承的属性），把属性名称赋值给循环变量。对象继承的内置方法是不可枚举的，但在代码中给对象添加的属性都是可枚举的。

```javascript
for (let prop in myCat){
    console.log(prop);
}
/*
  返回
name
age
food
greet
*/
```

