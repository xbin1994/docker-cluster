### [Docker Swarm-Mode](https://docs.docker.com/engine/swarm/)
***
为了对比Kubernetes和Swarm的区别，在浏览Docker官方文档的时候，意外发现docker-engine 1.12以后版本都原生自带了基础的Swarm-Mode功能。  
![swarm-mode](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/introduction.png)  
#####  对比K8S
 - Kubernetes对1.10以后版本的兼容性不好，而且不支持docker API，需另学Kubernetes的API，学习曲线比较陡峭。
 - 而且Kubernetes的搭建与配置较Swarm更为复杂(要求etcd与flannel)。
 - 由于支付中心等服务已经用上docker-compose，而kubernetes并不支持docker-compose功能，故选用Swarm为集群搭建框架。
 
***
##### Significant features
 - 动态扩容
 - 负载均衡
 ![load_balance](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/routing-mesh.png)
 - 热升级

***
#####  Basic commands to deploy a swarm cluster
 1. 在一台manager上初始化集群: `docker swarm init --advertise-addr MANAGER-IP`
 2. 上一条命令运行完成后，会在集群中创建全球唯一的两个token用来加入worker/manager nodes时使用。
 3. 在初始机上输入 `docker swarm join-token worker/manager`，得到输出如下：
 ![token-pic](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/token.png)
 4. 在想要加入集群的主机上输入上图提示的命令与token，swarm便会自动将node加入集群。在manager上通过命令`docker node ls`可以查看集群中的所有节点。
 ![node-status](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/node-status.png)

***
##### Deployment and maintainence of the services on a swarm cluster
 - 使用命令`docker create --name <service_name> <image_name> <CMD>`指定服务名及镜像名。
 ![service_deploy](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/deploy_service.png)
 - 创建服务后即可使用命令`docker service ls` 查看集群中所有的服务。
 ![service_ls](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/service_ls.png)
 - 动态改变服务规模：使用命令`docker service scale <SERVICE-ID>=<NUMBER-OF-TASKS>`可以改变集群中服务的任务数。
 ![service_scale](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/service_scale.png)
 ![service_scale](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/scale_result.png)
 - 此外，在服务运行时也可以使用`docker service update <flags and values> <service_name>` 来对服务进行热升级。
 ![service_scale](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/update_Service.png)
 - 删除服务：`docker service rm <service_name>`
 - 查看服务详细状态: `docker service inspect <service_name>`