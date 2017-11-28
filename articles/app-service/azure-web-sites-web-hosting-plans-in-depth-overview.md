---
title: "aaaAzure 앱 서비스 계획 심도 깊은 개요 | Microsoft Docs"
description: "Azure 앱 서비스에 대한 앱 서비스 계획의 작동 방식 및 이러한 계획을 통해 관리 환경을 향상시킬 수 있는 방법을 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 규모, 확장성, 앱 서비스 계획, 앱 서비스 비용"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="e7d2e-104">Azure 앱 서비스 계획의 포괄 개요</span><span class="sxs-lookup"><span data-stu-id="e7d2e-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="e7d2e-105">앱 서비스 계획을 사용 하는 실제 리소스 toohost의 hello 컬렉션 응용을 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="e7d2e-106">App Service 계획은 다음을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-106">App Service plans define:</span></span>

- <span data-ttu-id="e7d2e-107">지역(미국 서부, 미국 동부 등)</span><span class="sxs-lookup"><span data-stu-id="e7d2e-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="e7d2e-108">확장 개수(1, 2, 3개 인스턴스 등)</span><span class="sxs-lookup"><span data-stu-id="e7d2e-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="e7d2e-109">인스턴스 크기(소, 중, 대)</span><span class="sxs-lookup"><span data-stu-id="e7d2e-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="e7d2e-110">SKU(무료, 공유, 기본, 표준, 프리미엄)</span><span class="sxs-lookup"><span data-stu-id="e7d2e-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="e7d2e-111">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 Web Apps, Mobile Apps, API Apps, 함수 앱(또는 함수)은 모두 App Service 계획에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="e7d2e-112">앱에서 hello 같은 구독과 지역을 공유할 수 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="e7d2e-113">모든 응용 프로그램 할당 tooan **앱 서비스 계획** 에서 정의한 hello 리소스를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="e7d2e-114">따라서 단일 App Service 계획에서 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="e7d2e-115">프로그램 **앱 서비스 계획** 에서 확장할 수 **무료** 및 **Shared** Sku 너무**기본**, **표준**, 및 **프리미엄** toomore 리소스 및 hello 따라 기능을 제공 하는 Sku 액세스 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="e7d2e-116">앱 서비스 계획에 너무 설정 되어 있으면**기본** SKU 또는 그 이상으로 hello를 제어할 수 있습니다 다음 **크기** hello Vm의 수를 크기 조정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="e7d2e-117">예를 들어 hello standard 서비스 계층에 구성 된 toouse 두 "small" 인스턴스 계획을 사용 하는 경우 해당 계획과 연결 된 모든 앱 인스턴스 모두 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="e7d2e-118">앱은 액세스 toohello standard 서비스 계층 기능을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="e7d2e-119">앱을 실행 중인 계획 인스턴스는 완전히 관리되며 가용성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7d2e-120">hello **SKU** 및 **배율** 의 hello 앱 서비스 계획에 호스팅된 앱 hello 비용과 hello 하지 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="e7d2e-121">이 문서는 hello 키 등의 특성 계층, 앱 서비스 계획의 소수 자릿수 및 앱을 관리 하는 동안 재생 발휘 방법을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="e7d2e-122">앱 및 앱 서비스 계획</span><span class="sxs-lookup"><span data-stu-id="e7d2e-122">Apps and App Service plans</span></span>

