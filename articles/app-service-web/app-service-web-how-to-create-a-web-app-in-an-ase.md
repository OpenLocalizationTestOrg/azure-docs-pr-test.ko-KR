---
title: "앱 서비스 환경 v1의 웹 앱 aaaCreate"
description: "Toocreate 웹 앱 및 앱 서비스 환경 v1에서 앱 서비스 계획 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a><span data-ttu-id="f48ac-103">App Service Environment v1에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f48ac-103">Create a web app in an App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="f48ac-104">앱 서비스 환경 v1 hello에 대 한이 문서는입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="f48ac-105">최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="f48ac-106">hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="f48ac-107">개요</span><span class="sxs-lookup"><span data-stu-id="f48ac-107">Overview</span></span>
<span data-ttu-id="f48ac-108">이 자습서에서는 어떻게 toocreate 웹 앱 및 앱 서비스 계획에 [앱 서비스 환경 v1](app-service-app-service-environment-intro.md) (ASE).</span><span class="sxs-lookup"><span data-stu-id="f48ac-108">This tutorial shows how toocreate web apps and App Service plans in an [App Service Environment v1](app-service-app-service-environment-intro.md) (ASE).</span></span> 

> [!NOTE]
> <span data-ttu-id="f48ac-109">어떻게 toolearn 사용 하려는 경우 toocreate 웹 응용 프로그램 toodo 필요 하지 않은 있지만 앱 서비스 환경에서 참조 [.NET 웹 앱을 만듭니다](app-service-web-get-started-dotnet.md) 또는 다른 언어 및 프레임 워크에 대 한 자습서 관련 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-109">If you want toolearn how toocreate a web app but don't need toodo it in an App Service Environment, see [Create a .NET web app](app-service-web-get-started-dotnet.md) or one of hello related tutorials for other languages and frameworks.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f48ac-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f48ac-110">Prerequisites</span></span>
<span data-ttu-id="f48ac-111">이 자습서는 앱 서비스 환경을 만든 적이 있는 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-111">This tutorial assumes you have created an App Service Environment.</span></span> <span data-ttu-id="f48ac-112">만들어 본 적이 없는 경우 [앱 서비스 환경 만들기](app-service-web-how-to-create-an-app-service-environment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f48ac-112">If you haven't done that yet, see [Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="f48ac-113">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f48ac-113">Create a web app</span></span>
1. <span data-ttu-id="f48ac-114">Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로 만들기 > 웹 + 모바일 > 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-114">In hello [Azure Portal](https://portal.azure.com/), click **New > Web + Mobile > Web App**.</span></span> 
   
    ![][1]
2. <span data-ttu-id="f48ac-115">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-115">Select your subscription.</span></span>  
   
    <span data-ttu-id="f48ac-116">여러 구독이 있는 경우 주의 해야 할 앱 서비스 환경에서 응용 프로그램에서 해당 toocreate, toouse hello hello 환경을 만들 때 사용한 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-116">If you have multiple subscriptions be aware that toocreate an app in your App Service Environment, you need toouse hello same subscription that you used when creating hello environment.</span></span> 
3. <span data-ttu-id="f48ac-117">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-117">Select or create a resource group.</span></span>
   
    <span data-ttu-id="f48ac-118">*리소스 그룹* toomanage 하면 관련 Azure 리소스를 한 단위로 되며 유용 설정할 때 사용 *역할 기반 액세스 제어* 앱에 대 한 규칙 (RBAC).</span><span class="sxs-lookup"><span data-stu-id="f48ac-118">*Resource groups* enable you toomanage related Azure resources as a unit and are useful when establishing *role-based access control* (RBAC) rules for your apps.</span></span> <span data-ttu-id="f48ac-119">자세한 내용은 [Azure Resource Manager 개요][ResourceGroups]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f48ac-119">For more information, see [Azure Resource Manager overview][ResourceGroups].</span></span> 
