# auto
基于ansible的Java代码自动化部署

## 依赖

- [ansible](www.ansible.com)
- [nginx健康检测插件](https://github.com/yaoweibin/nginx_upstream_check_module)

## 拓扑
![](images/topo.png)

## 思路
1. 在Deploy拉取最新代码，打包                                             ---build
2. 切断nginx流量                                                          ---limit
3. 步骤2完成后，等待一段时间（有可能该tomcat还在执行任务），停Tomcat1     ---shutdown
4. 拷贝代码、配置文件到Tomcat1                                            ---push
5. 起Tomcat1                                                              ---startup
6. 验证Tomcat1                                                            ---test
7. 重复步骤3-6，分发到Tomcat2和Tomcat3                                    ---one more time

