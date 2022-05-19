# 疫情数据统计分析系统

#### 介绍
疫情数据统计分析系统是一个基于SSM框架的网页端系统，项目中实现的功能如下：用户访问网站可以浏览全国疫情的图表信息，管理员登录后台管理系统，可以进行数据录入、数据查询、图表展示、用户录入和用户编辑。



功能描述

1）图表展示：到目前为止，全国疫情分布图、扇形图、柱状图和表格。

2）数据录入：录入各个省份的确诊人数、疑似人数、隔离人数、治愈人数和死亡人数。

3）数据查询：展示录入疫情数据的各个省份的确诊人数、疑似人数、隔离人数、治愈人数和死亡人数，以及查询输入省份的疫情数据。

4）用户录入：录入用户信息，包括账号、用户名和密码，使用账号和密码可以登录后台进行数据管理和系统管理。

5）用户编辑：查询和修改用户的信息。



功能结构

![img](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps1.jpg)

系统用例

![img](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps2.jpg) 

![img](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps3.jpg) 

 

项目流程图

![img](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps4.jpg) 

 

E-R图

![img](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps5.png)



#### 软件架构
后端：Spring+SpringMVC+Mybatis

前端：jsp页面

jdk：1.8

开发环境：IDEA

数据库：MySQL 5.7




#### 安装教程

![image-20210330200329136](https://gitee.com/liu_cong11_11/picture/raw/master/img/image-20210330200329136.png)

1.在SQLyog或者Navicat中导入数据库文件，创建数据库和相关表。

2.将代码导入IDEA中

![image-20210330201808356](https://gitee.com/liu_cong11_11/picture/raw/master/img/image-20210330201808356.png)

启动成功，可以在浏览器中访问

![...](https://gitee.com/liu_cong11_11/picture/raw/master/img/image-20210330202837608.png)

地图上没有显示数据，因为需要录入当天各个省份的疫情数据，才能看到。

#### 使用说明

管理员操作

1）登录

![...](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps6.png)

若登录失败，则显示如下：

![...](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps7.png)

2）首页

![...](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps8.jpg)

3）数据录入

![...](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps9.jpg)

4）数据查询

![](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps10.jpg) 

若输入省份，点击查询，则会查询相关省份的疫情信息

![](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps11.jpg)

5）图表展示

全国疫情分布图：

各个省份颜色会随着确诊人数的增加而变深，当鼠标悬停在某个省的地图上时，这个省的颜色会变成黄色，并显示该省的名字和确诊人数。

 ![](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps12.jpg) 

 

扇形图：

![](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps13.jpg) 

表格：

![](C:\Users\DELL\Desktop\GitCode\epidemics\README1.assets\wps14.jpg)

 

当日全国疫情柱状图：

![......](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps15.jpg) 

 

6）用户录入

![......](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps16.jpg) 

若输入账号已存在，会提示用户

![......](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps17.jpg) 

 

7）用户编辑

![......](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps18.jpg) 

管理员输入账号，点击查询，出现如下输入框：

![......](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps19.jpg) 

管理员可以修改用户名和密码，然后点击修改

![......](https://gitee.com/liu_cong11_11/picture/raw/master/img/wps20.jpg) 

 

用户操作

普通用户访问http://localhost:8080/epidemic/，查看全国疫情数据统计信息。和上面图表展示信息相同。




#### 总结

如果有问题，可以在gitee上提问。