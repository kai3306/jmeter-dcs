# jmeter-dcs

#### 介绍
利用docekr容器实现Jmeter分布式压测，支持Grafana实时查看测试数据，在线查看测试报告。

#### 软件架构
C/S


#### 使用说明

```
#进入项目目录
cd jmeter-dcs

#构建镜像并运行容器（启动两个子节点slave=2）
docker-compose up -build --scale slave=2 -d

#进入master容器
docker exec -it jmeter-master bash

#切换到script文件夹下
cd script

#运行jmeter脚本（-R指定参与节点）
jmeter -n -t test.jmx  -l ../report/test01/data.csv -e -o ../report/test01 -R jmeter-dcs-slave-1,jmeter-dcs-slave-2

```

在线报告在脚本运行结束后通过[http://宿主机IP:3500]，记得关闭防火墙和开放端口。
Grafana实时运行结果通过[http://宿主机IP:3600]，记得关闭防火墙和开放端口。
账号密码：admin

