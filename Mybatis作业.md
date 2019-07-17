# Mybatis作业

## 表设计

```sql
/*
Navicat MySQL Data Transfer

Source Server         : local-mysql
Source Server Version : 80013
Source Host           : localhost:3306
Source Database       : mybatis_train

Target Server Type    : MYSQL
Target Server Version : 80013
File Encoding         : 65001

Date: 2019-07-16 17:03:17
*/

SET FOREIGN_KEY_CHECKS=0;

-- ----------------------------
-- Table structure for order_header
-- ----------------------------
DROP TABLE IF EXISTS `order_header`;
CREATE TABLE `order_header` (
  `order_header_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '订单头id',
  `order_number` varchar(30) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL COMMENT '订单编号',
  `customer_user_id` bigint(20) NOT NULL COMMENT '客户id',
  `remark` varchar(480) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `object_version_number` bigint(20) NOT NULL DEFAULT '0' COMMENT '版本号',
  `creation_date` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `created_by` bigint(20) NOT NULL DEFAULT '-1' COMMENT '创建人id',
  `last_update_date` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '最后更新时间',
  `last_updated_by` bigint(20) NOT NULL DEFAULT '-1' COMMENT '最后更新人id',
  PRIMARY KEY (`order_header_id`),
  UNIQUE KEY `order_header_u1` (`order_number`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;

-- ----------------------------
-- Records of order_header
-- ----------------------------
INSERT INTO `order_header` VALUES ('1', 'SO190716000001', '2', '买包辣条', '0', '2019-07-16 08:25:27', '1', '2019-07-16 08:25:27', '1');
INSERT INTO `order_header` VALUES ('2', 'SO190716000002', '3', null, '0', '2019-07-16 08:58:56', '1', '2019-07-16 08:58:56', '1');

-- ----------------------------
-- Table structure for order_line
-- ----------------------------
DROP TABLE IF EXISTS `order_line`;
CREATE TABLE `order_line` (
  `order_line_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '订单行id',
  `order_header_id` bigint(20) NOT NULL COMMENT '订单头id',
  `order_line_number` int(10) NOT NULL COMMENT '订单行号',
  `item_code` varchar(30) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL COMMENT '物料编码',
  `item_name` varchar(240) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL COMMENT '物料名称',
  `unit_price` decimal(20,8) NOT NULL COMMENT '单价',
  `quantity` decimal(20,2) NOT NULL COMMENT '数量',
  `line_amount` decimal(20,2) NOT NULL COMMENT '行总价',
  `object_version_number` bigint(20) NOT NULL DEFAULT '0' COMMENT '版本号',
  `creation_date` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `created_by` bigint(20) NOT NULL DEFAULT '-1' COMMENT '创建人id',
  `last_update_date` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '最后更新时间',
  `last_updated_by` bigint(20) NOT NULL DEFAULT '-1' COMMENT '最后更新人id',
  PRIMARY KEY (`order_line_id`),
  UNIQUE KEY `order_line_u1` (`order_header_id`,`order_line_number`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;

-- ----------------------------
-- Records of order_line
-- ----------------------------
INSERT INTO `order_line` VALUES ('1', '1', '10', '4900001', '卫龙亲嘴烧(500g)', '18.50000000', '1.00', '18.50', '0', '2019-07-16 08:26:14', '1', '2019-07-16 08:26:14', '1');
INSERT INTO `order_line` VALUES ('2', '1', '20', '4900002', '卫龙小面筋(20g)', '1.10000000', '20.00', '22.00', '0', '2019-07-16 08:30:48', '1', '2019-07-16 08:30:48', '1');
INSERT INTO `order_line` VALUES ('3', '2', '10', 'IT30015', 'ELK Service', '18000.00000000', '1.00', '18000.00', '0', '2019-07-16 08:59:49', '1', '2019-07-16 08:59:49', '1');
INSERT INTO `order_line` VALUES ('4', '2', '20', 'IT30011', 'Huawei Router', '8999.00000000', '1.00', '8999.00', '0', '2019-07-16 09:00:30', '1', '2019-07-16 09:00:30', '1');
INSERT INTO `order_line` VALUES ('5', '2', '30', '4900494', 'お弁当', '13.50000000', '50.00', '675.00', '0', '2019-07-16 09:02:01', '1', '2019-07-16 09:02:01', '1');

-- ----------------------------
-- Table structure for sys_user
-- ----------------------------
DROP TABLE IF EXISTS `sys_user`;
CREATE TABLE `sys_user` (
  `user_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `user_number` varchar(30) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL COMMENT '用户编号',
  `user_name` varchar(180) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL COMMENT '用户名称',
  `address` varchar(480) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL COMMENT '用户地址',
  `object_version_number` bigint(20) NOT NULL DEFAULT '0' COMMENT '版本号',
  `creation_date` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `created_by` bigint(20) NOT NULL DEFAULT '-1' COMMENT '创建人id',
  `last_update_date` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '最后更新时间',
  `last_updated_by` bigint(20) NOT NULL DEFAULT '-1' COMMENT '最后更新人id',
  PRIMARY KEY (`user_id`),
  UNIQUE KEY `sys_user_u1` (`user_number`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;

-- ----------------------------
-- Records of sys_user
-- ----------------------------
INSERT INTO `sys_user` VALUES ('1', '20001', '小王', '上海市青浦区汇联路33号', '0', '2019-07-16 08:22:44', '1', '2019-07-16 08:22:44', '1');
INSERT INTO `sys_user` VALUES ('2', '20002', '小明', '安徽省芜湖市芜湖县安徽信息工程学院(新芜校区)', '0', '2019-07-16 08:24:48', '1', '2019-07-16 08:24:48', '1');
INSERT INTO `sys_user` VALUES ('3', '20003', 'Ming', '1900 McCarthy Boulevard STE 445 Milpitas,CA 95035', '0', '2019-07-16 08:58:21', '1', '2019-07-16 08:58:21', '1');
```

## 要求

1. 在[码云](https://gitee.com)中创建一个新项目
1. 在自己本地`MySql`数据库中根据上述建表语句初始化数据库
1. 使用Spring + Mybatis，请注意`不是SpringMVC`
1. sql需写在xxxMapper.xml中
1. 开发`List<OrderLineQueryResult> selectOrderLinesByCondition(OrderLineQueryCondition condition);`方法，用以根据传入条件动态查询订单行数据。查询条件包含`订单编号(模糊)、订单行号、物料编码(模糊)、物料名称(模糊)、订单创建人id、订单客户id`。查询结果包含`订单编号、客户名称、客户地址、订单备注、订单创建人、订单行号、物料编码、物料名称、单价、数量、行总价`
1. 开发`int insertUser(User user);`方法，用以创建一个新用户，注意返回值中要返回用户ID
1. 开发`int updateUser(User user);`方法，用以根据ID更新一个用户信息
1. 开发`int deleteUser(Long userId);`方法，用以根据ID删除一个用户信息，注意返回值是被删除数据的数量
1. 分别调用上述方法，并打印所有执行结果的返回值并截图，放入根目录中。注意如果方法返回值是个对象则需要重写`toString()`方法，输出所有内涵成员变量的值。
1. 将项目及运行截图上传至码云，将工程地址填入考试系统中。
1. 选修：表设计中的`object_version_number、creation_date、created_by、last_update_date、last_updated_by`的作用是什么，怎样在代码中实现这些字段的自动更新
