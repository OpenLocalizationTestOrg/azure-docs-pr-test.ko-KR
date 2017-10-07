---
title: "Azure 트래픽 관리자와 함께 Azure 웹 앱 트래픽 aaaControlling"
description: "이 문서에서는 tooAzure 웹 응용 프로그램 관련 Azure 트래픽 관리자에 대 한 요약 정보를 제공 합니다."
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
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a><span data-ttu-id="c1a86-103">Azure 트래픽 관리자를 사용하여 Azure 웹 앱 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="c1a86-103">Controlling Azure web app traffic with Azure Traffic Manager</span></span>
> [!NOTE]
> <span data-ttu-id="c1a86-104">이 문서에서는 tooAzure 앱 서비스 웹 앱 관련해 서 Microsoft Azure 트래픽 관리자에 대 한 요약 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-104">This article provides summary information for Microsoft Azure Traffic Manager as it relates tooAzure App Service Web Apps.</span></span> <span data-ttu-id="c1a86-105">이 문서의 끝 hello에 hello 링크를 방문 하 여 자세한 정보에 대 한 Azure 트래픽 관리자 자체를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-105">More information about Azure Traffic Manager itself can be found by visiting hello links at hello end of this article.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="c1a86-106">소개</span><span class="sxs-lookup"><span data-stu-id="c1a86-106">Introduction</span></span>
<span data-ttu-id="c1a86-107">Azure 트래픽 관리자 toocontrol를 사용할 수 있습니다 어떻게 웹 클라이언트의 요청은 Azure 앱 서비스의 분산된 tooweb 앱.</span><span class="sxs-lookup"><span data-stu-id="c1a86-107">You can use Azure Traffic Manager toocontrol how requests from web clients are distributed tooweb apps in Azure App Service.</span></span> <span data-ttu-id="c1a86-108">웹 앱 끝점 tooa Azure 트래픽 관리자 프로필에 추가 되 면 Azure 트래픽 관리자는 추적 hello 상태 (실행 중, 중지 또는 삭제) 웹 응용 프로그램의 해당 끝점 중이 트래픽을 받아야 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-108">When web app endpoints are added tooa Azure Traffic Manager profile, Azure Traffic Manager keeps track of hello status of your web apps (running, stopped or deleted) so that it can decide which of those endpoints should receive traffic.</span></span>

## <a name="load-balancing-methods"></a><span data-ttu-id="c1a86-109">부하 분산 방법</span><span class="sxs-lookup"><span data-stu-id="c1a86-109">Load Balancing Methods</span></span>
<span data-ttu-id="c1a86-110">Azure 트래픽 관리자는 세 가지의 다른 부하 분산 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-110">Azure Traffic Manager uses three different load balancing methods.</span></span> <span data-ttu-id="c1a86-111">Hello tooAzure 웹 응용 프로그램 관련 된 목록 다음에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-111">These are described  in hello following list as they pertain tooAzure web apps.</span></span>

* <span data-ttu-id="c1a86-112">**장애 조치**: 웹 응용 프로그램 복제본 서로 다른 지역에 있으면이 메서드 tooconfigure 하나의 웹 앱 tooservice 모든 웹 클라이언트 트래픽을 사용 하 고 사례 hello 첫 번째 웹 응용 프로그램에서 트래픽을 하는 다른 지역의 tooservice에서 다른 웹 응용 프로그램 구성 수 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-112">**Failover**: If you have web app clones in different regions, you can use this method tooconfigure one web app tooservice all web client traffic, and configure another web app in a different region tooservice that traffic in case hello first web app becomes unavailable.</span></span>
* <span data-ttu-id="c1a86-113">**라운드 로빈**: 웹 응용 프로그램 복제본 서로 다른 지역에 있으면 있습니다를 사용할 수 있습니다이 메서드 toodistribute 트래픽을 균등 하 게 서로 다른 지역에 있는 hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-113">**Round Robin**: If you have web app clones in different regions, you can use this method toodistribute traffic equally across hello web apps in different regions.</span></span>
* <span data-ttu-id="c1a86-114">**성능**: hello 성능 방법 hello 가장 짧은 왕복 시간 tooclients에 기반 하는 트래픽을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-114">**Performance**: hello Performance method distributes traffic based on hello shortest round trip time tooclients.</span></span> <span data-ttu-id="c1a86-115">성능 방법 hello hello 내에서 웹 앱에 사용할 수 있습니다 동일한 지역 또는 서로 다른 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-115">hello Performance method can be used for web apps within hello same region or in different regions.</span></span>

## <a name="web-apps-and-traffic-manager-profiles"></a><span data-ttu-id="c1a86-116">웹 앱 및 트래픽 관리자 프로필</span><span class="sxs-lookup"><span data-stu-id="c1a86-116">Web Apps and Traffic Manager Profiles</span></span>
<span data-ttu-id="c1a86-117">웹 앱에 대 한 트래픽의 tooconfigure hello 컨트롤을 Azure 트래픽 관리자의 hello 3 부하 분산 앞에서 설명한 방법 중 하나를 사용 하는 프로필을 만들 추가 하는 다음 toocontrol 트래픽 toohello 원하는 hello 끝점에 (이 경우 웹 앱) 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-117">tooconfigure hello control of web app traffic, you create a profile in Azure Traffic Manager that uses one of hello three load balancing methods described previously, and then add hello endpoints (in this case, web apps) for which you want toocontrol traffic toohello profile.</span></span> <span data-ttu-id="c1a86-118">웹 응용 프로그램 상태 (실행 중, 중지 또는 삭제)은 정기적으로 전달된 toohello 프로 파일링 Azure 트래픽 관리자는 그에 따라 트래픽을 보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-118">Your web app status (running, stopped or deleted) is regularly communicated toohello profile so that Azure Traffic Manager can direct traffic accordingly.</span></span>

