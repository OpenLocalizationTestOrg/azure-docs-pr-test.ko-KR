---
title: "Azure App Service 하이브리드 연결 | Microsoft Docs"
description: "하이브리드 연결을 만들고 사용하여 서로 다른 네트워크의 리소스에 액세스하는 방법"
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
ms.openlocfilehash: fef9e7b280387934cb093f51b4c8aa134a3b87e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="a7f5f-103">Azure App Service 하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="a7f5f-103">Azure App Service Hybrid Connections</span></span> #

## <a name="overview"></a><span data-ttu-id="a7f5f-104">개요</span><span class="sxs-lookup"><span data-stu-id="a7f5f-104">Overview</span></span> ##

<span data-ttu-id="a7f5f-105">하이브리드 연결은 Azure의 서비스인 동시에 Azure App Service의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-105">Hybrid Connections is both a service in Azure as well as a feature in the Azure App Service.</span></span>  <span data-ttu-id="a7f5f-106">서비스로서 하이브리드 연결은 Azure App Service에서 제공되는 것보다 많은 용도와 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-106">As a service it has use and capabilities beyond those that are leveraged in the Azure App Service.</span></span>  <span data-ttu-id="a7f5f-107">하이브리드 연결 및 Azure App Service 외부에서의 관련 사용법을 자세히 알아보려면 [Azure Relay 하이브리드 연결][HCService]에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-107">To learn more about Hybrid Connections and their usage outside of the Azure App Service you can start here, [Azure Relay Hybrid Connections][HCService]</span></span>

<span data-ttu-id="a7f5f-108">Azure App Service 내에서 하이브리드 연결은 다른 네트워크의 응용 프로그램 리소스에 액세스하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-108">Within the Azure App Service, hybrid connections can be used to access application resources in other networks.</span></span> <span data-ttu-id="a7f5f-109">하이브리드 연결을 통해 앱에서 응용 프로그램 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-109">It provides access FROM your app TO an application endpoint.</span></span>  <span data-ttu-id="a7f5f-110">응용 프로그램에 액세스하는 대체 기능으로는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-110">It does not enable an alternative capability to access your application.</span></span>  <span data-ttu-id="a7f5f-111">App Service에서 사용되는 것처럼 각 하이브리드 연결은 단일 TCP 호스트 및 포트 조합에 상호 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-111">As used in the App Service, each hybrid connection correlates to a single TCP host and port combination.</span></span>  <span data-ttu-id="a7f5f-112">즉, TCP 수신 포트를 대상으로 하는 한, 하이브리드 연결 끝점은 모든 운영 체제 및 모든 응용 프로그램에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-112">This means that the hybrid connection endpoint can be on any operating system and any application provided you are hitting a TCP listening port.</span></span> <span data-ttu-id="a7f5f-113">하이브리드 연결은 응용 프로그램 프로토콜이 무엇인지 또는 사용자가 무엇에 액세스하고 있는지 인식하거나 상관하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-113">Hybrid connections does not know or care what the application protocol is or what you are accessing.</span></span>  <span data-ttu-id="a7f5f-114">단지 네트워크 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-114">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="a7f5f-115">작동 방법</span><span class="sxs-lookup"><span data-stu-id="a7f5f-115">How it works</span></span> ##
<span data-ttu-id="a7f5f-116">하이브리드 연결 기능은 Service Bus Relay에 대한 두 개의 아웃바운드 호출로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-116">The hybrid connections feature consists of two outbound calls to Service Bus Relay.</span></span>  <span data-ttu-id="a7f5f-117">App Service에서 앱이 실행되고 있는 호스트의 라이브러리에서의 연결과, HCM(하이브리드 연결 관리자)에서 Service Bus Relay로의 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-117">There is a connection from a library on the host where your app is running in the app service and then there is a connection from the Hybrid Connection Manager(HCM) to Service Bus relay.</span></span>  <span data-ttu-id="a7f5f-118">HCM은 네트워크 호스팅 내에서 배포하는 릴레이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-118">The HCM is a relay service that you deploy within the network hosting</span></span> 

