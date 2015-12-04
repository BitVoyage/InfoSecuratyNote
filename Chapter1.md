### 信息安全
***
#### chapter1
##### 1：为什么执行当前目录程序要加 ' ./'  ?
> 防李鬼，防止恶意程序与系统程序同名，恶意的执行它

##### 2：缓冲区
> 字符数组（整型数组很难攻击）

##### 3：调试器
> IDA-PRO  4000 $

##### 4：缓冲区溢出后果
> 1、程序崩溃  2、被拿到程序的控制权

##### 5、原理
> 编译过程
- 翻译
- 重组（代码段text、数据段data）

##### 6、冯.诺依曼体系
>- 核心思想：程序存储

##### 7、可重定向代码
>- PIC（位置无关代码）
>- gcc -fpic 编译一个位置无关的代码
>- 性能很差（缺点）

##### 8、call指令的动作
>- 把ret地址“记账”操作，自动push返回地址
>- 设置EIP

##### 9、leave指令的动作
>- mov ebp, esp
>- pop ebp

##### 10、ret指令
>- pop eip

##### 11、程序的序幕工作
><pre><code>
pushl %ebp
movl %esp, %ebp
subl %esp
</code></pre>
>- **pushl %ebp** : 保存前一个栈帧
>- **movl %esp, %ebp** : 然后把当前栈顶设置为新的ebp
>- **subl %esp** : 最后为临时变量开辟空间

##### 12、程序的结尾工作
><pre><code>
movl %ebp, %esp
popl %ebp
ret
</code></pre>
>- **movl %ebp, %esp** : 定位为当前栈帧位置
>- **popl %ebp** : 恢复老的ebp,即上一次调用栈帧位置
>- **ret** : 相当于**popl %eip**，设置eip.
