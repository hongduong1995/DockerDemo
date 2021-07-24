### Các bước build ứng dụng với Dockerfile

Chia làm 2 stage:

1. Stage 1

- Sử dụng base image ***maven:ibmjava-alpine***

- Copy source code vào image

- Từ source code build ra file ***websocket-demo-0.0.1-SNAPSHOT.jar*** bằng lệnh: `mvn clean package`.

- File ***websocket-demo-0.0.1-SNAPSHOT.jar*** sẽ nằm trong thư mục **target** của source code

2. Stage 2

- Sử dụng base image ***openjdk:8-alpine***

- Copy file ***websocket-demo-0.0.1-SNAPSHOT.jar*** từ stage 1 sang stage 2

- Dùng lệnh sau để start container: `java -Djava.security.egd=file:/dev/./urandom -jar websocket-demo-0.0.1-SNAPSHOT.jar`

Giải bài tập
Cách 1:
 B1: clone tài liệu từ đường link đã cho về máy bằng lệnh: git clone <git link http>
 B2: cd vào trong thư mục chứa source code
 B3: Tạo 1 file :"Dockerfile"
 B4: Viết các câu lệnh build Image.
 B5: Chạy lệnh: docker image build -f Dockerfile -t hongduong1995/spring-app:dev .
 B6: Chạy lệnh: docker container run -d --name springapp -port 9002:8080 hongduong1995/spring-app:dev
 B7: Kiểm tra container có chạy hay không: docker ps

Cách 2:
 B1: clone tài liệu từ đường link đã cho về máy bằng lệnh: git clone <git link http>
 B2: cd vào trong thư mục chứa source code
 B3: Chạy lệnh gán quyền cho file mvnw bằng lệnh: chmod u+x mvnw
 B4: Chạy lệnh sau để build dự án thành file jar bằng lệnh: ./mvnw clean package
 B5: Sau khi build Snapshot xong. Tạo một file :"Dockerfile2"
 B6: Viết các câu lệnh build image
 B7: Chạy lệnh: docker image build -f Dockerfile2 -t hongduong1995/spring-app2:dev .
 B8: Chạy lệnh: docker container run -d --name springapp2 -port 9003:8080 hongduong1995/spring-app2:dev
 B9: Kiểm tra container có chạy hay không: docker ps