<span data-ttu-id="a7f5f-119">앱에는 이 두 개의 결합된 연결을 통해 HCM의 다른 쪽에 고정 호스트:포트 조합에 대한 TCP 터널이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-119">Through the two joined connections your app has a TCP tunnel to a fixed host:port combination on the other side of the HCM.</span></span>  <span data-ttu-id="a7f5f-120">연결 시 보안을 위해 TLS 1.2를 사용하고 인증/권한 부여를 위해 SAS 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-120">The connection uses TLS 1.2 for security and SAS keys for authentication/authorization.</span></span>    

![][1]

<span data-ttu-id="a7f5f-121">앱이 구성 하이브리드 연결 끝점과 일치하는 DNS 요청을 실행하면 아웃바운드 TCP 트래픽이 하이브리드 연결 아래로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-121">When your app makes a DNS request that matches a configure Hybrid Connection endpoint, then the outbound TCP traffic will be redirected down the hybrid connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="a7f5f-122">이는 항상 하이브리드 연결에 DNS 이름을 사용해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-122">This means that you should try to always use a DNS name for your Hybrid Connection.</span></span>  <span data-ttu-id="a7f5f-123">일부 클라이언트 소프트웨어는 끝점에서 IP 주소를 사용하는 경우 DNS 조회를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-123">Some client software does not do a DNS lookup if the endpoint uses an IP address instead.</span></span>
>
>

<span data-ttu-id="a7f5f-124">하이브리드 연결의 유형은 두 가지로, 하나는 Azure Relay 서비스로 제공되는 새로운 하이브리드 연결과 이전 BizTalk 하이브리드 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-124">There are two types of hybrid connections, the new hybrid connections that are offered as a service under Azure Relay and the older BizTalk Hybrid Connections.</span></span>  <span data-ttu-id="a7f5f-125">이전 BizTalk 하이브리드 연결은 포털에서 클래스 하이브리드 연결이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-125">The older BizTalk Hybrid Connections are referred to as Classic Hybrid Connections in the portal.</span></span>  <span data-ttu-id="a7f5f-126">이 문서의 뒷부분에서 이에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-126">There is more information later in this document about them.</span></span>

### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="a7f5f-127">App Service 하이브리드 연결의 장점</span><span class="sxs-lookup"><span data-stu-id="a7f5f-127">App Service hybrid connection benefits</span></span> ###

<span data-ttu-id="a7f5f-128">하이브리드 연결 기능에는 다음과 같은 많은 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-128">There are a number of benefits to the hybrid connections capability including</span></span>

- <span data-ttu-id="a7f5f-129">앱이 온-프레미스 시스템 및 서비스에 안전하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-129">Apps can securely access on premises systems and services securely</span></span>
- <span data-ttu-id="a7f5f-130">기능에 인터넷 액세스 가능한 끝점이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-130">the feature does not require an internet accessible endpoint</span></span>
- <span data-ttu-id="a7f5f-131">빠르고 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-131">it is quick and easy to set up</span></span>  
- <span data-ttu-id="a7f5f-132">각 하이브리드 연결이 단일 호스트:포트 조합과 일치하므로 보안 측면에서 우수합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-132">each hybrid connection matches to a single host:port combination which is an excellent security aspect</span></span>
- <span data-ttu-id="a7f5f-133">연결이 모두 표준 웹 포트를 통해 아웃바운드되므로 일반적으로 방화벽 구멍이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-133">it normally does not require firewall holes as the connections are all outbound over standard web ports</span></span>
- <span data-ttu-id="a7f5f-134">기능이 네트워크 수준이므로 이는 앱에서 사용되는 언어 및 끝점에서 사용되는 기술과 관계없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-134">because the feature is network level that also means that it is agnostic to the language used by your app and the technology used by the endpoint</span></span>
- <span data-ttu-id="a7f5f-135">단일 앱에서 여러 네트워크에 액세스하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-135">it can be used to provide access in multiple networks from a single app</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="a7f5f-136">하이브리드 연결로 할 수 없는 작업</span><span class="sxs-lookup"><span data-stu-id="a7f5f-136">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="a7f5f-137">하이브리드 연결로 할 수 없는 몇 가지 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-137">There are a few things you cannot do with hybrid connections and they include:</span></span>

