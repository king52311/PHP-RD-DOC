# php编码规范（参考阿里巴巴JAVA编码规范）
------
### 一、编程规约
#### a、命名规约

变量：不知道类型的用大写字母开头。否则：
    字符串 = $sMyName
    数组 = $aMyCard	二维数组 = $aaMyCard
    对象 = $oMyObject
    资源 = $resource
    布尔值 = $flag
    整型 = $iMyNumber
    浮点型 = $fMyMoney

类名命名规则 = ‘i’ + 接口命名规则   例如：MyClass iMyInterface

数据库中的所有内容命名不得有大写字母。表名和字段用下划线连接单词，例如：blog_user_info。

部分缩写：
image = img
string = str
database = db
count = cnt
temporary = tmp
password = pwd
message = msg

代码注释应该描述为什么，而不是做什么。

SQL尽量不要写在函数里面，而是先赋给变量，再交给函数。
1.代码中的命名均不能以下划线或美元符号开始，也不能以下划线或美元符号结束。
反例： name / __name / $Object / name / name$ / Object$

2.代码中的命名严禁使用拼音与英文混合的方式。
正例： alibaba / taobao / youku / hangzhou 等国际通用的名称，可视同英文。

3. 【强制】类名使用 UpperCamelCase 风格，必须遵从驼峰形式，但以下情形例外：（领域模型
的相关命名）PDO 等。
正例：MarcoPolo / UserDO / XmlService / TcpUdpDeal / TaPromotion
反例：macroPolo / UserDo / XMLService / TCPUDPDeal / TAPromotion

4.【强制】方法名、参数名、成员变量、局部变量都统一使用 lowerCamelCase 风格，必须遵从
驼峰形式。

5. 【强制】常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚，不要嫌名字长。
正例： MAX_STOCK_COUNT

6. 【强制】类名特性应在结尾出表明：异常类命名使用 Exception 结尾；测试类
命名以它要测试的类的名称开始，以 Test 结尾。

7. 【强制】杜绝完全不规范的缩写，避免望文不知义。
反例： AbstractClass“缩写”命名成 AbsClass；condition“缩写”命名成 condi，此类
随意缩写严重降低了代码的可阅读性。

. 【推荐】如果使用到了设计模式，建议在类名中体现出具体模式。
正例：public class OrderFactory;
public class LoginProxy;
public class ResourceObserver;
#### b、格式规约
1. 【强制】大括号的使用约定。如果是大括号内为空，则简洁地写成{}即可，不需要换行；如果
是非空代码块则：
1） 左大括号前不换行。
2） 左大括号后换行。
3） 右大括号前换行。
4） 右大括号后还有 else 等代码则不换行；表示终止右大括号后必须换行。

2. 【强制】 左括号和后一个字符之间不出现空格；同样，右括号和前一个字符之间也不出现空
格。详见第 5 条下方正例提示。

3. 【强制】if/for/while/switch/do 等保留字与左右括号之间都必须加空格。

4. 【强制】任何运算符左右必须加一个空格。
说明：运算符包括赋值运算符=、逻辑运算符&&、加减乘除符号、三目运行符等。

5. 【强制】缩进采用 4 个空格，禁止使用 tab 字符。
说明：如果使用 tab 缩进，必须设置 1 个 tab 为 4 个空格。IDEA 设置 tab 为 4 个空格时，
请勿勾选 Use tab character；而在 eclipse 中，必须勾选 insert spaces for tabs。

正例： （涉及 1-5 点）
public static function student($id){
    //四个空格
    $id = 12;
    if ( $id == 1 ){
        echo 'no';
    } else {
        echo 'yes';
    }
}

6. 【强制】单行字符数限制不超过 120 个，超出需要换行，换行时遵循如下原则：
1） 第二行相对第一行缩进 4 个空格，从第三行开始，不再继续缩进，参考示例。
2） 运算符与下文一起换行。
3） 方法调用的符号与下文一起换行。
4） 在多个参数超长，逗号后进行换行。
5） 在括号前不要换行，见反例。

正例：
if ($a == $b || $c == $b
    || $b != $d && in_array($s,
    $arr))

