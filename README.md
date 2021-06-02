# Docker操作方法説明

## Dockerfileの内容

ベースイメージは、tomcat:10.0.6-jdk11-openjdk-slim


## tomcat sample.warの取得
```
./get_war.sh
```

## BuildしてDockerImageを作成する
```
# Dockerfileのあるディレクトリにておこなう
# myrepo/　の部分は、ecrの名前に合わせる
docker build . -t myrepo/tomcat:latest
```

## Build後のイメージの参照
```
docker image ls
```
## イメージの削除（安易に実施しないこと）
```
docker image rm <IMAGE_ID>
```

## Docker Containerの実行
```
docker container run -p 8080:8080 myrepo/tomcat:latest
```

## Container の実行確認
```
docker container ps
```

## Container のシェルに入る
```
docker exec -it <CONTAINER_ID> /bin/bash
# 抜けるときには、exit
```

## sampleの確認（Curlコマンドにて）
```
curl -i -L localhost:8080/sample
```

## Containerの停止
```
docker container stop <CONTAINER_ID>
```

--- Dockerfile
```
FROM tomcat:10.0.6-jdk11-openjdk-slim
WORKDIR /usr/local/tomcat/webapps/
COPY sample.war /usr/local/tomcat/webapps/sample.war

# [NOTE] In the case of downloading from tomcat site via wget.
# RUN apt-get update && apt-get install -y wget
# RUN wget http://tomcat.apache.org/tomcat-8.5-doc/appdev/sample/sample.war

#EXPOSE 8080
```
--- get_war.sh
```
#!/bin/bash

wget http://tomcat.apache.org/tomcat-8.5-doc/appdev/sample/sample.war
```
