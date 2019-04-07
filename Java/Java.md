# Java 

各个配置文件作用:

https://yq.aliyun.com/articles/2597

##  文件：.project

.project描述了一个Eclipse项目。

##  文件：.classpath

.classpath描述了一个Eclipse项目。

#  /.settings目录下的文件

Eclipse项目.settings目录下的配置比较杂，各种后缀名的都可以见到，绝大多数是文本文件，格式为properties（多数以.prefs为后缀名）或XML（多数以.*、.xml为文件名）格式的为主。下面挨个讲一些典型的文件。

## 文件：.jsdtscope

.jsdtscope文件定义了web项目中的源码路径，也就意味着只有web project才会有这个配置。这些源码Eclipse会进行validate（如果validate没有禁用）。这个文件在实际开发中最大的价值在于定义JS文件的例外路径，在配置界面中配置的话挨个选很烦人。

## 文件：org.eclipse.core.resources.prefs

org.eclipse.core.resources.prefs文件其实就是规定项目内的文件的编码用的。一般来说一个项目里的文件编码需要一致，特别是文件文本内容本身无法指示文件本身编码的（比较绕，XML文件第一行能指示自身编码，CSS也有这个能力但用得不多），尽量不要多种编码同时存在（最好在编码规范中禁止多重编码同时存在的现象发生）

## org.eclipse.jdt.core.prefs

org.eclipse.jdt.core.prefs文件指定了一些Java编译的特性，比如Java版本之类的，看文件每一行的key能猜出具体的用处。

## 文件：org.eclipse.m2e.core.prefs

org.eclipse.m2e.core.prefs是一些maven相关的配置。

## 文件：org.eclipse.wst.common.component

org.eclipse.wst.common.component文件规定了项目怎么组装成一个webapp，这里可以玩很多种组装方式。

## 文件：org.eclipse.wst.common.project.facet.core.xml

org.eclipse.wst.common.project.facet.core.xml指示了项目中**启用那些facet及facet的版本**。





