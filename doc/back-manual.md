# 1,JAVA开发规范

## 1.1 包命名规范
* Bean配置包名：com.geely.${project}.${module}.configuration
* Scheduler配置包名：com.geely.${project}.${module}.configuration.scheduler
* Controller包名：com.geely.${project}.${module}.controller
* Service接口包名：com.geely.${project}.${module}.service
* Service实现包名：com.geely.${project}.${module}.service.impl
* Mapper接口包名：com.geely.${project}.${module}.dao
* Model包名：com.geely.${project}.${module}.model </br>
注：${project}和${module}应与maven的groupId和artifactId相关，如一级不够表述，可多级。

## 1.2 类命名规范
* Bean配置类名：***Configuration
* Scheduler配置类名：***Scheduler
* Controller类名：***Controller
* Service接口类名：***Service
* ervice实现类名：***ServiceImpl
* Dao接口类名：***Dao
* Model类名：按照实际业务对象命名，要求准确无歧义

## 1.3 接口URI命名规范
* 原则上应使用“/”作为Web容器的Context-Path（默认值）
* REST资源地址：/${project}/${module}/***/${noun}
* URI只能包含小写字母、数字和“-”（dash）
* 准确使用HTTP请求动词：
* * GET : 适用于数据查询
* * POST : 适用于创建资源
* * PUT : 用于创建或更新某一个资源
* * ELETE：删除资源

## 1.4 RestController开发规范
* 统一使用APIResponse<T>泛型作为响应
* 不要将请求输入参数定义成POJO，必须一个个清晰地列出它们，这些参数的数据类型只应该是：原子类型、原子类型的包装类型、String型、Date型
* 资源的HTTP请求动词必须指定，原则上一个资源只有一个请求动词对应
* 使用Swagger注解描述接口、参数及返回值
* 使用JSR-349注解实现请求参数验证

</br>

# 2,数据库开发规范

## 2.1 Schema
* 英文字母加中划线"-"组成，命名简洁明确，</br>
  **例：app-cloud-dev**；
* 除了做备份使用，请不要在名称上加***数字***；
* 禁止使用大写字母；
* 禁止使用数据库关键字；


## 2.2 表
* 英文字母加下划线"_"组成，命名简洁明确，</br>
  **例：cloud_info**；
* 除了做备份使用，请不要在名称上加***数字***；
* 禁止使用大写字母；
* 禁止使用数据库关键字；
* 表名不应取太长，建议最长20个字符；
* 使用单数形式表示，不建议使用复数；
* 必须要有物理主键，</br>
  (mysql建议使用自增，oracle建议使用sequence)；
* 适当使用唯一性约束(unique)
* 非关联关系表，请加上字段createTime和updateTime，如果可以，请加上字段createUser；
* 使用统一的前缀表示一组相关的表，</br>
  **例：表示服务相关的一组表**</br>
  **service_info**</br>
  **service_extend**</br>
  **service_group**；
* 不建议建立外键，请在程序中保证外键约束；

## 2.3 字段
* 使用驼峰形式命名字段，首字母小写，</br>
  **例：cloudId**;
* 建议不要使用数字；
* 禁止使用数据库关键字；
* 含义要清晰，尽量不要使用缩写；
* 尽量不要重复表名，</br>
  **例：表名为cloud_info，字段中不需要再含有cloud_info**；
 
## 2.4 索引
* 普通索引，使用idx_表名_字段来命名(名字太长可以使用缩写)，</br>
  **例：idx_cloud_info_cloudId**；
* 唯一性索引，使用uni_表名_字段来命名(名字太长可以使用缩写)，</br>
  **例：uni_cloud_info_cloudId**；

## 2.5 字段属性
* 主键建议使用int类型，mysql建议使用auto_increment，oracle建议使用sequence；
* 建议都将字段设置成not null；
* 字符类型的字段，如果确定字段长度，请使用char代替varchar；
* 数字类型的字段，能使用tinyint，就使用tinyint代替int；
* 减少或者不使用text，longtest，blob等大存储量的属性，如果一定要使用，建议单独使用一张表来存储；

</br>

# 3 分支模型
![image](../evun-git-flow.png)

**Feature分支：**
属于用户故事，当我们需要开发一个新功能时，需要建立该分支，该分支主要用于开发环境，进行开发测试以及测试阶段的bug修复。
* feature分支命名规范：feature_用户故事ID_20170922（这个ID为jira的用户故事ID）

**Test分支：**
为了区分feature，feature-release，以及release分支，不在分支命名上产生歧义以及不让开发人员误解，我们将feature-release分支重新定义成test分支，用于feature分支的提测使用。当一个用户故事需要提测时，我们需要建立和用户故事相对应的test分支，test分支原则上不能进行代码修改，一旦测试出现bug，我们需要在对应的feature分支上完成bug修改，并合并会test分支，让测试回归。
* test分支命名规范：test_用户故事ID_20170922（按照对应的feature分支命名）

**Release分支：**
当存在多个feature分支需要发布时，我们需要建立一个release分支，用于多个feature的测试和发布使用。
* test分支命名规范：release_发布简述_日期

**Develop分支：**
我们保证该分支上的代码和线上的代码一致，所有的feature和release分支，都应该是从develop中出来的。记录最新的snapshot版本。

**Master分支：**
生产环境分支，主要记录下一个需要发布的release版本，禁止在该分支上进行任何开发操作。


