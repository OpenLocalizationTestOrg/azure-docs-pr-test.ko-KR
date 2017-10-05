---
title: "App Service Environment v1에서 웹앱 만들기"
description: "App Service Environment v1에서 웹앱 및 App Service 계획을 만드는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 0779486b040b8dc51cdd42521ba965e58388425a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a><span data-ttu-id="c8521-103">App Service Environment v1에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c8521-103">Create a web app in an App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="c8521-104">이 문서는 ASE(App Service Environment) v1에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="c8521-105">사용하기가 더 쉽고 더 강력한 인프라에서 실행되는 최신 버전의 App Service Environment가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="c8521-106">새 버전에 대한 자세한 내용은 [App Service Environment 소개](../app-service/app-service-environment/intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="c8521-107">개요</span><span class="sxs-lookup"><span data-stu-id="c8521-107">Overview</span></span>
<span data-ttu-id="c8521-108">이 자습서는 [ASE(App Service Environment) v1](app-service-app-service-environment-intro.md)에서 웹앱 및 App Service 계획을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-108">This tutorial shows how to create web apps and App Service plans in an [App Service Environment v1](app-service-app-service-environment-intro.md) (ASE).</span></span> 

> [!NOTE]
> <span data-ttu-id="c8521-109">웹앱을 만드는 방법을 알아보지만 앱 서비스 환경이 아니어도 된다면 [.NET 웹앱 만들기](app-service-web-get-started-dotnet.md) 또는 기타 언어와 프레임워크에 관련된 자습서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-109">If you want to learn how to create a web app but don't need to do it in an App Service Environment, see [Create a .NET web app](app-service-web-get-started-dotnet.md) or one of the related tutorials for other languages and frameworks.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c8521-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c8521-110">Prerequisites</span></span>
<span data-ttu-id="c8521-111">이 자습서는 앱 서비스 환경을 만든 적이 있는 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-111">This tutorial assumes you have created an App Service Environment.</span></span> <span data-ttu-id="c8521-112">만들어 본 적이 없는 경우 [앱 서비스 환경 만들기](app-service-web-how-to-create-an-app-service-environment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-112">If you haven't done that yet, see [Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="c8521-113">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c8521-113">Create a web app</span></span>
1. <span data-ttu-id="c8521-114">[Azure Portal](https://portal.azure.com/)에서 **새로 만들기 > 웹 + 모바일 > 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-114">In the [Azure Portal](https://portal.azure.com/), click **New > Web + Mobile > Web App**.</span></span> 
   
    ![][1]
2. <span data-ttu-id="c8521-115">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-115">Select your subscription.</span></span>  
   
    <span data-ttu-id="c8521-116">여러 구독이 있는 경우 앱 서비스 환경의 앱을 만들려면 환경을 만드는 데 사용한 동일한 구독을 사용해야 한다는 점에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-116">If you have multiple subscriptions be aware that to create an app in your App Service Environment, you need to use the same subscription that you used when creating the environment.</span></span> 
3. <span data-ttu-id="c8521-117">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-117">Select or create a resource group.</span></span>
   
    <span data-ttu-id="c8521-118">*리소스 그룹*을 통해 관련 Azure 리소스를 하나의 단위로 관리할 수 있으며 앱에 대해 *역할 기반 액세스 제어*(RBAC) 규칙을 설정할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-118">*Resource groups* enable you to manage related Azure resources as a unit and are useful when establishing *role-based access control* (RBAC) rules for your apps.</span></span> <span data-ttu-id="c8521-119">자세한 내용은 [Azure Resource Manager 개요][ResourceGroups]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-119">For more information, see [Azure Resource Manager overview][ResourceGroups].</span></span> 
4. <span data-ttu-id="c8521-120">앱 서비스 계획을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-120">Select or create an App Service plan.</span></span>
   
    <span data-ttu-id="c8521-121">*App Service 계획*은 관리되는 웹앱 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-121">*App Service plans* are managed sets of web apps.</span></span>  <span data-ttu-id="c8521-122">일반적으로 가격 책정을 선택하면 개별 앱이 아니라 앱 서비스 계획에 청구되는 가격이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-122">Normally when you select pricing, the price charged is applied to the App Service plan rather than to the individual apps.</span></span> <span data-ttu-id="c8521-123">ASE에서는 ASP와 함께 표시된 계산 인스턴스가 아니라 ASE에 할당된 계산 인스턴스에 대해 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-123">In an ASE you pay for the compute instances allocated to the ASE rather than what you have listed with your ASP.</span></span>  <span data-ttu-id="c8521-124">웹앱의 인스턴스 수를 늘리려면 앱 서비스 계획 인스턴스를 늘립니다. 그러면 해당 계획의 모든 웹앱에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-124">To scale up the number of instances of a web app you scale up the instances of your App Service plan and it affects all of the web apps in that plan.</span></span>  <span data-ttu-id="c8521-125">사이트 슬롯 또는 VNET 통합과 같은 일부 기능에는 계획 내 수량 제한도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-125">Some features such as site slots or VNET Integration also have quantity restrictions within the plan.</span></span>  <span data-ttu-id="c8521-126">자세한 내용은 [Azure App Service 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-126">For more information, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>
   
    <span data-ttu-id="c8521-127">계획 이름에서 설명한 위치를 확인하여 ASE의 앱 서비스 계획을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-127">You can identify the App Service plans in your ASE by looking at the location that is noted under the plan name.</span></span>  
   
    ![][5]
   
    <span data-ttu-id="c8521-128">앱 서비스 환경에 이미 존재하는 앱 서비스 계획을 사용하려는 경우 해당 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-128">If you want to use an App Service plan that already exists in your App Service Environment, select that plan.</span></span> <span data-ttu-id="c8521-129">새로운 앱 서비스 계획을 만들려는 경우 이 자습서의 다음 섹션인 [앱 서비스 환경에서 앱 서비스 계획 만들기](#createplan)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-129">If you want to create a new App Service plan, see the following section of this tutorial, [Create an App Service plan in an App Service Environment](#createplan).</span></span>
5. <span data-ttu-id="c8521-130">웹앱에 이름을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-130">Enter the name for your web app, and then click **Create**.</span></span> 
   
    <span data-ttu-id="c8521-131">ASE에서 외부 VIP를 사용하는 경우 ASE의 앱 URL은 [*사이트 이름*].azurewebsites.net 대신 [*사이트 이름*].[*앱 서비스 환경의 이름*].p.azurewebsites.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-131">If your ASE uses an External VIP the URL of an app in an ASE is:  [*sitename*].[*name of your App Service Environment*].p.azurewebsites.net  instead of  [*sitename*].azurewebsites.net</span></span>
   
    <span data-ttu-id="c8521-132">ASE에서 내부 VIP를 사용하는 경우 해당 ASE에 있는 앱의 URL은 [*사이트 이름*].[*ASE 생성 중에 지정된 하위 도메인*]과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-132">If your ASE uses an Internal VIP then the URL of an app in that ASE is: [*sitename*].[*subdomain specified during ASE creation*]</span></span>   
    <span data-ttu-id="c8521-133">ASE 생성 중에 ASP를 선택한 후 **이름**에서 하위 도메인 업데이트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-133">After you select your ASP during ASE creation you will see the subdomain update below **Name**</span></span>

## <span data-ttu-id="c8521-134"><a name="createplan"></a> 앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="c8521-134"><a name="createplan"></a> Create an App Service plan</span></span>
<span data-ttu-id="c8521-135">앱 서비스 환경에서 앱 서비스 계획을 만들 때 ASE에 공유 작업자가 없기 때문에 작업자 선택이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-135">When you create an App Service plan in an App Service Environment, your worker choices are different as there are no shared workers in an ASE.</span></span>  <span data-ttu-id="c8521-136">사용해야 하는 작업자는 관리자에 의해 ASE에 할당된 작업자입니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-136">The workers you have to use are the ones that have been allocated to the ASE by the admin.</span></span>  <span data-ttu-id="c8521-137">즉, 새 계획을 만들려면 ASE 작업자 풀에 할당된 수가 작업자 풀의 모든 계획에서 전체 인스턴스 수보다 많아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-137">This means that to create a new plan, you need to have more workers allocated to your ASE worker pool than the total number of instances across all of your plans already in that worker pool.</span></span>  <span data-ttu-id="c8521-138">ASE 작업자 풀의 작업자 수가 부족하여 계획을 만들 수 없는 경우 ASE 관리자와 함께 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-138">If you don't have enough workers in your ASE worker pool to create your plan, you need to work with your ASE admin to get them added.</span></span>

<span data-ttu-id="c8521-139">앱 서비스 환경에서 호스팅되는 앱 서비스 계획의 또 다른 차이점은 가격 책정을 선택할 수 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-139">Another difference with App Service plans hosted by an App Service Environment is the lack of pricing selection.</span></span>  <span data-ttu-id="c8521-140">앱 서비스 환경이 있는 경우 시스템에서 사용되는 계산 리소스에 대한 비용을 지불하며 해당 환경의 계획에 대한 추가 요금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-140">When you have an App Service Environment you are paying for compute resources used by the system and do not have added charges for the plans in that environment.</span></span>  <span data-ttu-id="c8521-141">일반적으로 앱 서비스 계획을 만들 때 청구를 결정하는 가격 책정 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-141">Normally when you create an App Service plan you select a pricing plan which determines your billing.</span></span>  <span data-ttu-id="c8521-142">앱 서비스 환경은 기본적으로 콘텐츠를 만들 수 있는 개인 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-142">An App Service Environment is essentially a private location where you can create content.</span></span>  <span data-ttu-id="c8521-143">따라서 콘텐츠 호스트 비용이 아니라 환경에 대한 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-143">You pay for the environment and not to host your content.</span></span>

<span data-ttu-id="c8521-144">다음 지침에는 자습서의 이전 섹션에서 설명한 대로 웹앱을 만드는 동안 앱 서비스 계획을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-144">The following instructions show how to create an App Service plan while you are creating a web app as explained in the previous section of the tutorial.</span></span>

1. <span data-ttu-id="c8521-145">계획 선택 UI에서 **새로 만들기** 를 클릭하고 ASE 외부에서 일반적으로 하는 대로 계획에 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-145">Click **Create New** in the plan selection UI and provide a name for your plan just as you normally would outside of an ASE.</span></span>
2. <span data-ttu-id="c8521-146">위치 선택에서 사용하려는 ASE를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-146">Select the ASE that you want to use from your location picker.</span></span>
   
    <span data-ttu-id="c8521-147">앱 서비스 환경이 기본적으로 개인 배포 위치이기 때문에 위치에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-147">Because an App Service Environment is essentially a private deployment location, it shows under Location.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="c8521-148">위치 선택에서 ASE를 선택한 후에 앱 서비스 계획 생성 UI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-148">After selection of an ASE in the location picker, the App Service plan creation UI updates.</span></span>  <span data-ttu-id="c8521-149">위치는 ASE 시스템의 이름 및 지역을 표시하고 가격 책정 계획 선택은 작업자 풀 선택으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-149">The location now shows the name of the ASE system and the region it is in, and the pricing plan picker is replaced with a worker pool picker.</span></span>  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a><span data-ttu-id="c8521-150">작업자 풀 선택</span><span class="sxs-lookup"><span data-stu-id="c8521-150">Selecting a worker pool</span></span>
<span data-ttu-id="c8521-151">일반적으로 Azure 앱 서비스 내부와 앱 서비스 환경 외부에는 전용 가격 계획을 선택할 때 사용할 수 있는 3가지 계산 크기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-151">Normally in Azure App Service and outside of an App Service Environment, there are 3 compute sizes that are available with the selection of a dedicated price plan.</span></span>  <span data-ttu-id="c8521-152">마찬가지로 ASE의 경우 최대 3개의 작업자 풀을 정의하고 해당 작업자 풀에 사용되는 계산 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-152">In a similar fashion, for an ASE you can define up to 3 pools of workers and specify the compute size that is used for that worker pool.</span></span>  <span data-ttu-id="c8521-153">ASE의 테넌트와 관련하여 앱 서비스 계획에 대해 가격 책정 계획을 계산 크기로 선택하는 대신 *작업자 풀*이라는 것을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-153">What that means for tenants of the ASE is that instead of selecting a pricing plan with compute size for your App Service plan, you select what is called a *worker pool*.</span></span>  

<span data-ttu-id="c8521-154">작업자 풀 선택 UI에는 작업자 풀 이름 아래에 해당 작업자 풀에 사용되는 계산 크기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-154">The worker pool selection UI shows the compute size used for that worker pool below the name.</span></span>  <span data-ttu-id="c8521-155">사용 가능한 양은 해당 풀에서 사용할 수 있는 계산 인스턴스 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-155">The quantity available refers to how many compute instances are available for use in that pool.</span></span>  <span data-ttu-id="c8521-156">실제로 전체 풀에는 이보다 많은 인스턴스가 있을 수 있지만 이 값은 현재 사용 중이지 않은 개수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-156">The total pool may actually have more instances than this number but this value refers to simply how many are not in use.</span></span>  <span data-ttu-id="c8521-157">앱 서비스 환경을 조정하여 계산 리소스를 추가해야 하는 경우 [앱 서비스 환경 구성](app-service-web-configure-an-app-service-environment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8521-157">If you need to adjust your App Service Environment to add more compute resources see [Configuring your App Service Environment](app-service-web-configure-an-app-service-environment.md).</span></span>

![][4]

<span data-ttu-id="c8521-158">이 예제에서는 사용 가능한 작업자 풀이 두 개뿐인 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-158">In this example you see only two worker pools available.</span></span> <span data-ttu-id="c8521-159">이는 ASE 관리자가 두 개의 작업자 풀에만 호스트를 할당했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-159">That is because the ASE administrator only allocated hosts into those two worker pools.</span></span>  <span data-ttu-id="c8521-160">세 번째 풀은 할당된 VM이 있으면 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-160">The third would show up when there are VMs allocated into it.</span></span>  

## <a name="after-web-app-creation"></a><span data-ttu-id="c8521-161">웹앱을 만든 후</span><span class="sxs-lookup"><span data-stu-id="c8521-161">After web app creation</span></span>
<span data-ttu-id="c8521-162">ASE에서 웹앱을 실행하고 앱 서비스 계획을 관리하기 위해 고려해야 하는 몇 가지 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-162">There are a few considerations for running web apps and managing App Service plans in an ASE that need to be taken into account.</span></span>  

<span data-ttu-id="c8521-163">앞서 설명한 것처럼 ASE 소유자는 시스템의 크기를 관리하므로 원하는 앱 서비스 계획을 호스트할 충분한 용량이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-163">As noted earlier, the owner of the ASE is responsible for the size of the system and as a result they are also responsible for ensuring that there is sufficient capacity to host the desired App Service plans.</span></span> <span data-ttu-id="c8521-164">사용 가능한 작업자가 없으면 앱 서비스 계획을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-164">If there are no available workers, you will not be able to create your App Service plan.</span></span>  <span data-ttu-id="c8521-165">또한 웹앱을 확장할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-165">This is also true to scaling up your web app.</span></span>  <span data-ttu-id="c8521-166">추가 인스턴스가 필요한 경우 앱 서비스 관리자에게 작업자를 추가하도록 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-166">If you need more instances then you would have to get your App Service Environment admin to add more workers.</span></span>

<span data-ttu-id="c8521-167">웹앱과 앱 서비스 계획을 만든 후 이를 확장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-167">After creating your web app and App Service plan it is a good idea to scale it up.</span></span>  <span data-ttu-id="c8521-168">ASE에는 앱에 대한 내결함성을 제공하기 위해 항상 2개 이상의 앱 서비스 계획 인스턴스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-168">In an ASE you always need to have at least 2 instances of your App Service plan to provide fault tolerance for your apps.</span></span>  <span data-ttu-id="c8521-169">ASE에서 앱 서비스 계획의 크기 조정은 앱 서비스 계획 UI 통한 정상적인 조정과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8521-169">Scaling an App Service plan in an ASE is the same as normal through the App Service plan UI.</span></span>  <span data-ttu-id="c8521-170">크기 조정에 대한 자세한 내용은 [앱 서비스 환경에서 웹앱 크기 조정하는 방법](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span><span class="sxs-lookup"><span data-stu-id="c8521-170">For more information about scaling, [How to scale a web app in an App Service Environment](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span></span>

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
