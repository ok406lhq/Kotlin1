Kotlin第一学
---
什么是Kotlin
Kotlin，它是JetBrains开发的基于JVM的语言。补充一下JetBrains，JetBrains公司是一个吊炸天的公司，起先开发的IntelliJ IDEA被认为是世界上最好的java开发工具之一，后来基于该IDE开发创造了Android Studio，被谷歌列为官方安卓开发IDE（实际上是基于Intellij，作为该平台的一个插件）。而后开发了Kotlin。

（以下摘自官方文档）
Kotlin的特点
Kotlin是使用Java开发者的思维被创建的，Intellij作为它的主要开发IDE。碎玉Android开发者，有两个有趣的特点：
1、对Java开发者来说，Kotlin是非常直觉化的，而且非常容易学习。语言的大部分内容都是与我们知道的非常相似，不同的地方，它的基础概念也能迅速地掌握它
2、它与我们日常生活使用的IDE无需配置就能完全整合。Android Studio能够非常完美地理解、编译运行Kotlin代码。而且对这门语言的支持正是来自于开发了这个IDE的公司本身，所以我们Android开发者是一等公民

----

但是这仅仅是开发语言和开发工具之间的整合。相比Java 7的优势到底是什么呢？

----
1、它更加易表现：这是它最重要的有点之一。你可以编写少得多的代码
2、他更加安全：Kotlin是空安全的，也就是说我们在编译时期就处理了各种null的情况，避免了执行时异常，如果一个对象可以是null，则我们需要明确地指定它，然后在使用它之前检查它是否是null。你可以节约很多调试空指针异常的时间，解决掉null引发的bug。
3、它是函数式：Kotlin是基于面向对象的语言。但是就如其他很多现代的语言那样，它使用了很多函数式编程的概念，比如，在使用lambda表达式来更方便地解决问题。其中一个很棒的特性就是Collections的处理方式。
4、它可以扩展函数：这意味着我们可以扩展类的更多特性，甚至我们没有权限去访问这个类中的代码。
5、它是高度互操作性的：你可以继续使用所有的你用Java写的代码和库，因为两个语言之间的互操作性是完美的。甚至可以在一个项目中使用Kotlin和Java两种语言混合编程。

---

第一个Kotlin项目
首先，打开Android Studio并选择File -> New -> New Project，取名任意，选择版本，一路next，最后选择一个Activity模板作为入口，这里选择Empty Activity
接着要导入Kotlin相关的配置
![](http://wx4.sinaimg.cn/mw690/7e86a892gy1fhcqc6mybej20su0jh76y.jpg)
选择Kotlin，点击Install（以前版本可能有两个Kotlin、kotlin extensions for android，现在Android Studio把它们整个到一起了）慢慢等待下载完成

接着可以手动在父子build.gradle文件中配置Gradle；或者，你可以跟我一样偷懒：
![](http://wx4.sinaimg.cn/mw690/7e86a892gy1fhcqg2r4jjj20m80aa75b.jpg)
检查配置文件会发现gradle配置多了几行代码：
Project视图下的build.gradle：
    
	buildscript {
	    ext.kotlin_version = '1.1.3-2'
	    repositories {
	        jcenter()
	    }
	    dependencies {
	        classpath 'com.android.tools.build:gradle:2.3.3'
	        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
	
	        // NOTE: Do not place your application dependencies here; they belong
	        // in the individual module build.gradle files
	    }
	}

Module视图下的build.gradle：
    apply plugin: 'com.android.application'
	apply plugin: 'kotlin-android'
	apply plugin: 'kotlin-android-extensions'
	
	android {
	    compileSdkVersion 25
	    buildToolsVersion "25.0.1"
	    defaultConfig {
	        applicationId "app.lhq.com.weatherapp"
	        minSdkVersion 15
	        targetSdkVersion 25
	        versionCode 1
	        versionName "1.0"
	        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
	    }
	    buildTypes {
	        release {
	            minifyEnabled false
	            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
	        }
	    }
	}
	
	dependencies {
	    compile fileTree(dir: 'libs', include: ['*.jar'])
	    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
	        exclude group: 'com.android.support', module: 'support-annotations'
	    })
	    compile 'com.android.support:appcompat-v7:25.3.1'
	    compile 'com.android.support.constraint:constraint-layout:1.0.2'
	    testCompile 'junit:junit:4.12'
	    compile "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"
	}
	repositories {
	    mavenCentral()
	}

简单写一下布局文件activity_main.xml:
	   
	<TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World"/>

把MainActivity转换成Kotlin代码
Kotlin plugin包含了一个有趣的特性，它能把Java代码转成Kotlin代码。我们在MainActivity.java类中使用它。
打开文件，然后选择Code -> Convert Java File to Kotlin File。然后在MainActivity代码中可以看到

	import android.os.Bundle
	import android.support.v7.app.AppCompatActivity
	
	
	class MainActivity : AppCompatActivity() {
	
	    override fun onCreate(savedInstanceState: Bundle?) {
	        super.onCreate(savedInstanceState)
	        setContentView(R.layout.activity_main)
	    }
	}
我们也可以手动import资源，然后直接使用布局文件中声明id的组件，而不用findViewById，这有效减少了我们编写的代码量，代码如下:

	import android.os.Bundle
	import android.support.v7.app.AppCompatActivity
	import kotlinx.android.synthetic.main.activity_main.*;
	
	class MainActivity : AppCompatActivity() {
	
	    override fun onCreate(savedInstanceState: Bundle?) {
	        super.onCreate(savedInstanceState)
	        setContentView(R.layout.activity_main)
	        textView.text = "Hello Kotlin"
	    }
	}

运行程序，界面如下：
![http://wx3.sinaimg.cn/mw690/7e86a892gy1fhcrk2n0czj20g40ri0sv.jpg](http://wx3.sinaimg.cn/mw690/7e86a892gy1fhcrk2n0czj20g40ri0sv.jpg)
