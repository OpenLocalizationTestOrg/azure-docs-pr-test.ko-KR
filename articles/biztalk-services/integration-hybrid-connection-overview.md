---
title: "aaaHybrid 연결 개요 | Microsoft Docs"
description: "하이브리드 연결, 보안, TCP 포트 및 지원되는 구성에 대해 알아봅니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a><span data-ttu-id="2d18b-104">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="2d18b-104">Hybrid Connections overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d18b-105">BizTalk 하이브리드 연결은 사용 중지되고 App Service 하이브리드 연결로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="2d18b-106">를 비롯 한 자세한 내용은 toomanage 기존 BizTalk 하이브리드 연결을 확인 하려면 어떻게 해야 [Azure 앱 서비스 하이브리드 연결](../app-service/app-service-hybrid-connections.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-106">For more information, including how toomanage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>

<span data-ttu-id="2d18b-107">목록 hello 필요한 TCP 포트 및 소개 tooHybrid 연결을 지원 hello 구성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-107">Introduction tooHybrid Connections, lists hello supported configurations, and lists hello required TCP ports.</span></span>

## <a name="what-is-a-hybrid-connection"></a><span data-ttu-id="2d18b-108">하이브리드 연결 정의</span><span class="sxs-lookup"><span data-stu-id="2d18b-108">What is a hybrid connection</span></span>
<span data-ttu-id="2d18b-109">하이브리드 연결은 Azure BizTalk 서비스의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-109">Hybrid Connections are a feature of Azure BizTalk Services.</span></span> <span data-ttu-id="2d18b-110">하이브리드 연결 Azure 앱 서비스 (이전의 웹 사이트)에 있는 간편 하 고 편리한 tooconnect hello 웹 응용 프로그램 기능이 및 Azure 앱 서비스 (이전의 모바일 서비스) tooon 온-프레미스 리소스 방화벽 뒤의 hello 모바일 앱 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-110">Hybrid Connections provide an easy and convenient way tooconnect hello Web Apps feature in Azure App Service (formerly Websites) and hello Mobile Apps feature in Azure App Service (formerly Mobile Services) tooon-premises resources behind your firewall.</span></span>

![하이브리드 연결][HCImage]

<span data-ttu-id="2d18b-112">하이브리드 연결은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-112">Hybrid Connections benefits include:</span></span>

* <span data-ttu-id="2d18b-113">웹앱 및 모바일 앱은 기존 온-프레미스 데이터 및 서비스에 안전하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-113">Web Apps and Mobile Apps can access existing on-premises data and services securely.</span></span>
* <span data-ttu-id="2d18b-114">여러 웹 응용 프로그램 또는 모바일 앱에 하이브리드 연결 tooaccess 온-프레미스 리소스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-114">Multiple Web Apps or Mobile Apps can share a Hybrid Connection tooaccess an on-premises resource.</span></span>
* <span data-ttu-id="2d18b-115">최소한의 TCP 포트는 필요한 tooaccess 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-115">Minimal TCP ports are required tooaccess your network.</span></span>
* <span data-ttu-id="2d18b-116">하이브리드 연결을 사용 하 여 응용 프로그램 리소스에 액세스할만 hello 특정 온-프레미스 게시 된 hello 하이브리드 연결을 통해.</span><span class="sxs-lookup"><span data-stu-id="2d18b-116">Applications using Hybrid Connections access only hello specific on-premises resource that is published through hello Hybrid Connection.</span></span>
* <span data-ttu-id="2d18b-117">SQL Server, MySQL, HTTP 웹 Api 및 대부분의 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하 여 tooany 온-프레미스 리소스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-117">Can connect tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2d18b-118">동적 포트(예: FTP 수동 모드 또는 확장 수동 모드)를 사용하는 TCP 기반 서비스는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-118">TCP-based services that use dynamic ports (such as FTP Passive Mode or Extended Passive Mode) are currently not supported.</span></span> <span data-ttu-id="2d18b-119">LDAP도 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-119">LDAP is also not supported.</span></span> <span data-ttu-id="2d18b-120">LDAP는 고정 TCP 포트를 사용하지만 UDP도 사용할 수 있기 때문에</span><span class="sxs-lookup"><span data-stu-id="2d18b-120">LDAP uses a static TCP port but it could also use UDP.</span></span> <span data-ttu-id="2d18b-121">지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-121">As a result, it is not supported.</span></span>
  > 
  > 
* <span data-ttu-id="2d18b-122">웹앱에서 지원하는 모든 프레임워크(.NET, PHP, Java, Python, Node.js) 및 모바일 앱에서 지원하는 모든 프레임워크(Node.js, .NET)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-122">Can be used with all frameworks supported by Web Apps (.NET, PHP, Java, Python, Node.js) and Mobile Apps (Node.js, .NET).</span></span>
* <span data-ttu-id="2d18b-123">웹 앱 및 모바일 앱 정확 하 게 hello에서 온-프레미스 리소스에 액세스할 수 같은 방식으로 hello 웹 또는 모바일 앱에 있으면 로컬 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-123">Web Apps and Mobile Apps can access on-premises resources in exactly hello same way as if hello Web or Mobile App is located on your local network.</span></span> <span data-ttu-id="2d18b-124">예를 들어 hello 동일한 연결 문자열 사용 되는 온-프레미스 Azure에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-124">For example, hello same connection string used on-premises can also be used on Azure.</span></span>

<span data-ttu-id="2d18b-125">또한 하이브리드 연결 된 제어 및 포함 하는 하이브리드 응용 프로그램에서 액세스 하는 hello 회사 리소스에 대 한 가시성 엔터프라이즈 관리자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-125">Hybrid Connections also provide enterprise administrators with control and visibility into hello corporate resources accessed by hybrid applications, including:</span></span>

* <span data-ttu-id="2d18b-126">사용 하 여 그룹 정책 설정 관리자 수 hello 네트워크에서 하이브리드 연결을 허용 및 하이브리드 응용 프로그램에서 액세스할 수 있는 리소스를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-126">Using Group Policy settings, administrators can allow Hybrid Connections on hello network and also designate resources that can be accessed by hybrid applications.</span></span>
* <span data-ttu-id="2d18b-127">Hello 회사 네트워크에 이벤트 및 감사 로그 하이브리드 연결에서 액세스 하는 hello 리소스에 대 한 가시성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-127">Event and audit logs on hello corporate network provide visibility into hello resources accessed by Hybrid Connections.</span></span>

## <a name="example-scenarios"></a><span data-ttu-id="2d18b-128">예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="2d18b-128">Example scenarios</span></span>
<span data-ttu-id="2d18b-129">하이브리드 연결 프레임 워크 및 응용 프로그램 조합을 다음 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-129">Hybrid Connections support hello following framework and application combinations:</span></span>

* <span data-ttu-id="2d18b-130">.NET framework 액세스 tooSQL 서버</span><span class="sxs-lookup"><span data-stu-id="2d18b-130">.NET framework access tooSQL Server</span></span>
* <span data-ttu-id="2d18b-131">.NET framework 액세스 tooHTTP/HTTPS 웹 클라이언트와 서비스</span><span class="sxs-lookup"><span data-stu-id="2d18b-131">.NET framework access tooHTTP/HTTPS services with WebClient</span></span>
* <span data-ttu-id="2d18b-132">PHP 액세스 tooSQL Server, MySQL</span><span class="sxs-lookup"><span data-stu-id="2d18b-132">PHP access tooSQL Server, MySQL</span></span>
* <span data-ttu-id="2d18b-133">Java 액세스 tooSQL Server, MySQL 및 Oracle</span><span class="sxs-lookup"><span data-stu-id="2d18b-133">Java access tooSQL Server, MySQL and Oracle</span></span>
* <span data-ttu-id="2d18b-134">Java 액세스 tooHTTP/HTTPS 서비스</span><span class="sxs-lookup"><span data-stu-id="2d18b-134">Java access tooHTTP/HTTPS services</span></span>

<span data-ttu-id="2d18b-135">경우 tooaccess 하이브리드 연결을 사용 하 여 온-프레미스 SQL Server에 hello 다음을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-135">When using Hybrid Connections tooaccess on-premises SQL Server, consider hello following:</span></span>

* <span data-ttu-id="2d18b-136">SQL Express 명명 된 인스턴스에 고정 포트 구성된 toouse 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-136">SQL Express Named Instances must be configured toouse static ports.</span></span> <span data-ttu-id="2d18b-137">기본적으로 SQL Express 명명된 인스턴스는 동적 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-137">By default, SQL Express named instances use dynamic ports.</span></span>
* <span data-ttu-id="2d18b-138">SQL Express 기본 인스턴스는 정적 포트를 사용하지만 TCP를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-138">SQL Express Default Instances use a static port, but TCP must be enabled.</span></span> <span data-ttu-id="2d18b-139">기본적으로 TCP는 사용되도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-139">By default, TCP is not enabled.</span></span>
* <span data-ttu-id="2d18b-140">클러스터링 또는 가용성 그룹을 사용 하는 경우 hello `MultiSubnetFailover=true` 모드 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-140">When using Clustering or Availability Groups, hello `MultiSubnetFailover=true` mode is currently not supported.</span></span>
* <span data-ttu-id="2d18b-141">hello `ApplicationIntent=ReadOnly` 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-141">hello `ApplicationIntent=ReadOnly` is currently not supported.</span></span>
* <span data-ttu-id="2d18b-142">SQL 인증 hello Azure 응용 프로그램 및 hello 온-프레미스 SQL server에서 지 원하는 hello 종단 간 인증 방법으로 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-142">SQL Authentication may be required as hello end-to-end authorization method supported by hello Azure application and hello on-premises SQL server.</span></span>

## <a name="security-and-ports"></a><span data-ttu-id="2d18b-143">보안 및 포트</span><span class="sxs-lookup"><span data-stu-id="2d18b-143">Security and ports</span></span>
<span data-ttu-id="2d18b-144">공유 액세스 서명 (SAS) 권한 부여 toosecure hello 연결을 사용 하는 하이브리드 연결 hello Azure에서에서 응용 프로그램 및 hello 온-프레미스 하이브리드 연결 관리자 toohello 하이브리드 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-144">Hybrid Connections use Shared Access Signature (SAS) authorization toosecure hello connections from hello Azure applications and hello on-premises Hybrid Connection Manager toohello Hybrid Connection.</span></span> <span data-ttu-id="2d18b-145">Hello 응용 프로그램에 대 한 별도 연결 키는 만들어집니다 및 hello 온-프레미스 하이브리드 연결 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-145">Separate connection keys are created for hello application and hello on-premises Hybrid Connection Manager.</span></span> <span data-ttu-id="2d18b-146">이러한 연결 키는 별도로 롤오버되고 해지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-146">These connection keys can be rolled over and revoked independently.</span></span>

<span data-ttu-id="2d18b-147">하이브리드 연결의 hello 키 toohello 응용 프로그램 원활 하 고 안전한 배포를 위해 제공 하 고 hello 온-프레미스 하이브리드 연결 관리자.</span><span class="sxs-lookup"><span data-stu-id="2d18b-147">Hybrid Connections provide for seamless and secure distribution of hello keys toohello applications and hello on-premises Hybrid Connection Manager.</span></span>

<span data-ttu-id="2d18b-148">[하이브리드 연결 만들기 및 관리](integration-hybrid-connection-create-manage.md)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d18b-148">See [Create and Manage Hybrid Connections](integration-hybrid-connection-create-manage.md).</span></span>

<span data-ttu-id="2d18b-149">*응용 프로그램 권한 부여는 hello 하이브리드 연결을 별도로*합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-149">*Application authorization is separate from hello Hybrid Connection*.</span></span> <span data-ttu-id="2d18b-150">적절한 어떤 권한 부여 방법도 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-150">Any appropriate authorization method can be used.</span></span> <span data-ttu-id="2d18b-151">hello 권한 부여 방법 hello Azure 클라우드 및 온-프레미스 구성 요소 hello 간에 지원 hello 종단 간 권한 부여 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-151">hello authorization method depends on hello end-to-end authorization methods supported across hello Azure cloud and hello on-premises components.</span></span> <span data-ttu-id="2d18b-152">예를 들어 Azure 응용 프로그램은 온-프레미스 SQL Server에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-152">For example, your Azure application accesses an on-premises SQL Server.</span></span> <span data-ttu-id="2d18b-153">이 시나리오에서는 SQL 권한 부여를 지원된 하려면 종단 간 hello 권한 부여 방법 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-153">In this scenario, SQL Authorization may be hello authorization method that is supported end-to-end.</span></span>

#### <a name="tcp-ports"></a><span data-ttu-id="2d18b-154">TCP 포트</span><span class="sxs-lookup"><span data-stu-id="2d18b-154">TCP ports</span></span>
<span data-ttu-id="2d18b-155">하이브리드 연결에는 개인 네트워크의 아웃바운드 TCP 또는 HTTP 연결만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-155">Hybrid Connections require only outbound TCP or HTTP connectivity from your private network.</span></span> <span data-ttu-id="2d18b-156">Tooopen 모든 방화벽 포트가 필요 또는 네트워크에 네트워크 경계 구성 tooallow 프로그램 모든 인바운드 연결을 변경 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-156">You do not need tooopen any firewall ports or change your network perimeter configuration tooallow any inbound connectivity into your network.</span></span>

<span data-ttu-id="2d18b-157">하이브리드 연결에서 TCP 포트를 수행 하는 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-157">hello following TCP ports are used by Hybrid Connections:</span></span>

| <span data-ttu-id="2d18b-158">포트</span><span class="sxs-lookup"><span data-stu-id="2d18b-158">Port</span></span> | <span data-ttu-id="2d18b-159">필요한 이유</span><span class="sxs-lookup"><span data-stu-id="2d18b-159">Why you need it</span></span> |
| --- | --- |
| <span data-ttu-id="2d18b-160">9350 - 9354</span><span class="sxs-lookup"><span data-stu-id="2d18b-160">9350 - 9354</span></span> |<span data-ttu-id="2d18b-161">이러한 포트는 데이터 전송에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-161">These ports are used for data transmission.</span></span> <span data-ttu-id="2d18b-162">서비스 버스 릴레이 관리자 hello TCP 연결을 사용할 수 있는 경우 포트 9350 toodetermine를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-162">hello Service Bus relay manager probes port 9350 toodetermine if TCP connectivity is available.</span></span> <span data-ttu-id="2d18b-163">사용 가능한 경우 포트 9352도 사용 가능한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-163">If it is available, then it assumes that port 9352 is also available.</span></span> <span data-ttu-id="2d18b-164">데이터 트래픽이 포트 9352를 통해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-164">Data traffic goes over port 9352.</span></span> <br/><br/><span data-ttu-id="2d18b-165">아웃 바운드 연결 toothese 포트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-165">Allow outbound connections toothese ports.</span></span> |
| <span data-ttu-id="2d18b-166">5671</span><span class="sxs-lookup"><span data-stu-id="2d18b-166">5671</span></span> |<span data-ttu-id="2d18b-167">포트가 9352 데이터 트래픽에 사용 하는 경우 포트 5671 hello 컨트롤 채널으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-167">When port 9352 is used for data traffic, port 5671 is used as hello control channel.</span></span> <br/><br/><span data-ttu-id="2d18b-168">Toothis 포트 아웃 바운드 연결을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-168">Allow outbound connections toothis port.</span></span> |
| <span data-ttu-id="2d18b-169">80, 443</span><span class="sxs-lookup"><span data-stu-id="2d18b-169">80, 443</span></span> |<span data-ttu-id="2d18b-170">이러한 포트는 일부 데이터 요청 tooAzure에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-170">These ports are used for some data requests tooAzure.</span></span> <span data-ttu-id="2d18b-171">또한 9352 및 5671 포트를 사용할 수 없는 경우, *다음* 포트 80 및 443 포트가 hello 대체 hello 컨트롤 채널 및 데이터 전송에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-171">Also, if ports 9352 and 5671 are not usable, *then* ports 80 and 443 are hello fallback ports used for data transmission and hello control channel.</span></span><br/><br/><span data-ttu-id="2d18b-172">아웃 바운드 연결 toothese 포트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-172">Allow outbound connections toothese ports.</span></span> <br/><br/><span data-ttu-id="2d18b-173">**참고** 없으면 hello 대신 대체 포트를 다른 TCP 포트 hello으로 toouse 이러한 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-173">**Note** It is not recommended toouse these as hello fallback ports in place of hello other TCP ports.</span></span> <span data-ttu-id="2d18b-174">HTTP/WebSocket hello 데이터 채널에 대 한 기본 TCP 대신 hello 프로토콜로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-174">hello HTTP/WebSocket is used as hello protocol instead of native TCP for data channels.</span></span> <span data-ttu-id="2d18b-175">성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d18b-175">It could result in lower performance.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2d18b-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d18b-176">Next steps</span></span>
[<span data-ttu-id="2d18b-177">Create and manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="2d18b-177">Create and manage Hybrid Connections</span></span>](integration-hybrid-connection-create-manage.md)<br/><span data-ttu-id="2d18b-178">
[Azure 웹 앱 tooan 연결 온-프레미스 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2d18b-178">
[Connect Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md)</span></span><br/><span data-ttu-id="2d18b-179">
[Azure 웹 앱에서 tooon 온-프레미스 SQL Server 연결](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)</span><span class="sxs-lookup"><span data-stu-id="2d18b-179">
[Connect tooon-premises SQL Server from an Azure web app](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)</span></span><br/>

## <a name="see-also"></a><span data-ttu-id="2d18b-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2d18b-180">See Also</span></span>
<span data-ttu-id="2d18b-181">[Microsoft Azure의 BizTalk Services를 관리하기 위한 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: 버전 차트](biztalk-editions-feature-chart.md)</span><span class="sxs-lookup"><span data-stu-id="2d18b-181">[REST API for Managing BizTalk Services on Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md)</span></span><br/><span data-ttu-id="2d18b-182">
[Azure Portal을 사용하여 BizTalk Service 만들기](biztalk-provision-services.md)</span><span class="sxs-lookup"><span data-stu-id="2d18b-182">
[Create a BizTalk Service using Azure portal](biztalk-provision-services.md)</span></span><br/><span data-ttu-id="2d18b-183">
[BizTalk Services: 대시보드, 모니터링 및 크기 조정 탭](biztalk-dashboard-monitor-scale-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="2d18b-183">
[BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md)</span></span><br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
