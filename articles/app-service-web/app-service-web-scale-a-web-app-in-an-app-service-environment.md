---
title: "앱 서비스 환경에서 앱을 확장하는 방법"
description: "앱 서비스 환경에서 앱 확장"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 240c2486c23b7cd84e2471bf5b2170e08ee1f150
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a><span data-ttu-id="29516-103">앱 서비스 환경에서 앱 확장</span><span class="sxs-lookup"><span data-stu-id="29516-103">Scaling apps in an App Service Environment</span></span>
<span data-ttu-id="29516-104">Azure 앱 서비스에서는 일반적으로 다음 세 가지를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-104">In the Azure App Service there are normally three things you can scale:</span></span>

* <span data-ttu-id="29516-105">가격 계획</span><span class="sxs-lookup"><span data-stu-id="29516-105">pricing plan</span></span>
* <span data-ttu-id="29516-106">작업자 크기</span><span class="sxs-lookup"><span data-stu-id="29516-106">worker size</span></span> 
* <span data-ttu-id="29516-107">인스턴스 수</span><span class="sxs-lookup"><span data-stu-id="29516-107">number of instances.</span></span>

<span data-ttu-id="29516-108">ASE에서는 가격 계획을 선택하거나 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-108">In an ASE there is no need to select or change the pricing plan.</span></span>  <span data-ttu-id="29516-109">기능적인 측면에서 이미 프리미엄 가격 기능 수준이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="29516-109">In terms of capabilities it is already at a Premium pricing capability level.</span></span>  

<span data-ttu-id="29516-110">작업자 크기와 관련하여 ASE 관리자는 고정 크기 대신 각 작업자 풀에 사용할 계산 리소스의 크기를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-110">With respect to worker sizes, the ASE admin can assign the size of the compute resource to be used for each worker pool.</span></span>  <span data-ttu-id="29516-111">따라서 필요한 경우 P4 계산 리소스가 있는 작업자 풀 1과 P1 계산 리소스가 있는 작업자 풀 2를 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-111">That means you can have Worker Pool 1 with P4 compute resources and Worker Pool 2 with P1 compute resources, if desired.</span></span>  <span data-ttu-id="29516-112">크기 순이 아니어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-112">They do not have to be in size order.</span></span>  <span data-ttu-id="29516-113">크기 및 해당 가격 책정에 대한 자세한 내용은 [Azure App Service 가격 책정][AppServicePricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29516-113">For details around the sizes and their pricing see the document here [Azure App Service Pricing][AppServicePricing].</span></span>  <span data-ttu-id="29516-114">따라서 앱 서비스 환경에서는 웹앱 및 앱 서비스 계획의 확장 옵션에 다음 항목만 남게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-114">This leaves the scaling options for web apps and App Service Plans in an App Service Environment to be:</span></span>

* <span data-ttu-id="29516-115">작업자 풀 선택</span><span class="sxs-lookup"><span data-stu-id="29516-115">worker pool selection</span></span>
* <span data-ttu-id="29516-116">인스턴스 수</span><span class="sxs-lookup"><span data-stu-id="29516-116">number of instances</span></span>

<span data-ttu-id="29516-117">한 항목을 변경하는 작업은 ASE 호스트된 앱 서비스 계획에 대해 표시되는 적절한 UI를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-117">Changing either item is done through the appropriate UI shown for your ASE hosted App Service Plans.</span></span>  

![][1]

<span data-ttu-id="29516-118">ASP가 있는 작업자 풀의 사용 가능한 계산 리소스 수를 초과하여 ASP를 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-118">You can't scale up your ASP beyond the number of available compute resources in the worker pool that your ASP is in.</span></span>  <span data-ttu-id="29516-119">해당 작업자 풀에 계산 리소스가 필요한 경우 ASE 관리자에게 추가해 달라고 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-119">If you need compute resources in that worker pool you need to get your ASE administrator to add them.</span></span>  <span data-ttu-id="29516-120">ASE를 다시 구성하는 방법에 대한 정보는 [App Service 환경을 구성하는 방법][HowtoConfigureASE]을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="29516-120">For information around re-configuring your ASE read the information here: [How to Configure an App Service environment][HowtoConfigureASE].</span></span>  <span data-ttu-id="29516-121">일정 또는 메트릭에 따라 용량을 추가하기 위해 ASE 자동 크기 조정 기능을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-121">You may also want to take advantage of the ASE autoscale features to add capacity based on schedule or metrics.</span></span>  <span data-ttu-id="29516-122">ASE 환경 자체에 대한 자동 크기 조정 구성에 대한 자세한 내용은 [App Service 환경에 대한 자동 크기 조정을 구성하는 방법][ASEAutoscale]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29516-122">To get more details on configuring autoscale for the ASE environment itself see [How to configure autoscale for an App Service Environment][ASEAutoscale].</span></span>

