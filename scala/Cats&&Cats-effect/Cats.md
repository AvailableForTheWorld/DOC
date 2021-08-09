# cats











## type class

类型类：创建一个trait来声明抽象方法，在根据不同的实例来定义不同的方法

比如

```scala
trait Eq[T]{
  def eq(a:T,b:T):Boolean
}
object EqInstance{
  implicit val intEq = new Eq[Int]{
    override def eq (a:Int,b:Int) = a==b
  }
  implicit val stringEq = instance[String]((a,b)=>a.equals(b))
  def instance[T](func:(T,T)=>Boolean):Eq[T] = new Eq[T]{
    override def eq (a:T,b:T) = func(a,b)
  }
}
object Same {
  def same[T](a:T,b:T)(implicit eq:Eq[T]):Boolean = eq.eq(a,b)
}
```

