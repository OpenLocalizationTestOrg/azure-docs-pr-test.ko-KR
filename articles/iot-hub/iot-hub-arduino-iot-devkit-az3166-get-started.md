---
title: "aaaIoT 하세요 toocloud IoT 하세요 AZ3166 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup이이 자습서에서는 toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 IoT 하세요 AZ3166 tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>IoT 하세요 AZ3166 tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

hello [MXChip IoT 하세요](https://microsoft.github.io/azure-iot-developer-kit/) 수 사용된 toodevelop 및 프로토타입 Microsoft Azure 서비스 활용 하 여 인터넷 IoT (사물) 솔루션입니다. 풍부한 주변 장치 및 센서가 있는 Arduino 호환 보드, 오픈 소스 보드 패키지 및 증가하는 [프로젝트 카탈로그](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/)를 포함합니다.

## <a name="what-you-do"></a>수행할 작업
연결 [하세요](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT 허브를 만들고, 센서의 온도 및 습도 데이터 수집 hello hello 데이터 tooIoT 허브 송신 하 합니다.

DevKit가 아직 없으세요? [여기](https://aka.ms/iot-devkit-purchase)에서 새 DevKit를 받으세요.

## <a name="what-you-learn"></a>학습 내용

* 어떻게 tooconnect IoT 하세요 tooWireless 액세스 가리킨 개발 환경을 준비 합니다.
* 어떻게 toocreate IoT hub MXChip IoT 하세요에 장치를 등록 하십시오.
* 어떻게 MXChip IoT 하세요에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.
* 어떻게 toosend hello 센서 데이터 tooyour IoT 허브입니다.

## <a name="what-you-need"></a>필요한 항목

* 마이크로 USB 케이블을 사용하는 MXChip IoT DevKit 보드. [지금 사용](https://aka.ms/iot-devkit-purchase)
* Windows 10 또는 macOS 10.10+를 실행하는 컴퓨터
* 활성 Azure 구독
  * [30일 평가판 Microsoft Azure 계정](https://azureinfo.microsoft.com/us-freetrial.html) 활성화

## <a name="prepare-your-hardware"></a>하드웨어 준비

Hello 하드웨어 tooyour 컴퓨터를 연결 합니다.

### <a name="hardware-you-need"></a>필요한 하드웨어

* DevKit 보드
* Micro USB 케이블

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>하세요 tooyour 컴퓨터 연결

1. USB 끝 tooyour PC를 연결 합니다.
2. 마이크로 USB 끝 toohello 하세요 연결
3. hello 녹색 led가 다음 toopower 연결 확인

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>WiFi 구성

IoT 프로젝트는 인터넷 연결에 의존합니다. 다음 지침 tooconfigure hello 하세요 tooconnect tooWiFi hello를 사용 합니다.

### <a name="enter-ap-mode"></a>AP 모드로 전환

단추 B 키를 누른 채, 푸시 및 릴리스 hello 단추를 선택한 다음 릴리스 단추 2. 그런 다음 다시 설정 프로그램 하세요 WiFi 구성 AP 모드 입력 됩니다. hello 구성 포털 IP 주소 뿐만 아니라 hello hello 하세요의 서비스 설정 Identifier(SSID) hello 화면 표시 됩니다.

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>TooDevKit AP를 연결 합니다.

이제 다른 WiFi 사용 장치 (PC 또는 모바일 폰) tooconnect toohello 하세요 SSID (또한 위의 스크린 샷에서 hello에 강조 표시)를 사용 하 여, hello 암호를 비워 둡니다.

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>DevKit용 WiFi 구성

PC 또는 모바일 폰 브라우저에서 hello 하세요 화면에 표시 된 hello open IP 주소, hello 하세요 tooconnect 원하는 hello WiFi 네트워크를 선택한 다음 hello 암호를 입력 합니다. 클릭 **연결** toocomplete:

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Hello 연결에 성공 hello 하세요 몇 초 후에 다시 부팅 됩니다. 성공한 경우 hello 화면에 hello WiFi 이름 및 IP 주소를 표시 됩니다.

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
hello 사진에 표시 된 hello IP 주소가 hello 실제 IP 할당 및 hello 하세요 화면에 표시 된 일치 하지 않을 수 있습니다. 이 정상으로 WiFi 사용 하 여 DHCP toodynamically Ip를 할당 합니다.

WiFi을 구성한 후 자격 증명 분리 하는 경우에 해당 연결에 대 한 hello 장치에 유지 됩니다. 예를 들어 집에 hello 하세요 WiFi에 대 한 구성 후 hello 하세요 toohello office 걸린 경우 tooreconfigure AP 모드 해야 합니다 (단계부터 **AP 모드 입력**) tooconnect hello tooyour office WiFi 하세요. 

## <a name="start-using-devkit"></a>DevKit 사용 시작

하세요에서 실행 되는 hello 기본 앱 hello 최신 펌웨어 버전을 hello 확인 하 고 사용자에 대 한 일부 센서 진단 데이터를 표시 합니다.

### <a name="upgrade-toohello-latest-firmware"></a>Toohello 최신 펌웨어를 업그레이드 합니다.

필요한 업그레이드 하는 경우 최신 펌웨어 버전을 hello 둘 다 hello 화면에 나타납니다. 에 따라 [펌웨어를 업그레이드](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) tooupgrade 안내 것입니다.

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
이 단일 작업 hello 하세요에서 개발을 시작 하면 되며 앱 업로드, hello 최신 펌웨어 응용 프로그램과 함께 제공 해야 합니다.

### <a name="test-various-sensors"></a>다양한 센서 테스트

Tootest 센서 단추 B 눌러, 각 센서를 통해 hello B 단추 toocycle를 눌렀다 계속 합니다.

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>개발 환경 준비

Hello 개발 환경을 시간 tooset 이제: 도구와 toobuild 멋진 IoT 응용 프로그램에 대 한 패키지입니다. Windows 또는 macOS 버전 tooyour 운영 체제에 따라 선택할 수 있습니다.


### <a name="windows"></a>Windows

하면 toouse hello 설치 패키지 tooprepare hello 개발 환경을 사용 하는 것이 좋습니다. 문제가 발생 하는 경우 참고할 수 hello [수동 단계](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget 수행 합니다.

#### <a name="download-latest-package"></a>최신 패키지 다운로드

hello `.zip` 모든 필요한 도구와 패키지 하세요 개발에 필요한 다운로드 한 파일을 포함 합니다.

> [!div class="button"]
[다운로드](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> hello `.zip` hello 다음을 포함 하는 파일 도구와 패키지 합니다. 이미 일부 구성 요소가 설치 되어 있으면 hello 스크립트에서는 검색 하 고을 건너뜁니다.
> * Node.js 및 Yarn: hello 설치 스크립트 및 자동화 된 작업에 대 한 런타임
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -MSI hello Azure 리소스를 관리 하기 위한 플랫폼 간 명령줄 환경을 종속 Python 및 pip를 포함 합니다.
> * [Visual Studio Code](https://code.visualstudio.com/): DevKit 개발을 위한 간단한 코드 편집기
> * [Arduino용 Visual Studio Code 확장](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS Code에서 Arduino 개발 활성화
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): hello 확장 Arduino에 대 한이 도구에 사용
> * 하세요 보드 패키지: 도구 체인, 라이브러리 및 프로젝트 형식에 hello 하세요
> * ST 링크 유틸리티: 필수 유틸리티 및 드라이버

#### <a name="run-installation-script"></a>설치 스크립트 실행

Windows 파일 탐색기에서 찾아 hello `.zip` 압축을 풀고, 찾기 및 `install.cmd`마우스 오른쪽 단추로 클릭 **"관리자 권한으로 실행"** toostart 합니다.

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

설치 하는 동안 각 도구 또는 패키지의 hello 진행률을 표시 됩니다.

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Tooinstall 드라이버를 확인 합니다.

VS Code Arduino 확장에 대 한 hello hello Arduino IDE에 의존합니다. 인 경우 hello hello Arduino IDE를 설치 하는 처음으로 증명된 tooinstall 관련 드라이버 수 있습니다.

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

인터넷 속도 따라 약 10 분 toofinish 설치를 취해야 합니다. Hello 설치가 완료 되 면 Visual Studio Code 및 Arduino IDE 바로 가기를 바탕 화면에 표시 됩니다.

> [!NOTE] 
경우에 따라서 VS Code를 시작할 때 Arduino IDE 또는 관련된 보드 패키지를 찾을 수 없다는 오류와 함께 메시지가 표시됩니다. VS Code 및 toosolve Arduino IDE를 한 번 시작 닫기 VS Code 것을 찾아야 Arduino IDE 경로 올바르게 합니다.


### <a name="macos-preview"></a>macOS(미리 보기)

이러한 단계 tooprepare 개발 환경을 macOS에 따릅니다.

#### <a name="install-azure-cli-20"></a>Azure CLI 2.0 설치

Hello에 따라 [공식 가이드](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:

`curl` 명령 하나로 Azure CLI 2.0을 설치합니다.

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

하 고 변경 내용 tootake 효과 대 한 명령 셸에서 다시 시작 합니다.

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Arduino IDE 설치

Visual Studio 코드 Arduino 확장 hello hello Arduino IDE에 의존합니다. 다운로드 및 설치 hello [macOS 용 Arduino IDE](https://www.arduino.cc/en/Main/Software)합니다.

#### <a name="install-visual-studio-code"></a>Visual Studio Code 설치

[macOS용 Visual Studio Code](https://code.visualstudio.com/)를 다운로드하고 설치합니다. 하세요 IoT 응용 프로그램을 구축 하기 위한 기본 개발 도구 hello 사용 됩니다.

####  <a name="download-latest-package"></a>최신 패키지 다운로드

1. Node.js를 설치합니다. 인기 있는 macOS 패키지 관리자를 사용할 수 있습니다 [Homebrew](https://brew.sh/) 또는 [설치 관리자 미리 만들어진](https://nodejs.org/en/download/) tooinstall 것입니다.

2. VS Code에서 DevKit 개발에 필요한 작업 스크립트를 포함하는 `.zip` 파일을 다운로드합니다.

   > [!div class="button"]
   [다운로드](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Hello 찾을 `.zip` 압축을 풉니다. 다음 실행 **터미널** 앱과 명령을 tooconfigure 다음 실행된 hello:

   압축 푼된 폴더 tooyour macOS 사용자 폴더를 이동 합니다.
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   `npm` 패키지 설치:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Arduino용 VS Code 확장 설치

Visual Studio Code 있습니다 tooinstall 마켓플레이스 확장 hello 도구에 직접, 단순히 hello 왼쪽된 메뉴 창의 hello 확장 아이콘을 클릭 한 다음 검색 `Arduino` tooinstall:

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>DevKit 보드 패키지 설치

Tooadd hello 하세요 보드 hello 보드 관리자를 사용 하 여 Visual Studio Code에서 필요 합니다.

1. 사용 하 여 `Cmd+Shift+P` tooinvoke 명령 팔레트과 형식 **Arduino** 다음 찾아 선택 **Arduino: 보드 관리자**합니다.

2. 클릭 **' Url을 추가로 '** 오른쪽 hello 아래에 있습니다.
   ![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. Hello에 `settings.json` 파일, hello 아래쪽에 선을 추가 `USER SETTINGS` 창 고 저장 합니다.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. 이제 'az3166' hello 보드 관리자에서에서 검색 하 고 hello 최신 버전을 설치 합니다.
   ![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

이제 모든 hello 필요한 도구 및 macOS에 설치 된 패키지를 완료 합니다.


## <a name="open-project-folder"></a>프로젝트 폴더 열기

### <a name="launch-vs-code"></a>VS Code 시작

DevKit이 연결되어 있지 않은지 확인합니다. VS Code를 처음 시작 하 고 hello 하세요 tooyour 컴퓨터를 연결 합니다. VS Code는 자동으로 찾고 소개 페이지를 팝업합니다.

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
경우에 따라서 VS Code를 시작할 때 Arduino IDE 또는 관련된 보드 패키지를 찾을 수 없다는 오류와 함께 메시지가 표시됩니다. toosolve Arduino IDE를 한 번 다시 시작이 닫기 VS Code 및 VS Code을 찾아야 Arduino IDE 경로 올바르게 합니다.

### <a name="open-arduino-examples-folder"></a>Arduino 예제 폴더 열기

너무 전환**' Arduino 예제 '** 탭, 너무 탐색`Examples for MXCHIP AZ3166 > AzureIoT` 을 클릭할 `GetStarted`합니다.

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Tooclose hello 창에서 문제가 발생 하는 경우 tooreload 것을 사용 하 여 `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke 명령 팔레트과 형식 **Arduino** toofind 선택 **Arduino: 예제**합니다.

## <a name="provision-azure-services"></a>Azure 서비스 프로비전

Hello 솔루션 창에서 작업을 통해 실행 `Ctrl+P` (macOS: `Cmd+P`) '클라우드를 프로 비전 작업'를 입력 하 여:

Hello VS Code 터미널 대화형 명령줄은 과정을 안내 하 프로비저닝 hello Azure 서비스를 필요 합니다.

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Arduino 스케치 빌드 및 업로드

### <a name="install-required-library"></a>필요한 라이브러리 설치

1. 키를 눌러 `F1` 또는 `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke 명령 팔레트과 형식 **Arduino** 다음 찾아 선택 **Arduino: 라이브러리 관리자**합니다.

2. `ArduinoJson` 라이브러리를 검색하고 **설치**를 클릭합니다.

### <a name="build-and-upload-hello-device-code"></a>빌드 및 hello 장치 코드 업로드

사용 하 여 `Ctrl+P` (macOS: `Cmd+P`) toorun ' 작업 장치 저장소에 자동 업로드 '. hello 터미널 tooenter 구성 모드 라는 메시지가 나타납니다. toodo A, 단추, 누른 다음 푸시 및 릴리스 hello 단추를 다시 설정 합니다. hello 화면에는 '구성' 표시 됩니다. ' 작업 클라우드 프로 비전 ' 단계에서 검색 하는 tooset hello 연결 문자열입니다.

다음을 확인 하 고 hello Arduino 스케치 업로드 시작 됩니다.

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

hello 하세요 재부팅 되며 hello 코드 실행을 시작 합니다.

## <a name="test-hello-project"></a>테스트 hello 프로젝트

VS Code hello 상태 표시줄 tooopen hello 직렬 모니터의 hello 전원 플러그 아이콘을 클릭 합니다.

hello 결과 뒤에 표시 되 면 hello 샘플 응용 프로그램을 성공적으로 실행:

* hello 직렬 모니터 디스플레이 hello 아래 스크린샷에서 hello의 hello 내용으로 동일한 정보입니다.
* hello MXChip IoT 하세요 LED가 깜박입니다.

![VS Code의 최종 출력](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>문제 및 피드백

찾을 수 있습니다 [Faq](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) 교류할 toous hello 채널 아래에서 문제가 발생 하는 경우.

## <a name="next-steps"></a>다음 단계

성공적 MXChip IoT 하세요 tooyour IoT 허브를 연결 하 고 보낸된 hello 캡처된 센서 데이터 tooyour IoT 허브입니다.

시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.

- [iothub-explorer를 사용하여 클라우드 장치 메시지 관리](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [데이터 저장소 tooAzure IoT Hub 메시지 저장](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Azure IoT 허브에서 Power BI toovisualize 실시간 센서 데이터를 사용 하 여](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Azure IoT 허브에서 Azure 웹 앱 toovisualize 실시간 센서 데이터를 사용 하 여](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [IoT 허브에서 hello 센서 데이터를 사용 하 여 Azure 기계 학습에서 일기 예보](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [iothub-explorer를 사용하여 장치 관리](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Logic Apps를 사용하여 원격 모니터링 및 알림](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)