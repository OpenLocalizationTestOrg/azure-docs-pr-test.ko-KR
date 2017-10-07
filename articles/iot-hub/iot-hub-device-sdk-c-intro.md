---
title: "C 언어용 aaaThe Azure IoT 장치 SDK | Microsoft Docs"
description: "C에 대 한 hello Azure IoT 장치와 SDK 시작 하 고 자세한 방법을 toocreate 장치 앱 통신 하는 IoT 허브를 사용 합니다."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>C용 Azure IoT 장치 SDK

hello **Azure IoT 장치 SDK** 라이브러리의 집합을 설계 hello에서 메시지 받기를 tooand 메시지를 보내는 toosimplify hello 과정은 **Azure IoT Hub** 서비스입니다. Hello에 설명 하지만 hello SDK, 각 특정 플랫폼을 대상으로 이름의 다른 변형이 **C에 대 한 Azure IoT 장치 SDK**합니다.

ANSI C (C99) toomaximize 이식성 C에 대 한 hello Azure IoT 장치 SDK로 작성 됩니다. 이 기능은 hello 라이브러리 잘 맞는 toooperate 여러 플랫폼 및 장치에 디스크를 최소화 하는 경우에 특히 만들고 메모리 사용량은 우선 순위를 합니다.

광범위 한 다양 한 플랫폼 SDK는 hello에서 테스트 되었습니다 (hello 참조 [Azure IoT 장치 카탈로그에 대 한 인증](https://catalog.azureiotsuite.com/) 세부 정보에 대 한). 이 문서 hello Windows 플랫폼에서 실행 되는 샘플 코드의 연습을 포함 하지만 hello 다양 한 지원 되는 플랫폼에서이 문서에서 설명 하는 hello 코드는 동일 합니다.

이 문서 hello Azure IoT 장치 SDK의 toohello 아키텍처의 소개 3. 방법을 tooinitialize hello 장치 라이브러리 데이터 tooIoT 허브에 메시지 보내기 및 받기 여기에서 보여 줍니다. 이 문서의 정보 hello hello SDK를 사용 하 여 시작 하는 데 충분 한 tooget 수도 있지만 또한 hello 라이브러리에 대 한 포인터 tooadditional 정보를 제공 합니다.

## <a name="sdk-architecture"></a>SDK 아키텍처

Hello를 찾을 수 있습니다 [ **C에 대 한 Azure IoT 장치 SDK** ](https://github.com/Azure/azure-iot-sdk-c) hello에 hello API의 GitHub 리포지토리 및 뷰 세부 정보 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)합니다.

hello에 최신 버전의 hello 라이브러리 hello 있습니다 **마스터** hello 리포지토리의 분기:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* hello hello SDK의 핵심 구현 중인 hello **iothub\_클라이언트** hello 구현의 hello 가장 낮은 API 계층 hello SDK에에서 포함 된 폴더: hello **IoTHubClient** 라이브러리입니다. hello **IoTHubClient** 라이브러리 메시지 tooIoT 허브 송수신 IoT 허브에서 메시지에 대 한 원시 메시징을 구현 하는 Api가 포함 되어 있습니다. 이 라이브러리를 사용할 때 메시지 직렬화를 구현해야 하며 IoT Hub와 통신하기 위한 기타 세부 사항도 직접 처리해야 합니다.
* hello **serializer** 폴더 도우미 함수 및 tooserialize 데이터 tooAzure IoT 허브를 사용 하 여 보내기 전에 클라이언트 라이브러리를 hello 하는 방법을 보여 주는 샘플이 포함 되어 있습니다. hello 사용 하 여 hello serializer의 필수 이며 편의 위해 제공 됩니다. toouse hello **serializer** hello 데이터 toosend tooIoT 허브 및 hello 메시지에서 tooreceive 예상를 지정 하는 모델을 정의할 라이브러리에 있습니다. Hello 모델에서 정의 되 면 hello SDK 한를 사용 하면 하는 API 화면으로 tooeasily 작업 장치-클라우드 하 고에 대 한 걱정 없이 클라우드-장치 메시지 hello serialization 정보입니다. hello 라이브러리와 같은 MQTT 및 AMQP 프로토콜을 사용 하 여 전송을 구현 하는 다른 오픈 소스 라이브러리에 따라 달라 집니다.
* hello **IoTHubClient** 라이브러리 다른 오픈 소스 라이브러리에 따라 달라 집니다.
  * hello [Azure C 공유 유틸리티](https://github.com/Azure/azure-c-shared-utility) 몇몇 Azure 관련 C Sdk에 필요한 기본 작업 (예: 문자열, 목록 조작 및 IO)에 대 한 공통 기능을 제공 하는 라이브러리입니다.
  * hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) AMQP 리소스 제한 된 장치에 대해 최적화를 구현 하는 클라이언트 쪽 라이브러리에 있습니다.
  * hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) hello MQTT 프로토콜을 구현 하는 일반적인 용도의 라이브러리 및 리소스 제한 된 장치에 대해 최적화 하는 라이브러리입니다.

이러한 라이브러리의 용도는 예제 코드를 살펴보면 쉽게 toounderstand입니다. 다음 섹션 hello hello SDK에에서 포함 된 hello 예제 응용 프로그램의 여러 과정을 안내 합니다. 이 연습에서는 좋은 회원님 hello에 대 한 SDK hello 및 Api 작동 하는 소개 toohow hello의 hello 아키텍처 계층의 다양 한 기능을 제공 해야 합니다.

## <a name="before-you-run-hello-samples"></a>Hello 샘플을 실행 하기 전에

C에 대 한 hello Azure IoT 장치 SDK에서에서 hello 샘플을 실행할 수 있습니다, 전에 해야 [hello IoT 허브 서비스의 인스턴스를 만들고](iot-hub-create-through-portal.md) Azure 구독에 있습니다. 그런 다음 작업을 수행 하는 hello를 완료 합니다.

* 개발 환경 준비
* 장치 자격 증명 가져오기

### <a name="prepare-your-development-environment"></a>개발 환경 준비

패키지는 일반적인 플랫폼 (예: Windows 용 NuGet 또는 apt_get Debian 및 Ubuntu)에 대 한 제공 됩니다 및 hello 샘플 사용 가능한 경우 이러한 패키지를 사용 합니다. 일부 경우에 또는 장치에 대 한 toocompile hello SDK 해야 합니다. Toocompile hello SDK 필요한 경우 참조 [개발 환경을 준비](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) hello GitHub 리포지토리에 합니다.

tooobtain hello 샘플 응용 프로그램 코드를 다운로드 hello GitHub에서 SDK의 복사본입니다. Hello에서 hello 소스의 사본을 가져옵니다 **마스터** hello의 분기 [GitHub 리포지토리](https://github.com/Azure/azure-iot-sdk-c)합니다.


### <a name="obtain-hello-device-credentials"></a>Hello 장치 자격 증명을 가져옵니다

Hello 샘플 소스 코드를가지고 hello 다음 일 toodo tooget 장치 자격 증명 집합은 합니다. 장치 toobe 수 tooaccess IoT hub 먼저 hello 장치 toohello IoT Hub id 레지스트리에 추가 해야 합니다. 장치를 추가할 때 필요한 hello 장치 toobe 수 tooconnect toohello IoT 허브에 대 한 장치 자격 증명 집합을 가져옵니다. hello 다음 섹션에서 설명 하는 hello 샘플 응용 프로그램의 hello 형태로 이러한 자격 증명을 예상는 **장치 연결 문자열**합니다.

IoT hub를 관리 하는 여러 오픈 소스 도구 toohelp 가지가 있습니다.

* [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)라는 Windows 응용 프로그램
* [iothub-explorer](https://github.com/azure/iothub-explorer)라는 플랫폼 간 node.js CLI 도구

이 자습서에서는 그래픽 hello *장치 탐색기* 도구입니다. Hello를 사용할 수도 있습니다 *iothub 탐색기* toouse CLI 도구를 선호 하는 경우 도구입니다.

hello 장치 탐색기 도구 IoT 허브에 장치를 추가 하는 등에서 hello Azure IoT 서비스 라이브러리 tooperform 다양 한 함수를 사용 합니다. Hello 장치 탐색기 도구 tooadd 장치를 사용 하는 경우 장치에 대 한 연결 문자열을 가져옵니다. 이 연결 문자열 toorun hello 예제 응용 프로그램에 필요합니다.

Hello 장치 탐색기 도구로 잘 모르는 경우에 절차를 수행 하는 hello 설명 어떻게 toouse 것 tooadd 장치 및 장치 연결 문자열을 가져옵니다.

tooinstall hello 장치 탐색기 도구 참조 [IoT Hub 장치에 대 한 toouse 장치 탐색기 hello 어떻게](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)합니다.

Hello 프로그램을 실행 하면이 인터페이스를 볼 수 있습니다.

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

입력 프로그램 **IoT 허브 연결 문자열** hello에 먼저 필드를 클릭 **업데이트**합니다. 이 단계에서는 IoT Hub와 통신할 수 있도록 hello 도구를 구성 합니다.

Hello IoT 허브 연결 문자열이 구성 된 경우 클릭 hello **관리** 탭:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

이 탭은 IoT 허브에 등록 된 hello 장치를 관리할 수 있습니다.

Hello를 클릭 하 여 장치를 만들면 **만들기** 단추입니다. 미리 채워진 키 집합(기본 및 보조)을 포함한 대화 상자가 표시됩니다. **장치 ID**를 입력한 다음 **만들기**를 클릭합니다.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Hello 장치를 만들면 hello 장치 하나 방금 만든 hello를 포함 하 여 모든 hello 등록 된 장치와 업데이트를 나열 합니다. 새 장치를 마우스 오른쪽 단추로 클릭하면 다음 메뉴가 표시됩니다.

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

선택 하면 **선택한 장치에 대 한 연결 문자열을 복사**, hello 장치 연결 문자열은 복사한 toohello 클립보드 합니다. Hello 장치 연결 문자열의 복사본을 유지 합니다. 경우에 필요한 hello 다음 섹션에에서 설명 된 hello 샘플 응용 프로그램을 실행 합니다.

위의 hello 단계를 완료 하면 일부 코드를 실행 하는 준비 toostart 것입니다. 두 샘플 tooenter 연결 문자열 수 있도록 하는 hello 주 소스 파일의 hello top에 상수를 포함 합니다. 예를 들어 hello에서 해당 줄을 hello **iothub\_클라이언트\_샘플\_mqtt** 응용 프로그램에는 다음과 같이 표시 됩니다.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Hello IoTHubClient 라이브러리 사용

Hello 내 **iothub\_클라이언트** 폴더 hello에 [azure iot-sdk c](https://github.com/azure/azure-iot-sdk-c) 저장소는는 **샘플** 를호출하는응용프로그램이포함된폴더**iothub\_클라이언트\_샘플\_mqtt**합니다.

Windows 버전의 hello hello **iothub\_클라이언트\_샘플\_mqtt** 응용 프로그램에 따라 Visual Studio 솔루션 hello:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Visual Studio 2017에서이 프로젝트를 열면 hello 프롬프트 tooretarget hello 프로젝트 toohello 최신 버전을 수락 합니다.

이 솔루션에는 다음의 단일 프로젝트가 포함됩니다. 이 솔루션에 설치되어 있는 4개의 NuGet 패키지는 다음과 같습니다.

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Hello 항상 필요한 **Microsoft.Azure.C.SharedUtility** 패키지 hello SDK 사용 하 여 작업할 때. 이 샘플에서는 hello MQTT 프로토콜, 따라서 hello를 포함 해야 **Microsoft.Azure.umqtt** 및 **Microsoft.Azure.IoTHub.MqttTransport** (해당 하는 패키지가 있습니다 AMQP 및 HTTP에 대 한 패키지 ). Hello 샘플 hello를 사용 하기 때문에 **IoTHubClient** 라이브러리 hello 포함 해야 **Microsoft.Azure.IoTHub.IoTHubClient** 솔루션의 패키지를 합니다.

Hello hello 샘플 응용 프로그램에 대 한 hello 구현을 찾을 수 있습니다 **iothub\_클라이언트\_샘플\_mqtt.c** 소스 파일입니다.

hello 다음 단계 사용 하 여이 샘플 응용 프로그램 toowalk toouse hello는 데 필요한 작업을 통해 있습니다 **IoTHubClient** 라이브러리입니다.

### <a name="initialize-hello-library"></a>Hello 라이브러리를 초기화 합니다.

> [!NOTE]
> Hello 라이브러리와 함께 작업을 시작 하기 전에 일부 플랫폼 특정 초기화 tooperform를 할 수 있습니다. 예를 들어 linux toouse AMQP를 사용 하려는 경우 hello OpenSSL 라이브러리를 초기화 해야 합니다. hello에 대 한 샘플 hello [GitHub 리포지토리](https://github.com/Azure/azure-iot-sdk-c) hello 유틸리티 함수를 호출 **플랫폼\_init** 클라이언트 시작 hello 시점과 hello 호출 **플랫폼\_deinit**  종료 하기 전에 함수입니다. 이러한 함수는 hello platform.h 헤더 파일에 선언 됩니다. Hello에 대상 플랫폼에 대 한 이러한 함수의 hello 정의 검사할 [리포지토리](https://github.com/Azure/azure-iot-sdk-c) toodetermine 해야 하는지 여부 tooinclude 모든 플랫폼 관련 초기화 코드가 클라이언트에서.

먼저 toostart hello 라이브러리 작업 IoT 허브 클라이언트 핸들을 할당 합니다.

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Hello 장치 탐색기 도구 toothis 함수에서 얻을 hello 장치 연결 문자열의 복사본을 전달 합니다. Hello 통신 프로토콜 toouse를 지정할 수도 있습니다. 이 예제에서는 MQTT를 사용하지만 AMQP와 HTTP도 옵션입니다.

유효한 설치한 경우 **IOTHUB\_클라이언트\_처리**, hello Api toosend 호출을 시작 하 고 메시지 tooand IoT 허브에서 받을 수 있습니다.

### <a name="send-messages"></a>메시지 보내기

hello 샘플 응용 프로그램 루프 toosend 메시지 tooyour IoT 허브를 설정합니다. 다음 코드 조각 hello:

- 메시지를 만듭니다.
- 속성 toohello 메시지를 추가합니다.
- 메시지를 보냅니다.

먼저, 메시지를 만듭니다.

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

메시지를 보낼 때마다 hello 데이터를 보낼 때 호출 되는 참조 tooa 콜백 함수를 지정 합니다. 이 예제에서는 hello 콜백 함수가 호출 될 **SendConfirmationCallback**합니다. 다음 코드 조각 hello이 콜백 함수를 보여 줍니다.

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Hello 호출 toohello 참고 **IoTHubMessage\_Destroy** hello 메시지와 함께 완료 되 면 작동 합니다. 이 함수는 hello 메시지를 만들 때 할당 된 hello 리소스를 해제 합니다.

### <a name="receive-messages"></a>메시지 받기

메시지 수신은 비동기 작업입니다. 첫째, hello 장치 메시지를 받을 때 hello 콜백 tooinvoke를 등록 합니다.

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

hello 마지막 매개 변수는 void 포인터 toowhatever 원하는입니다. Hello 샘플에서은 포인터 tooan 정수 이지만 포인터 tooa 수도 더 복잡 한 데이터 구조입니다. 이 매개 변수는이 함수의 호출자 hello와 공유 상태에 콜백 함수 toooperate hello를 사용 합니다.

Hello 장치는 메시지를 받으면 hello 등록 된 콜백 함수가 호출 됩니다. 이 콜백 함수에서 검색하는 항목은 다음과 같습니다.

* hello 메시지 id와 hello 메시지에서 상관 관계 id.
* hello 메시지 내용입니다.
* Hello 메시지에서 모든 사용자 지정 속성이 있습니다.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

사용 하 여 hello **IoTHubMessage\_GetByteArray** 함수 tooretrieve hello 메시지를이 예제는 문자열입니다.

### <a name="uninitialize-hello-library"></a>Hello 라이브러리를 초기화 합니다.

때 이벤트 전송을 완료 되 고 메시지를 받을 hello IoT 라이브러리 초기화 수 있습니다. 따라서 toodo hello 함수 호출을 실행 합니다.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

이 호출은 hello에서 이전에 할당 하는 hello 리소스를 확보 **IoTHubClient\_CreateFromConnectionString** 함수입니다.

볼 수 있듯이 쉽게 toosend 이며 hello로 메시지를 받을 **IoTHubClient** 라이브러리입니다. hello 라이브러리 hello 세부 사항을 처리 어떤 프로토콜 toouse를 포함 하 여 IoT 허브와의 통신 (hello hello 개발자의 관점에서 보면이 간단한 구성 옵션).

hello **IoTHubClient** 라이브러리도 tooserialize hello 데이터 장치에서 보내는 방법을 tooIoT 허브 정밀 하 게 제어를 제공 합니다. 경우에 따라 이러한 제어 수준은 장점이 이지만 있고 다른 toobe에 염려 하지 않도록 하는 구현 정보입니다. 경우에 해당 되는 hello 경우 hello를 사용 하 여 고려할 수 있습니다 **serializer** 라이브러리 hello 다음 섹션에 설명 되어 있습니다.

## <a name="use-hello-serializer-library"></a>Hello serializer 라이브러리 사용

개념적으로 hello **serializer** 라이브러리는 hello 상단 **IoTHubClient** hello SDK에에서는 라이브러리입니다. Hello를 사용 하 여 **IoTHubClient** 하지만 IoT Hub와의 통신을 내부 hello에 대 한 라이브러리 hello 개발자에서 메시지 serialization 처리 하는 hello 부담을 제거 하는 모델링 기능을 추가 합니다. 이 라이브러리가 동작하는 방식은 예제를 통해 가장 잘 이해할 수 있습니다.

내부 hello **serializer** hello에서 폴더 [azure iot-sdk c 리포지토리](https://github.com/Azure/azure-iot-sdk-c),이 **샘플** 호출 응용 프로그램이 들어 있는 폴더 **simplesample \_mqtt**합니다. 이 샘플의 hello Windows 버전 hello 다음 Visual Studio 솔루션에 포함 됩니다.

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Visual Studio 2017에서이 프로젝트를 열면 hello 프롬프트 tooretarget hello 프로젝트 toohello 최신 버전을 수락 합니다.

Hello 앞의 예제에서와 마찬가지로이 중 하나에 여러 NuGet 패키지가 포함 됩니다.

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

대부분의 hello 이전 샘플에서 이러한 패키지를 살펴 보았으며 하지만 **Microsoft.Azure.IoTHub.Serializer** 새로운 합니다. 이 패키지는 hello를 사용 하는 경우 필요한 **serializer** 라이브러리입니다.

Hello에서 hello 구현의 hello 샘플 응용 프로그램을 찾을 수 있습니다 **simplesample\_mqtt.c** 파일입니다.

hello 다음 섹션에서는 단계별로 hello이이 샘플의 주요 부분입니다.

### <a name="initialize-hello-library"></a>Hello 라이브러리를 초기화 합니다.

hello로 작업 toostart **serializer** 라이브러리, Api 호출 hello 초기화:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

hello 호출 toohello **serializer\_init** 초기화 hello 기본 라이브러리 및 함수는 한 번만 호출 합니다. Hello를 호출 하는 다음 **IoTHubClient\_LL\_CreateFromConnectionString** 함수 hello와 같이 동일한 API는 hello를 **IoTHubClient** 샘플. 장치 연결 문자열을 설정 하는이 호출 (hello 프로토콜을 선택 하면이 호출 또한은 toouse 원하는). 이 샘플 MQTT hello 전송으로 사용 하 여 하지만 AMQP 나 HTTP 중 사용할 수 없습니다.

마지막으로 hello 호출 **만들기\_모델\_인스턴스** 함수입니다. **WeatherStation** hello 모델의 hello 네임 스페이스 및 **ContosoAnemometer** hello hello 모델 이름입니다. Hello 모델 인스턴스를 만든 후 toostart 메시지 송수신 사용할 수 있습니다. 그러나 어떤 모델은 중요 한 toounderstand 되기 합니다.

### <a name="define-hello-model"></a>Hello 모델 정의

Hello에서 모델 **serializer** 장치 tooIoT 이라는 허브 및 hello 메시지를 보낼 수 있는 hello 메시지를 정의 하는 라이브러리 *동작* hello를 받을 수 있는 언어에서 모델링에 있습니다. Hello와 같이 C 매크로 집합을 사용 하 여 모델을 정의 **simplesample\_mqtt** 샘플 응용 프로그램:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

hello **시작\_네임 스페이스** 및 **끝\_네임 스페이스** 매크로 모두를 인수로 hello 모델의 hello 네임 스페이스를 사용 합니다. 모델 또는 모델 및 모델 hello를 사용 하는 hello 데이터 구조의 hello 정의 임을 이러한 매크로 사이 아무 것도 사용할 수 있습니다.

이 예에서는 **ContosoAnemometer**라는 단일 모델이 있습니다. 이 모델은 두 가지 장치 tooIoT 허브를 보낼 수 있음을 데이터 정의: **DeviceId** 및 **WindSpeed**합니다. 또한 장치에서 수신할 수 있는 세 가지 동작(메시지)으로 **TurnFanOn**, **TurnFanOff** 및 **SetAirResistance**를 정의합니다. 각 데이터 요소에는 형식이 있고, 각 작업에는 이름(필요에 따라 매개 변수 집합)이 있습니다.

hello 데이터와 hello 모델에 정의 된 작업 toosend 메시지 tooIoT 허브를 사용할 수 있으며 전송 toomessages toohello 장치 응답 하는 API 화면을 정의 합니다. 이 모델의 사용은 예제를 통해 가장 잘 이해할 수 있습니다.

### <a name="send-messages"></a>메시지 보내기

hello 모델 정의 hello 데이터 tooIoT 허브를 보낼 수 있습니다. 이 예제에서는 하는 중 하나를 의미 hello hello를 사용 하 여 정의 하는 두 데이터 항목이 **WITH_DATA** 매크로입니다. 여러 단계가 필요한 toosend **DeviceId** 및 **WindSpeed** 값 tooan IoT 허브입니다. hello는 toosend 원하는 tooset hello 데이터를 먼저가:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

hello 앞에서 정의한 모델 하면 tooset hello 값의 멤버를 설정 하 여 한 **구조체**합니다. 다음으로 직렬화 toosend hello 메시지:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

이 코드는 hello 장치-클라우드 tooa 버퍼를 serialize (참조 **대상**). hello 코드에는 다음 hello 호출 **sendMessage** toosend hello 메시지 tooIoT 허브 함수:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


두 번째 toolast 매개 hello **IoTHubClient\_LL\_SendEventAsync** 은 hello 데이터 성공적으로 전송 될 때 호출 되는 참조 tooa 콜백 함수입니다. 다음은 hello 샘플에서 hello 콜백 함수가입니다.

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

hello 두 번째 매개 변수는 포인터 toouser 컨텍스트입니다. 동일한 포인터가 너무 전달 hello**IoTHubClient\_LL\_SendEventAsync**합니다. 이 경우 hello 컨텍스트는 단순한 카운터 있지만 원하는 대로 수 있습니다.

그 toosending 장치-클라우드 메시지는 합니다. hello만 남았습니다 toocover은 어떻게 tooreceive 메시지입니다.

### <a name="receive-messages"></a>메시지 받기

메시지를 받는 메시지 hello에서 작동 하는 toohello 방식 유사 하 게 작동 **IoTHubClient** 라이브러리입니다. 먼저 메시지 호출 함수를 등록합니다.

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

그런 다음 메시지를 받을 때 호출 되는 hello 콜백 함수를 작성 합니다.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

이 코드는 상용구--모든 솔루션에 대 한 동일 hello 했습니다. 이 함수 hello 메시지를 수신 및 라우팅하기 hello 호출을 통해 적절 한 함수 toohello 너무 담당**EXECUTE\_명령**합니다. 이 시점에서 호출 하는 hello 함수 모델의 hello 함수 hello 정의에 따라 달라 집니다.

필요 하면 모델에서 동작을 정의할 때 tooimplement 장치 hello 해당 메시지를 받을 때 호출 되는 함수입니다. 예를 들어 모델에서 다음 동작을 정의하는 경우:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

다음 서명을 사용하는 함수를 정의합니다.

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Note hello 함수 hello 이름을 hello 모델의 액션에 hello의 hello 이름 일치 방법을 아니며 hello 함수의 hello 매개 변수 hello 동작에 대 한 지정 된 hello 매개 변수과 일치 합니다. hello 첫 번째 매개 변수는 항상 있어야 및 모델의 포인터 toohello 인스턴스를 포함 합니다.

Hello 장치가이 시그니처와 일치 하는 메시지를 받을 때 hello 해당 함수가 호출 됩니다. tooinclude hello 상용구 코드 외에도 따라서 **IoTHubMessage**, 메시지를 받는 과정은 모델에 정의 된 각 동작에 대 한 간단한 함수를 정의 합니다.

### <a name="uninitialize-hello-library"></a>Hello 라이브러리를 초기화 합니다.

데이터를 전송 하 고 맞아 고 때는 메시지를 받을 hello IoT 라이브러리 초기화 수 있습니다.

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

이러한 세 가지 함수는 각각 hello 세 초기화 함수 앞에서 설명한으로 맞춥니다. 이러한 API를 호출하면 이전에 할당된 리소스를 해제합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 hello에서 hello 라이브러리를 사용 하 여 hello 기본적인 **C에 대 한 Azure IoT 장치 SDK**합니다. 충분 한 정보 toounderstand hello SDK의 아키텍처 및 tooget 시작 샘플 Windows hello를 사용 하는 방법에 포함 된 항목을 집니까 있습니다. hello 다음 기사를 설명 하 여 hello SDK에 대 한 hello 설명을 계속 [hello IoTHubClient 라이브러리에 대 한 자세한](iot-hub-device-sdk-c-iothubclient.md)합니다.

IoT 허브에 대 한 개발에 대 한 더 toolearn 참조 hello [Azure IoT Sdk][lnk-sdks]합니다.

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
