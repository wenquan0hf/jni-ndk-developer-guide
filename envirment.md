# Android NDK 开发环境

## NDK 开发环境的搭建

### 下载安装 Android NDK

　　地址：http://developer.android.com/sdk/ndk/index.html

### 下载安装 cygwin

由于 NDK 编译代码时必须要用到 make 和 gcc，所以你必须先搭建一个 linux 环境， cygwin 是一个在windows 平台上运行的 unix 模拟环境,它对于学习 unix/linux 操作环境，或者从 unix 到 Windows 的应用程序移植，非常有用。通过它，你就可以在不安装 linux 的情况下使用 NDK 来编译 C、C++ 代码了。下载地址：http://www.cygwin.com

- 然后双击运行吧，运行后你将看到安装向导界面。
- 点击下一步,此时让你选择安装方式：Install from Internet：直接从 Internet 上下载并立即安装（安装完成后，下载好的安装文件并不会被删除，而是仍然被保留，以便下次再安装）。Download Without Installing：只是将安装文件下载到本地，但暂时不安装。Install from Local Directory：不下载安装文件，直接从本地某个含有安装文件的目录进行安装。
- 选择第一项，然后点击下一步。
- 选择要安装的目录，注意，最好不要放到有中文和空格的目录里，似乎会造成安装出问题，其它选项不用变，之后点下一步。
- 上一步是选择安装cygwin的目录，这个是选择你下载的安装包所在的目录，默认是你运行setup.exe的目录，直接点下一步就可以。
- 此时你共有三种连接方式选择：Direct Connection：直接连接。Use IE5 Settings：使用IE的连接参数设置进行连接。Use HTTP/FTP Proxy：使用HTTP或FTP代理服务器进行连接（需要输入服务器地址、端口号）。
用户可根据自己的网络连接的实情情况进行选择，一般正常情况下，均选择第一种，也就是直接连接方式。然后再点击“下一步”。
- 这是选择要下载的站点，选择后点下一步。
- 此时会下载加载安装包列表
- Search 是可以输入你要下载的包的名称，能够快速筛选出你要下载的包。那四个单选按钮是选择下边树的样式，默认就行，不用动。View 默认是 Category，建议改成 full 显示全部包再查，省的一些包被隐藏掉。左下角那个复选框是是否隐藏过期包，默认打钩，不用管它就行，下边开始下载我们要安装的包吧，为了避免全部下载，这里列出了后面开发NDK用得着的包：autoconf2.1、automake1.10、binutils、gcc-core、gcc- g++、gcc4-core、gcc4-g++、gdb、pcre、pcre-devel、gawk、make共12个包
- 然后开始选择安装这些包吧，点 skip，把它变成数字版本格式，要确保 Bin 项变成叉号，而 Src 项是源码，这个就没必要选了。
-下面测试一下 cygwin 是不是已经安装好了。

运行 cygwin，在弹出的命令行窗口输入：cygcheck -c cygwin 命令，会打印出当前 cygwin 的版本和运行状 态，如果 status 是 ok 的话，则 cygwin 运行正常。

然后依次输入 gcc –version，g++ --version，make –version，gdb –version 进行测试，如果都打印出版本信息和一些描述信息，则 cygwin 安装成功！

### 配置 NDK 环境变量

- 首先找到 cygwin 的安装目录，找到一个 home\< 你的用户名 >\.bash_profile 文件，我的是：E:\cygwin\home\Administrator\.bash_profile ， ( 注意：我安装的时候我的 home 文件夹下面什么都没有，解决 的办法：首先打开环境变量，把里面的用户变量中的 HOME 变量删掉，在 E:\cygwin\home 文件夹下建立名为 Administrator 的文件夹（是用户名），然后把 E:\cygwin\etc\skel\.bash_profile 拷贝到该文件夹下 ) 。

- 打开 bash_profile 文件，添加`NDK=/cygdrive/< 你的盘符 >/<android ndk 目录 >`例如：

　`NDK=/cygdrive/e/android-ndk-r5`

