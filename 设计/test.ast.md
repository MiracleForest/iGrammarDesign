<div style="display:none">

FunctionDeclaration
ParmVarDecl是参数节点
在AST层级，不区分函数声明和函数定义，统一用FunctionDecl来标识，两个区分主要看是否有函数体（Body），可以使用bool hasBody()来进行判断。
CompoundStmt
代表大括号，函数实现、struct、enum、for的body等一般用此包起来。
DeclStmt
定义语句，里边可能有VarDecl等类型的定义
VarDecl
变量定义，如果有初始化，可以通过getInit()获取到对应的初始化Expr
IfStmt
If语句，包括三部分Cond、TrueBody、FalseBody三部分，分别可以通过getCond()，getThen(), getElse()三部分获取，Cond和Then是必须要有的，Else可能为空
BinaryOperator
二元操作Op，=,>,<,<=,>=,==等各种二元操作都继承它，从继承关系来说：
ImplicitCastExpr
隐形转换表达式，在左右值转换和函数调用等各个方面都会用到。
IntegerLiteral
定点Integer值
UnaryOperator
一元操作
CallExpr
函数调用Expr，子节点有调用的参数列表
ReturnStmt
返回语句 
ForStmt
For语句对应，包括Init/Cond/Inc 对应（int a=0;a<mm;a++）这三部分，还有一部分是body，可以分别使用getInit() / getCond() / getInc() / getBody()来分别进行获取
ParenExpr
括号表达式
RecordDecl
┈┊┆┌ ┬ ┐├ ┼ ┤└ ┴ ┘

</div>

```cpp

import i.io;

i32 func(i32 a,i32 b)
{
    return a+b*2;
}

i32 main(void)
{
    i32 a=0;
    a++;

    if(func(a,__Builtin_console_input_i32()))    {
        return a;
    }
    else{
        return -1;
    }
}
```

**GlobalArea**
- **ImportStmt**
  - **Target(BinaryOperatorsExpr)**
    - **left:** ***i***
    - **right:** ***io***
    - **Operator:** ***.***
- **FunctionDecl**
  - **Header**D 