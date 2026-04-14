---
name: java-coding-review
description: "Java 代码规范审查标准，覆盖编程规约、异常日志、单元测试、安全、MySQL、工程结构、设计规约七大维度。"
---

# Java 代码规范审查标准

## 激活条件

- 审查或审计 Java 源代码时
- 生成需要符合企业级规范的 Java 代码时
- 用户明确要求进行 Java 代码审查或规范检查时
- 涉及 MySQL、ORM 框架或 Web API 的 Java 项目工作时

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

## 一、编程规约

### (一) 命名风格

1. [强制] 所有编程相关的命名均不能以下划线或美元符号开始或结束
   ❌ _name / __name / $Object / name_ / name$ / Object$

2. [强制] 严禁使用拼音与英文混合命名，不允许直接使用中文
   ❌ DaZhePromotion / getPingfenByName() / String fw

3. [强制] 代码和注释中避免使用种族歧视性或侮辱性词语
   ✅ blockList / allowList / secondary
   ❌ blackList / whiteList / slave / SB / WTF

4. [强制] 类名使用UpperCamelCase风格，以下情形例外：DO/PO/DTO/BO/VO/UID等
   ❌ forcecode / UserDo / HTMLDto / XMLService / TCPUDPDeal

5. [强制] 方法名、参数名、成员变量、局部变量统一使用lowerCamelCase风格
   ✅ localValue / getHttpMessage() / inputUserId

6. [强制] 常量命名全部大写，单词间用下划线隔开，力求语义完整
   ✅ MAX_STOCK_COUNT / CACHE_EXPIRED_TIME
   ❌ MAX_COUNT / EXPIRED_TIME

7. [强制] 抽象类命名使用Abstract或Base开头；异常类使用Exception结尾；测试类以被测试类名开始，以Test结尾

8. [强制] 类型与中括号紧挨相连定义数组
   ✅ int[] arrayDemo
   ❌ String args[]

9. [强制] POJO类中布尔类型变量不要加is前缀，否则部分框架解析会引起序列化错误
   ❌ Boolean isDeleted（getter为isDeleted()，框架可能误认为字段名为deleted）

10. [强制] 包名统一使用小写，点分隔符间有且仅有一个自然语义的英语单词，包名使用单数形式

11. [强制] 避免在子父类成员变量之间、或不同代码块的局部变量之间采用完全相同的命名

12. [强制] 杜绝不规范的英文缩写，避免望文不知义
    ❌ AbstractClass缩写成AbsClass，condition缩写成condi

13. [推荐] 命名使用完整单词组合表达，以达到代码自解释
    ❌ int a;

14. [推荐] 常量与变量命名时，表示类型的名词放在词尾
    ✅ startTime / workQueue / nameList
    ❌ startedAt / QueueOfWork / listName

15. [推荐] 若模块/接口/类/方法使用设计模式，命名时需体现具体模式
    ✅ OrderFactory / LoginProxy / ResourceObserver

16. [推荐] 接口中的方法和属性不要加修饰符号（public也不要加），保持简洁，加有效Javadoc注释

17. [强制] Service和DAO类基于SOA理念，暴露服务一定是接口，内部实现类用Impl后缀与接口区别
    [推荐] 形容能力的接口名称取对应形容词（通常-able结尾）
    ✅ AbstractTranslator实现Translatable

### (二) 常量定义

1. [强制] 不允许任何魔法值（未经预先定义的常量）直接出现在代码中

2. [强制] long或Long赋值时，数值后使用大写L，不能是小写l
    ✅ Long NUM = 2L;
    ❌ Long NUM = 2l;（可能被误认为21）

3. [强制] 浮点数类型数值后缀统一为大写D或F
    ✅ double HEIGHT = 175.5D; float WEIGHT = 150.3F;

4. [推荐] 不要使用一个常量类维护所有常量，按常量功能归类分开维护

5. [推荐] 常量复用层次分五层：跨应用共享、应用内共享、子工程内共享、包内共享、类内共享

6. [推荐] 如果变量值仅在一个固定范围内变化用enum类型定义

### (三) 代码格式

1. [强制] 大括号非空代码块格式：左大括号前不换行，后换行；右大括号前换行，后还有else等则不换行

2. [强制] 左小括号和右边相邻字符间不需要空格；右小括号和左边相邻字符间也不需要空格；左大括号前需加空格

3. [强制] if/for/while/switch/do等保留字与左右括号之间必须加空格

4. [强制] 任何二目、三目运算符的左右两边都需要加一个空格

5. [强制] 采用4个空格缩进，禁止使用Tab字符

6. [强制] 注释双斜线与注释内容之间有且仅有一个空格

7. [强制] 类型强制转换时，右括号与强制转换值之间不需要空格

8. [强制] 单行字符数限制不超过120个，超出需换行
    - 第二行相对第一行缩进4个空格，从第三行开始不再继续缩进
    - 运算符与下文一起换行
    - 方法调用的点符号与下文一起换行
    - 方法调用中多个参数需换行时在逗号后进行
    - 在括号前不要换行

9. [强制] 方法参数在定义和传入时，多个参数逗号后面必须加空格

10. [强制] IDE的text file encoding设置为UTF-8；文件换行符使用Unix格式

11. [推荐] 单个方法的总行数不超过80行（除注释外）

12. [推荐] 没有必要增加空格使变量赋值等号与上一行对应位置对齐

13. [推荐] 不同逻辑、不同语义、不同业务代码间插入一个空行分隔

### (四) OOP规约

1. [强制] 避免通过类对象引用访问此类的静态变量或静态方法，直接用类名访问

2. [强制] 所有覆写方法必须加@Override注解

3. [强制] 相同参数类型、相同业务含义才可使用可变参数，参数类型避免定义为Object

4. [强制] 外部正在调用的接口或二方库依赖接口不允许修改方法签名，接口过时必须加@Deprecated注解

5. [强制] 不能使用过时的类或方法

6. [强制] Object的equals方法容易抛空指针，应使用常量或确定有值的对象调用equals
    ✅ "test".equals(param)
    ❌ param.equals("test")

7. [强制] 所有整型包装类对象之间值比较全部使用equals方法
    ❌ Integer var在-128~127区间外使用==比较

8. [强制] 任何货币金额均以最小货币单位且为整型类型存储

9. [强制] 浮点数等值判断：基本类型不能用==，包装类型不能用equals
    ✅ (1)指定误差范围：Math.abs(a - b) < diff
    ✅ (2)使用BigDecimal：x.compareTo(y) == 0

10. [强制] BigDecimal等值比较使用compareTo()而非equals()

