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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="6c3a9-103">어떻게 toolog 이벤트 tooAzure Azure API 관리에서 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="6c3a9-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="6c3a9-104">Azure 이벤트 허브는 확장성이 높은 데이터 수신 서비스를 처리 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있도록 수백만 개의 이벤트 초당 수집 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="6c3a9-105">이벤트 허브는 이벤트 파이프라인에 대 한 "프런트 도어" hello 역할 하며 전환 하 여 이벤트 허브로 데이터 수집 되 면 및 모든 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용 하 여 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="6c3a9-106">이벤트 허브 이벤트 소비자 일정에 따라 hello 이벤트에 액세스할 수 있도록 이러한 이벤트의 hello 소비에서 이벤트 스트림 hello 생산을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="6c3a9-107">이 문서는 도우미 toohello [Azure API 관리 이벤트 허브와 통합](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) 비디오에 대해 설명 하 고 어떻게 Azure 이벤트 허브를 사용 하 여 toolog API 관리 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="6c3a9-108">Azure 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="6c3a9-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="6c3a9-109">새 이벤트 허브 로그인 toohello toocreate [Azure 클래식 포털](https://manage.windowsazure.com) 클릭 **새로**->**응용 프로그램 서비스**->**서비스 버스**  -> **이벤트 허브**->**빨리 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="6c3a9-110">이벤트 허브 이름, 지역을 입력하고 구독을 선택한 후 네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="6c3a9-111">네임 스페이스를 이전에 만든 하지 않은 경우 hello에 이름을 입력 하 여 하나를 만들 수 있습니다 **Namespace** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="6c3a9-112">모든 속성 구성 되 면 클릭 **새 이벤트 허브를 만들** toocreate hello 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![이벤트 허브 만들기][create-event-hub]

<span data-ttu-id="6c3a9-114">다음으로 toohello 이동 **구성** 새 이벤트 허브에 대 한 탭을 두 개 만든 **공유 액세스 정책의**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="6c3a9-115">Hello를 첫 번째 이름 **보내는** 하 고 **보낼** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![전송 정책][sending-policy]

<span data-ttu-id="6c3a9-117">Hello 두 번째 식 이름을 **수신**, 연습해 **수신** 권한과 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![수신 정책][receiving-policy]

<span data-ttu-id="6c3a9-119">각 공유 액세스 정책 응용 프로그램 toosend 있으며 이벤트 tooand hello 이벤트 허브에서에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="6c3a9-120">이러한 정책에 대 한 tooaccess hello 연결 문자열 이동 toohello **대시보드** 탭을 클릭 하 고 hello 이벤트 허브의 **연결 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![연결 문자열][event-hub-dashboard]

<span data-ttu-id="6c3a9-122">hello **보내는** , 이벤트를 기록할 때 연결 문자열이 사용 됩니다 하 고 hello **수신** hello 이벤트 허브에서에서 이벤트를 다운로드할 때 연결 문자열이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![연결 문자열][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="6c3a9-124">API 관리 로거 만들기</span><span class="sxs-lookup"><span data-stu-id="6c3a9-124">Create an API Management logger</span></span>
<span data-ttu-id="6c3a9-125">Hello 다음 단계는 tooconfigure 이벤트 허브를가지고 [로 거](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) API 관리에서 서비스에 이벤트 toohello 이벤트 허브를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="6c3a9-126">API 관리로 거 hello를 사용 하 여 구성 된 [API 관리 REST API](http://aka.ms/smapi)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="6c3a9-127">를 사용 하기 전에 hello REST API hello에 대 한 처음으로 hello 검토 [필수 구성 요소](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) 있는지 확인 하 고 [액세스 toohello REST API를 사용 하도록 설정](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="6c3a9-128">로 거를 toocreate URL 템플릿을 다음 hello를 사용 하 여 HTTP PUT 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="6c3a9-129">대체 `{your service}` 해당 API 관리 서비스 인스턴스에의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="6c3a9-130">대체 `{new logger name}` hello 새 사용자로 거에 대해 원하는 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="6c3a9-131">Hello를 구성할 때이 이름을 참조 하 게 됩니다 [로그-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) 정책</span><span class="sxs-lookup"><span data-stu-id="6c3a9-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="6c3a9-132">Hello toohello 요청 헤더를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="6c3a9-133">콘텐츠 형식 : 응용 프로그램/json</span><span class="sxs-lookup"><span data-stu-id="6c3a9-133">Content-Type : application/json</span></span>
* <span data-ttu-id="6c3a9-134">권한 부여 : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="6c3a9-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="6c3a9-135">Hello 생성에 대 한 지침은 `SharedAccessSignature` 참조 [Azure API 관리 REST API 인증](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="6c3a9-136">서식 파일을 다음 hello를 사용 하 여 hello 요청 본문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-136">Specify hello request body using hello following template.</span></span>

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

* <span data-ttu-id="6c3a9-137">`type`너무 설정 되어 있어야`AzureEventHub`합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="6c3a9-138">`description`hello로 거에 대 한 설명을 제공 하 고 원하는 경우 길이가 0 인 문자열이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="6c3a9-139">`credentials`hello 포함 `name` 및 `connectionString` Azure 이벤트 허브의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="6c3a9-140">Hello로 거를의 상태 코드를 만드는 경우 hello 요청을 수행할 때 `201 Created` 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3a9-141">다른 가능한 반환 코드 및 해당 이유의 경우 [로거 만들기](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="6c3a9-142">목록, update 및 delete hello 참조와 같은 방법을 다른 작업을 수행할 toosee [로 거](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) 엔터티 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="6c3a9-143">log-to-eventhubs 정책 구성</span><span class="sxs-lookup"><span data-stu-id="6c3a9-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="6c3a9-144">사용자로 거 API 관리에서 구성 되 면 로그-eventhubs 정책 toolog hello 원하는 이벤트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="6c3a9-145">hello 로그-eventhubs 정책에서에서 사용할 수 있습니다 어느 hello hello 아웃 바운드 정책 섹션 또는 인바운드 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="6c3a9-146">정책 tooconfigure 로그인 toohello [Azure 포털](https://portal.azure.com)tooyour API 관리 서비스를 찾아 클릭 **게시자 포털** tooaccess hello 게시자 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![게시자 포털][publisher-portal]

<span data-ttu-id="6c3a9-148">클릭 **정책** hello 왼쪽에 hello API 관리 메뉴에서 원하는 제품 hello 및 API를 선택 하 고 클릭 **정책 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="6c3a9-149">정책 toohello 추가할 예정이 예에서 **에코 API** hello에 **무제한** 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![정책 추가][add-policy]

<span data-ttu-id="6c3a9-151">Hello 커서를 이동 `inbound` 정책 섹션 및 hello 클릭 **로그 tooEventHub** 정책 tooinsert hello `log-to-eventhub` 정책 설명서 템플릿.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![정책 편집기][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="6c3a9-153">대체 `logger-id` hello API 관리로 거 hello 이전 단계에서 구성한의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="6c3a9-154">Hello에 대 한 hello 값으로 문자열을 반환 하는 식을 사용할 수 있습니다 `log-to-eventhub` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="6c3a9-155">이 예제에서 hello 날짜 및 시간, 서비스 이름, 요청 id, ip 주소를 요청 하는, 및 작업 이름을 포함 하는 문자열 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="6c3a9-156">클릭 **저장** toosave hello 정책 구성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="6c3a9-157">저장 되는 즉시 hello 정책 활성 상태 이며 이벤트는 기록 된 toohello 이벤트 허브를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3a9-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c3a9-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c3a9-158">Next steps</span></span>
* <span data-ttu-id="6c3a9-159">Azure 이벤트 허브에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="6c3a9-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="6c3a9-160">Azure 이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="6c3a9-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="6c3a9-161">EventProcessorHost를 사용하여 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="6c3a9-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="6c3a9-162">이벤트 허브 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="6c3a9-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="6c3a9-163">API 관리 및 이벤트 허브 통합에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="6c3a9-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="6c3a9-164">로거 엔터티 참조</span><span class="sxs-lookup"><span data-stu-id="6c3a9-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="6c3a9-165">log-to-eventhub 정책 참조</span><span class="sxs-lookup"><span data-stu-id="6c3a9-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="6c3a9-166">Azure API 관리, 이벤트 허브 및 Runscope를 사용하여 API 모니터링</span><span class="sxs-lookup"><span data-stu-id="6c3a9-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="6c3a9-167">연습 동영상 시청</span><span class="sxs-lookup"><span data-stu-id="6c3a9-167">Watch a video walkthrough</span></span>
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
