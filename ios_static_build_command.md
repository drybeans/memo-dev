iOS开发中，经常需要对静态库进行操作，以下是几个常用的静态库操作命令。
合并模拟器库文件和真机库文件
######lipo -create -output lib.a lib-armv6.a lib-i386.a
其中lib.a是合并后的输出文件，lib-armv6.a和lib-i386.a分别对应真机静态库和模拟器静态库文件。

查看静态库中包含哪些架构
######lipo -info lib.a
该命令可以查看静态库中包含哪些架构，如armv7和i386。

解压出指定架构的静态库
######lipo -extract_family armv7 -output lib-armv7.a lib.a
或者
######lipo lib.a -thin armv7 -output lib-armv7.a
以上命令可以从lib.a静态库中解压出armv7架构的静态库lib-armv7.a，可以以同样的方式解压出针对模拟器的架构库文件(如i386)。

将a格式的静态库解压为o文件
######ar -x lib.a
以上命令可以解压出lib.a中的所有o文件。

将o文件合并为a文件
######libtool -static -o lib.a *.o
与上一个解压命令相反，这个命令将所有o文件合并为一个a文件，这两个命令常用于多个项目中引用的a库存在冲突时(duplicate symbol)解决冲突的一种方式。

转自http://www.apkbus.com/android-127500-1-1.html