<span data-ttu-id="c1a86-119">Azure와 함께 Azure 트래픽 관리자를 사용할 때는 주의 hello 지점 다음에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c1a86-119">When using Azure Traffic Manager with Azure, keep in mind hello following points:</span></span>

* <span data-ttu-id="c1a86-120">Hello 내에서 웹 앱 전용 배포에 대 한 웹 앱에 이미 같은 지역의 tooweb 응용 프로그램 모드와 관계 없이 장애 조치 및 라운드 로빈 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-120">For web app only deployments within hello same region, Web Apps already provides failover and round-robin functionality without regard tooweb app mode.</span></span>
* <span data-ttu-id="c1a86-121">에 대 한 배포에 다른 Azure 클라우드 서비스와 함께에서 웹 응용 프로그램을 사용 하는 동일한 지역 hello, 두 가지 유형의 끝점 tooenable 하이브리드 시나리오를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-121">For deployments in hello same region that use Web Apps in conjunction with another Azure cloud service, you can combine both types of endpoints tooenable hybrid scenarios.</span></span>
* <span data-ttu-id="c1a86-122">프로필에서 지역당 하나의 웹 앱 끝점만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-122">You can only specify one web app endpoint per region in a profile.</span></span> <span data-ttu-id="c1a86-123">한 영역에 대 한 끝점으로 웹 응용 프로그램을 선택 하면 hello 나머지 웹 응용 프로그램에서 해당 지역의 해당 프로필에 대 한 선택을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-123">When you select a web app as an endpoint for one region, hello remaining web apps in that region become unavailable for selection for that profile.</span></span>
* <span data-ttu-id="c1a86-124">Azure 트래픽 관리자 프로필에 지정 하는 hello 웹 앱 끝점 hello 아래에 표시 될 **도메인 이름** hello 프로필의 hello 웹 앱에 대 한 hello 구성 페이지에서 섹션 하지만 됩니다 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-124">hello web app endpoints that you specify in a Azure Traffic Manager profile will appear under hello **Domain Names** section on hello Configure page for hello web app in hello profile, but will not be configurable there.</span></span>
* <span data-ttu-id="c1a86-125">웹 응용 프로그램 tooa 프로필에 추가한 후 hello **사이트 URL** hello 웹의 대시보드에서 hello에 응용 프로그램의 포털 페이지 하나를 설정한 경우 hello 웹 앱의 hello 사용자 지정 도메인 URL이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-125">After you add a web app tooa profile, hello **Site URL** on hello Dashboard of hello web app's portal page will display hello custom domain URL of hello web app if you have set one up.</span></span> <span data-ttu-id="c1a86-126">그렇지 않으면 hello 트래픽 관리자 프로필 URL 표시 됩니다 (예를 들어 `contoso.trafficmgr.com`).</span><span class="sxs-lookup"><span data-stu-id="c1a86-126">Otherwise, it will display hello Traffic Manager profile URL (for example, `contoso.trafficmgr.com`).</span></span> <span data-ttu-id="c1a86-127">Hello 웹 앱의 직접 도메인 이름을 둘 다 hello 및 트래픽 관리자 URL hello hello에서 hello 웹 앱의 구성 페이지에 표시 됩니다 **도메인 이름** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c1a86-127">Both hello direct domain name of hello web app and hello Traffic Manager URL will be visible on hello web app's Configure page under hello **Domain Names** section.</span></span>
* <span data-ttu-id="c1a86-128">사용자 지정 도메인 이름을 작동할지, 기대 하지만 또한 tooadding 해당 tooyour 웹 앱, DNS 맵 toopoint toohello 트래픽 관리자 URL을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-128">Your custom domain names will work as expected, but in addition tooadding them tooyour web apps, you must also configure your DNS map toopoint toohello Traffic Manager URL.</span></span> <span data-ttu-id="c1a86-129">방법에 대 한 Azure 웹 앱에 대 한 사용자 지정 도메인을 tooset 참조 [Azure 웹 사이트에 대 한 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-129">For information on how tooset up a custom domain for a Azure web app,  see [Configuring a custom domain name for an Azure web site](app-service-web-tutorial-custom-domain.md).</span></span>
* <span data-ttu-id="c1a86-130">표준 또는 프리미엄 모드 tooa Azure 트래픽 관리자 프로필에에서 있는 웹 응용 프로그램에만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-130">You can only add web apps that are in standard or premium mode tooa Azure Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1a86-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1a86-131">Next Steps</span></span>
<span data-ttu-id="c1a86-132">Azure 트래픽 관리자의 개념 및 기술 개요에 대해서는 [트래픽 관리자 개요](../traffic-manager/traffic-manager-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c1a86-132">For a conceptual and technical overview of Azure Traffic Manager, see [Traffic Manager Overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="c1a86-133">웹 앱과 트래픽 관리자를 사용 하는 방법에 대 한 자세한 내용은 hello 블로그 게시물을 참조 하십시오. [Azure 트래픽 관리자를 Azure 웹 사이트를 사용 하 여](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) 및 [Azure 트래픽 관리자의 경우 이제 Azure 웹 사이트를 통합할 수](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a86-133">For more information about using Traffic Manager with Web Apps, see hello blog posts [Using Azure Traffic Manager with Azure Web Sites](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) and [Azure Traffic Manager can now integrate with Azure Web Sites](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).</span></span>

