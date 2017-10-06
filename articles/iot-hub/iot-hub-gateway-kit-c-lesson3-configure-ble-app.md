---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 3: 샘플 앱 실행 | Microsoft Docs"
description: "IoT hub 및 배포용 SensorTag에서 배포용 샘플 응용 프로그램 tooreceive 데이터를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "배포용 응용 프로그램, 센서 모니터 응용 프로그램, 센서 데이터 수집, 센서, 센서 데이터 toocloud의 데이터"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>BLE 샘플 응용 프로그램 구성 및 실행

## <a name="what-you-will-do"></a>수행할 사항

- Hello 샘플 리포지토리를 복제 합니다. 
- SensorTag 및 Intel NUC 간에 hello 연결을 설정 합니다. 
- 배포용 (Bluetooth 낮은 에너지) 샘플 응용 프로그램에 대 한 hello Azure CLI tooget SensorTag 정보와 IoT 허브를 사용 합니다. 구성 하 고 hello 배포용 샘플 응용 프로그램을 실행 합니다. 

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

이 문서에서는 다음에 대해 알아봅니다.

- 어떻게 tooconfigure 및 실행된 hello 배포용 샘플 응용 프로그램입니다.

## <a name="what-you-need"></a>필요한 항목

다음을 완료해야 합니다.

- [IoT Hub 만들기 및 SensorTag 등록](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Hello 샘플 리포지토리 toohello 호스트 컴퓨터를 복제 합니다.

tooclone hello 샘플 리포지토리 hello 호스트 컴퓨터에서 다음이 단계를 수행 합니다.

1. Windows에서 명령 프롬프트 창을 열거나 macOS 또는 Ubuntu에서 터미널을 엽니다.
2. Hello 다음 명령을 실행 합니다.

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>SensorTag 및 Intel NUC 간 hello 연결 설정

hello 연결을 tooset hello 호스트 컴퓨터에서 다음이 단계를 따르십시오.

1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. 열기 `config-gateway.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. 다음 코드 줄을 hello 찾기 및 바꾸기 `[device hostname or IP address]` Intel NUC의 hello IP 주소 또는 호스트 이름으로 합니다.
   ![config gateway의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Hello 다음 명령을 실행 하 여 Intel NUC에 도우미 도구를 설치 합니다.

   ```bash
   gulp install-tools
   ```

5. 다음 그림에서는 hello 및 녹색 LED가 깜박입니다 hello로 hello 전원 단추를 눌러 SensorTag를 켭니다.

   ![센서 태그 켜기](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Hello 다음 명령을 실행 하 여 스캔 SensorTag 장치:

   ```bash
   gulp discover-sensortag
   ```

7. Hello 다음 명령을 실행 하 여 hello SensorTag 및 Intel NUC 간의 hello 연결을 테스트 합니다.

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   대체 `{mac address}` hello 이전 단계에서 가져온 MAC 주소 hello로 합니다.

## <a name="get-hello-connection-string-of-sensortag"></a>SensorTag의 hello 연결 문자열 가져오기

tooget hello hello 다음 hello 호스트 컴퓨터에서 명령을 실행 SensorTag의 Azure IoT 허브 연결 문자열:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`사용한 hello IoT 허브 이름이입니다. Iot 게이트웨이 사용 하 여의 hello 값으로 `{resource group name}` mydevice의 hello 값으로 사용 하 여 `{device id}` hello 값 2 단원에서에서 변경 되지 않은 경우.

## <a name="configure-hello-ble-sample-application"></a>Hello 배포용 샘플 응용 프로그램 구성

tooconfigure 및 실행된 hello 배포용 샘플 응용 프로그램에서는 hello 호스트 컴퓨터에서 다음이 단계를 따르십시오.

1. 열기 `config-sensortag.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Hello 대체 hello 코드에서 다음을 확인 합니다.
   - 대체 `[IoT hub name]` 사용한 hello IoT 허브 이름을 사용 합니다.
   - 대체 `[IoT device connection string]` 가져온 SensorTag의 hello 연결 문자열을 사용 합니다.
   - 대체 `[device_mac_address]` hello 가져온 SensorTag의 MAC 주소 hello로 합니다.

3. Hello 배포용 샘플 응용 프로그램을 실행 합니다.

   toorun hello 배포용 샘플 응용 프로그램에서는 hello 호스트 컴퓨터에서 다음이 단계를 따르십시오.

   1. SensorTag를 켭니다.

   2. 배포 및 실행 hello 배포용 샘플 응용 프로그램 Intel NUC hello 다음 명령을 실행 하 여:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Hello 배포용 샘플 응용 프로그램이 작동 하는지 확인 하십시오.

이제 hello 다음과 같은 출력을 표시 됩니다.

![BLE 샘플 응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

온도 데이터 수집을 유지 하 고 tooyour IoT 허브를 전송 하는 hello 샘플 응용 프로그램입니다. hello 샘플 응용 프로그램 보낸 40 초 후에 자동으로 종료 합니다.

## <a name="summary"></a>요약

성공적으로 SensorTag와 Intel NUC 간에 hello 연결을 설정 하 고 수집 하 고 SensorTag tooyour IoT 허브에서 데이터를 전송 하는 배포용 샘플 응용 프로그램을 실행 했습니다. Toolearn 준비를 하는 방법을 IoT hub 받은 tooverify hello 데이터입니다.

## <a name="next-steps"></a>다음 단계
[IoT Hub에서 메시지 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)