Kotlin第二学
基础语法
怎么定义一个类
使用class关键字即可

	class MainActivity{
		···	
	}
它有一个默认的唯一的构造器，大部分情况下我们只需要这个默认构造器。其次你只需要在类名后面写上它的参数；如果这个类没有任何内容，我们可以省略大括号：

	class Person(name:String,id:Int)
如果构造函数有函数体，那么写在哪呢？你可以写在init块里面：

	class Person(name:String,id:Int){
		init{
			···		
		}
	}

类继承
默认任何类都是基础继承自Any（与java中的Object类似），但是我们可以继承其它类。所有的类默认都是不可继承的（final），所以我们只能继承那些明确声明open或者abstract的类：

	open class Animals(name:String)
	class Person(name:String,id:Int):Animals(name)

函数
函数，即方法，可以用fun关键字来定义：
	
	fun onCreate(savedInstanceState：Bundle?){
	}
如果没有指定它的返回值，它就会返回Unit，与java中的void相似，但是Unit是一个真正的对象。你也可以指明明确类型的返回值
			
	fun add(x:Int,y:Int):Int{
		return x+y
	}
当然，你也可以这样写：

	fun add(x:Int,y:int):Int = x + y
这个时候你应该注意到了，所有的函数体里面都没有分号";"隔开，你当然也可以自己加上去，没问题的

函数参数
在Kotlin中，我们可以在函数传参时给参数设定默认值，这样可以使得方法传参更具灵活性

	fun toast(message：String，length：Int = Toast.LENGTH_SHORT){
		Toast.makeText(this,message,length).show()	
	} 
调用时，我们可以这样用：

	toast(“Hello”)
	toast(“Hello”,Toast.LENGTH_SHORT)

String模板表达式
你可以在String中直接使用模板表达式，它可以帮助你很简单地在静态值和变量的基础上编写复杂的String，比如：

	fun niceToast(message:String,tag:String = javaClass<MainActivi().getSimpleName(),
				length:Int = Toast.LENGTH_SHORT>){
		Toast.makeText(this,"[$className] $message",length).show()
	}
其中就使用了"[$className]$message"。如你所见，任何时候你使用一个"$"符号就可以插入一个表达式，如果这个表达式有一点复杂，你就需要使用一对大括号括起来:"Your name is ${user.name}"

