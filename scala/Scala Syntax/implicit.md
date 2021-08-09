# implicit

## 隐式参数：

通过设置一个隐式值当函数调用时缺省时去作用域找

通过在方法中声明一个隐式参数 当调用缺省此参数时进行作用域的搜寻找到相关类型数据进行赋值操作

```scala
def speak(x:Int)(implicit m:String):Unit = {
  println(s"you are a $x years old $m");
}
```



## 隐式转换：

通过隐式方法或者函数或者隐式类将一个类型的值转换成另一个类型的值

1. 隐式值：在作用域范围内创建一个隐式变量，当一个方法缺省这个变量类型的值时会以这个隐式变量填充

```scala
implicit val p = "hello,world"
def person(implicit val name:String):String = {
  s"name: $name"
}
person
```



2. 隐式方法：在作用域范围内定义一个隐式方法，当传入的参数类型不是形参类型时用定义的隐式方法进行类型转换成目标类型

```scala
implicit def int2string(x:Int):String = {
  ""+x
}
def gotScore(x:String):Unit={
  println(s"you've got $x scores");
}
gotScore(100)
```



3. 隐式类：定义一个隐式类，当一个类中使用了隐式类中的方法而自己却不包含时使用隐式类作为自己的方法调用

```scala
class N {}
object Main extends App{
  implicit class PrintRes(var m:N) {
    def speak():Unit = {
      println("you have finished!!!")
    }
  }
  var k = new N;
  k.speak()
}
```



## 隐式作用域

### 优先级顺序访问

1. 当前代码的作用域的隐式实体：隐式变量隐式方法隐式类
2. 去相关联作用域查找隐式类型T：
   1. 复合类型：T with A with B with C 若T没有隐式实体则去A，B，C中去查找
   2. T为参数化类型则去引用该类型的相关类型查找 List[T]去搜索List类型中的隐式实体
   3. T属于某个对象，访问这个对象的所用内容
   4. 类型注入S#T则S与T都搜索？？？

