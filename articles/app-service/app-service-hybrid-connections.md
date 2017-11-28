---
title: "aaa \"Azure 앱 서비스 하이브리드 연결 | \"Microsoft Docs"
description: "어떻게 서로 다른 네트워크의 하이브리드 연결 tooaccess 리소스 toocreate 및 사용"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="b1453-103">Azure App Service 하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="b1453-103">Azure App Service Hybrid Connections</span></span> #

## <a name="overview"></a><span data-ttu-id="b1453-104">개요</span><span class="sxs-lookup"><span data-stu-id="b1453-104">Overview</span></span> ##

<span data-ttu-id="b1453-105">하이브리드 연결은 모두 Azure에 서비스 뿐만 아니라 hello Azure 앱 서비스의에서 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-105">Hybrid Connections is both a service in Azure as well as a feature in hello Azure App Service.</span></span>  <span data-ttu-id="b1453-106">서비스는 사용 및 hello Azure 앱 서비스에서에서 활용 하는 것 이상의 기능에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-106">As a service it has use and capabilities beyond those that are leveraged in hello Azure App Service.</span></span>  <span data-ttu-id="b1453-107">하이브리드 연결 및 Azure 앱 서비스를 시작할 수 있습니다 hello 외부에서 사용 하는 방법에 대 한 자세한 toolearn [Azure 릴레이 하이브리드 연결][HCService]</span><span class="sxs-lookup"><span data-stu-id="b1453-107">toolearn more about Hybrid Connections and their usage outside of hello Azure App Service you can start here, [Azure Relay Hybrid Connections][HCService]</span></span>

<span data-ttu-id="b1453-108">Hello Azure 앱 서비스 내에서 하이브리드 연결에는 다른 네트워크에 사용 되는 tooaccess 응용 프로그램 리소스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-108">Within hello Azure App Service, hybrid connections can be used tooaccess application resources in other networks.</span></span> <span data-ttu-id="b1453-109">응용 프로그램 tooan 응용 프로그램 끝점에서 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-109">It provides access FROM your app tooan application endpoint.</span></span>  <span data-ttu-id="b1453-110">수 있는 대체 기능 tooaccess 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-110">It does not enable an alternative capability tooaccess your application.</span></span>  <span data-ttu-id="b1453-111">Hello 앱 서비스에서에서 사용 되는, 단일 TCP 호스트 및 포트 조합을 tooa 각 하이브리드 연결에 연관 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-111">As used in hello App Service, each hybrid connection correlates tooa single TCP host and port combination.</span></span>  <span data-ttu-id="b1453-112">즉, 해당 hello 하이브리드 연결 끝점 제공 될 수 있습니다는 운영 체제 및 모든 응용 프로그램에 적중할 TCP 수신 대기 포트.</span><span class="sxs-lookup"><span data-stu-id="b1453-112">This means that hello hybrid connection endpoint can be on any operating system and any application provided you are hitting a TCP listening port.</span></span> <span data-ttu-id="b1453-113">하이브리드 연결 알고 하거나 어떤 hello 응용 프로그램 프로토콜은 또는 기능에 액세스 하는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-113">Hybrid connections does not know or care what hello application protocol is or what you are accessing.</span></span>  <span data-ttu-id="b1453-114">단지 네트워크 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-114">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="b1453-115">작동 방법</span><span class="sxs-lookup"><span data-stu-id="b1453-115">How it works</span></span> ##
<span data-ttu-id="b1453-116">아웃 바운드 호출을 두 개의 tooService 버스 릴레이의 hello 하이브리드 연결 기능은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-116">hello hybrid connections feature consists of two outbound calls tooService Bus Relay.</span></span>  <span data-ttu-id="b1453-117">Hello 호스트 위치 hello 앱 서비스에서 앱을 실행 하 고, hello 하이브리드 연결 Manager(HCM) tooService 버스 릴레이에서 연결의 라이브러리에서 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-117">There is a connection from a library on hello host where your app is running in hello app service and then there is a connection from hello Hybrid Connection Manager(HCM) tooService Bus relay.</span></span>  <span data-ttu-id="b1453-118">HCM hello는 hello 네트워크 호스팅 내에서 배포 하는 릴레이 서비스</span><span class="sxs-lookup"><span data-stu-id="b1453-118">hello HCM is a relay service that you deploy within hello network hosting</span></span> 