11. [强制] DO类属性类型要与数据库字段类型匹配
    ❌ bigint unsigned字段对应Integer类型会溢出

12. [强制] 禁止使用BigDecimal(double)构造方法，存在精度损失
    ✅ new BigDecimal("0.1") 或 BigDecimal.valueOf(0.1)

13. [强制] 所有POJO类属性必须使用包装数据类型
    [强制] RPC方法返回值和参数必须使用包装数据类型
    [推荐] 局部变量使用基本数据类型

14. [强制] DO/PO/DTO/VO等POJO类不要设定任何属性默认值

15. [强制] 序列化类新增属性时不要修改serialVersionUID字段

16. [强制] 构造方法中禁止加入业务逻辑

17. [强制] POJO类必须写toString方法

18. [强制] 禁止在POJO类中同时存在对应属性xxx的isXxx()和getXxx()方法

19. [推荐] 使用索引访问String.split()得到的数组时需做最后分隔符后有无内容检查

20. [推荐] 类有多个构造方法或同名方法时应按顺序放置在一起

21. [推荐] 类内方法定义顺序：公有/保护方法 > 私有方法 > getter/setter方法

22. [推荐] setter方法中参数名与类成员变量名一致，getter/setter中不要增加业务逻辑

23. [推荐] 循环体内字符串连接使用StringBuilder的append方法
    ❌ String str = "start"; for(...) { str = str + "hello"; }

24. [推荐] final关键字使用场景：不允许被继承的类、不允许修改引用的域对象、不允许被覆写的方法、不允许运行中重新赋值的局部变量

25. [推荐] 慎用Object的clone方法拷贝对象（默认浅拷贝）

26. [推荐] 类成员与方法访问控制从严：严控访问范围，利于模块解耦

### (五) 日期时间

1. [强制] 日期格式化时pattern中表示年份统一使用小写y，大写YYYY代表week in which year
    ✅ "yyyy-MM-dd HH:mm:ss"
    ❌ "YYYY-MM-dd"（2017/12/31可能输出2018/12/31）

2. [强制] 日期格式中大写M是月份，小写m是分钟；大写H是24小时制，小写h是12小时制

3. [强制] 获取当前毫秒数使用System.currentTimeMillis()

4. [强制] 不允许使用java.sql.Date、java.sql.Time、java.sql.Timestamp

5. [强制] 禁止写死一年为365天，避免闰年错误
    ✅ LocalDate.now().lengthOfYear()
    ❌ int[] dayArray = new int[365];

6. [推荐] 避免公历闰年2月问题（闰年2月29日，一年后不可能是2月29日）

7. [推荐] 使用枚举值指代月份（Calendar.JANUARY等），注意月份范围0-11

### (六) 集合处理

1. [强制] 只要覆写equals就必须覆写hashCode；Set存储对象必须覆写；自定义对象作Map键必须覆写

2. [强制] 判断集合元素为空使用isEmpty()而非size() == 0

3. [强制] 使用Collectors.toMap()转为Map时必须指定mergeFunction参数，否则相同key抛IllegalStateException

4. [强制] 使用Collectors.toMap()时value为null会抛NPE

5. [强制] ArrayList的subList结果不可强转成ArrayList

6. [强制] Map的keySet()/values()/entrySet()返回的集合不可添加元素

7. [强制] Collections类返回的emptyList()/singletonList()等是immutable list，不可增删

8. [强制] 高度注意对父集合元素的增删会导致子列表遍历/增删抛ConcurrentModificationException

9. [强制] 集合转数组使用toArray(T[] array)，传入类型完全一致、长度为0的空数组

10. [强制] 使用Collection的addAll()方法时需对输入集合参数进行NPE判断

11. [强制] Arrays.asList()转换的集合不能使用修改集合相关方法（add/remove/clear）

12. [强制] 泛型通配符<? extends T>不能使用add方法，<? super T>不能使用get方法

13. [强制] 无泛型限制集合赋值给泛型限制集合时，使用元素需进行instanceof判断

14. [强制] 不要在foreach循环里进行元素的remove/add操作，remove使用iterator方式

15. [强制] Comparator实现类需满足三个条件：比较结果互反、传递性、相等一致性

16. [推荐] 泛型集合使用JDK7+的diamond语法<>或全省略

17. [推荐] 集合初始化时指定集合初始值大小

18. [推荐] 使用entrySet遍历Map类集合KV而非keySet方式

19. [推荐] 注意Map类集合K/V能不能存储null值
    - Hashtable/ConcurrentHashMap：Key/Value都不允许null
    - TreeMap：Key不允许null，Value允许null
    - HashMap：Key/Value都允许null

### (七) 并发处理

1. [强制] 获取单例对象需要保证线程安全，其中的方法也要保证线程安全

2. [强制] 创建线程或线程池时请指定有意义的线程名称

3. [强制] 线程资源必须通过线程池提供，不允许自行显式创建线程

4. [强制] 线程池不允许使用Executors创建，通过ThreadPoolExecutor方式
    ❌ FixedThreadPool/SingleThreadPool/CachedThreadPool/ScheduledThreadPool可能OOM

5. [强制] SimpleDateFormat是线程不安全的类，一般不定义为static变量
    ✅ 使用ThreadLocal<DateFormat>或JDK8的DateTimeFormatter

6. [强制] 必须回收自定义的ThreadLocal变量，尤其在线程池场景下

7. [强制] 高并发时同步调用应考量锁性能损耗：能用无锁就不用锁；能锁区块就不锁方法体；能用对象锁就不用类锁

8. [强制] 对多个资源/数据库表/对象同时加锁需保持一致的加锁顺序，避免死锁

9. [强制] 使用阻塞等待获取锁时，必须在try代码块之外加锁，避免加锁成功后在finally中无法解锁

10. [强制] 使用tryLock方式获取锁时，进入业务代码前必须判断当前线程是否持有锁

11. [强制] 并发修改同一记录时避免更新丢失，需要加锁：应用层/缓存层/数据库乐观锁（version）

12. [强制] 多线程并行处理定时任务使用ScheduledExecutorService而非Timer

13. [推荐] 资金相关的金融敏感信息使用悲观锁策略

14. [推荐] 使用CountDownLatch进行异步转同步操作，每个线程退出前必须调用countDown方法

15. [推荐] 避免Random实例被多线程使用，使用ThreadLocalRandom（JDK7+）

16. [推荐] 双重检查锁实现延迟初始化需将目标属性声明为volatile

### (八) 控制语句

1. [强制] switch块内每个case要通过continue/break/return等终止，或注释说明将继续执行到哪个case；必须包含default语句放在最后

2. [强制] switch括号内变量类型为String且为外部参数时必须先进行null判断

