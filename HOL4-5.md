# Hands-on Lab 4 ~ 5 
# Lab 4 - Container Registry 생성
Azure Portal에서 리소스 생성을 진행합니다.

![image](https://user-images.githubusercontent.com/14192817/139304897-7b9da569-2b93-447e-b1a1-376994bc1693.png)

Container Registry를 선택하여 생성 진행 합니다.

![image](https://user-images.githubusercontent.com/14192817/139304856-8a50c553-2e40-4f3e-8215-6ccf58fcd9ef.png)

생성 화면에서 아래와 같이 입력 후 Review+Create을 실행합니다.

Registry name은 중복을 허용하지 않으므로 이름 이니셜등을 통해 중복되지 않는 이름으로 입력합니다.

![image](https://user-images.githubusercontent.com/14192817/139305000-612e5cda-0d09-4900-aaaf-eaca5ca37bea.png)

문제없이 아래 화면이 나오면 Create를 실행하여 생성 진행합니다.

![image](https://user-images.githubusercontent.com/14192817/139305178-953c16b3-c63c-4b7a-9e87-431ee8c4c1a4.png)

생성된 Container Registry에서 설정 > 액세스 키 메뉴로 이동합니다.

Admin user 버튼을 Enabled로 활성화 합니다.

Registry name, Login Server, username, password를 복사하여 이후 진행을 위해 메모장 등에 저장합니다.
![image](https://user-images.githubusercontent.com/14192817/139305379-79f01811-b73a-40cb-829c-a6ff35ec6874.png)


# Lab 5 - Visual Studio Code를 활용하여 Edge 모듈 빌드 및 배포
[>> Visual Studio Code 활용 모듈 빌드 및 배포 참조 LINK](https://docs.microsoft.com/ko-kr/azure/iot-edge/tutorial-develop-for-linux?view=iotedge-2020-11#set-up-vs-code-and-tools)

*** IoT Edge Runtime 버전 설정***
View > Command Palette 메뉴를 실행하여 "Azure IoT Edge: New IoT Edge Solution" 선택
![image](https://user-images.githubusercontent.com/14192817/139306052-352ed5c0-8682-4662-9da0-a930ad4584a4.png)

폴더 선택 화면이 나오면 모듈 코드 저장 위치를 생성하여 선택
![image](https://user-images.githubusercontent.com/14192817/139306503-67f4759b-097d-4777-b35d-fe0d882031cd.png)

솔루션 이름 입력 - EdgeSolution으로 진행

![image](https://user-images.githubusercontent.com/14192817/139306534-bf4ac014-2145-4603-983e-bf2f17e01a60.png)

모듈 템플릿 선택 - C# 모듈

![image](https://user-images.githubusercontent.com/14192817/139306637-faae9446-ae65-47d7-825f-3b1955f8b76f.png)

모듈 이름 입력 - SampleModule

![image](https://user-images.githubusercontent.com/14192817/139306695-b0a82987-166f-4c1e-9378-007e8dc76b54.png)

도커 이미지 레지스트리 주소 입력 - localhost:5000 부분을 실습4에서 저장해둔 Login Server 주소로 변경
![image](https://user-images.githubusercontent.com/14192817/139306795-00f3d782-ebb3-4f4a-b4c0-fa59d2553ac9.png)

Azure IoT Edge: Set Default IoT Edge Rumtime Version 선택
![image](https://user-images.githubusercontent.com/14192817/139306966-aa018d63-6b0e-4b55-858c-cf9b25372ffb.png)

Edge runtime 버전 선택 - 1.2
![image](https://user-images.githubusercontent.com/14192817/139307237-d6d1f7f2-8eb9-4cf2-936b-febf79a26b9d.png)

진행 완료 후 .env 파일을 열어 Container Registry Username과 Password가 업데이트 되었는지 확인 합니다.
![image](https://user-images.githubusercontent.com/14192817/139307323-3777d53e-287b-47ea-920c-55609767a1d0.png)

***모듈 배포 대상 아키텍처 선택***
View > Command Palette 메뉴를 실행하여 "Azure IoT Edge: set Default Target Platfrom Edge Solution" 선택
![image](https://user-images.githubusercontent.com/14192817/139307597-8db0df62-4ce7-4439-ab7a-ae0abf8e1d1a.png)

amd64 선택

![image](https://user-images.githubusercontent.com/14192817/139307683-b6390720-4057-4013-a485-1e6afac02c49.png)

***Container Registry 로그인***

터미널을 실행 합니다.

![image](https://user-images.githubusercontent.com/14192817/139307740-96cff238-6107-46b6-a620-51ef809075b3.png)


실습4에서 저장해 두었던 Azure Container Registry 정보를 사용하여 Docker에 로그인 합니다.
```bash
docker login -u <ACR username> -p <ACR password> <ACR login server>
```
![image](https://user-images.githubusercontent.com/14192817/139308088-68034a7a-688c-4dbe-93f8-0b631e76ed9b.png)

Azure Container Registry에 로그인 합니다.
```bash
docker login -u <ACR username> -p <ACR password> <ACR login server>
```
![image](https://user-images.githubusercontent.com/14192817/139308747-5638680d-98e6-4356-9ea1-3564ffe03030.png)

로그인에 문제 발생시 az login을 수행 합니다.

![image](https://user-images.githubusercontent.com/14192817/139308583-d7a831c2-077c-4cd2-930e-8303a5c4a641.png)


***모듈 빌드 및 푸쉬 로그인***

deployment.template.json을 마우스 우클릭하여 "Build and Push IoT Edge Solution"을 실행합니다.

![image](https://user-images.githubusercontent.com/14192817/139308957-927b4a66-47d7-4e9a-a730-6fa6755d9474.png)

config 폴더 아래 생성된 deployment.amd64.json 파일을 열어 배포할 SampleModule의 버전 등을 확인 합니다.

![image](https://user-images.githubusercontent.com/14192817/139309055-8f8c18bd-b850-4144-9a6f-b2ea6da5c93d.png)

module.json 파일을 열어 모듈 변경 테스트를 위해 소스코드 변경을 가정하여 모듈 패치 버전을 0.0.2로 업데이트 합니다.

모듈을 빌드 및 푸쉬하기 전에 버전을 증가 시키지 않으면 기존 Container Registry의 Repository의 내용이 배포 됩니다.

![image](https://user-images.githubusercontent.com/14192817/139310100-a9dbf2ee-50e5-4db5-b949-fc178d477a1a.png)

deployment.template.json을 마우스 우클릭하여 "Build and Push IoT Edge Solution"을 실행합니다.

![image](https://user-images.githubusercontent.com/14192817/139310184-a244fdb5-c8e5-4d77-a924-662530a005dd.png)

config 폴더 아래 생성된 deployment.amd64.json 파일을 열어 배포할 SampleModule의 버전이 0.0.2로 증가한 것을 확인합니다.

![image](https://user-images.githubusercontent.com/14192817/139310226-d910d529-68d1-447f-90a5-222dbdfbd9dc.png)

Azure Portal의 Container Registry의 Repository 메뉴에서 0.0.2 버전이 업데이트 되었는지 확인합니다.
![image](https://user-images.githubusercontent.com/14192817/139310300-fedea816-81fb-49ba-b080-e96b841e1da4.png)


***Edge 디바이스에 모듈 배포***

배포 대상 Edge 디바이스를 우클릭하여 “Create Deployment for Single Device” 선택합니다.

![image](https://user-images.githubusercontent.com/14192817/139310537-60745e57-08c3-4b85-a553-ca06f9cf278f.png)

배포 Json 파일 선택 화면에서 config 폴더 아래의 deployment.amd64.json 파일을 선택합니다.

![image](https://user-images.githubusercontent.com/14192817/139310577-f6bbe9c9-ba5b-4909-b05f-8172273a8cf7.png)

Edge 디바이스에 모듈 배포 상황을 VS Code에서 확인할 수 있습니다. (배포시 정상 실행까지 지연 시간이 있습니다.)

![image](https://user-images.githubusercontent.com/14192817/139310820-952fefc2-dc50-4468-8464-ffd65185d3e9.png)

Edge VM에 접속하여 명령어를 통해 배포된 모듈을 확인할 수 있습니다.
```bash
sudo iotedge list
```
![image](https://user-images.githubusercontent.com/14192817/139310949-a80761ad-67e8-46d1-830c-d9ce4ce85a45.png)


***디바이스 메시지 확인***

Edge 디바이스를 마우스 우클릭하여 "Start Monitoring Built-in Event Endpoint" 실행합니다.

![image](https://user-images.githubusercontent.com/14192817/139311278-019a4633-d26d-47be-9d12-c9cae5be0059.png)

터미널 출력 창에서 Edge 디바이스에서 전송하는 텔레메트리 데이터를 확인합니다.

![image](https://user-images.githubusercontent.com/14192817/139311399-a4603ad5-a5db-4814-a64a-910734639d41.png)
```bash
sudo iotedge logs SampleModule
```
Edge VM에 접속하여 명령어를 통해서 전송되는 텔레메트리 데이터를 확인합니다.
![image](https://user-images.githubusercontent.com/14192817/139311478-784ffa95-bd56-472a-9530-eaadea2ee2b4.png)

[Hands-on Lab 1 ~ 3 바로가기](https://github.com/min-git/IoTEdgeHOL/blob/main/HOL1-3.md)

[README 바로가기](https://github.com/min-git/IoTEdgeHOL/blob/main/README.md)