7. 【强制】方法参数在定义和传入时，多个参数逗号后边必须加空格。
正例：下例中实参的"a",后边必须要有一个空格。
method("a", "b", "c");

8. 【强制】IDE 的 text file encoding 设置为 UTF-8; IDE 中文件的换行符使用 Unix 格式，
不要使用 windows 格式。

9. 【推荐】没有必要增加若干空格来使某一行的字符与上一行的相应字符对齐。
正例：
int a = 3;
long b = 4L;
float c = 5F;
StringBuffer sb = new StringBuffer();

10. 【推荐】方法体内的执行语句组、变量的定义语句组、不同的业务逻辑之间或者不同的语义
之间插入一个空行。相同业务逻辑和语义之间不需要插入空行。
说明：没有必要插入多行空格进行隔开。
#### c、OOP
1. 【强制】避免通过一个类的对象引用访问此类的静态变量或静态方法，直接用类名来访问即可。

2. 【强制】所有的覆写方法，必须加@Override 注解。
反例：getObject()与 get0bject()的问题。一个是字母的 O，一个是数字的 0，加@Override
可以准确判断是否覆盖成功。另外，如果在抽象类中对方法签名进行修改，其实现类会马上编
译报错。

3. 【强制】构造方法里面禁止加入任何业务逻辑。

4. 【推荐】 类内方法定义顺序依次是：公有方法或保护方法 > 私有方法 > 魔术方法。

5. 【推荐】final 可提高程序响应效率，声明成 final 的情况：
1） 不需要重新赋值的变量，包括类属性、局部变量。
2） 对象参数前加 final，表示不允许修改引用的指向。
3） 类方法确定不允许被重写。

6. 【推荐】类成员与方法访问控制从严：
1） 如果不允许外部直接通过 new 来创建对象，那么构造方法必须是 private。
2） 工具类不允许有 public 构造方法。
3） 类非 static 成员变量并且与子类共享，必须是 protected。
4） 类非 static 成员变量并且仅在本类使用，必须是 private。
5） 类 static 成员变量如果仅在本类使用，必须是 private。
6） 若是 static 成员变量，必须考虑是否为 final。
7） 类成员方法只供类内部调用，必须是 private。
8） 类成员方法只对继承类公开，那么限制为 protected。
说明：任何类、方法、参数、变量，严控访问范围。过宽泛的访问范围，不利于模块解耦。思
考：如果是一个 private 的方法，想删除就删除，可是一个 public 的 Service 方法，或者一
个 public 的成员变量，删除一下，不得手心冒点汗吗？变量像自己的小孩，尽量在自己的视
线内，变量作用域太大，如果无限制的到处跑，那么你会担心的。
#### d、控制语句
1. 【强制】在一个 switch 块内，每个 case 要么通过 break/return 等来终止，要么注释说明程
序将继续执行到哪一个 case 为止；在一个 switch 块内，都必须包含一个 default 语句并且
放在最后，即使它什么代码也没有。

2. 【强制】在 if/else/for/while/do 语句中必须使用大括号，即使只有一行代码，避免使用
下面的形式：if (condition) statements;

3. 【推荐】推荐尽量少用 else， if-else 的方式可以改写成：
if(condition){
 ...
 return obj;
}
// 接着写 else 的业务逻辑代码;
说明：如果非得使用 if()...else if()...else...方式表达逻辑，【强制】请勿超过 3 层，
超过请使用状态设计模式。
正例：逻辑上超过 3 层的 if-else 代码可以使用卫语句，或者状态模式来实现。

4. 【推荐】除常用方法（如 getXxx/isXxx）等外，不要在条件判断中执行其它复杂的语句，将复
杂逻辑判断的结果赋值给一个有意义的布尔变量名，以提高可读性。
说明：很多 if 语句内的逻辑相当复杂，阅读者需要分析条件表达式的最终结果，才能明确什么
样的条件执行什么样的语句，那么，如果阅读者分析逻辑表达式错误呢？
正例：
//伪代码如下
boolean existed = (file.open(fileName, "w") != null) && (...) || (...);
if (existed) {
 ...
}
反例：
if ((file.open(fileName, "w") != null) && (...) || (...)) {
 ...
}

