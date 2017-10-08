---
title: "c-IoTHubClient aaaAzure IoT 장치 SDK | Microsoft Docs"
description: "어떻게 toouse hello IoTHubClient 라이브러리 C toocreate 장치 앱에 대 한 hello Azure IoT 장치 SDK에서에서 통신 하는 IoT 허브를 사용 합니다."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>C용 Azure IoT 장치 SDK – IoTHubClient에 대한 자세한 정보
hello [먼저 문서](iot-hub-device-sdk-c-intro.md) 이 도입 시리즈 hello에 **C에 대 한 Azure IoT 장치 SDK**합니다. 첫 번째 문서에서 SDK에 두 아키텍처 계층이 있다는 것을 설명했습니다. 기본 hello에는 hello **IoTHubClient** 직접 IoT Hub와의 통신을 관리 하는 라이브러리입니다. 또한 hello **serializer** 라이브러리 빌드의 tooprovide serialization 서비스입니다. 이 문서의 hello에 추가 세부 정보가 제공 됩니다 **IoTHubClient** 라이브러리입니다.

방법을 설명 하는 hello 이전 문서 toouse hello **IoTHubClient** 라이브러리 toosend 이벤트 tooIoT 허브 및 메시지를 수신 합니다. 이 문서 toomore 정확 하 게 관리 하는 방법에 대해 설명 하 여 그 토론을 확장 *때* 보내고 받는 데이터를 소개 하는 toohello **하위 Api**합니다. 또한 설명 합니다 방법을 tooattach 속성 tooevents (및 메시지에서이 검색) hello에 기능을 처리 하는 hello 속성을 사용 하 여 **IoTHubClient** 라이브러리입니다. 마지막으로, 다양 한 방법 toohandle의 추가 설명을 제공 IoT 허브에서 수신 된 메시지입니다.

hello 문서 마지막으로 완료 몇 가지 장치 자격 증명에 대 한 자세한 정보 및 방법 toochange hello hello의 동작을 비롯 한 기타 항목을 다루는 **IoTHubClient** 구성 옵션을 통해.

Hello에서는 **IoTHubClient** SDK 샘플 tooexplain 이러한 항목입니다. Toofollow을 따라 하려는 경우 참조 hello **iothub\_클라이언트\_샘플\_http** 및 **iothub\_클라이언트\_샘플\_amqp** 이러한 예제에 설명 된 3. 모든 hello 다음 섹션에에서 설명 된에 대 한 hello Azure IoT 장치 SDK에에서 포함 된 응용 프로그램입니다.