<span data-ttu-id="29516-123">다양한 작업자 풀의 계산 리소스를 사용하여 여러 앱 서비스 계획을 만들거나, 동일한 작업자 풀을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-123">You can create multiple app service plans using compute resources from different worker pools, or you can use the same worker pool.</span></span>  <span data-ttu-id="29516-124">예를 들어 작업자 풀 1에 사용 가능한 계산 리소스 10개가 있는 경우 6개의 계산 리소스를 사용하여 하나의 앱 서비스 계획을 만들고 나머지 4개의 계산 리소스를 사용하는 두 번째 앱 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-124">For example if you have (10) available compute resources in Worker Pool 1, you can choose to create one app service plan using (6) compute resources, and a second app service plan that uses (4) compute resources.</span></span>

### <a name="scaling-the-number-of-instances"></a><span data-ttu-id="29516-125">인스턴스 수 확장</span><span class="sxs-lookup"><span data-stu-id="29516-125">Scaling the number of instances</span></span>
<span data-ttu-id="29516-126">앱 서비스 환경에서 웹앱을 처음 만드는 경우 1개의 인스턴스로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-126">When you first create your web app in an App Service Environment it starts with 1 instance.</span></span>  <span data-ttu-id="29516-127">그런 다음 앱에 대한 추가 계산 리소스를 제공하기 위해 추가 인스턴스로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-127">You can then scale out to additional instances to provide additional compute resources for your app.</span></span>   

<span data-ttu-id="29516-128">ASE의 용량이 충분한 경우에는 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-128">If your ASE has enough capacity then this is pretty simple.</span></span>  <span data-ttu-id="29516-129">확장할 사이트를 유지하는 앱 서비스 계획으로 이동하여 크기 조정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-129">You go to your App Service Plan that holds the sites you want to scale up and select Scale.</span></span>  <span data-ttu-id="29516-130">그러면 수동으로 ASP 프로그램에 대한 확장을 설정하거나 ASP에 대한 자동 크기 조정 규칙을 구성하는 UI가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="29516-130">This opens the UI where you can manually set the scale for your ASP or configure autoscale rules for your ASP.</span></span>  <span data-ttu-id="29516-131">수동으로 앱을 확장하려면 ***확장 기준***을 ***수동으로 입력한 인스턴스 수***로 설정하기면 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-131">To manually scale your app simply set ***Scale by*** to ***an instance count that I enter manually***.</span></span>  <span data-ttu-id="29516-132">여기에서 원하는 수량으로 슬라이더를 끌거나 슬라이더 옆에 있는 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-132">From here either drag the slider to the desired quantity or enter it in the box next to the slider.</span></span>  

![][2] 

<span data-ttu-id="29516-133">ASE의 ASP에 대한 자동 크기 조정 규칙은 일반적인 경우와 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-133">The autoscale rules for an ASP in an ASE work the same as they do normally.</span></span>  <span data-ttu-id="29516-134">***확장 기준***에 있는 ***CPU 비율***을 선택하여 CPU 비율에 따라 ASP에 대한 자동 크기 조정 규칙을 만들거나 ***일정 및 성능 규칙***을 사용하여 좀 더 복잡한 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-134">You can select ***CPU Percentage*** under ***Scale by*** and create autoscale rules for your ASP based on CPU Percentage or you can create more complex rules using ***schedule and performance rules***.</span></span>  <span data-ttu-id="29516-135">자동 크기 조정 구성에 관하여 전체 세부 정보를 자세히 보려면 [Azure App Service에서 앱 확장][AppScale] 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29516-135">To see more complete details on configuring autoscale use the guide here [Scale an app in Azure App Service][AppScale].</span></span> 

