示例代码：
```cpp
int main(void)
{
	int a=0;
	if(a==2)
	{
		int b=a;
		int c=1;
	}
	a+=1;
}
```


示例代码对应AST（初步设计）：

**GlobalArea**  
　└[**0**]-**FuncDef**  
　　　　├**Name**:`main`  
　　　　├**ReturnType**\<**Type**:*Type*>  
　　　　┊　├**Type**:`Keyword`  
　　　　┊　└**Value**:`int`  
　　　　├**ParamList**  
　　　　┊　└**Null**  
　　　　└**Body**\<**Type**:*CompoundStmt*>  
　　　　　　├[**0**]-**VarDef**  
　　　　　　┊　　　├**Name**:`a`  
　　　　　　┊　　　├**Type**   
　　　　　　┊　　　┊　├**Type**:`Keyword`  
　　　　　　┊　　　┊　└**Value**:`int`   
　　　　　　┊　　　└**Value**\<**Type**:*IntegerLiteral*>   
　　　　　　┊　　　　　└**Value**:`0`   
　　　　　　├[**1**]-**IfStmt**  
　　　　　　┊　　　├**Condition**\<**Type**:*BinOp*>  
　　　　　　┊　　　┊　├**Left**\<**Type**:*Id*>  
　　　　　　┊　　　┊　┊　└**Value**=`a`  
　　　　　　┊　　　┊　├**Right**\<**Type**:*IntegerLiteral*>    
　　　　　　┊　　　┊　┊　└**Value**:`2`   
　　　　　　┊　　　┊　└**Op**:`==`   
　　　　　　┊　　　└**Body**\<**Type**:*CompoundStmt*>   
　　　　　　┊　　　　　├[**0**]-**VarDef**  
　　　　　　┊　　　　　┊　　　├**Name**:`b`   
　　　　　　┊　　　　　┊　　　├**Type**  
　　　　　　┊　　　　　┊　　　┊　├**Type**:`Keyword`  
　　　　　　┊　　　　　┊　　　┊　└**Value**:`int`  
　　　　　　┊　　　　　┊　　　└**Value**\<**Type**:*Id*>  
　　　　　　┊　　　　　┊　　　　　└**Value**:`a`  
　　　　　　┊　　　　　└[**1**]-**VarDef**  
　　　　　　┊　　　　　　　　　├**Name**:`c`  
　　　　　　┊　　　　　　　　　├**Type**  
　　　　　　┊　　　　　　　　　┊　├**Type**:`Keyword`  
　　　　　　┊　　　　　　　　　┊　└**Value**:`int`  
　　　　　　┊　　　　　　　　　└**Value**\<**Type**:*IntegerLiteral*>  
　　　　　　┊　　　　　　　　　　　└**Value**:`1`  
　　　　　　└[**2**]-**BinOp**  
　　　　　　　　　├**Left**\<**Type**:*Id*>  
　　　　　　　　　┊　└**Value**=`a`  
　　　　　　　　　├**Right**\<**Type**:*IntegerLiteral*>  
　　　　　　　　　┊　└**Value**:`1`  
　　　　　　　　　└**Op**:`+=`   
