### javaScript基础书籍 
- JavaScript高级程序设计
- ES6标准
    + es6.ruanyifeng.com
- JavaScript权威指南
- 你不知道的JavaScript
    + 上、中、下
    + JavaScript底层知识
### JavaScript错误
- SyntaxError：语法错误 
> 对象代表尝试解析语法上不合法的代码的错误

- TypeError（类型错误） 
> 对象用来表示值的类型非预期类型时发生的错误。

### 浏览器内核
- webkit内核（V8引擎）
    + 谷歌Chrome
    + Safari
    + Opera >=V14
    + 国产浏览器
    + 手机浏览器
    + ...
- Gecko
    + 火狐Firefox
- Presto
    + Opera <v14
- Trisent
    + IE
    + IE EDGE开始采用双内内核（包括chrome迷你）

### JS做客户的一样
>按照相关的JS语法，去操作页面中的元素，有时还要操作浏览器里面的功能。
- ECMAScript3/5/6...
    + JS语法规范(遍量、数据类型、操作语句得等)
- DOM（ document object model ）：用来操作页面中的DOM元素
    + 文档对象模型，提供一些JS的属性和方法，用来操作页面中的DOM元素
- BOM（ browser opject model ）：用来操作浏览器
    + 浏览器对象模型，提供一些JS的属性和方法，用来操作浏览器
### JS中的变量 variable
- 变量：可变的量，在编程语言中，变量就是一个名字，原来存储和代表不同的枝
- 创建变量方式：var/let/const/function/import/class 

```
    //ES3
    var a=12;//创建一个变量a，并赋值12
    console.log(a);//输出变量a

    //ES6创建变量的方法
    let b=100;//创建一个变量b
    const c=1000//创建一个变量c，const创建的变量值不能修改（可以理解为常量）


    //创建函数也相当于创建变量
    function fn(){}
    //创建类也相当于创建变量
    class A{}
    //ES6的模块导入也相当于创建变量
    import B from './B.js';
    //Symbol创建唯一值(没有一个值会和它相等)
    Symbol C=100;
    let n=Symbol(100);
    let m=Symbol(100);
    n==m;-->false;

```
### JS中的命名规范
> 注意命名规范：区分大小写/驼峰法/关键字保留字
- 严格区分大小写
```
let Test=100;
console.log(test); //=>无法输出 Test≠test 

```

- 使用数字、字母、下划线、$,数字不能开头
```
let $box;//=>一般用JQ获取的用$开头
let _box;//=>一般公共变量都是_开头（全局变量）

```
- 驼峰法
>首字母小写，其余每一个有意义字母的首字母都要大写（密码尽可能明显，使用英问单词）
```
let studentInformation;
let studentInfo;
//常用的缩写：add /insert/create/new、update、delete/del/remove/rm(删除)、sel/select/query/get（查询）、info(信息)...
```
###  数据类型
- 基本数据类型
    + 数字number 
        > 常规数字和NaN0

    + 字符串string 
        > 所有用单引号、双引号、反引号（撇 ES6模板字符串）包起来的字符串 

    + 布尔boolean 
    + null(对象空指针) 
    + undefined(未定义)
- 引用类型
    + objcet对象数据类型
        + {} 普通对象 
        + [] 数组对象 
        + /^[+-]?(\d|([1-9]\d))(\.\d)?$/ 正则对象 
        + Math 数学对象
        + 日期对象
        + ...
    + 函数数据类型 function、Symbol（唯一值）
### NaN
- not a number：不是一个数字 
    + NaN和任何值（包括自己）都不相等：即NaN!=NaN 
```
 console.log('AA' == NaN); //输出 => false
 console.log(10 == NaN); //输出 => false
 console.log(NaN == NaN); //输出 => false 
```

### isNaN
- 检测一个值是否为有效数字,如果不是有效数字返回true,反值是有效数字返回false（不是数字true，是数字false）
    + isNaN检测机制：首先会检测值是否位数字类型,如果不是,先基于Number()这个方法,把值转换为数字,然后再检查
```
console.log(isNaN(10)); //=>false 
console.log(isNaN('AA')); //=>true 

console.log(isNaN('10')); //=>false 
    //检测机制
    1)Number('10'); => 10 
    2)isNaN(10);   =>false

```

### 数字number
> 常规数字和NaN

### 把其他类型值转换为数字类型，即底层机制
- Number(val) //val转换为数字类型`·浏览器内置对象`
    + 字符串转换数字规律
    > 把字符串转换为数字,只要有任意一个非有效数字字符（第一个点除外）经过都是NaN,空字符串会变为零`V8引擎底层机制` 
    
    + 布尔换位数字规律
    >  true-->1, false-->0

    + 引用数据类型转换数字规律
    >先基于toString方法转换为字符串，然后转换数字 

