# less
##### 先看css：
###### css是一门历史悠久的标识语言，与HTML一起.被广泛应用于Web应用和设计开发中。HTML主要负责文档结构的定义，CSS负责文档表现样式的定义。作为一门标识语言，CSS语法相对简单，对使用者的要求较低，但同时也带来一些问题:CSS需要书写大量看似没有逻辑的代码.不方便维护及扩展，不利于重用.非前端开发人员，往往会因为缺少CSS编写经验而很难写出组织良好且易于维护的CSS代码。造成这些困难的很大原因源于CSS是一门非程序设计语言，没有变量、函数、作用域等概念。

##### LESS具有以下明显的优点:

######     (1).需要编写的代码量明显变少了。
######     (2).CSS管理更加容易了.在需要更换网站样式风格时尤其如此,此时如果直接重写这些样式，工作量将非常浩大，但是用LESS就很简单,改个全局配置就可以了。
######     (3).LESS学习成本不是很高，与CSS规则完全融合，如果用户熟悉CSS的话，那么只需要简单的学习，就能够快速驾驭LESS,
######     (4).使用LESS实现配色变得非常容易。在传统设计中，用户需要借助配色工具或者图像编辑软件来实现色彩的搭配.不但效果不是很理想，而且还需要投人很大的精力。例如,在设计的时候,常常需要反复试验哪种颜色比较适合。虽然知道主色调要用原色，但是根据设计意图，可能需要深一点、浅一点、亮一点、暗一点，或者再带一点黄色,再带一点棕色,如此等等。如果每试一次都要改全套的样式，那么这个工作量是非常大的，而且也不能够精确址化。现在，利用LESS的变址，结合颜色函数，所有配色问题就变得容易多了。在网站改版中也是如此。
######     (5).兼容 CSS3。很多CSS3语法目前还需要为各个浏览器写特别的语法，如圆角、盒子阴影、变形、过渡等，如果把这些代码使用LESS先封装起来，使用时就会省事很多。
######     (6).与CSS能够很好地融合使用。在LESS代码中可以融人CSS代码，在CSS代码中可以插人LESS语法。因此，对于用户来说,有了LESS,同样还需要继续学习CSS,还是需要会写CSS, LESS只是帮我们省下一些工夫，大部分样式还是要知道CSS是如何实现的,否则就不知道如何把LESS编译成为CSS.
    
Less类似于Jquery
LESS是一种动态样式语言，属于CSS预处理语言的一种，它使用类似CSS的语法，为CSS的赋予了动态语言的特性，如变量、继承、运算、函数等，更方便CSS的编写和维护。
LESSCSS可以在多种语言、环境中使用，包括浏览器端、桌面客户端、服务端。

#####    本质上，LESS 包含一套自定义的语法及一个解析器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的 CSS 文件。LESS 并没有裁剪 CSS 原有的特性，更不是用来取代 CSS 的，而是在现有 CSS 语法的基础上，为 CSS 加入程序式语言的特性。


##### 1.注释：
###### //形式不会被编译到css
###### /**/会被编译到css
# 一、初识less
传统写法：

    .conten ul{
        list-style: none;
    }
    .conten li{
        height: 25px;
        line-height: 25px;
    }
    .conten li a{
        text-decoration: none;
        color: #535353;
    }
    
less的写法如下：

    .conten {
        ul{
            list-style: none;
        }
        li{
            height: 25px;
            line-height: 25px;
            a{
                text-decoration: none;
                color: #535353;
            }
        }
    }

# 二、使用

###### less不能直接被使用，需要转化为css
###### a、koala,用工具将less转化为css文件，再引用
###### b、link直接引入，再引入less.min.js
    <link rel="stylesheet/less" href="style.less"/> 
    <script src="less.min.js"></script>
    读取出less文件的内容，语法分析处理成css，插入style标签注入到页面上。
    （vue中使用less：下载对应less、less-loader <style lang="less"></style>）
    
# 三、变量
定义多个相同名字的变量，会使用向上寻找最近作用域的变量

    @green: #801f77;
    @baise:white;
    header,footer{
      background: @green;
      h1{
        color: @baise;
      }
    }
    //作为选择器和属性名的变量
    @kuandu:width;
    .@{kuandu}{
      @{kuandu}:150px
    }
    //作为URL的变量
    @imgurl:"https://img.yaolaivip.com/";
    header{
      background: @green url("@{imgurl}logo.png");
      height: 500px;
    }