### <a name="worker-pool-selection"></a><span data-ttu-id="29516-136">작업자 풀 선택</span><span class="sxs-lookup"><span data-stu-id="29516-136">Worker Pool selection</span></span>
<span data-ttu-id="29516-137">앞에서 언급한 것처럼 작업자 풀 선택은 ASP UI에서 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-137">As noted earlier, the worker pool selection is accessed from the ASP UI.</span></span>  <span data-ttu-id="29516-138">확장하려는 ASP의 블레이드를 열고 작업자 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-138">Open the blade for the ASP that you want to scale and select worker pool.</span></span>  <span data-ttu-id="29516-139">앱 서비스 환경에서 구성한 모든 작업자 풀이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-139">You will see all of the worker pools which you have configured in your App Service Environment.</span></span>  <span data-ttu-id="29516-140">작업자 풀이 하나뿐인 경우에는 하나의 풀만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-140">If you have only one worker pool then you will only see the one pool listed.</span></span>  <span data-ttu-id="29516-141">ASP가 있는 작업자 풀을 변경하려면 앱 서비스 계획을 이동할 작업자 풀을 선택하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-141">To change what worker pool your ASP is in, you simply select the worker pool you want your App Service Plan to move to.</span></span>  

![][3]

<span data-ttu-id="29516-142">한 작업자 풀에서 다른 작업자 풀로 ASP를 이동하기 전에 ASP에 대해 적절한 용량이 있는지 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-142">Before moving your ASP from one worker pool to another it is important to make sure you will have adequate capacity for your ASP.</span></span>  <span data-ttu-id="29516-143">작업자 풀 목록에는 작업자 풀 이름이 나열될 뿐만 아니라 해당 작업자 풀에서 사용 가능한 작업자 수도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-143">In the list of worker pools, not only is the worker pool name listed but you can also see how many workers are available in that worker pool.</span></span>  <span data-ttu-id="29516-144">앱 서비스 계획을 포함할 수 있는 충분한 인스턴스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-144">Make sure that there are enough instances available to contain your App Service Plan.</span></span>  <span data-ttu-id="29516-145">이동할 작업자 풀에 추가 계산 리소스가 필요한 경우 ASE 관리자에게 추가하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-145">If you need more compute resources in the worker pool you wish to move to, then get your ASE administrator to add them.</span></span>  

> [!NOTE]
> <span data-ttu-id="29516-146">한 작업자 풀에서 ASP를 이동하면 해당 ASP에서 앱이 콜드 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="29516-146">Moving an ASP from one worker pool will cause cold starts of the apps in that ASP.</span></span>  <span data-ttu-id="29516-147">이렇게 하면 앱이 새 계산 리소스에서 시작할 때 요청이 느리게 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-147">This can cause requests to run slowly as your app is cold started on the new compute resources.</span></span>  <span data-ttu-id="29516-148">Azure App Service에서 [응용 프로그램 준비 기능][AppWarmup]을 사용하여 콜드 부팅을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29516-148">The cold start can be avoided by using the [application warm up capability][AppWarmup] in Azure App Service.</span></span>  <span data-ttu-id="29516-149">앱이 새 계산 리소스에서 콜드 시작하는 경우에 초기화 프로세스가 호출되기 때문에 문서에서 설명하는 응용 프로그램 초기화 모듈은 콜드 시작에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="29516-149">The Application Initialization module described in the article also works for cold starts because the initialization process is also invoked when apps are cold started on new compute resources.</span></span> 
> 
> 

## <a name="getting-started"></a><span data-ttu-id="29516-150">시작</span><span class="sxs-lookup"><span data-stu-id="29516-150">Getting started</span></span>
<span data-ttu-id="29516-151">App Service 환경을 시작하려면 [App Service 환경을 만드는 방법][HowtoCreateASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29516-151">To get started with App Service Environments, see [How To Create An App Service Environment][HowtoCreateASE]</span></span>

<span data-ttu-id="29516-152">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service][AzureAppService]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29516-152">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
