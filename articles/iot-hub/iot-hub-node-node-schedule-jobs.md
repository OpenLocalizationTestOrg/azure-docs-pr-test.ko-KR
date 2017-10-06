---
title: "Azure IoT Hub (노드)와 aaaSchedule 작업 | Microsoft Docs"
description: "어떻게 tooschedule Azure IoT Hub 여러 장치에서 직접 메서드 tooinvoke를 작업입니다. Node.js tooimplement hello 시뮬레이션 된 장치 앱과 서비스 응용 프로그램 toorun hello 작업에 대 한 hello Azure IoT Sdk를 사용합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>작업 예약 및 브로드캐스트(노드)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Azure IoT Hub는 완전히 관리 되는 서비스를 백 엔드 응용 프로그램 toocreate 및 추적 작업을 예약 하 고 수백만 개의 장치로 업데이트는 합니다.  작업을 수행 하는 hello에 대 한 작업을 사용할 수 있습니다.

* desired 속성 업데이트
* tags 업데이트
* 직접 메서드 호출

개념적으로 작업이 다음이 작업 중 하나를 래핑하고 트랙 hello 장치로 이중 쿼리 문자로 정의 되는, 장치 집합에 대 한 실행의 진행 상태.  예를 들어 백 엔드 응용 프로그램 수 작업 tooinvoke 다시 부팅에서 메서드를 사용할 장치 10, 000 장치로 이중 쿼리에 의해 지정 되 고 이후 시간에 예약 합니다.  해당 응용 프로그램 수신 각각의 이러한 장치 및 hello 재부팅 메서드를 실행 한 다음 진행률을 추적할 수입니다.

이러한 기능에 대한 자세한 내용은 다음 문서를 참조하세요.

* 장치로 이중 및 속성: [장치 트윈스 시작] [ lnk-get-started-twin] 및 [자습서: 어떻게 toouse 장치로 이중 속성][lnk-twin-props]
* 직접 메서드: [IoT Hub 개발자 가이드 - 직접 메서드][lnk-dev-methods] 및 [자습서: 직접 메서드][lnk-c2d-methods]

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* 그러면 직접 메서드가 있는 시뮬레이트된 장치 앱 만들기 **lockDoor** hello 솔루션 백 엔드에서 호출할 수 있습니다.
* 해당 호출 hello Node.js 콘솔 응용 프로그램 만들기 **lockDoor** 작업 및 업데이트 hello를 사용 하 여 hello 시뮬레이션 된 장치 앱에서 직접적인 방법 원하는 장치 작업을 사용 하는 속성입니다.

이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램을 사용할 수 있습니다.

**simDevice.js**, hello 장치 id를 가진 tooyour IoT 허브를 연결 하 고 수신 하는 **lockDoor** 직접적인 방법입니다.

**scheduleJobService.js**, 작업을 사용 하 여로 이중의 원하는 속성 hello 시뮬레이션 된 장치 앱과 업데이트 hello 장치에서 직접 메서드를 호출 하 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Node.js 버전 0.12.x 이상, <br/>  [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기
이 섹션에서는 tooa 직접 메서드 호출에서 시뮬레이션 된 장치를 다시 부팅을 트리거하는 hello 클라우드가 응답 하 여 Node.js 콘솔 응용 프로그램을 만들고 사용 하 여 hello 속성 tooenable 장치로 이중 쿼리 tooidentify 장치 및 마지막 재부팅 될 보고 합니다.

1. **simDevice**라는 빈 폴더를 새로 만듭니다.  Hello에 **simDevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **simDevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 장치 SDK 패키지 및 **azure iot-장치 mqtt** 패키지:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 텍스트 편집기를 사용 하 여 만드는 새 **simDevice.js** hello에 대 한 파일 **simDevice** 폴더입니다.
4. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **simDevice.js** 파일:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. 추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. 다음 함수 toohandle hello hello 추가 **lockDoor** 메서드.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Hello hello에 대 한 코드 tooregister hello 처리기를 다음 추가 **lockDoor** 메서드.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. 저장 후 닫기 hello **simDevice.js** 파일입니다.

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>직접 메서드를 호출하고 장치 쌍의 속성을 업데이트하기 위한 작업 예약
이 섹션에서는 원격을 시작 하 여 Node.js 콘솔 응용 프로그램을 만들면 **lockDoor** 는 직접 메서드와 업데이트 hello 장치로 이중의 속성을 사용 하는 장치에 있습니다.

1. **scheduleJobService**라는 빈 폴더를 새로 만듭니다.  Hello에 **scheduleJobService** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **scheduleJobService** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 장치 SDK 패키지 및 **azure-iot-장치-mqtt**패키지:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. 텍스트 편집기를 사용 하 여 만드는 새 **scheduleJobService.js** hello에 대 한 파일 **scheduleJobService** 폴더입니다.
4. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_gscheduleJobServiceetstarted_service.js** 파일:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. 다음 변수 선언을 hello를 추가 하 고 hello 자리 표시자 값을 바꿉니다.
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Hello 함수 hello 작업을 사용 하는 toomonitor hello 실행 될 다음을 추가 합니다.
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. 다음 코드 tooschedule hello 작업 hello 장치 메서드를 호출 하는 hello를 추가 합니다.
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. 다음 코드 tooschedule hello 작업 tooupdate hello 장치로 이중 hello를 추가 합니다.
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. 저장 후 닫기 hello **scheduleJobService.js** 파일입니다.

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행
준비 toorun hello 응용 프로그램입니다.

1. Hello에 대 한 hello 명령 프롬프트 **simDevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.
   
    ```
    node simDevice.js
    ```
2. Hello에 대 한 hello 명령 프롬프트 **scheduleJobService** hello 명령 tootrigger hello 작업 toolock hello 문과 업데이트 hello로 이중 다음를 실행 하는 폴더
   
    ```
    node scheduleJobService.js
    ```
3. Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 작업 tooschedule 직접적인 방법 tooa 장치 및 hello hello 장치로 이중의 속성을 업데이트를 사용 합니다.

IoT Hub 및 시작 원격 같은 장치 관리 패턴 hello 공기 펌웨어 업데이트를 통해 toocontinue 참조:

[자습서: toodo 펌웨어 업데이트 방법][lnk-fwupdate]

IoT Hub와 시작 toocontinue 참조 [Azure IoT 가장자리 시작][lnk-iot-edge]합니다.

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
