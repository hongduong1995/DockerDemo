1. Tạo service mongodb

B1. tạo volume dbdata
docker volume create dbdata

B2. Tạo network overlay myapp
docker network create -d overlay myapp

B3. Tạo service mongodb
docker service create \
--name mongodb \
--mount source="dbdata",destination=/data/db:rw \
--network myapp \
--constraint node.hostname==worker1node \
mongo:latest

2. Tạo service demo-service

B1. Build Image từ Dockerfile, tạo image nodejs Demo
docker build -t hongduong1995/nodejsdemo:demo1 .

B2. Tạo service demo-service
docker service create \
--name nodejsapp \
--replicas=3 \
-p 8000:3000 \
--net=myapp \
-e MONGODB_URI=mongodb:/mongodb:27017/demo \
-e PORT=3000 \
hongduong1995/nodejsdemo:demo1