<span data-ttu-id="b1453-119">Hello를 통해 두 개의 조인 된 연결 응용 프로그램에 TCP 터널 tooa hello HCM의 다른 쪽 hello에 호스트: 포트 조합을 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-119">Through hello two joined connections your app has a TCP tunnel tooa fixed host:port combination on hello other side of hello HCM.</span></span>  <span data-ttu-id="b1453-120">보안 및 인증/권한 부여에 대 한 SAS 키에 대 한 TLS 1.2를 사용 하는 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-120">hello connection uses TLS 1.2 for security and SAS keys for authentication/authorization.</span></span>    

![][1]

<span data-ttu-id="b1453-121">응용 프로그램에서 DNS 요청 구성 하이브리드 연결 끝점을 일치 하는 다음 hello 아웃 바운드 TCP 트래픽을 hello 하이브리드 연결 아래로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-121">When your app makes a DNS request that matches a configure Hybrid Connection endpoint, then hello outbound TCP traffic will be redirected down hello hybrid connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="b1453-122">이 것이 좋습니다 tooalways 사용 하 여 하이브리드 연결의 DNS 이름을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-122">This means that you should try tooalways use a DNS name for your Hybrid Connection.</span></span>  <span data-ttu-id="b1453-123">Hello 끝점 IP 주소를 대신 사용 하는 경우 일부 클라이언트 소프트웨어에서 DNS 조회를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-123">Some client software does not do a DNS lookup if hello endpoint uses an IP address instead.</span></span>
>
>

<span data-ttu-id="b1453-124">하이브리드 연결을 Azure 릴레이 서비스로 제공 되 고 hello 이전 BizTalk 하이브리드 연결 하는 hello 새 하이브리드 연결의는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-124">There are two types of hybrid connections, hello new hybrid connections that are offered as a service under Azure Relay and hello older BizTalk Hybrid Connections.</span></span>  <span data-ttu-id="b1453-125">hello 이전 BizTalk 하이브리드 연결은 hello 포털에서 기존 하이브리드 연결 tooas를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-125">hello older BizTalk Hybrid Connections are referred tooas Classic Hybrid Connections in hello portal.</span></span>  <span data-ttu-id="b1453-126">이 문서의 뒷부분에서 이에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-126">There is more information later in this document about them.</span></span>

### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="b1453-127">App Service 하이브리드 연결의 장점</span><span class="sxs-lookup"><span data-stu-id="b1453-127">App Service hybrid connection benefits</span></span> ###

<span data-ttu-id="b1453-128">이점 toohello 하이브리드 연결 기능 등의 여러 가지</span><span class="sxs-lookup"><span data-stu-id="b1453-128">There are a number of benefits toohello hybrid connections capability including</span></span>

- <span data-ttu-id="b1453-129">앱이 온-프레미스 시스템 및 서비스에 안전하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-129">Apps can securely access on premises systems and services securely</span></span>
- <span data-ttu-id="b1453-130">hello 기능에 액세스할 수 있는 인터넷 끝점 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-130">hello feature does not require an internet accessible endpoint</span></span>
- <span data-ttu-id="b1453-131">신속 하 고 쉽게 tooset를</span><span class="sxs-lookup"><span data-stu-id="b1453-131">it is quick and easy tooset up</span></span>  
- <span data-ttu-id="b1453-132">하이브리드 연결 각 일치 tooa 단일 호스트: 포트 조합으로 서 우수한 보안 기능</span><span class="sxs-lookup"><span data-stu-id="b1453-132">each hybrid connection matches tooa single host:port combination which is an excellent security aspect</span></span>
- <span data-ttu-id="b1453-133">일반적으로 필요 하지 않습니다 방화벽 구멍 hello 연결은 표준 웹 포트를 통해 모든 아웃 바운드</span><span class="sxs-lookup"><span data-stu-id="b1453-133">it normally does not require firewall holes as hello connections are all outbound over standard web ports</span></span>
- <span data-ttu-id="b1453-134">hello 기능은 hello 끝점에서 사용 하는 응용 프로그램 및 hello 기술에 사용 되는 알 수 없는 toohello 언어에 액세스할 수 있는 네트워크 수준 때문에</span><span class="sxs-lookup"><span data-stu-id="b1453-134">because hello feature is network level that also means that it is agnostic toohello language used by your app and hello technology used by hello endpoint</span></span>
- <span data-ttu-id="b1453-135">것이 단일 응용 프로그램에서 여러 네트워크에서 tooprovide 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="b1453-135">it can be used tooprovide access in multiple networks from a single app</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="b1453-136">하이브리드 연결로 할 수 없는 작업</span><span class="sxs-lookup"><span data-stu-id="b1453-136">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="b1453-137">하이브리드 연결로 할 수 없는 몇 가지 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-137">There are a few things you cannot do with hybrid connections and they include:</span></span>