- <span data-ttu-id="a7f5f-138">드라이브 탑재</span><span class="sxs-lookup"><span data-stu-id="a7f5f-138">mounting a drive</span></span>
- <span data-ttu-id="a7f5f-139">UDP 사용</span><span class="sxs-lookup"><span data-stu-id="a7f5f-139">using UDP</span></span>
- <span data-ttu-id="a7f5f-140">FTP 수동 모드 또는 확장 수동 모드 같은 동적 포트를 사용하는 TCP 기반 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="a7f5f-140">accessing TCP based services that use dynamic ports such as FTP Passive Mode or Extended Passive Mode</span></span>
- <span data-ttu-id="a7f5f-141">LDAP 지원(경우에 따라 UDP가 필요하므로)</span><span class="sxs-lookup"><span data-stu-id="a7f5f-141">LDAP support, as it sometimes requires UDP</span></span>
- <span data-ttu-id="a7f5f-142">Active Directory 지원</span><span class="sxs-lookup"><span data-stu-id="a7f5f-142">Active Directory support</span></span>

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a><span data-ttu-id="a7f5f-143">앱에서 하이브리드 연결 추가 및 만들기</span><span class="sxs-lookup"><span data-stu-id="a7f5f-143">Adding and Creating a Hybrid Connection in your App</span></span> ##

<span data-ttu-id="a7f5f-144">하이브리드 연결은 앱 포털 또는 하이브리드 연결 서비스 포털을 통해 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-144">Hybrid Connections can be created through the app portal or from the Hybrid Connection service portal.</span></span>  <span data-ttu-id="a7f5f-145">앱에서 사용할 하이브리드 연결을 만드는 데는 앱 포털을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-145">It is highly recommended that you use the app portal to create the Hybrid Connections you wish to use with your app.</span></span>  <span data-ttu-id="a7f5f-146">하이브리드 연결을 만들려면 [Azure Portal][portal]로 이동하고 해당 앱의 UI로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-146">To create a Hybrid Connection go to the [Azure portal][portal] and go into the UI for your app.</span></span>  <span data-ttu-id="a7f5f-147">**네트워킹 > 하이브리드 연결 끝점 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-147">Select **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="a7f5f-148">여기서 앱에서 구성된 하이브리드 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-148">From here you can see the Hybrid Connections that are configured with your app</span></span>  

![][2]

<span data-ttu-id="a7f5f-149">새 하이브리드 연결을 추가하려면 [하이브리드 연결 추가]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-149">To add a new Hybrid Connection, click Add Hybrid Connection.</span></span>  <span data-ttu-id="a7f5f-150">열리는 UI에는 이미 만들어진 하이브리드 연결이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-150">The UI that opens up lists the Hybrid Connections that you have already created.</span></span>  <span data-ttu-id="a7f5f-151">하이브리드 연결을 하나 이상 앱에 추가하려면 원하는 항목을 클릭하고 **선택한 하이브리드 연결 추가**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-151">To add one or more of them to your app, click on the ones you want and hit **Add selected hybrid connection**.</span></span>  

![][3]

<span data-ttu-id="a7f5f-152">새 하이브리드 연결을 만들려면 **새 하이브리드 연결 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-152">If you want to create a new Hybrid Connection, click **Create new hybrid connection**.</span></span>  <span data-ttu-id="a7f5f-153">여기에서 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-153">From here you specify the:</span></span> 

