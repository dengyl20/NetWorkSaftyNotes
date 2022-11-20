# Lettuce2&3 密码学基础



## 密码学基本概念

### 两种加密形式

-   传统加密：又称为**对称加密**、单钥加密，安全性在于保持算法本身的保密性  
-   现代加密：又称为**非对称加密**、公钥加密，把算法和密钥分开，密码算法公开，密钥保密，安全性在于保持密钥的保密性  

### 基本概念

-   明文/密文
-   加密/解密
-   密码算法/密码：用来加密和解密的数学函数  
-   密钥：密码算法中的一个变量， $D_{Kd}(E_{Ke}(m))= m  $

### 密码学的基本模型

-   密码编码学
-   密码分析学
-   密码编码学和密码分析学统称为密码学  

### 密码编码学

-   研究各种加密方案的学科称为密码编码学  
-   密码编码学系统有三个独立的特征：
    1.   转换明文为密文的运算类型，基于两种原理：
         -   **置换**：将明文中的元素重新排列  
         -   **代换**：将明文中每个元素映射成为另外一个元素  
         -   原则是不允许丢失信息，即所有的运算都是可逆的  
    2.   所用的密钥数：
         -   **对称密码**：发送方和接收方使用相同的密钥
         -   **非对称密码**：发送方和接收方使用不同的密钥
    3.   处理明文的方法：
         -   **分组密码/块密码**：每次处理一个输入分组，相应地输出一个输出分组
         -   **流密码/序列密码**：连续地处理输入元素，每次输出一个元素

-   无条件安全和计算安全：
    -   无条件安全：无论有多少可以使用密文，都不足以唯一地确定由该体制产生密文所对应的明文，则加密机制是无条件安全的  
    -   计算安全：满足以下条件之一：
        -   破译密码的代价大于加密数据本身的价值  
        -   破译密码的时间超过了密文信息的生命期  

## 古典密码

### 代换技术

-   代换技术是将明文字母替换成其它字母、数字或者符号的方法
-   **Caesar密码**：$c = (m+3) \ \ Mod\ \ 26$,单表代换密码，只有25个密钥（1~25）
-   **秘钥词密码**：设一个秘钥词放在前面，其余字母按顺序排列，单表代换密码
-   **Playfair密码**：多表代换密码，将明文中的双字母作为一个单元并将其转换为密文的双字母音节，即将单字母映射关系变为了一个字母对到另一个字母对的映射关系
    -   构造密钥词的方法是：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221119220301293.png" alt="image-20221119220301293" style="zoom:33%;" />  
    -   加密规则是（一次加密两个字母）：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221119220333723.png" alt="image-20221119220333723" style="zoom:25%;" />

-   **Hill密码**：多表代换密码，将m个连续的明文字母代换成m个密文字母，如下图：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221119220926656.png" alt="image-20221119220926656" style="zoom:33%;" />
    -   n维矩阵能够隐藏（n-1）大小的字母对的频率特征

-   **Vigenere密码**：是使用一系列Caesar密码组成密码字母表的加密算法，属于多表代换密码  
-   **Vernam密码**：选择一个与明文毫无统计关系并且和明文一样长的密钥，其运算是基于二进制数据而非字母的  
    -   $c_i=p_i⊕ ki   $
    -   一次一密（One-time Pad； OTP）,基于Vernam密码的改进方案，使用与消息一样长且无重复的随机密钥来加密消息，无条件安全  

### 置换技术

-   置换密码是通过置换形成新的排列  
-   单步置换还是容易被识破，一般采用多步置换密码就安全多了  
-   转轮机采用多层加密原理  

### 破译举例

-   穷举法
-   频率分析法：单码/双码/三码统计特征

## 对称密码算法

### 简介

-   加密和解密使用相同的密钥：$K_E=K_D$

-   密钥必须使用秘密的信道分配  

### S-DES

-   简化DES(S-DES)是为教学使用的一个加密算法，与DES有着相似的性质和结构，但是参数要小很多，便于理解  
-   加密/解密算法的输入为一个8位明文/密文组和一个10位密钥，输出为8位密文组/明文组

-   加密/解密：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221119235143321.png" alt="image-20221119235143321" style="zoom:50%;" />