3. [强制] if/else/for/while/do语句中必须使用大括号

4. [强制] 三目运算符注意类型对齐可能抛自动拆箱导致的NPE

5. [强制] 高并发场景避免使用"等于"判断作为中断或退出条件，使用大于或小于区间判断

6. [推荐] 方法代码总行数超过10行时，return/throw等中断逻辑右大括号后加空行

7. [推荐] 表达异常分支少用if-else，改写卫语句；避免超过3层

8. [推荐] 条件判断中不执行复杂语句，将结果赋值给有意义的布尔变量

9. [推荐] 不要在条件表达式中插入赋值语句

10. [推荐] 循环体中定义对象/变量/获取数据库连接等操作尽量移至循环体外

11. [推荐] 避免采用取反逻辑运算符

12. [推荐] 公开接口需要进行入参保护，尤其是批量操作接口

### (九) 注释规约

1. [强制] 类/类属性/类方法注释必须使用Javadoc规范/** 内容 */格式

2. [强制] 所有抽象方法（包括接口方法）必须用Javadoc注释，说明方法做什么、实现什么功能

3. [强制] 所有类都必须添加创建者和创建日期

4. [强制] 方法内部单行注释使用//，多行注释使用/* */

5. [强制] 所有枚举类型字段必须要有注释说明每个数据项用途

6. [推荐] 与其用半吊子英文注释不如用中文说清楚，专有名词保持英文

7. [推荐] 代码修改时注释也要相应修改，尤其是参数/返回值/异常/核心逻辑

8. [推荐] 删除类中未使用的字段/方法/内部类，删除方法中未使用的参数与变量

### (十) 前后端规约

1. [强制] 前后端交互API需明确：协议（生产环境HTTPS）、域名、路径、请求方法、请求内容、状态码、响应体
    - 路径为名词推荐复数，不能为动词，不使用大写，单词分隔用下划线，不携带.json/.xml后缀

2. [强制] 前后端数据列表接口返回为空时返回空数组[]或空集合{}

3. [强制] 服务端错误时返回响应信息必须包含HTTP状态码、errorCode、errorMessage、用户提示信息四部分

4. [强制] JSON数据中所有key必须为lowerCamelCase风格，符合英文表达习惯
    ✅ errorCode / errorMessage / assetStatus
    ❌ ERRORCODE / ERROR_CODE / error_message

5. [强制] errorMessage可在前端输出type="hidden"控件或用户日志中帮助定位问题

6. [强制] 需要超大整数的场景服务端一律使用String返回，禁止使用Long（前端精度损失）

7. [强制] HTTP请求通过URL传递参数时不能超过2048字节

8. [强制] HTTP请求通过body传递内容时必须控制长度（nginx默认1MB，tomcat默认2MB）

9. [强制] 翻页场景用户输入参数小于1返回第一页，大于总页数返回最后一页

10. [强制] 服务器内部重定向使用forward；外部重定向地址使用URL统一代理模块生成

11. [推荐] 服务器返回信息标记是否可缓存

12. [推荐] 服务端返回数据使用JSON格式而非XML

13. [推荐] 前后端时间格式统一为"yyyy-MM-dd HH:mm:ss"，统一为GMT

### (十一) 其他

1. [强制] 使用正则表达式利用预编译功能加快匹配速度，不要在方法体内定义Pattern.compile()

2. [强制] 避免使用ApacheBeanUtils进行属性copy，性能较差

3. [强制] velocity调用POJO类属性时直接使用属性名取值

4. [强制] 后台输送给页面的变量必须加$!{var}（感叹号），否则null直接显示在页面

5. [强制] Math.random()返回double类型，范围0 ≤ x < 1，获取整数随机数使用Random对象的nextInt或nextLong

6. [强制] 枚举enum的属性字段必须是私有且不可变

7. [推荐] 不要在视图模板中加入复杂逻辑运算

8. [推荐] 任何数据结构构造或初始化都应指定大小，避免无限增长吃光内存

9. [推荐] 及时清理不再使用的代码段或配置信息

## 二、异常日志

### (一) 错误码

1. [强制] 错误码制定原则：快速溯源、沟通标准化
- 错误码必须能够快速知晓错误来源，可清晰比对，有利于团队对错误原因达成一致认知
- 回答问题：谁的错？错在哪？

2. [强制] 错误码不体现版本号和错误等级信息
- 错误码以不断追加的方式进行兼容，错误等级由日志和错误码释义决定

3. [强制] 全部正常但不得不填充错误码时返回00000

4. [强制] 错误码为字符串类型，共5位：错误来源+四位数字编号
- **A**：用户错误（参数错误、版本过低、支付超时等）
- **B**：系统错误（业务逻辑出错、程序健壮性差等）
- **C**：第三方服务错误（CDN出错、消息投递超时等）
- 编号范围：0001-9999，大类间步长预留100

```java
// 正例
String errorCode = "A0001"; // 用户端错误
String errorCode = "B1001"; // 系统执行出错
String errorCode = "C0001"; // 调用第三方服务出错
```

5. [强制] 错误码编号不与公司业务架构或组织架构挂钩
- 以先到先得原则在统一平台审批生效，编号永久固定

6. [强制] 避免随意定义新的错误码
- 优先在原有错误码附表中找语义相同或相近的错误码复用

7. [强制] 错误码不能直接输出给用户作为提示信息
- 堆栈、错误信息、错误码、提示信息各司其职，不可越俎代庖

```java
// 正例
{
  "error_code": "A0001",
  "error_message": "参数校验失败",
  "user_tip": "用户名不能为空"
}

// 反例
{
  "user_tip": "A0001"  // 错误码直接给用户
}
```

8. [推荐] 错误码之外的业务信息由error_message承载
- 错误码本身不应涵盖过多具体业务属性

9. [推荐] 获取第三方服务错误码时向上抛出允许本系统转义
- 将C类型错误转为B类型，错误信息中带上原有第三方错误码

```java
// 正例
catch (ThirdPartyException e) {
    throw new ServiceException("B2001", "第三方服务失败: " + e.getErrorCode());
}
```

---

### (二) 异常处理

1. [强制] 可预检查的RuntimeException不用catch处理
- 如NullPointerException、IndexOutOfBoundsException等应通过预检查规避

```java
// 正例
if (obj != null) {
    obj.method();
}

// 反例
try {
    obj.method();
} catch (NullPointerException e) {
    // 处理异常
}
```

2. [强制] 异常捕获不可用于流程控制或条件控制
- 异常处理效率远低于条件判断