- <span data-ttu-id="a7f5f-154">끝점 이름</span><span class="sxs-lookup"><span data-stu-id="a7f5f-154">endpoint name</span></span>
- <span data-ttu-id="a7f5f-155">끝점 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="a7f5f-155">endpoint hostname</span></span>
- <span data-ttu-id="a7f5f-156">끝점 포트</span><span class="sxs-lookup"><span data-stu-id="a7f5f-156">endpoint port</span></span>
- <span data-ttu-id="a7f5f-157">사용할 Service Bus 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="a7f5f-157">servicebus namespace you wish to use</span></span>

![][4]

<span data-ttu-id="a7f5f-158">모든 하이브리드 연결은 Service Bus 네임스페이스에 연결되고 각 Service Bus 네임스페이스는 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-158">Every hybrid connection is tied to a service bus namespace and each service bus namespace is in an Azure region.</span></span>  <span data-ttu-id="a7f5f-159">네트워크에서 발생하는 대기 시간을 피하려면 앱과 같은 지역에서 Service Bus 네임스페이스를 시도하고 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-159">It is important to try and use a service bus namespace in the same region as your app so as to avoid network induced latency.</span></span>

<span data-ttu-id="a7f5f-160">앱에서 하이브리드 연결을 제거하려면 해당 항목을 마우스 오른쪽 단추로 클릭하고 **연결 끊기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-160">If you want to remove your hybrid connection from your app, right click on it and select **Disconnect**.</span></span>  

<span data-ttu-id="a7f5f-161">하이브리드 연결이 웹앱에 추가되면 웹앱을 클릭하여 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-161">Once a hybrid connection is added to your web app, you can see details on it by simply clicking on it.</span></span>  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="a7f5f-162">하이브리드 연결 및 App Service 계획</span><span class="sxs-lookup"><span data-stu-id="a7f5f-162">Hybrid Connections and App Service Plans</span></span> ##

<span data-ttu-id="a7f5f-163">현재 만들 수 있는 하이브리드 연결은 새로운 하이브리드 연결뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-163">The only hybrid connections you can now make are the new hybrid connections.</span></span>  <span data-ttu-id="a7f5f-164">하이브리드 연결은 기본, 표준, 프리미엄 및 격리 요금제 SKU에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-164">They are only available in Basic, Standard, Premium and Isolated pricing SKUs.</span></span>  <span data-ttu-id="a7f5f-165">요금제에는 연결된 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-165">There are limits tied to the pricing plan.</span></span>  

| <span data-ttu-id="a7f5f-166">요금제</span><span class="sxs-lookup"><span data-stu-id="a7f5f-166">Pricing Plan</span></span> | <span data-ttu-id="a7f5f-167">요금제에서 사용 가능한 하이브리드 연결 수</span><span class="sxs-lookup"><span data-stu-id="a7f5f-167">Number of hybrid connections usable in the plan</span></span> |
|----|----|
| <span data-ttu-id="a7f5f-168">Basic</span><span class="sxs-lookup"><span data-stu-id="a7f5f-168">Basic</span></span> | <span data-ttu-id="a7f5f-169">5</span><span class="sxs-lookup"><span data-stu-id="a7f5f-169">5</span></span> |
| <span data-ttu-id="a7f5f-170">Standard</span><span class="sxs-lookup"><span data-stu-id="a7f5f-170">Standard</span></span> | <span data-ttu-id="a7f5f-171">25</span><span class="sxs-lookup"><span data-stu-id="a7f5f-171">25</span></span> |
| <span data-ttu-id="a7f5f-172">Premium</span><span class="sxs-lookup"><span data-stu-id="a7f5f-172">Premium</span></span> | <span data-ttu-id="a7f5f-173">200</span><span class="sxs-lookup"><span data-stu-id="a7f5f-173">200</span></span> |
| <span data-ttu-id="a7f5f-174">격리</span><span class="sxs-lookup"><span data-stu-id="a7f5f-174">Isolated</span></span> | <span data-ttu-id="a7f5f-175">200</span><span class="sxs-lookup"><span data-stu-id="a7f5f-175">200</span></span> |