4. <span data-ttu-id="f48ac-120">앱 서비스 계획을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-120">Select or create an App Service plan.</span></span>
   
    <span data-ttu-id="f48ac-121">*App Service 계획*은 관리되는 웹앱 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-121">*App Service plans* are managed sets of web apps.</span></span>  <span data-ttu-id="f48ac-122">일반적으로 가격을 선택 하면 청구 hello 가격 적용된 toohello toohello 개별 앱 대신 앱 서비스 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-122">Normally when you select pricing, hello price charged is applied toohello App Service plan rather than toohello individual apps.</span></span> <span data-ttu-id="f48ac-123">Hello 계산에 대 한 비용을 지불 ASE에 인스턴스 toohello ASE를 할당 하면 asp 나열 했는지도 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-123">In an ASE you pay for hello compute instances allocated toohello ASE rather than what you have listed with your ASP.</span></span>  <span data-ttu-id="f48ac-124">앱 서비스 계획의 hello 인스턴스를 확장할 tooscale hello 웹 응용 프로그램의 인스턴스 수를 하 고 해당 계획의 hello 웹 앱을 모두 영향을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-124">tooscale up hello number of instances of a web app you scale up hello instances of your App Service plan and it affects all of hello web apps in that plan.</span></span>  <span data-ttu-id="f48ac-125">사이트 슬롯 또는 VNET 통합 같은 일부 기능은 hello 계획 내에서 수량 제한 사항을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-125">Some features such as site slots or VNET Integration also have quantity restrictions within hello plan.</span></span>  <span data-ttu-id="f48ac-126">자세한 내용은 [Azure App Service 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f48ac-126">For more information, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>
   
    <span data-ttu-id="f48ac-127">Hello 계획 이름 아래에서 설명한 hello 위치를 확인 하 여 프로그램 ASE에 hello 앱 서비스 계획을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-127">You can identify hello App Service plans in your ASE by looking at hello location that is noted under hello plan name.</span></span>  
   
    ![][5]
   
    <span data-ttu-id="f48ac-128">앱 서비스 환경에 이미 존재 하는 앱 서비스 계획 toouse를 원하는 경우 해당 계획을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-128">If you want toouse an App Service plan that already exists in your App Service Environment, select that plan.</span></span> <span data-ttu-id="f48ac-129">Toocreate 새 앱 서비스 계획을 사용 하도록 하려는 경우 다음이 자습서의 단원을 hello 참조 [앱 서비스 환경에 앱 서비스 계획 만들기](#createplan)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-129">If you want toocreate a new App Service plan, see hello following section of this tutorial, [Create an App Service plan in an App Service Environment](#createplan).</span></span>
5. <span data-ttu-id="f48ac-130">웹 앱에 대 한 hello 이름을 입력 한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-130">Enter hello name for your web app, and then click **Create**.</span></span> 
   
    <span data-ttu-id="f48ac-131">프로그램 ASE ASE에 응용 프로그램에 대 한 외부 VIP hello URL을 사용 하는 경우: [*sitename*]. [ *앱 서비스 환경 이름*]. 대신 p.azurewebsites.net [*sitename*]. azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f48ac-131">If your ASE uses an External VIP hello URL of an app in an ASE is:  [*sitename*].[*name of your App Service Environment*].p.azurewebsites.net  instead of  [*sitename*].azurewebsites.net</span></span>
   
    <span data-ttu-id="f48ac-132">프로그램 ASE 않다는 ASE 응용 프로그램에 대 한 내부 VIP 다음 hello URL을 사용 하는 경우: [*sitename*]. [ *ASE 만들 때 지정한 하위 도메인*]</span><span class="sxs-lookup"><span data-stu-id="f48ac-132">If your ASE uses an Internal VIP then hello URL of an app in that ASE is: [*sitename*].[*subdomain specified during ASE creation*]</span></span>   
    <span data-ttu-id="f48ac-133">아래 업데이트 hello 하위 도메인을 보게 ASE 만드는 동안 하면 ASP를 선택한 후 **이름**</span><span class="sxs-lookup"><span data-stu-id="f48ac-133">After you select your ASP during ASE creation you will see hello subdomain update below **Name**</span></span>

## <span data-ttu-id="f48ac-134"><a name="createplan"></a> 앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="f48ac-134"><a name="createplan"></a> Create an App Service plan</span></span>
<span data-ttu-id="f48ac-135">앱 서비스 환경에서 앱 서비스 계획을 만들 때 ASE에 공유 작업자가 없기 때문에 작업자 선택이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-135">When you create an App Service plan in an App Service Environment, your worker choices are different as there are no shared workers in an ASE.</span></span>  <span data-ttu-id="f48ac-136">toouse 해야 하는 hello 작업자는 hello hello 관리자 toohello ASE 할당 된 것과  즉, 해당 toocreate 새 계획을 통해 모든 해당 작업자 풀에 이미 있는 관리 toohave hello 총 인스턴스 수 보다 더 많은 할당 된 작업자 tooyour ASE 작업자 풀 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-136">hello workers you have toouse are hello ones that have been allocated toohello ASE by hello admin.  This means that toocreate a new plan, you need toohave more workers allocated tooyour ASE worker pool than hello total number of instances across all of your plans already in that worker pool.</span></span>  <span data-ttu-id="f48ac-137">충분 한 작업자에에서 없는 프로그램 ASE 작업자 풀 toocreate 계획을 추가 하 여 ASE admin tooget와 할 toowork 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-137">If you don't have enough workers in your ASE worker pool toocreate your plan, you need toowork with your ASE admin tooget them added.</span></span>

<span data-ttu-id="f48ac-138">앱 서비스 환경에서 호스트 하는 앱 서비스 계획을 가진 또 다른 차이점은 선택 가격 hello 부족 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-138">Another difference with App Service plans hosted by an App Service Environment is hello lack of pricing selection.</span></span>  <span data-ttu-id="f48ac-139">앱 서비스 환경에 있는 경우 hello 시스템에서 사용 하는 계산 리소스에 대 한 부담 하 고 해당 환경에서 추가 된 요금 hello 계획에 대 한 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-139">When you have an App Service Environment you are paying for compute resources used by hello system and do not have added charges for hello plans in that environment.</span></span>  <span data-ttu-id="f48ac-140">일반적으로 앱 서비스 계획을 만들 때 청구를 결정하는 가격 책정 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-140">Normally when you create an App Service plan you select a pricing plan which determines your billing.</span></span>  <span data-ttu-id="f48ac-141">앱 서비스 환경은 기본적으로 콘텐츠를 만들 수 있는 개인 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-141">An App Service Environment is essentially a private location where you can create content.</span></span>  <span data-ttu-id="f48ac-142">콘텐츠 hello 환경과 하지 toohost에 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-142">You pay for hello environment and not toohost your content.</span></span>

<span data-ttu-id="f48ac-143">hello 한 지침은 다음과 hello hello 자습서의 이전 섹션에 설명 된 대로 웹 응용 프로그램을 만드는 동안 toocreate 앱 서비스 계획 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-143">hello following instructions show how toocreate an App Service plan while you are creating a web app as explained in hello previous section of hello tutorial.</span></span>

1. <span data-ttu-id="f48ac-144">클릭 **새로 만들기** 에 계획 선택 UI hello 하 고 일반적으로 외부 ASE 것 처럼 계획에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-144">Click **Create New** in hello plan selection UI and provide a name for your plan just as you normally would outside of an ASE.</span></span>
2. <span data-ttu-id="f48ac-145">위치 선택에서 toouse 되도록 hello ASE를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-145">Select hello ASE that you want toouse from your location picker.</span></span>
   
    <span data-ttu-id="f48ac-146">앱 서비스 환경이 기본적으로 개인 배포 위치이기 때문에 위치에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-146">Because an App Service Environment is essentially a private deployment location, it shows under Location.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="f48ac-147">Hello 위치 선택에서 ASE 선택한 후 hello 앱 서비스 계획 만들기 UI 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-147">After selection of an ASE in hello location picker, hello App Service plan creation UI updates.</span></span>  <span data-ttu-id="f48ac-148">hello 위치 이제 표시 hello ASE 시스템의 hello 이름과 hello 지역에 고 가격 계획 선택 hello 작업자 풀 선택기 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-148">hello location now shows hello name of hello ASE system and hello region it is in, and hello pricing plan picker is replaced with a worker pool picker.</span></span>  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a><span data-ttu-id="f48ac-149">작업자 풀 선택</span><span class="sxs-lookup"><span data-stu-id="f48ac-149">Selecting a worker pool</span></span>
<span data-ttu-id="f48ac-150">일반적으로 Azure 앱 서비스 및 앱 서비스 환경 외부에서 전용된 가격 계획의 hello 선택 하 여 사용할 수 있는 3 가지 계산 크기는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-150">Normally in Azure App Service and outside of an App Service Environment, there are 3 compute sizes that are available with hello selection of a dedicated price plan.</span></span>  <span data-ttu-id="f48ac-151">유사한 방식 ASE에 대 한 정의 too3 풀의 작업자를 하 고 수 해당 작업자 풀에 사용 되는 hello 계산 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-151">In a similar fashion, for an ASE you can define up too3 pools of workers and specify hello compute size that is used for that worker pool.</span></span>  <span data-ttu-id="f48ac-152">hello ASE 앱 서비스 계획에 대 한 계산 크기가 요금제를 선택 하는 대신 선택 하는 요청 된 것은 테 넌 트에 대 한 의미를 *작업자 풀*합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-152">What that means for tenants of hello ASE is that instead of selecting a pricing plan with compute size for your App Service plan, you select what is called a *worker pool*.</span></span>  

<span data-ttu-id="f48ac-153">hello 작업자 풀 선택 UI hello 이름 아래에 해당 작업자 풀에 사용 되는 hello 계산 크기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-153">hello worker pool selection UI shows hello compute size used for that worker pool below hello name.</span></span>  <span data-ttu-id="f48ac-154">hello 수 있는 수량 참조 toohow 많은 계산 인스턴스는 해당 풀에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-154">hello quantity available refers toohow many compute instances are available for use in that pool.</span></span>  <span data-ttu-id="f48ac-155">hello 총 풀이이 값 보다 더 많은 인스턴스를 포함 실제로 될 수도 있지만이 값이 toosimply 참조 개수 사용 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-155">hello total pool may actually have more instances than this number but this value refers toosimply how many are not in use.</span></span>  <span data-ttu-id="f48ac-156">Tooadjust 해야 할 경우 앱 서비스 환경 tooadd 더 계산 리소스를 참조 하십시오 [앱 서비스 환경 구성](app-service-web-configure-an-app-service-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-156">If you need tooadjust your App Service Environment tooadd more compute resources see [Configuring your App Service Environment](app-service-web-configure-an-app-service-environment.md).</span></span>

![][4]

<span data-ttu-id="f48ac-157">이 예제에서는 사용 가능한 작업자 풀이 두 개뿐인 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-157">In this example you see only two worker pools available.</span></span> <span data-ttu-id="f48ac-158">ASE 관리자에 게 할당 된 호스트를 이러한 두 작업자 풀으로 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-158">That is because hello ASE administrator only allocated hosts into those two worker pools.</span></span>  <span data-ttu-id="f48ac-159">hello 셋째 나타납니다 Vm에 할당 된 경우.</span><span class="sxs-lookup"><span data-stu-id="f48ac-159">hello third would show up when there are VMs allocated into it.</span></span>  

## <a name="after-web-app-creation"></a><span data-ttu-id="f48ac-160">웹앱을 만든 후</span><span class="sxs-lookup"><span data-stu-id="f48ac-160">After web app creation</span></span>
<span data-ttu-id="f48ac-161">실행 중인 웹 응용 프로그램 및 toobe 고려를 해야 하는 ASE에 앱 서비스 계획을 관리 하기 위한 몇 가지 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-161">There are a few considerations for running web apps and managing App Service plans in an ASE that need toobe taken into account.</span></span>  

<span data-ttu-id="f48ac-162">Hello ASE hello 소유자가 hello 시스템의 hello 크기에 대해 설명한 것 처럼 있으며 결과적으로 책임에 앱 서비스 계획에 필요한 충분 한 용량 toohost hello 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-162">As noted earlier, hello owner of hello ASE is responsible for hello size of hello system and as a result they are also responsible for ensuring that there is sufficient capacity toohost hello desired App Service plans.</span></span> <span data-ttu-id="f48ac-163">사용 가능한 작업자가 있는 경우는 금지 됩니다 수 toocreate 앱 서비스 계획 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-163">If there are no available workers, you will not be able toocreate your App Service plan.</span></span>  <span data-ttu-id="f48ac-164">웹 앱을 true tooscaling 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-164">This is also true tooscaling up your web app.</span></span>  <span data-ttu-id="f48ac-165">더 많은 인스턴스 필요한 경우 tooget 앱 서비스 환경 관리 tooadd 해야 추가 작업 자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-165">If you need more instances then you would have tooget your App Service Environment admin tooadd more workers.</span></span>

<span data-ttu-id="f48ac-166">웹 앱과 앱 서비스 계획을 만든 후 것이 좋습니다 tooscale 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-166">After creating your web app and App Service plan it is a good idea tooscale it up.</span></span>  <span data-ttu-id="f48ac-167">ASE에 항상 응용 프로그램을 위한 하거나 앱 서비스 계획 tooprovide 내결함성 toohave 2 개 이상 인스턴스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48ac-167">In an ASE you always need toohave at least 2 instances of your App Service plan tooprovide fault tolerance for your apps.</span></span>  <span data-ttu-id="f48ac-168">앱 서비스 계획 UI hello를 통해 일반적인 방법으로 동일한 hello ASE에는 계획은 응용 프로그램 서비스를 크기 조정.</span><span class="sxs-lookup"><span data-stu-id="f48ac-168">Scaling an App Service plan in an ASE is hello same as normal through hello App Service plan UI.</span></span>  <span data-ttu-id="f48ac-169">를 확장 하는 방법에 대 한 자세한 내용은 [어떻게 tooscale 앱 서비스 환경에 웹 앱](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span><span class="sxs-lookup"><span data-stu-id="f48ac-169">For more information about scaling, [How tooscale a web app in an App Service Environment](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span></span>

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