3. [强制] catch时分清稳定代码和非稳定代码
- 对非稳定代码尽可能区分异常类型，做对应异常处理
- 避免大段代码try-catch导致无法正确应激反应

```java
// 正例
try {
    // 注册用户
} catch (InvalidCharacterException e) {
    return "包含非法字符";
} catch (DuplicateUsernameException e) {
    return "用户名已存在";
} catch (PasswordTooWeakException e) {
    return "密码过于简单";
}
```

4. [强制] 捕获异常必须处理，不处理则抛给调用者
- 最外层业务使用者必须处理异常，转化为用户可理解的内容

```java
// 反例
try {
    doSomething();
} catch (Exception e) {
    // 什么都不做，直接丢弃异常
}
```

5. [强制] 事务场景中异常被catch后如需回滚必须手动回滚

```java
// 正例
try {
    // 业务逻辑
} catch (Exception e) {
    transactionManager.rollback(status);
    throw e;
}
```

6. [强制] finally块必须关闭资源和流对象

```java
// 正例 - JDK7+使用try-with-resources
try (InputStream is = new FileInputStream(file)) {
    // 使用资源
} catch (IOException e) {
    logger.error("读取文件失败", e);
}

// 正例 - 传统方式
InputStream is = null;
try {
    is = new FileInputStream(file);
    // 使用资源
} catch (IOException e) {
    logger.error("读取文件失败", e);
} finally {
    if (is != null) {
        try {
            is.close();
        } catch (IOException e) {
            // 关闭异常也要处理
        }
    }
}
```

7. [强制] 不要在finally块中使用return

```java
// 反例 - finally中的return会丢弃try块中的返回值
private int x = 0;
public int checkReturn() {
    try {
        return ++x;  // x=1，但不会返回
    } finally {
        return ++x;  // 返回2，丢弃了try中的返回点
    }
}
```

8. [强制] 捕获异常与抛异常必须完全匹配或为父子类关系

```java
// 正例
try {
    throw new IOException();
} catch (IOException e) {
    // 处理
}

// 反例
try {
    throw new IOException();
} catch (SQLException e) {
    // 永远不会捕获到
}
```

9. [强制] RPC/二方包/动态生成类调用时用Throwable拦截

```java
// 正例
try {
    // 通过反射调用方法
    Method method = clazz.getMethod(methodName);
    method.invoke(obj);
} catch (Throwable t) {
    // 捕获Throwable，包括Exception和Error
    logger.error("调用失败", t);
}
```

10. [推荐] 方法返回值可为null，但必须注释说明何时返回null

```java
/**
 * 根据ID查询用户
 * @param id 用户ID
 * @return 用户对象，不存在时返回null
 */
public User findById(Long id) {
    return userMapper.selectById(id);
}
```

11. [推荐] 防止NPE是程序员基本修养，注意产生场景

1. 基本类型返回值，自动拆箱包装类型可能NPE
2. 数据库查询结果可能为null
3. 集合元素可能为null（即使isNotEmpty）
4. 远程调用返回对象必须判空
5. Session中获取的数据建议NPE检查
6. 级联调用`obj.getA().getB().getC()`易产生NPE

```java
// 反例 - 自动拆箱NPE
public int method() {
    return Integer对象;  // 如果为null，抛NPE
}

// 正例 - 使用Optional
Optional.ofNullable(user)
    .map(User::getAddress)
    .map(Address::getCity)
    .orElse("未知");
```

12. [推荐] 区分unchecked/checked异常，避免直接抛RuntimeException
- 不允许抛出Exception或Throwable
- 使用有业务含义的自定义异常，如DAOException、ServiceException

```java
// 正例
public class BusinessException extends RuntimeException {
    private String errorCode;
    // ...
}

// 反例
throw new RuntimeException("错误");
throw new Exception("错误");
throw new Throwable("错误");
```

---

### (三) 日志规约

1. [强制] 使用日志框架（SLF4J、JCL）而非直接使用日志系统API

```java
// 正例 - 使用SLF4J
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
private static final Logger logger = LoggerFactory.getLogger(Test.class);

// 正例 - 使用JCL
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
private static final Log log = LogFactory.getLog(Test.class);

// 反例 - 直接使用Log4j或Logback
import org.apache.log4j.Logger;
import org.slf4j.impl.Log4jLoggerFactory;
```

2. [强制] 日志文件至少保存15天

**日志保存规则：**
- 当天日志：`{应用名}.log`
- 保存目录：`/{统一目录}/{应用名}/logs/`
- 历史日志：`{logname}.log.yyyy-MM-dd`

3. [强制] 敏感信息操作日志留存不少于六个月并多机备份

4. [强制] 扩展日志命名格式：`appName_logType_logName.log`

- **logType**：stats/monitor/access等
- **logName**：日志描述

```java
// 正例
mppserver_monitor_timeZoneConvert.log
trade_stats_orderCreate.log
user_access_login.log
```

5. [强制] 日志输出使用占位符而非字符串拼接

```java
// 正例
logger.debug("Processing trade with id: {} and symbol: {}", id, symbol);

// 反例
logger.debug("Processing trade with id: " + id + " and symbol: " + symbol);
```

6. [强制] trace/debug/info级别日志必须进行级别判断

```java
// 正例
if (logger.isDebugEnabled()) {
    logger.debug("Current ID is: {} and name is: {}", id, getName());
}
```

7. [强制] 避免重复打印日志，设置additivity=false

```xml
<!-- 正例 -->
<logger name="com.taobao.dubbo.config" additivity="false">
    <appender-ref ref="dubbo-appender" />
</logger>
```

8. [强制] 生产环境禁止使用System.out/System.err或printStackTrace

```java
// 反例
System.out.println("debug info");
System.err.println("error info");
e.printStackTrace();
```

9. [强制] 异常信息须包含案发现场信息和异常堆栈信息

```java
// 正例
logger.error("inputParams: {} and errorMessage: {}", params, e.getMessage(), e);

// 反例
logger.error("Something went wrong");  // 缺少现场信息
logger.error(e.getMessage());  // 缺少堆栈
```

10. [强制] 禁止直接用JSON工具将对象转换成String打印日志
- 某些get方法被覆写可能抛异常，影响业务流程

```java
// 正例
logger.info("Order info: id={}, amount={}", order.getId(), order.getAmount());
logger.info("Order info: {}", order.toString());  // 假设toString()实现安全

// 反例
logger.info("Order info: {}", JSON.toJSONString(order));  // 可能触发异常
```

11. [推荐] 谨慎记录日志
- 生产环境禁止输出debug日志
- 有选择地输出info日志
- 使用warn记录上线观察信息时注意输出量，及时删除