- <span data-ttu-id="b1453-138">드라이브 탑재</span><span class="sxs-lookup"><span data-stu-id="b1453-138">mounting a drive</span></span>
- <span data-ttu-id="b1453-139">UDP 사용</span><span class="sxs-lookup"><span data-stu-id="b1453-139">using UDP</span></span>
- <span data-ttu-id="b1453-140">FTP 수동 모드 또는 확장 수동 모드 같은 동적 포트를 사용하는 TCP 기반 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="b1453-140">accessing TCP based services that use dynamic ports such as FTP Passive Mode or Extended Passive Mode</span></span>
- <span data-ttu-id="b1453-141">LDAP 지원(경우에 따라 UDP가 필요하므로)</span><span class="sxs-lookup"><span data-stu-id="b1453-141">LDAP support, as it sometimes requires UDP</span></span>
- <span data-ttu-id="b1453-142">Active Directory 지원</span><span class="sxs-lookup"><span data-stu-id="b1453-142">Active Directory support</span></span>

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a><span data-ttu-id="b1453-143">앱에서 하이브리드 연결 추가 및 만들기</span><span class="sxs-lookup"><span data-stu-id="b1453-143">Adding and Creating a Hybrid Connection in your App</span></span> ##

<span data-ttu-id="b1453-144">Hello 앱 포털을 통해 또는 hello 하이브리드 연결 서비스 포털에서 하이브리드 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-144">Hybrid Connections can be created through hello app portal or from hello Hybrid Connection service portal.</span></span>  <span data-ttu-id="b1453-145">Hello 앱 포털 toocreate hello toouse 앱을 사용 하 여 원하는 하이브리드 연결을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-145">It is highly recommended that you use hello app portal toocreate hello Hybrid Connections you wish toouse with your app.</span></span>  <span data-ttu-id="b1453-146">하이브리드 연결 toocreate 이동 toohello [Azure 포털] [ portal] 하며 앱에 대 한 UI hello로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-146">toocreate a Hybrid Connection go toohello [Azure portal][portal] and go into hello UI for your app.</span></span>  <span data-ttu-id="b1453-147">**네트워킹 > 하이브리드 연결 끝점 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-147">Select **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="b1453-148">여기에서 응용 프로그램으로 구성 된 hello 하이브리드 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-148">From here you can see hello Hybrid Connections that are configured with your app</span></span>  

![][2]

<span data-ttu-id="b1453-149">새 하이브리드 연결을 tooadd 하이브리드 연결 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-149">tooadd a new Hybrid Connection, click Add Hybrid Connection.</span></span>  <span data-ttu-id="b1453-150">UI가 열리면 hello 이미 만든 hello 하이브리드 연결을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-150">hello UI that opens up lists hello Hybrid Connections that you have already created.</span></span>  <span data-ttu-id="b1453-151">그 중 하나 이상의 tooadd tooyour 앱을 클릭 하 고 적중 hello 것 **하이브리드 연결을 선택 하는 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-151">tooadd one or more of them tooyour app, click on hello ones you want and hit **Add selected hybrid connection**.</span></span>  

![][3]