-   加密流程和解密流程几乎相同，不同之处在于密钥$K_1,K_2$输入的位置
-   加密过程的函数：
    -   IP：初始置换函数，$IP(n1,n2,n3,n4,n5,n6,n7,n8)= (n2,n6,n3,n1,n4,n8,n5,n7)  $
    -   E/P:扩展位宽的置换函数，$E/P(n1,n2,n3,n4)=(n4,n1,n2,n3,n2,n3,n4,n1)  $
    -   S盒：
        -   第1、 4位作为二进制数决定S盒的行  
        -   第2、 3位作为二进制数决定S盒的列  
        -   输出即是二进制的2位输出  
        -   $S_0:$<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221119235909386.png" alt="image-20221119235909386" style="zoom:33%;" />
        -   $S_1:$<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221119235927417.png" alt="image-20221119235927417" style="zoom:33%;" />
    -   $P_4$：置换函数，$P4(n1,n2,n3,n4)=(n2,n4,n3,n1)  $
    -   SW: 交换函数，SW将输入的左4位和右4位交换  
    -   $IP^{-1}：$末尾置换函数，$IP^{-1}(n1,n2,n3,n4,n5,n6,n7,n8)= (n4,n1,n3,n5,n7,n2,n8,n6)  $

-   子密钥产生过程中的函数：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120000253194.png" alt="image-20221120000253194" style="zoom:50%;" />

### Feistel密码结构

-   现在使用的对称分组密码算法都基于Feistel分组密码结构的  
-   Feistel建议使用乘积密码的概念来逼近简单代换密码  
-   乘积密码是指依次使用两个或以上的基本密码  
-   Feistel 建议交替使用代换和置换  
-   混淆和扩散：
    -   **扩散**是指使明文的统计特征消散在密文中，让每个明文数字尽可能地影响多个密文数字  
    -   **混淆**是尽可能地使密文和加密密钥间的统计关系更复杂，以挫败推导出密钥的企图  

-   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120001453241.png" alt="image-20221120001453241" style="zoom:33%;" />



-   Feistel密码每轮迭代都有相同的结构

### DES

-   DES采用分组加密，是一种对称密钥算法 
-   分组长度是64 bits   
-   除了初始置换和末尾置换， DES的结构与Feistel密码结构完全相同  
-   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120003308457.png" alt="image-20221120003308457" style="zoom:33%;" />

-   E盒扩展置换：将Ri从32位扩展到48位，输入的一位影响下一步的两个替换，使得输出对输入的依赖性传播得更快，密文的每一位都依赖于明文的每一位  
-   S-盒代换选择：将48比特压缩成32比特  

### 最常用的对称密码

-   3DES：三重DES加密，密钥长度为112比特。  

-   Blowfish：分组长度是64位，密钥长度可以在32～ 448位之间变化  

    -   加密过程：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120135613795.png" alt="image-20221120135613795" style="zoom:33%;" />

    -   Blowfish算法的子密钥和S盒都是用Blowfish算法本身生成的，这使得数据完全不可以辨认，对它的密钥分析也就异常困难  
    -   Blowfish算法每轮运算都是对数据的左右两个部分同时执行运算，与古典Feistel结构不同；这使得密码的强度又增强了  

-   RC5：

    -   RC5的分组长度可以位32、 64或者128位，密钥长度则可取0~2040位  
    -   RC5是一个由三个参数确定的加密算法族  ：
        -   w：分组长度
        -   r：迭代次数
        -   b：密钥K的8位字节数

    -   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120135859926.png" alt="image-20221120135859926" style="zoom:33%;" />



-   AES：AES的分组长度128位，密钥长度128位  

    -   AES不是Feistel结构，AES的每一轮都使用代换和置换并行的处理整个数据分组  
    -   AES的每一轮迭代都包括四个阶段：
        -   字节代换：用一个S盒完成分组中的字节代换  
        -   行移位：一个简单的置换  
        -   列混淆：算术代换  
        -   轮密钥加：利用当前分组和扩展密钥的一部分进行按位异或  

    -   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120140639290.png" alt="image-20221120140639290" style="zoom:33%;" />
    -   密钥被扩展成44个32位字所构成的数组  
    -   仅仅在轮密钥加阶段使用密钥；轮密钥加实际上是一种Vernam密码  

## 非对称密码算法

### 公钥密码原理

-   对称密码的缺陷：
    -   密钥必须经过安全的信道分配  
    -   无法用于数字签名  
    -   密钥管理复杂  

-   公钥密码是基于数学函数而不是代换和置换  
-   公钥密码的组成部分：
    -   明文：可读的信息，做为加密算法的输入  
    -   加密算法：对明文进行的各种变换  
    -   公钥/私钥：一个用于加密，一个用于解密。加密算法执行的变换依赖于公钥和私钥
    -   密文：加密算法的输出，不可读信息  
    -   解密算法：根据密文和相应的密钥，产生出明文  

-   符号说明：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120142825319.png" alt="image-20221120142825319" style="zoom:33%;" />

