# docker-compose_django_mysql_nginx

처음 docker-compose.yml 에 image 는 docker-compose에서 지원해주는 이미지를 pull받아 사용하고 그 후에 
변경사항이 있어 container 에 들어가 수정한 후에 commit을 한다면 docker-compose image에도 image를 변경해준다.

## ubuntu django setting

```
apt-get update

apt-get install -y vim git wget

apt-get install -y software-properties-common

apt-get install -y virtualenv

add-apt-repository ppa:deadsnakes/ppa
[enter]

apt-get update

apt-get install -y python3.6

apt-get install -y python3.6-dev libmysqlclient-dev build-essential

cd ~

virtualenv -p python3.6 venv

source venv/bin/activate

cd main

pip install -r requirements.txt
```

<hr/>

docker-compose yml에 depend on 옵션을 설정해 주더라도

depend on은 container 실행 순서만 영향을 미친다. 그렇기 때문에 django를 올릴때 database check 로직을 실행하여

database의 시작 여부를 먼저 파악해야만 한다.

<hr/>

기존의 만들어 놨던 docker-compose.yml 파일로 swarm 구성하는법
( docker-compose와 다른점은 docker-compose는 yml에 지정한 container_name 으로 docker process가 생기지만 docker stack은 yml의 파일의 service 이름으로 지정한것에
  stack name을 붙여 구성된다. 
  
  service_name = 'django' , stack_name = 'test_swarm' 이라면
  process 는 test_swarm_dajngo.... 으로 구성된다.
  service 는 test_swarm_django
  
  따라서 django setting파일의 database구성이나 nginx conf파일을 그에 맞게 변경하여야 한다.
 )

docker_test폴더에서 

- docker swarm init
- docker stack deploy -c docker-compose.yml (stack_name)

swarm 은 하나의 stack ( pc ) 단위로 이루어져 있으며

stack은 service 로 구성되어있다.

ex) 
나는 django, mysql, nginx 를 하나로 합친 stack이 있는것 이고
django, mysql, nginx는 하나하나 service 이다.

docker service ls (service 구성 보기)

--------------------------------------------

django가 먼저 올라가 있는 상태에서 nginx 뒤늦게 구동되면

nginx가 동작하지 않을수 있다.

django를 다시 올려주면 해결된다....(다른 해결방안을 찾아 볼 것)

