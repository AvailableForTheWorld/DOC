# YML

## YAML 定义

YAML不是一种标记语言 yet anoter markup language

- 大小写敏感
- 缩进表示层级关系
- 缩进只用空格不用tab
- 相同层级的元素左对齐，缩进空格数不重要
- #号表示注释

## 数据类型

 - 对象（键值对）

   ​	格式一：

   ​				key: value.     #注意key与value之间的空格

   ​	格式二：

   ​				key:{key1: value, key2: value, ...}

   ​	格式三：

   ​				key:

   ​						key1: value

   ​						key2: value2

   ​	格式四：

   ​				?    #注意问号后面有一个空格

   ​					- complexkey1

   ​					- complexkey2

   ​				:   #注意冒号后面有一个空格

   ​					- complexkey1

   ​					- complexkey2	



 - 数组（序列，列表）

   格式一： 

   ​	- 开头

   

   格式二：

   ​	-

   ​		- A

   ​		- B

   ​		- C



 - 纯量（单个不可再分的值）

   ```yml
   boolean: 
       - TRUE  #true,True都可以
       - FALSE  #false，False都可以
   float:
       - 3.14
       - 6.8523015e+5  #可以使用科学计数法
   int:
       - 123
       - 0b1010_0111_0100_1010_1110    #二进制表示
   null:
       nodeName: 'node'
       parent: ~  #使用~表示null
   string:
       - 哈哈
       - 'Hello world'  #可以使用双引号或者单引号包裹特殊字符
       - newline
         newline2    #字符串可以拆成多行，每一行会被转化成一个空格
   date:
       - 2018-02-17    #日期必须使用ISO 8601格式，即yyyy-MM-dd
   datetime: 
       -  2018-02-17T15:02:31+08:00    #时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区
   ```

- 引用

  **&** 锚点和 ***** 别名，可以用来引用:

  ```yml
  defaults: &defaults
    adapter:  postgres
    host:     localhost
  
  development:
    database: myapp_development
    <<: *defaults
  
  test:
    database: myapp_test
    <<: *defaults
  ```

  相当于:

  ```yml
  defaults:
    adapter:  postgres
    host:     localhost
  
  development:
    database: myapp_development
    adapter:  postgres
    host:     localhost
  
  test:
    database: myapp_test
    adapter:  postgres
    host:     localhost
  ```

  **&** 用来建立锚点（defaults），**<<** 表示合并到当前数据，***** 用来引用锚点。

- 



# properties



## Properties文本格式



- 以!或#开头的行将作为comment注释行 

\# this is a comment

! this is a comment

 

- 一行一个键值对
- 键值对以下面4种字符分隔：[=, :, 空格, tab制表符]

key:value

key=value

key   value

key　　　　　　value

 

- [=, :]作为键字符，需要插入转移符 \

\# 键为"key1:key2"

key1\:key2=value

\# 键为"key1=key2"

key1\=key2=value

 

- 忽略所有非实际意义的空格和制表符 

​     \# 下面所有键值对格式意义相等

key=value

key    =   value

​     key    :value

 

- 值过长时支持分行书写，在值末尾插入转移符 \ 

\# 转移符 \ 后至下一有效值字符直接的所有空格将忽略不计

key = verylonglong\

​     longlonglong\

​     longlonglongvalue

 

- 值可不书写，视为空字符串 

\# 下面键key均关联到空字符串

key=

key

 

- 非ASCII字符需要使用Unicode转义序列 

\# “中文” 转义为 \u4E2D\u6587

key \u4E2D\u6587