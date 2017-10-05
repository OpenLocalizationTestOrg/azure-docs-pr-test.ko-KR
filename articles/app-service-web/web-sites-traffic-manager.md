---
title: "Azure 트래픽 관리자를 사용하여 Azure 웹 앱 트래픽 제어"
description: "이 문서에서는 Azure 웹앱과 관련된 Azure Traffic Manager의 요약 정보를 제공합니다."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: fb7d391e3118a9dccde5501c3f30c6f580932a30
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a><span data-ttu-id="12144-103">Azure 트래픽 관리자를 사용하여 Azure 웹 앱 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="12144-103">Controlling Azure web app traffic with Azure Traffic Manager</span></span>
> [!NOTE]
> <span data-ttu-id="12144-104">이 문서에서는 Azure 앱 서비스 웹 앱과 관련된 Microsoft Azure 트래픽 관리자의 요약 정보를 제공합니다."</span><span class="sxs-lookup"><span data-stu-id="12144-104">This article provides summary information for Microsoft Azure Traffic Manager as it relates to Azure App Service Web Apps.</span></span> <span data-ttu-id="12144-105">Microsoft Azure 트래픽 관리자 자체에 대한 추가 정보는 이 문서의 끝 부분에 있는 링크를 방문하면 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-105">More information about Azure Traffic Manager itself can be found by visiting the links at the end of this article.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="12144-106">소개</span><span class="sxs-lookup"><span data-stu-id="12144-106">Introduction</span></span>
<span data-ttu-id="12144-107">Azure 트래픽 관리자를 사용하면 웹 클라이언트의 요청을 Azure 앱 서비스의 웹 앱에 분산하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-107">You can use Azure Traffic Manager to control how requests from web clients are distributed to web apps in Azure App Service.</span></span> <span data-ttu-id="12144-108">웹 앱 끝점을 Azure 트래픽 관리자 프로필에 추가하는 경우 Azure 트래픽 관리자가 웹 앱의 상태(실행 중, 중지됨 또는 삭제됨)를 계속 추적하므로 트래픽을 수신할 끝점을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-108">When web app endpoints are added to a Azure Traffic Manager profile, Azure Traffic Manager keeps track of the status of your web apps (running, stopped or deleted) so that it can decide which of those endpoints should receive traffic.</span></span>

## <a name="load-balancing-methods"></a><span data-ttu-id="12144-109">부하 분산 방법</span><span class="sxs-lookup"><span data-stu-id="12144-109">Load Balancing Methods</span></span>
<span data-ttu-id="12144-110">Azure 트래픽 관리자는 세 가지의 다른 부하 분산 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-110">Azure Traffic Manager uses three different load balancing methods.</span></span> <span data-ttu-id="12144-111">각 방법은 Azure 웹앱과 관련된 다음 목록에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-111">These are described  in the following list as they pertain to Azure web apps.</span></span>

* <span data-ttu-id="12144-112">**장애 조치(failover)**: 다른 지역에 웹앱 복제본이 있는 경우 이 방법을 사용하여 모든 웹 클라이언트 트래픽을 처리하도록 웹앱을 하나 구성하고, 첫 번째 웹앱을 사용할 수 없게 되는 경우 해당 트래픽을 처리하도록 다른 지역에 추가 웹앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-112">**Failover**: If you have web app clones in different regions, you can use this method to configure one web app to service all web client traffic, and configure another web app in a different region to service that traffic in case the first web app becomes unavailable.</span></span>
* <span data-ttu-id="12144-113">**라운드 로빈**: 다른 지역에 웹앱 복제본이 있는 경우 이 방법을 사용하여 여러 지역의 웹앱에 균등하게 트래픽을 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-113">**Round Robin**: If you have web app clones in different regions, you can use this method to distribute traffic equally across the web apps in different regions.</span></span>
* <span data-ttu-id="12144-114">**성능**: 성능 방법은 클라이언트에 대한 가장 짧은 왕복 시간에 따라 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-114">**Performance**: The Performance method distributes traffic based on the shortest round trip time to clients.</span></span> <span data-ttu-id="12144-115">성능 방법은 동일한 지역 내에 있거나 다른 지역에 있는 웹 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-115">The Performance method can be used for web apps within the same region or in different regions.</span></span>

## <a name="web-apps-and-traffic-manager-profiles"></a><span data-ttu-id="12144-116">웹 앱 및 트래픽 관리자 프로필</span><span class="sxs-lookup"><span data-stu-id="12144-116">Web Apps and Traffic Manager Profiles</span></span>
<span data-ttu-id="12144-117">웹 앱 트래픽을 제어하도록 구성하려면 앞서 설명한 세 가지 부하 분산 방법 중 하나를 사용하는 프로필을 Azure 트래픽 관리자에서 만든 후 트래픽을 제어하려는 끝점(이 경우에는 웹 앱)을 프로필에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-117">To configure the control of web app traffic, you create a profile in Azure Traffic Manager that uses one of the three load balancing methods described previously, and then add the endpoints (in this case, web apps) for which you want to control traffic to the profile.</span></span> <span data-ttu-id="12144-118">웹 앱 상태(실행 중, 중지됨 또는 삭제됨)가 정기적으로 프로필에 전달되므로 Azure 트래픽 관리자가 상태에 따라 트래픽을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-118">Your web app status (running, stopped or deleted) is regularly communicated to the profile so that Azure Traffic Manager can direct traffic accordingly.</span></span>