-   公钥密码体制：每个用户产生一对密钥：用于加密和解密。其中一个密钥存于公开的寄存器或者文件中，即公钥；另外一个密钥是私有的，称为私钥  

    -   公钥公开，用于加密和验证签名
    -   私钥保密，用作解密和签名
    -   利用这种方法，通信各方皆可以访问公钥，而私钥是个通信方在本地产生的，所以不必进行分配
    -   只要系统控制了私钥，那么它的通信是安全的  
    -   任何时刻，系统都可以改变自己的私钥，而公布相应的公钥代替原来的公钥  
    -   **加密原理**示例图：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120143132057.png" alt="image-20221120143132057" style="zoom:33%;" />
    -   **签名原理**示例图：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120143333311.png" alt="image-20221120143333311" style="zoom:33%;" />

    -   **数字签名**和**加密**同时使用：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120143447657.png" alt="image-20221120143447657" style="zoom:33%;" />

-   公钥密码的数学原理：陷门单向函数

    -   单向函数是求逆困难的函数；单向陷门函数，是在不知陷门信息下求逆困难的函数，当知道陷门信息后，求逆是易于实现的
    -   单向陷门函数f(x)，必须满足以下三个条件 ：
        -    给定x，计算y=f(x)是容易的  
        -   给定y, 计算x使y=f(x)是困难的  
        -   存在δ，已知δ时对给定的任何y，若相应的x存在，则计算x使y=f(x)是容易的  

    -   仅满足前两条的称为单向函数，第三条为陷门性，δ称为陷门信息

-   公钥密码系统的应用：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120143858149.png" alt="image-20221120143858149" style="zoom:50%;" />

-   在实际应用中，公钥密码目前仅局限于密钥管理和数字签名  
-   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120144121552.png" alt="image-20221120144121552" style="zoom:50%;" />

-   数论基础：
    -   欧拉函数：ф(n) ： n是正整数,ф(n) 是比n小且与n 互素的正整数个数  ， 如果p是素数，则 ф(p)=(p-1)  
    -   欧拉定理：若整数m 和n 互素，则$m^{\phi(n)}\equiv 1\ \ {\rm mod}\ \ n \ \ \ \to\ \ \  M^{k\phi(n)+1}\equiv m\ \ {\rm mod}\ \ n$

### RSA算法

-   RSA体制是一种分组密码，其明文和密文都是0~n-1之间的整数，通常n的大小为1024位二进制数或者309位十进制数  
-   密钥的产生：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120145519008.png" alt="image-20221120145519008" style="zoom:33%;" />

-   加密/解密过程：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120150024410.png" alt="image-20221120150024410" style="zoom:33%;" />

-   RSA算法举例1：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120150950484.png" alt="image-20221120150950484" style="zoom:50%;" />

-   RSA算法举例2：

    <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120151418776.png" alt="image-20221120151418776" style="zoom:33%;" />

<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120151428521.png" alt="image-20221120151428521" style="zoom:33%;" />



<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120151441290.png" alt="image-20221120151441290" style="zoom:33%;" />

-   RSA算法的安全性：对RSA算法的攻击方法：蛮力攻击、数学攻击、计时攻击  
    -   蛮力攻击：对所有密钥都进行尝试  
    -   数学攻击：实质是两个素数乘积(n)的因子分解  
    -   计时攻击：攻击者可以通过记录计算机解密消息所用的时间来确定私钥  

-   RSA算法的性能：
    -   软件实现比DES慢100倍  
    -   硬件实现比DES慢1000倍  

### DH密钥交换算法

-   Diffie-Hellman密钥交换算法的目的是使两个用户能够安全地交换密钥，该算法本身也只局限于进行密钥交换  

-   数学背景：

    -   本原根：a是素数p 的一个本原根，如果a mod p, $a^2$ mod p , …, $a^{p-1}$ mod p 是1到p-1的排列，即各不相同，是整数1到p-1的一个置换  
    -   对于整数b（b<p） 和素数p 的一个本原根a,可以找到一个唯一的指数i，使得：b ≡ $a^i$ mod p , 其中0≤i≤(p-1)  
    -   i 称为 b 的 以a 为底 模p的离散对数或指数 , 记为 $ind_{a,p} (b)$  
        -   $ind_{a,p} (1)=0$
        -   $ind_{a,p} (a)=1$

    -   对于$b= a^x\ {\rm mod}\ p$
        -   已知a, x, p，计算b 是容易的  
        -   已知a, b, p，计算x 是非常困难的  

-   DH算法举例：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120153418484.png" alt="image-20221120153418484" style="zoom:33%;" />

### 其他公钥密码算法

-   DSA：数字签名算法，算法的安全性是基于计算离散对数的难度  
-   椭圆曲线密码系统  
-   RSA是事实上的标准  



## 密钥的分配

-   存在两种加密方法：
    -   链路加密
    -   端到端加密

-   密钥分配方法就是将密钥发放给希望交换数据的双方而不让别人知道的方法  

### 传统的对称密码分配

-   方法一：密钥由A选择，并亲自交给B

