# IoT Edge Hands-on Lab 실습
IoT Edge 모듈 배포 Hands-on Lap 입니다.
Ubuntu Linux VM상에 Azure IoT Edge를 설치하여 Edge 디바이스를 생성 합니다.
생성된 Edge 디바이스 VM에 VSCode를 활용하여 소스코드를 컨테이너 이미지로 생성하여 배포 합니다.

이번 과정에서는 아래의 내용을 실습 합니다.
1. Ubuntu Linux VM 생성
2. 생성된 Ubuntu Linux에 Azure IoT Edge runtime 설치
3. Visual Studio Code의 IoT Edge Extension을 통해서 SampleModule 프로젝트 생성
4. Azure Container Registry 생성
5. Visual Studio Code를 통한 컨테이너 이미지 빌드 및 Azure Container Registry 연동
6. IoT Edge 디바이스에 Edge 모듈 배포

# 사전 준비사항
- IoT Hub 생성 완료
- [Git 설치](https://git-scm.com/downloads)
- [Visual Studio Code 설치](https://code.visualstudio.com/)
   - Visual Studio Code Extension 설치 (C#, Azure IoT Hub Toolkit, Azure IoT Edge)
- [.NET Core 3.1 설치](https://dotnet.microsoft.com/download/dotnet)
- [Docker Container Desktop 설치 교육목적](https://docs.docker.com/desktop/windows/install/)


# Hands-on Lab
[Hands-on Lab 1 ~ 3](https://github.com/min-git/IoTEdgeHOL/blob/main/HOL1-3.md)

[Hands-on Lab 4 ~ 5](https://github.com/min-git/IoTEdgeHOL/blob/main/HOL4-5.md)