# 四、混合minxin
将一个混合集引入到另一个混合集

    //基本混合 （.font_hn输出到样式中）
    .font_hn{
      color: red;
    }
    h1{
      font-size: 28px;
      .font_hn;
    }
    h2{
      font-size: 24px;
      .font_hn;
    }
    //不带输出的混合，类名后面使用() （.font_hn不会输出到样式中）
    .font_hn(){
      color: red;
    }
    h1{
      font-size: 28px;
      .font_hn;
    }
    h2{
      font-size: 24px;
      .font_hn;
    }
    //带选择器的混合
    .my-hover-mixin {
      &:hover {
        border: 1px solid red;
      }
    }
    button {
      .my-hover-mixin;
    }
    h1{
      .my-hover-mixin;
    }
    //带参数的混合
    .border(@color){
      border: 1px solid @color;
    }
    h1{
      &:hover{
        .border(green);
      }
    }
    //带参数并且有默认值的混合
    .border_you(@color:red){
      border: 1px solid @color;
    }
    h1{
      &:hover{
        .border_you();
      }
    }
    h2{
      &:hover{
        .border_you(yellow);
      }
    }
    //带多个参数的混合
    .mixin(@color; @padding:xxx; @margin: 2) {
      color: @color;
      padding: @padding;
      margin: @margin @margin @margin @margin;
    }
    .div01 {
     .mixin(1,2,3;something, ele;132);//;为分隔符
    }
    .div02 {
     .mixin(1,2,3);//，为分隔符
    }
    //如果传参的括号里面全部都是以“，”分割，那么会依次传给各个参数值，
    //如果传参的括号里面既有“，”又有“；”那么，会把“；”前面的看作一个整体，传给一个参数值
    
    
    /*定义多个具有相同名称和参数数量的混合*/
    .mixin(@color) {
        color-1: @color;
    }
    .mixin(@color; @padding:2) {
        color-2: @color;
        padding-2: @padding;
    }
    .mixin(@color; @padding; @margin: 2) {
        color-3: @color;
        padding-3: @padding;
        margin: @margin @margin @margin @margin;
    }
    .some .selector div {
        .mixin(#008000);
    }
    <!--生成结果-->
    .some .selector div {
        color-1: #008000;
        color-2: #008000;
        padding-2: 2;
    }
    <!--传两个参数-->
    .some .selector div {
        .mixin(#008000,3);
    }
    <!--生成结果-->
    .some .selector div {
        color-2: #008000;
        padding-2: 3;
        color-3: #008000;
        padding-3: 3;
        margin: 2 2 2 2;
    }
    
    /*命名参数*/
    .mixin(@color: black; @margin: 10px; @padding: 20px) {
        color: @color;
        margin: @margin;
        padding: @padding;
    }
    .class{
       .mixin(@padding: 80px;)
    }
    <!---->
    .class {
        color: #000000;
        margin: 10px;
        padding: 80px;
    }
    
    /*@arguments;*/
    .border(@x:solid,@c:red){
        border: 21px @arguments;
    }
    .div1{
        .border(solid);
    }
    
    /*匹配模式*/
    .border(t_l,@w:5px){
        border-top-left-radius: @w;
    }
    .border(b-r,@w:5px){
        border-bottom-right-radius: @w;
    }
    footer{
        .border(t_l,10px);
        .border(b-r,10px);
        background: #33acfe;
    }
    
    //混合的返回值
    .average(@x, @y) {
        @average: ((@x + @y) / 2);
        @he:(@x + @y);
    }
    div {
        .average(16px, 50px);
        padding: @average;
        margin: @he;
    }
    <!--编译后-->
    div {
        padding: 33px;
        margin: 66px;
    }
    
# 五、嵌套规则(nested-rules)
    /*&写在前边表示所有父元素，&后没有空格的话，则表示同时有几个类*/
    .a{
      .b{
        & .c{
          color: 123;
        }
      }
    }
    <!--编译后-->
    .a .b .c {
        color: 123;
    }
    /*&写在后边则表示之前所有的父元素放在它的后边*/
    .a{
      .b{
        .c &{
          color: 123;
        }
      }
    }
    <!--编译后-->
    .c .a .b {
        color: 123;
    }
    /*多个&则会生生多种组合*/
    p, a, ul, li {
        border-top: 2px dotted #366;
        &   & {
            border-top: 0;
        }
    }
    <!--编译后-->
    p,
    a,
    ul,
    li {
      border-top: 2px dotted #366;
    }
    p p,
    p a,
    p ul,
    p li,
    a p,
    a a,
    a ul,
    a li,
    ul p,
    ul a,
    ul ul,
    ul li,
    li p,
    li a,
    li ul,
    li li {
      border-top: 0;
    }
# 六、运算(operations)
任何数值、颜色都可以计算，less会自动推断计算值的单位，运算符和数值之间需以空格隔开，涉及优先级时用（）括起来

    //涉及到优先级，使用()区分优先级
    .wp{
      margin: 0 auto;
      width: (550 - 50)*2 + 24px;
      height: 400 + 400px;
      color: #ff0000 - 55;
      background:#ff0000 + 355;
    }
    //颜色运算（不能使用颜色的英文名称），less会先将其转化为rgb模式，运算完再换为16进制的颜色值再返回。rgb模式他的值是 0~255 ，当你的值超过255 ，那么就会以255进行相加操作
    .wp {
      margin: 0 auto;
      width: 1024px;
      height: 800px;
      color: #c80000;
      background: #ffffff;
    }
# 七、函数(functions)
less提供了很多用于转换颜色、处理字符串和进行算术运算的函数
a、常见的rgb（）函数，将rgb转换为16进制的值
b、提取蓝色值blue（）函数

    .wp {
      background: rgb(1,21,1);
      font-size: blue(#129030);
      z-index: red(#050516);
    }
    <!--编译为-->
    .wp {
      background: #011501;
      font-size: 48;
      z-index: 5;
    }
# 八、命名空间
    /*写法1：*/
    #bgcolor(){
      background: #ffffff;
      .a{
        color: #888888;
        &:hover{
          color: #ff6600;
        }
        .b{
          background: #ff0000;
        }
      }
    }
    .wi{
      background: green;
      color: #fff;
      .a{
        color: green;
        background: #ffffff;
      }
    }
    .bgcolor1{
      background: #fdfee0;
      #bgcolor>.a;
    }
    .bgcolor2{
      .wi>.a;
    }
    //省略> 写法2：
    #bgcolor(){
      background: #ffffff;
      .a{
        color: #888888;
        &:hover{
          color: #ff6600;
        }
        .b{
          background: #ff0000;
        }
      }
    }
    .wi {
      background: green;
      color: #fff;
      .a {
        color: green;
        background: #ffffff;
      }
    }
    .bgcolor1{
      background: #fdfee0;
      #bgcolor .a;
    }
    .bgcolor2{
      .wi .a;
    }
    <!--编译后-->
    .wi {
      background: green;
      color: #fff;
    }
    .wi .a {
      color: green;
      background: #ffffff;
    }
    .bgcolor1 {
      background: #fdfee0;
      color: #888888;
    }
    .bgcolor1:hover {
      color: #ff6600;
    }
    .bgcolor1 .b {
      background: #ff0000;
    }
    .bgcolor2 {
      color: green;
      background: #ffffff;
    }
# 九、作用域
作用域：基本与javascript的作用域相似，即先找局部变量，后找全局变量。找变量时遵循就近原则。

    @clolor:#ffffff;
    .bgcolor{
      width: 50px;
      @clolor:blue;//此句不写则编译为color: #ff0000;加上此后为color: #0000ff;
      a{
        color: @clolor;
      }
    }
    @clolor:#ff0000;
    
# 十、引入(importing)
    只有引入less文件，里边的变量才能被使用
    
    main.less：
    
    @wp:960px;
    .colorsss{
      color: darkgreen;
    }
    
    style.less:
    @import "main.less";
    @import (reference) "main.less";  //引用LESS文件，但是不输出（main.less里的样式不输出到样式中）
    @import (inline) "main.less";  //原样引用LESS文件，但是不进行操作
    @import (once) "main.less";  //引用一次LESS文件
    @import (less) "index.css";  //无论是什么格式的文件，都把他作为LESS文件操作
    @import (css) "main.less";  //无论是什么格式的文件，都把他作为CSS文件操作
    @import (multiple) "main.less";  //multiple，允许引入多次相同文件名的文件
    .centen{
      width:@wp;
      .colorsss;
    }
#   11、关键字(important)
在调用混合机后面追加！important关键字，可以是混合集里面的所有属性都继承！important

    .foo (@bg: #f5f5f5, @color: #900) {
      background: @bg;
      color: @color;
      font-size: 16px;
      font-weight: 900;
    }
    .unimportant {
      .foo();
    }
    .important {
      .foo() !important;
    }
    <!--编译后-->
    .unimportant {
      background: #f5f5f5;
      color: #990000;
      font-size: 16px;
      font-weight: 900;
    }
    .important {
      background: #f5f5f5 !important;
      color: #990000 !important;
      font-size: 16px !important;
      font-weight: 900 !important;
    }
    
# 十二、条件表达式

    .mixin (@a) when (lightness(@a) >= 50%) {   //255/2=127.5
      background-color: black;
    }
    .mixin (@a) when (lightness(@a) < 50%) {
      background-color: white;
    }
    .class1 { .mixin(#7e7e7e) }  //221  > 127.5  >50%  background-color: black;  7e7e7e  =  126
    .class2 { .mixin(#808080) }  //85 <127.5  <50%   background-color: white;  808080 = 128
    
    /*iscolor,isnumber.....判断值的类型*/
    
    .mixin (@a) when (iscolor(@a)) {  
      background-color: black;
    }
    .mixin (@a) when (isnumber(@a) ) {
      background-color: white;
    }
    .class1 { .mixin(#7e7e7e) }  //background-color: black;
    .class2 { .mixin(123) }  //background-color: white;
    
    /*ispixel,ispercentage.....单位检查函数*/
    .mixin (@a) when (ispixel(@a)) {
      background-color: black;
    }
    .mixin (@a) when (ispercentage(@a) ) {
      background-color: white;
    }
    .mixin (@a) {
      width: @a;
    }
    .class1 { .mixin(960px) }  //background-color: black; width:960px
    .class2 { .mixin(95%) }  //background-color: white;width:95%
    
# 十三、循环(loop)

    .loop(@counter) when (@counter < 7) {
      h@{counter}{
        padding: (10px * @counter);
      }// 每次调用时产生的样式代码
      .loop((@counter + 1));    // 递归调用自身
    }
    div {
      .loop(1); // 调用循环
    }
    <!--编译后-->
    div h1 {
      padding: 10px;
    }
    div h2 {
      padding: 20px;
    }
    div h3 {
      padding: 30px;
    }
    div h4 {
      padding: 40px;
    }
    div h5 {
      padding: 50px;
    }
    div h6 {
      padding: 60px;
    }
    
# 十四、合并属性

    //+ 合并以后，以逗号分割属性值
    .mixin() {
      box-shadow+: inset 0 0 10px #555 ;
    }
    .myclass {
      .mixin();
      box-shadow+: 0 0 20px black;
    }
    <!--编译后-->
    .myclass {
      box-shadow: inset 0 0 10px #555 , 0 0 20px black;
    }
    
    //+_ 合并以后，以空格分割属性值
    .a(){
      background+:#f60;
      background+_:url("/sss.jod") ;
      background+:no-repeat;
      background+_:center;
    }
    .myclass {
      .a()
    }
    <!--编译后-->
    .myclass {
      background: #f60 url("/sss.jod"), no-repeat center;
    }
    
# 十五、函数库
    
###     1、其他函数
    /*color()函数:解析颜色，将代表颜色的字符串转换为颜色值*/
    background: color("#f60");
    background: #ff6600;//编译后
    
    /*convert()函数：将数字从一种类型转换为另一种类型（m,cm,mm,in,pt,px,pc）(s,ms)(rad：弧度,grad.turn:园,deg)*/
    width: convert(1s,ms);
    width: 1000ms;//编译后
    width: convert(20cm,px);
    width: 755.90551181px;//编译后
    
    /*data-uri()函数:将一个资源使用BASE64编码嵌入到样式文件，如果开启了ieCompat选项，而且资源文件的体积过大或者是在浏览器中使用，则会使用url()进行回退。如果没有指定MIME，则Node.js会使用MIME包来决定正确的MIME*/
    background: data-uri('arr.jpg');
    <!--编译后会变成base64的格式-->
    
    /*default()函数：（只能边界条件使用，没有匹配到其他自定义函数时返回true）没有一个条件满足时显示该样式、not(default())只要有一个条件满足时就会显示该样式*/
    /*ispixel()函数：是像素则返回true*/
    .x(@x) when (ispixel(@x)) {width:@x}
    .x(@x) when not(default()) {padding:(@x/10)}
    .div1{
     .x(100px)
    }
    .div2{
     .x(100cm);
     color:red;
    }
    <!--编译后-->
    .div1 {
      width: 100px;
      padding: 10px;
    }
    .div2 {
      color: red;
    }
    
    .x(@x) when (ispixel(@x)) {width:@x}
    .x(@x) when (default()) {background:(@x/10)}
    .div1{
     .x(100px)
    }
    .div2{
     .x(100cm);
     color:red;
    }
    <!--编译后-->
    .div1 {
      width: 100px;
    }
    .div2 {
      background: 10cm;
      color: red;
    }
    
    /*unit()函数：移除或更改单位(如果省略则移除原单位)*/
    width: unit(100px);
    width: 100;//编译后
    width: unit(100px,cm);
    width: 100cm;//编译后
    
    
###     2、 函数库 - 字符串函数和长度相关函数
    /*escape()函数：将输入字符串的url特殊字符进行编码处理。会转义的：#, ^, (, ), {, }, |, :, >, <, ;, ], [ , =；不会转义的：, / / / ? / @ / & / + / ' / ~ / ! / $*/
    d:escape('#, ^, (, ), {, }, |, :, >, <, ;, ], [ , =');
    d: %23,%20%5E,%20%28,%20%29,%20%7B,%20%7D,%20%7C,%20%3A,%20%3E,%20%3C,%20%3B,%20%5D,%20%5B%20,%20%3D;//‘，’原样输出，空格转为‘%20’
    /*e()函数：用于对CSS的转义，与~"value"类似。它接受一个字符串作为参数，并原样返回内容（不含引号）。它可用于输出一些不合法的CSS语法，或者是使用LESS不能识别的属性。*/
    filter: e("ms:alwaysHasItsOwnSyntax.For.Stuff()");
    filter: ~"ms:alwaysHasItsOwnSyntax.For.Stuff()";
    <!--编译后-->
    filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
    
    width: calc(960px-100px);
    width: calc(~'960px-100px');//需要由浏览器自己计算
    <!--编译后-->
    width: calc(860px);
    width: calc(960px-100px);
    
    /*%()函数：格式化字符串。%("format", arguments ...)将会格式化字符串。第一个参数是一个包含占位符的字符串。占位符以百分号%开头，后面接字母s / S / d / D / a / A。后续的参数用于替换这些占位符。如果你需要输出百分号，可以多用一个百分号来转义%%。*/
    使用大写的占位符可以将特殊字符按照UTF-8进行转义，函数将会对所有的特殊字符进行转义，除了( / ) / ' /~ /!。空格会被转义为%20。小写的占位符将原样保持特殊字符，不进行转义。

    占位符说明：d / D / a / A 可以被任意类型的参数替换（颜色、数字、转义的字符串、表达式等）。如果将它们和字符串一起使用，则整个字符串都会被使用，包含引号。但是，引号将会原样放在字符串中，不会被转义。s / S 可以被除了颜色的之外的任何类型参数替换。如果你将它们和字符串一起使用，则只有字符串的值会被使用，引号会被忽略。
    
    参数：
    
    字符串：带有占位符的格式化字符串
    任意值：用于替换占位符的值
    返回值：格式化后的字符串
    
    例如：

    使用a/d格式化：%("repetitions: %a file: %d", 1 + 2, "directory/file.less");
    使用大写的a/d格式化：%('repetitions: %A file: %D', 1 + 2, "directory/file.less");
    使用s格式化：%("repetitions: %s file: %s", 1 + 2, "directory/file.less");
    使用大写s格式化：%('repetitions: %S file: %S', 1 + 2, "directory/file.less");
    分别输出如下：
    
    使用a/d格式化："repetitions: 3 file: "directory/file.less"";
    使用大写的a/d格式化："repetitions: 3 file: %22directory%2Ffile.less%22";
    使用s格式化："repetitions: 3 file: directory/file.less";
    使用大写s格式化："repetitions: 3 file: directory%2Ffile.less";
    
    /*color(@string)解析颜色，将代表颜色的字符串转换为颜色值，参数必须是16进制表示的颜色或者缩写写法。*/
    参数:
    
    @字符串：代表颜色值的字符串
    例如：
    
    color("#445566")
    color(~"#123")
    输出：
    
    #445566
    #112233
    
    /*ceil()函数:向上取整*/
    ceil(2.4)
    3
    
    /*floor()函数:向下取整*/
    floor(2.4)
    2
    
    /*percentage()函数:将浮点数转换为百分比字符串*/
    percentage(0.5)
    50%
    
    /*round()函数:四舍五入取整*/
    参数:

    数字：浮点数
    小数位数：数字，可选，四舍五入取整的小数点位置，默认值为0。
    round(0.5)
    1
    round(1.67, 1)
    1.7
    
    /*sqrt()函数:计算一个数的平方根，原样保持单位*/
    sqrt(25cm)
    5cm
    sqrt(18.6%)
    4.312771730569565%;
    
    /*abs()函数:计算数字的绝对值，原样保持单位*/
    abs(25cm)
    25cm
    abs(-18.6%)
    18.6%
    
    /*sin()函数:正弦函数，处理时会将没有单位的数字认为是弧度值位*/
    sin(1); // 1弧度角的正弦值
    sin(1deg); // 1角度角的正弦值
    sin(1grad); // 1百分度角的正弦值(百分度是将一个圆周分为400份，每份为一个百分度，英文gradian，简写grad。)
    分别输出：
    0.8414709848078965;
    0.01745240643728351;
    0.015707317311820675;
    
    /*asin()函数:反正弦函数，返回以弧度为单位的角度，区间在 -PI/2 到 PI/2之间*/
    asin(-0.8414709848078965)
    asin(0)
    asin(2)
    分别输出：
    -1rad
    0rad
    NaNrad
    
    /*cos()函数:余弦函数，处理时会将没有单位的数字认为是弧度值。*/
    参数：
    数字：浮点数，角度
    返回值：数字，角度对应的余弦值
    例如：
    cos(1); // 1弧度角的余弦值
    cos(1deg); // 1角度角的余弦值
    cos(1grad); // 1百分度角的余弦值
    分别输出：
    0.5403023058681398
    0.9998476951563913
    0.9998766324816606
    
    /*acos()函数:反余弦函数，返回以弧度为单位的角度，区间在 0 到 PI之间。*/
    参数：
    数字：浮点数，代表余弦值，范围为 [-1,1]
    返回值：数字，角度
    例如：
    acos(0.5403023058681398)
    acos(1) 
    acos(2)
    分别输出：
    1rad
    0rad
    NaNrad
    
    /*tan()函数:正切函数，处理时会将没有单位的数字认为是弧度值。*/
    参数：
    数字：浮点数，角度
    返回值：数字，角度对应的正切值
    例如：
    sin(1); // 1弧度角的正切值
    sin(1deg); // 1角度角的正切值
    sin(1grad); // 1百分度角的正切值
    分别输出：
    1.5574077246549023
    0.017455064928217585
    0.015709255323664916
    
    /*atan()函数:反正切函数，返回以弧度为单位的角度，区间在 -PI/2 到 PI/2之间。*/
    参数：
    数字：浮点数，代表正切值
    返回值：数字，角度
    例如：
    atan(-1.5574077246549023)
    atan(0)
    round(atan(22), 6) // 四舍五入输出6位小数
    分别输出：
    -1rad
    0rad
    1.525373rad;
    
    /*pow()函数:返回圆周率PI。*/
    参数：无
    返回值：数字，圆周率
    例如：
    pi()
    输出：
    3.141592653589793
    
    /*pi()函数:假设第一个参数为A，第二个参数为B，返回A的B次方。返回值与A有相同的单位，B的单位被忽略。*/
    参数：
    数字：浮点数，基数
    数字：浮点数，冪指数
    返回值：数字，基数的冪指数次方
    例如：
    pow(0cm, 0px)
    pow(25, -2)
    pow(25, 0.5)
    pow(-25, 0.5)
    pow(-25%, -0.5)
    输出：
    1cm
    0.0016
    5
    NaN
    NaN%
    
    /*mod()函数:返回第一个参数对第二参数取余的结果。返回值与第一个参数单位相同，第二个参数单位被忽略。这个函数也可以处理负数和浮点数。*/
    参数：
    数字：浮点数
    数字：浮点数
    返回值：数字，取余的结果
    例如：
    mod(0cm, 0px)
    mod(11cm, 6px);
    mod(-26%, -5);
    输出：
    NaNcm;
    5cm
    -1%;
    
    
    /*convert()函数:将数字从一种类型转换到另一种类型。第一个参数为带单位的数值，第二个参数为单位。如果两个参数的单位是兼容的，则数字的单位被转换。如果两个参数的单位不兼容，则原样返回第一个参数*/
    兼容的单位组：
    长度：m / cm / mm / in / pt / pc
    时间：s / ms
    角度：rad / deg / grad / turn//(grad为“百分度”，见正弦函数下的说明。turn为“圈/周”的意思，1turn为360度。)
    参数：
    数字：带单位的数值，浮点数
    单位
    返回值：转换单位后的数值
    例如：
    convert(9s, "ms")
    convert(14cm, mm)
    convert(8, mm) // 不兼容的单位
    输出：
    9000ms
    140mm
    8
    
    /*Unit()函数:返回带不同单位的数值。只有单位被改变，数值本身不会被转换。函数会假设第二个参数带上了合法单位。*/
    参数：
    数字：带单位的浮点数
    单位
    返回值：带单位的数值
    例如：
    unit(9s, ~"ms")
    unit(-9, m)
    输出：
    9ms
    -9m
    
    /*rgb(@r, @g, @b)函数:通过十进制红色，绿色，蓝色三种值 (RGB) 创建不透明的颜色对象。在 HTML/CSS 中也会用文本颜色值 (literal color values) 定义颜色，例如 red -> #ff0000。*/
    参数:
    @red: 整数 0-255 或百分比 0-100%
    @green: 整数 0-255 或百分比 0-100%
    @blue: 整数 0-255 或百分比 0-100%
    返回值：颜色 (color)
    例如：
    rgb(90, 129, 32)
    输出：
    #5a8120
    
    /*rgba(@r, @g, @b, @a)函数:通过十进制红色，绿色，蓝色，以及 alpha 四种值 (RGBA) 创建带alpha透明的颜色对象。*/
    参数:
    @red: 整数 0-255 或百分比 0-100%
    @green: 整数 0-255 或百分比 0-100%
    @blue: 整数 0-255 或百分比 0-100%
    @alpha: 数字 0-1 或百分比 0-100%
    返回值：颜色 (color)
    例如：
    rgba(90, 129, 32, 0.5)
    输出：
    rgba(90, 129, 32, 0.5)
    
    /*argb(@color)函数:创建格式为 #AARRGGBB 的十六进制 (hex representation) 颜色 (注意不是 #RRGGBBAA！)。这种格式被用在IE滤镜中，以及.NET和Android开发中。*/
    参数:
    @color: 颜色对象 (A color object.)
    返回值：字符串 (string)
    例如：
    argb(rgba(90, 23, 148, 0.5));
    输出：
    #805a1794
    
    /*hsl(@hue, @saturation, @lightness)函数:通过色相 (hue)，饱和度 (saturation)，亮度 (lightness) 三种值 (HSL) 创建不透明的颜色对象。*/
    参数:
    @hue: 整数 0-360 表示度数。
    @saturation: 百分比 0-100% 或数字 0-1
    @lightness: 百分比 0-100% 或数字 0-1
    返回值：颜色 (color)
    例如：
    hsl(90, 100%, 50%)
    输出：
    #80ff00
    
    /*hsla(@hue, @saturation, @lightness, @alpha)函数:通过色相 (hue)，饱和度 (saturation)，亮度 (lightness)，以及 alpha 四种值 (HSLA) 创建透明的颜色对象。*/
    参数:
    @hue: 整数 0-360 表示度数
    @saturation: 百分比 0-100% 或数字 0-1
    @lightness: 百分比 0-100% 或数字 0-1
    @alpha: 百分比 0-100% 或数字 0-1
    返回值：颜色 (color)
    例如：
    hsl(90, 100%, 50%, 0.5)
    输出：
    rgba(128, 255, 0, 0.5)
    
    /*hsv(@hue, @saturation, @value)函数:通过色相 (hue)，饱和度 (saturation)，色调 (value) 三种值 (HSV) 创建不透明的颜色对象。注意与 HSL 不同，这是另一种在Photoshop中可用的色彩空间。*/
    参数:
    @hue: 整数 0-360 表示度数
    @saturation: 百分比 0-100% 或数字 0-1
    @value: 百分比 0-100% 或数字 0-1
    返回值：颜色 (color)
    例如：
    hsv(90, 100%, 50%)
    输出：
    #408000
    
    /*hsva(@hue, @saturation, @value, @alpha)函数:通过色相 (hue)，饱和度 (saturation)，色调 (value)，以及 alpha 四种值 (HSVA) 创建透明的颜色对象。注意与 HSLA 不同，这是另一种在Photoshop中可用的色彩空间。*/
    参数:
    @hue: 整数 0-360 表示度数
    @saturation: 百分比 0-100% 或数字 0-1
    @value: 百分比 0-100% 或数字 0-1
    @alpha: 百分比 0-100% 或数字 0-1
    返回值：颜色 (color)
    例如：
    hsva(90, 100%, 50%, 0.5)
    输出：
    rgba(64, 128, 0, 0.5)
    
    /*hue(@color)函数:从颜色对象中提取色相值。*/
    参数：
    @color: 颜色对象 (A color object.)
    返回值：整数，范围从0-360
    例如：
    hue(hsl(90, 100%, 50%))
    输出：
    90
    
    /*saturation(@color)函数:从颜色对象中提取饱和度值。*/
    参数:
    @color: 颜色对象 (A color object.)
    返回值：百分比值 0-100
    例如：
    saturation(hsl(90, 100%, 50%))
    输出：
    100%
    
    /*lightness(@color)函数:从颜色对象中提取亮度值。*/
    参数:
    @color: 颜色对象 (A color object.)
    返回值：百分比值 0-100
    例如：
    lightness(hsl(90, 100%, 50%))
    输出：
    50%
    
    /*hsvhue函数:以HSV色彩空间提取颜色中的色相值。*/
    参数：
    颜色
    返回：整数，范围为0-360
    例如：
    hsvhue(hsv(90, 100%, 50%))
    输出：
    90
    
    /*hsvsaturation函数:以HSV色彩空间提取颜色中的饱和度值。*/
    参数：
    颜色
    返回值：百分比，范围0-100
    例如：
    hsvsaturation(hsv(90, 100%, 50%))
    输出：
    100%
    
    /*hsvvalue函数:以HSV色彩空间提取颜色中的色调值。*/
    参数：
    颜色
    返回：百分比，范围为0-100
    例如：
    hsvvalue(hsv(90, 100%, 50%))
    输出：
    50%
    
    /*red(@color)函数:从颜色对象中提取红色值。*/ //green(),blue()
    参数:
    @color: 颜色对象 (A color object.)
    返回值：整数 0-255
    例如：
    red(rgb(10, 20, 30))
    输出：
    10
    
    /*alpha(@color)函数:从颜色对象中提取 alpha 值。*/
    参数:
    @color: 颜色对象 (A color object.)
    返回值：浮点数，介于 0-1 之间
    例如：
    alpha(rgba(10, 20, 30, 0.5))
    输出：
    0.5
    
    /*luma(@color)函数:计算颜色对象的 luma 值（亮度的百分比表示法）。使用在WCAG2.0中定义的SMPTE C / Rec. 709 coefficients。 这个计算公式也用在 contrast() 函数中。*/
    参数:
    @color: 颜色对象 (A color object.)
    返回值：百分比 0-100%
    例如：
    luma(rgb(100, 200, 30))
    输出：
    65%