# 搞定毕设|基于SSM+jsp+echarts的疫情地图系统系统

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
/*
 Navicat Premium Data Transfer

 Source Server         : windows
 Source Server Type    : MySQL
 Source Server Version : 80022
 Source Host           : localhost:3306
 Source Schema         : epidemic

 Target Server Type    : MySQL
 Target Server Version : 80022
 File Encoding         : 65001

 Date: 19/05/2022 14:03:50
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for epidemics
-- ----------------------------
DROP TABLE IF EXISTS `epidemics`;
CREATE TABLE `epidemics`  (
  `serial_id` int NOT NULL AUTO_INCREMENT,
  `province_id` int NULL DEFAULT NULL,
  `data_year` smallint NULL DEFAULT NULL,
  `data_month` smallint NULL DEFAULT NULL,
  `data_day` smallint NULL DEFAULT NULL,
  `affirmed` int NULL DEFAULT NULL,
  `suspected` int NULL DEFAULT NULL,
  `isolated` int NULL DEFAULT NULL,
  `dead` int NULL DEFAULT NULL,
  `cured` int NULL DEFAULT NULL,
  `user_id` int NULL DEFAULT NULL,
  `input_date` datetime(0) NULL DEFAULT NULL,
  PRIMARY KEY (`serial_id`) USING BTREE,
  INDEX `FK_Reference_1`(`province_id`) USING BTREE,
  INDEX `FK_Reference_2`(`user_id`) USING BTREE,
  CONSTRAINT `FK_Reference_1` FOREIGN KEY (`province_id`) REFERENCES `provinces` (`province_id`) ON DELETE RESTRICT ON UPDATE RESTRICT,
  CONSTRAINT `FK_Reference_2` FOREIGN KEY (`user_id`) REFERENCES `users` (`user_id`) ON DELETE RESTRICT ON UPDATE RESTRICT
) ENGINE = InnoDB AUTO_INCREMENT = 189 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of epidemics
-- ----------------------------
INSERT INTO `epidemics` VALUES (1, 5, 2022, 5, 12, 505, 505, 5051, 1, 5051, 1, '2022-04-05 08:26:45');
INSERT INTO `epidemics` VALUES (75, 81, 2022, 5, 13, 0, 0, 0, 0, 0, 1, '2022-04-13 12:03:25');
INSERT INTO `epidemics` VALUES (77, 44, 2022, 5, 18, 1, 1, 1, 1, 1, 2, '2022-04-18 05:48:02');
INSERT INTO `epidemics` VALUES (78, 45, 2022, 5, 18, 2, 2, 2, 2, 2, 2, '2022-04-18 05:48:02');
INSERT INTO `epidemics` VALUES (79, 46, 2022, 5, 18, 3, 3, 3, 3, 3, 2, '2022-04-18 05:48:02');
INSERT INTO `epidemics` VALUES (80, 50, 2022, 5, 18, 4, 4, 4, 4, 4, 2, '2022-04-18 05:48:02');
INSERT INTO `epidemics` VALUES (81, 51, 2022, 5, 18, 5, 5, 5, 5, 5, 2, '2022-04-18 05:48:02');
INSERT INTO `epidemics` VALUES (82, 52, 2022, 5, 18, 6, 6, 6, 6, 6, 2, '2022-04-18 05:48:02');
INSERT INTO `epidemics` VALUES (83, 5, 2022, 5, 16, 1, 1, 1, 1, 1, 2, '2022-04-18 05:51:29');
INSERT INTO `epidemics` VALUES (84, 12, 2022, 5, 16, 0, 0, 0, 0, 0, 2, '2022-04-18 05:51:29');
INSERT INTO `epidemics` VALUES (85, 13, 2022, 5, 16, 0, 0, 0, 0, 0, 2, '2022-04-18 05:51:29');
INSERT INTO `epidemics` VALUES (86, 14, 2022, 5, 16, 0, 0, 0, 0, 0, 2, '2022-04-18 05:51:29');
INSERT INTO `epidemics` VALUES (87, 15, 2022, 5, 16, 0, 0, 0, 0, 0, 2, '2022-04-18 05:51:29');
INSERT INTO `epidemics` VALUES (88, 21, 2022, 5, 16, 0, 0, 0, 0, 0, 2, '2022-04-18 05:51:29');
INSERT INTO `epidemics` VALUES (89, 5, 2022, 5, 14, 0, 0, 0, 0, 0, 1, '2022-04-18 04:42:46');
INSERT INTO `epidemics` VALUES (90, 12, 2022, 5, 14, 0, 0, 0, 0, 0, 1, '2022-04-18 04:42:46');
INSERT INTO `epidemics` VALUES (155, 5, 2022, 5, 15, 30, 0, 0, 0, 0, 7, '2022-05-15 02:57:48');
INSERT INTO `epidemics` VALUES (156, 12, 2022, 5, 15, 1, 0, 0, 0, 0, 7, '2022-05-15 02:57:48');
INSERT INTO `epidemics` VALUES (157, 13, 2022, 5, 15, 2, 0, 0, 0, 0, 7, '2022-05-15 02:57:48');
INSERT INTO `epidemics` VALUES (158, 14, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:49');
INSERT INTO `epidemics` VALUES (159, 15, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:49');
INSERT INTO `epidemics` VALUES (160, 21, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:49');
INSERT INTO `epidemics` VALUES (161, 22, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:51');
INSERT INTO `epidemics` VALUES (162, 23, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:51');
INSERT INTO `epidemics` VALUES (163, 31, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:51');
INSERT INTO `epidemics` VALUES (164, 32, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:51');
INSERT INTO `epidemics` VALUES (165, 33, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:51');
INSERT INTO `epidemics` VALUES (166, 34, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:51');
INSERT INTO `epidemics` VALUES (167, 35, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (168, 36, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (169, 37, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (170, 41, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (171, 42, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (172, 43, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (173, 44, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (174, 45, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (175, 46, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (176, 50, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (177, 51, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (178, 52, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (179, 53, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (180, 54, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (181, 61, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (182, 62, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (183, 63, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:52');
INSERT INTO `epidemics` VALUES (184, 64, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:53');
INSERT INTO `epidemics` VALUES (185, 65, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:53');
INSERT INTO `epidemics` VALUES (186, 71, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:53');
INSERT INTO `epidemics` VALUES (187, 81, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:53');
INSERT INTO `epidemics` VALUES (188, 82, 2022, 5, 15, 0, 0, 0, 0, 0, 7, '2022-05-15 02:57:53');
INSERT INTO `epidemics` VALUES (189, 5, 2022, 5, 18, 49, 0, 0, 0, 0, 1, '2022-05-18 13:03:55');
INSERT INTO `epidemics` VALUES (190, 12, 2022, 5, 18, 12, 0, 0, 0, 0, 1, '2022-05-18 13:03:55');
INSERT INTO `epidemics` VALUES (191, 13, 2022, 5, 18, 0, 0, 0, 0, 0, 1, '2022-05-18 13:03:55');
INSERT INTO `epidemics` VALUES (192, 14, 2022, 5, 18, 0, 0, 0, 0, 0, 1, '2022-05-18 13:03:55');
INSERT INTO `epidemics` VALUES (193, 15, 2022, 5, 18, 0, 0, 0, 0, 0, 1, '2022-05-18 13:03:55');
INSERT INTO `epidemics` VALUES (194, 21, 2022, 5, 18, 0, 0, 0, 0, 0, 1, '2022-05-18 13:03:55');
INSERT INTO `epidemics` VALUES (195, 5, 2022, 5, 19, 34, 0, 0, 0, 0, 18, '2022-05-19 01:20:59');
INSERT INTO `epidemics` VALUES (196, 12, 2022, 5, 19, 34, 0, 0, 0, 0, 18, '2022-05-19 01:20:59');
INSERT INTO `epidemics` VALUES (197, 13, 2022, 5, 19, 3333, 0, 0, 0, 0, 18, '2022-05-19 01:20:59');
INSERT INTO `epidemics` VALUES (198, 14, 2022, 5, 19, 4, 0, 0, 0, 0, 18, '2022-05-19 01:20:59');
INSERT INTO `epidemics` VALUES (199, 15, 2022, 5, 19, 4, 0, 0, 0, 0, 18, '2022-05-19 01:20:59');
INSERT INTO `epidemics` VALUES (200, 21, 2022, 5, 19, 4, 0, 0, 0, 0, 18, '2022-05-19 01:20:59');
INSERT INTO `epidemics` VALUES (201, 22, 2022, 5, 19, 10, 0, 0, 0, 0, 20, '2022-05-19 01:25:47');
INSERT INTO `epidemics` VALUES (202, 23, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:25:47');
INSERT INTO `epidemics` VALUES (203, 31, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:25:47');
INSERT INTO `epidemics` VALUES (204, 32, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:25:47');
INSERT INTO `epidemics` VALUES (205, 33, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:25:47');
INSERT INTO `epidemics` VALUES (206, 34, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:25:47');
INSERT INTO `epidemics` VALUES (207, 35, 2022, 5, 19, 10, 0, 0, 0, 0, 20, '2022-05-19 01:26:16');
INSERT INTO `epidemics` VALUES (208, 36, 2022, 5, 19, 33, 0, 0, 0, 0, 20, '2022-05-19 01:26:16');
INSERT INTO `epidemics` VALUES (209, 37, 2022, 5, 19, 20, 0, 0, 0, 0, 20, '2022-05-19 01:26:16');
INSERT INTO `epidemics` VALUES (210, 41, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:26:16');
INSERT INTO `epidemics` VALUES (211, 42, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:26:16');
INSERT INTO `epidemics` VALUES (212, 43, 2022, 5, 19, 0, 0, 0, 0, 0, 20, '2022-05-19 01:26:16');
INSERT INTO `epidemics` VALUES (213, 44, 2022, 5, 19, 50, 0, 0, 0, 0, 1, '2022-05-19 01:27:02');
INSERT INTO `epidemics` VALUES (214, 45, 2022, 5, 19, 70, 0, 0, 0, 0, 1, '2022-05-19 01:27:02');
INSERT INTO `epidemics` VALUES (215, 46, 2022, 5, 19, 30, 0, 0, 0, 0, 1, '2022-05-19 01:27:02');
INSERT INTO `epidemics` VALUES (216, 50, 2022, 5, 19, 49, 0, 0, 0, 0, 1, '2022-05-19 01:27:02');
INSERT INTO `epidemics` VALUES (217, 51, 2022, 5, 19, 60, 0, 0, 0, 0, 1, '2022-05-19 01:27:02');
INSERT INTO `epidemics` VALUES (218, 52, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 01:27:02');
INSERT INTO `epidemics` VALUES (219, 53, 2022, 5, 19, 50, 0, 0, 0, 0, 1, '2022-05-19 01:27:05');
INSERT INTO `epidemics` VALUES (220, 54, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 01:27:05');
INSERT INTO `epidemics` VALUES (221, 61, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 01:27:05');
INSERT INTO `epidemics` VALUES (222, 62, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 01:27:05');
INSERT INTO `epidemics` VALUES (223, 63, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 01:27:05');
INSERT INTO `epidemics` VALUES (224, 64, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 01:27:05');
INSERT INTO `epidemics` VALUES (225, 65, 2022, 5, 19, 111, 0, 0, 0, 0, 1, '2022-05-19 05:58:19');
INSERT INTO `epidemics` VALUES (226, 71, 2022, 5, 19, 111, 0, 0, 0, 0, 1, '2022-05-19 05:58:19');
INSERT INTO `epidemics` VALUES (227, 81, 2022, 5, 19, 111, 0, 0, 0, 0, 1, '2022-05-19 05:58:19');
INSERT INTO `epidemics` VALUES (228, 82, 2022, 5, 19, 0, 0, 0, 0, 0, 1, '2022-05-19 05:58:19');

-- ----------------------------
-- Table structure for provinces
-- ----------------------------
DROP TABLE IF EXISTS `provinces`;
CREATE TABLE `provinces`  (
  `province_id` int NOT NULL AUTO_INCREMENT,
  `province_name` varchar(10) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `province_py` varchar(30) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `del_flag` smallint NULL DEFAULT NULL,
  PRIMARY KEY (`province_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 83 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of provinces
-- ----------------------------
INSERT INTO `provinces` VALUES (5, '北京', 'beijing', NULL);
INSERT INTO `provinces` VALUES (12, '天津', 'tianjin', NULL);
INSERT INTO `provinces` VALUES (13, '河北', 'hebei', NULL);
INSERT INTO `provinces` VALUES (14, '山西', 'shanxi', NULL);
INSERT INTO `provinces` VALUES (15, '内蒙古', 'neimenggu', NULL);
INSERT INTO `provinces` VALUES (21, '辽宁', 'liaoning', NULL);
INSERT INTO `provinces` VALUES (22, '吉林', 'jilin', NULL);
INSERT INTO `provinces` VALUES (23, '黑龙江', 'heilongjiang', NULL);
INSERT INTO `provinces` VALUES (31, '上海', 'shanghai', NULL);
INSERT INTO `provinces` VALUES (32, '江苏', 'jiangsu', NULL);
INSERT INTO `provinces` VALUES (33, '浙江', 'zhejiang', NULL);
INSERT INTO `provinces` VALUES (34, '安徽', 'anhui', NULL);
INSERT INTO `provinces` VALUES (35, '福建', 'fujian', NULL);
INSERT INTO `provinces` VALUES (36, '江西', 'jiangxi', NULL);
INSERT INTO `provinces` VALUES (37, '山东', 'shandong', NULL);
INSERT INTO `provinces` VALUES (41, '河南', 'henan', NULL);
INSERT INTO `provinces` VALUES (42, '湖北', 'hubei', NULL);
INSERT INTO `provinces` VALUES (43, '湖南', 'hunan', NULL);
INSERT INTO `provinces` VALUES (44, '广东', 'guangdong', NULL);
INSERT INTO `provinces` VALUES (45, '广西', 'guangxi', NULL);
INSERT INTO `provinces` VALUES (46, '海南', 'hainan', NULL);
INSERT INTO `provinces` VALUES (50, '重庆', 'chongqing', NULL);
INSERT INTO `provinces` VALUES (51, '四川', 'sichuan', NULL);
INSERT INTO `provinces` VALUES (52, '贵州', 'guizhou', NULL);
INSERT INTO `provinces` VALUES (53, '云南', 'yunnan', NULL);
INSERT INTO `provinces` VALUES (54, '西藏', 'xizang', NULL);
INSERT INTO `provinces` VALUES (61, '陕西', 'shaanxi', NULL);
INSERT INTO `provinces` VALUES (62, '甘肃', 'gansu', NULL);
INSERT INTO `provinces` VALUES (63, '青海', 'qinghai', NULL);
INSERT INTO `provinces` VALUES (64, '宁夏', 'ningxia', NULL);
INSERT INTO `provinces` VALUES (65, '新疆', 'xinjiang', NULL);
INSERT INTO `provinces` VALUES (71, '台湾', 'taiwan', NULL);
INSERT INTO `provinces` VALUES (81, '香港', 'xianggang', NULL);
INSERT INTO `provinces` VALUES (82, '澳门', 'aomen', NULL);

-- ----------------------------
-- Table structure for users
-- ----------------------------
DROP TABLE IF EXISTS `users`;
CREATE TABLE `users`  (
  `user_id` int NOT NULL AUTO_INCREMENT,
  `account` varchar(30) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `password` varchar(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `user_name` varchar(30) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `del_flag` smallint NULL DEFAULT NULL,
  PRIMARY KEY (`user_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 19 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of users
-- ----------------------------
INSERT INTO `users` VALUES (1, '1', '1', 'admin', 0);
INSERT INTO `users` VALUES (2, 'zhangsan', '23', '张三', 0);
INSERT INTO `users` VALUES (3, 'zhangsan2', '232', '张三2', 0);
INSERT INTO `users` VALUES (4, 'lisi', '123456', '李四', 1);
INSERT INTO `users` VALUES (7, 'wangwu', '123', '王五', 1);
INSERT INTO `users` VALUES (18, '2', '2', '2', 1);
INSERT INTO `users` VALUES (19, 'abc', '123345566', 'abc', 1);
INSERT INTO `users` VALUES (20, '6', '6', '6', 1);
INSERT INTO `users` VALUES (21, '8', '8', '8', 1);
INSERT INTO `users` VALUES (22, 'whj', '123', 'whj', 1);

SET FOREIGN_KEY_CHECKS = 1;

```

### 3、Maven导入项目所依赖的jar包

```xml
 <!-- 统一管理jar包版本 -->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>

        <spring.version>5.0.2.RELEASE</spring.version>
        <slf4j.version>1.6.6</slf4j.version>
        <log4j.version>1.2.12</log4j.version>
        <mysql.version>8.0.22</mysql.version>
        <mybatis.version>3.4.5</mybatis.version>
    </properties>

    <!-- 锁定jar包版本 -->
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-context</artifactId>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-web</artifactId>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-webmvc</artifactId>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-tx</artifactId>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-test</artifactId>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupId>org.mybatis</groupId>
                <artifactId>mybatis</artifactId>
                <version>${mybatis.version}</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <!-- 项目依赖jar包 -->
    <dependencies>
        <!-- spring -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.6.8</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysql.version}</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <!-- log start -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>${log4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <!-- log end -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>${mybatis.version}</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>1.3.0</version>
        </dependency>
        <dependency>
            <groupId>c3p0</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.1.2</version>
            <type>jar</type>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>5.1.2</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.0.9</version>
        </dependency>

        <dependency>
            <groupId>commons-dbcp</groupId>
            <artifactId>commons-dbcp</artifactId>
            <version>1.4</version>
        </dependency>

        <!--Jackson required包-->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.3</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.9.3</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
            <version>2.9.3</version>
        </dependency>

        <!--        <dependency>-->
        <!--            <groupId>com.alibaba</groupId>-->
        <!--            <artifactId>fastjson</artifactId>-->
        <!--            <version>1.2.47</version>-->
        <!--        </dependency>-->
    </dependencies>
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
![image](https://user-images.githubusercontent.com/77565682/169259873-10deeab3-62d0-4854-919a-abb84273e009.png)