-   方法二：第三方选择密钥后亲自交给A和B
-   方法三：如果A和B以前或者最近使用过某个密钥，其中一方可用它加密一个新密钥后再发送给另外一方
-   方法四： A和B与第三方C均有秘密渠道，则C可以将一密钥分别秘密发送给A和B  

-   方法一和二需要人工传送密钥，适用于链路加密；对于端到端加密，则使用密钥分配中心  

-   密钥分配中心KDC模式 ：

    -   假定每个用户与密钥分配中心KDC共享唯一的一个主密钥 ：
        -   A有一个除了自己只有KDC知道的主密钥Ka  
        -   B有一个除了自己只有KDC知道的主密钥Kb  

    -   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120154108752.png" alt="image-20221120154108752" style="zoom:33%;" />
    -   在网络规模很大的时候，密钥的分配功能不限定在单个的KDC上面，而是使用层次式的KDC  
    -   层次式KDC密钥分配使得主密钥分配的代价变小了。而且，如果一个本地KDC出错，或者被攻击了，破坏只是集中在一个区域中，不会影响全局  

### 公钥的分配

-   公钥密码可用于下面两个方面：  
    -   公钥的分配  
    -   公钥密码用于传统密码体制的密钥分配  

-   常用的公钥分配方法有四种  ：
    -   公开发布  ：缺点：任何人都可以伪造这种公钥的公开发布  
    -   公开可访问目录：维护一个动态可访问的公钥目录可以获得更大程度的安全性；某个可信的实体或组织负责这个公开目录的维护和分配  
    -   公钥授权 ：缺点在于公钥管理员就会成为系统的瓶颈    
    -   公钥证书   ：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120154752837.png" alt="image-20221120154752837" style="zoom:33%;" />

### 利用公钥分配传统密码的密钥

-   简单的密钥分配  ：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120154924360.png" alt="image-20221120154924360" style="zoom:33%;" />

-   具有保密性和真实性的密钥分配  ：

    ![image-20221120155331967](C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120155331967.png)









# Lettuce4 认证技术

## 消息认证

### 消息认证基本概念

-   泄密：将消息透露给没有合法密钥的接收方  
-   传输分析
-   伪装
-   网络环境中的攻击：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120155952595.png" alt="image-20221120155952595" style="zoom:33%;" />

-   **消息认证就是验证所收到的消息确实是来自真正的发送方且未被修改的消息**  

-   任何消息认证都能在功能上看做两层：
    -   下面一层中有某种产生认证符的函数，认证符是一个用来认证消息的值
    -   上面一层将该函数作为原语，使得接收方可以验证消息的真实性

### 认证函数

-   认证函数：产生认证符的函数
-   可以分为三类：
    -   消息加密：将整个消息的密文作为认证符
    -   消息认证码MAC： MAC是消息和密钥的公开函数，它产生定长的值，该值作为认证符  
    -   Hash函数：它是将任意长的消息映射为定长的hash值的公开函数，以该hash值作为认证符  

### 认证函数1：消息加密

-   对称加密：
    -   发送方A用A和B共享的密钥K，对发送到接收方B的消息M进行加密，如果没有其他人知道该密钥，就可以提供保密性  
    -   B可以在接收到消息后，用密钥K解密，确认该消息是由A发出的  

-   对称加密的例子：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120160902904.png" alt="image-20221120160902904" style="zoom:33%;" />

-   对称加密时需要先构造FCS，再加密，顺序不能变化
-   对称加密的协议：TCP协议，可以对除了IP报头之外的所有数据进行加密
-   公钥加密：
    -   公钥加密只提供保密性，不能提供认证  
    -   如果既要提供保密性，又要提供认证，发送方A可以先用其私钥加密(数字签名)，然后用B的公钥加密  
    -   这种方法的缺点是执行了四次附加的公钥算法运算  

-   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120162047823.png" alt="image-20221120162047823" style="zoom:33%;" />



### 认证函数2：消息认证码MAC

-   消息认证码：
    -   消息认证码MAC也是一种认证技术，它利用密码生成一个固定长度的短数据块，并将该数据块附加在消息之后
    -   MAC是消息和密钥的函数：$MAC=C_k(M)$
    -   MAC函数与加密类似，区别就是MAC算法不要求可逆性，而加密算法必须可逆  

-   MAC认证的过程:<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120162806315.png" alt="image-20221120162806315" style="zoom:33%;" />

-   使用MAC的情况：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120162832375.png" alt="image-20221120162832375" style="zoom:33%;" />

### 认证函数3：Hash函数