<span data-ttu-id="e7d2e-123">앱 서비스의 앱은 주어진 시간에 항상 하나의 앱 서비스 계획에만 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="e7d2e-124">앱과 계획은 둘 다 **리소스 그룹**에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="e7d2e-125">리소스 그룹 내에 있는 모든 리소스에 대 한 hello 수명 주기 경계 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="e7d2e-126">있습니다 수 사용 하 여 리소스 그룹 toomanage 응용 프로그램의 모든 hello 조각을.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="e7d2e-127">단일 리소스 그룹에 앱 서비스 계획을 여러 개 있을 수 있지만, 때문에 다양 한 앱을 toodifferent 물리적 리소스 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="e7d2e-128">예를 들어 개발, 테스트 및 프로덕션 환경 간에 리소스를 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="e7d2e-129">프로덕션 및 개발/테스트에 대해 별도의 환경을 두면 리소스를 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="e7d2e-130">이러한 방식으로 새 버전의 앱에 대해 부하 테스트 경합 하지 않습니다 hello에 대 한 동일한 실제 고객의 서비스를 제공는 프로덕션 응용 프로그램으로 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="e7d2e-131">단일 리소스 그룹에 여러 계획이 있는 경우 지역에 걸쳐 있는 응용 프로그램을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="e7d2e-132">예를 들어 두 개의 지역에서 실행되는 고가용성 앱에는 각 지역별로 하나씩 두 개 이상의 계획이 포함되고 각 계획과 연결된 앱이 하나씩 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="e7d2e-133">이러한 경우 hello 응용 프로그램의 모든 hello 복사본 다음 단일 리소스 그룹에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="e7d2e-134">여러 계획 및 여러 앱에서 있는 리소스 그룹을 사용 하면 쉽게 toomanage, 제어 및 hello 응용 프로그램의 hello 상태 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="e7d2e-135">App Service 계획 만들기 또는 기존 계획 사용</span><span class="sxs-lookup"><span data-stu-id="e7d2e-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="e7d2e-136">앱을 만들 때 리소스 그룹을 만드는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="e7d2e-137">이 앱은 더 큰 응용 프로그램에 대 한 구성 요소를 hello에, 해당 더 큰 응용 프로그램에 할당 되는 hello 리소스 그룹 내에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="e7d2e-138">Hello 앱은 완전히 새로운 응용 프로그램 또는 큰의 일부 인지 선택할 수 있습니다 toouse는 기존 계획 toohost 것 하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="e7d2e-139">이 선택은 용량과 예상 부하에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="e7d2e-140">다음의 경우 새 App Service 계획으로 앱을 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="e7d2e-141">앱이 리소스를 많이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-141">App is resource-intensive.</span></span>
- <span data-ttu-id="e7d2e-142">앱에는 기존 계획에서 호스트 되는 다른 앱에서 hello 다른 배율 인수.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="e7d2e-143">앱에 서로 다른 지역의 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="e7d2e-144">이 방식을 사용하면 앱에 새 리소스 집합을 할당하고 앱을 더 잘 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="e7d2e-145">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="e7d2e-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="e7d2e-146">앱 서비스 환경을 설정한 경우에 hello 설명서 특정 tooApp 서비스 환경 여기을 검토할 수 있습니다: [앱 서비스 환경에 앱 서비스 계획 만들기](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="e7d2e-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="e7d2e-147">앱 서비스 계획 찾아보기 경험 hello 또는 응용 프로그램 생성의 일환으로 빈 앱 서비스 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="e7d2e-148">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로** > **웹 + 모바일**, 선택한 후 **웹 앱** 또는 다른 앱 서비스 응용 프로그램 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Hello Azure 포털에서에서 앱을 만듭니다.][createWebApp]

<span data-ttu-id="e7d2e-150">다음을 선택 하거나 hello hello 새 응용 프로그램에 대 한 앱 서비스 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![앱 서비스 계획을 만듭니다.][createASP]

<span data-ttu-id="e7d2e-152">toocreate 앱 서비스 계획을 클릭 하 여 **[+] Create New**, 형식 hello **앱 서비스 계획** 이름을 지정 하 고 다음 적절 한 선택 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="e7d2e-153">클릭 **가격 책정 계층**, 한 다음 hello 서비스에 대 한 적절 한 가격대를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="e7d2e-154">선택 **모든 보기** 더와 같은 옵션, 가격 책정 tooview **무료** 및 **Shared**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="e7d2e-155">Hello 가격 책정 계층을 선택한 후 클릭 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="e7d2e-156">앱 다른 앱 서비스 계획을 tooa 이동</span><span class="sxs-lookup"><span data-stu-id="e7d2e-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="e7d2e-157">Hello 앱 tooa 다른 앱 서비스 계획을 이동할 수 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e7d2e-158">Hello에 hello 계획 되는 응용 프로그램 계획 간에 이동할 수 있습니다 동일한 리소스 그룹 및 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="e7d2e-159">toomove 앱 tooanother 계획:</span><span class="sxs-lookup"><span data-stu-id="e7d2e-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="e7d2e-160">원하는 toomove toohello 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="e7d2e-161">Hello에 **메뉴**, hello에 대 한 확인 **앱 서비스 계획** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="e7d2e-162">선택 **변경 앱 서비스 계획** toostart hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="e7d2e-163">**앱 서비스 계획 변경** 열립니다 hello **앱 서비스 계획** 선택기입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="e7d2e-164">이 시점에서이 응용 프로그램에는 기존 계획 toomove를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7d2e-165">앱 서비스 계획을 선택 하는 hello. UI hello 다음 기준으로 필터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="e7d2e-166">내에 있는 hello 동일한 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="e7d2e-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="e7d2e-167">동일한 hello에 있는 지리적 위치 영역</span><span class="sxs-lookup"><span data-stu-id="e7d2e-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="e7d2e-168">내에 있는 hello 동일한 웹 공간</span><span class="sxs-lookup"><span data-stu-id="e7d2e-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="e7d2e-169">웹 공간은 서버 리소스의 그룹화를 정의하는 App Service 내의 논리적 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="e7d2e-170">지역 (예: 미국 서 부) 응용 프로그램 서비스를 사용 하는 순서 tooallocate 고객에서 웹 스페이스에 많은 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="e7d2e-171">현재 응용 프로그램 서비스 리소스 수 toobe 웹 스페이스에 간에 이동 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![앱 서비스 계획 선택기입니다.][change]

