---
title: "공유 액세스 서명으로 서비스 버스 인증 aaaAzure | Microsoft Docs"
description: "공유 액세스 서명을 사용한 Azure Service Bus 인증 개요, Azure Service Bus를 사용한 SAS 인증 상세 정보"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>공유 액세스 서명을 사용한 Service Bus 인증

*공유 액세스 서명을* (SAS)는 서비스 버스 메시징에 대 한 hello 기본 보안 메커니즘입니다. 이 문서에서는 SAS을 설명 하 고 작동 하는 방법 toouse 플랫폼 제약 없는 방식으로 합니다.

SAS 인증을 사용 하면 응용 프로그램 tooauthenticate tooService hello 네임 스페이스 또는 메시징 엔터티 (큐 또는 항목)는 특정 권한이 연결 된 hello 구성 된 선택 키를 사용 하 여 버스입니다. 그런 다음이 키 toogenerate 클라이언트 tooauthenticate tooService 버스에 사용할 수 있는 SAS 토큰을 사용할 수 있습니다.

SAS 인증 지원은 Azure SDK 버전 2.0 이상 hello에 포함 됩니다.

## <a name="overview-of-sas"></a>SAS 개요

공유 액세스 서명은 SHA-256 보안 해시 또는 URI에 따른 인증 메커니즘입니다. SAS는 모든 서비스 버스 서비스에서 사용되는 매우 강력한 메커니즘입니다. 실제 사용 시, SAS에는 *공유 액세스 정책*과 *공유 액세스 서명*(*토큰*이라고 부름)의 두 구성 요소가 있습니다.

SAS 인증 서비스 버스에 연결 된 권한으로 서비스 버스 리소스에 대 한 암호화 키 hello 구성을 수행 해야 합니다. 클라이언트 클레임 tooService 버스 리소스에 액세스 한 SAS 토큰을 제공 하 여 합니다. 이 토큰 hello 액세스할 리소스 URI, 구성 되며 hello로 서명 된 expiry 키를 구성 합니다.