　`export NDK`

NDK 这个名字是随便取的，为了方面以后使用方便，选个简短的名字，然后保存。

- 打开 cygwin ，输入 cd $NDK ，如果输出上面配置的` /cygdrive/e/android-ndk-r5 `信息，则表明环境变量设置成功了。

### 用 NDK 来编译程序   

- 现在我们用安装好的 NDK 来编译一个简单的程序吧，我们选择 ndk 自带的例子 hello-jni ，我的位于E:\android-ndk-r5\samples\hello-jni( 根据你具体的安装位置而定 ) ，

- 运行 cygwin ，输入命令 cd /cygdrive/e/android-ndk-r5/samples/hello-jni ，进入到 E:\android-ndk-r5\samples\hello-jni 目录。

- 输入 $NDK/ndk-build ，执行成功后，它会自动生成一个 libs 目录，把编译生成的 .so 文件放在里面。 ($NDK是调用我们之前配置好的环境变量， ndk-build 是调用 ndk 的编译程序 )

- 此时去 hello-jni 的 libs 目录下看有没有生成的 .so 文件，如果有，你的 ndk 就运行正常啦！

 

### 在 eclipse 中集成 c/c++ 开发环境

- 装 Eclipse 的 C/C++ 环境插件： CDT ，这里选择在线安装。首先登录 http://www.eclipse.org/cdt/downloads.php ，找到对应你 Eclipse 版本的 CDT 插件 的在线安装地址。

- 然后点 Help 菜单，找到 Install New Software 菜单

- 点击 Add 按钮，把取的地址填进去，出来插件列表后，选 Select All ，然后选择下一步即可完成安装。

- 安装完成后，在 eclispe 中右击新建一个项目，如果出现了 c/c++ 项目，则表明你的 CDT 插件安装成功啦！

 

### 配置 C/C++ 的编译器

- 打开 eclipse ，导入ndk 自带的hello-jni 例子，右键单击项目名称，点击 Properties ，弹出配置界面，之后再点击 Builders ，弹出项目的编译工具列表，之后点击 New，新添加一个编译器，点击后出现添加界面，选择 Program ，点击 OK。

- 出现了添加界面，首先给编译配置起个名字，如： C_Builder，设置 Location 为` < 你 cygwin 安装路径 >\bin\bash.exe `程序，例：`E:\cygwin\bin\bash.exe `，设置 Working Directory 为`<你 cygwin 安装路径 >\bin 目录`，例如： `E:\cygwin\bin`，设置 Arguments 为` --login -c "cd /cygdrive/e/android-ndk-r5/samples/hello-jni && $NDK /ndk-build"`，上面的配置中` /cygdrive/e/android-ndk-r5/samples/hello-jni `是你当前要编译的程序的目录， $NDK 是之前配置的 ndk 的环境变量，这两个根据你具体的安装目录进行配置，其他的不用变， Arguments 这串参数实际是给 bash.exe 命令行程序传参数，进入要编译的程序目录，然后运行 ndk-build 编译程序。

- 接着切换到 Refresh 选项卡，给 Refresh resources upon completion 打上钩。

- 然后切换到 Build Options 选项卡，勾选上最后三项。

- 之后点击 Specify Resources 按钮，选择资源目录，勾选你的项目目录即可。

- 最后点击 Finish，点击 OK 一路把刚才的配置都保存下来，注意：如果你配置的编译器在其它编译器下边，记得一定要点 Up 按钮，把它排到第一位，否则 C 代码的编译晚于Java代码的编译，会造成你的 C 代码要编译两次才能看到最新的修改。

- 编译配置也配置完成啦，现在来测试一下是否可以自动编译呢，打开项目 jni 目录里的 hello-jni.c 文件把提示 Hello from JNI! 改成其他的文字：如： Hello ， My name is alex. ，然后再模 拟器中运行你的程序，如果模拟器中显示了你最新修改的文字，那么 Congratulations ！你已经全部配置成功啦！

 