<span data-ttu-id="e7d2e-173">각 계획에는 고유한 가격 책정 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="e7d2e-174">예를 들어 tooit toouse hello 기능과 hello 표준 계층의 리소스를 할당 하는 모든 앱을 사용 하면 사이트를 무료 계층 tooa 표준 계층에서에서으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="e7d2e-175">응용 프로그램 tooa 다른 앱 서비스 계획 복제</span><span class="sxs-lookup"><span data-stu-id="e7d2e-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="e7d2e-176">Toomove hello 앱 tooa 다른 지역의 경우 하나는 응용 프로그램 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="e7d2e-177">복제를 수행하면 모든 하위 지역의 새로운 또는 기존 App Service 계획으로 앱이 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="e7d2e-178">찾을 수 있습니다 **복제 앱** hello에 **개발 도구** hello 메뉴의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7d2e-179">복제에는 몇 가지 제한이 있으며 [Azure 포털을 사용하여 Azure 앱 서비스 앱 복제](../app-service-web/app-service-web-app-cloning-portal.md)에서 이에 대해 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="e7d2e-180">앱 서비스 계획 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e7d2e-180">Scale an App Service plan</span></span>

<span data-ttu-id="e7d2e-181">세 가지 방법으로 tooscale 계획</span><span class="sxs-lookup"><span data-stu-id="e7d2e-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="e7d2e-182">**변경 hello 계획 가격 책정 계층**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="e7d2e-183">모든 앱 할당 tooit toouse hello 표준 계층의 hello 기능 있으며 hello 기본 계층의 계획에는 변환 된 tooStandard 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="e7d2e-184">**Hello 계획의 인스턴스 크기를 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="e7d2e-185">예를 들어, 작은 인스턴스를 사용 하는 hello 기본 계층의 계획에는 변경 된 toouse 큰 인스턴스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="e7d2e-186">에 해당 계획과 연결 된 모든 앱 hello 추가 메모리와 CPU 리소스를 더 큰 인스턴스 크기 제공 hello 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="e7d2e-187">**Hello 계획 인스턴스 수 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="e7d2e-188">예를 들어 toothree 인스턴스 확장은 표준 계획 크기 조정 된 too10 인스턴스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="e7d2e-189">프리미엄 요금제 too20 인스턴스 (제목 tooavailability) 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="e7d2e-190">에 해당 계획과 연결 된 모든 앱 hello 추가 메모리와 CPU 리소스를 더 큰 인스턴스 개수 제공 hello에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="e7d2e-191">Hello hello를 클릭 하 여 가격 책정 계층 및 인스턴스 크기를 변경할 수 있습니다 **크기 확장** hello 앱 또는 앱 서비스 계획 hello에 대 한 설정 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="e7d2e-192">변경은 toohello 앱 서비스 계획을 적용 하 고 호스트 되는 모든 앱에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![응용 프로그램을 tooscale 값을 설정 합니다.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="e7d2e-194">App Service 계획 정리</span><span class="sxs-lookup"><span data-stu-id="e7d2e-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7d2e-195">**앱 서비스 계획** 한 요금은 계속 청구 tooreserve hello 계산 용량을 계속 있으므로 연결 앱 toothem 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="e7d2e-196">tooavoid 예기치 않은 요금, 앱 서비스 계획에서 호스트 되는 hello 마지막 앱이 삭제 되 면 hello 결과 비어 있는 앱 서비스 계획도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="e7d2e-197">요약</span><span class="sxs-lookup"><span data-stu-id="e7d2e-197">Summary</span></span>

<span data-ttu-id="e7d2e-198">앱 서비스 계획은 앱 간에 공유할 수 있는 기능 및 용량 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="e7d2e-199">앱 서비스 계획은 유연성 tooallocate 특정 앱 tooa 리소스 집합이 hello 및 Azure 리소스 사용률을 최적화할 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="e7d2e-200">이러한 방식으로 테스트 환경의 toosave money를 원하는 경우 여러 앱 간에 계획을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="e7d2e-201">여러 지역과 계획에 걸쳐 크기를 조정하여 프로덕션 환경의 생산량을 최대화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d2e-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e7d2e-202">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="e7d2e-202">What's changed</span></span>

- <span data-ttu-id="e7d2e-203">가이드 toohello 변경 tooApp 웹 사이트 서비스에서에서 참조: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e7d2e-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
