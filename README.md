# docker-compose_django_mysql_nginx

--- ubuntu django setting ---

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