<span data-ttu-id="b1453-152">새 하이브리드 연결을 toocreate 클릭 **새 하이브리드 연결을 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-152">If you want toocreate a new Hybrid Connection, click **Create new hybrid connection**.</span></span>  <span data-ttu-id="b1453-153">여기에서 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-153">From here you specify the:</span></span> 

- <span data-ttu-id="b1453-154">끝점 이름</span><span class="sxs-lookup"><span data-stu-id="b1453-154">endpoint name</span></span>
- <span data-ttu-id="b1453-155">끝점 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="b1453-155">endpoint hostname</span></span>
- <span data-ttu-id="b1453-156">끝점 포트</span><span class="sxs-lookup"><span data-stu-id="b1453-156">endpoint port</span></span>
- <span data-ttu-id="b1453-157">서비스 버스 네임 스페이스 원하는 toouse</span><span class="sxs-lookup"><span data-stu-id="b1453-157">servicebus namespace you wish toouse</span></span>

![][4]

<span data-ttu-id="b1453-158">모든 하이브리드 연결이 동률된 tooa 서비스 버스 네임 스페이스 및 Azure 지역에서 각 서비스 버스 네임 스페이스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-158">Every hybrid connection is tied tooa service bus namespace and each service bus namespace is in an Azure region.</span></span>  <span data-ttu-id="b1453-159">서비스 버스 네임 스페이스를 사용 하 여 tootry hello 앱와 동일한 지역 따라서 tooavoid 인 한 네트워크 대기 시간으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-159">It is important tootry and use a service bus namespace in hello same region as your app so as tooavoid network induced latency.</span></span>

<span data-ttu-id="b1453-160">앱에서 하이브리드 연결 tooremove 않으려면 마우스 오른쪽 단추로 클릭 하 고 선택 **연결 끊기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-160">If you want tooremove your hybrid connection from your app, right click on it and select **Disconnect**.</span></span>  

<span data-ttu-id="b1453-161">하이브리드 연결 tooyour 웹 앱에 추가 되 면 클릭 해도에 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-161">Once a hybrid connection is added tooyour web app, you can see details on it by simply clicking on it.</span></span>  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="b1453-162">하이브리드 연결 및 App Service 계획</span><span class="sxs-lookup"><span data-stu-id="b1453-162">Hybrid Connections and App Service Plans</span></span> ##

<span data-ttu-id="b1453-163">hello만 하이브리드 연결을 사용할 수 있습니다는 hello 새 하이브리드 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-163">hello only hybrid connections you can now make are hello new hybrid connections.</span></span>  <span data-ttu-id="b1453-164">하이브리드 연결은 기본, 표준, 프리미엄 및 격리 요금제 SKU에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-164">They are only available in Basic, Standard, Premium and Isolated pricing SKUs.</span></span>  <span data-ttu-id="b1453-165">연결 제한 toohello 계획 가격 책정 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-165">There are limits tied toohello pricing plan.</span></span>  

| <span data-ttu-id="b1453-166">요금제</span><span class="sxs-lookup"><span data-stu-id="b1453-166">Pricing Plan</span></span> | <span data-ttu-id="b1453-167">Hello 계획에서 사용할 수 있는 하이브리드 연결의 수</span><span class="sxs-lookup"><span data-stu-id="b1453-167">Number of hybrid connections usable in hello plan</span></span> |
|----|----|
| <span data-ttu-id="b1453-168">Basic</span><span class="sxs-lookup"><span data-stu-id="b1453-168">Basic</span></span> | <span data-ttu-id="b1453-169">5</span><span class="sxs-lookup"><span data-stu-id="b1453-169">5</span></span> |
| <span data-ttu-id="b1453-170">Standard</span><span class="sxs-lookup"><span data-stu-id="b1453-170">Standard</span></span> | <span data-ttu-id="b1453-171">25</span><span class="sxs-lookup"><span data-stu-id="b1453-171">25</span></span> |
| <span data-ttu-id="b1453-172">Premium</span><span class="sxs-lookup"><span data-stu-id="b1453-172">Premium</span></span> | <span data-ttu-id="b1453-173">200</span><span class="sxs-lookup"><span data-stu-id="b1453-173">200</span></span> |
| <span data-ttu-id="b1453-174">격리</span><span class="sxs-lookup"><span data-stu-id="b1453-174">Isolated</span></span> | <span data-ttu-id="b1453-175">200</span><span class="sxs-lookup"><span data-stu-id="b1453-175">200</span></span> |

