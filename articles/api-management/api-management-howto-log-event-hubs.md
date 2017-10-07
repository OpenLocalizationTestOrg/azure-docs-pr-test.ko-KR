---
title: "aaaHow toolog 이벤트 tooAzure Azure API 관리에서 이벤트 허브 | Microsoft Docs"
description: "자세한 내용은 방법 toolog 이벤트 tooAzure Azure API 관리에서 이벤트 허브입니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>어떻게 toolog 이벤트 tooAzure Azure API 관리에서 이벤트 허브
Azure 이벤트 허브는 확장성이 높은 데이터 수신 서비스를 처리 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있도록 수백만 개의 이벤트 초당 수집 수입니다. 이벤트 허브는 이벤트 파이프라인에 대 한 "프런트 도어" hello 역할 하며 전환 하 여 이벤트 허브로 데이터 수집 되 면 및 모든 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용 하 여 저장 합니다. 이벤트 허브 이벤트 소비자 일정에 따라 hello 이벤트에 액세스할 수 있도록 이러한 이벤트의 hello 소비에서 이벤트 스트림 hello 생산을 분리 합니다.

이 문서는 도우미 toohello [Azure API 관리 이벤트 허브와 통합](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) 비디오에 대해 설명 하 고 어떻게 Azure 이벤트 허브를 사용 하 여 toolog API 관리 이벤트입니다.