============`Number`============
> 浏览器内置对象`V8引擎底层机制`
```
//字符串转换位数字
console.log(Number('12.5')); //=>12.5 
console.log(Number('12.5px')); //=>NaN 
console.log(Number('12.5.5')); //=>NaN 
console.log(Number('')); //=>0 

//布尔换位数字
console.log(Number(true)); //=>1 
console.log(Number(false)); //=>0 
console.log(isNaN(false)); //=>false 
console.log(isNaN(treu)); //=>false 

// null对象空指针、undefined(未定义) null->0 undefined->NaN
console.log(isNaN(null)); //=>0 
console.log(isNaN(undefined)); //=>NaN 

//引用数据类型转换数字

console.log(Number({name:'10'})); //=>NaN 
console.log(Number({})); //=>NaN 
    1) ({}).toString(); // =>""
    2) Number(""); //=>0 
console.log(Number([])); //=>0 
console.log(Number([12])); //=>12 
    1) ([12]).toString(); // =>"12"
    2) Number("12"); //=>12 
console.log(Number([12,23])); //=>NaN 
    1) ([12]).toString(); // =>"12,23"
    2) Number("12,23"); //=>NaN 

```
- parseInt/parseFloat([val],[进制]) //val转换为数字类型`处理字符串` 
    > 从`左到右查`找有效数字直到遇到非有效字符,停止查找（不管后面是否还有数字,都不在找）

============`parseInt/parseFloat`============
```
let str='12.5px'; 
console.log(Number(str)); //=>NaN 
console.log(parseInt(str)); //=>12 
console.log(parseFloat(str)); //=>12.5 
console.log(parseFloat('width:12.5px')); //=>NaN 
console.log(parseFloat(true)); //=>NaN 
    1)console.log(parseFloat('true'));

```


- == 进行比较的时候，可能要出现把其他类型值转换为数字 

### string字符串数据类型
> 所有用`单引号、双引号、反引号（撇 ES6模板字符串）`包起来的字符串 

- val.toString() 
> 注意：null和undefinde是`禁止直接toString`的，但是null和undefinde转换成字符串结果是`'null','undefinde'`。不能调用toString,`直接加`单引号或双引号
```
let a = 12; 
console.log(a.tostring()); //=>'12' 
console.log((NaN).tostring()); //=>'NaN' 
console.log((true).tostring()); //=>'true' 
console.log((null).tostring()); //=> TypeError 
console.log((undefinde).tostring()); //=> TypeError  
//数组[]
console.log(([]).tostring()); //=>'' 
console.log(([12]).tostring()); //=>'12' 
console.log(([12,23]).tostring()); //=>'12,23' 
// 正则对象 
console.log((/^[+-]?(\d|([1-9]\d))(\.\d)?$/).tostring()); //=>'/^[+-]?(\d|([1-9]\d))(\.\d)?$/' 
//{} 普通对象 
console.log(({name:'xxxx'}).tostring()); //=>"[object Object]" 
//因为=> Object.prototype.toString方法不是转换为字符串的，而是用来检测数据类型的 


```


- 字符串拼接 
> 凡是遇到字符串直接拼接 























### ES6基础语法 
+ let 定义变量 
    > 有块级作用域

+ 对象的增强语法

### javaScript高阶函数 
+ ES6 for循环
```
    //1.普通for循环
    for(let i = 0; i<=this.books ;i++){
        ......
    }
    //2. for(let i in this.books)
    for(let item in this.books){
        ......
    }
    ///3.for(let i in of this.books)
    for(let item in of this.books){
        item.price * item.count
    }

```
+ 高阶函数`filter、map、reduce`
    > 知识 编程范式：命令编程/声明编程<br/>
      编程范式: 面向对象编程（第一公民：对象）/ 函数式编程（第一公民：函数）

```
    //需求输出小于100的数，将小于100的数乘以2，输出汇总数

    //过滤  filter中的回调函数有一个要求：必须返回一个boolean
    //返回true：函数内部会自动将这次回调的n加入到新的数组中
    //返回false：函数会过滤这次的n
    //1.输出小于100的数
    const nums = {10,20,111,222,444,40,50}
    //遍历nums数组 n 是nums数组的每一项
    let newNums = nums.filter(function(n){//回调函数 n
        return n < 100
    });
    //2.将小于100的数乘以2
    //map函数的使用
    let new2Nums = newNums.map(function(n){
        return n*2;
    });
    //3.输出汇总数
    //reduce函数的使用 等数组的所有内容汇总 
    //new2Nums.reduce(参数一,参数二);
    let total = new2Nums.reduce(function(preValue,n){
        return preValue+n;//返回new2Nums数组的和
    },0);
    // 第一次遍历：preValue 为0 ,与参数二有关；n 为数组的第一个值
    // 第二次遍历：preValue 为 第一次遍历return的值； n 为数组的第二个值
    //......



    //filter、map、reduce 结合使用  (函数式编程)
    //输出小于100的数，将小于100的数乘以2，输出汇总数
    let newNums = nums.filter(function(n){//回调函数 n
        return n < 100
    }).map(function(n){
        return n*2;
    }).reduce(function(preValue,n){
        return preValue+n;//返回new2Nums数组的和
    },0);
    // === > 改为箭头函数 
    let newNums = nums.filter(n => n < 100>).map(n => n * 2).reduce((pre, n) => pre + n);

```