5. 【推荐】循环体中的语句要考量性能，以下操作尽量移至循环体外处理，如定义对象、变量、
获取数据库连接，进行不必要的 try-catch 操作（这个 try-catch 是否可以移至循环体外）。
#### e、MySQL规约
1. 【强制】表达是与否概念的字段，必须使用 is_xxx 的方式命名，数据类型是 unsigned tinyint
（ 1 表示是，0 表示否），此规则同样适用于 odps 建表。
说明：任何字段如果为非负数，必须是 unsigned。

2. 【强制】表名、字段名必须使用小写字母或数字；禁止出现数字开头，禁止两个下划线中间只
出现数字。数据库字段名的修改代价很大，因为无法进行预发布，所以字段名称需要慎重考虑。
正例：getter_admin，task_config，level3_name
反例：GetterAdmin，taskConfig，level_3_name

3. 【强制】表名不使用复数名词。
说明：表名应该仅仅表示表里面的实体内容，不应该表示实体数量，对应于 DO 类名也是单数
形式，符合表达习惯。

4. 【强制】禁用保留字，如 desc、range、match、delayed 等，请参考 MySQL 官方保留字。

5. 【强制】唯一索引名为 uk_字段名；普通索引名则为 idx_字段名。
说明：uk_ 即 unique key；idx_ 即 index 的简称。

6. 【强制】小数类型为 decimal，禁止使用 float 和 double。
说明：float 和 double 在存储的时候，存在精度损失的问题，很可能在值的比较时，得到不
正确的结果。如果存储的数据范围超过 decimal 的范围，建议将数据拆成整数和小数分开存储。

7. 【强制】如果存储的字符串长度几乎相等，使用 char 定长字符串类型。

8. 【强制】varchar 是可变长字符串，不预先分配存储空间，长度不要超过 5000，如果存储长
度大于此值，定义字段类型为 text，独立出来一张表，用主键来对应，避免影响其它字段索
引效率。

9. 【强制】表必备三字段：id, gmt_create, gmt_modified。
说明：其中 id 必为主键，类型为 unsigned bigint、单表时自增、步长为 1。gmt_create,
gmt_modified 的类型均为 date_time 类型。

10. 【推荐】表的命名最好是加上“业务名称_表的作用”。
正例：tiger_task / tiger_reader / mpp_config

11. 【推荐】库名与应用名称尽量一致。

12. 【推荐】如果修改字段含义或对字段表示的状态追加时，需要及时更新字段注释。

13. 【推荐】字段允许适当冗余，以提高性能，但是必须考虑数据同步的情况。冗余字段应遵循：
1）不是频繁修改的字段。
2）不是 varchar 超长字段，更不能是 text 字段。
正例：商品类目名称使用频率高，字段长度短，名称基本一成不变，可在相关联的表中冗余存
储类目名称，避免关联查询。

14. 【推荐】单表行数超过 500 万行或者单表容量超过 2GB，才推荐进行分库分表。
说明：如果预计三年后的数据量根本达不到这个级别，请不要在创建表时就分库分表。

15. 【参考】合适的字符存储长度，不但节约数据库表空间、节约索引存储，更重要的是提升检
索速度。
正例：人的年龄用 unsigned tinyint（表示范围 0-255，人的寿命不会超过 255 岁）；海龟
就必须是 smallint，但如果是太阳的年龄，就必须是 int；如果是所有恒星的年龄都加起来，
那么就必须使用 bigint。

16. 【强制】业务上具有唯一特性的字段，即使是组合字段，也必须建成唯一索引。
说明：不要以为唯一索引影响了 insert 速度，这个速度损耗可以忽略，但提高查找速度是明
显的；另外，即使在应用层做了非常完善的校验和控制，只要没有唯一索引，根据墨菲定律，
必然有脏数据产生。

17. 【强制】 超过三个表禁止 join。需要 join 的字段，数据类型保持绝对一致；多表关联查询
时，保证被关联的字段需要有索引。
说明：即使双表 join 也要注意表索引、SQL 性能。

