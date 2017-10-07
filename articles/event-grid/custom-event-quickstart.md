---
title: "Azure 이벤트 표 형태에 대 한 이벤트 aaaCustom | Microsoft Docs"
description: "Toothat 이벤트 구독 및 Azure 이벤트 표 형태 toopublish 항목을 사용 합니다."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="65b66-103">Azure Event Grid로 사용자 지정 이벤트 만들기 및 라우팅</span><span class="sxs-lookup"><span data-stu-id="65b66-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="65b66-104">Azure의 이벤트 표 형태에는 hello 클라우드에 대 한 이벤트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="65b66-105">Hello Azure CLI toocreate 사용자 지정 항목을 사용 하 여이 문서에서는 toohello 항목, 구독 및 hello 이벤트 tooview hello 결과 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="65b66-106">일반적으로 이벤트 tooan 끝점을 webhook 또는 Azure 함수와 같은 toohello 이벤트에 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="65b66-107">그러나 toosimplify이 문서에서는, hello 메시지를 단순히 수집 하는 hello 이벤트 tooa URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="65b66-108">오픈 소스이면서 [RequestBin](https://requestb.in/)이라는 타사 도구를 사용하여 이 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="65b66-109">**RequestBin**은 높은 처리량 사용을 위해 설계되지 않은 오픈 소스 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="65b66-110">순수 하 게 가격은 hello 도구의 여기 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="65b66-111">한 번에 둘 이상의 이벤트를 밀어 넣으면 hello 도구에서 사용자 이벤트를 모두 표시 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="65b66-112">완료 했으면 hello 이벤트 데이터 tooan 끝점 전송 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![이벤트 데이터](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="65b66-114">이 문서 hello Azure CLI의 최신 버전을 실행 되 고 있는지 필요 tooinstall 선택한 hello CLI를 사용 하 여 로컬로 (2.0.14 이상 버전).</span><span class="sxs-lookup"><span data-stu-id="65b66-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="65b66-115">toofind hello 버전을 실행 `az --version`합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="65b66-116">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="65b66-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="65b66-117">Create a resource group</span></span>

<span data-ttu-id="65b66-118">Event Grid 토픽은 Azure 리소스이며 Azure 리소스 그룹에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="65b66-119">hello 리소스 그룹은 리소스는 Azure에 배포 되 고 관리 하는 논리적 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="65b66-120">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="65b66-121">hello 다음 예제에서는 명명 된 리소스 그룹 *gridResourceGroup* hello에 *westus2* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="65b66-122">사용자 지정 토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="65b66-122">Create a custom topic</span></span>

<span data-ttu-id="65b66-123">토픽은 이벤트를 게시하는 사용자 정의 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="65b66-124">hello 다음 예제에서는 hello 항목 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="65b66-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="65b66-125">`<topic_name>`을 토픽의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="65b66-126">DNS 항목으로 표시 되기 때문에 hello 항목 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="65b66-127">이벤트 표 형태 hello 미리 보기 릴리스에 대 한 지원 **westus2** 및 **westcentralus** 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="65b66-128">메시지 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="65b66-128">Create a message endpoint</span></span>

<span data-ttu-id="65b66-129">Toohello 항목, 구독 하기 전에 hello 이벤트 메시지에 대 한 hello 끝점을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="65b66-130">Toorespond toohello 이벤트 코드를 작성 하지 않고 빠르게 검색할 수 있도록 hello 메시지를 수집 하는 끝점을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="65b66-131">RequestBin는 오픈 소스, toocreate 끝점을 사용 하면 타사 도구 및 tooit 전송 되는 요청을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="65b66-132">너무 이동[RequestBin](https://requestb.in/)를 클릭 하 고 **는 RequestBin 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="65b66-133">Toohello 항목 구독할 때 필요 하므로 hello bin URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="65b66-134">Tooa 항목 구독</span><span class="sxs-lookup"><span data-stu-id="65b66-134">Subscribe tooa topic</span></span>

<span data-ttu-id="65b66-135">Tooa 항목 tootell 이벤트 표 형태를 구독 하면 이벤트 tootrack 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="65b66-136">hello 다음 예제에서는 구독 toohello 항목을 생성 하 고 이벤트 알림에 대 한 hello 끝점으로 RequestBin hello URL 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="65b66-137">대체 `<event_subscription_name>` 구독에 대 한 고유한 이름을 사용 하 고 `<URL_from_RequestBin>` hello 섹션 앞의 hello 값으로.</span><span class="sxs-lookup"><span data-stu-id="65b66-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="65b66-138">끝점을 구독할 때 지정 하 여 이벤트 표 형태 hello 이벤트 toothat 끝점의 라우팅을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="65b66-139">에 대 한 `<topic_name>`, 이전에 만든 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="65b66-140">이벤트 tooyour 항목 보내기</span><span class="sxs-lookup"><span data-stu-id="65b66-140">Send an event tooyour topic</span></span>

<span data-ttu-id="65b66-141">이제 보겠습니다 이벤트 toosee를 트리거할 이벤트 표 형태 hello 메시지 tooyour 끝점을 배포 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="65b66-142">첫째, hello URL 가져오고 hello 항목에 대 한 주요 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="65b66-143">다시, `<topic_name>`의 토픽 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="65b66-144">toosimplify이이 문서에서는까지 설정한 샘플 이벤트 데이터 toosend toohello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="65b66-145">일반적으로 응용 프로그램 또는 Azure 서비스는 hello 이벤트 데이터를 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="65b66-146">다음 예제는 hello hello 이벤트 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="65b66-147">경우 있습니다 `echo "$body"` hello 전체 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="65b66-148">hello `data` hello JSON 요소가 이벤트의 hello 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="65b66-149">모든 잘 구성된(Well-Formed) JSON은 이 필드에 배치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="65b66-150">또한 고급 라우팅 및 필터링에 대 한 hello 제목 필드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="65b66-151">CURL은 HTTP 요청을 수행하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="65b66-152">이 문서에서는 CURL toosend hello 이벤트 tooour 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="65b66-153">Hello 이벤트를 실행 하 고 이벤트 표 형태 구독할 때 구성한 hello 메시지 toohello 끝점으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="65b66-154">Toohello 앞에서 만든 RequestBin URL를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="65b66-155">또는 열려 있는 RequestBin 브라우저에서 새로 고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="65b66-156">방금 전송 받은 hello 이벤트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-156">You see hello event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="65b66-157">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="65b66-157">Clean up resources</span></span>
<span data-ttu-id="65b66-158">이 이벤트는 toocontinue 컨트롤러로이 문서에서 만든 hello 리소스를 정리할 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="65b66-159">Toocontinue 않으려는 경우이 문서에서 만든 명령 toodelete hello 리소스 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="65b66-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65b66-160">Next steps</span></span>

<span data-ttu-id="65b66-161">배웠으므로 어떻게 toocreate 항목과 이벤트 구독에 대 한 자세한 내용 이벤트 표 형태 수행할 수 있습니다 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65b66-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="65b66-162">Event Grid 정보</span><span class="sxs-lookup"><span data-stu-id="65b66-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="65b66-163">Azure Event Grid 및 Logic Apps를 사용하여 가상 컴퓨터 변경 모니터링</span><span class="sxs-lookup"><span data-stu-id="65b66-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