<span data-ttu-id="a7f5f-176">App Service 계획 제한 사항이 있으므로 App Service 계획에는 사용 중인 하이브리드 연결 수 및 연결이 사용되는 앱을 보여 주는 UI도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-176">Since there are App Service Plan restrictions there is also UI in the App Service Plan that shows you how many hybrid connections are being used and by what apps.</span></span>  

![][6]

<span data-ttu-id="a7f5f-177">앱 보기와 같이 하이브리드 연결을 클릭하여 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-177">Just as with the app view, you can see details on your hybrid connection by clicking on it.</span></span>  <span data-ttu-id="a7f5f-178">여기 표시된 속성에서 앱 보기에 있는 모든 정보를 확인할 수 있지만 같은 App Service 계획에서 해당 하이브리드 연결을 사용 중인 다른 앱 수도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-178">In the properties shown here you can see all the information you had at the app view but can also see how many other apps in the same App Service Plan are using that hybrid connection.</span></span>

![][7]

<span data-ttu-id="a7f5f-179">App Service 계획에서 사용할 수 있는 하이브리드 연결 끝점 수에는 제한이 있지만 사용되는 각 하이브리드 연결은 해당 App Service 계획의 앱 전체에서 제한 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-179">While there is a limit on the number of hybrid connection endpoints that can be used in an App Service Plan, each hybrid connection used can be used across any number of apps in that App Service Plan.</span></span>  <span data-ttu-id="a7f5f-180">즉, 내 App Service 계획에서 1개의 하이브리드 연결을 5개의 서로 다른 응용 프로그램에 사용했어도 하이브리드 연결 개수는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-180">That is to say that if I had 1 hybrid connection that I used in 5 separate apps in my App Service Plan, that is still just 1 hybrid connection.</span></span>