12. [推荐] 用户输入参数错误使用warn级别，避免error级别频繁报警

```java
// 正例
if (invalidInput(param)) {
    logger.warn("用户输入参数错误: param={}", param);
    return "参数错误";
}
```

13. [推荐] 尽量用英文描述日志错误信息
- 英文描述不清时使用中文
- 国际化团队或海外部署建议全英文

14. [推荐] 用户敏感信息需脱敏处理

```java
// 正例
// 手机号脱敏：139****1219
// 身份证脱敏：3101**********1234
logger.info("用户登录: userId={}, mobile={}", userId, maskMobile(mobile));
```

## 三、单元测试

1. [强制] AIR原则
- 好的单元测试必须遵守AIR原则：Automatic（自动化）、Independent（独立性）、Repeatable（可重复）
- 单元测试在线上运行时应像空气一样无感，但却是质量保障的关键

2. [强制] 全自动执行
- 单元测试必须全自动执行且非交互式，使用assert验证而非System.out人肉验证
- 输出结果需人工检查的测试不是好的单元测试

```java
// ❌ 错误：使用System.out进行人工验证
@Test
public void testBad() {
    System.out.println(user.getName()); // 需要人工查看输出
}

// ✅ 正确：使用assert自动验证
@Test
public void testGood() {
    assertEquals("张三", user.getName()); // 自动验证
}
```

3. [强制] 保持独立性
- 单元测试用例之间决不能互相调用，也不能依赖执行的先后次序
- 保证单元测试稳定可靠且便于维护

4. [强制] 可重复执行
- 单元测试不能受到外界环境（网络、服务、中间件等）的影响
- 设计代码时应把SUT的依赖改成注入，测试时用DI框架注入本地或Mock实现

```java
// ❌ 错误：直接依赖外部环境
@Test
public void testBad() {
    User user = userService.queryFromRemoteAPI(123L); // 依赖外部API
}

// ✅ 正确：使用Mock实现
@Test
public void testGood() {
    when(userService.getById(123L)).thenReturn(mockUser);
    User user = userService.getById(123L);
}
```

5. [强制] 测试粒度
- 单元测试粒度至多是类级别，一般是方法级别
- 测试粒度小才能在出错时快速定位问题，不负责跨类或跨系统的交互逻辑

```java
// ❌ 错误：测试跨类交互
@Test
public void testBad() {
    // 测试Controller -> Service -> DAO 整个流程
    controller.process();
}

// ✅ 正确：测试单个方法
@Test
public void testGood() {
    // 只测试Service层的单个业务方法
    assertEquals("result", service.calculate(x, y));
}
```

6. [强制] 核心模块覆盖
- 核心业务、核心应用、核心模块的增量代码确保单元测试通过
- 新增代码及时补充单元测试，影响原有测试时及时修正

7. [强制] 目录规范
- 单元测试代码必须写在`src/test/java`目录，不允许写在业务代码目录下
- 源码编译时会跳过此目录，单元测试框架默认扫描此目录

```
项目结构/
├── src/
│   ├── main/java/          # 业务代码
│   └── test/java/          # 单元测试代码（必须在此目录）
```

8. [推荐] 代码覆盖率
- 单测基本目标：语句覆盖率达到70%
- 核心模块的语句覆盖率和分支覆盖率都要达到100%

9. [推荐] BCDE原则
编写单元测试代码遵守BCDE原则：
- **B**order：边界值测试（循环边界、特殊取值、特殊时间点、数据顺序等）
- **C**orrect：正确的输入，并得到预期的结果
- **D**esign：与设计文档相结合编写单元测试
- **E**rror：强制错误信息输入（非法数据、异常流程、业务允许外等），并得到预期结果

```java
@Test
public void testUserAge() {
    // Border: 边界值测试
    assertEquals(0, calculator.calculateAge(0));
    assertEquals(150, calculator.calculateAge(150));

    // Correct: 正确输入
    assertEquals(18, calculator.calculateAge(LocalDate.of(2006, 1, 1)));

    // Error: 异常输入
    assertThrows(IllegalArgumentException.class, () -> calculator.calculateAge(-1));
    assertThrows(IllegalArgumentException.class, () -> calculator.calculateAge(200));
}
```

10. [推荐] 数据准备
- 对于数据库相关的操作，不能假设数据库里的数据存在
- 使用程序插入或导入数据的方式来准备数据，不能手动操作数据库

```java
// ❌ 错误：假设数据库中有数据或手动插入
@Test
public void testBad() {
    // 假设数据库中存在id=1的用户，但测试可能失败
    user = userService.findById(1L);
}

// ✅ 正确：使用程序准备数据
@Test
public void testGood() {
    User user = createUser(1L, "测试用户");
    userRepository.save(user);
    assertNotNull(userService.findById(1L));
}
```

11. [推荐] 数据库回滚
- 和数据库相关的单元测试，可设定自动回滚机制，不给数据库造成脏数据
- 或者对单元测试产生的数据有明确的前后缀标识

```java
@Test
@Transactional // 自动回滚
@Rollback
public void testDatabase() {
    // 测试数据在测试结束后自动回滚，不污染数据库
    userRepository.save(new User("test"));
}

// 或使用明确前缀标识
@Test
public void testDatabase() {
    User user = new User("FOUNDATION_UNIT_TEST_用户名");
}
```

12. [推荐] 代码可测性
- 对于不可测的代码在适当时机做必要的重构，使代码变得可测
- 避免为了达到测试要求而书写不规范的测试代码

13. [推荐] 测试范围确定
- 在设计评审阶段，开发人员需要和测试人员一起确定单元测试范围
- 单元测试最好覆盖所有测试用例（UC）

14. [推荐] 测试时机
- 单元测试作为一种质量保障手段，在项目提测前完成
- 不建议项目发布后补充单元测试用例

---

## 四、安全规约

1. [强制] 权限控制校验
- 隶属于用户个人的页面或功能必须进行权限控制校验
- 防止没有做水平权限校验就可随意访问、修改、删除别人的数据

```java
// ❌ 错误：未进行权限校验
@GetMapping("/message/{id}")
public Message getMessage(@PathVariable Long id) {
    // 任何人都可以访问任意消息
    return messageService.getById(id);
}

// ✅ 正确：进行权限校验
@GetMapping("/message/{id}")
public Message getMessage(@PathVariable Long id, Principal principal) {
    Message msg = messageService.getById(id);
    if (!msg.getUserId().equals(getCurrentUserId(principal))) {
        throw new ForbiddenException("无权访问");
    }
    return msg;
}
```

2. [强制] 敏感数据脱敏
- 用户敏感数据禁止直接展示，必须对展示数据进行脱敏
- 防止隐私泄露，如手机号显示：139****1219