<span data-ttu-id="b1453-176">또한 UI가 어떤 응용 프로그램 및 hello 하이브리드 연결 수를 사용 하는 것을 보여 주는 앱 서비스 계획의 앱 서비스 계획 제한 사항 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-176">Since there are App Service Plan restrictions there is also UI in hello App Service Plan that shows you how many hybrid connections are being used and by what apps.</span></span>  

![][6]

<span data-ttu-id="b1453-177">마찬가지로 hello 앱 보기를 볼 수 있습니다 세부 정보에서 하이브리드 연결 클릭 하 여.</span><span class="sxs-lookup"><span data-stu-id="b1453-177">Just as with hello app view, you can see details on your hybrid connection by clicking on it.</span></span>  <span data-ttu-id="b1453-178">Hello 앱 보기에서 사용 했던 모든 hello 정보를 볼 수 있지만 다른 응용 프로그램과 hello에서 확인할 수 여기에 표시 된 hello 속성에서 동일한 앱 서비스 계획 사용 하는 하이브리드 연결에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-178">In hello properties shown here you can see all hello information you had at hello app view but can also see how many other apps in hello same App Service Plan are using that hybrid connection.</span></span>

![][7]

<span data-ttu-id="b1453-179">앱 서비스 계획에 사용할 수 있는 하이브리드 연결 끝점 hello 수를 제한 하는 동안 개수에 관계 없이 해당 앱 서비스 계획의 앱에서 사용 되는 각 하이브리드 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-179">While there is a limit on hello number of hybrid connection endpoints that can be used in an App Service Plan, each hybrid connection used can be used across any number of apps in that App Service Plan.</span></span>  <span data-ttu-id="b1453-180">앱 서비스 계획에 5 개의 별도 앱에서 사용한 하이브리드 연결 1 한다면 되는 여전히 하나만 하이브리드 연결 toosay입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-180">That is toosay that if I had 1 hybrid connection that I used in 5 separate apps in my App Service Plan, that is still just 1 hybrid connection.</span></span>

