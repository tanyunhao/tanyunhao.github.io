
源码下载分享https://www.123865.com/ps/WlFzVv-3Kuph
用户表:编号，用户名，密码，邮箱，角色，用户头像；

影片表：编号，影片名称，国外名称，演职人员，导演，电影详情，电影时长，电影类型，电影评分，票房，电影参评人数，上映时间，制片地区，电影海报地址，电影状态；

影院表：编号，影院名称，影院地址；

放映厅表：编号，放映厅名称，放映厅容量，所属影院编号；

订单表：编号，所属用户编号，所属场次编号，电影票座位信息，订单状态，订单价格，订单支付时间，所属用户对象；

订单详情表：编号，所属放映厅，放映的电影编号，电影放映时间，售价，剩余座位数，场次状态，所属放映厅对象，放映的电影；

评论表：编号，所属用户编号，评论内容，所属电影编号，评论时间，所属用户，评分；

# 1 需求分析
## 1.1 用户管理模块  
<font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">用户管理模块提供完整的账户生命周期管理，支持新用户通过邮箱验证进行注册登录，允许用户维护个人信息（包括头像修改和密码更新），实施基于角色的权限控制（区分普通用户、影院管理员和系统管理员），并记录用户活动历史（如登录时间、购票记录等），确保账户安全性和操作可追溯性。</font>

## 1.2 影片管理模块  
<font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">影片管理模块负责维护电影全生命周期数据，包括影片基本信息（名称、导演、时长、类型等）的增删改查，管理影片上映状态（即将上映</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">热映</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">已下架），提供多维度搜索筛选功能（按类型、评分、地区等），自动生成票房统计报表，并支持电影海报的上传与展示。</font>

## 1.3 影院管理模块  
<font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">影院管理模块实现影院资源的数字化管理，维护影院基础信息（名称、地址等），配置放映厅参数（名称、座位容量），通过地图</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">API</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">展示影院地理分布，并统计各影院场次安排数据（如每日排片量、上座率等），为影院资源调度提供数据支持。</font>

## 1.4 场次管理模块  
<font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">场次管理模块提供放映计划的全流程管理，支持创建</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">修改影厅放映计划（时间、影厅），设置动态票价策略（分时段差异化定价），实现可视化座位图展示，自动监控并更新场次状态（可预订</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">即将售罄</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">已售罄），并通过冲突检测机制防止同一影厅时间重叠排片。</font>

## 1.5 订单管理模块  
<font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">订单管理模块实现票务交易闭环，支持在线选座购票流程，集成模拟支付系统（支持支付宝</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">微信等支付方式），管理订单全生命周期状态（待支付</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">已支付</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">已取消），提供用户订单历史查询功能，并处理退票业务（含退款规则计算）。</font>

## 1.6 评论管理模块  
<font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">评论管理模块构建影片评价体系，允许用户发表评分和文字评论，实施先审后发的审核机制，支持评论互动功能（点赞</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">/</font><font style="color:rgb(64,64,64);background-color:rgb(255,255,255);">回复），自动生成评论分析报告（包含评分分布、热词分析等），并实时更新影片综合评分数据。</font>

# 2 系统设计
## 2.1 系统结构功能图
根据需求分析，确定系统结构功能如图2-1所示：



