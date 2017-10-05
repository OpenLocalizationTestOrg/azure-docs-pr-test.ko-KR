---
title: "Azure App Service 및 기존 Azure 서비스에 미치는 영향"
description: "새로운 Azure App Service와 해당 기능이 Azure의 기존 서비스에 미치는 영향을 설명합니다."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="e9d79-103">Azure App Service 및 기존 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="e9d79-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="e9d79-104">이 문서에서는 여러 Azure 서비스를 새로운 통합 제품인 [Azure App Service](https://azure.microsoft.com/services/app-service/)로 결합하는 변경의 일부로 적용된 기존 Azure 서비스의 변경 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="e9d79-105">개요</span><span class="sxs-lookup"><span data-stu-id="e9d79-105">Overview</span></span>
<span data-ttu-id="e9d79-106">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 개발자가 모든 플랫폼 및 장치용 웹앱과 모바일 앱을 만들 수 있게 해주는 고유한 새 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="e9d79-107">App Service는 반복 코딩 기능을 간소화하고 엔터프라이즈 및 SaaS 시스템과 통합되며 보안, 안정성 및 확장성 요구를 충족하는 동시에 비즈니스 프로세스를 자동화하도록 설계된 통합 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="e9d79-108">App Service는 강력한 새 기능을 추가하는 동시에 [웹 사이트](https://azure.microsoft.com/services/websites/), [모바일 서비스](https://azure.microsoft.com/services/mobile-services/) 및 [Biztalk 서비스](https://azure.microsoft.com/services/biztalk-services/)와 같은 기존 Azure 서비스를 하나의 통합 서비스로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="e9d79-109">App Service를 통해 다음과 같은 앱 유형을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="e9d79-110">웹앱</span><span class="sxs-lookup"><span data-stu-id="e9d79-110">Web Apps</span></span>
* <span data-ttu-id="e9d79-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="e9d79-111">Mobile Apps</span></span>
* <span data-ttu-id="e9d79-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="e9d79-112">API Apps</span></span>
* <span data-ttu-id="e9d79-113">논리 앱</span><span class="sxs-lookup"><span data-stu-id="e9d79-113">Logic Apps</span></span>

<span data-ttu-id="e9d79-114">다음 표에서는 기존 Azure 서비스와 App Service 간의 매핑 및 App Service 내에서 사용할 수 있는 앱 유형을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="e9d79-115">기존 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="e9d79-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="e9d79-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e9d79-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="e9d79-117">변경 내용</span><span class="sxs-lookup"><span data-stu-id="e9d79-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="e9d79-118">Azure 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="e9d79-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="e9d79-119">웹앱</span><span class="sxs-lookup"><span data-stu-id="e9d79-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="e9d79-120">Azure 웹 사이트의 경우 App Service가 웹 사이트에서 웹앱으로의 이름 변경만으로 엄격하게 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="e9d79-121">모든 기존 웹 사이트 인스턴스는 이제 App Service에서 웹앱이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="e9d79-122"><em>웹앱</em> 아래에 기존 사이트가 모두 나열되어 있는 <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>을 통해 기존 웹 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="e9d79-123"><em>웹 호스팅 계획</em> 이제 <em>앱 서비스 계획</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="e9d79-124"><em>App Service 계획</em>은 웹앱, Mobile App, 논리 앱 또는 API 앱과 같은 App Service의 모든 앱 유형을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="e9d79-125">Azure App Service 웹앱은 일반 공급됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="e9d79-126"><a href="http://azure.microsoft.com/services/app-service/web/">웹 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="e9d79-127">Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="e9d79-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="e9d79-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="e9d79-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="e9d79-129">모바일 서비스는 독립 실행형 서비스로 계속 사용할 수 있으며 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="e9d79-130">Mobile Apps는 모바일 서비스의 모든 기능과 추가 기능을 통합하는 App Service의 새로운 앱 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="e9d79-131">쉽게 <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">모바일 서비스에서 Mobile Apps로 마이그레이션</a>할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="e9d79-132">App Service의 일부로 Mobile Apps에는 온-프레미스 및 SaaS 시스템과 통합, 스테이징 슬롯, WebJobs, 향상된 크기 조정 옵션 등 모바일 서비스의 범위를 초월한 새 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="e9d79-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">모바일 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="e9d79-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="e9d79-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="e9d79-135">API 앱은 클라우드에서 API를 쉽게 빌드하고 사용할 수 있게 해주는 App Service의 새로운 앱 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="e9d79-136"><a href="http://azure.microsoft.com/services/app-service/api/">API 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="e9d79-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e9d79-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="e9d79-138">논리 앱은 비즈니스 프로세스를 쉽게 자동화할 수 있게 해주는 App Service의 새로운 앱 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="e9d79-139"><a href="http://azure.microsoft.com/services/app-service/logic/">논리 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="e9d79-140">Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="e9d79-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="e9d79-141">BizTalk API 앱</span><span class="sxs-lookup"><span data-stu-id="e9d79-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="e9d79-142">BizTalk 서비스는 독립 실행형 서비스로 계속 사용할 수 있으며 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="e9d79-143">BizTalk 서비스의 모든 기능은 App Service에 API 앱으로 통합되어 사용자가 App Service의 모든 앱 유형에서 엔터프라이즈 응용 프로그램 통합 및 B2B 통합 시나리오를 수행할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="e9d79-144">이제 논리 앱을 사용하여 시각적 디자인 환경을 통해 워크플로를 만들어 비즈니스 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d79-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="e9d79-145">자세한 내용은 [App Service 설명서](https://azure.microsoft.com/documentation/services/app-service/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9d79-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