Service Bus [릴레이](service-bus-fundamentals-hybrid-solutions.md#relays), [큐](service-bus-fundamentals-hybrid-solutions.md#queues) 및 [토픽](service-bus-fundamentals-hybrid-solutions.md#topics)에 대해 공유 액세스 서명 권한 부여 규칙을 구성할 수 있습니다 

SAS 인증 요소 다음 hello를 사용 합니다.

* [공유 액세스 권한 부여 규칙](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): Base64 표현에서 256비트 기본 암호화 키, 선택적 보조키 및 키 이름과 관련된 권한입니다(*수신*, *보내기* 또는 *관리* 권한의 컬렉션).
* [공유 액세스 서명](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) 토큰: hello에 액세스 하는 hello 리소스의 URI로 구성 된 리소스 문자열의 hmac-sha256 hello와 expiry로 hello 암호화 키로 사용 하 여 생성 합니다. hello 서명 및 hello 다음 섹션에에서 설명 된 기타 요소가 문자열 tooform hello SAS 토큰에 형식이 지정 됩니다.

## <a name="shared-access-policy"></a>공유 액세스 정책

SAS에 대 한 중요 한 사항은 toounderstand는 정책과 시작 됨입니다. 각각의 정책에 대해 **이름**, **범위** 및 **권한** 등, 3가지 정보를 결정합니다. hello **이름** 해당;은 해당 범위 내에서 고유한 이름입니다. hello 범위는 아주 쉽게: 문제의 hello 리소스의 URI hello의 합니다. 서비스 버스 네임 스페이스에 대 한 hello 범위가 hello 정규화 된 도메인 이름 (FQDN)와 같은 `https://<yournamespace>.servicebus.windows.net/`합니다.

hello 사용할 수 있는 정책에 대 한 권한은 주로 자체 설명 합니다.

* 보내기
* 수신 대기
* 관리

Hello 정책을 만든 후 할당 한 *기본 키* 및 *보조 키*합니다. 이들은 강력한 암호화 키입니다. 항상 hello에 사용할 수-변경 내용이 손실 하지 않거나 해당 누출 [Azure 포털][Azure portal]합니다. 생성 된 hello 키 중 하나를 사용 하 고 언제 든 지 생성 하려면. 그러나를 다시 생성 하거나 hello hello 정책에 기본 키를 변경 하는 경우 여기에서 만든 모든 공유 액세스 서명에 유효 하지 것입니다.

서비스 버스 네임 스페이스를 만들 때 정책을 자동으로 만들어집니다 라는 hello 전체 네임 스페이스 **RootManageSharedAccessKey**,이 정책은 모든 사용 권한을 갖게 하 고 있습니다. **root**로 로그온하지 않아야 합니다. Hello에서 정책을 추가로 만들 수 있습니다 **구성** hello 포털에서 hello 네임 스페이스에 대 한 탭 합니다. 서비스 버스 (네임 스페이스, 큐 등)의 단일 트리 수준 too12 연결 된 정책은 tooit를 하나만 사용할 수 있는 중요 한 toonote 것 합니다.

## <a name="configuration-for-shared-access-signature-authentication"></a>공유 액세스 서명 인증을 위한 구성
Hello를 구성할 수 있습니다 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 서비스 버스 네임 스페이스, 큐 또는 항목에는 규칙입니다. 구성 된 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 서비스 버스 구독은 현재 지원 되지 않지만 toosecure 액세스 toosubscriptions 네임 스페이스 또는 항목에 구성 된 규칙을 사용할 수 있습니다. 이 절차를 설명 하는 작업 예제에 대 한 참조 hello [공유 액세스 서명 (SAS)를 사용 하 여 인증 서비스 버스 구독을](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) 샘플.

이러한 규칙을 서비스 버스 네임 스페이스, 큐 또는 항목에서 최대 12개까지 구성할 수 있습니다. 서비스 버스 네임 스페이스에 구성 된 규칙에는 해당 네임 스페이스의 tooall 엔터티에 적용 됩니다.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

이 그림에서는 hello *manageRuleNS*, *sendRuleNS*, 및 *listenRuleNS* 권한 부여 규칙 tooboth 큐 Q1 및 항목 t 1 적용 하는 동안 *listenRuleQ*  및 *sendRuleQ* tooqueue q 1을 적용 하 고 *sendRuleT* tootopic T1만 적용 됩니다.

키 매개 변수를 hello는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 다음과 같습니다.

| 매개 변수 | 설명 |
| --- | --- |
| *KeyName* |Hello 권한 부여 규칙을 설명 하는 문자열입니다. |
| *PrimaryKey* |Base64 인코딩 256 비트 기본 키 서명 및 hello SAS 토큰 유효성을 검사 합니다. |
| *SecondaryKey* |base64 인코딩 256 비트 보조 키를 서명 하 고 hello SAS 토큰 유효성을 검사 합니다. |
| *AccessRights* |Hello 권한 부여 규칙에서 허용 된 액세스 권한의 목록입니다. 이러한 권한은 수신, 보내기 및 관리 권한의 컬렉션일 수 있습니다. |

서비스 버스 네임 스페이스를 프로 비전 하는 경우는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)와 [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) 도**RootManageSharedAccessKey**, 기본적으로 생성 됩니다.

## <a name="generate-a-shared-access-signature-token"></a>공유 액세스 서명(토큰) 생성

hello 정책 자체 서비스 버스에 대 한 액세스 토큰 hello 않습니다. Hello는 hello에서 액세스 토큰 생성 된 개체-hello 기본 또는 보조 키 중 하나를 사용 하는 서명 hello 공유 액세스 권한 부여 규칙에 지정 된 키 액세스 toohello 있는 클라이언트는 hello SAS 토큰을 생성할 수 있습니다. hello 토큰 형식에 따라 hello에 문자열을 만들어 신중 하 게 생성 됩니다.

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

여기서 `signature-string` 는 hello 토큰의 hello 범위의 hello sha-256 해시 (**범위** hello 이전 섹션에 설명 된 대로) 추가 CRLF 및 만료 시간 (hello epoch 이후의 초: `00:00:00 UTC` 1970 년 1 월 1에). 

> [!NOTE]
> tooavoid 짧은 토큰 만료 시간 것이 좋습니다 이상는 32 비트 부호 없는 정수 (64 비트) long 정수 또는 가급적 hello 만료 시간 값을 인코딩하는.  
> 
> 

