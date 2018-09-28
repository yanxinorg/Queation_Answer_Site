# Queation_Answer_Site


## 项目介绍
* 项目搭建了一个类似与知乎的问答网站,能够实现用户的注册登陆,问答,赞踩功能,关注取关,粉丝消息推送,敏感词过滤设计,站内信发送以及solr站内问题搜索。


## 项目构建
1.  基于Spring boot + Mybatis 整合;
2.  主数据库：MySQL;
3.  辅助数据库：Redis;
4.  搜索服务器：solr;


## 项目架构

### 基于SpringMVC架构,构建整个web响应;

1.  前端控制器（DispacherServlet）：整个响应与返回的核心，接收请求交给映射处理器HandlerMapping;

2.  映射处理器（HandlerMapping）：根据路径找到相应的处理适配器HandlerAdapter;

3.  处理器适配器（HandlerAdapter）：包括拦截器/controller等，用来处理一些功能请求，返回ModelAndView对象（包括模型数据、逻辑视图名）;

4.  视图解析器（ViewResolver）：根据ModelAndView中解析具体视图;

5.  将Model模型中的数据渲染到View上；


### 架构模块和分层：（路径：..\src\main\java\com\nowcoder）

1.  aspect包：aop模块，将各个功能模块中的登陆横切出来;

2.  async包：异步队列模块,各个小功能设计成异步的;

3.  configuradtion包：WebMVC配置，重写拦截器方法，登陆请求拦截，密码拦截;

4.  controller包：处理器适配器;

5.  dao包：数据库交互;

6.  Intercepter包：拦截器;

7.  model包：模型和视图对象;

8.  service包：业务层;

9.  util包：redis基本使用方法测试;redis点赞点踩模块实现;redis关注取关模块;站内邮件发送模块;

## 项目功能模块设计


### 登陆注册、拦截器、MD5加密模块

1.  登陆注册实现;
2.  登陆请求拦截器LoginRequiredInterceptor和密码拦截器PassportInterceptor,实现HandlerInterceptor接口;重写preHandle、postHandle、afterCompletion方法;
3.  MD5加密算法（信息-摘要算法）：MD5是基于消息摘要原理的，消息摘要的基本特征就是很难根据摘要推算出消息报文，因此要验证密码是否正确，就必须对输入密码（消息报文）重新计算其摘要，和数据库中存储的摘要进行对比（即数据库中存储的其实为用户密码的摘要），若两个摘要相同，则说明密码正确，不同，则说明密码错误。

### 用户名合法性检验和敏感词过滤设计模块
1.  用户名合法性检验模块：用户名不能为空、密码不能为空、用户名已被注册、密码强度、用户名不存在、密码错误;
2.  敏感词过滤模块：读取sensitiveWords.txt文件中的敏感词，字典树实现敏感词匹配，遇到敏感词做敏感词替换;

### Redis数据库
####  redis的几个数据类型使用
1.  List：双向列表，适用于最新列表/关注列表;
2.  Set：适用于无序集合，点赞点踩，抽奖已读;
3.  SortedSet：适用于排行榜，优先队列;
4.  hash：对象属性;
5.  String：字符串;
#### 关注和取关功能模块(问题/评论关注，粉丝关注);点赞、点踩功能模块；(整个模块采用Set集合去做，也防止了重复点赞问题)
1.  通过RedisKeyUtil类专门管理生成key，针对不同的业务需求，生成不同的key，统一管理;实体包括“LIKE”，“DISLIKE”，“EVENT_QUEUE”，“FOLLOWER”，“FOLLOWEE”，“TIMELINE”这些业务，避免了key的混乱;
2.  点赞点踩：用LIKE和DISLIKE实体，通过userId生成key值，将点赞点踩业务做成互斥状态，赞后点踩需要移除掉点赞的LIKE实体中的userId;最后调用set数据结构中的Scard()方法返回key的总数（userId总数），将集合中的点赞/点踩总数返回显示;
3.  关注取关：思路同点赞点踩;
### 被关注者消息SNS推送模块
1.  被关注者发布问题/评论，向关注者实现消息的推送;

### 异步队列模块设计


### Solr站内问题搜索模块



