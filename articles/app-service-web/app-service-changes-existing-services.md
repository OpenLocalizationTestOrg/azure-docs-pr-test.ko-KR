---
title: "앱 서비스 aaaAzure 및 기존 Azure 서비스에 미치는 영향"
description: "에 대해 설명 어떻게 새 Azure 앱 서비스 hello 및 Azure에서 기존 서비스의 기능에 영향을 줄 합니다."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="ddc88-103">Azure App Service 및 기존 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="ddc88-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="ddc88-104">이 문서에서는 Azure에 몇 가지 Azure 서비스를 함께 hello 변경 toobring의 일부로 서비스는 hello 변경 tooexisting 설명 [Azure 앱 서비스](https://azure.microsoft.com/services/app-service/), 새 통합된 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="ddc88-105">개요</span><span class="sxs-lookup"><span data-stu-id="ddc88-105">Overview</span></span>
<span data-ttu-id="ddc88-106">[Azure 앱 서비스](https://azure.microsoft.com/services/app-service/) 는 새롭고 고유한 클라우드 서비스 개발자가 toocreate 웹 앱 및 모든 플랫폼 및 모든 장치에 대 한 모바일 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="ddc88-107">앱 서비스는 통합된 솔루션 설계 toostreamline 코딩 함수를 반복 하 고 엔터프라이즈 및 SaaS 시스템과 통합 보안, 안정성 및 확장성에 대 한 요구 사항을 충족 하는 동안 비즈니스 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="ddc88-108">앱 서비스 다음 기존 Azure hello 종합 서비스- [웹 사이트](https://azure.microsoft.com/services/websites/), [모바일 서비스](https://azure.microsoft.com/services/mobile-services/), 및 [Biztalk 서비스](https://azure.microsoft.com/services/biztalk-services/) 을 단일 서비스를 결합 하는 동안 강력한 새 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="ddc88-109">앱 서비스 앱 유형에 따라 toohost hello가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="ddc88-110">웹앱</span><span class="sxs-lookup"><span data-stu-id="ddc88-110">Web Apps</span></span>
* <span data-ttu-id="ddc88-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="ddc88-111">Mobile Apps</span></span>
* <span data-ttu-id="ddc88-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="ddc88-112">API Apps</span></span>
* <span data-ttu-id="ddc88-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ddc88-113">Logic Apps</span></span>

<span data-ttu-id="ddc88-114">hello 다음 표에서 설명 방법을 기존 Azure 서비스 tooApp 서비스 및 hello 응용 프로그램 형식을 매핑할 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="ddc88-115">기존 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="ddc88-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="ddc88-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ddc88-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="ddc88-117">변경 내용</span><span class="sxs-lookup"><span data-stu-id="ddc88-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="ddc88-118">Azure 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="ddc88-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="ddc88-119">웹앱</span><span class="sxs-lookup"><span data-stu-id="ddc88-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="ddc88-120">Azure 웹 사이트에 대 한 앱 서비스는 엄격 하 게 제한 toochanging hello 이름 웹 사이트 tooWeb 앱.</span><span class="sxs-lookup"><span data-stu-id="ddc88-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="ddc88-121">모든 기존 웹 사이트 인스턴스는 이제 App Service에서 웹앱이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="ddc88-122">Hello 통해 기존 웹 사이트에 액세스할 수 있습니다 <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure 포털</a>위치에서 기존의 모든 사이트를 찾을 수 있습니다, <em>웹 앱</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="ddc88-123"><em>웹 호스팅 계획</em> 이제 <em>앱 서비스 계획</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="ddc88-124"><em>App Service 계획</em>은 웹앱, Mobile App, 논리 앱 또는 API 앱과 같은 App Service의 모든 앱 유형을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="ddc88-125">Azure App Service 웹앱은 일반 공급됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="ddc88-126"><a href="http://azure.microsoft.com/services/app-service/web/">웹 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="ddc88-127">Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="ddc88-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="ddc88-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="ddc88-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="ddc88-129">모바일 서비스는 독립 실행형 서비스로 사용할 수 있는 toobe 계속와 계속 완벽 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="ddc88-130">모바일 앱에는 모든 모바일 서비스 등의 hello 기능을 통합 하는 앱 서비스에서 응용 프로그램 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="ddc88-131">쉽습니다 너무<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">모바일 서비스 tooMobile 앱에서에서 마이그레이션할</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="ddc88-132">App Service의 일부로 Mobile Apps에는 온-프레미스 및 SaaS 시스템과 통합, 스테이징 슬롯, WebJobs, 향상된 크기 조정 옵션 등 모바일 서비스의 범위를 초월한 새 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="ddc88-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">모바일 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="ddc88-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="ddc88-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="ddc88-135">API 앱에 쉽게 빌드하고 hello 클라우드 Api를 사용 하면 앱 서비스에서 새 응용 프로그램 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="ddc88-136"><a href="http://azure.microsoft.com/services/app-service/api/">API 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="ddc88-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ddc88-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="ddc88-138">논리 앱은 비즈니스 프로세스를 쉽게 자동화할 수 있게 해주는 App Service의 새로운 앱 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="ddc88-139"><a href="http://azure.microsoft.com/services/app-service/logic/">논리 앱에 대 한 자세한</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="ddc88-140">Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="ddc88-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="ddc88-141">BizTalk API 앱</span><span class="sxs-lookup"><span data-stu-id="ddc88-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="ddc88-142">BizTalk 서비스는 독립 실행형 서비스로 사용할 수 있는 toobe를 계속 하 고 계속 완벽 하 게 지원.</span><span class="sxs-lookup"><span data-stu-id="ddc88-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="ddc88-143">BizTalk Services의 모든 hello 기능 API 앱 사용할 수 있도록 사용자 tooperform 엔터프라이즈 응용 프로그램 통합 및 앱 서비스에서 응용 프로그램 형식을 hello 사용 하 여 B2B 통합 시나리오로 앱 서비스에 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="ddc88-144">논리 앱은 이제 시각적 디자인 환경을 toocreate 워크플로 사용 하 여 비즈니스 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="ddc88-145">toolearn을 방문 하세요 [앱 서비스 설명서](https://azure.microsoft.com/documentation/services/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc88-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