18. 【强制】在 varchar 字段上建立索引时，必须指定索引长度，没必要对全字段建立索引，根据
实际文本区分度决定索引长度。
说明：索引的长度与区分度是一对矛盾体，一般对字符串类型数据，长度为 20 的索引，区分
度会高达 90%以上，可以使用 count(distinct left(列名, 索引长度))/count(*)的区分度
来确定。

19. 【强制】页面搜索严禁左模糊或者全模糊，如果需要请走搜索引擎来解决。
说明：索引文件具有 B-Tree 的最左前缀匹配特性，如果左边的值未确定，那么无法使用此索
引。

20. 【推荐】如果有 order by 的场景，请注意利用索引的有序性。order by 最后的字段是组合
索引的一部分，并且放在索引组合顺序的最后，避免出现 file_sort 的情况，影响查询性能。
正例：where a=? and b=? order by c; 索引：a_b_c
反例：索引中有范围查找，那么索引有序性无法利用，如：WHERE a>10 ORDER BY b; 索引
a_b 无法排序。

21. 【推荐】利用覆盖索引来进行查询操作，来避免回表操作。
说明：如果一本书需要知道第 11 章是什么标题，会翻开第 11 章对应的那一页吗？目录浏览
一下就好，这个目录就是起到覆盖索引的作用。
正例：能够建立索引的种类：主键索引、唯一索引、普通索引，而覆盖索引是一种查询的一种
效果，用 explain 的结果，extra 列会出现：using index。

22. 【推荐】利用延迟关联或者子查询优化超多分页场景。
说明：MySQL 并不是跳过 offset 行，而是取 offset+N 行，然后返回放弃前 offset 行，返回
N 行，那当 offset 特别大的时候，效率就非常的低下，要么控制返回的总页数，要么对超过
特定阈值的页数进行 SQL 改写。
正例：先快速定位需要获取的 id 段，然后再关联：
 SELECT a.* FROM 表 1 a, (select id from 表 1 where 条件 LIMIT 100000,20 ) b where a.id=b.id

23. 【推荐】SQL 性能优化的目标：至少要达到 range 级别，要求是 ref 级别，如果可以是 consts
最好。
说明：
1）consts 单表中最多只有一个匹配行（主键或者唯一索引），在优化阶段即可读取到数据。
2）ref 指的是使用普通的索引（normal index）。
3）range 对索引进行范围检索。
反例：explain 表的结果，type=index，索引物理文件全扫描，速度非常慢，这个 index 级
别比较 range 还低，与全表扫描是小巫见大巫。

24. 【推荐】建组合索引的时候，区分度最高的在最左边。
正例：如果 where a=? and b=? ，a 列的几乎接近于唯一值，那么只需要单建 idx_a 索引即
可。
说明：存在非等号和等号混合判断条件时，在建索引时，请把等号条件的列前置。如：where a>?
and b=? 那么即使 a 的区分度更高，也必须把 b 放在索引的最前列。

25. 【参考】创建索引时避免有如下极端误解：
1）误认为一个查询就需要建一个索引。
2）误认为索引会消耗空间、严重拖慢更新和新增速度。
3）误认为唯一索引一律需要在应用层通过“先查后插”方式解决。

26. 【强制】不要使用 count(列名)或 count(常量)来替代 count(*)，count(*)就是 SQL92 定义
的标准统计行数的语法，跟数据库无关，跟 NULL 和非 NULL 无关。
说明：count(*)会统计值为 NULL 的行，而 count(列名)不会统计此列为 NULL 值的行。

27. 【强制】count(distinct col) 计算该列除 NULL 之外的不重复数量。注意 count(distinct
col1, col2) 如果其中一列全为 NULL，那么即使另一列有不同的值，也返回为 0。

28. 【强制】当某一列的值全是 NULL 时，count(col)的返回结果为 0，但 sum(col)的返回结果为
NULL，因此使用 sum()时需注意 NPE 问题。
正例：可以使用如下方式来避免 sum 的 NPE 问题：SELECT IF(ISNULL(SUM(g)),0,SUM(g))
FROM table;

