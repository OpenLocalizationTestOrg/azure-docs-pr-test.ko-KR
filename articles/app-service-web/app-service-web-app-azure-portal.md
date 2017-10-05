---
title: "Azure 포털 탐색을 위한 참조"
description: "앱 서비스 웹에 대한 사용자 환경과 관련해서 관리 포털과 Azure 포털 간의 차이점을 알아봅니다."
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="0315d-103">Azure 포털 탐색을 위한 참조</span><span class="sxs-lookup"><span data-stu-id="0315d-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="0315d-104">Azure 웹 사이트를 이제 [앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="0315d-105">이 이름 변경을 반영하고 Azure 포털에 대한 지침을 제공하기 위해 모든 설명서를 업데이트하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="0315d-106">해당 프로세스가 완료될 때까지 이 문서를 Azure 포털의 웹앱 작업을 위한 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="0315d-107">Azure 클래식 포털의 미래</span><span class="sxs-lookup"><span data-stu-id="0315d-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="0315d-108">Azure 클래식 포털의 브랜딩 변경과 더불어 해당 포털도 Azure 포털로 대체되는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="0315d-109">클래식 포털이 단계적으로 중단됨에 따라 새 개발의 포커스도 Azure 포털로 전환되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="0315d-110">웹앱에 대해 제공될 예정인 모든 새 기능은 Azure 포털에서 소개됩니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="0315d-111">웹앱이 제공하는 가장 강력한 최신 기능을 이용하려면 Azure 포털을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="0315d-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="0315d-112">Azure 클래식 포털과 Azure 포털 간의 레이아웃 차이점</span><span class="sxs-lookup"><span data-stu-id="0315d-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="0315d-113">클래식 포털에서는 모든 Azure 서비스가 왼쪽에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="0315d-114">클래식 포털의 탐색은 트리 구조를 따르므로 서비스부터 시작하여 각 요소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="0315d-115">이 구조는 독립 구성 요소를 관리할 때 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="0315d-116">그러나 Azure에서 빌드된 응용 프로그램은 상호 연결된 서비스 컬렉션이며 이 트리 구조는 서비스 컬렉션 작업에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="0315d-117">Azure 포털에서는 여러 서비스의 구성 요소로 종단 간 응용 프로그램을 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="0315d-118">포털은 *추이*로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="0315d-119">*추이*는 다양한 구성 요소의 컨테이너인 일련의 *블레이드*입니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="0315d-120">예를 들어 웹앱에 대해 자동 크기 조정을 설정하는 작업은 다음 예제와 같이 **웹 사이트** 블레이드(해당 블레이드 제목은 아직 새 용어를 사용하도록 업데이트되지 않음), **설정** 블레이드, **규모 확장** 블레이드 등의 여러 블레이드를 안내하는 *추이*입니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="0315d-121">예제에서 자동 크기 조정은 CPU 사용에 종속되도록 설정되므로 **CPU 백분율** 블레이드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="0315d-122">*블레이드* 내의 구성 요소를 *파트*라고 하며 타일과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="0315d-123">탐색 예제: 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0315d-123">Navigation example: create a web app</span></span>
<span data-ttu-id="0315d-124">새 웹앱을 만드는 작업은 여전히 1-2-3만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="0315d-125">다음 이미지는 클래식 포털과 포털을 나란히 표시하여 웹앱을 작동하고 실행하는 데 필요한 단계 수가 많이 변경되지 않았음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="0315d-126">포털에서는 WordPress와 같은 인기 있는 갤러리 응용 프로그램을 포함하여 가장 일반적인 유형의 웹앱에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="0315d-127">사용 가능한 응용 프로그램의 전체 목록은 [Azure 마켓플레이스]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0315d-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="0315d-128">웹앱을 만드는 경우 클래식 포털과 마찬가지로 포털에서 URL, 앱 서비스 계획 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="0315d-129">또한 포털에서는 다른 일반적인 설정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="0315d-130">예를 들어 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 사용하면 관련된 Azure 리소스를 간단하게 확인하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="0315d-131">탐색 예제: 설정 및 기능</span><span class="sxs-lookup"><span data-stu-id="0315d-131">Navigation example: settings and features</span></span>
<span data-ttu-id="0315d-132">이제 모든 설정과 기능이 논리적으로 단일 블레이드에 그룹화되며, 이 블레이드에서 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="0315d-133">예를 들어 **설정** 블레이드에서 **사용자 지정 도메인 및 SSL**을 클릭하여 사용자 지정 도메인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="0315d-134">모니터링 경고를 설정하려면 **요청 및 오류**를 클릭한 다음 **경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="0315d-135">진단을 사용하도록 설정하려면 **설정** 블레이드에서 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="0315d-136">응용 프로그램 설정을 구성하려면 **설정** 블레이드에서 **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="0315d-137">브랜드 이름 외에 포털의 몇 가지 항목이 찾기 쉽도록 이름이 바뀌거나 다르게 그룹화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="0315d-138">예를 들어 다음은 클래식 포털의 앱 설정(**구성**)에 해당하는 페이지의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="0315d-139">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0315d-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="0315d-140">[Azure 마켓플레이스]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="0315d-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="0315d-141">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0315d-142">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0315d-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="0315d-143">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="0315d-143">What's changed</span></span>
* <span data-ttu-id="0315d-144">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure App Service와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0315d-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

