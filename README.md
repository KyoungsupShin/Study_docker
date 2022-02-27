Docker environment consideration & settings

1. 🚀 Environment
  - Intranet network: Docker download		
  ### HOST PC
  <pre><code>docker pull imagename:5.5.0</code></pre>
  <pre><code>docker save imagename > imagename.tar</code></pre>
  
  ### DEPLOYEE PC
  <pre><code>docker load < imagename.tar</code></pre>
  
2. Application
  - GPU: Nvidia-CUDA, RUNTIME
  - PYTHON: 3.6
  - Github source(ex yolov5, detectron etc)

3. Function
  - database connect
  - store semi-structured data
  - interface another container
  - customize
  - deployment

Docker Scenario
1. Virtual Box를 이용하여 CentOS7 설치, 네트워크 setting

  ### 포트포워딩 hostpc local:2222 >> centos 10.0.2.15:22
  
![image](https://user-images.githubusercontent.com/66240947/155874795-1537b86f-c3a5-4e26-8d96-275b15be26df.png)
![image](https://user-images.githubusercontent.com/66240947/155875640-decd4030-89ea-4a47-b3fc-b42633cd4af1.png)

2. Docker를 설치
  <pre><code>yum update && yum install yum-utils device-mapper-persistent-data lvm2</code></pre>
  <pre><code>yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo</code></pre>
  <pre><code>yum install -y docker-ce</code></pre>
  <pre><code>systemctl start docker</code></pre>
  <pre><code>systemctl enable docker</code></pre>
  <pre><code>docker -v</code></pre>
  <pre><code>usermod -aG docker $USER</code></pre>
  
3. 해당 OS에 배포하기 위한 Docker container를 다운로드
  - container1. yolov5로 이미지의 물체를 검출, Daemon으로 이미지를 Listening (Application)
  <pre><code>docker pull ultralytics/yolov5</code></pre>
  
  - container2. database로 container1에서의 결과를 받아 저장 (Backend)
  <pre><code>docker pull mysql:5.7</code></pre>
  
  - container3. Django webserver로 새로운 이미지를 받아 일정한 폴더로 저장 (Frondend, WAS)
  <pre><code>ddocker pull django</code></pre>
  
4. volume mount를 진행하여 신규 이미지를 저장, 이미지 분석, 결과 저장, 결과 이미지를 return
5. Port forwarding를 통해 container끼리 통신함. 
6. Dockerfile로 작성
