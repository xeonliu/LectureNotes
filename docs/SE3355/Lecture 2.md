![](assets/Pasted%20image%2020240924143036.png)
# Three pass compilers

![](assets/Pasted%20image%2020240924143546.png)

+ HIR
+ LIR: 很接近汇编的伪代码

IRS
`Source -> AST -> MIR -> Instruction List -> Dest`

+ MIR：平台无关的IR（将使用LLVM IR？）
+ IL：无限寄存器和变量，接近结果
![](assets/Pasted%20image%2020240924143637.png)


![](assets/Pasted%20image%2020240924144137.png)
+ Pass 8 结束
+ Pass1：Lex -> Parsing
+ Pass2： IR部分
+ 后边是后端、优化


Two important points:
1. This is implemented by reading left to right, recogninzing one at a time
2. Decide where one token ends and the next token begins(可能前面对后边突然错了)