```java
// ❌ 错误：直接展示敏感数据
public String toString() {
    return "User{" +
        "name='" + name + '\'' +
        ", phone='" + phone + '\'' + // 13812345678 完整显示
        '}';
}

// ✅ 正确：脱敏处理
public String toSafeString() {
    return "User{" +
        "name='" + name + '\'' +
        ", phone='" + DesensitizedUtil.mobilePhone(phone) + '\'' + // 138****5678
        '}';
}
```

3. [强制] 防止SQL注入
- 用户输入的SQL参数严格使用参数绑定或METADATA字段值限定
- 禁止字符串拼接SQL访问数据库

```java
// ❌ 错误：字符串拼接SQL，存在注入风险
String sql = "SELECT * FROM user WHERE name = '" + userName + "'";
// 输入：admin' OR '1'='1
// 结果：SELECT * FROM user WHERE name = 'admin' OR '1'='1'

// ✅ 正确：使用参数绑定
String sql = "SELECT * FROM user WHERE name = ?";
jdbcTemplate.queryForObject(sql, String.class, userName);

// ✅ 正确：使用MyBatis参数绑定
@Select("SELECT * FROM user WHERE name = #{name}")
User findByName(@Param("name") String name);
```

4. [强制] 参数有效性验证
- 用户请求传入的任何参数必须做有效性验证
- 忽略参数校验可能导致：内存溢出、慢查询、缓存击穿、SSRF、任意重定向、注入攻击、ReDoS等

```java
// ❌ 错误：未进行参数验证
@GetMapping("/list")
public List<User> list(@RequestParam Integer pageSize) {
    // 恶意请求：?pageSize=99999999 导致内存溢出
    return userService.list(pageSize);
}

// ✅ 正确：进行参数验证
@GetMapping("/list")
public List<User> list(@RequestParam @Min(1) @Max(100) Integer pageSize) {
    return userService.list(pageSize);
}
```

5. [强制] 防止XSS攻击
- 禁止向HTML页面输出未经安全过滤或未正确转义的用户数据
- XSS跨站脚本攻击可导致获取用户cookie、钓鱼、获取用户页面数据、蠕虫、挂马等危害

```java
// ❌ 错误：直接输出用户数据
model.addAttribute("content", userInput); // 包含 <script>alert('XSS')</script>

// ✅ 正确：进行HTML转义
model.addAttribute("content", HtmlUtils.htmlEscape(userInput));

// ✅ 正确：使用模板引擎自动转义（Thymeleaf默认转义）
<div th:text="${content}"></div>
```

6. [强制] CSRF安全验证
- 表单、AJAX提交必须执行CSRF安全验证
- CSRF跨站请求伪造可导致攻击者在用户不知情的情况下修改用户数据

```java
// ✅ 正确：使用Spring Security的CSRF防护
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http.csrf().csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse());
        return http.build();
    }
}
```

7. [强制] URL重定向白名单
- URL外部重定向传入的目标地址必须执行白名单过滤
- 攻击者通过恶意构造跳转链接可发起钓鱼攻击

```java
// ❌ 错误：直接使用用户输入的URL进行重定向
@GetMapping("/redirect")
public String redirect(@RequestParam String url) {
    return "redirect:" + url; // 可被恶意利用：?url=http://evil.com
}

// ✅ 正确：白名单验证
@GetMapping("/redirect")
public String redirect(@RequestParam String url) {
    List<String> whiteList = Arrays.asList(
        "https://example.com",
        "https://app.example.com"
    );
    if (whiteList.contains(url)) {
        return "redirect:" + url;
    }
    throw new IllegalArgumentException("非法的跳转地址");
}
```

8. [强制] 防重放机制
- 使用平台资源（短信、邮件、电话、下单、支付）时必须实现正确的防重放机制
- 如数量限制、疲劳度控制、验证码校验，避免被滥刷导致资损

```java
// ✅ 正确：实现防刷机制
@Service
public class SmsService {
    private static final int MAX_DAILY_SMS = 10;
    private static final int MIN_INTERVAL_SECONDS = 60;

    public void sendSms(String phone) {
        // 检查每日发送次数
        if (getTodayCount(phone) >= MAX_DAILY_SMS) {
            throw new BusinessException("超过每日发送限制");
        }
        // 检查发送间隔
        if (getLastSendTime(phone) > MIN_INTERVAL_SECONDS) {
            throw new BusinessException("发送过于频繁");
        }
        // 发送短信...
    }
}
```

9. [强制] 文件上传检查
- 对于文件上传功能，需要对文件大小、类型进行严格检查和控制
- 攻击者可利用上传漏洞上传恶意文件并远程执行，控制网站服务器

```java
// ✅ 正确：严格检查上传文件
@PostMapping("/upload")
public Result upload(@RequestParam MultipartFile file) {
    // 检查文件大小
    if (file.getSize() > 10 * 1024 * 1024) {
        return Result.error("文件大小不能超过10MB");
    }
    // 检查文件类型（通过MIME和扩展名双重验证）
    String contentType = file.getContentType();
    String originalFilename = file.getOriginalFilename();
    if (!ALLOWED_TYPES.contains(contentType)
        || !hasAllowedExtension(originalFilename)) {
        return Result.error("不支持的文件类型");
    }
    // 重命名文件，防止路径遍历攻击
    String filename = UUID.randomUUID() + getFileExtension(originalFilename);
    // ...
}
```

10. [强制] 密码加密
- 配置文件中的密码需要加密存储

```properties
db.password=MySecretPassword123

db.password=ENC(AQ5G8xK9...)
```


11. [推荐] 内容风控策略
- 发贴、评论、发送即时消息等需要用户输入内容的场景
- 必须实现防刷、内容违禁词过滤等风控策略

```java
@Service
public class CommentService {
    public void postComment(Comment comment) {
        // 防刷：检查提交频率
        if (isSpamming(comment.getUserId())) {
            throw new BusinessException("提交过于频繁");
        }
        // 违禁词过滤
        if (containsForbiddenWords(comment.getContent())) {
            throw new BusinessException("内容包含违规词汇");
        }
        commentRepository.save(comment);
    }
}
```

## 五、MySQL 数据库

### (一) 建表规约


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

### (二) 索引规约


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

### (三) SQL 语句


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

---

### (四) ORM 映射


1. [强制] 查询禁止使用*，必须明确列出所需字段。

```sql
-- ✅ 正确
SELECT id, name, email FROM user WHERE id = ?;

-- ❌ 错误
SELECT * FROM user WHERE id = ?;
```

