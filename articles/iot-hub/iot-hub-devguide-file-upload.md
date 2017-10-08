---
title: "Azure IoT Hub 파일 업로드 aaaUnderstand | Microsoft Docs"
description: "개발자 가이드-IoT Hub toomanage 장치 tooan Azure 저장소 blob 컨테이너에서 파일 업로드 중 사용 하 여 hello 파일 업로드 기능입니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a>IoT Hub를 사용하여 파일 업로드

Hello에 설명 된 대로 [IoT Hub 끝점] [ lnk-endpoints] 문서, 장치를 장치에 연결 끝점을 통해 알림을 전송 하 여 파일 업로드를 시작할 수 있습니다 (**/devices/ {deviceId}파일/**). IoT Hub hello 통해 파일 업로드 알림 메시지를 보냅니다는 업로드가 완료 되는 되는 장치 IoT Hub을 확인 하면 **/messages/servicebound/filenotifications** 웹 서비스 끝점입니다.

IoT Hub 자체 IoT 허브를 통해 메시지를 조정 하는 대신 발송자 tooan 연결 된 Azure 저장소 계정으로 대신 사용 합니다. 장치는 tooupload 하지 않고자 한다면 특정 toohello 파일 hello 장치가 IoT 허브에서 저장소 토큰을 요청 합니다. hello 장치에서 SAS URI tooupload hello 파일 toostorage hello를 사용 하 고 hello 장치 완료 tooIoT 허브에 대 한 알림을 보냅니다 hello 업로드가 완료 되 면 키를 누릅니다. IoT Hub hello 파일 업로드가 완료 되 고 다음 파일 업로드 알림 메시지 toohello 서비스 지향 파일 알림 끝점에 추가 확인 합니다.

장치에서 파일 tooIoT 허브를 업로드 하기 전에 하 여 허브를 구성 해야 [Azure 저장소 연결] [ lnk-associate-storage] tooit 계정.

그런 다음 다른 장치를 [업로드 초기화] [ lnk-initialize] 차례로 [IoT hub를 알릴] [ lnk-notify] hello 업로드가 완료 되 면 합니다. 필요에 따라 해당 hello 업로드가 완료 되 되는 장치가 IoT Hub을 확인 하면 hello 서비스 수를 생성 한 [알림 메시지][lnk-service-notification]합니다.

### <a name="when-toouse"></a>때 toouse

파일 업로드 toosend 미디어 파일 및 간헐적으로 연결 된 장치 또는 압축 된 toosave 대역폭에서 업로드 하는 큰 원격 분석 일괄 처리를 사용 합니다.

너무 참조[장치-클라우드 통신 지침] [ lnk-d2c-guidance] 보고 속성, 장치-클라우드 메시지 또는 파일을 업로드 하 여 확실 하지 않은 경우.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Azure Storage 계정을 IoT Hub와 연결

toouse hello 파일 업로드 기능을 먼저 Azure 저장소 계정 toohello IoT 허브 연결 해야 합니다. Hello를 통해이 작업을 완료할 수 [Azure 포털][lnk-management-portal], 또는 hello를 통해 프로그래밍 방식으로 [IoT 허브 리소스 공급자 REST Api] [ lnk-resource-provider-apis]. IoT Hub와 Azure 저장소 계정을 연결한 후 hello 서비스 장치를 반납 SAS URI tooa hello 장치 파일 업로드 요청을 시작 합니다.

> [!NOTE]
> hello [Azure IoT Sdk] [ lnk-sdks] 자동으로 SAS URI hello 파일을 업로드 하 고 업로드 완료의 IoT 허브를 알리는 hello 핸들을 검색 합니다.


## <a name="initialize-a-file-upload"></a>파일 업로드 초기화
IoT Hub에 장치 toorequest 저장소 tooupload 파일에 대 한 SAS URI에 대 한 구체적으로 끝점이 있습니다. tooinitiate hello 파일 업로드 프로세스가 hello 전송 하는 장치에 POST 요청 너무`{iot hub}.azure-devices.net/devices/{deviceId}/files` JSON 본문을 수행 하는 hello로:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IoT Hub 같은 tooupload hello 파일을 사용 하 여 hello 장치 데이터가 hello를 반환 합니다.

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>사용되지 않음: GET으로 파일 업로드 초기화

> [!NOTE]
> 이 섹션에서는 사용 되지 않는 기능 방법에 대 한 설명 tooreceive IoT 허브에서 SAS URI입니다. 앞에서 설명한 hello POST 메서드를 사용 합니다.

IoT Hub에 두 개의 REST 끝점 toosupport 파일이 저장소에 대 한 하나의 tooget hello SAS URI를 업로드 하 고 다른 toonotify hello IoT hub 업로드 완료의 hello 있습니다. hello 장치 시작 hello 파일 업로드 프로세스에서 GET toohello IoT 허브를 전송 하 여 `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`합니다. hello IoT hub를 반환합니다.

* 특정 toohello 파일 toobe 업로드 하는 SAS URI입니다.
* 상관 관계 ID toobe hello 업로드를 완료 한 후 사용 합니다.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>IoT Hub에 완료된 파일 업로드 알림

hello 장치는 hello 파일 toostorage hello Azure 저장소 Sdk를 사용 하 여 업로드 합니다. Hello 장치 너무 POST 요청을 보냅니다 hello 업로드가 완료 되 면`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` JSON 본문을 수행 하는 hello로:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

값을 hello `isSuccess` 은 성공적으로 업로드 된 hello 파일이 있는지 여부를 나타내는 Boolean입니다. 상태 코드에 대 한 hello `statusCode` hello hello 파일 toostorage의 hello 업로드에 대 한 상태 이며 hello `statusDescription` toohello 해당 `statusCode`합니다.

## <a name="reference-topics"></a>참조 항목:

hello 다음 참조 항목 제공 장치에서 파일을 업로드 하는 방법에 대 한 자세한 내용은 합니다.

## <a name="file-upload-notifications"></a>파일 업로드 알림

필요에 따라 장치를 메시지를 표시 IoT 허브는 업로드가 완료 되 IoT Hub hello 파일의 hello 이름 및 저장소 위치를 포함 하는 알림 메시지를 생성할 수 있습니다.

[끝점][lnk-endpoints]에서 설명한 대로 IoT Hub는 서비스 지향 끝점(**/messages/servicebound/fileuploadnotifications**)을 통해 파일 업로드 알림을 메시지로 전달합니다. 파일 업로드 알림 되며 클라우드-장치 메시지의 경우와 동일 hello 동일 hello 있는 hello 수신 의미 체계 [메시지 수명 주기][lnk-lifecycle]합니다. Hello 파일 업로드 알림 끝점에서 검색 된 각 메시지는 다음과 같은 속성 hello로 JSON 레코드:

| 속성 | 설명 |
| --- | --- |
| EnqueuedTimeUtc |Hello 알림이 생성 될 때를 나타내는 타임 스탬프입니다. |
| deviceId |**DeviceId** hello 장치 hello 파일 업로드 됩니다. |
| BlobUri |Hello 업로드 된 파일의 URI입니다. |
| BlobName |파일을 업로드 하는 hello의 이름. |
| LastUpdatedTime |Hello 파일에 마지막으로 업데이트를 나타내는 타임 스탬프입니다. |
| BlobSizeInBytes |Hello의 크기는 파일을 업로드 합니다. |

**예제**. 이 예제에서는 파일 hello 본문 업로드 알림 메시지를 보여 줍니다.

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a>파일 업로드 알림 구성 옵션

각 IoT 허브는 다음 구성 옵션에 대 한 파일 업로드 알림 hello를 노출 합니다.

| 속성 | 설명 | 범위 및 기본값 |
| --- | --- | --- |
| **enableFileUploadNotifications** |파일 업로드 알림 toohello 파일 notifications 끝점에 기록 되는지 여부를 제어 합니다. |Bool. 기본값은 True입니다. |
| **fileNotifications.ttlAsIso8601** |파일 업로드 알림에 대한 기본 TTL입니다. |Too48H ISO_8601 간격 (최소 1 분)입니다. 기본값은 1시간입니다. |
| **fileNotifications.lockDuration** |Hello 파일 업로드 알림 큐에 대 한 잠금 기간입니다. |5 too300 초 (최소 5 초)입니다. 기본값은 60초입니다. |
| **fileNotifications.maxDeliveryCount** |최대 배달 횟수 hello 파일에 대 한 알림 큐를 업로드 합니다. |1 too100 합니다. 기본값은 100입니다. |

## <a name="additional-reference-material"></a>추가 참조 자료

Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.

* [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.
* [제한 및 할당량] [ lnk-quotas] hello 할당량을 설명 하 고 toohello IoT 허브 서비스에 적용 되는 동작을 조정 합니다.
* [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.
* [IoT Hub 쿼리 언어] [ lnk-query] 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용할 수는 hello 쿼리 언어에 설명 합니다.
* [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계

IoT 허브를 사용 하 여 장치에서 파일을 tooupload 방법 파악 했으므로, 이제 hello 다음 IoT 허브 개발자 가이드 항목에에서 관심이 있을 수 있습니다.

* [IoT Hub에서 장치 ID 관리][lnk-devguide-identities]
* [컨트롤 액세스 tooIoT 허브][lnk-devguide-security]
* [장치 트윈스 toosynchronize 상태 및 구성 사용][lnk-devguide-device-twins]
* [장치에서 직접 메서드 호출][lnk-devguide-directmethods]
* [여러 장치에서 jobs 예약][lnk-devguide-jobs]

이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.

* [IoT Hub와 장치 toohello에서 tooupload 파일 클라우드 하는 방법][lnk-fileupload-tutorial]

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
