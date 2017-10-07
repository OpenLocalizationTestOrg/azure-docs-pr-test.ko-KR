---
title: "webhook 사용 하 여 Azure 자동화 runbook aaaStarting | Microsoft Docs"
description: "에서 허용 하는 클라이언트 toostart runbook Azure 자동화에 대 한 HTTP 호출 webhook 합니다.  이 문서에서는 설명 방법을 toocreate는 webhook 방법과 toocall 하나의 toostart runbook입니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="79d1e-104">웹후크를 사용하여 Azure Automation Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="79d1e-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="79d1e-105">A *webhook* 사용 하면 특정 runbook toostart Azure 자동화에서 단일 HTTP 요청을 통해.</span><span class="sxs-lookup"><span data-stu-id="79d1e-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="79d1e-106">그러면 Visual Studio Team Services, GitHub, Microsoft Operations Management Suite 로그 분석 또는 사용자 지정 응용 프로그램 같은 외부 서비스 toostart runbook hello Azure 자동화 API를 사용 하 여 전체 솔루션을 구현 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="79d1e-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="79d1e-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="79d1e-108">runbook 시작의 webhook tooother 메서드를 비교할 수 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="79d1e-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="79d1e-109">Webhook의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="79d1e-109">Details of a webhook</span></span>
<span data-ttu-id="79d1e-110">hello 다음 표에서 webhook에 대 한 구성 해야 하는 hello 속성.</span><span class="sxs-lookup"><span data-stu-id="79d1e-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="79d1e-111">속성</span><span class="sxs-lookup"><span data-stu-id="79d1e-111">Property</span></span> | <span data-ttu-id="79d1e-112">설명</span><span class="sxs-lookup"><span data-stu-id="79d1e-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="79d1e-113">이름</span><span class="sxs-lookup"><span data-stu-id="79d1e-113">Name</span></span> |<span data-ttu-id="79d1e-114">이 사용자가 원하는 webhook에 대 한 이름을 노출 되지 않습니다. toohello 클라이언트를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="79d1e-115">하면 tooidentify hello Azure 자동화에서 runbook에 대 한만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="79d1e-116">모범 사례로, hello webhook 사용 하는 이름이 관련된 toohello 클라이언트를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="79d1e-117">URL</span><span class="sxs-lookup"><span data-stu-id="79d1e-117">URL</span></span> |<span data-ttu-id="79d1e-118">hello webhook의 hello URL은 HTTP POST toostart hello runbook 호출 하는 클라이언트 hello 고유한 주소 toohello webhook을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="79d1e-119">Hello webhook을 만들 때 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="79d1e-120">사용자 지정 URL은 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="79d1e-121">hello URL hello runbook toobe 더 이상의 인증이 없는 제 3 자 시스템에 의해 호출을 허용 하는 보안 토큰을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="79d1e-122">따라서 암호처럼 취급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="79d1e-123">보안상의 이유로 hello hello 시간 hello webhook에 Azure 포털의에서 URL이 만들어집니다 보기 hello만 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="79d1e-124">나중에 사용할 안전한 위치에 hello URL에 유념 하십시오.</span><span class="sxs-lookup"><span data-stu-id="79d1e-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="79d1e-125">만료 날짜</span><span class="sxs-lookup"><span data-stu-id="79d1e-125">Expiration date</span></span> |<span data-ttu-id="79d1e-126">각 webhook는 인증서처럼 만료 날짜가 있으며, 이 날짜가 되면 인증서를 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="79d1e-127">Hello webhook 만들어지면이 만료 날짜를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="79d1e-128">사용</span><span class="sxs-lookup"><span data-stu-id="79d1e-128">Enabled</span></span> |<span data-ttu-id="79d1e-129">webhook는 생성되었을 때 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="79d1e-130">TooDisabled를 설정할 경우 클라이언트가 수 toouse 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="79d1e-131">Hello를 설정할 수 있습니다 **Enabled** 속성이 hello webhook 또는 언제 든 지 한 번 만들 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="79d1e-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="79d1e-132">Parameters</span></span>
<span data-ttu-id="79d1e-133">webhook 해당 webhook hello runbook을 시작할 때 사용 되는 runbook 매개 변수의 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="79d1e-134">hello webhook hello runbook의 모든 필수 매개 변수에 대 한 값을 포함 해야 하 고 선택적 매개 변수 값이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="79d1e-135">매개 변수 값 구성 tooa webhook hello webhoook를 만든 후에 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="79d1e-136">여러 연결 하는 webhook tooa 단일 runbook 각각 다른 매개 변수 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="79d1e-137">클라이언트는 webhook을 사용 하 여 runbook이 시작 되 면 hello webhook에 정의 된 hello 매개 변수 값을 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="79d1e-138">tooreceive 데이터 hello 클라이언트의 경우, runbook hello 라는 단일 매개 변수를 받아들일 수 **$WebhookData** 형식의 [object] 데이터를 포함 하는 hello 클라이언트 hello POST 요청에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Webhookdata 속성](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="79d1e-140">hello **$WebhookData** 개체 hello 다음과 같은 속성을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="79d1e-141">속성</span><span class="sxs-lookup"><span data-stu-id="79d1e-141">Property</span></span> | <span data-ttu-id="79d1e-142">설명</span><span class="sxs-lookup"><span data-stu-id="79d1e-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="79d1e-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="79d1e-143">WebhookName</span></span> |<span data-ttu-id="79d1e-144">hello webhook의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="79d1e-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="79d1e-145">RequestHeader</span></span> |<span data-ttu-id="79d1e-146">Hello 들어오는 POST 요청의 hello 헤더를 포함 하는 해시 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="79d1e-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="79d1e-147">RequestBody</span></span> |<span data-ttu-id="79d1e-148">hello 들어오는 POST 요청의 본문 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="79d1e-149">문자열, JSON, XML 또는 인코딩된 데이터와 같은 서식을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="79d1e-150">hello runbook toowork 예상 되는 hello 데이터 형식으로 작성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="79d1e-151">Hello webhook 필요한 toosupport hello의 구성이 **$WebhookData** 매개 변수를 hello runbook tooaccept 필요 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="79d1e-152">Hello runbook hello 매개 변수를 정의 하지 않으면, hello 클라이언트에서 보낸 hello 요청의 세부 정보는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="79d1e-153">Hello webhook을 만들 때 $WebhookData에 대 한 값을 지정 하면 해당 값은 재정의할 수 hello webhook hello 클라이언트가 POST 요청을 hello 데이터로 hello runbook을 시작할 때 hello 클라이언트 hello 요청 본문에 데이터를 포함 하지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="79d1e-154">webhook 이외의 메서드를 사용 하 여 $WebhookData를 가진 runbook을 시작 하는 경우에 hello runbook에서 인식 됩니다 $Webhookdata에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="79d1e-155">이 값은 hello로 개체 여야 합니다. 동일한 [속성](#details-of-a-webhook) 으로 $Webhookdata는 webhook로 전달 하는 실제 WebhookData 작업 했던 마치 함께 해당 hello runbook 제대로 작동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="79d1e-156">예를 들어 경우 hello hello Azure 포털에서에서 runbook을 다음 시작 하 고 toopass WebhookData WebhookData 개체 이므로 테스트를 위해 몇 가지 예제를 사용할 것 전달 되어야 JSON으로 hello UI에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![UI에서의 WebhookData 매개 변수](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="79d1e-158">Runbook hello 다음 hello WebhookData 매개 변수에 대 한 속성이 있는 경우 위의 hello에 대 한:</span><span class="sxs-lookup"><span data-stu-id="79d1e-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="79d1e-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="79d1e-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="79d1e-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="79d1e-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="79d1e-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="79d1e-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="79d1e-162">Hello 다음 hello WebhookData 매개 변수에 대 한 UI hello에 대 한 JSON 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="79d1e-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="79d1e-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![UI에서 WebhookData 매개 변수 시작](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="79d1e-165">모든 입력된 매개 변수 값 hello hello runbook 작업으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="79d1e-166">즉, 모든 hello 클라이언트가 hello webhook 요청에 제공 된 입력 액세스 toohello 자동화 작업으로 기록 되 고 사용 가능한 tooanyone 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="79d1e-167">따라서 webhook 호출에 중요한 정보를 포함할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="79d1e-168">보안</span><span class="sxs-lookup"><span data-stu-id="79d1e-168">Security</span></span>
<span data-ttu-id="79d1e-169">webhook의 hello 보안 toobe 호출을 허용 하는 보안 토큰을 포함 하는 URL의 hello 개인 정보에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="79d1e-170">Azure 자동화 toohello 올바른 URL 구성으로 hello 요청에서 인증이 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="79d1e-171">이러한 이유로 webhook 쓰일 수 없습니다는 다른 방법이 hello 요청 유효성 검사를 사용 하지 않고 매우 중요 한 기능을 수행 하는 runbook에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="79d1e-172">호출 했는 webhook hello를 확인 하 여 hello runbook toodetermine 내에서 논리를 포함할 수 **WebhookName** $WebhookData hello 매개 변수 속성.</span><span class="sxs-lookup"><span data-stu-id="79d1e-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="79d1e-173">hello runbook 수 추가 유효성 검사를 수행할 hello에 특정 한 정보를 검색 하 여 **RequestHeader** 또는 **RequestBody** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="79d1e-174">또 다른 전략은 toohave hello runbook webhook 요청을 받았을 때 외부는 상태의 일부 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="79d1e-175">예를 들어 새 커밋 tooa GitHub 리포지토리 있을 때마다 GitHub에 의해 호출 되는 runbook을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="79d1e-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="79d1e-176">hello runbook에는 계속 하기 전에 새 커밋 실제로 발생 tooGitHub toovalidate를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="79d1e-177">webhook 만들기</span><span class="sxs-lookup"><span data-stu-id="79d1e-177">Creating a webhook</span></span>
<span data-ttu-id="79d1e-178">다음 프로시저 toocreate hello Azure 포털에서에서 새 연결 하는 webhook tooa runbook hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="79d1e-179">Hello에서 **Runbook 블레이드에서** hello Azure 포털에서에서 클릭 webhook hello hello runbook tooview 해당 세부 정보 블레이드에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="79d1e-180">클릭 **Webhook** hello 블레이드 tooopen hello의 hello 위쪽 **추가 Webhook** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="79d1e-181">
   ![Webhooks 단추](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="79d1e-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="79d1e-182">클릭 **새 webhook 만들기** tooopen hello **만들기 webhook 블레이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="79d1e-183">지정 된 **이름**, **만료 날짜** hello webhook 및 사용 여부에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="79d1e-184">이러한 속성에 대한 자세한 내용은 [webhook 세부 정보](#details-of-a-webhook) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="79d1e-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="79d1e-185">Ctrl + C toocopy hello URL의 webhook hello와 hello 복사 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="79d1e-186">그런 다음 안전한 곳에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-186">Then record it in a safe place.</span></span>  <span data-ttu-id="79d1e-187">**Hello webhook을 만든 후 다시 hello URL를 검색할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="79d1e-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="79d1e-188">
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="79d1e-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="79d1e-189">클릭 **매개 변수** tooprovide hello runbook 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="79d1e-190">Hello runbook은 필수 매개 변수를 다음 됩니다 수 toocreate hello webhook 값을 제공 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="79d1e-191">클릭 **만들기** toocreate hello webhook 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="79d1e-192">webhook 사용</span><span class="sxs-lookup"><span data-stu-id="79d1e-192">Using a webhook</span></span>
<span data-ttu-id="79d1e-193">만들어진 후 webhook toouse 클라이언트 응용 프로그램 hello webhook에 대 한 hello URL 인 HTTP POST를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="79d1e-194">형식에 따라 hello hello webhook의 hello 구문이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="79d1e-195">hello 클라이언트 hello hello POST 요청에서 반환 코드를 다음 중 하나를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="79d1e-196">코드</span><span class="sxs-lookup"><span data-stu-id="79d1e-196">Code</span></span> | <span data-ttu-id="79d1e-197">텍스트</span><span class="sxs-lookup"><span data-stu-id="79d1e-197">Text</span></span> | <span data-ttu-id="79d1e-198">설명</span><span class="sxs-lookup"><span data-stu-id="79d1e-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79d1e-199">202</span><span class="sxs-lookup"><span data-stu-id="79d1e-199">202</span></span> |<span data-ttu-id="79d1e-200">수락됨</span><span class="sxs-lookup"><span data-stu-id="79d1e-200">Accepted</span></span> |<span data-ttu-id="79d1e-201">hello 요청이 수락 되었음 및 hello runbook 성공적으로 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="79d1e-202">400</span><span class="sxs-lookup"><span data-stu-id="79d1e-202">400</span></span> |<span data-ttu-id="79d1e-203">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="79d1e-203">Bad Request</span></span> |<span data-ttu-id="79d1e-204">hello 다음 이유 중 하나에 대 한 hello 요청이 수락 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="79d1e-205">hello webhook은 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="79d1e-206">hello webhook 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="79d1e-207">hello URL에 hello 토큰이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="79d1e-208">404</span><span class="sxs-lookup"><span data-stu-id="79d1e-208">404</span></span> |<span data-ttu-id="79d1e-209">찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="79d1e-209">Not Found</span></span> |<span data-ttu-id="79d1e-210">hello 다음 이유 중 하나에 대 한 hello 요청이 수락 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="79d1e-211">hello webhook은 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="79d1e-212">hello runbook은 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="79d1e-213">hello 계정은 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="79d1e-214">500</span><span class="sxs-lookup"><span data-stu-id="79d1e-214">500</span></span> |<span data-ttu-id="79d1e-215">내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="79d1e-215">Internal Server Error</span></span> |<span data-ttu-id="79d1e-216">hello URL 올바르지만 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="79d1e-217">Hello 요청을 다시 전송 하십시오.</span><span class="sxs-lookup"><span data-stu-id="79d1e-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="79d1e-218">Hello webhook 응답 hello 작업 id를 JSON 형식에 다음과 같이 포함 hello 요청은 성공 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="79d1e-219">단일 작업 id를 포함 합니다 있지만 hello JSON 형식 잠재적인 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="79d1e-220">hello 클라이언트 hello runbook 작업이 완료 될 때 또는 hello webhook에서의 완료 상태를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="79d1e-221">와 같은 다른 방법으로 hello 작업 id를 사용 하는이 정보를 확인할 수 [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) 또는 hello [Azure 자동화 API](https://msdn.microsoft.com/library/azure/mt163826.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="79d1e-222">예제</span><span class="sxs-lookup"><span data-stu-id="79d1e-222">Example</span></span>
<span data-ttu-id="79d1e-223">다음 예제는 hello는 webhook을 Windows PowerShell toostart runbook을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="79d1e-224">HTTP 요청을 만들 수 있는 모든 언어는 webhook를 사용할 수 있습니다. Windows PowerShell은 예제로 여기에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="79d1e-225">hello runbook hello hello 요청 본문의 JSON으로 서식이 지정 된 가상 컴퓨터의 목록에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="79d1e-226">Hello 요청의 hello 헤더에서 시작 되 고 hello runbook 및 hello 날짜 및 시간에 시작 되 게 하는 방법에 대 한 정보도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="79d1e-227">hello 다음 그림에 나와 hello 헤더 정보 (사용 하는 [Fiddler](http://www.telerik.com/fiddler) 추적)에서이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="79d1e-228">여기에 HTTP 요청의 표준 헤더 추가 toohello에 사용자 지정 날짜 및 추가 하는 헤더에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="79d1e-229">이러한 각 값은 hello에서 사용할 수 있는 toohello runbook **RequestHeaders** 속성 **WebhookData**합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Webhook 단추](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="79d1e-231">hello 다음 그림에 나와 hello hello 요청 본문 (사용 하 여는 [Fiddler](http://www.telerik.com/fiddler) 추적) hello에서 사용할 수 있는 toohello runbook 즉 **RequestBody** 속성 **WebhookData**합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="79d1e-232">기 때문에 해당 hello hello 요청 본문에 포함 된 hello 형식을 JSON으로 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Webhook 단추](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="79d1e-234">hello 다음 그림은 hello 요청 Windows PowerShell 및 hello 결과 응답에서 보내는입니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="79d1e-235">hello 작업 id는 hello 응답 및 tooa 변환 된 문자열에서 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Webhook 단추](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="79d1e-237">hello 다음 샘플 runbook hello 이전 예제에서는 요청을 수락 하 고 hello 요청 본문에 지정 된 hello 가상 컴퓨터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="79d1e-238">응답 tooAzure 경고에서 runbook 시작</span><span class="sxs-lookup"><span data-stu-id="79d1e-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="79d1e-239">Webhook 사용이 가능한 runbook 수 사용된 tooreact 너무[Azure 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="79d1e-240">성능, 가용성 및 사용 하 여 hello Azure 경고 사용 같은 hello 통계를 수집 하 여 Azure의에서 리소스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="79d1e-241">모니터링 메트릭이나 이벤트를 기반으로 Azure 리소스에 대한 경고를 받을 수 있습니다. 현재 자동화 계정은 메트릭만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="79d1e-242">할당 hello 임계값 또는 hello 구성 된 이벤트는 트리거되지 다음 알림을 toohello 서비스 관리자 또는 공동 관리자 tooresolve hello 경고, 메트릭에 대 한 자세한 내용은 전송 되 고 이벤트 너무 참조 하십시오 지정 된 메트릭 hello 값을 초과 하는 경우[ Azure 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="79d1e-243">외에도 Azure 경고를 사용 하 여 알림 시스템으로, runbook에 대 한 응답 tooalerts 시작 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="79d1e-244">Azure 자동화로 Azure 경고 hello 기능 toorun webhook 사용이 가능한 runbook을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="79d1e-245">메트릭 초과 하는 경우 hello hello 경고 규칙이 활성화 되 고 트리거 hello 차례로 hello runbook을 실행 하는 자동화 webhook 임계값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="79d1e-247">경고 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="79d1e-247">Alert context</span></span>
<span data-ttu-id="79d1e-248">이 컴퓨터의 CPU 사용률은 hello 주요 성능 메트릭 중 하나, 가상 컴퓨터와 같은 Azure 리소스를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="79d1e-249">이면 hello CPU 사용률이 100% 또는 특정 시간 보다 긴 기간 동안 toorestart hello 가상 컴퓨터 toofix hello 문제를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="79d1e-250">경고 규칙 toohello 가상 컴퓨터를 구성 하 여 해결할 수이 고이 규칙은 메트릭으로 CPU 비율 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="79d1e-251">예를 들어 CPU 백분율 여기 바로 수행 되지만 tooyour Azure를 구성할 수 있는 다른 많은 메트릭 리소스 및 hello 가상 컴퓨터를 다시 시작 되는 작업은이 문제를 toofix 수행 hello runbook tootake 다른 동작을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="79d1e-252">이 hello 경고 규칙이 활성화 되 고 트리거 hello webhook 사용이 가능한 runbook을 hello 경고 컨텍스트 toohello runbook을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="79d1e-253">[경고 컨텍스트](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) 포함 하 여 세부 정보를 포함 **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** 및 **타임 스탬프** hello runbook tooidentify hello 리소스에 있는 것을 받겠습니다 동작에 대 한 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="79d1e-254">상황에 맞는 hello의 hello 본문 부분에 포함 되어 경고 **WebhookData** 보낸된 toohello runbook 개체를 사용 하 여 액세스할 수 있습니다 **Webhook.RequestBody** 속성</span><span class="sxs-lookup"><span data-stu-id="79d1e-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="79d1e-255">예제</span><span class="sxs-lookup"><span data-stu-id="79d1e-255">Example</span></span>
<span data-ttu-id="79d1e-256">구독과 연결에는 Azure 가상 컴퓨터 만들기는 [toomonitor CPU 비율 메트릭을 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="79d1e-257">Hello 경고를 만드는 동안 hello webhook를 만드는 동안 생성 된 hello webhook URL이 hello 인 hello webhook 필드를 채울 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="79d1e-258">hello 다음 샘플 runbook이 트리거되 hello 경고 규칙이 활성화 되 고 hello runbook tooidentify hello 리소스에 있는 것을 받겠습니다 작업에 필요한 hello 경고 컨텍스트 매개 변수를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="79d1e-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79d1e-259">Next steps</span></span>
* <span data-ttu-id="79d1e-260">다양 한 방법 toostart runbook에 대 한 세부 정보를 참조 하십시오. [Runbook 시작](automation-starting-a-runbook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="79d1e-261">Runbook 작업의 상태 보기 hello에 대 한 자세한 내용은 참조 너무[Azure 자동화에서 Runbook 실행](automation-runbook-execution.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="79d1e-262">toouse Azure 자동화 tootake 작업 Azure 경고를 확인 하려면 어떻게 해야 toolearn [자동화 Runbook과 Azure VM 경고 재구성](automation-azure-vm-alert-integration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79d1e-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
