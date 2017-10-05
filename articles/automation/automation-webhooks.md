---
title: "웹후크를 사용하여 Azure Automation Runbook 시작 | Microsoft Docs"
description: "클라이언트가 Azure 자동화에서 HTTP 호출을 통해 runbook을 시작하는 데 사용되는 webhook입니다.  이 문서는 webhook를 만드는 방법 및 webhook를 호출하여 runbook을 시작하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="0db65-104">웹후크를 사용하여 Azure Automation Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="0db65-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="0db65-105">*Webhook*를 사용하면 단일 HTTP 요청을 통해 Azure 자동화에서 특정 runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="0db65-106">이는 Azure Automation API를 사용하여 전체 솔루션을 구현하지 않아도 Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics 또는 사용자 지정 응용 프로그램과 같은 외부 서비스가 Runbook을 시작할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="0db65-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="0db65-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="0db65-108">[Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0db65-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="0db65-109">Webhook의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="0db65-109">Details of a webhook</span></span>
<span data-ttu-id="0db65-110">다음 표에서는 Webhook에 대해 구성해야 하는 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="0db65-111">속성</span><span class="sxs-lookup"><span data-stu-id="0db65-111">Property</span></span> | <span data-ttu-id="0db65-112">설명</span><span class="sxs-lookup"><span data-stu-id="0db65-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0db65-113">이름</span><span class="sxs-lookup"><span data-stu-id="0db65-113">Name</span></span> |<span data-ttu-id="0db65-114">클라이언트에 노출되지 않으므로 원하는 Webhook 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="0db65-115">Azure 자동화에서 사용자가 runbook을 식별하는 용도로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="0db65-116">가장 좋은 방법은 webhook를 사용할 클라이언트와 관련된 이름을 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="0db65-117">URL</span><span class="sxs-lookup"><span data-stu-id="0db65-117">URL</span></span> |<span data-ttu-id="0db65-118">webhook의 URL은 클라이언트가 webhook에 연결된 runbook을 시작하기 위해 HTTP POST로 호출하는 고유한 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="0db65-119">webhook를 만들 때 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="0db65-120">사용자 지정 URL은 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="0db65-121">URL에는 타사 시스템이 추가 인증 없이 runbook을 호출할 수 있게 해주는 보안 토큰이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="0db65-122">따라서 암호처럼 취급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="0db65-123">보안상의 이유로 이 URL은 Azure 포털에서 webhook가 생성될 때만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="0db65-124">이 URL을 나중에 사용할 수 있도록 안전한 위치에 기록해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="0db65-125">만료 날짜</span><span class="sxs-lookup"><span data-stu-id="0db65-125">Expiration date</span></span> |<span data-ttu-id="0db65-126">각 webhook는 인증서처럼 만료 날짜가 있으며, 이 날짜가 되면 인증서를 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="0db65-127">웹후크를 생성한 후에 이 만료 날짜를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="0db65-128">사용</span><span class="sxs-lookup"><span data-stu-id="0db65-128">Enabled</span></span> |<span data-ttu-id="0db65-129">webhook는 생성되었을 때 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="0db65-130">사용 안함으로 설정할 경우 클라이언트가 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="0db65-131">**Enabled** 속성은 webhook를 만들 때 또는 webhook가 생성된 후 언제든지 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="0db65-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0db65-132">Parameters</span></span>
<span data-ttu-id="0db65-133">webhook는 runbook을 시작할 때 사용되는 runbook 매개 변수 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="0db65-134">webhook에는 runbook의 모든 필수 매개 변수 값이 포함되어야 하고 선택적 매개 변수 값이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="0db65-135">Webhook에 구성된 매개 변수 값은 webhook를 만든 후에도 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="0db65-136">단일 runbook에 연결된 여러 webhook는 각각 다른 매개 변수 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="0db65-137">클라이언트는 webhook를 사용하여 runbook을 시작할 때 webhook에 정의된 매개 변수 값을 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="0db65-138">클라이언트에서 데이터를 수신하기 위해 runbook은 클라이언트가 POST 요청에 포함하는 데이터가 포함된 [object] 형식의 **$WebhookData** 라는 단일 매개 변수를 받아들일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Webhookdata 속성](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="0db65-140">**$WebhookData** 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="0db65-141">속성</span><span class="sxs-lookup"><span data-stu-id="0db65-141">Property</span></span> | <span data-ttu-id="0db65-142">설명</span><span class="sxs-lookup"><span data-stu-id="0db65-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0db65-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="0db65-143">WebhookName</span></span> |<span data-ttu-id="0db65-144">Webhook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-144">The name of the webhook.</span></span> |
| <span data-ttu-id="0db65-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="0db65-145">RequestHeader</span></span> |<span data-ttu-id="0db65-146">들어오는 POST 요청의 헤더를 포함한 해시 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="0db65-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="0db65-147">RequestBody</span></span> |<span data-ttu-id="0db65-148">들어오는 POST 요청의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="0db65-149">문자열, JSON, XML 또는 인코딩된 데이터와 같은 서식을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="0db65-150">Runbook은 예상되는 데이터 형식으로 작동하도록 작성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="0db65-151">**$WebhookData** 매개 변수를 지원하는 데 필요한 webhook 구성은 없으며, runbook은 이를 수락할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="0db65-152">runbook이 매개 변수를 정의하지 않을 경우 클라이언트에서 전송된 요청의 모든 세부 정보가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="0db65-153">webhook를 만들 때 $WebhookData에 값을 지정 하면 클라이언트가 요청 본문에 데이터를 포함하지 않을 경우에도 webhook가 클라이언트 POST 요청의 데이터로 runbook을 시작할 때 해당 값이 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="0db65-154">webhook 이외의 방법을 사용하는 $WebhookData가 있는 runbook을 시작하는 경우 runbook에서 인식할 $Webhookdata 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="0db65-155">이 값은 runbook이 webhook에서 전달된 실제 WebhookData로 작동하는 것처럼 제대로 작동할 수 있도록 $Webhookdata와 동일한 [속성](#details-of-a-webhook)을 가진 개체여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="0db65-156">예를 들어 Azure 포털에서 다음 runbook을 시작하고 테스트용으로 일부 샘플 WebhookData를 전달하려는 경우 WebhookData는 개체이기 때문에 UI에서 JSON으로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![UI에서의 WebhookData 매개 변수](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="0db65-158">위의 runbook의 경우 WebhookData 매개 변수에 대한 다음 속성을 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="0db65-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="0db65-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="0db65-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="0db65-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="0db65-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="0db65-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="0db65-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="0db65-162">그런 다음 WebhookData 매개 변수에 대한 UI에서 다음 JSON 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="0db65-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="0db65-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![UI에서 WebhookData 매개 변수 시작](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="0db65-165">모든 입력 매개 변수의 값은 runbook 작업에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="0db65-166">webhook 요청에서 클라이언트에서 제공된 입력이 기록되고 자동화 작업에 액세스할 수 있는 모든 사용자가 사용할 수 있게 된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="0db65-167">따라서 webhook 호출에 중요한 정보를 포함할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="0db65-168">보안</span><span class="sxs-lookup"><span data-stu-id="0db65-168">Security</span></span>
<span data-ttu-id="0db65-169">webhook의 보안은 webhook의 호출에 사용되는 보안 토큰을 포함하는 URL의 개인 정보에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="0db65-170">Azure 자동화는 올바른 URL로 설정되어 있는 경우에만 요청에 대한 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="0db65-171">따라서 대체 유효성 검사 방법을 사용하지 않고 매우 중요한 기능을 수행하는 runbook에 webhook를 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="0db65-172">$WebhookData 매개 변수의 **WebhookName** 속성을 확인하여 webhook에서 호출했는지 확인하는 논리를 runbook 내에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="0db65-173">Runbook은 **RequestHeader** 또는 **RequestBody** 속성에서 특정 정보를 찾아 추가로 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="0db65-174">또 다른 전략은 runbook이 webhook 요청을 받았을 때 외부 조건의 일부 유효성 검사를 수행하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="0db65-175">예를 들어 GitHub 리포지토리에 대한 새 커밋이 있을 때마다 GitHub에 의해 호출되는 runbook을 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="0db65-176">이 Runbook은 계속하기 전에 GitHub에 연결하여 새 커밋이 실제로 방금 전에 발생했는지 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="0db65-177">webhook 만들기</span><span class="sxs-lookup"><span data-stu-id="0db65-177">Creating a webhook</span></span>
<span data-ttu-id="0db65-178">Azure 포털에서 runbook에 연결된 새 webhook를 만들려면 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="0db65-179">Azure 포털의 **Runbook 블레이드** 에서 해당 세부 정보 블레이드를 표시하도록 webhook를 시작할 runbook을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="0db65-180">블레이드 맨 위에서 **Webhook**을 클릭하여 **Webhook 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="0db65-181">
   ![Webhooks 단추](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="0db65-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="0db65-182">**새 webhook 만들기**를 클릭하여 **webhook 블레이드 만들기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="0db65-183">webhook의 **이름**, **만료 날짜**와 사용 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="0db65-184">이러한 속성에 대한 자세한 내용은 [webhook 세부 정보](#details-of-a-webhook) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="0db65-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="0db65-185">복사 아이콘을 클릭하고 Ctrl+C를 눌러 webhook의 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="0db65-186">그런 다음 안전한 곳에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-186">Then record it in a safe place.</span></span>  <span data-ttu-id="0db65-187">**webhook를 만들고 나면 URL을 다시 검색할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="0db65-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="0db65-188">
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="0db65-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="0db65-189">**매개 변수** 를 클릭하여 runbook 매개 변수의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="0db65-190">runbook에 필수 매개 변수가 있으면 값을 제공 하지 않는 한 webhook를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="0db65-191">**만들기** 를 클릭하여 webhook를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="0db65-192">webhook 사용</span><span class="sxs-lookup"><span data-stu-id="0db65-192">Using a webhook</span></span>
<span data-ttu-id="0db65-193">만들어진 후 webhook를 사용하려면 클라이언트 응용 프로그램이 webhook의 URL로 HTTP POST를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="0db65-194">webhook의 구문 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="0db65-195">클라이언트는 POST 요청으로부터의 다음 반환 코드 중 하나를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="0db65-196">코드</span><span class="sxs-lookup"><span data-stu-id="0db65-196">Code</span></span> | <span data-ttu-id="0db65-197">텍스트</span><span class="sxs-lookup"><span data-stu-id="0db65-197">Text</span></span> | <span data-ttu-id="0db65-198">설명</span><span class="sxs-lookup"><span data-stu-id="0db65-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0db65-199">202</span><span class="sxs-lookup"><span data-stu-id="0db65-199">202</span></span> |<span data-ttu-id="0db65-200">수락됨</span><span class="sxs-lookup"><span data-stu-id="0db65-200">Accepted</span></span> |<span data-ttu-id="0db65-201">요청이 수락되었고 runbook에서 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="0db65-202">400</span><span class="sxs-lookup"><span data-stu-id="0db65-202">400</span></span> |<span data-ttu-id="0db65-203">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="0db65-203">Bad Request</span></span> |<span data-ttu-id="0db65-204">다음 이유 중 하나로 인해 요청이 수락되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="0db65-205">webhook가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="0db65-206">webhook가 비활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="0db65-207">URL의 토큰이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="0db65-208">404</span><span class="sxs-lookup"><span data-stu-id="0db65-208">404</span></span> |<span data-ttu-id="0db65-209">찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0db65-209">Not Found</span></span> |<span data-ttu-id="0db65-210">다음 이유 중 하나로 인해 요청이 수락되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="0db65-211">webhook를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="0db65-212">runbook을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="0db65-213">계정을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="0db65-214">500</span><span class="sxs-lookup"><span data-stu-id="0db65-214">500</span></span> |<span data-ttu-id="0db65-215">내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="0db65-215">Internal Server Error</span></span> |<span data-ttu-id="0db65-216">URL은 유효했지만 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="0db65-217">요청을 다시 제출하십시오.</span><span class="sxs-lookup"><span data-stu-id="0db65-217">Please resubmit the request.</span></span> |

<span data-ttu-id="0db65-218">요청이 성공했다고 가정하면 webhook 응답은 다음과 같은 JSON 형식의 작업 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="0db65-219">단일 작업 ID를 포함하지만 잠재적인 이후 향상 기능에 대해 JSON 형식이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="0db65-220">클라이언트는 runbook 작업이 완료되었거나 webhook의 완료 상태인 경우 클라이언트를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="0db65-221">[Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) 또는 [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx)와 같은 다른 메서드로 작업 ID를 사용하여 이 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="0db65-222">예</span><span class="sxs-lookup"><span data-stu-id="0db65-222">Example</span></span>
<span data-ttu-id="0db65-223">다음 예제는 Windows PowerShell을 사용하여 webhook로 runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="0db65-224">HTTP 요청을 만들 수 있는 모든 언어는 webhook를 사용할 수 있습니다. Windows PowerShell은 예제로 여기에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="0db65-225">Runbook에는 요청 본문에 JSON으로 서식이 지정된 가상 컴퓨터의 목록이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="0db65-226">runbook을 시작한 사람 및 요청 헤더에서 시작된 날짜와 시간에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="0db65-227">다음 이미지는 요청에서 헤더 정보를 표시합니다( [Fiddler](http://www.telerik.com/fiddler) 추적 사용).</span><span class="sxs-lookup"><span data-stu-id="0db65-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="0db65-228">사용자 지정 날짜 및 추가한 헤더 외에 HTTP 요청의 표준 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="0db65-229">이러한 각 값은 **WebhookData**의 **RequestHeaders** 속성으로 runbook에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Webhook 단추](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="0db65-231">다음 이미지는 **WebhookData**의 **RequestBody** 속성에서 runbook에 사용할 수 있는 요청 본문을 보여줍니다([Fiddler](http://www.telerik.com/fiddler) 추적 사용).</span><span class="sxs-lookup"><span data-stu-id="0db65-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="0db65-232">요청의 본문에 포함된 형식이기 때문에 JSON으로 서식 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Webhook 단추](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="0db65-234">다음 이미지는 Windows PowerShell 및 결과 응답에서 전송되는 요청을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="0db65-235">작업 ID는 응답에서 추출되고 문자열로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-235">The job id is extracted from the response and converted to a string.</span></span>

![Webhook 단추](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="0db65-237">다음 샘플 runbook은 이전 예제 요청을 수락하고 요청 본문에 지정된 가상 컴퓨터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

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

            # Authenticate to Azure resources
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
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="0db65-238">Azure 경고에 답하여 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="0db65-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="0db65-239">Webhook 지원 Runbook을 사용하여 [Azure 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)에 대처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0db65-240">Azure 경고를 통해 성능, 가용성 및 사용량 등의 통계를 수집하여 Azure의 리소스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="0db65-241">모니터링 메트릭이나 이벤트를 기반으로 Azure 리소스에 대한 경고를 받을 수 있습니다. 현재 자동화 계정은 메트릭만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="0db65-242">지정한 메트릭의 값이 할당된 임계값을 초과하거나 구성된 이벤트가 트리거된 경우 서비스 관리자나 공동 관리자에게 알림을 보내 경고를 해결하도록 합니다. 메트릭과 이벤트에 대한 자세한 내용은 [Azure 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db65-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0db65-243">Azure 경고를 알림 시스템으로 사용하는 것 외에도 알림에 대한 응답으로 Runbook을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="0db65-244">Azure 자동화는 Azure 경고를 통해 Webhook 지원 Rubbook을 실행하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="0db65-245">메트릭이 구성된 임계값을 초과할 경우 경고 규칙이 활성화되고 그에 따라 Runbook을 실행하는 자동화 Webhook를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="0db65-247">경고 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="0db65-247">Alert context</span></span>
<span data-ttu-id="0db65-248">가상 컴퓨터, CPU 사용률 등의 Azure 리소스를 주요한 성능 메트릭 중 하나로 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="0db65-249">CPU 사용률이 100%이거나 장기간 특정 수준 이상이면 가상 컴퓨터를 다시 시작하여 문제를 해결하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="0db65-250">이 문제는 가상 컴퓨터에 대한 규칙 경고를 구성하여 해결할 수 있으며 이 규칙에서는 CPU 백분율을 메트릭으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="0db65-251">여기서 CPU 백분율은 단순한 예일 뿐이며 Azure 리소스에 대해 많은 다른 메트릭을 구성할 수 있습니다. 가상 컴퓨터를 다시 시작하는 것은 문제를 해결하기 위한 조치로, Runbook이 다른 조치를 취하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="0db65-252">이 경고 규칙이 활성화되고 Webhook 지원 Runbook이 트리거되면 Runbook의 컨텍스트에서 경고를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="0db65-253">[경고 컨텍스트](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)는 **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** 및 **Timestamp** 등, Runbook이 조치를 취할 리소스를 파악하는 데 필요한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="0db65-254">경고 컨텍스트는 Runbook으로 전송된 **WebhookData** 개체의 본문 부분에 포함되며 **Webhook.RequestBody** 속성으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="0db65-255">예</span><span class="sxs-lookup"><span data-stu-id="0db65-255">Example</span></span>
<span data-ttu-id="0db65-256">구독에서 Azure 가상 컴퓨터를 만들고 [CPU 백분율 메트릭 모니터링을 위한 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0db65-257">경고를 만들 때, Webhook를 만들 때 생성된 Webhook URL로 Webhook 필드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="0db65-258">다음 Rubbook 샘플은 경고 규칙이 활성화되었을 때 트리거되며 Runbook이 조치를 취할 리소스를 파악하는 데 필요한 경고 컨텍스트 매개 변수를 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="0db65-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

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

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
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

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="0db65-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0db65-259">Next steps</span></span>
* <span data-ttu-id="0db65-260">Runbook을 시작하는 다양한 방법에 대한 자세한 내용은 [Runbook 시작](automation-starting-a-runbook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db65-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="0db65-261">Runbook 작업의 상태 보기에 대한 내용은 [Azure Automation에서 Runbook 실행](automation-runbook-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db65-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="0db65-262">Azure Automation을 사용하여 Azure 경고에 대해 조치를 취하는 방법을 알아보려면 [Automation Runbook으로 Azure VM 경고 수정](automation-azure-vm-alert-integration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db65-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
