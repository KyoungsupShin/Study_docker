Docker environment consideration & settings

# 🚀 Environment
  - Intranet network: Docker download		
  #### HOST PC
  <pre><code>docker pull imagename:5.5.0</code></pre>
  <pre><code>docker save imagename > imagename.tar</code></pre>
  
  #### DEPLOYEE PC
  <pre><code>docker load < imagename.tar</code></pre>
  
# 🎮 Application
  - GPU: Nvidia-CUDA, RUNTIME
  - PYTHON: 3.6
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
  <pre><code>yum update && yum install yum-utils device-mapper-persistent-data lvm2</code></pre>
  <pre><code>yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo</code></pre>
  <pre><code>yum install -y docker-ce</code></pre>
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
  
### 📌 volume mount to save new images, analyze for object detection, save result data etc
  <pre><code>docker create -d -v.. -p.. --name.. </code></pre>

### 📌 start container to run.
  <pre><code>docker run ... </code></pre>

### 📌 Modification python code(yolov5)
  ##### to wait and listen to new image (image, code)
  
### 📌 Port forwarding를 통해 container끼리 통신함. 
![image](https://user-images.githubusercontent.com/66240947/155876646-af205618-a7fd-4734-a16e-cc5b094a5518.png)

### 📌 Dockerfile로 작성