hello 해시 의사 코드 다음 비슷한 toohello 찾아서 32 바이트를 반환 합니다.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

hello에 hello 해시 되지 않은 값은 **SharedAccessSignature** hello 받는 사람을 계산할 수 hello 해시에서 동일한 매개 변수를 반환 하는지 있는지 toobe hello로 동일한 결과 hello 합니다. hello URI hello 범위를 지정 하 고 hello 키 이름 hello 정책 사용 toobe toocompute hello 해시를 식별 합니다. 이것은 보안의 관점에서 중요합니다. Hello 서명이 있는 hello 받는 사람 (서비스 버스)을 계산 하는 일치 하지 않습니다, 액세스가 거부 되었습니다. 이 시점에서 있는지 hello 발신자 액세스 toohello 키를 가지 며 hello 정책에 지정 된 hello 권한을 부여 해야 할 수 있습니다.

Hello를 사용 해야 하는이 작업에 대 한 리소스 URI 인코딩됩니다. hello 리소스 URI는 서비스 버스 리소스 toowhich 액세스 hello의 전체 URI를 요청 하는 hello입니다. 예를 들면 `http://<namespace>.servicebus.windows.net/<entityPath>` 또는 `sb://<namespace>.servicebus.windows.net/<entityPath>`입니다. 즉, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`과 같습니다.

이 URI 또는 계층 구조 부모 중 하나를 지정 하는 hello 엔터티에서 hello 서명에 사용 되는 공유 액세스 권한 부여 규칙 구성 되어야 합니다. 예를 들어 `http://contoso.servicebus.windows.net/contosoTopics/T1` 또는 `http://contoso.servicebus.windows.net` hello 이전 예제에서 합니다.

SAS 토큰은 hello에서 모든 리소스에 대 한 유효 `<resourceURI>` hello에 사용 된 `signature-string`합니다.

hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) hello SAS 토큰 의미 toohello **keyName** 공유 액세스 권한 부여 규칙의 hello toogenerate hello 토큰을 사용 했습니다.

