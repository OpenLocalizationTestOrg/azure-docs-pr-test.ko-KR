---
title: "Azure IoT 가장자리에 맞춰 IoT 게이트웨이에서 aaaData 변환 | Microsoft Docs"
description: "IoT 게이트웨이 tooconvert hello Azure IoT 가장자리에서 사용자 지정 된 모듈을 통해 센서 데이터의 형식을 사용 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 게이트웨이 데이터 변환, IoT 게이트웨이 데이터 변환"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>IoT 게이트웨이를 사용하여 Azure IoT Edge를 통해 센서 데이터 변환

> [!NOTE]
> 이 자습서를 시작 하기 전에 확인 완료 된 hello 단원을 순서에서 다음을 저장 했습니다.
> * [Intel NUC를 IoT 게이트웨이로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [IoT 게이트웨이 tooconnect 작업 toohello 클라우드 SensorTag tooAzure IoT 허브를 사용 하 여](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

하나는 Iot 게이트웨이 데이터 수집 tooprocess toohello 클라우드를 보내기 전에 합니다. Azure IoT 가장자리는 생성 되 고 어셈블된 tooform hello 데이터 처리 워크플로 수 있는 모듈을 소개 합니다. 모듈은 메시지를 수신, 특별 한 조치를 수행 및 다른 모듈 tooprocess에 대 한에서 이동 합니다.

## <a name="what-you-learn"></a>학습 내용

다른 형식으로 SensorTag hello에서 toocreate 모듈 tooconvert 메시지 방법을 방법을 배웁니다.

## <a name="what-you-do"></a>수행할 작업

* Hello.json 형식으로 모듈 tooconvert 받은 메시지를 만듭니다.
* Hello 모듈을 컴파일하십시오.
* Azure IoT 가장자리에서 hello 모듈 toohello 배포용 샘플 응용 프로그램을 추가 합니다.
* Hello 샘플 응용 프로그램을 실행 합니다.

## <a name="what-you-need"></a>필요한 항목

* 다음 순서 대로 완료할 자습서 hello:
  * [Intel NUC를 IoT 게이트웨이로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [IoT 게이트웨이 tooconnect 작업 toohello 클라우드 SensorTag tooAzure IoT 허브를 사용 하 여](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* 호스트 컴퓨터에서 실행되는 SSH 클라이언트 - Windows의 경우 PuTTY를 사용하는 것이 좋습니다. Linux와 macOS의 경우 이미 SSH 클라이언트와 함께 제공됩니다.
* hello IP 주소 및 hello SSH 클라이언트에서 hello 사용자 이름 및 암호 tooaccess hello 게이트웨이 제공 합니다.
* 인터넷 연결.

## <a name="create-a-module"></a>모듈 만들기

1. Hello 호스트 컴퓨터에서 hello SSH 클라이언트를 실행 하 고 toohello IoT 게이트웨이 연결 합니다.
1. GitHub의 hello IoT 게이트웨이 toohello 홈 디렉터리에서 hello 변환 모듈의 소스 파일 hello hello 다음 명령을 실행 하 여 복제:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   이것이 hello C 프로그래밍 언어로 작성 된 네이티브 Azure 가장자리 모듈입니다. hello 모듈 하나를 따르는 hello에 수신된 된 메시지의 hello 형식을 변환 합니다.

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Hello 모듈을 컴파일합니다

toocompile hello 모듈을 hello 다음 명령을 실행 합니다.

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

얻게는 `libmy_module.so` hello 컴파일 완료 된 후 파일입니다. 이 파일의 절대 경로 hello 기록해 둡니다.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Hello 모듈 toohello 배포용 샘플 응용 프로그램 추가

1. Hello 다음 명령을 실행 하 여 toohello samples 폴더를 이동 합니다.

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.

   ```bash
   vi ble_gateway.json
   ```

1. 다음 코드 toohello hello를 삽입 하 여 모듈을 추가 `modules` 섹션.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. 대체 `[Your libmy_module.so path]` hello hello libmy_module.so의 절대 경로 사용 하 여 hello 코드에서 ' 파일입니다.
1. Hello의 hello 코드 `links` 하나를 따르는 hello로 섹션:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. 키를 눌러 `ESC`, 한 다음 입력 `:wq` toosave hello 파일입니다.

## <a name="run-hello-sample-application"></a>Hello 샘플 응용 프로그램 실행

1. Hello SensorTag 켭니다.
1. Hello 다음 명령을 실행 하 여 hello SSL_CERT_FILE 환경 변수를 설정 합니다.

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Hello 다음 명령을 실행 하 여 hello 추가 된 모듈과 함께 hello 샘플 응용 프로그램을 실행 합니다.

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>다음 단계

성공적으로 사용 하 여 hello IoT 게이트웨이 tooconvert hello 메시지를 SensorTag에서 hello.json 형식으로 했습니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
