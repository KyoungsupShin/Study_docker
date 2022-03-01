# 도커 컨테이너를 이용하여 프론트앤드 - 백앤드 - 딥러닝 분석을 위한 3가지 솔루션을 실행, 통신, 저장 기능 구현 

# 🚀 Environment
  #### HOST PC - Virtual Box - Hyperviser - CentOS7
    
# 🎮 Application
  - GPU: Nvidia-CUDA, RUNTIME
  - PYTHON: 3.6
  - MySQL: 5.6
  - Github source(ex yolov5, detectron etc)

# 📚 Scenario & Function
  - database setup, connect, store
  - store semi-structured data in disk
  - interface with other containers
  - customize python code
  - deployment setting, docker-compose

# 🔥 Docker Steps
### 📌 Using virtual Box, CentOS7 installation, network setting(SSH)

  #### PORT-forwarding hostpc local:2222 >> centos 10.0.2.15:22
  
![image](https://user-images.githubusercontent.com/66240947/155874795-1537b86f-c3a5-4e26-8d96-275b15be26df.png)
 
 #### Turn-off firewall
 <pre><code>systemctl stop firewalld</code></pre>
 <pre><code>systemctl disable firewalld</code></pre>
  
![image](https://user-images.githubusercontent.com/66240947/155875640-decd4030-89ea-4a47-b3fc-b42633cd4af1.png)

### 📌 Docker installation
  <pre><code>yum -y update</code></pre>
  <pre><code>yum install -y yum-utils</code></pre>
  
  <pre><code>yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo</code></pre>
  <pre><code>yum install -y docker-ce docker-ce-cli containerd.io</code></pre>
  
  <pre><code>systemctl start docker</code></pre>
  <pre><code>systemctl enable docker</code></pre>
  <pre><code>docker -v</code></pre>
  
  <pre><code>usermod -aG docker $USER</code></pre>
  
### 📌 Docker base image download
  - container1. yolov5(image object detection)
  <pre><code>docker pull ultralytics/yolov5</code></pre>
  
  - container2. MySQL database
  <pre><code>docker pull mysql:5.7.37</code></pre>
  
  - container3. Django webserver
  <pre><code>docker pull django</code></pre>
  
  - docker image pulled check-out
  <pre><code>docker images</code></pre>

### 📌 Docker base image download(off-line)
  #### HOST PC
  <pre><code>docker pull imagename:5.5.0</code></pre>
  <pre><code>docker save imagename > imagename.tar</code></pre>
  
  #### DEPLOYEE PC
  <pre><code>docker load < imagename.tar</code></pre>

### 📌 Docker volume create
  <pre><code>docker volume create mysql-volume </code></pre>
  <pre><code>docker volume create django-volume </code></pre>
  <pre><code>docker volume create yolov5-volume </code></pre>
  
  ##### We can check out volume config file list by below..
  <pre><code>docker volume ls </code></pre>
  
  <pre><code>docker volume inspect yolov5-volume </code></pre>
  <pre><code>
  [
    {
        "CreatedAt": "2022-03-01T01:42:05-05:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/mysql-volume/_data", #This is the path to be mounted
        "Name": "mysql-volume",
        "Options": {},
        "Scope": "local"
    }
]
</code></pre>

### 📌 volume mount to save new images, analyze for object detection, save result data etc
  <pre><code>docker run -d -v mysql-volume:/var/lib/mysql -p 33060:3306 -e MYSQL_ROOT_PASSWORD=root --name mysql mysql </code></pre>

### 📌 start container to run.
  <pre><code>docker run ... </code></pre>

### 📌 Modification python code(yolov5)
  ##### to wait and listen to new image (image, code)
  
### 📌 Port forwarding를 통해 container끼리 통신함. 
![image](https://user-images.githubusercontent.com/66240947/155876646-af205618-a7fd-4734-a16e-cc5b094a5518.png)

### 📌 Dockerfile로 작성