## <a name="create-an-azure-event-hub"></a>Azure 이벤트 허브 만들기
새 이벤트 허브 로그인 toohello toocreate [Azure 클래식 포털](https://manage.windowsazure.com) 클릭 **새로**->**응용 프로그램 서비스**->**서비스 버스**  -> **이벤트 허브**->**빨리 만들기**합니다. 이벤트 허브 이름, 지역을 입력하고 구독을 선택한 후 네임스페이스를 선택합니다. 네임 스페이스를 이전에 만든 하지 않은 경우 hello에 이름을 입력 하 여 하나를 만들 수 있습니다 **Namespace** 텍스트 상자에 붙여넣습니다. 모든 속성 구성 되 면 클릭 **새 이벤트 허브를 만들** toocreate hello 이벤트 허브입니다.

![이벤트 허브 만들기][create-event-hub]

다음으로 toohello 이동 **구성** 새 이벤트 허브에 대 한 탭을 두 개 만든 **공유 액세스 정책의**합니다. Hello를 첫 번째 이름 **보내는** 하 고 **보낼** 사용 권한.

![전송 정책][sending-policy]

Hello 두 번째 식 이름을 **수신**, 연습해 **수신** 권한과 클릭 **저장**합니다.

![수신 정책][receiving-policy]

각 공유 액세스 정책 응용 프로그램 toosend 있으며 이벤트 tooand hello 이벤트 허브에서에서 수신 합니다. 이러한 정책에 대 한 tooaccess hello 연결 문자열 이동 toohello **대시보드** 탭을 클릭 하 고 hello 이벤트 허브의 **연결 정보**합니다.

![연결 문자열][event-hub-dashboard]

hello **보내는** , 이벤트를 기록할 때 연결 문자열이 사용 됩니다 하 고 hello **수신** hello 이벤트 허브에서에서 이벤트를 다운로드할 때 연결 문자열이 사용 됩니다.

![연결 문자열][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>API 관리 로거 만들기
Hello 다음 단계는 tooconfigure 이벤트 허브를가지고 [로 거](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) API 관리에서 서비스에 이벤트 toohello 이벤트 허브를 기록할 수 있습니다.

API 관리로 거 hello를 사용 하 여 구성 된 [API 관리 REST API](http://aka.ms/smapi)합니다. 를 사용 하기 전에 hello REST API hello에 대 한 처음으로 hello 검토 [필수 구성 요소](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) 있는지 확인 하 고 [액세스 toohello REST API를 사용 하도록 설정](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI)합니다.

로 거를 toocreate URL 템플릿을 다음 hello를 사용 하 여 HTTP PUT 요청을 확인 합니다.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* 대체 `{your service}` 해당 API 관리 서비스 인스턴스에의 hello 이름으로 합니다.
* 대체 `{new logger name}` hello 새 사용자로 거에 대해 원하는 이름을 사용 합니다. Hello를 구성할 때이 이름을 참조 하 게 됩니다 [로그-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) 정책

Hello toohello 요청 헤더를 다음을 추가 합니다.

* 콘텐츠 형식 : 응용 프로그램/json
* 권한 부여 : SharedAccessSignature 58...
  * Hello 생성에 대 한 지침은 `SharedAccessSignature` 참조 [Azure API 관리 REST API 인증](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication)합니다.

서식 파일을 다음 hello를 사용 하 여 hello 요청 본문을 지정 합니다.

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* `type`너무 설정 되어 있어야`AzureEventHub`합니다.
* `description`hello로 거에 대 한 설명을 제공 하 고 원하는 경우 길이가 0 인 문자열이 될 수 있습니다.
* `credentials`hello 포함 `name` 및 `connectionString` Azure 이벤트 허브의 합니다.

Hello로 거를의 상태 코드를 만드는 경우 hello 요청을 수행할 때 `201 Created` 반환 됩니다.

> [!NOTE]
> 다른 가능한 반환 코드 및 해당 이유의 경우 [로거 만들기](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT)를 참조하세요. 목록, update 및 delete hello 참조와 같은 방법을 다른 작업을 수행할 toosee [로 거](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) 엔터티 설명서입니다.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>log-to-eventhubs 정책 구성
사용자로 거 API 관리에서 구성 되 면 로그-eventhubs 정책 toolog hello 원하는 이벤트를 구성할 수 있습니다. hello 로그-eventhubs 정책에서에서 사용할 수 있습니다 어느 hello hello 아웃 바운드 정책 섹션 또는 인바운드 정책입니다.

정책 tooconfigure 로그인 toohello [Azure 포털](https://portal.azure.com)tooyour API 관리 서비스를 찾아 클릭 **게시자 포털** tooaccess hello 게시자 포털입니다.

![게시자 포털][publisher-portal]

클릭 **정책** hello 왼쪽에 hello API 관리 메뉴에서 원하는 제품 hello 및 API를 선택 하 고 클릭 **정책 추가**합니다. 정책 toohello 추가할 예정이 예에서 **에코 API** hello에 **무제한** 제품입니다.

![정책 추가][add-policy]

Hello 커서를 이동 `inbound` 정책 섹션 및 hello 클릭 **로그 tooEventHub** 정책 tooinsert hello `log-to-eventhub` 정책 설명서 템플릿.

![정책 편집기][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

대체 `logger-id` hello API 관리로 거 hello 이전 단계에서 구성한의 hello 이름으로 합니다.

Hello에 대 한 hello 값으로 문자열을 반환 하는 식을 사용할 수 있습니다 `log-to-eventhub` 요소입니다. 이 예제에서 hello 날짜 및 시간, 서비스 이름, 요청 id, ip 주소를 요청 하는, 및 작업 이름을 포함 하는 문자열 기록 됩니다.

클릭 **저장** toosave hello 정책 구성을 업데이트 합니다. 저장 되는 즉시 hello 정책 활성 상태 이며 이벤트는 기록 된 toohello 이벤트 허브를 지정 합니다.

## <a name="next-steps"></a>다음 단계
* Azure 이벤트 허브에 대해 자세히 알아보기
  * [Azure 이벤트 허브 시작](../event-hubs/event-hubs-c-getstarted-send.md)
  * [EventProcessorHost를 사용하여 메시지 수신](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [이벤트 허브 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)
* API 관리 및 이벤트 허브 통합에 대해 자세히 알아보기
  * [로거 엔터티 참조](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [log-to-eventhub 정책 참조](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Azure API 관리, 이벤트 허브 및 Runscope를 사용하여 API 모니터링](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>연습 동영상 시청
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
