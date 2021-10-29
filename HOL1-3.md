
# Hands-on Lab 1 ~ 3 #
# Lab 1 - IoT Hub에 Edge 디바이스 생성
IoT Hub에 Edge 디바이스 등록을 진행합니다

![image](https://user-images.githubusercontent.com/14192817/139300912-fdc68578-88dd-4d71-8c99-3f39c246aa8d.png)

디바이스 생성시 Device ID를 입력하고 나머지는 default값으로 생성 진행 합니다.

![image](https://user-images.githubusercontent.com/14192817/139301040-b22407dc-00f3-40b7-bf9e-47f1868cec21.png)

등록 완료된 Edge 디바이스를 클릭합니다.

![image](https://user-images.githubusercontent.com/14192817/139301177-8d63b338-281f-44dc-ac64-0c5dc9da02e2.png)

이후 실습에서 사용될 Primary Connection String을 복사하여 메모장 등에 저장 합니다.

![image](https://user-images.githubusercontent.com/14192817/139301221-4db9bc4a-2d50-42c1-911a-aec7a97760ec.png)


# Lab 2 - Ubuntu Linux VM 생성
IoT Edge 디바이스용으로 Ubuntu VM을 생성 합니다.

Azure Portal에서 Create 아이콘 클릭

![image](https://user-images.githubusercontent.com/14192817/139298970-6744e729-eec7-4371-8ace-f4a818f58804.png)

Virtual machine의 생성 버튼 클릭

![image](https://user-images.githubusercontent.com/14192817/139299181-cf0e0ef3-9d72-47eb-8321-a18ce8f10697.png)

아래 화면과 같이 Resource Group 선택, Virtual Machine name 입력 및 Username & Password를 입력하여 생성 합니다.
보안을 고려하여 SSH public key를 선택하여 진행할 수 있습니다.

[>> Azure Portal에서 Linux 가상 머신 만들기 참조 LINK](https://docs.microsoft.com/ko-kr/azure/virtual-machines/linux/quick-create-portal#create-virtual-machine)

![image](https://user-images.githubusercontent.com/14192817/139299248-b9c80f8b-3a16-43f3-ad39-5c6ef1334d64.png)

Cloud Shell을 통하여 생성된 Linux VM에 접속합니다.
https://shell.azure.com/ 접속 혹은 Azure Portal에서 아이콘 클릭하여 접속합니다.
![image](https://user-images.githubusercontent.com/14192817/139300185-432cc299-d89c-42db-8dd7-3f4a3be54efb.png)

VM 생성시 입력하였던 ID & Password를 활용하여 Linux VM에 접속합니다.
![image](https://user-images.githubusercontent.com/14192817/139300489-61f97004-e2f0-4aef-a588-8a969ae06cd4.png)


# Lab 3 - Ubuntu Linux VM에 IoT Edge Runtime 설치
[>> IoT Edge Runtime 설치 참조 LINK](https://docs.microsoft.com/ko-kr/azure/iot-edge/how-to-provision-single-device-linux-symmetric?view=iotedge-2020-11&tabs=azure-portal)

Ubuntu Linux 버전과 일치하는 리포지토리 구성을 설치합니다.
  ```bash
curl https://packages.microsoft.com/config/ubuntu/18.04/multiarch/prod.list > ./microsoft-prod.list
 ```

생성된 목록을 sources.list.d 디렉터리에 복사합니다.
```bash
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
 ```

Microsoft GPG public key를 설치합니다.
 ```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
 ```

**컨테이너 엔진 설치**
패키지 목록 업데이트
 ```bash
    sudo apt-get update
 ```
 
 컨테이너 Moby 엔진 설치
Install the Moby engine.
   ```bash
   sudo apt-get install moby-engine
  ```


**IoT Runtime 설치**

 ```bash
   sudo apt-get update
   apt list -a aziot-edge aziot-identity-service
   sudo apt-get install aziot-edge
 ```

**Edge 디바이스 Provision**
 ```bash
sudo iotedge config mp --connection-string '실습1에서 저장하였던 Connection String 입력'
sudo nano /etc/aziot/config.toml
  ```
 Connection String 적용을 확인 합니다.

설정 파일의 변경 사항을 적용합니다.
 ```bash
 sudo iotedge config apply
 ```

**Edge 설치 확인**

서비스 실행 확인
```bash
sudo iotedge system status
sudo iotedge list
 ```

Edge 데몬 재시작 명령어
 ```bash
sudo systemctl restart iotedge
 ```

[Hands-on Lab 4 ~ 5 바로가기](https://github.com/min-git/IoTEdgeHOL/blob/main/HOL4-5.md)

[README 바로가기](https://github.com/min-git/IoTEdgeHOL/blob/main/README.md)
