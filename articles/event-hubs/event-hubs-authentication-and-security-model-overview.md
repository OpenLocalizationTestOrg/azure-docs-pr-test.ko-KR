---
title: "Azure 이벤트 허브 인증 및 보안 모델의 aaaOverview | Microsoft Docs"
description: "이벤트 허브 인증 및 보안 모델 개요"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>이벤트 허브 인증 및 보안 모델 개요
hello Azure 이벤트 허브 보안 모델 hello 요구 사항을 준수를 충족 합니다.

* 유효한 자격 증명을 제공 하는 유일한 클라이언트 tooan 이벤트 허브 데이터를 보낼 수 있습니다.
* 클라이언트는 다른 클라이언트를 가장할 수 없습니다.
* 악의적인 클라이언트가 tooan 이벤트 허브 데이터를 보내지 못하도록 차단할 수 있습니다.

## <a name="client-authentication"></a>클라이언트 인증
hello 이벤트 허브 보안 모델은의 조합에 따라 [공유 액세스 서명 (SAS)](../service-bus-messaging/service-bus-sas.md) 토큰 및 *이벤트 게시자*합니다. 이벤트 게시자는 이벤트 허브에 대한 가상 끝점을 정의합니다. hello 게시자에 사용 되는 toosend 메시지 tooan 이벤트 허브 수만 있습니다. 게시자에서 가능한 tooreceive 메시지는 없습니다.

일반적으로 이벤트 허브에서는 클라이언트당 하나의 게시자를 사용합니다. 이벤트 허브의 hello 게시자 tooany 보내지는 모든 메시지는 해당 이벤트 허브 내에서 큐에 대기 된 합니다. 게시자는 세분화된 액세스 제어 및 제한을 사용하도록 설정합니다.

각 이벤트 허브 클라이언트에는 업로드 된 toohello 클라이언트는 고유한 토큰이 할당 됩니다. hello 토큰 생성 되어 각 고유 토큰이 액세스 tooa 다른 고유 게시자에 게 부여 합니다. 토큰을 소유 하는 클라이언트 tooone 게시자 하지만 다른 게시자에만 보낼 수 있습니다. 여러 클라이언트 공유 hello 동일한 토큰을 다음 각각의 경우 게시자를 공유 합니다.

권장 되지는 않지만 tooan 이벤트 허브에 직접 액세스를 허용 하는 토큰을 사용 하 여 가능한 tooequip 장치 됩니다. 이 토큰을 보유하는 모든 장치는 해당 이벤트 허브에 직접 메시지를 보낼 수 있습니다. 이러한 장치는 주체 toothrottling 되지 않습니다. 또한 hello 장치 toothat 이벤트 허브를 보내지 못하도록 차단할 수 없습니다.

모든 토큰은 SAS 키로 서명됩니다. Hello로 모든 토큰 서명 일반적으로 동일한 키입니다. 클라이언트는 hello 키; 인식 하지 않습니다. 따라서 다른 클라이언트를 토큰을 생성할 수 없습니다.

### <a name="create-hello-sas-key"></a>Hello SAS 키 만들기

Hello 서비스 라는 256 비트 SAS 키를 생성 한 이벤트 허브 네임 스페이스를 만들 때 **RootManageSharedAccessKey**합니다. 이 키 부여, 수신 대기, 보내고 권한 toohello 네임 스페이스를 관리 합니다. 추가 키를 만들 수도 있습니다. 부여 권한을 toohello 특정 이벤트 허브를 송신 하는 키를 생성 하는 것이 좋습니다. 이 항목의 나머지 hello 인 것으로 가정이 키 라는 **EventHubSendKey**합니다.

다음 예제는 hello hello 이벤트 허브를 만들 때 송신 전용 키를 만듭니다.

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>토큰 생성

