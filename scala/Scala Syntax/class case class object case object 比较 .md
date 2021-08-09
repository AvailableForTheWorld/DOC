# class与case class

class 必须new 实例类

case class 直接默认带有apply，自动实现了new 功能

case class 一般用于val 不可变数值变量

case class 自带unapply用于模式匹配

//TODO最好配上代码说明

# trait

Trait 是一种接口 一般用于class类来继承而不是来定义成员函数 

类可以多重继承trait// TODO 怎么继承？写个demo



# object与class

对象，定义类的实例，即：

​	类中函数无法自己运行，在工程中必须指定一个main方法来运行程序类

companion object配合来互相访问内部private变量

//TODO 伴生对象和伴生类的定义是什么

//TODO 代码说明

# case object 与object

没有构造参数 

类似于与class 与 case class，拥有比object更多的特性：序列化 默认哈希值 增强tostring实现

用于枚举对象以及作为消息使用即在另外的地方选择多个 case object

