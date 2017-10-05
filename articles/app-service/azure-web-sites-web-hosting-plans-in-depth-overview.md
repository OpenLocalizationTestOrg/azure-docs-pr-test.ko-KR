---
title: "Azure App Service 계획의 포괄 개요 | Microsoft Docs"
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
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="626c7-104">Azure 앱 서비스 계획의 포괄 개요</span><span class="sxs-lookup"><span data-stu-id="626c7-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="626c7-105">App Service 계획은 앱을 호스트하는 데 사용되는 실제 리소스의 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="626c7-106">App Service 계획은 다음을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-106">App Service plans define:</span></span>

- <span data-ttu-id="626c7-107">지역(미국 서부, 미국 동부 등)</span><span class="sxs-lookup"><span data-stu-id="626c7-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="626c7-108">확장 개수(1, 2, 3개 인스턴스 등)</span><span class="sxs-lookup"><span data-stu-id="626c7-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="626c7-109">인스턴스 크기(소, 중, 대)</span><span class="sxs-lookup"><span data-stu-id="626c7-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="626c7-110">SKU(무료, 공유, 기본, 표준, 프리미엄)</span><span class="sxs-lookup"><span data-stu-id="626c7-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="626c7-111">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 Web Apps, Mobile Apps, API Apps, 함수 앱(또는 함수)은 모두 App Service 계획에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="626c7-112">동일한 구독 및 하위 지역의 앱은 App Service 계획을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="626c7-113">**App Service 계획**에 할당된 모든 응용 프로그램은 정의된 리소스를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="626c7-114">따라서 단일 App Service 계획에서 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="626c7-115">**App Service 계획**은 **무료** 및 **공유** SKU에서 **기본**, **표준**, **프리미엄** SKU로 확장하여 이에 따라 더 많은 리소스 및 기능에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="626c7-116">App Service 계획이 **기본** SKU 이상으로 설정되면 VM **크기** 및 확장 개수를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="626c7-117">예를 들어 계획이 표준 서비스 계층의 "작은" 인스턴스 2개를 사용하도록 구성되어 있으면 해당 계획과 연결된 모든 앱이 두 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="626c7-118">앱은 표준 서비스 계층 기능에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="626c7-119">앱을 실행 중인 계획 인스턴스는 완전히 관리되며 가용성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="626c7-120">App Service 계획의 **SKU** 및 **규모**에 따라 호스트되는 앱 수가 아닌 비용이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="626c7-121">이 문서에서는 App Service 계획의 계층 및 크기와 앱을 관리하는 동안 계획이 진행되는 방식과 같은 주요 특징을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="626c7-122">앱 및 앱 서비스 계획</span><span class="sxs-lookup"><span data-stu-id="626c7-122">Apps and App Service plans</span></span>

