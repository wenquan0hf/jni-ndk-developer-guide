# JNI 开发流程

## 开发流程

JNI 全称是 Java Native Interface（Java 本地接口）单词首字母的缩写，本地接口就是指用 C 和 C++ 开发的接口。由于 JNI 是 JVM 规范中的一部份，因此可以将我们写的 JNI 程序在任何实现了 JNI 规范的 Java 虚拟机中运行。同时，这个特性使我们可以复用以前用 C/C++ 写的大量代码。

开发 JNI 程序会受到系统环境的限制，因为用 C/C++ 语言写出来的代码或模块，编译过程当中要依赖当前操作系统环境所提供的一些库函数，并和本地库链接在一起。而且编译后生成的二进制代码只能在本地操作系统环境下运行，因为不同的操作系统环境，有自己的本地库和 CPU 指令集，而且各个平台对标准 C/C++ 的规范和标准库函数实现方式也有所区别。这就造成使用了 JNI 接口的 JAVA 程序，不再像以前那样自由的跨平台。如果要实现跨平台，就必须将本地代码在不同的操作系统平台下编译出相应的动态库。

JNI 开发流程主要分为以下6步：

- 编写声明了 native 方法的 Java 类
- 将 Java 源代码编译成 class 字节码文件
- 用 javah -jni 命令生成`.h`头文件（javah 是 jdk 自带的一个命令，-jni 参数表示将 class 中用native 声明的函数生成 JNI 规则的函数）
- 用本地代码实现`.h头`文件中的函数
- 将本地代码编译成动态库（Windows：\\\*.dll，linux/unix：\\\*.so，mac os x：\\\*.jnilib）
- 拷贝动态库至 java.library.path 本地库搜索目录下，并运行 Java 程序

![](images/workflow1.png)

通过上面的介绍，相信大家对 JNI 及开发流程有了一个整体的认识，下面通过一个 HelloWorld 的示例，再深入了解 JNI 开发的各个环节及注意事项。

### HelloWorld

>注意：这个案例用命令行的方式介绍开发流程，这样大家对 JNI 开发流程的印象会更加深刻，后面的案例都采用eclipse+cdt 来开发。

第一步，新建一个 HelloWorld.java 源文件

public class HelloWorld {

	public static native String sayHello(String name); 	// 1.声明这是一个native函数，由本地代码实现

	public static void main(String[] args) {
		String text = sayHello("yangxin");	// 3.调用本地函数
		System.out.println(text);
	}

	static {
		System.loadLibrary("HelloWorld");	// 2.加载实现了native函数的动态库，只需要写动态库的名字
	}

}