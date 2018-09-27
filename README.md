# Queation_Answer_Site

[TOC]




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


### 用户名合法性检验和敏感词过滤设计模块


### 粉丝关注和取关功能模块


### 点赞、点踩功能模块


### 被关注者消息SNS推送模块


### Solr站内问题搜索模块



