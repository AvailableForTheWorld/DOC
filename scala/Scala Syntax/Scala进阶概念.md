# 柯里化

​	将一个函数作用域的参数拆成单独的参数作用域的集合，使之少一个参数的函数结果是多一个参数的匿名函数

如：

```scala
def add(x:Int,y:Int):Int = x+y;
//写成柯里化后
def add(x:Int)(y:Int):Int = x+y;//相当于 def add(x:Int)=(y:Int)=>x+y;
var res = add(1); //res 为匿名函数(y:Int)=1+y;
var sum = res(2);// 3
```



# 序列化与反序列化



序列化是将对象数据转化成Json格式数据传输，反序列化则反之