Hello를 찾을 수 있습니다 [ **C에 대 한 Azure IoT 장치 SDK** ](https://github.com/Azure/azure-iot-sdk-c) hello에 hello API의 GitHub 리포지토리 및 뷰 세부 정보 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)합니다.

## <a name="hello-lower-level-apis"></a>hello 하위 수준 Api
이전 문서 hello hello hello의 기본 동작 설명 **IotHubClient** hello hello 컨텍스트 내에서 **iothub\_클라이언트\_샘플\_amqp** 응용 프로그램입니다. 예를 들어 tooinitialize이이 코드를 사용 하 여 라이브러리를 hello 하는 방법을 설명 합니다.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

에서도이 사용 하 여 toosend 이벤트 함수 호출 하는 방법을 설명 합니다.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

hello 문서는 에서도 tooreceive 콜백 함수를 등록 하 여 메시지 하는 방법을 설명 합니다.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

hello 문서에는 사용 하 여 toofree 리소스 hello 다음과 같은 코드 하는 방법을 보여 주었습니다.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

그러나 이러한 Api의 도우미 함수 tooeach 가지가 있습니다.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

이러한 함수는 모두 hello api 앱 이름에 "LL"를 포함합니다. 을 제외 하면 이러한 각 함수의 hello 매개 변수는 동일한 tootheir 비 LL 함수와는 합니다. 그러나 이러한 함수의 동작 hello 중요 한 차이점 하나에 차이가 있습니다.

호출 하는 경우 **IoTHubClient\_CreateFromConnectionString**, hello 기본 라이브러리 hello 백그라운드에서 실행 하는 새 스레드를 만듭니다. 이 스레드는 IoT Hub로 이벤트 전송 및 메시지 수신을 처리합니다. Hello "LL" Api로 작업 하는 경우 이러한 스레드가 생성 됩니다. hello 백그라운드 스레드가 hello 만들기는 편의 toohello 개발자. 명시적으로 이벤트를 전송 하 고 hello 백그라운드에서 자동으로 수행 됨-IoT 허브에서 메시지를 수신 하는 방법에 대 한 tooworry가 필요는 없습니다. 반면, "LL" Api hello 제어할 수 명시적 IoT Hub와의 통신 필요 합니다.

toounderstand이이 나타낼지, 예를 살펴보겠습니다.

호출 하는 경우 **IoTHubClient\_SendEventAsync**, 실제로 무엇 지정 하는 것 hello 이벤트 버퍼에 있습니다. 백그라운드 스레드를 호출할 때 만든 hello **IoTHubClient\_CreateFromConnectionString** 지속적으로이 버퍼를 모니터링 하 고 데이터 보내는 tooIoT 허브를 포함 합니다. 해당 hello 시간이 hello에 hello 백그라운드에서 이런 주 스레드에서 다른 작업을 수행 합니다.

마찬가지로, 사용 하 여 메시지에 콜백 함수를 등록할 때 **IoTHubClient\_SetMessageCallback**, hello SDK toohave hello 백그라운드 지시 하는 스레드 메시지 hello 콜백 함수를 호출 받은 hello 주 스레드의 독립적입니다.

hello "LL" Api 백그라운드 스레드를 만들지 않습니다. 대신, 새로운 API tooexplicitly 송신 호출 해야 하며 IoT 허브에서 데이터를 수신 합니다. 다음 예제는 hello에서이 확인할 수 있습니다.

hello **iothub\_클라이언트\_샘플\_http** hello SDK에서는에 포함 된 응용 프로그램 hello 하위 Api입니다. 해당 샘플에서 이벤트 tooIoT 허브 hello 다음과 같은 코드로 보냅니다.

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

hello 처음 세 줄 hello 메시지를 만들고 hello 마지막 줄은 hello 이벤트를 보냅니다. 그러나 앞에서 설명한 대로 "보내는" hello 이벤트 의미 hello 데이터는 버퍼에 배치 하기만 하면 됩니다. 호출할 때 hello 네트워크에서 전송 되는 아무 것도 **IoTHubClient\_LL\_SendEventAsync**합니다. 호출 해야 순서 tooactually 수신 hello 데이터 tooIoT 허브, **IoTHubClient\_LL\_DoWork**이 예제와 같이,:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

이 코드 (hello에서 **iothub\_클라이언트\_샘플\_http** 응용 프로그램) 반복 해 서 호출 **IoTHubClient\_LL\_DoWork** . 때마다 **IoTHubClient\_LL\_DoWork** 가 hello 버퍼 tooIoT 허브에서에서 일부 이벤트를 전송 하 고 호출 toohello 장치에 전송 되는 대기 중인된 메시지를 검색 합니다. hello 후자의 경우 즉, 메시지에 대 한 콜백 함수를 등록 했습니다 (모든 메시지는 큐에서 대기 가정) hello 콜백이 호출 합니다. 콜백 함수 hello 다음과 같은 코드로 등록 합니다.

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

hello 이유를 **IoTHubClient\_LL\_DoWork** 일반적으로 라고 보냅니다는 루프를 호출할 때마다는, *일부* tooIoT 이벤트 허브 및 검색 버퍼링*다음 hello* hello 장치에 대 한 큐 메시지입니다. 각 호출에서 버퍼링 toosend 모든 이벤트를 보장 되지 않습니다 구독이 나 모든 tooretrieve 지연 메시지입니다. Toosend hello의 모든 이벤트를 버퍼링 한 후에 다른 처리를 계속 하려는 경우이 루프 hello 다음과 같은 코드로 바꿀 수 있습니다.

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

이 코드는 호출 **IoTHubClient\_LL\_DoWork** hello 버퍼의 모든 이벤트 허브 tooIoT 전송 될 때까지 합니다. 이 또한 대기 상태인 모든 메시지를 수신함을 의미하지 않습니다. Hello 이유의 부분은 결정적 함수로 동작 없습니다 "all 로" 메시지를 확인 합니다. "전체" hello 메시지를 검색 하지만 그런 다음 다른 toohello 장치 전송 되 면 어떻게 될까요 직후? 와 더 나은 방법은 toodeal 프로그래밍 된 제한 시간입니다. 예를 들어 hello 메시지 콜백 함수는 호출 될 때마다 타이머를 초기화할 수 있었습니다. 작성할 수 있습니다 논리 toocontinue 처리 하는 경우, 예를 들어 메시지가 받은 hello에서 마지막 *X* 초입니다.

완성 된 ingressing 이벤트는 및 리소스를 있는지 toocall hello 해당 함수 tooclean 될 메시지를 수신 합니다.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

기본적으로 Api toosend 집합이 하나만 있는 및 백그라운드 스레드 및 다른 집합이 없이 hello 백그라운드 스레드에서 동일한 작업을 hello 않는 Api 사용 하 여 데이터를 수신 합니다. 대부분의 개발자 들은 hello 비-LL Api 것이 적절할 수 있지만 hello 하위 수준 Api는 유용 hello 개발자가 명시적으로 네트워크 전송 제어 하는 경우. 예를 들어, 일부 장치에서 시간에 따라 데이터를 수집하고 지정된 간격(예: 1시간에 한 번, 하루에 한 번)으로만 이벤트를 수신합니다. hello 보내고 IoT 허브에서 데이터를 받을 때 기능이 tooexplicitly 컨트롤 hello 하위 Api 제공 합니다. 다른 사용자를 단순히 선호 hello 단순성 해당 hello 하위 수준 Api를 제공 합니다. Hello 백그라운드에서 몇 가지 작업 발생 하지 않고 hello 주 스레드에서 모든 차이 발생합니다.

어떤 모델을 선택 하면 있는지 toobe 일관 된 Api를 사용 하 여 수 있습니다. 호출 하 여 시작 하는 경우 **IoTHubClient\_LL\_CreateFromConnectionString**만 모든 후속 작업에 대 한 하위 수준 Api에 해당 하는 hello를 사용 해야 합니다.

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

hello 반대도 true 됩니다. 로 시작 하는 경우 **IoTHubClient\_CreateFromConnectionString**, 사용 하 여 추가 처리에 대 한-LL Api 비 hello 합니다.

C에 대 한 hello Azure IoT 장치 SDK에서 참조 hello **iothub\_클라이언트\_샘플\_http** 전체 예제는 hello에 대 한 응용 프로그램 하위 Api입니다. hello **iothub\_클라이언트\_샘플\_amqp** 전체 예를 보려면 hello 비-LL Api에 대 한 응용 프로그램을 참조할 수 있습니다.

## <a name="property-handling"></a>속성 처리
지금까지 데이터 보내기, 제목 때 म 했으므로 언급 toohello hello 메시지 본문입니다. 다음 코드를 예로 들 수 있습니다.

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

이 예제에서는 보냅니다 hello 텍스트 "Hello World."와 메시지 tooIoT 허브 그러나 IoT 허브는 또한 속성 toobe tooeach 연결 된 메시지를 수 있습니다. 속성은 연결 된 toohello 메시지 수 있는 이름/값 쌍입니다. 예를 들어 hello 이전 코드 tooattach 속성 toohello 메시지를 수정할 수 있습니다.

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

호출 하 여 시작 **IoTHubMessage\_속성** 메시지의 hello 핸들을 전달 합니다. 다시에 get는 **지도\_처리** 참조 수 있도록 toostart 속성을 추가 합니다. 후자의 hello를 호출 하 여 수행 됩니다 **지도\_AddOrUpdate**, 참조 tooa 지도 사용 하는\_핸들, hello 속성 이름 및 hello 속성 값입니다. 이 API를 통해 속성을 원하는 만큼 추가할 수 있습니다.

hello 이벤트를 읽을 때 **이벤트 허브**, hello 수신자 hello 속성을 열거 하 고 해당 값을 검색할 수 있습니다. 예를 들어.net에서은 이렇게 hello에 액세스 하 여 [속성 개체의 컬렉션에 hello EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx)합니다.

Hello 이전 예제에서는 속성 tooan 이벤트 허브 tooIoT 받으실를 연결 합니다. 속성에 연결 된 toomessages IoT 허브에서 수신 될 수도 있습니다. 메시지에서 tooretrieve 속성을 원하는 경우 메시지 콜백 함수에 hello 다음과 같은 코드를 사용할 수 있습니다.

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

호출을 너무 hello**IoTHubMessage\_속성** 반환 hello **지도\_처리** 참조 합니다. 그런 다음 전달 참조 하는 너무**지도\_GetInternals** (뿐만 아니라 hello 속성의 개수) tooobtain 참조 tooan 배열을 hello 이름/값 쌍입니다. 해당 시점에 원하는 hello 속성 tooget toohello 값을 열거 하는 간단한 방법

응용 프로그램에서 toouse 속성 필요는 없습니다. 그러나 tooset 해야 할 경우 이벤트에서 검색할 메시지에서 hello 또는 **IoTHubClient** 라이브러리를 사용 합니다.

## <a name="message-handling"></a>메시지 처리
앞서 설명한 것 처럼 메시지가 도착 하면 IoT Hub hello에서 **IoTHubClient** 라이브러리 등록 된 콜백 함수를 실행 하 여 응답 합니다. 이 함수에는 반환 매개 변수가 있으며 이에 대한 추가 설명이 필요합니다. 여기은 hello에 대 한 hello 콜백 함수의 일부 **iothub\_클라이언트\_샘플\_http** 샘플 응용 프로그램:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

반환 형식이 hello는 **IOTHUBMESSAGE\_처리\_결과** 및 경우에 따라 반환 **IOTHUBMESSAGE\_"승인 됨"**합니다. 다른 값을 반환할 수 있습니다이 함수에서 변경 방법 hello **IoTHubClient** toohello 메시지 콜백을 반응 하는 라이브러리입니다. 다음은 hello 옵션입니다.

* **IOTHUBMESSAGE\_"승인 됨"** – hello 메시지를 처리 했습니다. hello **IoTHubClient** 라이브러리 hello 사용 하 여 다시 hello 콜백 함수를 호출 하지 않으므로 동일한 메시지입니다.
* **IOTHUBMESSAGE\_거부 됨** – hello 메시지 처리 되지 않았습니다 고 없습니다 desire toodo에서 미래의 hello는 합니다. hello **IoTHubClient** 라이브러리 hello 사용 하 여 다시 hello 콜백 함수를 호출 하지 않아야 동일한 메시지입니다.
* **IOTHUBMESSAGE\_중단 된** – hello 메시지가 성공적으로 처리 되지 않았습니다. 하지만 hello **IoTHubClient** 라이브러리 hello 사용 하 여 다시 hello 콜백 함수를 호출 해야 동일한 메시지입니다.

Hello에 대 한 처음 두 개의 코드를 반환 hello **IoTHubClient** 라이브러리 hello 메시지를 해당 나타내는 허브 hello 장치 큐에서 삭제 하 고 다시 전달 되지 해야 메시지 tooIoT 보냅니다. hello 한 순수 효과 동일 hello는 (hello 메시지 hello 장치 큐에서 삭제)을 추적 하지만 hello 메시지를 승인 또는 거부 여부는 계속 기록 됩니다.  피드백에 대 한 수신 대기 하 고 장치를 수락 또는 거절 특정 메시지 경우 확인 수 있는 유용한 hello 메시지 toosenders는 이러한 구분을 기록 합니다.

마지막 경우 hello 메시지도 보내집니다 tooIoT 허브에 있지만 해당 hello 메시지를 다시 배달 해야 나타냅니다. 일반적으로 몇 가지 오류가 발생 해도 tootry tooprocess hello 메시지 다시 사용할 경우 메시지를 중단 합니다. 반면, 메시지를 거부 하는 적절 한 복구할 수 없는 오류가 발생 하는 경우 (또는 단순히 tooprocess hello 메시지를 표시 하지 않으려면 결정 한 경우).

어떤 경우 든, 유의 hello 다른 반환 코드의 hello에서 원하는 동작을 hello 소개 수 있도록 **IoTHubClient** 라이브러리입니다.

## <a name="alternate-device-credentials"></a>대체 장치 자격 증명
Hello로 작업 하는 경우 먼저 toodo 앞에서 설명한 대로 hello **IoTHubClient** 라이브러리는 tooobtain는 **IOTHUB\_클라이언트\_처리** hello와 같은 호출 하 여 다음:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

인수를 너무 hello**IoTHubClient\_CreateFromConnectionString** hello 장치 연결 문자열 및 toocommunicate IoT Hub와 사용 하 여 hello 프로토콜을 나타내는 매개 변수입니다. hello 장치 연결 문자열의 형식이 다음과 같이 표시 됩니다.

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

이 문자열에는 IoT Hub 이름, IoT Hub 접미사, 장치 ID 및 공유 액세스 키의 네 가지 정보가 있습니다. Hello Azure 포털에서에서 IoT hub 인스턴스를 만들 때 hello IoT 허브의 정규화 된 도메인 이름 (FQDN)을 가져올-hello IoT 허브 이름 (hello FQDN의 첫 번째 부분 hello) 및 hello IoT 허브 접미사 (hello FQDN의 hello의 나머지 부분)이 제공 합니다. IoT Hub와 장치를 등록할 때 hello 장치 ID와 hello 공유 액세스 키를 받아야 (hello에 설명 된 대로 [이전 문서](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** 는 한 가지 방법은 tooinitialize hello 라이브러리를 제공 합니다. 원하는 경우 새로 만들 수 있습니다는 **IOTHUB\_클라이언트\_처리** hello 장치 연결 문자열 대신 이러한 개별 매개 변수를 사용 하 여 합니다. 이 작업은 코드 다음 hello로 수행 됩니다.

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

이 기능을 수행 hello와 같은 작업 **IoTHubClient\_CreateFromConnectionString**합니다.

Toouse 원하지 확실 해 보일 수 있습니다 **IoTHubClient\_CreateFromConnectionString** 초기화의 더 자세한이 메서드가 아니라 합니다. 하지만 장치를 IoT Hub에 등록할 때 연결 문자열이 아닌, 장치 ID 및 장치 키를 얻게 되는 것을 유의해야 합니다. hello *장치 탐색기* hello에 도입 된 SDK 도구 [이전 문서](iot-hub-device-sdk-c-intro.md) hello에서 라이브러리를 사용 하 여 **Azure IoT 서비스 SDK** 에서 toocreate hello 장치 연결 문자열 hello 장치 ID, 장치 키 및 IoT Hub 호스트 이름입니다. 따라서 호출 **IoTHubClient\_LL\_만들기** 저장 하기 때문에 더 적합할 수 있습니다 hello 단계의 연결 문자열을 생성 합니다. 어떤 것이든 편한 방법을 사용하세요.

## <a name="configuration-options"></a>구성 옵션
Hello 방식으로 hello에 대 한 지금까지 설명한 모든 **IoTHubClient** 라이브러리 works 기본 동작을 반영 합니다. 그러나 toochange hello 라이브러리의 작동 원리를 설정할 수 있는 몇 가지 옵션이 있습니다. Hello를 활용 하 여 이렇게 **IoTHubClient\_LL\_SetOption** API입니다. 다음 예를 살펴보세요.

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

일반적으로 사용되는 몇 가지 옵션이 있습니다.

* **SetBatching** (bool) – 경우 **true**, 전송 되는 데이터 tooIoT 허브 일괄 처리로 보내집니다. **false**이면 메시지가 개별적으로 전송됩니다. hello 기본값은 **false**합니다. 해당 hello 참고 **SetBatching** toohello HTTP 프로토콜 및 하지 toohello MQTT 또는 AMQP 프로토콜 옵션 적용 합니다.
* **Timeout** (unsigned int) – 이 값은 밀리초 단위로 표시됩니다. HTTP 요청 또는 응답을 수신이 시간 보다 오래 걸리는 보내는 경우 hello 연결 시간이 초과 됩니다.

hello 옵션을 일괄 처리 하는 것이 중요 합니다. 기본적으로 라이브러리 ingresses 이벤트를 개별적으로 hello (단일 이벤트는 무엇이 든 전달 너무**IoTHubClient\_LL\_SendEventAsync**). 이 옵션을 일괄 처리 하는 hello **true**, hello 라이브러리 (위쪽 IoT 허브에서 허용할 toohello 최대 메시지 크기) hello 버퍼에서 많은 이벤트를 수집 합니다.  hello 이벤트 일괄 처리 전송 되 tooIoT 허브 단일에서 HTTP 호출 (hello 개별 이벤트는 JSON 배열에 포함 됨). 일괄 처리를 설정하면 네트워크 왕복이 감소되므로 성능상 이점이 상당합니다. 각 개별 이벤트에 대한 헤더 집합이 아닌, 이벤트 일괄 처리가 포함된 한 집합의 HTTP 헤더를 전송하므로 대역폭도 크게 감소합니다. 그렇지 않은 경우 특별 한 이유가 toodo 없다면 일반적으로 해도 좋을 tooenable 일괄 처리입니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 자세히 hello 동작의 hello 설명 **IoTHubClient** hello에 라이브러리를 찾을 **C에 대 한 Azure IoT 장치 SDK**합니다. 이 정보를 통해 hello의 hello 기능에 잘 알고 있어야 **IoTHubClient** 라이브러리입니다. hello [다음 기사](iot-hub-device-sdk-c-serializer.md) hello에 비슷한 세부 정보를 제공 **serializer** 라이브러리입니다.

IoT 허브에 대 한 개발에 대 한 더 toolearn 참조 hello [Azure IoT Sdk][lnk-sdks]합니다.

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
