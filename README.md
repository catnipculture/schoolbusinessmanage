> #### 作者主页：[舒克日记](https://blog.csdn.net/cativen)
>
>  简介：Java领域优质创作者、Java项目、学习资料、技术互助
>
> <b><font color=red>文中获取源码</font></b>

# 项目介绍

人事管理系统分为管理员和用户两部分操作角色

主要的功能有资产报废管理、用户管理、入库管理、资产借用管理、校园资产管理、个人信息管理

# 环境要求

1.运行环境：最好是java jdk1.8,我们在这个平台上运行的。其他版本理论上也可以。

2.IDE环境：IDEA,Eclipse,Myeclipse都可以。推荐IDEA;

3.tomcat环境：Tomcat7.x,8.X,9.x版本均可

4.硬件环境：windows7/8/10 4G内存以上；或者Mac OS;

5.是否Maven项目：是；查看源码目录中是否包含pom.xml;若包含，则为maven项目，否则为非maven.项目

6.数据库：MySql5.7/8.0等版本均可；

# 技术栈

运行环境：jdk8 + tomcat9 + mysql5.7 + windows10

服务端技术：Spring Boot+ Mybatis +VUE

# 使用说明

1.使用Navicati或者其它工具，在mysql中创建对应sq文件名称的数据库，并导入项目的sql文件；

2.使用IDEA/Eclipse/MyEclipse导入项目，修改配置，运行项目；

3.将项目中config-propertiesi配置文件中的数据库配置改为自己的配置，然后运行；

# 运行指导

idea导入源码空间站顶目教程说明(Vindows版)-ssm篇：

http://mtw.so/5MHvZq

源码地址：[http://www.codegym.top](http://www.codegym.top/)


# 运行截图

## 文档截图

![img](https://img-blog.csdnimg.cn/img_convert/f9ea18d5a7dea0951fe9a9c7109968e6.png)

### 项目截图

![springboot248校园资产管理0](https://img-blog.csdnimg.cn/img_convert/e8f04267624c255c41e03387ea85f8fc.png)

![springboot248校园资产管理1](https://img-blog.csdnimg.cn/img_convert/61bed65a693e60ab6752270715b07ef1.png)

![springboot248校园资产管理2](https://img-blog.csdnimg.cn/img_convert/3596eb8fbfd5b7046d3091e97c5301aa.png)

![springboot248校园资产管理3](https://img-blog.csdnimg.cn/img_convert/6392ca08af02ed4dc1b504d6fecbc25d.png)

![springboot248校园资产管理4](https://img-blog.csdnimg.cn/img_convert/2d8ff13e283ba9c2180e574a77aec451.png)

![springboot248校园资产管理5](https://img-blog.csdnimg.cn/img_convert/3f2315ff45e44e87a6da1dcc6c0449a5.png)

![springboot248校园资产管理6](https://img-blog.csdnimg.cn/img_convert/dc8f6586a3579f515e3e48960f1703d4.png)

![springboot248校园资产管理7](https://img-blog.csdnimg.cn/img_convert/ad5a6a5d5033498310ee954a92280c19.png)

![springboot248校园资产管理8](https://img-blog.csdnimg.cn/img_convert/767b343172fc8c6883010e9c6955cac1.png)

### 代码

```
    private Map<String, List<UserRoleDTO>> getRoleMap(List<String> ids) {
        List<UserRoleDTO> roleDOS = new ArrayList<>();
        Map<String, List<UserRoleDTO>> map = new HashMap<>();
        if (RequestUtils.isAdministrator()) {
            roleDOS=userRoleAccessMapper.selectRoleListByUserIds(ids,null);
        }else {
            roleDOS = userRoleAccessMapper.selectRoleListByUserIds(ids,RequestUtils.getCurrentTenantId());
        }
        if (!CollectionUtils.isEmpty(roleDOS)) {
            for(UserRoleDTO roleDO:roleDOS){
                List<UserRoleDTO> oldList = map.get(roleDO.getUserId());
                if (CollectionUtils.isEmpty(oldList)) {
                    List<UserRoleDTO> newList = new ArrayList<>();
                    newList.add(roleDO);
                    map.put(roleDO.getUserId(),newList);
                }else{
                    oldList.add(roleDO);
                    map.put(roleDO.getUserId(),oldList);
                }
            }
        }
        return map;
    }
```