<span data-ttu-id="626c7-123">앱 서비스의 앱은 주어진 시간에 항상 하나의 앱 서비스 계획에만 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="626c7-124">앱과 계획은 둘 다 **리소스 그룹**에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="626c7-125">리소스 그룹은 그룹 내에 포함된 모든 리소스에 대한 수명 주기 경계 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="626c7-126">리소스 그룹을 사용하여 응용 프로그램의 모든 부분을 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="626c7-127">단일 리소스 그룹은 여러 앱 서비스 계획을 가질 수 있으므로 각 물리적 리소스에 다른 앱을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="626c7-128">예를 들어 개발, 테스트 및 프로덕션 환경 간에 리소스를 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="626c7-129">프로덕션 및 개발/테스트에 대해 별도의 환경을 두면 리소스를 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="626c7-130">이렇게 하면 새 버전의 앱에 대한 부하 테스트가 실제 고객에게 서비스를 제공하는 프로덕션 앱과 동일한 리소스를 경쟁하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="626c7-131">단일 리소스 그룹에 여러 계획이 있는 경우 지역에 걸쳐 있는 응용 프로그램을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="626c7-132">예를 들어 두 개의 지역에서 실행되는 고가용성 앱에는 각 지역별로 하나씩 두 개 이상의 계획이 포함되고 각 계획과 연결된 앱이 하나씩 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="626c7-133">이러한 경우 앱의 모든 복사본이 단일 리소스 그룹에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="626c7-134">여러 계획과 여러 앱을 포함하는 하나의 리소스 그룹이 있으면 응용 프로그램의 상태를 쉽게 관리, 제어 및 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="626c7-135">App Service 계획 만들기 또는 기존 계획 사용</span><span class="sxs-lookup"><span data-stu-id="626c7-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="626c7-136">앱을 만들 때 리소스 그룹을 만드는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="626c7-137">반면, 앱이 대규모 응용 프로그램의 구성 요소인 경우 대규모 응용 프로그램에 대해 할당된 리소스 그룹 내에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="626c7-138">앱이 완전히 새로운 응용 프로그램이든, 대규모 응용 프로그램의 일부이든 관계없이 기존 계획을 사용하여 앱을 호스트하거나 새 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="626c7-139">이 선택은 용량과 예상 부하에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="626c7-140">다음의 경우 새 App Service 계획으로 앱을 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="626c7-141">앱이 리소스를 많이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-141">App is resource-intensive.</span></span>
- <span data-ttu-id="626c7-142">앱의 크기 조정 인수가 기존 계획에서 호스트되는 다른 앱과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="626c7-143">앱에 서로 다른 지역의 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="626c7-144">이 방식을 사용하면 앱에 새 리소스 집합을 할당하고 앱을 더 잘 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="626c7-145">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="626c7-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="626c7-146">App Service Environment가 있는 경우 [App Service Environment에서 App Service 계획 만들기](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)에서 App Service Environment와 관련된 설명서를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="626c7-147">앱 서비스 계획 찾아보기 환경에서 또는 앱 만들기 과정의 일부로 빈 앱 서비스 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="626c7-148">[Azure Portal](https://portal.azure.com)에서 **새로 만들기** > **웹+모바일**을 클릭하고 **웹앱** 또는 다른 App Service 앱 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Azure Portal에서 앱을 만듭니다.][createWebApp]

<span data-ttu-id="626c7-150">그런 다음 새 앱에 대한 앱 서비스 계획을 선택하거나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-150">You can then select or create the App Service plan for the new app.</span></span>

 ![앱 서비스 계획을 만듭니다.][createASP]

<span data-ttu-id="626c7-152">새 App Service 계획을 만들려면 **[+] 새로 만들기**를 클릭하고 **App Service 계획** 이름을 입력한 다음 적절한 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="626c7-153">**가격 책정 계층**을 클릭한 다음 서비스에 대한 적절한 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="626c7-154">**무료** 및 **공유** 등의 더 많은 가격 책정 옵션을 보려면 **모두 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="626c7-155">가격 책정 계층을 선택한 다음 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="626c7-156">다른 앱 서비스 계획으로 앱 이동</span><span class="sxs-lookup"><span data-stu-id="626c7-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="626c7-157">[Azure Portal](https://portal.azure.com)에서 앱을 다른 App Service 계획으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="626c7-158">계획이 동일한 리소스 그룹 및 지리적 지역에 있는 한 계획 간에 앱을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="626c7-159">앱을 다른 계획으로 이동하려면:</span><span class="sxs-lookup"><span data-stu-id="626c7-159">To move an app to another plan:</span></span>

- <span data-ttu-id="626c7-160">이동하려는 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="626c7-161">**메뉴**에서 **App Service 계획** 섹션을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="626c7-162">**App Service 계획 변경**을 선택하여 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="626c7-163">**App Service 계획 변경**이 열리면서 **App Service 계획** 선택 기능이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="626c7-164">이때 이 앱을 이동할 기존 계획을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="626c7-165">선택한 App Service 계획 UI는 다음 기준으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="626c7-166">동일한 리소스 그룹 내에 존재</span><span class="sxs-lookup"><span data-stu-id="626c7-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="626c7-167">동일한 지리적 지역에 존재</span><span class="sxs-lookup"><span data-stu-id="626c7-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="626c7-168">동일한 웹 공간 내에 존재</span><span class="sxs-lookup"><span data-stu-id="626c7-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="626c7-169">웹 공간은 서버 리소스의 그룹화를 정의하는 App Service 내의 논리적 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="626c7-170">지리적 지역(예: 미국 서부)에는 App Service를 사용하여 고객을 할당하기 위한 여러 웹 공간이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="626c7-171">현재 App Service 리소스는 웹 공간 간에 이동될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![앱 서비스 계획 선택기입니다.][change]

