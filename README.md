# crowd

## Requirement
- docker-compose: 17.09.0+

## How to run with docker-compose

- start crowd & mysql

```
git clone https://github.com/mrleloi/crowd-docker.git \
    && cd crowd-docker \
    && docker-compose up
```

- start crowd & mysql daemon

```
docker-compose up -d
```

- default db(mysql8.0) configure:

```bash
driver=mysql
host=mysql-crowd
port=3306
db=crowd
user=root
passwd=123456
```

## How to run with docker

- start crowd

```
docker volume create crowd_home_data && docker network create crowd-network && docker run -p 8090:8090 -v crowd_home_data:/var/crowd --network crowd-network --name crowd-srv -e TZ='Asia/Shanghai' haxqer/crowd:8.7.1
```

- config your own db:


## How to hack crowd

```
docker exec crowd-server java -jar /atlassian-agent.jar \
    -d \
    -p crowd \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

## How to hack crowd plugin

- .eg I want to use BigGantt plugin
1. Install BigGantt from crowd marketplace.
2. Find `App Key` of BigGantt is : `eu.softwareplant.biggantt`
3. Execute :

```
docker exec crowd-server java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p eu.softwareplant.biggantt \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

4. Paste your license


## How to upgrade

```shell
cd crowd && git pull
docker pull haxqer/crowd:latest && docker-compose stop
docker-compose rm
```

enter `y`, then start server

```shell
docker-compose up -d
```

