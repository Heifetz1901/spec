---
name: mysql-coding-review
description: "MySQL 数据库规范审查标准，覆盖建表规约、索引规约、SQL语句三大维度。"
---

# MySQL 数据库规范审查标准

## 激活条件

- 审查或设计 MySQL 数据库表结构时
- 编写或审查 DDL（CREATE TABLE、CREATE INDEX）时
- 编写或审查复杂 SQL 查询时
- 数据库性能优化或索引设计时

## 审查输出格式

代码审查时，按以下格式输出结果：

    ## 审查结果

    ### 严重（违反【强制】规则）
    1. **[维度-序号]** 规则简述
       - 位置：文件名:行号
       - 代码：`违规代码片段`
       - 修复：`正确代码`

    ### 建议（违反【推荐】规则）
    1. **[维度-序号]** 规则简述
       - 位置：文件名:行号
       - 代码：`违规代码片段`
       - 修复：`正确代码`

## 一、建表规约

1. [强制] 表达是与否概念的字段，必须使用is_xxx方式命名，数据类型为unsigned tinyint（1表示是，0表示否）。POJO类中布尔变量不加is前缀，需在resultMap中配置映射。

```sql
-- ✅ 正确
is_deleted TINYINT UNSIGNED COMMENT '是否删除：1-删除，0-未删除'

-- ❌ 错误
deleted TINYINT COMMENT '是否删除'
is_enabled BOOLEAN COMMENT '是否启用'
```

2. [强制] 表名、字段名必须使用小写字母或数字，禁止数字开头，禁止两个下划线中间只出现数字。

```sql
-- ✅ 正确
CREATE TABLE alipay_task ( ... );
-- level3_name, rdc_config

-- ❌ 错误
CREATE TABLE AliyunAdmin ( ... );
-- level_3_name, rdcConfig
```

3. [强制] 表名不使用复数名词。

```sql
-- ✅ 正确
user, order, product

-- ❌ 错误
users, orders, products
```

4. [强制] 禁用保留字，如desc、range、match、delayed等。

5. [强制] 索引命名规范：主键索引名为pk_字段名，唯一索引名为uk_字段名，普通索引名为idx_字段名。

```sql
-- ✅ 正确
PRIMARY KEY pk_id (id),
UNIQUE KEY uk_user_id (user_id),
KEY idx_create_time (create_time)
```

6. [强制] 小数类型必须使用decimal，禁止使用float和double，避免精度损失。

```sql
-- ✅ 正确
amount DECIMAL(10, 2) COMMENT '金额'

-- ❌ 错误
amount FLOAT COMMENT '金额'
price DOUBLE COMMENT '价格'
```

7. [强制] 字符串长度几乎相等时使用char定长类型。

8. [强制] varchar长度不要超过5000，超过则使用text类型并独立成表。

```sql
-- ✅ 正确
content VARCHAR(500) COMMENT '内容'
-- 大文本独立表
CREATE TABLE large_content (
  id BIGINT PRIMARY KEY,
  content TEXT,
  -- 其他字段
  KEY idx_ref_id (ref_id)
);

-- ❌ 错误
content VARCHAR(10000) COMMENT '长文本'
```

9. [强制] 表必备三字段：id（bigint unsigned自增）、create_time、update_time（datetime或timestamp）。

```sql
-- ✅ 正确
CREATE TABLE example (
  id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT,
  -- 其他字段
  create_time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  update_time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

10. [强制] 使用逻辑删除而非物理删除，通过is_deleted等字段标记。

```sql
-- ✅ 正确
is_deleted TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否删除：1-删除，0-未删除'

-- ❌ 错误
DELETE FROM user WHERE id = 1;
```

11. [推荐] 表命名遵循"业务名称_表的作用"格式。

```sql
-- ✅ 推荐
alipay_task, force_project, trade_config, tes_question
```

12. [推荐] 库名与应用名称尽量一致。

13. [推荐] 修改字段含义或追加状态值时，及时更新字段注释。

14. [推荐] 字段允许适当冗余以提高查询性能，但需满足：非频繁修改、非唯一索引、非varchar超长或text字段。

```sql
-- ✅ 推荐：商品名称冗余到订单表
CREATE TABLE order_item (
  id BIGINT PRIMARY KEY,
  product_id BIGINT,
  product_name VARCHAR(200) COMMENT '商品名称冗余',
  -- 其他字段
  KEY idx_product_id (product_id)
);
```

15. [推荐] 单表行数超过500万或容量超过2GB时才考虑分库分表。

---

## 二、索引规约

1. [强制] 业务上具有唯一特性的字段（包括组合字段）必须建成唯一索引。

```sql
-- ✅ 正确
CREATE UNIQUE INDEX uk_user_mobile ON user(mobile);
CREATE UNIQUE INDEX uk_order_no ON order(order_no);

-- ❌ 错误：仅靠应用层校验，数据库无唯一约束
```

2. [强制] 超过三个表禁止join，关联字段数据类型必须一致，被关联字段必须有索引。

```sql
-- ✅ 正确：最多两个表join
SELECT t1.name, t2.order_no
FROM user t1
INNER JOIN order t2 ON t1.id = t2.user_id
WHERE t1.id = 1;

-- ❌ 错误：三个以上表join
SELECT * FROM t1
JOIN t2 ON t1.id = t2.id
JOIN t3 ON t2.id = t3.id
JOIN t4 ON t3.id = t4.id;
```

3. [强制] varchar字段建索引时必须指定索引长度。

```sql
-- ✅ 正确
CREATE INDEX idx_name ON user(name(20));