<span data-ttu-id="626c7-173">각 계획에는 고유한 가격 책정 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="626c7-174">예를 들어 무료 계층에서 표준 계층으로 사이트를 이동하면 여기에 할당된 모든 앱이 표준 계층의 기능과 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="626c7-175">앱을 다른 앱 서비스 계획으로 변경</span><span class="sxs-lookup"><span data-stu-id="626c7-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="626c7-176">앱을 다른 지역으로 이동하는 한 가지 대안은 앱 복제입니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="626c7-177">복제를 수행하면 모든 하위 지역의 새로운 또는 기존 App Service 계획으로 앱이 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="626c7-178">메뉴의 **개발 도구** 섹션에서 **앱 복제**를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="626c7-179">복제에는 몇 가지 제한이 있으며 [Azure 포털을 사용하여 Azure 앱 서비스 앱 복제](../app-service-web/app-service-web-app-cloning-portal.md)에서 이에 대해 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="626c7-180">앱 서비스 계획 크기 조정</span><span class="sxs-lookup"><span data-stu-id="626c7-180">Scale an App Service plan</span></span>

<span data-ttu-id="626c7-181">계획의 크기를 조정하는 세 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="626c7-182">**계획의 가격 책정 계층을 변경합니다**.</span><span class="sxs-lookup"><span data-stu-id="626c7-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="626c7-183">기본 계층의 계획을 표준 계층으로 변환할 수 있고 여기에 할당된 모든 앱이 표준 계층의 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="626c7-184">**계획의 인스턴스 크기를 변경합니다**.</span><span class="sxs-lookup"><span data-stu-id="626c7-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="626c7-185">예를 들어 작은 인스턴스를 사용하는 기본 계층의 계획을 큰 인스턴스를 사용하도록 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="626c7-186">이제 해당 계획과 연결된 모든 앱이 큰 인스턴스 크기에서 제공하는 추가 메모리 및 CPU 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="626c7-187">**계획의 인스턴스 수를 변경합니다**.</span><span class="sxs-lookup"><span data-stu-id="626c7-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="626c7-188">예를 들어 3개의 인스턴스로 확장되는 표준 계획을 10개의 인스턴스로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="626c7-189">프리미엄 계획은 20개의 인스턴스로 확장될 수 있습니다(가용성에 따라).</span><span class="sxs-lookup"><span data-stu-id="626c7-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="626c7-190">이제 해당 계획과 연결된 모든 앱이 더 많은 인스턴스 수가 제공하는 추가 메모리 및 CPU 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="626c7-191">앱 또는 앱 서비스 계획에 대한 설정에서 **강화** 항목을 클릭하여 가격 책정 계층과 인스턴스 크기를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="626c7-192">변경 내용이 App Service 계획에 적용되고 호스팅하는 모든 앱에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![앱을 강화하도록 값을 설정합니다.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="626c7-194">App Service 계획 정리</span><span class="sxs-lookup"><span data-stu-id="626c7-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="626c7-195">연결된 앱이 없는 **App Service 계획**이더라도 계산 용량을 계속 예약하고 있으므로 여전히 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="626c7-196">예기치 않은 요금이 부과되지 않게 하기 위해 App Service 계획에 마지막으로 호스트된 앱이 삭제될 때 빈 상태가 된 App Service 계획도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="626c7-197">요약</span><span class="sxs-lookup"><span data-stu-id="626c7-197">Summary</span></span>

<span data-ttu-id="626c7-198">앱 서비스 계획은 앱 간에 공유할 수 있는 기능 및 용량 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="626c7-199">앱 서비스 계획은 리소스 집합에 특정 앱을 할당하고 Azure 리소스 사용률을 더욱 최적화하는 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="626c7-200">따라서 테스트 환경에서 비용을 절약하려는 경우 여러 앱에서 계획을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="626c7-201">여러 지역과 계획에 걸쳐 크기를 조정하여 프로덕션 환경의 생산량을 최대화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="626c7-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="626c7-202">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="626c7-202">What's changed</span></span>

- <span data-ttu-id="626c7-203">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="626c7-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