hello *URL로 인코딩된 resourceURI* hello hello 서명의 hello 계산 하는 동안 hello 서명할 문자열에에서 사용 되는 URI와 동일 hello 합니다. [%로 인코딩](https://msdn.microsoft.com/library/4fkewx0t.aspx)되어야 합니다.

주기적으로 다시 생성 하는 hello 키 hello에 사용 되는 것이 좋습니다. [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체입니다. 응용 프로그램에서 일반적으로 hello를 사용 해야 [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate SAS 토큰입니다. Hello 바꿔야 hello 키를 다시 생성할 때는 [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) hello 이전 기본으로 키를 새 기본 키 hello로 새 키를 생성 합니다. 이렇게 하면 이전 기본 키 hello로 가져가기는 아직 만료 되지 않은 및 권한 부여에 대 한 토큰을 사용 하 여 toocontinue 있습니다.

두 hello를 다시 생성할 수는 키가 손상 된 경우 toorevoke hello 키를 있으면 [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) 및 hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) 의 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), 새 키로 대체 하 합니다. 이 절차는 hello 이전 키로 서명한 모든 토큰이 무효화 됩니다.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>어떻게 서비스 버스에 toouse 공유 액세스 서명 인증

다음 시나리오는 hello SAS 토큰 및 클라이언트 권한 부여를 생성, 권한 부여 규칙의 구성을 포함 합니다.

전체에 대 한 hello 구성 및 사용 하 여 SAS 권한 부여를 설명 하는 서비스 버스 응용 프로그램의 작업 예제 참조 [서비스 버스를 통해 공유 액세스 서명 인증](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8)합니다. 네임 스페이스 또는 항목 toosecure 서비스 버스 구독에 구성 된 SAS 권한 부여 규칙의 hello 사용을 보여 주는 관련된 샘플은 여기: [서비스 버스 구독을 사용 하는 공유 액세스 서명 (SAS)를 사용 하 여 인증 ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>네임스페이스에 대한 공유 액세스 권한 부여 규칙 액세스

서비스 버스 네임 스페이스 루트 hello에 대 한 작업에는 인증서 인증이 필요합니다. Azure 구독에 대한 관리 인증서를 업로드해야 합니다. 관리 인증서 tooupload hello 단계에 따라 [여기](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), hello를 사용 하 여 [Azure 포털][Azure portal]합니다. Azure 관리 인증서에 대 한 자세한 내용은 참조 hello [Azure 인증서 개요](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates)합니다.

서비스 버스 네임 스페이스에 대 한 공유 액세스 권한 부여 규칙 액세스를 위한 hello 끝점은 다음과 같습니다.

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 서비스 버스 네임 스페이스에서 개체를 JSON 또는 XML로 serialize 하는 hello 규칙 정보로이 끝점에서 POST 작업을 실행 합니다. 예:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

마찬가지로, hello 네임 스페이스에 구성 된 hello 끝점 tooread hello 권한 부여 규칙에 대 한 GET 작업을 사용 합니다.

tooupdate 또는 특정 권한 부여 규칙을 삭제 hello 다음 끝점을 사용 합니다.

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>엔터티에 대한 공유 액세스 권한 부여 규칙 액세스

에 액세스할 수 있습니다는 [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 에 서비스 버스 큐 또는 항목 hello 통해 구성 된 개체 [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) hello에 대 한 컬렉션 해당 [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) 또는 [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription)합니다.

코드 다음 hello tooadd 권한 부여 규칙 큐에 대 한 방법을 보여 줍니다.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>공유 액세스 서명 권한 부여 사용

서비스 버스.NET 라이브러리 hello와 hello Azure.NET SDK를 사용 하 여 응용 프로그램 hello 통해 SAS 권한 부여 צ ְ ײ [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) 클래스입니다. hello 다음 코드에서는 hello 토큰 공급자 toosend 메시지 tooa 서비스 버스 큐의 hello 사용.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

또한 응용 프로그램은 연결 문자열을 수락하는 메서드에 SAS 연결 문자열을 사용하여 인증에 SAS을 사용합니다.

서비스 버스 릴레이 통해 해당 toouse SAS 권한 부여를 hello 서비스 버스 네임 스페이스에 구성 된 SAS 키를 사용할 수 있습니다. Hello 네임 스페이스에 릴레이 명시적으로 만들면 ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 와 [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) 개체를 해당 릴레이 대 한 hello SAS 규칙을 설정할 수 있습니다. 서비스 버스 구독으로 toouse SAS 권한 부여, 항목 또는 서비스 버스 네임 스페이스에 구성 된 SAS 키를 사용할 수 있습니다.

## <a name="use-hello-shared-access-signature-at-http-level"></a>공유 액세스 서명을 hello를 사용 하 여 (HTTP 수준)

배웠으므로 어떻게 toocreate 공유 액세스 서명 서비스 버스의 모든 엔터티에 대 한,는 HTTP POST tooperform 준비:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

이 방식은 모든 항목에 대해 작동한다는 것을 기억하세요. 큐, 토픽, 구독에 대해 SAS를 만들 수 있습니다. 

부여 보낸 사람 또는 클라이언트는 SAS 토큰 hello 키를 직접 부여 되지 하 고 hello 해시 tooobtain를 되돌릴 수 없는 것입니다. 예를 들어 사용자가 액세스할 수 있는 항목 및 액세스 기간을 제어할 수 있습니다. 중요 한 사항은 tooremember는 hello hello 정책에 기본 키를 변경 하면 여기에서 만든 모든 공유 액세스 서명을 무효화 될입니다.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>공유 액세스 서명을 hello를 사용 하 여 (AMQP 수준)

Hello 이전 단원의 toouse 데이터 toohello 서비스 버스 전송에 대 한 HTTP POST 요청으로 SAS 토큰을 hello 하는 방법을 배웠습니다. 서비스 버스에 액세스할 수 아시다시피, 고급 메시지 큐 프로토콜 AMQP ()를 다양 한 시나리오에서 성능상의 이유로 hello 기본 설정 프로토콜 toouse hello를 사용 하 여 합니다. SAS 토큰 사용 하 여 사용 AMQP hello hello 문서에 설명 되어 [AMQP Claim-Based 보안 버전 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) 즉에 시행 중인 초안 오늘 완벽 하 게 Azure에서 지원 되지만 2013 버전부터 합니다.

Toosend 데이터 tooService 버스를 시작 하기 전에 hello 게시자는 AMQP 메시지 tooa 잘 정의 된 AMQP 노드 라는 내부 hello SAS 토큰을 전송 해야 **$cbs** (것 hello 서비스 tooacquire에서 사용 하는 "특별 한" 큐로 파악 하 고 모든 유효성 검사 hello SAS 토큰)입니다. hello 게시자 hello를 지정 해야 **ReplyTo** hello AMQP 메시지 내부의 필드 나타냅니다;이 서비스는 hello에 hello 토큰 유효성 검사 (간단한 요청/회신 패턴 간에 hello 결과 함께 toohello 게시자에 응답 하는 hello 노드 게시자 및 서비스)입니다. 이 회신 노드가 만들어집니다 "hello 즉석에서" hello AMQP 1.0 사양에 설명 된 대로 "원격 노드의 동적 만들기"에 대 한 말입니다. 해당 hello SAS 토큰은 유효을 확인 한 후 hello 게시자 수 앞으로 이동한 다음 toosend 데이터 toohello 서비스를 시작 합니다.

hello 다음 단계 보여 toosend hello를 사용 하 여 AMQP 프로토콜와 SAS 토큰을 hello 하는 방법을 [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) 라이브러리입니다. Hello 공식을 사용할 수 없는 경우에 유용 서비스 버스 SDK (예를 들어 WinRT,.Net Compact Framework,.Net 마이크로 프레임 워크 및 모노) c에서 개발\#합니다. 물론,이 라이브러리는 유용 toohelp 클레임 기반 보안을 이해 "는 HTTP POST 요청 및 hello SAS 토큰 내 보낸된 hello 인증" 헤더) (사용 하는 hello HTTP 수준에서 작동 방식을 본 것 처럼 hello AMQP 수준에서 작동 합니다. AMQP에 대 한 이러한 깊은 지식이 없어도, hello 공식을 사용할 수 있습니다 서비스 버스 SDK.net Framework 응용 프로그램을 수행 하는 합니다.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

hello `PutCbsToken()` 메서드 수신 hello *연결* (AMQP 연결 클래스 인스턴스 hello 제공한 [AMQP.NET Lite 라이브러리](https://github.com/Azure/amqpnetlite))을 나타내는 hello TCP 연결 toohello 서비스와 hello *sasToken* hello SAS 토큰 toosend 된 매개 변수가 있습니다. 

> [!NOTE]
> Hello 연결이 이루어진 반드시 **SASL 인증 메커니즘 설정 tooEXTERNAL** (및 사용자 이름 및 암호로 toosend hello SAS 토큰이 필요 하지 않을 때 사용 되는 기본 일반 하지 hello).
> 
> 

다음으로 hello 게시자 hello SAS 토큰 송수신 hello 서비스에서 hello 회신 (hello 토큰 유효성 검사 결과)에 대 한 두 개의 AMQP 링크를 만듭니다.

hello AMQP 메시지 속성 집합과 간단한 메시지 보다 더 많은 정보가 포함 됩니다. hello SAS 토큰은 hello 메시지 (생성자를 사용 하 여)의 hello 본문입니다. hello **"ReplyTo"** 속성이 hello 수신기 링크 (이름을 변경할 수 있습니다는 원하는 경우 hello 서비스에 의해 동적으로 생성 됩니다) hello 유효성 검사 결과 받기 위한 toohello 노드 이름입니다. hello 마지막 세 응용 프로그램/사용자 지정 속성을 사용 하 여 hello 서비스 tooindicate 종류 있기 tooexecute 연산의 합니다. Hello 되는 hello CBS 초안 사양에서 설명한 것 처럼 **작업 이름** ("put-토큰"), hello **형식의 토큰** (이 경우는 "servicebus.windows.net:sastoken")에 hello 및 **" "hello 대상 그룹의 이름** toowhich hello 토큰 (전체 엔터티 hello)를 적용 합니다.

Hello 보낸 사람 링크 hello SAS 토큰을 보낸 후 hello 게시자 hello 수신기 링크 hello 회신을 읽어야 합니다. hello 회신은 라는 응용 프로그램 속성이 있는 간단한 AMQP 메시지 **"상태 코드"** hello 동일한 값으로 HTTP 상태 코드를 포함할 수 있는 합니다.

## <a name="rights-required-for-service-bus-operations"></a>서비스 버스 작업에 필요한 권한

hello 다음 표에 서비스 버스 리소스에 대 한 다양 한 작업에 필요한 hello 액세스 권한이 있습니다.

| 작업 | 필요한 클레임 | 클레임 범위 |
| --- | --- | --- |
| **네임스페이스** | | |
| 네임스페이스에서 권한 부여 규칙 구성 |관리 |네임스페이스 주소 |
| **서비스 레지스트리** | | |
| 개인 정책 열거 |관리 |네임스페이스 주소 |
| 네임스페이스에서 수신 시작 |수신 대기 |네임스페이스 주소 |
| 네임 스페이스에서 tooa 수신기 메시지 보내기 |보내기 |네임스페이스 주소 |
| **큐** | | |
| 큐 만들기 |관리 |네임스페이스 주소 |
| 큐 삭제 |관리 |유효한 큐 주소 |
| 큐 열거 |관리 |/$Resources/Queues |
| Hello 큐 설명 가져오기 |관리 |유효한 큐 주소 |
| 큐에서 권한 부여 규칙 구성 |관리 |유효한 큐 주소 |
| Toohello 큐로 보내기 |보내기 |유효한 큐 주소 |
| 큐에서 메시지 받기 |수신 대기 |유효한 큐 주소 |
| 중단 또는 미리 보기-잠금 모드에서 hello 메시지를 받은 후 메시지 완료 |수신 대기 |유효한 큐 주소 |
| 나중에 검색에 대한 메시지 연기 |수신 대기 |유효한 큐 주소 |
| 메시지 효력 상실 |수신 대기 |유효한 큐 주소 |
| 메시지 큐 세션과 연결 된 hello 상태 가져오기 |수신 대기 |유효한 큐 주소 |
| 메시지 큐 세션과 연결 된 hello 상태 설정 |수신 대기 |유효한 큐 주소 |
| **항목** | | |
| 토픽 만들기 |관리 |네임스페이스 주소 |
| 항목 삭제 |관리 |유효한 항목 주소 |
| 항목 열거 |관리 |/$Resources/Topics |
| Hello 항목 설명 가져오기 |관리 |유효한 항목 주소 |
| 항목에서 권한 부여 규칙 구성 |관리 |유효한 항목 주소 |
| Toohello 항목 보내기 |보내기 |유효한 항목 주소 |
| **구독** | | |
| 구독 만들기 |관리 |네임스페이스 주소 |
| 구독 삭제 |관리 |../myTopic/Subscriptions/mySubscription |
| 구독 열거 |관리 |../myTopic/Subscriptions |
| 구독 설명 가져오기 |관리 |../myTopic/Subscriptions/mySubscription |
| 중단 또는 미리 보기-잠금 모드에서 hello 메시지를 받은 후 메시지 완료 |수신 대기 |../myTopic/Subscriptions/mySubscription |
| 나중에 검색에 대한 메시지 연기 |수신 대기 |../myTopic/Subscriptions/mySubscription |
| 메시지 효력 상실 |수신 대기 |../myTopic/Subscriptions/mySubscription |
| 항목 세션과 연결 된 hello 상태 가져오기 |수신 대기 |../myTopic/Subscriptions/mySubscription |
| 항목 세션과 연결 된 hello 상태 설정 |수신 대기 |../myTopic/Subscriptions/mySubscription |
| **규칙** | | |
| 규칙 만들기 |관리 |../myTopic/Subscriptions/mySubscription |
| 규칙 삭제 |관리 |../myTopic/Subscriptions/mySubscription |
| 규칙 열거 |관리 또는 수신 |../myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>다음 단계

서비스 버스 메시징에 대 한 더 toolearn hello 다음 항목을 참조 하십시오.

* [서비스 버스 기본 사항](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus 큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md)
* [어떻게 toouse 서비스 버스 큐](service-bus-dotnet-get-started-with-queues.md)
* [어떻게 toouse 서비스 버스 항목 및 구독](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com