-   单向的Hash函数是消息认证码的一种变形
-   hash函数的输入是长度可变的消息M，输出是长度固定的hash码
-   hash函数不使用密钥，仅是消息M的函数，因此也称为消息摘要(Message Digest， MD)  
-   Hash码是所有消息位的函数，它具有错误检测能力  
-   将hash码用于消息认证的多种形式：
    1.   用对称密码对消息以及hash码进行加密：提供了**认证**和**保密性**
    2.   用对称密码仅对hash加密：仅提供**认证**（相当于MAC），对于不要求保密性的应用，会减少处理代价
    3.   用公钥密码和发送方的私钥对hash码加密：提供了**认证**和**数字签名**（数字签名有发送方的私钥所保证）
    4.   先用发送方的私钥对hash码进行加密，再用对称密码中的密钥对消息和上述加密结果进行加密：提供了**认证**、**数字签名**和**保密性**  
    5.   假定通信双方共享公共的秘密值S， A将M和S联接后再计算hash值，并将其附加在M后面 ， 由于B也知道S， B可以计算hash值，并验证其正确性：提供了**认证**  
    6.   在假设（5）的基础上对整个消息和hash码加密：提供了**认证**和**保密性**

-   对hash函数的要求：
    -   可以操作任意大小的报文m
    -   生成的h长度固定
    -   单向性
    -   抗弱碰撞性
    -   抗强碰撞性

### 安全hash算法的一般结构

-   Hash函数将输入消息分为L个固定长度的分组，每个分组长度为b位，最后一个分组不足b位时，需要填充成b位  
-   输入中包含长度，增加了攻击的难度  
-   <img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120173830658.png" alt="image-20221120173830658" style="zoom:50%;" />

-   Hash函数中重复使用了压缩函数f：
    -   它的输入是前一步中得出的n位结果（即连接变量）和一个b位分组，输出位一个n位分组
    -   连接变量的初始值在算法开始的时候指定，其终值即为hash值。通常b>n，因此称为压缩函数  

-   设计安全hash函数可以归纳为设计具有抗碰撞能力的压缩函数问题，并且该压缩函数的输入是定长的  

### 主要的hash算法概述

-   MD族：
    -   MD = Message Digest （消息摘要）  
    -   MD2、 MD4和MD5都产生一个128位的消息摘要  

-   SHA族：
    -   SHA = Secure Hash Algorithm  
    -   SHA-0 ：正式地称作SHA系列，发行后不久即被指出存在弱点
    -   SHA-1： 1994年发布的，与MD4和MD5散列算法非常相似，被认为是
        MD4和 MD5的后继者.
    -   SHA-2：实际上分为SHA-224、 SHA-256、 SHA-384和SHA-512算法。
    -   SHA-3：方案正在征集中。  

-   HAVAL：加密哈希算法  
-   Gost：是一套俄国标准  
-   RIPEMD-128/160/320：RIPEMD由欧洲财团开发和设计的MD算法  

-   以上算法中，仅有SHA-2和RIPEMD-160未被攻破

### Hash算法：MD5

-   MD5的输入是任意长度的消息，对输入按照512位的分组为单位进行处理，算法的输出是128位的消息摘要  
    -   使用小端结构（低端结构）

-   MD5算法步骤：
    -   Step1：增加填充位
    -   Step2：填充长度
    -   Step3：初始化MD缓存
    -   Step4：以512位的分组处理信息
    -   Step5：输出

-   MD5算法过程：<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120175047880.png" alt="image-20221120175047880" style="zoom:50%;" />

-   Step1：增加填充位
    -   填充bit：第1位为1，其后所有位都为0
    -   填充bit后，使得消息长度与448（512-64）mod 512同余

-   Step2：填充长度
    -   用64位表示填充前的报文长度，附加填充比特的后面，如果长度大于$2^{64}$，则对$2^{64}$取模    
    -   以低端结构方式表示被填充前的消息长度  
    -   完成填充后，消息的总长度是512的整数倍  

-   Step3:初始化MD缓存
    -   Hash函数的中间结果和最终结果都保存于128位的缓冲区中，缓冲区用4个32位的寄存器(A,B,C,D)表示  
    -   A,B,C,D寄存器以低端格式存储，初始值为0~ F F ~ 0

-   Step4：

    -   计算Hash值<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120180256948.png" alt="image-20221120180256948" style="zoom:33%;" />
    -   MD5的压缩函数<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120181047177.png" alt="image-20221120181047177" style="zoom:33%;" />

    -   MD5 每轮处理512位分组的过程<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120181125787.png" alt="image-20221120181125787" style="zoom:33%;" />

    -   续上图<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120181206389.png" alt="image-20221120181206389" style="zoom:33%;" />

-   Step5：输出  
    -   所有的L个512位的分组处理完之后，第L个分组的输出即是128位的消息摘要  

-   MD5算法中，hash函数的每一位都是输入的每一位的函数；基本逻辑函数的复杂迭代使得输出对输入的依赖性非常小  