-- ❌ 错误：全字段索引
CREATE INDEX idx_name ON user(name);
```

4. [强制] 页面搜索严禁左模糊或全模糊查询，如需要使用搜索引擎。

```sql
-- ✅ 正确：右模糊可用索引
SELECT * FROM user WHERE name LIKE '张%';

-- ❌ 错误：左模糊和全模糊无法使用索引
SELECT * FROM user WHERE name LIKE '%明';
SELECT * FROM user WHERE name LIKE '%张三%';
```

5. [推荐] order by利用索引有序性，将排序字段放在组合索引最后。

```sql
-- ✅ 正确：索引a_b_c，排序使用索引
SELECT * FROM t WHERE a = ? AND b = ? ORDER BY c;
-- 索引：INDEX idx_a_b_c (a, b, c)

-- ❌ 错误：范围查询后索引有序性失效
SELECT * FROM t WHERE a > 10 ORDER BY b;
-- 索引：INDEX idx_a_b (a, b) -- 无法利用排序
```

6. [推荐] 使用覆盖索引避免回表。

```sql
-- ✅ 正确：查询字段都在索引中
-- 索引：INDEX idx_user_id_status (user_id, status, create_time)
SELECT user_id, status FROM order WHERE user_id = ? AND status = 1;

-- ✅ 结果：explain的extra列显示"using index"
```

7. [推荐] 深分页使用延迟关联优化。

```sql
-- ✅ 正确：先定位ID再关联
SELECT t1.* FROM table1 t1
INNER JOIN (SELECT id FROM table1 WHERE condition LIMIT 100000, 20) t2 ON t1.id = t2.id;

-- ❌ 错误：直接深分页
SELECT * FROM table1 WHERE condition LIMIT 100000, 20;
```

8. [推荐] SQL性能优化目标：至少达到range级别，要求ref级别，const最好。

```sql
-- 性能级别（从好到差）：
-- const: 主键或唯一索引单行匹配
-- ref: 普通索引
-- range: 索引范围检索
-- index: 索引全扫描（避免）
-- ALL: 全表扫描（禁止）
```

9. [推荐] 组合索引中区分度最高的字段放在最左边（等号条件优先）。

```sql
-- ✅ 正确：等号条件前置
WHERE c > ? AND d = ?
-- 索引：INDEX idx_d_c (d, c)

-- ✅ 高区分度单字段
WHERE a = ? AND b = ?
-- a接近唯一值，只需建INDEX idx_a (a)
```

10. [推荐] 防止字段类型隐式转换导致索引失效。

```sql
-- ❌ 错误：字符串字段用数字比较，索引失效
SELECT * FROM user WHERE phone = 13800138000;

-- ✅ 正确：类型匹配
SELECT * FROM user WHERE phone = '13800138000';
```

---

## 三、SQL 语句

1. [强制] 使用count(*)统计行数，不要用count(列名)或count(常量)。

```sql
-- ✅ 正确
SELECT count(*) FROM user;

-- ❌ 错误
SELECT count(id) FROM user;
SELECT count(1) FROM user;
```

2. [强制] count(distinct col)计算除NULL外的不重复行数；多列count(distinct col1, col2)中任一列全为NULL则返回0。

3. [强制] sum(col)在列值全为NULL时返回NULL，使用IFNULL处理NPE。

```sql
-- ✅ 正确
SELECT IFNULL(SUM(amount), 0) FROM order WHERE user_id = ?;

-- ❌ 错误：可能返回NULL导致NPE
SELECT SUM(amount) FROM order WHERE user_id = ?;
```

4. [强制] 使用ISNULL()函数判断NULL值，避免直接比较。

```sql
-- ✅ 正确
SELECT * FROM user WHERE ISNULL(name);
SELECT * FROM user WHERE name IS NOT NULL;

-- ❌ 错误：NULL与任何值比较结果都是NULL
SELECT * FROM user WHERE name = NULL;
SELECT * FROM user WHERE name != NULL;
```

5. [强制] 分页查询时count为0应直接返回，避免执行分页语句。

6. [强制] 禁止使用外键与级联，在应用层解决关联关系。

```sql
-- ❌ 错误：使用外键
CREATE TABLE order (
  id BIGINT PRIMARY KEY,
  user_id BIGINT,
  FOREIGN KEY (user_id) REFERENCES user(id)
);

-- ✅ 正确：应用层维护关联
CREATE TABLE order (
  id BIGINT PRIMARY KEY,
  user_id BIGINT,
  KEY idx_user_id (user_id)
);
```

7. [强制] 禁止使用存储过程，难以调试和扩展且无移植性。

8. [强制] 数据订正操作要先select确认再执行更新。

9. [强制] 多表查询/更新/删除时，列名前必须加表别名或表名限定。

```sql
-- ✅ 正确
SELECT t1.name, t2.order_no
FROM user t1, order t2
WHERE t1.id = t2.user_id;

-- ❌ 错误：未限定可能导致歧义
SELECT name, order_no
FROM user t1, order t2
WHERE t1.id = t2.user_id;
```

10. [推荐] SQL中表别名加as，按t1、t2、t3顺序命名。

```sql
-- ✅ 推荐
SELECT t1.name FROM first_table AS t1, second_table AS t2 WHERE t1.id = t2.id;
```

11. [推荐] 避免使用in操作，不可避免时控制在1000个元素内。

```sql
-- ✅ 推荐：使用临时表或JOIN
-- ❌ 避免：大量IN
SELECT * FROM user WHERE id IN (1, 2, 3, ..., 10000);
```