Hello SAS 키를 사용 하 여 토큰을 생성할 수 있습니다. 클라이언트당 하나의 토큰만 생성해야 합니다. 메서드를 다음 hello를 사용 하 여 토큰을 생성할 수 있습니다. 모든 토큰 hello를 사용 하 여 생성 된 **EventHubSendKey** 키입니다. 각 토큰에는 고유한 URI가 할당됩니다.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Hello URI로 지정 해야이 메서드를 호출할 때 `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`합니다. 모든 토큰에 대 한 hello URI는 hello 제외 동일 `PUBLISHER_NAME`, 각 토큰에 대 한 달라 야 합니다. 이상적으로 `PUBLISHER_NAME` 나타냅니다 hello 해당 토큰을 수신 하는 hello 클라이언트의 ID입니다.

이 메서드는 다음 구조 hello로 토큰을 생성 합니다.

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

hello 토큰 만료 시간은 1970 년 1 월 1 일에서 초에 지정 됩니다. hello 다음은 토큰의 예입니다.

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

일반적으로 hello 토큰 수명은 수명과 비슷하거나 hello 클라이언트 hello 수명입니다. 클라이언트 hello에 hello 기능 tooobtain 새 토큰 수명이 짧은 토큰을 사용할 수 있습니다.

### <a name="sending-data"></a>데이터 전송
Hello 토큰을 만든 후에 각 클라이언트와 고유한 토큰이 프로 비전 됩니다.

Hello 클라이언트가 이벤트 허브로 데이터 보내면 hello 토큰으로 보내기 요청을 태그 합니다. tooprevent hello 토큰, hello 클라이언트와 hello 이벤트 허브 간의 hello 통신을 알아 내 도용는 공격자가 암호화 된 채널을 통해 수행 되어야 합니다.

### <a name="blacklisting-clients"></a>클라이언트 차단 목록
공격자가 토큰을 도용 hello 공격자는 도용 토큰 인 hello 클라이언트를 가장할 수 있습니다. 클라이언트를 차단할 경우 해당 클라이언트는 다른 게시자를 사용하는 새 토큰을 수신할 때까지 사용할 수 없게 됩니다.

## <a name="authentication-of-back-end-applications"></a>백 엔드 응용 프로그램의 인증

이벤트 허브 이벤트 허브 클라이언트에서 생성 된 hello 데이터를 사용 하는 tooauthenticate 백 엔드 응용 프로그램은 서비스 버스 주제에 사용 되는 비슷한 toohello 모델 하는 보안 모델을 사용 합니다. 이벤트 허브 소비자 그룹에 해당 하는 tooa 구독 tooa 서비스 버스 항목입니다. 클라이언트는 hello 요청 toocreate hello 소비자 그룹은 관리 hello 이벤트 허브에 대 한 권한을 허용 하거나 hello 이벤트 허브 네임 스페이스 toowhich hello에 대 한 속한 토큰으로과 함께 사용 하는 경우 소비자 그룹을 만들 수 있습니다. 클라이언트는 소비자 그룹에서 tooconsume 데이터 hello 요청을 수신 하는 경우 토큰이 포함 되어는 부여 수신 해당 소비자 그룹에 대 한 권한, hello 이벤트 허브 또는 hello 네임 스페이스 toowhich hello 이벤트 허브 속한 허용 됩니다.

서비스 버스의 hello 현재 버전은 개별 구독에 대 한 SAS 규칙을 지원 하지 않습니다. 이벤트 허브 소비자 그룹에 대 한 페더레이션 번호입니다. SAS는 hello 앞의 두 기능에 대 한 추가 됩니다.

개별 소비자 그룹에 대 한 SAS 인증 hello 없는 경우, 공용 키로 SAS 키 toosecure에 소비자 그룹을 모두 사용할 수 있습니다. 이 방법을 응용 프로그램 tooconsume 데이터를 사용 하 여 이벤트 허브의 hello 소비자 그룹 중 하나를 사용 하면 됩니다.

## <a name="next-steps"></a>다음 단계
이벤트 허브에 대해 자세히 toolearn 방문 hello 다음 항목:

* [이벤트 허브 개요]
* [공유 액세스 서명 개요]
* [Event Hubs를 사용하는 샘플 응용 프로그램]

[이벤트 허브 개요]: event-hubs-what-is-event-hubs.md
[Event Hubs를 사용하는 샘플 응용 프로그램]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[공유 액세스 서명 개요]: ../service-bus-messaging/service-bus-sas.md