### Hash算法：各类算法比较

<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120230000218.png" alt="image-20221120230000218" style="zoom:33%;" />

<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120230013034.png" alt="image-20221120230013034" style="zoom:33%;" />

<img src="C:/Users/27084/AppData/Roaming/Typora/typora-user-images/image-20221120230031424.png" alt="image-20221120230031424" style="zoom:33%;" />

### 数字签名算法DSS

-   数字签名：消息认证可以保证通信双方不受第三方的攻击，但是它不能处理通信双方自身发生的攻击  

-   数字签名的特征：
    -   它必须能够验证签名者、签名日期和时间  
    -   它必须能认证被签的消息内容  
    -   签名应能由第三方仲裁，以解决争执  

-   数字签名可以分成两类：直接数字签名和仲裁数字签名  
    -   直接数字签名只涉及通信双方：
        -   假定接收方已知发送方的公钥，则发送方可以通过用自己的私钥对整个消息或者消息的hash码加密来产生数字签名  
        -   用接收方的公钥(公钥密码)和共享的密钥(对称密码)对整个消息和签名进行加密，则可以获得保密性  
        -   直接数字签名的弱点在于方法的有效性依赖于发送方私钥安全性
    -    仲裁数字签名：
        -    从发送方X到接收方Y的每条已签名的消息都先发给仲裁者A， A对消息
             及其签名进行检查以验证消息源及其内容，然后给消息加上日期，并发
             给Y，同时指明该消息已通过仲裁者的检验  
        -    通过A的加入解决了直接数字签名的问题

- DSS使用SHA-1算法的给出的数字签名方法叫做数字签名算法DSA
- DSS只提供数字签名功能，不能用于加密或者密钥分配
- 原理图：<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121022810602.png" alt="image-20221121022810602" style="zoom:50%;" />

- 用hash函数产生的hash码和随机数k，以及发送方的私钥$KR_a$和$KU_G$作为数字签名函数sig的输入
- 签名函数sig的输出分为s和r两部分，将m，s，r，拼接为新的消息
- 接收方对接收到的消息产生hash码，此hash码和签名以其作为验证函数Ver的输入，验证函数依赖于全局公钥$KU_G$ 和$KU_a$，若验证函数Ver的输出等于签名中的r，则签名有效
- <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121025133853.png" alt="image-20221121025133853" style="zoom:50%;" />

## 电子身份认证

- 身份认证是指在主客体交互行为过程中确认行为参与（主体或客体，通常称为用户）身份的解决方法  

- 电子身份认证是在计算机及网络中确认操作者身份的解决方法  

### 网站身份认证技术

- 最简单的网站用户认证：HTTP的Basic认证
- HTTP的Basic认证：
  - 用户身份凭证：账号+静态口令（U,P）
  - 由于HTTP协议是面向一次连接的无状态网络协议，因此需要在每次发出HTTP请求时，把用户身份凭证的明文发送到服务器端，服务器与存储在服务器端的用户凭证进行比较  
  - 发送时，对账号口令进行Base64编码，服务器端接收后进行Base64解码

- HTTP的Basic认证：改进1
  - 解决账号口令明文传输可能被监听盗取的问题  
    - 使用加密技术
    - 使用消息认证技术
  - 解决账号口令长期本地保存以及服务器端每次都进行账号口令验证的问题 
    - 使用表单验证+session的机制  

- HTTP的Basic认证：改进2
  - 将口令P作为密钥$E_k$，每次发送$U || E_k[U]$

- HTTP的Basic认证：改进3
  - 使用MAC认证
  - 采用
  - 挑战/响应(Challenge/Response)机制，需要进行两次HTTP请求  ：
    - 第一次请求：服务器向客户端返回一个随机生成的挑战码M  
    - 第二次请求：服务器向客户端返回一个挑战码M，服务器端进行验证  

### 基于表单的身份认证

- Web的Session机制：
  - 一个Session包括特定的客户端、特定的服务器端和特定的操作时间段

- Session的工作原理：

  - 当某个Session首次启用时，服务器会产生一个唯一的标识符发送到客户端
    - 唯一标识符通常是一串随机字符串
    - 在客户端浏览器上，唯一标识符通常用Cookie技术存储

  - 在Session存活期间，客户端每次向服务器发送的HTTP请求都会包含上述唯一标识符，使得服务器能够把前后多次请求关联起来
  - 当Session结束时，服务器端和客户端都应当销毁上述唯一标识符  

- 基于表单的Web身份认证过程通常包括三个步骤：  
  1. 客户端向服务器发送请求，服务器返回包含表单的页面  
  2. 用户按要求填写表单的内容完成后，客户端把表单内容发送到服务器；服务器获取表单中的内容后，进行验证，验证通过则启动Session并返回给客户端（这里账号和口令通过明文传输）
  3. 客户端后续的请求包含Session的唯一标识符，服务端验证唯一标识符的合法性  

