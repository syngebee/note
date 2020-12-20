### Activiti7

#### 工作流: 

​	工作的一个流程, 事务发展的一个业务过程

​	流程:

​	请假流程: 员工申请----部门经理----总经理----人事存档

​	传统方式? 		请假条的传递来实现

​	无纸化办公?	 线上申请----线上审批----一条请假记录

​	在计算机的帮助下, 能够实现流程的自动化控制, 就称为工作流.

#### 工作流引擎:

​	为了实现自动化控制, Activiti引擎就产生了.

​	作用: 实现流程自动化控制

#### 什么是工作流

​	工作流(Workflow), 就是通过计算机对业务流程自动化执行管理. 

​	它主要解决的是"使在**多个参与者**之间按照某种**预定义的规则自动进行传递**文档, 信息 或 任务的过程 , 从而实现某个预期的业务目标, 或者促使此目标的实现"

#### 工作流系统

​	一个软件系统中具有工作流的功能, 我们把它称为工作流系统.

​	如果一个系统**具备流程的自动化管理功能**, 这个系统可以成为工作流系统.

​	一个系统中工作流的功能是什么? 

​	就是对系统的业务流程进行自动化管理, 所以工作流是建立在业务流程的基础上, 所以一个软件的系统核心根本上还是系统的业务流程, 工作流只是协助进行业务流程管理. 机试没有工作流业务系统也可以开发运行, 只不过有了工作流可以更好的管理业务流程, 提高系统的可扩展性.

#### 工作流系统的实现手段

​	工作流系统, 如何实现流程的自动化管理?

#### **编码实现**

​	没有Activiti前, 流程自动化管理: 程序员编码来实现

​	请假: 员工申请 -- 部门经理 -- 总经理 -- 人事存档

 1. 工号, 姓名, 日期, 天数, 原因, 状态 0未提交 1提交

    员工: 

    ​	0 未提交 1提交

    部门经理:  部门号 = 部门经理的部门编号相同, 状态=1 (员工已提交)

    ​	2 同意 3不同意

    总经理: 状态=2 查询条件

    ​	4同意 5不同意

    人事存档: 状态=4

    ​	6同意 7不同意

**问题: 业务流程变更后, 程序不能使用**

如何解决, 以不变应万变?

----Activiti就可以实现业务流程变化后, 程序代码不需要改动

SaaS - 人力资源管理系统		行政审批(调薪)

为什么Activiti就可以解决业务需求变更时, 源代码不需要更新, 更新的是业务流程图? 原理?

#### 自动化实现核心机制

业务流程作为节点, 把整个节点的数据加载进表中.

 每次读取表中的第一行数据, 处理完成后删除当前行.

刷新表, 再次读取第一行数据.

业务怎么扩展都行, 代码都是读取->删除->更新.

业务的变更只是对应的表中数据行的变化.

![image-20201219220758201](C:\Users\cyc\AppData\Roaming\Typora\typora-user-images\image-20201219220758201.png)

1. 先将流程图画好
2. 将流程图中每个节点的数据读取并放入表中
3. 读取表中的第一条记录, 处理并删除

#### 自动化实现流程

1. 业务流程图要规范化, 要遵守一套标准
2. 业务流程图本质上是一个xml文件, 这样就可以存入我们所需要的数据.
3. 读取业务了流程图的过程就是解析xml的过程.
4. 读取一个业务流程图中的节点, 就相当于解析一个xml结构, 进一步将数据插入到mysql的表中, 形成一条记录.
5. 将所有的节点都读取, 存入mysql表中.
6. 后面只要读取mysql表中的记录就可以了, 读一条记录就相当于读一个节点.
7. 业务流程的推进, 转化为读取表中的数据, 并且处理数据, 结束时这一行数据就可以删除.

技术点: xml + dom4j + mysql +jdbc

#### Activiti介绍

​	Alfresco软件在2010年5月17日宣布Activiti业务流程管理(BPM)开源项目的正式启动.

​	Activiti是一个工作流引擎, Activiti可以将业务系统中复杂的业务流程抽取出来, 使用专门的建模语言(BPMN2.0)进行定义, 业务系统按照预先定义的流程进行执行, 实现了业务系统的业务流程 由activiti进行管理, 减少业务系统由于流程变更进行系统升级改造的工作量, 从而提高系统的健壮性, 同时减少了系统开发维护成本.

#### BPM

​	BPM(Business Process Management) 业务流程管理, 是一种规范化的构造端到端的卓越业务流程为中心, 以持续地提高组织业务绩效为目的的系统化方法, 常见商业管理教育如EMBA, MBA等均将BPM包含在内.

​	企业流程管理主要是对企业内部改革, 改变企业职能管理机构重叠, 中间层次太多, 流程不闭环等, 做到机构不重叠, 业务不重复, 达到缩短流程周期, 节约运作资本, 提高企业效益的作用.

​	BPM软件就是根据企业中业务环境的变化, 推进人与人之间, 人与系统之间以及系统与系统之间的整合及调整的经营方法与解决方案的IT工具. 

​	通常以Internet方式实现信息传递, 数据同步, 业务监控 和 企业业务流程的持续升级优化, 从而实现跨应用, 跨部门, 跨合作伙伴与客户的企业运作. 

​	通过BPM软件对企业内部及外部的业务流程的整个生命周期进行建模, 自动化, 管理监控和优化, 使企业成本降低, 利润得以大幅提升.