<span data-ttu-id="a7f5f-181">기본, 표준, 프리미엄 또는 격리 SKU에서만 사용 가능한 개수를 초과한 하이브리드 연결에는 추가 비용이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-181">There is an additional cost to hybrid connections beyond being only usable in a Basic, Standard, Premium or Isolated SKU.</span></span>  <span data-ttu-id="a7f5f-182">하이브리드 연결 가격 책정에 대한 자세한 내용은 [Service Bus 가격 책정][sbpricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-182">For details on hybrid connection pricing please go here: [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="a7f5f-183">하이브리드 연결 관리자</span><span class="sxs-lookup"><span data-stu-id="a7f5f-183">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="a7f5f-184">하이브리드 연결이 작동하려면 하이브리드 연결 끝점을 호스트하는 릴레이 에이전트가 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-184">In order for hybrid connections to work you need a relay agent in the network that hosts your hybrid connection endpoint.</span></span>  <span data-ttu-id="a7f5f-185">이 릴레이 에이전트를 HCM(하이브리드 연결 관리자)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-185">That relay agent is called the Hybrid Connection Manager (HCM).</span></span>  <span data-ttu-id="a7f5f-186">이 도구는 [Azure Portal][portal]의 앱에서 사용 가능한 **네트워킹 > 하이브리드 연결 끝점 구성** UI에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-186">This tool can be downloaded from the **Networking > Configure your hybrid connection endpoints** UI available from your app in the [Azure portal][portal].</span></span>  

<span data-ttu-id="a7f5f-187">이 도구는 Windows의 Windows Server 2008 R2 이상 버전에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-187">This tool runs on Windows server 2008 R2 and later versions of Windows.</span></span>  <span data-ttu-id="a7f5f-188">설치된 후 HCM은 서비스로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-188">Once installed the HCM runs as a service.</span></span>  <span data-ttu-id="a7f5f-189">이 서비스는 구성된 끝점을 기준으로 Azure Service Bus 릴레이에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-189">This service connects to Azure servicebus relay based on the configured endpoints.</span></span>  <span data-ttu-id="a7f5f-190">HCM의 연결은 포트 80 및 443으로 아웃바운드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-190">The connections from the HCM are outbound to ports 80 and 443.</span></span>    

<span data-ttu-id="a7f5f-191">HCM에는 구성을 위한 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-191">The HCM has a UI to configure it.</span></span>  <span data-ttu-id="a7f5f-192">HCM이 설치된 후 하이브리드 연결 관리자 설치 디렉터리에 있는 HybridConnectionManagerUi.exe를 실행하여 UI를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-192">After the HCM is installed you can bring up the UI by running the HybridConnectionManagerUi.exe that sits in the Hybrid Connection Manager installation directory.</span></span>  <span data-ttu-id="a7f5f-193">Windows 10에서는 검색 상자에 *Hybrid Connection Manager UI*를 입력하여 UI에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-193">It is also easily reached on Windows 10 by typing *Hybrid Connection Manager UI* in your search box.</span></span>  

<span data-ttu-id="a7f5f-194">HCM UI가 시작되면 가장 먼저 이 HCM 인스턴스로 구성된 하이브리드 연결을 모두 나열한 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-194">When the HCM UI is started, the first thing you see is a table that lists all of the hybrid connections that are configured with this instance of the HCM.</span></span>  <span data-ttu-id="a7f5f-195">변경하려면 Azure를 통해 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-195">If you wish to make any changes you will need to authenticate with Azure.</span></span> 

<span data-ttu-id="a7f5f-196">HCM에 하나 이상의 하이브리드 연결을 추가하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-196">To add one or more Hybrid Connections to your HCM:</span></span>

1. <span data-ttu-id="a7f5f-197">HCM UI를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-197">Start the HCM UI</span></span>
1. <span data-ttu-id="a7f5f-198">[Configure another hybrid connection](다른 하이브리드 연결 구성)을 클릭합니다. ![][8]</span><span class="sxs-lookup"><span data-stu-id="a7f5f-198">Click Configure another hybrid connection ![][8]</span></span>

1. <span data-ttu-id="a7f5f-199">Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-199">Sign in with your Azure account</span></span>
1. <span data-ttu-id="a7f5f-200">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-200">Choose a subscription</span></span>
1. <span data-ttu-id="a7f5f-201">이 HCM이 릴레이할 하이브리드 연결을 클릭합니다. ![][9]</span><span class="sxs-lookup"><span data-stu-id="a7f5f-201">Click on the hybrid connections you want this HCM to relay ![][9]</span></span>

1. <span data-ttu-id="a7f5f-202">저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-202">Click Save</span></span>

<span data-ttu-id="a7f5f-203">이때 추가한 하이브리드 연결이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-203">At this point you will see the hybrid connections you added.</span></span>  <span data-ttu-id="a7f5f-204">구성된 하이브리드 연결을 클릭하고 연결에 대한 세부 정보를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-204">You can also click on the configured hybrid connection and see details about the connection.</span></span>

![][10]

<span data-ttu-id="a7f5f-205">HCM에서 구성된 하이브리드 연결을 지원하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-205">For your HCM to be able to support the hybrid connections it is configured with, it needs:</span></span>

- <span data-ttu-id="a7f5f-206">포트 80 및 443을 통한 Azure에 대한 TCP 액세스</span><span class="sxs-lookup"><span data-stu-id="a7f5f-206">TCP access to Azure over ports 80 and 443</span></span>
- <span data-ttu-id="a7f5f-207">하이브리드 연결 끝점에 대한 TCP 액세스</span><span class="sxs-lookup"><span data-stu-id="a7f5f-207">TCP access to the hybrid connection endpoint</span></span>
- <span data-ttu-id="a7f5f-208">끝점 호스트 및 Azure Service Bus 네임스페이스에서 DNS 조회를 수행할 수 있음</span><span class="sxs-lookup"><span data-stu-id="a7f5f-208">ability to do DNS look ups on the endpoint host and the azure servicebus namespace</span></span>

<span data-ttu-id="a7f5f-209">HCM은 이전 BizTalk 하이브리드 연결과 새로운 하이브리드 연결을 둘 다 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-209">The HCM supports both new hybrid connections as well as the older BizTalk hybrid connections.</span></span>

### <a name="redundancy"></a><span data-ttu-id="a7f5f-210">중복</span><span class="sxs-lookup"><span data-stu-id="a7f5f-210">Redundancy</span></span> ###

<span data-ttu-id="a7f5f-211">각 HCM은 여러 하이브리드 연결을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-211">Each HCM can support multiple hybrid connections.</span></span>  <span data-ttu-id="a7f5f-212">특정 하이브리드 연결이 여러 HCM에서 지원될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-212">Also, any given hybrid connection can be supported by multiple HCMs.</span></span>  <span data-ttu-id="a7f5f-213">기본 동작은 특정 끝점에 대해 구성된 HCM에 걸쳐 트래픽을 라운드 로빈 방식으로 순환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-213">The default behavior is to round robin traffic across the configured HCMs for any given endpoint.</span></span>  <span data-ttu-id="a7f5f-214">네트워크에서 하이브리드 연결에 대한 고가용성이 필요한 경우에는 개별 컴퓨터에서 여러 HCM을 인스턴스화하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-214">If you want high availability on your hybrid connections from your network, simply instantiate multiple HCMs on separate machines.</span></span> 

### <a name="manually-adding-a-hybrid-connection"></a><span data-ttu-id="a7f5f-215">수동으로 하이브리드 연결 추가</span><span class="sxs-lookup"><span data-stu-id="a7f5f-215">Manually adding a hybrid connection</span></span> ###

<span data-ttu-id="a7f5f-216">구독 외부에서 사용자가 특정 하이브리드 연결에 대한 HCM 인스턴스를 호스트하게 하려면 해당 하이브리드 연결에 대한 게이트웨이 연결 문자열을 공유하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-216">If you wish somebody outside of your subscription to host an HCM instance for a given hybrid connection, you can share with them the gateway connection string for the hybrid connection.</span></span>  <span data-ttu-id="a7f5f-217">[Azure Portal][portal]의 하이브리드 연결 속성에서 이 문자열을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-217">You can see this in the properties for a hybrid connection in the [Azure portal][portal].</span></span> <span data-ttu-id="a7f5f-218">이 문자열을 사용하려면 HCM에서 **수동으로 구성** 단추를 클릭하고 게이트웨이 연결 문자열에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-218">To use that string, click the **Configure manually** button in the HCM and paste in the gateway connection string.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="a7f5f-219">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a7f5f-219">Troubleshooting</span></span> ##

<span data-ttu-id="a7f5f-220">실행 중인 응용 프로그램과의 하이브리드 연결이 설정되고 하나 이상의 HCM에 이 하이브리드 연결이 구성되어 있으면 포털에서 상태가 **연결됨**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-220">When your hybrid connection is set up with a running application and there is at least one HCM that has that hybrid connection configured, then the status will say **Connected** in the portal.</span></span>  <span data-ttu-id="a7f5f-221">**연결됨**으로 표시되지 않으면 앱이 다운되거나 HCM이 포트 80 또는 443에서 Azure로 연결될 수 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-221">If it does not say **Connected** then it means that either your app is down or your HCM cannot connect out to Azure on ports 80 or 443.</span></span>  

<span data-ttu-id="a7f5f-222">클라이언트가 끝점에 연결할 수 없는 주된 이유는 끝점이 DNS 이름이 아닌 IP 주소를 사용하여 지정되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-222">The primary reason that clients cannot connect to their endpoint is because the endpoint was specified using an IP address instead of a DNS name.</span></span>  <span data-ttu-id="a7f5f-223">앱이 원하는 끝점에 도달할 수 없고 IP 주소가 사용되었으면 HCM이 실행 중인 호스트에서 유효한 DNS 이름을 사용하도록 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-223">If your app cannot reach the desired endpoint and you used an IP address, switch to using a DNS name that is valid on the host where the HCM is running.</span></span>  <span data-ttu-id="a7f5f-224">HCM이 실행 중인 호스트에서 DNS 이름이 제대로 확인되고 HCM이 실행 중인 호스트에서 하이브리드 연결 끝점으로 연결이 설정되어 있는지도 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-224">Other things to check are that the DNS name resolves properly on the host where the HCM is running and that there is connectivity from the host where the HCM is running to the hybrid connection endpoint.</span></span>  

<span data-ttu-id="a7f5f-225">App Service에는 콘솔에서 호출할 수 있는 tcpping이라는 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-225">There is a tool in the App Service that can be invoked from the console called tcpping.</span></span>  <span data-ttu-id="a7f5f-226">이 도구를 통해 TCP 끝점에 액세스할 수 있는지 알 수 있지만 하이브리드 연결 끝점에 액세스할 수 있는지는 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-226">This tool can tell you if you have access to a TCP endpoint but does not tell you if you have access to a hybrid connection endpoint.</span></span>  <span data-ttu-id="a7f5f-227">콘솔에서 하이브리드 연결 끝점에 사용될 경우 성공한 ping은 호스트:포트 조합을 사용하는 앱에 구성된 하이브리드 연결이 있다는 것을 알려줄 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-227">When used in the console against a hybrid connection endpoint, a successful ping will only tell you that you have a hybrid connection configured for your app that uses that host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="a7f5f-228">BizTalk 하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="a7f5f-228">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="a7f5f-229">이전 BizTalk 하이브리드 연결 기능의 경우 추가 BizTalk 하이브리드 연결 만들기가 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-229">The older BizTalk Hybrid Connections capability has been closed off to further BizTalk Hybrid Connection creations.</span></span>  <span data-ttu-id="a7f5f-230">앱에 있는 기존 BizTalk 하이브리드 연결은 계속 사용할 수 있지만 새 서비스로 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-230">You can continue using your preexisting BizTalk Hybrid Connections with your apps but should migrate to the new service.</span></span>  <span data-ttu-id="a7f5f-231">BizTalk 버전에 비해 새 서비스의 몇 가지 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-231">Among the benefits in the new service over the BizTalk version are:</span></span>

- <span data-ttu-id="a7f5f-232">추가 BizTalk 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-232">no additional BizTalk account is required</span></span>
- <span data-ttu-id="a7f5f-233">BizTalk 하이브리드 연결에서 TLS는 1.0이 아닌 1.2입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-233">TLS is 1.2 instead of 1.0 as in BizTalk Hybrid Connections</span></span>
- <span data-ttu-id="a7f5f-234">통신이 IP 주소 및 추가적인 기타 포트 범위 대신 DNS 이름을 사용하여 포트 80 및 443을 통해 Azure에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-234">Communication is over ports 80 and 443 using a DNS name to reach Azure instead of IP addresses and a range of additional other ports.</span></span>  

<span data-ttu-id="a7f5f-235">BizTalk 하이브리드 연결을 앱에 추가하려면 [Azure Portal][portal]에서 해당 앱으로 이동하고 **네트워킹 > 하이브리드 연결 끝점 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-235">To add a BizTalk hybrid connection to your app, go to your app in the [Azure portal][portal] and click **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="a7f5f-236">클래식 하이브리드 연결 표에서 **클래식 하이브리드 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-236">In the Classic hybrid connections table click **Add classic hybrid connection**.</span></span>  <span data-ttu-id="a7f5f-237">여기에 BizTalk 하이브리드 연결 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f5f-237">From here you will see a list of your BizTalk hybrid connections.</span></span>  


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