- 缺点是安全性低，账号和口令明文在网络上传输  
- 基于表单的身份认证：改进1  
- <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121031331256.png" alt="image-20221121031331256" style="zoom:33%;" />

- 基于表单的身份认证：改进2
  - 使用传输层SSL协议传输HTTP请求  

- 网站身份增强认证的其它方式：
  - 手机短信口令
  - 动态口令
  - USB KEY
  - 数字证书





# Lettuce5 WLAN安全

## 无线网络概述

- 无线电通信技术是在没有物理连接的情况下多个设备之间能够互相通信的技术  
- 无线网络分类：<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121032929071.png" alt="image-20221121032929071" style="zoom:33%;" />

- WLAN的安全威胁：
  - 无线窃听
  - 假冒攻击
  - 信息篡改
  - 重放、重路由、错误路由、删除消息
  - 网络泛洪

### 无线局域网加密认证技术

- 无线局域网加密认证技术
  - 无加密认证
  - WEP
  - WPA
- 无加密认证：
  - 无线接入点AP：网络的中心节点
  - STA站点：连接到无线网络中的终端
  - SSID：便于用户识别，为每个AP配置的标志名，通常情况下，AP会向外广播SSID，可以通过disable SSID Broadcast提高安全性

- 有线等效保密协议WEP：

  - 有线等效保密协议WEP（Wired Equivalent Privacy）目的是为无线局域网提供与有线网络相同级别的安全保护，协议标准为IEEE 802.11b 
  - 使用对称加密算法 

  - <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121034242779.png" alt="image-20221121034242779" style="zoom:33%;" />

  - <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121034920909.png" alt="image-20221121034920909" style="zoom:33%;" />

  - <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121034940521.png" alt="image-20221121034940521" style="zoom:33%;" />

  - <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121035005807.png" alt="image-20221121035005807" style="zoom:33%;" />

- WPA1：因为WEP的严重安全漏洞， 2002年Wi-Fi联盟制定了WPA1，这
  是一个过度性的中间标准，其核心就是IEEE 802.1x和TKIP  
  - 临时密钥完整性协议TKIP：包在已有的WEP密码外围的一层“外壳”
    - TKIP使用WEP同样的加密引擎和RC4算法，但是TKIP中密码使
      用的密钥长度是128位  
    - 动态变化每个数据包所使用的密钥  
    - 利用TKIP传送的每一个数据包都具有独有的48位序列号  
  - IEEE 802.1x  ：
    - IEEE 802.1x是针对以太网而提出的，基于端口的网络访问控制利用物理层特性对连接到无线端口的设备进行身份认证  
    - IEEE 802.1x基于客户/服务器模式，可以在无线终端与AP建立连接之前，对用户身份的合法性进行认证  
    - 认证过程：<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121040016385.png" alt="image-20221121040016385" style="zoom:33%;" />

- WEP-WPA1-WPA2比较：<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121040115484.png" alt="image-20221121040115484" style="zoom:33%;" />  



# Lettuce 6 CIA & VPN

## 安全目标

- 安全目标、服务、机制的关系：<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121040337369.png" alt="image-20221121040337369" style="zoom:33%;" />

### 安全目标：CIA

- Confidentiality： 保密性、机密性  
- Integrity： 完整性  
- Availability： 可用性  

### OSI 安全框架

OSI安全框架主要关注安全服务、安全机制和安全攻击  

- 安全服务：一种由系统提供的对系统自愿进行特殊的处理或通信服务，安全服务通过
  安全机制来实现安全策略
- 安全机制：用来保护系统免受监听、阻止安全攻击及恢复系统的机制    
- 安全攻击：主动攻击、被动攻击  

## 安全服务

- X.800提供了以下安全服务：<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121041832524.png" alt="image-20221121041832524" style="zoom:33%;" />

### Authentication 认证服务

- 认证服务Authentication与保证通信的真实性有关  
- 在单向通信时：认证服务向接受方保证发送方的真实性  
- 在双方通信时：
  - 在连接的初始化阶段，认证服务保证双方的真实性  
  - 认证服务还需要保证该连接不受第三方非法干扰  

- 两个特殊的认证服务：

  - 对等实体认证：
    - 参与通信的实体的身份是真实的  
    - 一个实体不能试图进行伪装或者对以前连接进行非授权的重放  
    - 面向连接的应用  

  - 数据源认证：
    - 对数据的来源提供确认，但是对数据的复制和修改不提供保护  
    - 保证接收到的信息的确来自它所宣称的来源  
    - 面向无连接的应用  

### Confidentiality  保密服务

