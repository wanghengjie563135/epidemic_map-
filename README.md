# 搞定毕设|基于SSM+jsp+echarts的疫情地图系统系统（已经开源）

# 一、前言

&#x20;  2022毕业季，特别是软件工程，计算机专业的同学他们的毕业设计主要以开发网站为主，我在2022年3月至今，也参与了一些小项目的开发，可以用做毕业设计，其中包含：企业报销管理系统,垃圾回收系统，物业管理系统，汉服商城，住院管理系统，图书商城系统，疫情下线上考试系统，疫情地图系统共计8个系统的开发，将在今年7月份陆续全部进行开源，供以后学弟学妹毕业设计参考，今天开源的一个项目是基于SSM+jsp+echarts的疫情地图系统，本系统使用Java作为主要的编程语言编程开发，后台以SSM框架作为主要的技术支撑，数据库采用采用MySQL，前端采用JSP同时配合JavaScript语言。开发环境：JDK8+IDEA+MySQL8.0

在这个项目合适才学完ssm框架的同学练习使用，就是一个小demo，数据库只有3张表，如果感兴趣的同学可以参考源码：

基于SSM+jsp+echarts的疫情地图系统源代码在githee仓库：[https://gitee.com/wanghengjie563135/epidemic\_map.git](https://gitee.com/wanghengjie563135/epidemic_map.git "https://gitee.com/wanghengjie563135/epidemic_map.git")

# 二、项目实现细节

### 1、整个项目实现功能

1）图表展示：到目前为止，全国疫情分布图、扇形图、柱状图和表格。
2）数据录入：录入各个省份的确诊人数、疑似人数、隔离人数、治愈人数和死亡人数。
3）数据查询：展示录入疫情数据的各个省份的确诊人数、疑似人数、隔离人数、治愈人数和死亡人数，以及查询输入省份的疫情数据。
4）用户录入：录入用户信息，包括账号、用户名和密码，使用账号和密码可以登录后台进行数据管理和系统管理。
5）用户编辑：查询和修改用户的信息。

6\) 全球的疫情信息获取，实时更新

7\)关于疫情最新的新闻获取，实时更新

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_V6_9-yMB12.png)

### 2、开发环境

| **分类**     | **名称**                                                     | **语种** |
| ------------ | ------------------------------------------------------------ | -------- |
| 操作系统     | windows10                                                    | 简体中文 |
| 数据库平台   | MySQL Server 8.0+                                            |          |
| 应用服务器   | apache-tomcat-8.5.71                                         |          |
| java开发工具 | idea                                                         |          |
| 框架         | mybatis+Spring+SpringMVC                                     |          |
| 项目名称     | 基于SSM+jsp+echarts的疫情地图系统系统                        |          |
| 实现技术     | mybatis+Spring+SpringMVC+mysql+Servlet+jquery+bootStrap+js+Maven+tomcat+echarts等技术 |          |

### 3、数据库表设计

```sql

```

### 3、Maven导入项目所依赖的jar包

```xml

```

# 三、具体功能实现

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_H8tf6H44xO.png)

### 1、登录功能

这里根据数据库判断del\_flag,如果是0代表管理员登录进入管理员页面，如果是1代码用户登录，进入用户界面

```java
@RequestMapping("/input")
    public String userInput(UserInfo userInfo,Model model){
        userInfo.setDelFlag(1);
        System.out.println(userInfo);
        userService.userInput(userInfo);
        model.addAttribute("msg1","用户录入成功！");
        return "admin/user_input";
    }
```

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_yC6B-FNbKB.png)

### 2、用户功能

```java
/**
 * @author tjcu
 * @date 2022/5/15 - 14:48
 */
@Controller
@RequestMapping("/province")
public class ProvinceController {
    @Autowired
    private ProvinceService provinceService;

    @ResponseBody //只返回数据，不返回视图
    @RequestMapping("/ajax/noDataList")
    public AjaxResponseInfo noDataProvinceList(String date){
        System.out.println("ProvinceController "+date);
        AjaxResponseInfo ajaxResponseInfo = new AjaxResponseInfo();

        if(!StringUtils.isEmpty(date)){
            //表示页面的日期有效
            //使用服务层的对象调用服务层的方法
            List<ProvinceInfo> provinceInfos = provinceService.noDataProvinceList(date);
            ajaxResponseInfo.setCode(0);
            ajaxResponseInfo.setMsg("请求成功");
            ajaxResponseInfo.setData(provinceInfos);
        }else{
            //表示页面没有提交日期
            ajaxResponseInfo.setCode(-1);
            ajaxResponseInfo.setMsg("请求参数有误");
        }
        return ajaxResponseInfo;
    }
}
```

*   第一个页面是国内疫情，需要管理员进行输入当前国内疫情，然后在用户界面显示

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_ortWOG0DCL.png)

*   新冠病毒，实时更新国内最新新闻

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_YDt1Aqfb7e.png)

*   世界疫情，更新全球疫情

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_812hHeZEhn.png)

### 2、管理员功能

*   管理员功能详情

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_vBi3rHfELG.png)

*   管理员收页就是欢迎进入系统

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_QreYtNuiPL.png)

*   点击数据录入，可以各个省市录入

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_Ls88gVeeBX.png)

*   数据查询

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_s0UcNcChsn.png)

*   图表展示功能

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_qdLthsPUZY.png)

*   用户录入功能

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_6HKLAHjd3G.png)

*   修改用户功能

![](https://csdn-image.oss-cn-beijing.aliyuncs.com/img/image_n4kqjLHtc4.png)

基于SSM+jsp+echarts的疫情地图系统源代码在githee仓库：[https://gitee.com/wanghengjie563135/epidemic\_map.git](https://gitee.com/wanghengjie563135/epidemic_map.git "https://gitee.com/wanghengjie563135/epidemic_map.git")
