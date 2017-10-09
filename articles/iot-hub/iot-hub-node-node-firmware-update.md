---
title: "Azure IoT Hub (노드)와 aaaDevice 펌웨어 업데이트 | Microsoft Docs"
description: "Azure IoT Hub tooinitiate 장치 펌웨어에 toouse 장치 관리 업데이트 하는 방법입니다. 시뮬레이션 된 장치 응용 프로그램 및 서비스 앱 hello 펌웨어 업데이트를 트리거하는 Node.js tooimplement에 대 한 hello Azure IoT Sdk를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>장치 관리 tooinitiate 장치 펌웨어 업데이트 / (노드)를 사용 하 여
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>소개
Hello에 [장치 관리 시작] [ lnk-dm-getstarted] 자습서에서 언급 했 듯이 어떻게 toouse hello [장치로 이중] [ lnk-devtwin] 및 [직접 메서드] [ lnk-c2dmethod] 기본 형식 tooremotely는 장치를 다시 부팅 합니다. 이 자습서에서는 hello IoT Hub 기본 형식과 동일 하 고 지침을 제공 및 toodo는-종단 펌웨어 업데이트를 시뮬레이션 하는 방법을 보여 줍니다.  이 패턴은 hello Intel Edison 장치 샘플에 대 한 hello 펌웨어 업데이트 구현에서 사용 됩니다.

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 hello firmwareUpdate 직접 메서드를 호출 하 여 Node.js 콘솔 응용 프로그램을 만듭니다.
* **firmwareUpdate** 직접 메서드를 구현하는 시뮬레이트된 장치 앱을 만듭니다. 이 메서드를 toodownload hello 펌웨어 이미지 될 때까지 대기 하 고, hello 펌웨어 이미지를 다운로드 하 고, 마지막으로 hello 펌웨어 이미지를 적용 하는 여러 단계로 이루어진 프로세스를 시작 합니다. Hello 업데이트의 각 단계 hello 장치 사용 하 여 hello 속성 tooreport를 진행률 보고 했습니다.

이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램을 사용할 수 있습니다.

**dmpatterns_fwupdate_service.js**, hello 응답 표시 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 고 정기적으로 (500 밀리초 마다) 업데이트 표시 hello 보고 속성입니다.

**dmpatterns_fwupdate_device.js**를 포함 하 여 펌웨어 업데이트 다중 상태 프로세스 toosimulate을 통해 실행을 firmwareUpdate 직접 메서드를 받으면 앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는: hello에 대 한 대기 중 이미지를 다운로드 hello 새 이미지를 다운로드 하 고 마지막으로 hello 이미지를 적용 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Node.js 버전 0.12.x 이상, <br/>  [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

Hello에 따라 [장치 관리 시작](iot-hub-node-node-device-management-get-started.md) 문서 toocreate IoT hub 및 IoT 허브 연결 문자열을 가져옵니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>직접 메서드를 사용 하 여 hello 장치에 대 한 원격 펌웨어 업데이트 트리거
이 섹션에서는 장치에서 원격 펌웨어 업데이트를 시작하는 Node.js 콘솔 앱을 만듭니다. hello 앱 직접적인 방법 tooinitiate hello 업데이트를 사용 하 고 사용 하 여 장치로 이중 쿼리 tooperiodically hello 액티브 펌웨어 업데이트의 hello 상태를 가져옵니다.

1. **triggerfwupdateondevice**라는 빈 폴더를 만듭니다.  Hello에 **triggerfwupdateondevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **triggerfwupdateondevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 허브** 및 **azure iot-장치 mqtt** 장치 SDK 패키지:
   
    ```
    npm install azure-iothub --save
    ```
3. 텍스트 편집기를 사용 하 여 만들는 **dmpatterns_getstarted_service.js** hello에 대 한 파일 **triggerfwupdateondevice** 폴더입니다.
4. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_service.js** 파일:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. 다음 변수 선언을 hello를 추가 하 고 hello 자리 표시자 값을 바꿉니다.
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Hello 다음 toofind 함수 값을 표시할 hello hello firmwareUpdate의 추가 속성을 보고 합니다.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. Hello 함수 tooinvoke hello firmwareUpdate 메서드 tooreboot hello 대상 장치를 다음을 추가 합니다.
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. 마지막으로 추가 hello 다음 toocode toostart hello 펌웨어 업데이트 시퀀스를 작동 하 고 정기적으로 표시 되기 시작 hello 속성을 보고 합니다.
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. 저장 후 닫기 hello **dmpatterns_fwupdate_service.js** 파일입니다.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Hello 앱 실행
준비 toorun hello 앱입니다.

1. Hello에 대 한 hello 명령 프롬프트 **manageddevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Hello에 대 한 hello 명령 프롬프트 **triggerfwupdateondevice** hello 명령 tootrigger hello 원격 다음를 실행 하는 폴더를 다시 부팅 하 고 hello 장치로 이중 toofind hello 마지막 시간을 다시 부팅에 대 한 쿼리 합니다.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 직접적인 방법 tootrigger 원격을 사용 하는 장치 및 사용 하는 hello에 펌웨어 업데이트가 보고 되는 hello 펌웨어 업데이트의 속성 toofollow hello 진행률입니다.

toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