​	BPM软件在企业中应用领域广泛, 凡是有业务流程的地方都可以BPM软件进行管理, 比如企业人事办公管理, 采购流程管理, 公文审批流程, 财务管理等. 

#### BPMN

BPMN(Business Process Model And Notation) - 业务流程模型和符号, 是由BPMI开发的一套标准的业务流程

建模符号, 使用BPMN提供的符号可以创建业务流程

成本预算: 公司开发软件的规模会去决定是否使用activiti

Activiti7会生成25张表, 有成本

#### SaaS-IHRM

1. 整合Activiti
2. 实现业务流程建模, 使用BPM实现业务流程图
3. 部署业务流程到Activiti
4. 启动一个流程实例 (张三要请假,启动一个流程; 李四要请假, 启动一个流程, 流程之间互不影响)
5. 查询待办任务
6. 处理待办任务
7. 结束流程

#### 生成表结构

创建数据库

加入maven若干依赖

log4j.properties

activiti.cfg.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--dbcp简单数据源-->
    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/itcast1220activiti"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
        <property name="maxIdle" value="3"/>
        <property name="maxActive" value="1"/>
    </bean>

    <!--
		activiti单独运行的ProcessEngine配置,使用单独启动方式
		默认情况下会去读取id为processEngineConfiguration的bean
	-->
    <bean id="processEngineConfiguration" class="org.activiti.engine.impl.cfg.StandaloneProcessEngineConfiguration">
        <!-- 注入数据源 -->
        <property name="dataSource" ref="dataSource"/>
        <!-- 是否生成表结构 -->
        <property name="databaseSchemaUpdate" value="true"/>
    </bean>
</beans>
```



```java
	@Test
    public void testGenTable(){
        //创建配置对象(该方法, 可以指定bean名称第二个参数)
        ProcessEngineConfiguration configuration = ProcessEngineConfiguration
               .createProcessEngineConfigurationFromResource("activiti.cfg.xml");
        //创建实例(创建表结构)
        ProcessEngine processEngine = configuration.buildProcessEngine();
        //查看创建结果
        System.out.println(processEngine);
    }
```

**生成表结构的简便方式**

要求配置文件名称: activiti.cfg.xml

bean的id名称: processEngineConfiguration

```java
@Test
public void testGenTable(){
    ProcessEngine processEngine = ProcessEngines.getDefaultProcessEngine();
    System.out.println(processEngine);
}
```



#### 表分类

##### ACT_RE_*: _

​	表示repository. 

​	这个前缀的表包含了流程定义和流程静态资源.(图片, 规则 等等)._

##### _ACT_RU_*:

​	表示runtime. 

​	这些运行时的表, 包含流程实例, 任务, 变量, 异步任务 等运行中的数据. Activiti只在流程实例执行过程中保存这些数据, 流程结束时就会删除这些记录. 这样运行时表可以一直很小速度很快.

##### ACT_HI_*: 

​	表示history.

​	这些表包含历史数据, 比如历史流程实例, 变量, 任务等等.

##### ACT_GE_*:

​	表示general. 

​	通用数据, 用于 不同场景下.



#### 重要的表

act_re_deployment 	部署信息

act_re_procdef 			流程定义的一些信息

act_ge_bytearray		 流程定义的bpmn文件及png文件



#### 获取Service使用

processEngine.getXxxService();

![image-20201220211846284](C:\Users\cyc\AppData\Roaming\Typora\typora-user-images\image-20201220211846284.png)

#### 流程定义

画图, 属性变量弄好

#### 流程定义的部署

```java
/**
 * 流程定义的部署
 */
public class ActivitiDeployment {
    //流程定义部署
    public static void main(String[] args) {
        //创建ProcessEngine对象
        ProcessEngine processEngine = ProcessEngines.getDefaultProcessEngine();
        //得到RepositoryService实例 资源管理类
        RepositoryService repositoryService = processEngine.getRepositoryService();
        //进行部署
        Deployment deploy = repositoryService
                .createDeployment()
                .addClasspathResource("diagram/myHoliday.bpmn")
                .addClasspathResource("diagram/myHoliday.png")
                .name("请假申请单流程")
                .deploy();
        //输出部署信息
        System.out.println("id: " + deploy.getId());
        System.out.println("name: " + deploy.getName());

    }
}
```

#### 流程实例的启动

启动流程实例:

​	前提是已经完成流程定义的部署工作

```java
public class ActivitiStartInstance {
    public static void main(String[] args) {
        ProcessEngine defaultProcessEngine = ProcessEngines.getDefaultProcessEngine();
        RuntimeService runtimeService = defaultProcessEngine.getRuntimeService();
        ProcessInstance myholiday = runtimeService.startProcessInstanceByKey("myholiday");
        System.out.println(myholiday.getId());
        System.out.println(myholiday.getActivityId());
        System.out.println(myholiday.getProcessDefinitionId());
    }
}
```



#### 流程名词解释:

流程定义可以理解为我们使用bpmn画的xml文件.

流程部署即将xml解析, 放入activiti的数据表中.

流程定义好比是java的类, 流程实例好比是java的对象.

一个流程定义, 可以对应多个流程实例.



#### Spring整合Activiti

通过org.activiti.SpringProcessEngineConfiguration

创建spring与activiti的整合配置文件

activity-spring.cfg.xml (名称不固定)