29. 【强制】使用 ISNULL()来判断是否为 NULL 值。注意：NULL 与任何值的直接比较都为 NULL。
说明：
1） NULL<>NULL 的返回结果是 NULL，而不是 false。
2） NULL=NULL 的返回结果是 NULL，而不是 true。
3） NULL<>1 的返回结果是 NULL，而不是 true。

30. 【强制】在代码中写分页查询逻辑时，若 count 为 0 应直接返回，避免执行后面的分页语句。

31. 【强制】不得使用外键与级联，一切外键概念必须在应用层解决。
说明：（概念解释）学生表中的 student_id 是主键，那么成绩表中的 student_id 则为外键。
如果更新学生表中的 student_id，同时触发成绩表中的 student_id 更新，则为级联更新。
外键与级联更新适用于单机低并发，不适合分布式、高并发集群；级联更新是强阻塞，存在数
据库更新风暴的风险；外键影响数据库的插入速度。

32. 【强制】禁止使用存储过程，存储过程难以调试和扩展，更没有移植性。

33. 【强制】数据订正时，删除和修改记录时，要先 select，避免出现误删除，确认无误才能执
行更新语句。

34. 【推荐】in 操作能避免则避免，若实在避免不了，需要仔细评估 in 后边的集合元素数量，控
制在 1000 个之内。

35. 【参考】如果有全球化需要，所有的字符存储与表示，均以 utf-8 编码，那么字符计数方法
注意：
说明：
 SELECT LENGTH("轻松工作")； 返回为 12
 SELECT CHARACTER_LENGTH("轻松工作")； 返回为 4
 如果要使用表情，那么使用 utfmb4 来进行存储，注意它与 utf-8 编码的区别。

36. 【参考】TRUNCATE TABLE 比 DELETE 速度快，且使用的系统和事务日志资源少，但 TRUNCATE
无事务且不触发 trigger，有可能造成事故，故不建议在开发代码中使用此语句。
说明：TRUNCATE TABLE 在功能上与不带 WHERE 子句的 DELETE 语句相同。

#### f、安全规约
1. 【强制】隶属于用户个人的页面或者功能必须进行权限控制校验。
说明：防止没有做水平权限校验就可随意访问、操作别人的数据，比如查看、修改别人的订单。

2. 【强制】用户敏感数据禁止直接展示，必须对展示数据脱敏。
说明：查看个人手机号码会显示成:158****9119，隐藏中间 4 位，防止隐私泄露。

3. 【强制】用户输入的 SQL 参数严格使用参数绑定或者 METADATA 字段值限定，防止 SQL 注入，
禁止字符串拼接 SQL 访问数据库。

4. 【强制】用户请求传入的任何参数必须做有效性验证。
说明：忽略参数校验可能导致：
    page size 过大导致内存溢出
    恶意 order by 导致数据库慢查询
    任意重定向
    SQL 注入
    反序列化注入
    正则输入源串拒绝服务 ReDoS
说明：Java 代码用正则来验证客户端的输入，有些正则写法验证普通用户输入没有问题，
但是如果攻击人员使用的是特殊构造的字符串来验证，有可能导致死循环的效果。

5. 【强制】禁止向 HTML 页面输出未经安全过滤或未正确转义的用户数据。

6. 【强制】表单、AJAX 提交必须执行 CSRF 安全过滤。
说明：CSRF(Cross-site request forgery)跨站请求伪造是一类常见编程漏洞。对于存在
CSRF 漏洞的应用/网站，攻击者可以事先构造好 URL，只要受害者用户一访问，后台便在用户
不知情情况下对数据库中用户参数进行相应修改。

7. 【强制】在使用平台资源，譬如短信、邮件、电话、下单、支付，必须实现正确的防重放限制，
如数量限制、疲劳度控制、验证码校验，避免被滥刷、资损。
说明：如注册时发送验证码到手机，如果没有限制次数和频率，那么可以利用此功能骚扰到其
它用户，并造成短信平台资源浪费。

8. 【推荐】发贴、评论、发送即时消息等用户生成内容的场景必须实现防刷、文本内容违禁词过
滤等风控策略。