<span data-ttu-id="12144-119">Azure에서 Azure 트래픽 관리자를 사용할 경우 다음 사항에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="12144-119">When using Azure Traffic Manager with Azure, keep in mind the following points:</span></span>

* <span data-ttu-id="12144-120">동일한 지역 내에서 웹 앱 전용 배포의 경우 웹 앱은 웹 앱 모드와 상관없이 장애 조치(failover) 및 라운드 로빈 기능을 이미 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-120">For web app only deployments within the same region, Web Apps already provides failover and round-robin functionality without regard to web app mode.</span></span>
* <span data-ttu-id="12144-121">동일한 지역에서 다른 Azure 클라우드 서비스와 함께 웹 앱을 사용하는 배포의 경우 끝점의 두 유형을 결합하여 하이브리드 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-121">For deployments in the same region that use Web Apps in conjunction with another Azure cloud service, you can combine both types of endpoints to enable hybrid scenarios.</span></span>
* <span data-ttu-id="12144-122">프로필에서 지역당 하나의 웹 앱 끝점만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-122">You can only specify one web app endpoint per region in a profile.</span></span> <span data-ttu-id="12144-123">한 지역의 끝점으로 하나의 웹 앱을 선택한 경우 해당 지역의 나머지 웹 앱은 해당 프로필에 대해 선택할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12144-123">When you select a web app as an endpoint for one region, the remaining web apps in that region become unavailable for selection for that profile.</span></span>
* <span data-ttu-id="12144-124">Azure 트래픽 관리자 프로필에서 지정한 웹앱 끝점은 프로필에서 웹앱에 대한 구성 페이지의 **도메인 이름** 섹션에 표시되지만 이 섹션에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-124">The web app endpoints that you specify in a Azure Traffic Manager profile will appear under the **Domain Names** section on the Configure page for the web app in the profile, but will not be configurable there.</span></span>
* <span data-ttu-id="12144-125">프로필에 웹앱을 추가한 후 사이트를 설정한 경우 웹앱의 포털 페이지의 대시보드에 있는 **사이트 URL** 은 해당 웹앱의 사용자 지정 도메인 URL을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-125">After you add a web app to a profile, the **Site URL** on the Dashboard of the web app's portal page will display the custom domain URL of the web app if you have set one up.</span></span> <span data-ttu-id="12144-126">그렇지 않으면 트래픽 관리자 프로필 URL(예: `contoso.trafficmgr.com`)을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-126">Otherwise, it will display the Traffic Manager profile URL (for example, `contoso.trafficmgr.com`).</span></span> <span data-ttu-id="12144-127">웹앱의 직접적인 도메인 이름과 트래픽 관리자 URL은 모두 웹앱 구성 페이지의 **도메인 이름** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12144-127">Both the direct domain name of the web app and the Traffic Manager URL will be visible on the web app's Configure page under the **Domain Names** section.</span></span>
* <span data-ttu-id="12144-128">사용자 지정 도메인 이름이 예상대로 작동하지만 웹 앱에 해당 이름을 추가하는 작업 외에도 DNS 맵이 트래픽 관리자 URL을 가리키도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12144-128">Your custom domain names will work as expected, but in addition to adding them to your web apps, you must also configure your DNS map to point to the Traffic Manager URL.</span></span> <span data-ttu-id="12144-129">Azure 웹앱에 대해 사용자 지정 도메인을 설정하는 방법에 대한 자세한 내용은 [Azure 웹 사이트에 대한 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12144-129">For information on how to set up a custom domain for a Azure web app,  see [Configuring a custom domain name for an Azure web site](app-service-web-tutorial-custom-domain.md).</span></span>
* <span data-ttu-id="12144-130">Standard 또는 Premium 모드의 웹앱만 Azure Traffic Manager 프로필에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12144-130">You can only add web apps that are in standard or premium mode to a Azure Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12144-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12144-131">Next Steps</span></span>
<span data-ttu-id="12144-132">Azure 트래픽 관리자의 개념 및 기술 개요에 대해서는 [트래픽 관리자 개요](../traffic-manager/traffic-manager-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="12144-132">For a conceptual and technical overview of Azure Traffic Manager, see [Traffic Manager Overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="12144-133">Web Apps에서 Traffic Manager를 사용하는 방법에 대한 자세한 내용은 블로그 게시물 [Azure 웹 사이트에서 Azure Traffic Manager 사용](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) 및 [이제 Azure Traffic Manager를 Azure 웹 사이트와 통합할 수 있음](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12144-133">For more information about using Traffic Manager with Web Apps, see the blog posts [Using Azure Traffic Manager with Azure Web Sites](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) and [Azure Traffic Manager can now integrate with Azure Web Sites](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).</span></span>

