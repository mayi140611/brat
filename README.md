# brat
brat标注工具

## 配置brat
brat中分了4类标注实体：entity，event，relation，attribute。
在annotation.conf文件中配置

实体的颜色在visual.conf中

搜索引擎配置在tools.conf中

用户名和密码的配置在config.py中，可以配置多个用户名和密码

## 启动
首先, `sh install.sh`初始化环境并设置用户名和密码
启动服务器：python standalone.py [port]
如果不设置端口号，默认的端口号是8001
## 添加标注语料
把需要标注的文件放到data文件夹下，以txt文本格式。
标注过程中会生成一个同名的.ann文件


brat的功能很全，基本可以满足标注实体和关系的需求
如一个.ann的文件内容如下：
```
T14	症状 228 230	头晕
T15	症状 254 256	物过
R4	拥有 Arg1:T12 Arg2:T8	
R5	拥有 Arg1:T12 Arg2:T9	
R6	拥有 Arg1:T3 Arg2:T11	
T16	疾病 196 198	发热
#1	AnnotatorNotes T16	1
R7	拥有 Arg1:T16 Arg2:T13	
T17	疾病 119 123	后夜尤甚
#2	AnnotatorNotes T17	5555555555555555
A1	修饰 T17 待证实的
A2	有条件的 T17
```
以`T14	症状 228 230	头晕`为例：
T14：T表示这个标注是一个entity，14表示这是标注的第14个entity，那么T14可以看做是实体的唯一ID
症状：表示entity的名称
228 230：表示实体在全文中的位置索引
头晕：表示标注的实体内容

以`R4	拥有 Arg1:T12 Arg2:T8`为例：
R4：R表示标注的是relation
拥有：表示relation的名称
用neo4j的表示方法：(T12)-[:拥有]->(T8)

以`A1	修饰 T17 待证实的`为例：
A：表示这是一个属性
修饰：表示属性的名称
待证实的：表示属性的具体值
这个例子的意思：entity T17有个属性是修饰，具体值为：待证实的
当然，属性下面也可以没有具体值，如`A2	有条件的 T17`


以`#2	AnnotatorNotes T17	5555555555555555`为例：
`#`：表示这是一个注释
这段合起来表示T17的注释为5555555555555555