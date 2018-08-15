# 3 搭建Spring框架的过程

## 3.1 导入Spring的jar包

1: 在eclipse中新建工程"spring"  
2: 并在工程中创建文件夹lib  
3: 将spring的jar包放入lib文件夹中并进行“add to build path”操作

## 3.2 编写主配置文件（applicationContext.xml）

创建资源文件夹“resource”，并在该文件夹中创建“applicationContext.xml”配置文件。

创建一个名为“黄鼠狼”的java类：

	package com.marshal.ioc;
	
	public class YelloMouseWolf {
	
	    public YelloMouseWolf() {
	        System.out.println("YelloMouseWolf..........哈哈一只黄鼠狼出生了");
	    }
	
	    public void behavior() {
	        System.out.println("偷鸡");
	    }
	}

在该类中有一个无参的构造方法，该方法便于在创建对象时直接被调用。另外，还创建了一个对象的行为方法。

在主配置文件“applicationContext.xml”中对类容器的配置进行编写：

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans"
	       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	       xsi:schemaLocation="http://www.springframework.org/schema/beans
	           http://www.springframework.org/schema/beans/spring-beans-2.5.xsd">
	           
	    <!-- 
	        bean：将一个类的对象创建过程交给spring容器
	        class：指定类的具体路径
	        id：唯一标识符
	    -->       
	    <bean id="yelloMouseWolf" class="com.marshal.ioc.YelloMouseWolf"></bean>
	  
	</beans>

以上配置文件将com.marshal.ioc.YelloMouseWolf类以实例名为yelloMouseWolf的方式配置在了Spring主配置文件中。

## 3.3 启动框架测试

创建一个启动类“Window.java”：

	package com.marshal.ioc;
	
	import org.springframework.context.ApplicationContext;
	import org.springframework.context.support.ClassPathXmlApplicationContext;
	
	public class Window {
	
	    public static void main(String[] args) {
	    
	        // 1、启动框架(context代表spring容器)
	        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
	        
	        // 2、获取spring容器中创建的对象(通过id值获取)
	        YelloMouseWolf yello1 = (YelloMouseWolf) context.getBean("yelloMouseWolf");
	        YelloMouseWolf yello2 = (YelloMouseWolf) context.getBean("yelloMouseWolf");
	        
	        yello1.behavior();
	        yello2.behavior();
	        
	        System.out.println(yello1 == yello2);
	        System.out.println(yello1.equals(yello2));
	    }
	
	}

该类通过启动的Spring容器来创建类的实例，运行结果如下：

	YelloMouseWolf..........哈哈一只黄鼠狼出生了
	偷鸡
	偷鸡
	true
	true

从运行结果可以看出，该Spring容器只创建了一个实例，并将该实例的引用地址分别赋值给了两个引用地址变量，因此这两个实例是相同的。