- 保密服务Confidentiality是防止传输数据遭到被动攻击  
- 分为连接保密服务和无连接保密服务
- 保密力度：流(stream)、 消息(message)、 选择字段(field)  
- 保密服务防止攻击者观察到消息的源、目的、频率、长度或者其它流量特征  

### Integrity & Access Control  

- 数据完整性服务Integrity：可对消息流、单条消息或消息的选定部分进行保护  
- 访问控制服务Access Control：是指限制实体的访问权限，通常是经过认证的合法的实体才可以访问  

### Non-repudiation & Availability  

- 抗抵赖服务Non-repudiation：防止发送方或者接收方否认传输或者接收过某条消息  

- 可用性服务Availability：根据系统的性能说明，能够按照授权的系统实体的要求存取或使用系统或系统资源的性质  

## 安全机制

### 分类

安全机制分为两类：

- 普通安全机制：不属于任何协议层或者安全服务的安全机制  
- 特定安全机制：在特定的协议层实现的安全机制  

### 普通的安全机制

<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121043013564.png" alt="image-20221121043013564" style="zoom:33%;" />

### 特定的安全机制

<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121043050985.png" alt="image-20221121043050985" style="zoom:50%;" />

### 安全性攻击

- 主动攻击：试图改变系统资源或者影响系统运行  
- 被动攻击：试图了解或者利用系统的信息但不影响系统资源  
  - 窃听
  - 流量分析

### 虚拟专用网VPN

- 需求背景：TCP/IP协议本身存在许多固有的安全缺陷，架设物理专用网难度大

- VPN的定义：Virtual Private Network，虚拟专用网  
- <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121043637873.png" alt="image-20221121043637873" style="zoom:33%;" />

- VPN提供的安全功能
  - 数据机密性保护
  - 数据完整性保护
  - 数据源身份验证
  - 重放攻击保护

- VPN的解决方案
  - 基于数据链路层的VPN解决方案:L2TP/PPTP/L2F
  - 基于网络层的VPN解决方案:IPsec/IKE
  - 基于传输层的VPN解决方案:SSL

- 基于数据链路层的VPN解决方案：
  - 由于数据链路层的VPN技术在认证、数据完整性以及密钥管理等方面的不足，现在已经很少应用  

- 基于传输层的VPN解决方案:SSL
  - 基于传输层SSL协议的VPN解决方案， 零客户端是其最大优势  
  - 在实际应用中， SSL VPN和IPsec VPN两种方案往往结合实行  
  - 像视频会议这样的非B/S（Browser-Server）结构的业务是无法通过SSL VPN建立和开展的  





# Lettuce 7 IPsec & IKE

## 网络层安全协议：IPsec

### IP级安全性

- IPsec保证了IP级的安全性，包括：
  - 认证
  - 保密
  - 密钥管理

- 现有IP协议的安全特性：
  - 无连接，不保证顺序到达；存在着重复包、丢失包；设备简单、无状态  
  - 所提供的安全服务：无认证、完整性、保密性，基于IP地址的访问控制，不完备

- IPsec的原理在于可以在IP层加密和/或认证所有流量
- IPsec可以在主机、防火墙或路由器上实施

### IPsec：文档

- IPsec文档：

  - 重要的有1998年发布的RFC 2401/2402/2406/2408  
  - 整个IPsec文档被分为7个部分：
    - 体系结构
    - 认证头AH
    - 封装安全载荷ESP
    - 加密算法
    - 认证算法
    - 密钥管理
    - 解释域

  - <img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121052716286.png" alt="image-20221121052716286" style="zoom:50%;" />

### IPsec提供的服务

<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121052844549.png" alt="image-20221121052844549" style="zoom:50%;" />

### 安全关联

- IP认证和保密机制中的一个核心概念是安全关联SA  
- 安全关联SA是IPsec通信双方之间对某些要素的一种协商，一组安全信息参数集合，包括：协议、操作模式、密码算法、认证算法、密钥、密钥生存期等  
- 关联是发送方和接收方之间的单向关系，该关联为双方的通信提供了安全服务  
  - 如果需要双方安全交换，则建立两个安全关联
  - 安全服务可由AH或者ESP提供， 但不能两者都提供  

- 一个安全关联SA由3个参数唯一确定：
  - 安全参数索引SPI：一个和SA相关的位串，仅在本地有意义，由AH和ESP携带，使得接收方能够选择合适的SA处理接收包    
  - IP目的地址IPDA：只允许使用单一地址  
  - 安全协议标识：标识该关联是一个AH安全关联或ESP安全关联  

- 安全关联数据库SADB：包含了（SPI，IPDA，AH/ESP）三元组索引<img src="D:\documents\计算机网络安全技术\NetWorkSaftyNotes\assets\image-20221121054558060.png" alt="image-20221121054558060" style="zoom:50%;" />
