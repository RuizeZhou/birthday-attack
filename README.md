# birthday-attack
# 项目说明

**1.小组成员**：周睿泽。git账户名称：RuizeZhou

**2,所作项目名称：**

本项目名称为：Project: implement the naïve birthday attack of reduced SM3 

简介：实现基础版对sm3的生日攻击，编程语言为python。

完成人：周睿泽

**3.清单：**

完成的项目：

√Project: implement the naïve birthday attack of reduced SM3 

√Project: implement the Rho method of reduced SM3

√Project: implement length extension attack for SM3, SHA256, etc.

√Project: do your best to optimize SM3 implementation (software)

√Project: Impl Merkle Tree following RFC6962

√Project: report on the application of this deduce technique in Ethereum with ECDSA

√Project: Implement sm2 with RFC6979

√Project: verify the above pitfalls with proof-of-concept code

√Project: Implement a PGP scheme with SM2

未完成的项目：

Project: Try to Implement this scheme

Project: Implement the above ECMH scheme

Project: implement sm2 2P sign with real network communication

Project: implement sm2 2P decrypt with real network communication

Project: PoC impl of the scheme, or do implement analysis by Google

Project: forge a signature to pretend that you are Satoshi

Project: send a tx on Bitcoin testnet, and parse the tx data down to every bit, better write script yourself

Project: research report on MPT

Project: Find a key with hash value “sdu_cst_20220610” under a message composed of your name followed by your student ID. For example, “San Zhan 202000460001”.

有问题的项目及问题：\

**4.本项目具体内容：**具体内容如下


# 生日攻击

Project: implement the naïve birthday attack of reduced SM3 

### A.具体的项目代码说明

​	本项目代码需要提前安装好numpy库和gmssl库。本项目主体代码如下：

```
def naive_birthday(n):
    memory=[]
    for i in range(2**n):
        memory+=['blank']
    temp=n//2
    for i in range(2**temp):
        input_data=getinput()
        joint_b=bytes(input_data,encoding='utf-8')
        output_data= sm3.sm3_hash(func.bytes_to_list(joint_b))

        prefix=output_data[0:(temp//2)]
        index=int(prefix,16)

        if memory[index]=="blank":
            memory[index]=input_data
        else:
            return memory[index],input_data
    else:
    	return None,None 
```

​	存储所有$\{y_i\}$,通过索引寻找碰撞。由于哈希函数的本身是抗碰撞的，我们真正找到碰撞复杂度极高。因此代码找的是前几位相同的局部碰撞。将前（temp//2）位对应的

### B.运行指导(跑不起来的不算成功)

​	已有本项目需要的库后直接运行即可。

### C.代码运行全过程截图(无截图无说明的代码不给分)

​	lenth=8时，表示寻找前两位的碰撞，得到结果如下，第一行为两个产生哈希碰撞的消息，下面是这两个消息及其对应的哈希值：

![1659155191707](https://cdn.jsdelivr.net/gh/RuizeZhou/images/1659155191707.png)

​	增加lenth值的大小，lenth=12,寻找前三位碰撞：

![1659155475311](https://cdn.jsdelivr.net/gh/RuizeZhou/images/1659155475311.png)

​	lenth=16，寻找前四位碰撞：

![1659155503972](https://cdn.jsdelivr.net/gh/RuizeZhou/images/1659155503972.png)

​	以此类推

### D.每个人的具体贡献说明及贡献排序(复制的代码需要标出引用)

本人负责全部。