![](https://i-blog.csdnimg.cn/img_convert/09cb65fba15267e4496eedb94ad80249.png)

图2-1 系统功能结构图

## 2.2 功能流程图
系统最主要的功能就是管理员登录之后对各种功能的使用。管理员功能如图4-2所示。

![](https://i-blog.csdnimg.cn/img_convert/f34825a6a1abe737e3d89a3ccd754fc4.png)

图2-2 管理员登录管理流程

![](https://i-blog.csdnimg.cn/img_convert/fd959826f127d9d9314b6a196911ef2e.png)

图2-3普通用户登录流程

## 2.3 数据库设计
整体功能的E-R图如图2-4所示。

![](https://i-blog.csdnimg.cn/img_convert/0a3900d7135d590bee1aa966d5dc7511.png)

图2-4 系统E-R图

本系统包含的数据表如下：

**1****书架类型表**** (shelf_types)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| shelf_type_id | NUMBER | 主键 | - | 否 | - | 书架类型ID |
| shelf_type_name | VARCHAR2 | 非空 | 50 | 否 | - | 书架类型名称 |


**2****读者类型表**** (reader_types)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| reader_type_id | NUMBER | 主键 | - | 否 | - | 读者类型ID |
| reader_type_name | VARCHAR2 | 非空 | 50 | 否 | - | 读者类型名称 |


**3****书架表**** (shelves)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| shelf_id | NUMBER | 主键 | - | 否 | - | 书架ID |
| shelf_number | VARCHAR2 | 非空 | 20 | 否 | - | 书架编号 |
| shelf_type_id | NUMBER | 外键且非空 | - | 否 | - | 书架类型ID |


**4****工作人员表**** (staff)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| staff_id | NUMBER | 主键 | - | 否 | - | 工作人员ID |
| staff_name | VARCHAR2 | 非空 | 100 | 否 | - | 工作人员姓名 |
| staff_position | VARCHAR2 | 非空 | 50 | 否 | - | 工作人员职位 |


**5****图书表**** (books)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| book_id | NUMBER | 主键 | - | 否 | - | 图书ID |
| title | VARCHAR2 | 非空 | 200 | 否 | - | 图书标题 |
| author | VARCHAR2 | 非空 | 100 | 否 | - | 图书作者 |
| isbn | VARCHAR2 | 唯一且非空 | 20 | 否 | - | 图书国际标准书号 |
| publication_year | NUMBER | 可空 | - | 是 | - | 出版年份 |
| shelf_id | NUMBER | 外键且非空 | - | 否 | - | 书架ID |


**6****读者表**** (readers)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| reader_id | NUMBER | 主键 | - | 否 | - | 读者ID |
| reader_name | VARCHAR2 | 非空 | 100 | 否 | - | 读者姓名 |
| reader_type_id | NUMBER | 外键且非空 | - | 否 | - | 读者类型ID |
| contact_phone | VARCHAR2 | 可空 | 15 | 是 | - | 联系电话 |


**7****正借阅表**** (loans)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| loan_id | NUMBER | 主键 | - | 否 | - | 借阅记录ID |
| book_id | NUMBER | 外键且非空 | - | 否 | - | 图书ID |
| reader_id | NUMBER | 外键且非空 | - | 否 | - | 读者ID |
| loan_date | DATE | 非空 | - | 否 | - | 借书日期 |
| due_date | DATE | 非空 | - | 否 | - | 应还日期 |


**8****已还书籍表**** (returns)**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| return_id | NUMBER | 主键 | - | 否 | - | 还书记录ID |
| loan_id | NUMBER | 外键 | - | 是 | - | 借阅记录ID |
| return_date | DATE | 非空 | - | 否 | - | 还书日期 |


**9****通知记录表（****overdue_notifications****）**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| notification_id | NUMBER | 主键 | - | 否 | - | 通知记录 |
| loan_id | NUMBER | 外键 | - | 否 | - | 借阅记录 ID |
| reader_id | NUMBER | 外键 | - | 否 | - | 读者 ID |
| notification_date | DATE | 日期 | - | 是 | SYSDATE | 通知日期 |
| message | VARCHAR2 | 字符串 | 500 | 是 | - | 通知内容 |


**10****历史记录表（****book_location_history****）**

| 列名 | 数据类型 | 字段类型 | 长度 | 是否为空 | 默认值 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| history_id | NUMBER | 主键 | - | 否 | - | 历史记录 |
| book_id | NUMBER | 外键 | - | 否 | - | 图书 ID |
| old_shelf_id | NUMBER | 外键 | - | 是 | - | 旧书架 ID |
| new_shelf_id | NUMBER | 外键 | - | 否 | - | 新书架 ID |
| change_date | DATE | 日期 | - | 是 | SYSDATE | 变更日期 |
| changed_by | NUMBER | 外键 | - | 是 | - | 操作人 ID |


# **3 SQL实现**
```sql
-- 创建用户表
CREATE TABLE 用户表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    用户名 VARCHAR2(100) NOT NULL,
    密码 VARCHAR2(100) NOT NULL,
    邮箱 VARCHAR2(100) UNIQUE NOT NULL,
    角色 VARCHAR2(50) NOT NULL,
    用户头像 VARCHAR2(255)
);

-- 创建影片表
CREATE TABLE 影片表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    影片名称 VARCHAR2(200) NOT NULL,
    国外名称 VARCHAR2(200),
    演职人员 VARCHAR2(500),
    导演 VARCHAR2(100),
    电影详情 VARCHAR2(1000),
    电影时长 NUMBER, -- 电影时长（以分钟为单位）
    电影类型 VARCHAR2(100),
    电影评分 NUMBER CHECK (电影评分 BETWEEN 0 AND 10),
    票房 NUMBER,
    电影参评人数 NUMBER,
    上映时间 DATE,
    制片地区 VARCHAR2(100),
    电影海报地址 VARCHAR2(255),
    电影状态 VARCHAR2(50) -- 电影状态，例如正在上映或已下架
);

-- 创建影院表
CREATE TABLE 影院表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    影院名称 VARCHAR2(100) NOT NULL,
    影院地址 VARCHAR2(255) NOT NULL
);

-- 创建放映厅表
CREATE TABLE 放映厅表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    放映厅名称 VARCHAR2(100) NOT NULL,
    放映厅容量 NUMBER NOT NULL,
    所属影院编号 NUMBER,
    FOREIGN KEY (所属影院编号) REFERENCES 影院表(编号)
);

-- 创建订单详情表
CREATE TABLE 订单详情表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    所属放映厅 NUMBER,
    放映的电影编号 NUMBER,
    电影放映时间 DATE,
    售价 NUMBER NOT NULL,
    剩余座位数 NUMBER NOT NULL,
    场次状态 VARCHAR2(50), -- 可预订、已售罄等状态
    FOREIGN KEY (所属放映厅) REFERENCES 放映厅表(编号),
    FOREIGN KEY (放映的电影编号) REFERENCES 影片表(编号)
);

-- 创建订单表
CREATE TABLE 订单表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    所属用户编号 NUMBER,
    所属场次编号 NUMBER,
    电影票座位信息 VARCHAR2(500), -- 存储座位信息
    订单状态 VARCHAR2(50),
    订单价格 NUMBER NOT NULL,
    订单支付时间 DATE,
    FOREIGN KEY (所属用户编号) REFERENCES 用户表(编号),
    FOREIGN KEY (所属场次编号) REFERENCES 订单详情表(编号)
);

-- 创建评论表
CREATE TABLE 评论表 (
    编号 NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    所属用户编号 NUMBER,
    评论内容 VARCHAR2(1000),
    所属电影编号 NUMBER,
    评论时间 DATE DEFAULT SYSDATE,
    所属用户 VARCHAR2(100),
    评分 NUMBER CHECK (评分 BETWEEN 0 AND 10),
    FOREIGN KEY (所属用户编号) REFERENCES 用户表(编号),
    FOREIGN KEY (所属电影编号) REFERENCES 影片表(编号)
);


```

```sql
-- 用户表索引
CREATE INDEX idx_username ON 用户表 (用户名);
CREATE INDEX idx_email ON 用户表 (邮箱);

-- 影片表索引
CREATE INDEX idx_movie_name ON 影片表 (影片名称);
CREATE INDEX idx_director ON 影片表 (导演);
CREATE INDEX idx_movie_rating ON 影片表 (电影评分);

-- 影院表索引
CREATE INDEX idx_cinema_name ON 影院表 (影院名称);

-- 放映厅表索引
CREATE INDEX idx_screening_room_name ON 放映厅表 (放映厅名称);

-- 订单表索引
CREATE INDEX idx_user_id ON 订单表 (所属用户编号);
CREATE INDEX idx_showtime_id ON 订单表 (所属场次编号);

-- 订单详情表索引
CREATE INDEX idx_hall_id ON 订单详情表 (所属放映厅);
CREATE INDEX idx_movie_id ON 订单详情表 (放映的电影编号);

-- 评论表索引
CREATE INDEX idx_user_id_comment ON 评论表 (所属用户编号);
CREATE INDEX idx_movie_id_comment ON 评论表 (所属电影编号);
```

```sql
-- 创建用户信息视图
CREATE VIEW 用户信息视图 AS
SELECT 编号 AS 用户编号, 用户名, 邮箱, 角色
FROM 用户表;

-- 创建正在上映电影视图
CREATE VIEW 正在上映电影视图 AS
SELECT 编号 AS 电影编号, 影片名称, 上映时间, 票房, 电影状态
FROM 影片表
WHERE 电影状态 = '正在上映';

-- 创建影院放映厅信息视图
CREATE VIEW 影院放映厅信息视图 AS
SELECT c.编号 AS 影院编号, c.影院名称, c.影院地址, 
       r.编号 AS 放映厅编号, r.放映厅名称, r.放映厅容量
FROM 影院表 c
JOIN 放映厅表 r ON c.编号 = r.所属影院编号;

-- 创建用户订单详情视图
CREATE VIEW 用户订单详情视图 AS
SELECT o.编号 AS 订单编号, u.用户名, 
      m.影片名称, d.电影放映时间,
      o.电影票座位信息, o.订单状态
FROM 订单表 o
JOIN 用户表 u ON o.所属用户编号 = u.编号
JOIN 订单详情表 d ON o.所属场次编号 = d.编号
JOIN 影片表 m ON d.放映的电影编号 = m.编号;

-- 创建用户电影评论视图
CREATE VIEW 用户电影评论视图 AS
SELECT c.编号 AS 评论编号, u.用户名, 
      m.影片名称, c.评论内容, c.评分, c.评论时间
FROM 评论表 c
JOIN 用户表 u ON c.所属用户编号 = u.编号
JOIN 影片表 m ON c.所属电影编号 = m.编号;
```

```sql
-- 创建用户注册存储过程
CREATE OR REPLACE PROCEDURE 用户注册 (
    p_username IN VARCHAR2,
    p_password IN VARCHAR2,
    p_email IN VARCHAR2,
    p_role IN VARCHAR2
) AS
BEGIN
    INSERT INTO 用户表 (用户名, 密码, 邮箱, 角色)
    VALUES (p_username, p_password, p_email, p_role);
END 用户注册;
/

-- 创建更新订单状态存储过程
CREATE OR REPLACE PROCEDURE 更新订单状态 (
    p_order_id IN NUMBER,
    p_new_status IN VARCHAR2
) AS
BEGIN
    UPDATE 订单表
    SET 订单状态 = p_new_status
    WHERE 编号 = p_order_id;

    COMMIT; -- 提交事务
END 更新订单状态;
/

-- 创建计算电影平均评分函数
CREATE OR REPLACE FUNCTION 计算电影平均评分 (
    p_movie_id IN NUMBER
) RETURN NUMBER AS
    v_average_rating NUMBER;
BEGIN
    SELECT AVG(评分)
    INTO v_average_rating
    FROM 评论表
    WHERE 所属电影编号 = p_movie_id;

    RETURN NVL(v_average_rating, 0); -- 如果没有评分，则返回0
END 计算电影平均评分;
/

-- 创建查询用户订单总数函数
CREATE OR REPLACE FUNCTION 查询用户订单总数 (
    p_user_id IN NUMBER
) RETURN NUMBER AS
    v_order_count NUMBER;
BEGIN
    SELECT COUNT(*)
    INTO v_order_count
    FROM 订单表
    WHERE 所属用户编号 = p_user_id;

    RETURN v_order_count;
END 查询用户订单总数;
/
```

```sql
-- 自动更新影片评分和参评人数
CREATE OR REPLACE TRIGGER 更新影片评分
AFTER INSERT OR UPDATE OR DELETE ON 评论表
FOR EACH ROW
DECLARE
    v_电影编号 影片表.编号%TYPE;
BEGIN
    IF INSERTING THEN
        v_电影编号 := :NEW.所属电影编号;
        UPDATE 影片表 SET
            电影评分 = (SELECT AVG(评分) FROM 评论表 WHERE 所属电影编号 = v_电影编号),
            电影参评人数 = (SELECT COUNT(*) FROM 评论表 WHERE 所属电影编号 = v_电影编号)
        WHERE 编号 = v_电影编号;
    ELSIF DELETING THEN
        v_电影编号 := :OLD.所属电影编号;
        UPDATE 影片表 SET
            电影评分 = (SELECT AVG(评分) FROM 评论表 WHERE 所属电影编号 = v_电影编号),
            电影参评人数 = (SELECT COUNT(*) FROM 评论表 WHERE 所属电影编号 = v_电影编号)
        WHERE 编号 = v_电影编号;
    ELSE
        -- 处理电影变更的情况
        IF :NEW.所属电影编号 != :OLD.所属电影编号 THEN
            -- 更新原电影
            UPDATE 影片表 SET
                电影评分 = (SELECT AVG(评分) FROM 评论表 WHERE 所属电影编号 = :OLD.所属电影编号),
                电影参评人数 = (SELECT COUNT(*) FROM 评论表 WHERE 所属电影编号 = :OLD.所属电影编号)
            WHERE 编号 = :OLD.所属电影编号;
            
            -- 更新新电影
            UPDATE 影片表 SET
                电影评分 = (SELECT AVG(评分) FROM 评论表 WHERE 所属电影编号 = :NEW.所属电影编号),
                电影参评人数 = (SELECT COUNT(*) FROM 评论表 WHERE 所属电影编号 = :NEW.所属电影编号)
            WHERE 编号 = :NEW.所属电影编号;
        ELSE
            -- 只更新当前电影
            UPDATE 影片表 SET
                电影评分 = (SELECT AVG(评分) FROM 评论表 WHERE 所属电影编号 = :NEW.所属电影编号),
                电影参评人数 = (SELECT COUNT(*) FROM 评论表 WHERE 所属电影编号 = :NEW.所属电影编号)
            WHERE 编号 = :NEW.所属电影编号;
        END IF;
    END IF;
END;
/

-- 订单支付后更新场次座位
CREATE OR REPLACE TRIGGER 更新场次座位
AFTER UPDATE OF 订单状态 ON 订单表
FOR EACH ROW
WHEN (NEW.订单状态 = '已支付' AND OLD.订单状态 != '已支付')
DECLARE
    v_座位数 NUMBER;
BEGIN
    -- 计算订单中的座位数量（以逗号分隔）
    v_座位数 := REGEXP_COUNT(:NEW.电影票座位信息, ',') + 1;
    
    UPDATE 订单详情表
    SET 剩余座位数 = 剩余座位数 - v_座位数
    WHERE 编号 = :NEW.所属场次编号;
END;
/

-- 自动更新场次状态
CREATE OR REPLACE TRIGGER 更新场次状态
AFTER UPDATE OF 剩余座位数 ON 订单详情表
FOR EACH ROW
BEGIN
    IF :NEW.剩余座位数 <= 0 THEN
        UPDATE 订单详情表
        SET 场次状态 = '已售罄'
        WHERE 编号 = :NEW.编号;
    ELSIF :NEW.剩余座位数 < (:NEW.剩余座位数 + :NEW.剩余座位数 * 0.2) THEN  -- 示例：少于20%座位时
        UPDATE 订单详情表
        SET 场次状态 = '即将售罄'
        WHERE 编号 = :NEW.编号;
    ELSE
        UPDATE 订单详情表
        SET 场次状态 = '可预订'
        WHERE 编号 = :NEW.编号;
    END IF;
END;
/

-- 新评论自动关联用户名
CREATE OR REPLACE TRIGGER 填充评论用户名
BEFORE INSERT ON 评论表
FOR EACH ROW
BEGIN
    SELECT 用户名 INTO :NEW.所属用户
    FROM 用户表
    WHERE 编号 = :NEW.所属用户编号;
END;
/

-- 票房自动累加
CREATE OR REPLACE TRIGGER 更新影片票房
AFTER UPDATE OF 订单状态 ON 订单表
FOR EACH ROW
WHEN (NEW.订单状态 = '已支付' AND OLD.订单状态 != '已支付')
DECLARE
    v_电影编号 影片表.编号%TYPE;
BEGIN
    -- 获取关联的电影编号
    SELECT 放映的电影编号 INTO v_电影编号
    FROM 订单详情表
    WHERE 编号 = :NEW.所属场次编号;
    
    -- 更新票房
    UPDATE 影片表
    SET 票房 = 票房 + :NEW.订单价格
    WHERE 编号 = v_电影编号;
END;
/

-- 场次时间冲突检查
CREATE OR REPLACE TRIGGER 检查场次冲突
BEFORE INSERT OR UPDATE ON 订单详情表
FOR EACH ROW
DECLARE
    v_conflict_count NUMBER;
BEGIN
    SELECT COUNT(*) INTO v_conflict_count
    FROM 订单详情表
    WHERE 所属放映厅 = :NEW.所属放映厅
    AND 编号 != :NEW.编号  -- 排除自身
    AND 电影放映时间 BETWEEN :NEW.电影放映时间 - INTERVAL '2' HOUR
                     AND :NEW.电影放映时间 + INTERVAL '2' HOUR;
    
    IF v_conflict_count > 0 THEN
        RAISE_APPLICATION_ERROR(-20001, '该放映厅在此时间段已有其他场次安排');
    END IF;
END;
/
```

### 1. 用户管理操作
```sql
-- 用户注册
INSERT INTO 用户表 (用户名, 密码, 邮箱, 角色) 
VALUES ('张三', 'zhangsan123', 'zhangsan@example.com', '普通用户');

-- 用户信息更新
UPDATE 用户表 
SET 用户头像 = 'avatars/zhangsan.jpg', 密码 = 'newpassword123' 
WHERE 用户名 = '张三';

-- 用户删除
DELETE FROM 用户表 WHERE 用户名 = '张三';

-- 用户登录验证
SELECT 编号, 用户名, 角色 FROM 用户表 
WHERE 邮箱 = 'zhangsan@example.com' AND 密码 = 'zhangsan123';
```

### 2. 影片管理操作
```sql
-- 添加新影片
INSERT INTO 影片表 (
    影片名称, 国外名称, 导演, 电影详情, 电影时长, 
    电影类型, 上映时间, 制片地区, 电影海报地址, 电影状态
) VALUES (
    '流浪地球', 'The Wandering Earth', '郭帆', 
    '太阳即将毁灭，人类在地球表面建造巨大推进器...',
    125, '科幻/灾难', DATE '2019-02-05', '中国', 
    'posters/wandering_earth.jpg', '已下架'
);

-- 更新影片信息
UPDATE 影片表 
SET 电影评分 = 7.9, 电影参评人数 = 1250000 
WHERE 影片名称 = '流浪地球';

-- 影片查询 (按类型和评分)
SELECT * FROM 影片表 
WHERE 电影类型 LIKE '%科幻%' AND 电影评分 > 7.0 
ORDER BY 上映时间 DESC;

-- 票房排行榜
SELECT 影片名称, 票房 FROM 影片表 
WHERE 票房 IS NOT NULL 
ORDER BY 票房 DESC 
FETCH FIRST 10 ROWS ONLY;
```

### 3. 影院管理操作
```sql
-- 新增影院
INSERT INTO 影院表 (影院名称, 影院地址) 
VALUES ('万达影城(北京CBD店)', '北京市朝阳区建国路93号万达广场');

-- 新增放映厅
INSERT INTO 放映厅表 (放映厅名称, 放映厅容量, 所属影院编号) 
VALUES ('IMAX厅', 250, (SELECT 编号 FROM 影院表 WHERE 影院名称 = '万达影城(北京CBD店)'));
```

### 4. 场次管理操作
```sql
-- 创建新场次
INSERT INTO 订单详情表 (
    所属放映厅, 放映的电影编号, 电影放映时间, 售价, 剩余座位数, 场次状态
) VALUES (
    (SELECT 编号 FROM 放映厅表 WHERE 放映厅名称 = 'IMAX厅'),
    (SELECT 编号 FROM 影片表 WHERE 影片名称 = '流浪地球'),
    TIMESTAMP '2023-05-20 19:30:00',
    65.00,
    (SELECT 放映厅容量 FROM 放映厅表 WHERE 放映厅名称 = 'IMAX厅'),
    '可预订'
);

-- 查询可用场次
SELECT 
    m.影片名称, 
    c.影院名称, 
    h.放映厅名称, 
    s.电影放映时间, 
    s.售价, 
    s.剩余座位数
FROM 订单详情表 s
JOIN 影片表 m ON s.放映的电影编号 = m.编号
JOIN 放映厅表 h ON s.所属放映厅 = h.编号
JOIN 影院表 c ON h.所属影院编号 = c.编号
WHERE m.影片名称 = '流浪地球'
AND s.电影放映时间 > SYSDATE
AND s.剩余座位数 > 0;
```

### 5. 订单管理操作
```sql
-- 创建新订单
INSERT INTO 订单表 (
    所属用户编号, 所属场次编号, 电影票座位信息, 订单状态, 订单价格
) VALUES (
    (SELECT 编号 FROM 用户表 WHERE 邮箱 = 'zhangsan@example.com'),
    (SELECT 编号 FROM 订单详情表 WHERE 电影放映时间 = TIMESTAMP '2023-05-20 19:30:00'),
    'A5,A6,A7',
    '待支付',
    195.00
);

-- 支付订单
UPDATE 订单表 
SET 订单状态 = '已支付', 订单支付时间 = SYSDATE 
WHERE 编号 = (SELECT MAX(编号) FROM 订单表);

-- 查询用户历史订单
SELECT 
    o.订单支付时间,
    m.影片名称,
    c.影院名称,
    h.放映厅名称,
    s.电影放映时间,
    o.电影票座位信息,
    o.订单价格
FROM 订单表 o
JOIN 订单详情表 s ON o.所属场次编号 = s.编号
JOIN 影片表 m ON s.放映的电影编号 = m.编号
JOIN 放映厅表 h ON s.所属放映厅 = h.编号
JOIN 影院表 c ON h.所属影院编号 = c.编号
WHERE o.所属用户编号 = (SELECT 编号 FROM 用户表 WHERE 邮箱 = 'zhangsan@example.com');
```

### 6. 评论管理操作
```sql
-- 添加评论
INSERT INTO 评论表 (所属用户编号, 评论内容, 所属电影编号, 评分)
VALUES (
    (SELECT 编号 FROM 用户表 WHERE 邮箱 = 'zhangsan@example.com'),
    '特效震撼，中国科幻的里程碑作品',
    (SELECT 编号 FROM 影片表 WHERE 影片名称 = '流浪地球'),
    9.0
);

-- 查询影片评论
SELECT 
    u.用户名,
    c.评论内容,
    c.评分,
    c.评论时间
FROM 评论表 c
JOIN 用户表 u ON c.所属用户编号 = u.编号
WHERE c.所属电影编号 = (SELECT 编号 FROM 影片表 WHERE 影片名称 = '流浪地球')
ORDER BY c.评论时间 DESC;
```

### 7. 事务处理示例 (购票全流程)
```sql
DECLARE
    v_user_id 用户表.编号%TYPE;
    v_session_id 订单详情表.编号%TYPE;
    v_seats VARCHAR2(100) := 'B10,B11';
    v_seat_count NUMBER := 2;
    v_price NUMBER;
BEGIN
    -- 获取用户ID
    SELECT 编号 INTO v_user_id 
    FROM 用户表 WHERE 邮箱 = 'zhangsan@example.com';
    
    -- 获取场次信息和价格
    SELECT 编号, 售价 INTO v_session_id, v_price 
    FROM 订单详情表 
    WHERE 编号 = 101; -- 假设场次ID为101
    
    -- 验证座位可用性
    IF (SELECT 剩余座位数 FROM 订单详情表 WHERE 编号 = v_session_id) < v_seat_count THEN
        RAISE_APPLICATION_ERROR(-20001, '座位不足');
    END IF;
    
    -- 开始事务
    SAVEPOINT start_transaction;
    
    -- 创建订单
    INSERT INTO 订单表 (所属用户编号, 所属场次编号, 电影票座位信息, 订单状态, 订单价格)
    VALUES (v_user_id, v_session_id, v_seats, '待支付', v_price * v_seat_count);
    
    -- 锁定座位 (通过更新场次)
    UPDATE 订单详情表 
    SET 剩余座位数 = 剩余座位数 - v_seat_count 
    WHERE 编号 = v_session_id;
    
    -- 模拟支付成功
    UPDATE 订单表 
    SET 订单状态 = '已支付', 订单支付时间 = SYSDATE 
    WHERE 所属用户编号 = v_user_id 
    AND 所属场次编号 = v_session_id;
    
    COMMIT;
EXCEPTION
    WHEN OTHERS THEN
        ROLLBACK TO start_transaction;
        RAISE;
END;
/
```

### 8. 复杂查询示例
```sql
-- 查询各类型影片平均评分
SELECT 
    电影类型,
    ROUND(AVG(电影评分), 2) AS 平均评分,
    COUNT(*) AS 影片数量
FROM 影片表
GROUP BY 电影类型
HAVING AVG(电影评分) > 6.0
ORDER BY 平均评分 DESC;

-- 查询热门影片(评分高且评论多)
SELECT 
    m.影片名称,
    m.电影评分,
    COUNT(c.编号) AS 评论数量,
    SUM(o.订单价格) AS 总票房
FROM 影片表 m
LEFT JOIN 评论表 c ON m.编号 = c.所属电影编号
LEFT JOIN 订单详情表 s ON m.编号 = s.放映的电影编号
LEFT JOIN 订单表 o ON s.编号 = o.所属场次编号
GROUP BY m.影片名称, m.电影评分
HAVING COUNT(c.编号) > 1000
ORDER BY m.电影评分 DESC, 评论数量 DESC;

-- 查询用户观影偏好
SELECT 
    u.用户名,
    m.电影类型,
    COUNT(*) AS 观影次数,
    SUM(o.订单价格) AS 总消费
FROM 订单表 o
JOIN 用户表 u ON o.所属用户编号 = u.编号
JOIN 订单详情表 s ON o.所属场次编号 = s.编号
JOIN 影片表 m ON s.放映的电影编号 = m.编号
GROUP BY u.用户名, m.电影类型
ORDER BY 观影次数 DESC;
```