2. [强制] POJO布尔属性不加is，数据库字段必须加is_，在resultMap中映射。

```xml
<!-- ✅ 正确 -->
<resultMap id="BaseResultMap" type="com.example.User">
  <id column="id" property="id"/>
  <result column="is_deleted" property="deleted"/>
  <result column="is_enabled" property="enabled"/>
</resultMap>
```

3. [强制] 必须定义resultMap，即使属性名与字段名一一对应。

```xml
<!-- ✅ 正确：始终定义resultMap -->
<resultMap id="BaseResultMap" type="com.example.User">
  <id column="id" property="id"/>
  <result column="user_name" property="userName"/>
</resultMap>
<select id="selectById" resultMap="BaseResultMap">
  SELECT id, user_name FROM user WHERE id = #{id}
</select>

<!-- ❌ 错误：使用resultClass -->
<select id="selectById" resultClass="com.example.User">
  SELECT id, user_name FROM user WHERE id = #{id}
</select>
```

4. [强制] sql.xml配置使用#{}或#param#，禁止使用${}防止SQL注入。

```xml
<!-- ✅ 正确：预编译 -->
<select id="selectById">
  SELECT * FROM user WHERE id = #{id}
</select>

<!-- ❌ 错误：字符串拼接，SQL注入风险 -->
<select id="selectById">
  SELECT * FROM user WHERE id = ${id}
</select>
```

5. [强制] 禁止使用iBATIS的queryForList(statementName, start, size)实现分页，会先查询全部数据再subList导致OOM。

6. [强制] 禁止直接使用HashMap/Hashtable作为查询结果集输出。

```java
// ❌ 错误：类型不明确，可能解析问题
List<Map<String, Object>> result = sqlSession.selectList("selectUser");

// ✅ 正确：使用明确的DO/DTO
List<UserDO> result = sqlSession.selectList("selectUser");
```

7. [强制] 更新记录时必须同时更新update_time字段为当前时间。

```xml
<!-- ✅ 正确 -->
<update id="update">
  UPDATE user SET
    name = #{name},
    email = #{email},
    update_time = NOW()
  WHERE id = #{id}
</update>
```


8. [推荐] 不要写大而全的更新接口，只更新有变化的字段。

```xml
<!-- ✅ 正确：动态SQL，只更新变化的字段 -->
<update id="update">
  UPDATE user
  <set>
    <if test="name != null">name = #{name},</if>
    <if test="email != null">email = #{email},</if>
    update_time = NOW()
  </set>
  WHERE id = #{id}
</update>

<!-- ❌ 错误：全字段更新 -->
UPDATE user SET name = #{name}, email = #{email}, phone = #{phone} WHERE id = #{id};
```

## 六、工程结构

#### (一) 应用分层

1. [推荐] 遵循标准分层架构：开放API层 → Web层 → Service层 → Manager层 → DAO层，上层可依赖下层。

分层职责说明：
- **开放API层**：封装Service接口暴露为RPC接口或HTTP接口
- **Web层（Controller层）**：访问控制转发、参数校验、简单业务处理
- **Service层**：核心业务逻辑服务层
- **Manager层**：通用业务处理层（第三方封装、缓存下沉、多DAO组合）
- **DAO层**：数据访问层，与数据库交互

❌ 反例：Web层直接操作数据库，跳过Service层
✅ 正例：
```java
// Web层
@RestController
public class UserController {
    @Autowired
    private UserService userService;  // 依赖Service层

    @GetMapping("/user/{id}")
    public UserVO getUser(@PathVariable Long id) {
        return userService.getUserById(id);
    }
}

// Service层
@Service
public class UserService {
    @Autowired
    private UserDao userDao;  // 依赖DAO层

    public UserVO getUserById(Long id) {
        UserDO userDO = userDao.findById(id);
        return UserConvertor.toVO(userDO);
    }
}
```

---

#### (二) 二方库依赖

1. [强制] GAV坐标定义规范：
- **GroupId**：`com.{公司/BU}.业务线.[子业务线]`，最多4级
- **ArtifactId**：`产品线名-模块名`，语义不重复不遗漏
- **Version**：`主版本号.次版本号.修订号`，起始版本必须为1.0.0

❌ 反例：`com.alibaba < artifactId>dubbo < version>0.0.1`
✅ 正例：`com.alibaba < artifactId>dubbo-client < version>1.0.0`

2. [强制] 线上应用禁止依赖SNAPSHOT版本（安全包除外），正式发布的类库必须先去中央仓库验证。

3. [强制] 二方库新增或升级时，保持除功能点外的其它jar包仲裁结果不变，如有改变必须明确评估和验证。

4. [强制] 二方库接口返回值不允许使用枚举类型或包含枚举类型的POJO对象（参数可使用枚举）。

❌ 反例：
```java
// 二方库接口返回值使用枚举
public enum StatusEnum {
    ACTIVE, INACTIVE
}

public Result getUser() {
    return Result.success(StatusEnum.ACTIVE);  // ❌ 返回值包含枚举
}
```

✅ 正例：
```java
public Result getUser() {
    return Result.success("ACTIVE");  // ✅ 返回String
}
```

5. [强制] 二方库定制包命名：版本号后加`-英文说明[序号]`，如`fastjson-1.0.0-SCM1`。

6. [强制] 依赖二方库群时，必须定义统一版本变量，避免版本不一致。

❌ 反例：
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.0.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.0.2</version>  <!-- ❌ 版本不一致 -->
</dependency>
```

✅ 正例：
```xml
<properties>
    <spring.version>5.0.1</spring.version>
