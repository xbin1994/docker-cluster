### [Docker Swarm-Mode](https://docs.docker.com/engine/swarm/)
***
Ϊ�˶Ա�Kubernetes��Swarm�����������Docker�ٷ��ĵ���ʱ�����ⷢ��docker-engine 1.12�Ժ�汾��ԭ���Դ��˻�����Swarm-Mode���ܡ�  
![swarm-mode](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/introduction.png)  
#####  �Ա�K8S
 - Kubernetes��1.10�Ժ�汾�ļ����Բ��ã����Ҳ�֧��docker API������ѧKubernetes��API��ѧϰ���߱Ƚ϶��͡�
 - ����Kubernetes�Ĵ�����ý�Swarm��Ϊ����(Ҫ��etcd��flannel)��
 - ����֧�����ĵȷ����Ѿ�����docker-compose����kubernetes����֧��docker-compose���ܣ���ѡ��SwarmΪ��Ⱥ���ܡ�
 
***
##### Significant features
 - ��̬����
 - ���ؾ���
 ![load_balance](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/routing-mesh.png)
 - ������

***
#####  Basic commands to deploy a swarm cluster
 1. ��һ̨manager�ϳ�ʼ����Ⱥ: `docker swarm init --advertise-addr MANAGER-IP`
 2. ��һ������������ɺ󣬻��ڼ�Ⱥ�д���ȫ��Ψһ������token��������worker/manager nodesʱʹ�á�
 3. �ڳ�ʼ�������� `docker swarm join-token worker/manager`���õ�������£�
 ![token-pic](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/token.png)
 4. ����Ҫ���뼯Ⱥ��������������ͼ��ʾ��������token��swarm����Զ���node���뼯Ⱥ����manager��ͨ������`docker node ls`���Բ鿴��Ⱥ�е����нڵ㡣
 ![node-status](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/node-status.png)

***
##### Deployment and maintainence of the services on a swarm cluster
 - ʹ������`docker create --name <service_name> <image_name> <CMD>`ָ������������������
 ![service_deploy](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/deploy_service.png)
 - ��������󼴿�ʹ������`docker service ls` �鿴��Ⱥ�����еķ���
 ![service_ls](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/service_ls.png)
 - ��̬�ı�����ģ��ʹ������`docker service scale <SERVICE-ID>=<NUMBER-OF-TASKS>`���Ըı伯Ⱥ�з������������
 ![service_scale](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/service_scale.png)
 ![service_scale](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/scale_result.png)
 - ���⣬�ڷ�������ʱҲ����ʹ��`docker service update <flags and values> <service_name>` ���Է��������������
 ![service_scale](https://raw.githubusercontent.com/xbin1994/docker-cluster/master/images/update_Service.png)
 - ɾ������`docker service rm <service_name>`
 - �鿴������ϸ״̬: `docker service inspect <service_name>`