<span data-ttu-id="b1453-181">추가 비용 toohybrid 연결 초과 되 고 Basic, Standard, Premium 또는 격리 된 SKU에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-181">There is an additional cost toohybrid connections beyond being only usable in a Basic, Standard, Premium or Isolated SKU.</span></span>  <span data-ttu-id="b1453-182">하이브리드 연결 가격 책정에 대한 자세한 내용은 [Service Bus 가격 책정][sbpricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1453-182">For details on hybrid connection pricing please go here: [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="b1453-183">하이브리드 연결 관리자</span><span class="sxs-lookup"><span data-stu-id="b1453-183">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="b1453-184">하이브리드 연결 toowork 하려면에서 하이브리드 연결 끝점을 호스트 하는 hello 네트워크에서 릴레이 에이전트를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-184">In order for hybrid connections toowork you need a relay agent in hello network that hosts your hybrid connection endpoint.</span></span>  <span data-ttu-id="b1453-185">해당 릴레이 에이전트 hello 하이브리드 연결 관리자 (HCM) 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-185">That relay agent is called hello Hybrid Connection Manager (HCM).</span></span>  <span data-ttu-id="b1453-186">이 도구는 hello에서 다운로드할 수 있습니다 **네트워킹 > 하이브리드 연결 끝점 구성** hello에서 응용 프로그램에서 사용할 수 있는 UI [Azure 포털][portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-186">This tool can be downloaded from hello **Networking > Configure your hybrid connection endpoints** UI available from your app in hello [Azure portal][portal].</span></span>  

<span data-ttu-id="b1453-187">이 도구는 Windows의 Windows Server 2008 R2 이상 버전에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-187">This tool runs on Windows server 2008 R2 and later versions of Windows.</span></span>  <span data-ttu-id="b1453-188">설치가 완료 되 면 hello HCM 서비스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-188">Once installed hello HCM runs as a service.</span></span>  <span data-ttu-id="b1453-189">이 서비스는 hello 구성 된 끝점에 따라 tooAzure 서비스 버스 릴레이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-189">This service connects tooAzure servicebus relay based on hello configured endpoints.</span></span>  <span data-ttu-id="b1453-190">HCM hello에서 hello 연결 80 및 443 아웃 바운드 tooports 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-190">hello connections from hello HCM are outbound tooports 80 and 443.</span></span>    

<span data-ttu-id="b1453-191">HCM hello에 UI tooconfigure 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-191">hello HCM has a UI tooconfigure it.</span></span>  <span data-ttu-id="b1453-192">Hello HCM 설치 된 후 hello 하이브리드 연결 관리자 설치 디렉터리에서에 있는 HybridConnectionManagerUi.exe hello를 실행 하 여 hello UI 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-192">After hello HCM is installed you can bring up hello UI by running hello HybridConnectionManagerUi.exe that sits in hello Hybrid Connection Manager installation directory.</span></span>  <span data-ttu-id="b1453-193">Windows 10에서는 검색 상자에 *Hybrid Connection Manager UI*를 입력하여 UI에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-193">It is also easily reached on Windows 10 by typing *Hybrid Connection Manager UI* in your search box.</span></span>  

<span data-ttu-id="b1453-194">참조는 hello HCM UI를 시작 하면 먼저 hello 경우 hello HCM의이 인스턴스와 함께 구성 된 hello 하이브리드 연결을 모두 나열 하는 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-194">When hello HCM UI is started, hello first thing you see is a table that lists all of hello hybrid connections that are configured with this instance of hello HCM.</span></span>  <span data-ttu-id="b1453-195">변경 내용을 toomake을 원하는 경우 Azure 사용한 tooauthenticate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-195">If you wish toomake any changes you will need tooauthenticate with Azure.</span></span> 

<span data-ttu-id="b1453-196">tooadd 하나 또는 자세한 하이브리드 연결 tooyour HCM:</span><span class="sxs-lookup"><span data-stu-id="b1453-196">tooadd one or more Hybrid Connections tooyour HCM:</span></span>

1. <span data-ttu-id="b1453-197">Hello HCM UI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-197">Start hello HCM UI</span></span>
1. <span data-ttu-id="b1453-198">[Configure another hybrid connection](다른 하이브리드 연결 구성)을 클릭합니다. ![][8]</span><span class="sxs-lookup"><span data-stu-id="b1453-198">Click Configure another hybrid connection ![][8]</span></span>

1. <span data-ttu-id="b1453-199">Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-199">Sign in with your Azure account</span></span>
1. <span data-ttu-id="b1453-200">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-200">Choose a subscription</span></span>
1. <span data-ttu-id="b1453-201">클릭이 HCM toorelay 원하는 hello 하이브리드 연결![][9]</span><span class="sxs-lookup"><span data-stu-id="b1453-201">Click on hello hybrid connections you want this HCM toorelay ![][9]</span></span>

1. <span data-ttu-id="b1453-202">저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-202">Click Save</span></span>

<span data-ttu-id="b1453-203">이 시점에서 추가한 hello 하이브리드 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-203">At this point you will see hello hybrid connections you added.</span></span>  <span data-ttu-id="b1453-204">하이브리드 연결을 구성 하는 hello 클릭 하 고 hello 연결에 대 한 세부 정보를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-204">You can also click on hello configured hybrid connection and see details about hello connection.</span></span>

![][10]

<span data-ttu-id="b1453-205">프로그램 HCM toobe 수 toosupport hello 하이브리드 연결의 구성 된 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-205">For your HCM toobe able toosupport hello hybrid connections it is configured with, it needs:</span></span>

- <span data-ttu-id="b1453-206">포트 80 및 443을 통해 액세스 tooAzure TCP</span><span class="sxs-lookup"><span data-stu-id="b1453-206">TCP access tooAzure over ports 80 and 443</span></span>
- <span data-ttu-id="b1453-207">TCP 액세스 toohello 하이브리드 연결 끝점</span><span class="sxs-lookup"><span data-stu-id="b1453-207">TCP access toohello hybrid connection endpoint</span></span>
- <span data-ttu-id="b1453-208">기능 toodo DNS 모양 ups hello 끝점 호스트와 hello azure 서비스 버스 네임 스페이스에서</span><span class="sxs-lookup"><span data-stu-id="b1453-208">ability toodo DNS look ups on hello endpoint host and hello azure servicebus namespace</span></span>

<span data-ttu-id="b1453-209">HCM hello hello 이전 BizTalk 하이브리드 연결을 새 하이브리드 연결 모두를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-209">hello HCM supports both new hybrid connections as well as hello older BizTalk hybrid connections.</span></span>

### <a name="redundancy"></a><span data-ttu-id="b1453-210">중복</span><span class="sxs-lookup"><span data-stu-id="b1453-210">Redundancy</span></span> ###

<span data-ttu-id="b1453-211">각 HCM은 여러 하이브리드 연결을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-211">Each HCM can support multiple hybrid connections.</span></span>  <span data-ttu-id="b1453-212">특정 하이브리드 연결이 여러 HCM에서 지원될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-212">Also, any given hybrid connection can be supported by multiple HCMs.</span></span>  <span data-ttu-id="b1453-213">hello 기본 동작은 tooround 로빈 트래픽의 hello 분산 지정 된 모든 끝점에 대해 HCMs 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-213">hello default behavior is tooround robin traffic across hello configured HCMs for any given endpoint.</span></span>  <span data-ttu-id="b1453-214">네트워크에서 하이브리드 연결에 대한 고가용성이 필요한 경우에는 개별 컴퓨터에서 여러 HCM을 인스턴스화하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-214">If you want high availability on your hybrid connections from your network, simply instantiate multiple HCMs on separate machines.</span></span> 

### <a name="manually-adding-a-hybrid-connection"></a><span data-ttu-id="b1453-215">수동으로 하이브리드 연결 추가</span><span class="sxs-lookup"><span data-stu-id="b1453-215">Manually adding a hybrid connection</span></span> ###

<span data-ttu-id="b1453-216">공유 하기 원하는 경우 다른 사람이 구독 toohost 외부에서 특정된 하이브리드 연결의 HCM 인스턴스 hello hello 하이브리드 연결에 대 한 게이트웨이 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-216">If you wish somebody outside of your subscription toohost an HCM instance for a given hybrid connection, you can share with them hello gateway connection string for hello hybrid connection.</span></span>  <span data-ttu-id="b1453-217">하이브리드 연결 hello에 대 한 hello 속성에서 볼 수 있습니다 [Azure 포털][portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-217">You can see this in hello properties for a hybrid connection in hello [Azure portal][portal].</span></span> <span data-ttu-id="b1453-218">문자열, toouse 클릭 hello **수동으로 구성** hello HCM 단추를 선택한 hello 게이트웨이 연결 문자열에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-218">toouse that string, click hello **Configure manually** button in hello HCM and paste in hello gateway connection string.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="b1453-219">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b1453-219">Troubleshooting</span></span> ##

<span data-ttu-id="b1453-220">경우 실행 중인 응용 프로그램으로 하이브리드 연결 설정 된 해당 하이브리드 연결이 구성 되어 있는 하나 이상의 HCM는 힙이고 hello 상태는 예를 들어 **연결 됨** hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-220">When your hybrid connection is set up with a running application and there is at least one HCM that has that hybrid connection configured, then hello status will say **Connected** in hello portal.</span></span>  <span data-ttu-id="b1453-221">아니면 경우 **연결 됨** 는 앱 다운 되었거나 프로그램 HCM tooAzure 포트 80 또는 443에서 아웃 연결할 수 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-221">If it does not say **Connected** then it means that either your app is down or your HCM cannot connect out tooAzure on ports 80 or 443.</span></span>  

<span data-ttu-id="b1453-222">hello 클라이언트가 tootheir 끝점을 연결할 수 없습니다는 때문 DNS 이름 대신 IP 주소를 사용 하 여 지정 된 hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-222">hello primary reason that clients cannot connect tootheir endpoint is because hello endpoint was specified using an IP address instead of a DNS name.</span></span>  <span data-ttu-id="b1453-223">응용 프로그램 hello 원하는 끝점에 도달할 수 없는 IP 주소를 사용 하는 경우 toousing hello hello HCM 실행 중인 호스트에 유효한 DNS 이름 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-223">If your app cannot reach hello desired endpoint and you used an IP address, switch toousing a DNS name that is valid on hello host where hello HCM is running.</span></span>  <span data-ttu-id="b1453-224">다른 작업 toocheck 여기서 hello HCM 실행 되 고 hello hello HCM 실행 중인 호스트 toohello 하이브리드 연결 끝점에서에서 연결 하는 hello 호스트에서 해당 hello DNS 이름을 제대로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-224">Other things toocheck are that hello DNS name resolves properly on hello host where hello HCM is running and that there is connectivity from hello host where hello HCM is running toohello hybrid connection endpoint.</span></span>  

<span data-ttu-id="b1453-225">Hello tcpping 라는 hello 콘솔에서 호출 될 수 있는 응용 프로그램 서비스에에서는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-225">There is a tool in hello App Service that can be invoked from hello console called tcpping.</span></span>  <span data-ttu-id="b1453-226">이 도구 액세스 tooa TCP 끝점을 포함 하는 경우 하지만 알려주지 않습니다 액세스 tooa 하이브리드 연결 끝점 있는지 알려 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-226">This tool can tell you if you have access tooa TCP endpoint but does not tell you if you have access tooa hybrid connection endpoint.</span></span>  <span data-ttu-id="b1453-227">하이브리드 연결 끝점에 대해 hello 콘솔에 사용 하면, 성공적인 ping만 알려 해당 호스트: 포트 조합 하 여 사용 하는 앱에 대해 구성 된 하이브리드 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-227">When used in hello console against a hybrid connection endpoint, a successful ping will only tell you that you have a hybrid connection configured for your app that uses that host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="b1453-228">BizTalk 하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="b1453-228">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="b1453-229">BizTalk 하이브리드 연결 기능을 이전 hello toofurther BizTalk 하이브리드 연결 만들기 오프 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-229">hello older BizTalk Hybrid Connections capability has been closed off toofurther BizTalk Hybrid Connection creations.</span></span>  <span data-ttu-id="b1453-230">앱과 기존 BizTalk 하이브리드 연결을 사용 하 여 계속할 수 있지만 toohello 새 서비스를 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-230">You can continue using your preexisting BizTalk Hybrid Connections with your apps but should migrate toohello new service.</span></span>  <span data-ttu-id="b1453-231">Hello 간에 hello BizTalk 버전에 비해 hello 새 서비스의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-231">Among hello benefits in hello new service over hello BizTalk version are:</span></span>

- <span data-ttu-id="b1453-232">추가 BizTalk 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-232">no additional BizTalk account is required</span></span>
- <span data-ttu-id="b1453-233">BizTalk 하이브리드 연결에서 TLS는 1.0이 아닌 1.2입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-233">TLS is 1.2 instead of 1.0 as in BizTalk Hybrid Connections</span></span>
- <span data-ttu-id="b1453-234">통신은 포트 80 및 443 IP 주소 대신 DNS 이름 tooreach Azure와 추가의 범위를 사용 하 여 다른 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-234">Communication is over ports 80 and 443 using a DNS name tooreach Azure instead of IP addresses and a range of additional other ports.</span></span>  

<span data-ttu-id="b1453-235">BizTalk 하이브리드 연결 tooyour 앱, tooadd hello에서는 이동 tooyour app [Azure 포털] [ portal] 클릭 **네트워킹 > 하이브리드 연결 끝점 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-235">tooadd a BizTalk hybrid connection tooyour app, go tooyour app in hello [Azure portal][portal] and click **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="b1453-236">Hello 클래식 하이브리드 연결 테이블에서 클릭 **클래식 하이브리드 연결을 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-236">In hello Classic hybrid connections table click **Add classic hybrid connection**.</span></span>  <span data-ttu-id="b1453-237">여기에 BizTalk 하이브리드 연결 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1453-237">From here you will see a list of your BizTalk hybrid connections.</span></span>  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