</properties>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>${spring.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>${spring.version}</version>  <!-- ✅ 版本统一 -->
</dependency>
```

7. [强制] 禁止在子项目pom依赖中出现相同GroupId和ArtifactId但不同Version的情况。

8. [推荐] 底层基础技术框架、核心数据管理平台、近硬件端系统谨慎引入第三方实现。

9. [推荐] pom文件中依赖声明放在`<dependencies>`，版本仲裁放在`<dependencyManagement>`。

10. [推荐] 二方库不要有配置项，最低限度不要再增加配置项。

11. [推荐] 不要使用不稳定的工具包或Utils类，优先使用业界稳定的二方工具包。

---

#### (三) 服务器

1. [强制] 调用远程操作必须设置超时时间。

❌ 反例：
```java
// ❌ 没有设置超时
HttpClient client = new DefaultHttpClient();
HttpGet request = new HttpGet("http://example.com");
HttpResponse response = client.execute(request);  // 可能无限等待
```

✅ 正例：
```java
// ✅ 设置连接超时和读取超时
RequestConfig config = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(10000)
    .build();

HttpClient client = HttpClients.custom()
    .setDefaultRequestConfig(config)
    .build();
```

2. [推荐] 客户端远程接口超时设置生效顺序：客户端Special Method > 客户端接口级别 > 服务端Special Method > 服务端接口级别。

3. [推荐] 高并发服务器调小TCP协议的`time_wait`超时时间（Linux默认240秒，建议调整为30秒）。

4. [推荐] 调大服务器支持的最大文件句柄数（File Descriptor），Linux默认1024，建议调高数倍。

5. [推荐] JVM设置`-XX:+HeapDumpOnOutOfMemoryError`参数，OOM时输出dump信息便于排查。

6. [推荐] 生产环境JVM的`Xms`和`Xmx`设置相同大小，避免GC后调整堆大小带来压力。

7. [推荐] 为耗时较长的服务配置独立线程池，与主线程池隔离。

❌ 反例：
```java
// ❌ 慢服务和快服务共用线程池
@Async
public void fastService() { }

@Async
public void slowService() {
    Thread.sleep(10000);  // 阻塞线程池
}
```

✅ 正例：
```java
// ✅ 为慢服务配置独立线程池
@Bean("slowExecutor")
public Executor slowExecutor() {
    ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
    executor.setCorePoolSize(10);
    executor.setMaxPoolSize(20);
    executor.setQueueCapacity(100);
    executor.setThreadNamePrefix("slow-");
    return executor;
}

@Async("slowExecutor")
public void slowService() {
    Thread.sleep(10000);
}
```

---

## 七、设计规约

1. [强制] 存储方案和底层数据结构设计必须评审通过并沉淀文档，包括存储介质选型、表结构设计、性能评估、索引设计等。

2. [强制] 需求分析阶段，如与系统交互的User超过一类且UseCase超过5个，使用用例图表达。

3. [强制] 业务对象状态超过3个时，使用状态图表达并明确状态变化触发条件。

❌ 反例：订单状态用魔法值或简单字符串表示
```java
order.setStatus("已付款");  // ❌ 状态关系不明确
```

✅ 正例：
```java
public enum OrderStatus {
    CREATED, PENDING_PAYMENT, PAID, PENDING_DELIVERY,
    DELIVERED, RECEIVED, CANCELLED
}

// 明确状态转换规则
OrderStatus.CAN_TRANSITION_FROM[OrderStatus.PAID] = OrderStatus.PENDING_DELIVERY;
```

4. [强制] 功能调用链路涉及对象超过3个时，使用时序图表达并明确各环节输入输出。

5. [强制] 系统中模型类超过5个且存在复杂依赖关系时，使用类图表达并明确类之间关系。

6. [强制] 超过2个对象存在协作关系且需表示复杂处理流程时，使用活动图表示。

7. [强制] 系统设计要识别弱依赖并设计降级和应急预案，保证核心系统可用。

❌ 反例：
```java
// ❌ 外部服务故障导致主流程中断
public OrderDTO getOrderDetail(Long orderId) {
    OrderDTO order = orderDao.findById(orderId);
    // 调用外部服务获取推荐商品，超时导致整个接口失败
    List<Product> recommendations = externalService.getRecommendations(order.getUserId());
    order.setRecommendations(recommendations);
    return order;
}
```

✅ 正例：
```java
// ✅ 降级处理，保证主流程可用
public OrderDTO getOrderDetail(Long orderId) {
    OrderDTO order = orderDao.findById(orderId);
    try {
        List<Product> recommendations = externalService.getRecommendations(order.getUserId());
        order.setRecommendations(recommendations);
    } catch (Exception e) {
        // 降级：外部服务故障时使用默认推荐或空列表
        order.setRecommendations(Collections.emptyList());
        log.warn("推荐服务降级，orderId={}", orderId, e);
    }
    return order;
}
```

8. [推荐] 系统架构设计要明确：系统边界、模块间依赖关系、设计演化原则、非功能性需求（安全性、可用性、可扩展性）。

9. [推荐] 需求分析与系统设计需充分评估异常流程与业务边界。

10. [推荐] 类设计遵循单一职责原则。

❌ 反例：
```java
// ❌ 一个类承担多个职责
public class UserService {
    public User getUser(Long id) { }
    public void sendEmail(User user) { }  // 邮件职责
    public void generateReport(List<User> users) { }  // 报表职责
}
```

✅ 正例：
```java
// ✅ 职责分离
public class UserService {
    public User getUser(Long id) { }
}

public class EmailService {
    public void sendEmail(User user) { }
}

public class ReportService {
    public void generateReport(List<User> users) { }
}
```

11. [推荐] 优先使用聚合/组合实现扩展，谨慎使用继承，使用继承必须符合里氏代换原则。

❌ 反例：违反里氏代换原则
```java
// ❌ 子类改变了父类的行为约定
class Rectangle {
    public void setWidth(int width) { }
    public void setHeight(int height) { }
}

class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);  // 强制正方形，违反父类契约
    }
}
```

12. [推荐] 系统设计遵循依赖倒置原则，依赖抽象类与接口，便于扩展维护。

13. [推荐] 遵循开闭原则：对扩展开放，对修改关闭。

14. [推荐] 遵循DRY原则，抽取共性业务或公共行为到公共模块、公共类、公共方法，避免重复代码。

❌ 反例：
```java
// ❌ 重复的参数校验
public void method1(DTO dto) {
    if (dto == null || dto.getId() == null) {
        throw new IllegalArgumentException();
    }
    // ...
}

public void method2(DTO dto) {
    if (dto == null || dto.getId() == null) {  // 重复代码
        throw new IllegalArgumentException();
    }
    // ...
}
```

✅ 正例：
```java
// ✅ 抽取公共方法
private void validateDto(DTO dto) {
    if (dto == null || dto.getId() == null) {
        throw new IllegalArgumentException();
    }
}

public void method1(DTO dto) {
    validateDto(dto);
    // ...
}

public void method2(DTO dto) {
    validateDto(dto);
    // ...
}
```

15. [推荐] 敏捷开发不等于省略必要设计和文档，核心关键点需要设计文档沉淀。

---

### 附：分层领域模型规约（参考）

| 模型 | 说明 | 使用层级 |
|------|------|----------|
| DO（Data Object） | 与数据库表结构一一对应 | DAO层向上传输 |
| DTO（Data Transfer Object） | 数据传输对象 | Service/Manager向外传输 |
| BO（Business Object） | 业务对象，封装业务逻辑 | Service层输出 |
| Query | 数据查询对象 | 各层接收上层查询请求 |
| VO（View Object） | 显示层对象 | Web层向模板渲染传输 |
