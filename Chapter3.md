### 信息安全
***
#### chapter3
##### 1、静态链接与动态链接
> Pay as you go.
>- ld命令：负责链接每个程序的片段。  
>   
 原理：判断e8（**call**）指令后面4个字节为-4的地方为‘洞’，等待装载器把程序中引用的函数填进去。这4个字节的值不能是其他值，为-4，是最好的，其他值也行，不过有时候可能会重复补洞。因为这样为调用这条指令的本身，如果其他值，其他函数可能就处于这个偏移位置，造成冲突。


 >- 二进制程序携带一张符号表( key - value )  
 程序中引用的外部函数以及外部数据，对应着在程序中的位置  


 >- IDE设置断点的原理：    
 > 也是有一张符号表，行号和对应的汇编指令。在某一行设置断点就会查询符号表。

##### 2、编译器
> 编译的时候，不管源代码中的函数是否能实现，只管编译程序中的语法错误，做了一些假定，假定这些函数一定存在。如
<pre><code>
int main()
{
 int x = add( 3, 4 );
 printf("x = %d\n", x);
 return 0;
}
</code></pre>
是可以编译成功的，编译器假定add函数一定存在，只负责编译方面的工作。链接add函数，是有链接器完成的。但对printf的编译会有warning，对add的编译却没warning。gcc中有一张符号表，是库函数的，却没有明显引用的情况下，就要报warning，对库函数和普通函数区分。(猜测)  
**gcc -Wall** 严格的编译，都会出warning。  
**gcc -pedantic** 只允许出现ANS C的代码。  
**gcc -static -v** 静态链接

#### 3、静态链接
>- 大 ：链接后的程序很大
>- 难 ：新版本的库无法更新到旧程序中。维护艰难
>- 快 ：程序是完整的，CPU全速执行
