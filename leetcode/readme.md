# how to be a coder

<p align="right"><font color=red size =4 ><i>HIK</i></font><font size=4><i>VISION</i></font></p>

##Spring Boot 在Linux部署流程 


<font color=blue>部门</font>：海康威视研究院/大数据技术部/多维大数据挖掘组/原型组/挖掘平台组

----------
写在前面：spring Boot Demo可参考该文章：[https://blog.csdn.net/soldier_123/article/details/78966185](https://blog.csdn.net/soldier_123/article/details/78966185 "如何用IDEA创建第一个Spring Boot项目")

本文中所使用的程序对该文章代码进行了DIY。

----------

1.连接Linux服务器，查看spring Boot默认端口是否占用
    
    netstat -anp|grep 8080 

若已占用更改application.properties设置为未被占用的端口

![](http://p89by23ep.bkt.clouddn.com/duankou.PNG)
 	
2.我们先将pom中的 war 改成 jar保存。

![](http://p89by23ep.bkt.clouddn.com/01-jar.PNG)

3.利用IDEA 命令行或者windows cmd命令框(转到目录下)，输入mvn clean package.

![](http://p89by23ep.bkt.clouddn.com/02-package.PNG)

成功打包，位置在项目的target文件夹下。

4.将jar包上传到服务器（Xshell中采用 **rz**）

使用命令启动项目。命令是：

    java -jar firstboot-0.0.1-SNAPSHOT.jar(上传的jar包)。

<font color=red>注意:</font>这里运行会出现无法连接Apache的问题，需要将maven的settings.xml文件添加mirror，本文使用的海康的镜像，也可使用其他。

![](http://p89by23ep.bkt.clouddn.com/run%20jar.PNG)




5.浏览器输入：http://服务器ip:8085/hello/Sayhello

![](http://p89by23ep.bkt.clouddn.com/%E6%B5%8F%E8%A7%88%E5%99%A8.PNG)

参考资料：

1. Spring boot 初次探访与服务器部署
[https://blog.csdn.net/Zebra_916/article/details/78487454?locationNum=4&fps=1](https://blog.csdn.net/Zebra_916/article/details/78487454?locationNum=4&fps=1 "Spring boot 初次探访与服务器部署")

2. Intellij IDEA 打包jar的多种方式
[https://blog.csdn.net/Thousa_Ho/article/details/72799871?locationNum=5&fps=1](https://blog.csdn.net/Thousa_Ho/article/details/72799871?locationNum=5&fps=1 "Intellij IDEA 打包jar的多种方式")

3. LINUX中如何查看某个端口是否被占用 
[https://www.cnblogs.com/hindy/p/7249234.html](https://www.cnblogs.com/hindy/p/7249234.html "LINUX中如何查看某个端口是否被占用")

4. Xshell实现Windows上传文件到Linux主机
[https://blog.csdn.net/shenjianxz/article/details/56686449](https://blog.csdn.net/shenjianxz/article/details/56686449 "Xshell实现Windows上传文件到Linux主机")

![](http://p89by23ep.bkt.clouddn.com/%E7%82%B9%E5%88%B0%E8%B6%85%E5%B9%B3%E9%9D%A2%E7%9A%84%E8%B7%9D%E7%A6%BB.PNG)
