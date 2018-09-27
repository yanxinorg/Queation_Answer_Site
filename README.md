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

4.  视图解析器（ModelAndView）：根据ModelAndView中解析具体视图;

5.  将Model模型中的数据渲染到View上；

* 每个模块传出、传入参数具体如下：
<ol>
<li>Bird</li>
<li>McHale</li>
<li>Parish</li>
</ol>



### 架构模块和分层：（路径：..\src\main\java\com\nowcoder）

1.  



## 项目功能模块设计

1.  
