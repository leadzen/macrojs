# macrojs
macrojs使用注释指令简单组合Javascript文件代码片段。  

## 1.用法
### Node环境
#### 安装
    npm install -g macrojs
#### 命令行
    macrojs input-file [output-file]
#### 代码中
    var macrojs = require('macrojs');
    ...
    var code = macrojs('source.js');
    
### Browser环境
#### 引入

    <script src="macro.js"></script>
#### 使用

    var code = macrojs('source.js');

#### 直接运行

    <script src="macro.js" run="source.js"></script>

或者

    <script src="macro.js">
    ...     //source code here.
    </script>

## 2. 宏指令
### 包含
包含指令用于在当前代码块中引入指定文件的外部代码块:
> /\*[ ]#include[!] *filename* [*comment*]\*/  
> //[ ]#include[!] *filename* [*comment*]  

若在注释引导符("/\*"或"//")与#include之间有空格, 则引入的代码块会按注释引导符前面的空格自动缩进引入代码.
默认情况下, 每个代码文件块只会被包含一次. 但是, 若紧接#include之后有叹号("!"), 则如果文件的代码块会在该处再重复引入一次.

### 定义
定义指令用于定义宏常量或宏函数:
> /\*#define *name[(parameters)]* *body* \*/  
> //#define *name[(parameters)]* *body*  

宏定义只是简单的源代码替换逻辑. 一旦定义了宏的 name 和 body, 后续代码的中匹配该 name 的标示符将被替换成 body 中的代码. 带参数的宏实际上是一个源代码替换模板, 替换时用实际参数来实例化模板形成要替换的源代码.  
 

### 行注释
行注释指令用于以注释或删除一行代码:
> /\*[!]//\*/ *any source code line*

若"//"前有叹号"!", 则删除从该指令处至行尾的代码, 否则只是注释掉行尾的代码. 

### 块注释
块注释指令是一对, 用于注释代码块:
> /\*[!]{\*/ *any source code block ...* /\*}\*/

若"{"前有叹号"!", 则删除从该代码块, 否则只是注释掉该代码块. 若"/\*{\*/"没有匹配的"/\*}\*/", 则将删除或注释掉从"/\*{\*/"至该代码文件结束的所有代码. 

## TODO
### 代码片段模块化?
