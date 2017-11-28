---
title: "aaaOn 온-프레미스 데이터 게이트웨이 | Microsoft Docs"
description: "온-프레미스 게이트웨이 Azure에서 Analysis Services 서버는 tooon 온-프레미스 데이터 원본에 연결할 경우에 필요 합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="688d0-103">Azure 온-프레미스 데이터 게이트웨이 사용 하 여 tooon 온-프레미스 데이터 원본 연결</span><span class="sxs-lookup"><span data-stu-id="688d0-103">Connecting tooon-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="688d0-104">hello 온-프레미스 데이터 게이트웨이 온-프레미스 데이터 원본 및 hello 클라우드에서 Azure Analysis Services 서버 간에 안전한 데이터 전송을 제공 하는 브리지 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-104">hello on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in hello cloud.</span></span> <span data-ttu-id="688d0-105">또한 tooworking hello에 여러 Azure Analysis Services 서버와 동일한 지역, 최신 버전의 hello 게이트웨이 hello Azure 논리 앱, Power BI, 전원 응용 프로그램, Microsoft Flow와 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-105">In addition tooworking with multiple Azure Analysis Services servers in hello same region, hello latest version of hello gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="688d0-106">Hello에 여러 서비스에 연결할 수 있습니다 단일 게이트웨이 사용 하 여 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-106">You can associate multiple services in hello same region with a single gateway.</span></span> 

 <span data-ttu-id="688d0-107">Azure Analysis Services를 사용 하려면 hello에 게이트웨이 리소스가 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-107">Azure Analysis Services requires a gateway resource in hello same region.</span></span> <span data-ttu-id="688d0-108">예를 들어 Azure Analysis Services 서버 hello 2 미국 동부 지역에 있으면 게이트웨이 리소스가 hello 미국 동부 2 지역에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-108">For example, if you have Azure Analysis Services servers in hello East US 2 region, you need a gateway resource in hello East US 2 region.</span></span> <span data-ttu-id="688d0-109">미국 동부 2에서에서 여러 서버 hello를 사용 하 여 동일한 게이트웨이에 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-109">Multiple servers in East US 2 can use hello same gateway.</span></span>

<span data-ttu-id="688d0-110">Hello 게이트웨이 hello 사용 하 여 설치를 처음으로 가져오기는 네 부분으로 이루어진 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-110">Getting setup with hello gateway hello first time is a four-part process:</span></span>

- <span data-ttu-id="688d0-111">**설치 프로그램 다운로드 및 실행** - 이 단계는 조직의 컴퓨터에 게이트웨이 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="688d0-112">**게이트웨이 등록** -이 단계는 이름 지정 및 복구, 게이트웨이 키 hello 게이트웨이 클라우드 서비스에 게이트웨이 등록 하는 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with hello Gateway Cloud Service.</span></span>

- <span data-ttu-id="688d0-113">**Azure에서 게이트웨이 리소스 만들기** - 이 단계에서는 Azure 구독에서 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="688d0-114">**서버 tooyour 게이트웨이 리소스를 연결** -게이트웨이 리소스를 구독에 있으면 서버 tooit 연결을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-114">**Connect your servers tooyour gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers tooit.</span></span>

<span data-ttu-id="688d0-115">구독에 대해 구성 된 게이트웨이 리소스를 만든 후에 다른 서비스 tooit 및 여러 서버를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services tooit.</span></span> <span data-ttu-id="688d0-116">만 tooinstall 다른 게이트웨이 필요 하 고 서버 또는 다른 서비스를 다른 지역에 있는 경우 추가 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-116">You only need tooinstall a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="688d0-117">지금 바로 시작 tooget 참조 [설치 하 고 온-프레미스 데이터 게이트웨이 구성](analysis-services-gateway-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-117">tooget started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="688d0-118"><a name="how-it-works"> </a>작동 방법</span><span class="sxs-lookup"><span data-stu-id="688d0-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="688d0-119">조직에서 컴퓨터에 설치 하는 hello 게이트웨이 Windows 서비스로 실행 **온-프레미스 데이터 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-119">hello gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="688d0-120">이 로컬 서비스는 hello Azure 서비스 버스를 통해 게이트웨이 클라우드 서비스에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-120">This local service is registered with hello Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="688d0-121">그런 다음 Azure 구독에 대한 게이트웨이 리소스 게이트웨이 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="688d0-122">Azure Analysis Services 서버는 다음 tooyour 게이트웨이 리소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-122">Your Azure Analysis Services servers are then connected tooyour gateway resource.</span></span> <span data-ttu-id="688d0-123">때 서버 필요 tooconnect tooyour 프로그램에 대 한 모델 온-프레미스 데이터 원본 쿼리 또는 처리를 위해, 로컬 온-프레미스 데이터 게이트웨이 서비스 및 데이터 원본 쿼리 및 데이터 흐름 트래버스하여 hello 게이트웨이 리소스에 Azure 서비스 버스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-123">When models on your server need tooconnect tooyour on-premises data sources for queries or processing, a query and data flow traverses hello gateway resource, Azure Service Bus, hello local on-premises data gateway service, and your data sources.</span></span> 

![작동 방법](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="688d0-125">쿼리 및 데이터 흐름:</span><span class="sxs-lookup"><span data-stu-id="688d0-125">Queries and data flow:</span></span>

1. <span data-ttu-id="688d0-126">쿼리는 hello 온-프레미스 데이터 원본에 대 한 hello 암호화 된 자격 증명으로 hello 클라우드 서비스에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-126">A query is created by hello cloud service with hello encrypted credentials for hello on-premises data source.</span></span> <span data-ttu-id="688d0-127">그런 다음 게이트웨이 tooprocess hello에 대 한 큐를 tooa 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-127">It's then sent tooa queue for hello gateway tooprocess.</span></span>
2. <span data-ttu-id="688d0-128">hello 게이트웨이 클라우드 서비스 hello 쿼리를 분석 하 고 hello 요청 toohello 푸시 [Azure 서비스 버스](https://azure.microsoft.com/documentation/services/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-128">hello gateway cloud service analyzes hello query and pushes hello request toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="688d0-129">hello 온-프레미스 데이터 게이트웨이 보류 중인 요청 hello에 대 한 Azure 서비스 버스를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-129">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="688d0-130">hello 쿼리 가져오고 hello 자격 증명의 암호를 해독 toohello 데이터 원본 자격 증명으로 연결 하는 hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-130">hello gateway gets hello query, decrypts hello credentials, and connects toohello data sources with those credentials.</span></span>
5. <span data-ttu-id="688d0-131">hello 게이트웨이 hello 쿼리 toohello 실행할 데이터 소스에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-131">hello gateway sends hello query toohello data source for execution.</span></span>
6. <span data-ttu-id="688d0-132">뒤로 toohello 게이트웨이 hello 데이터 원본의 그리고 hello 클라우드 서비스와 서버 hello 결과 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-132">hello results are sent from hello data source, back toohello gateway, and then onto hello cloud service and your server.</span></span>

## <span data-ttu-id="688d0-133"><a name="windows-service-account"> </a>Windows 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="688d0-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="688d0-134">hello 온-프레미스 데이터 게이트웨이 구성 된 toouse *NT SERVICE\PBIEgwService* hello Windows 서비스 로그온 자격 증명에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-134">hello on-premises data gateway is configured toouse *NT SERVICE\PBIEgwService* for hello Windows service logon credential.</span></span> <span data-ttu-id="688d0-135">기본적으로 서비스로; hello 로그온의 오른쪽에 hello의 컨텍스트에서 hello 게이트웨이 설치 하는 hello 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-135">By default, it has hello right of Logon as a service; in hello context of hello machine that you are installing hello gateway on.</span></span> <span data-ttu-id="688d0-136">이 자격 증명은 동일한 계정 사용 tooconnect tooon 온-프레미스 데이터 원본 또는 Azure 계정에 하지 안녕 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-136">This credential is not hello same account used tooconnect tooon-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="688d0-137">인해 프록시 서버와 함께 문제가 발생 한 경우 tooauthentication, 좋습니다 toochange hello Windows 서비스 계정 tooa 도메인 사용자 또는 관리 되는 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="688d0-137">If you encounter issues with your proxy server due tooauthentication, you may want toochange hello Windows service account tooa domain user or managed service account.</span></span>

## <span data-ttu-id="688d0-138"><a name="ports"> </a>포트</span><span class="sxs-lookup"><span data-stu-id="688d0-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="688d0-139">hello 게이트웨이 아웃 바운드 연결 tooAzure 서비스 버스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-139">hello gateway creates an outbound connection tooAzure Service Bus.</span></span> <span data-ttu-id="688d0-140">아웃바운드 포트 TCP 443(기본값), 5671, 5672, 9350-9354에서 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="688d0-141">hello 게이트웨이 인바운드 포트가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-141">hello gateway does not require inbound ports.</span></span>

<span data-ttu-id="688d0-142">방화벽의 프로그램 데이터 영역에 대 한 hello IP 주소를 화이트 리스트 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-142">We recommend you whitelist hello IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="688d0-143">Hello를 다운로드할 수 있습니다 [Microsoft Azure 데이터 센터 IP 목록](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-143">You can download hello [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="688d0-144">이 목록은 매주 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="688d0-145">hello Azure 데이터 센터 IP 목록에 나열 된 hello IP 주소는 CIDR 표기법 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-145">hello IP Addresses listed in hello Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="688d0-146">예를 들어, 10.0.0.0/24는 10.0.0.0-10.0.0.24를 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="688d0-147">Hello에 대 한 자세한 [CIDR 표기법](http://whatismyipaddress.com/cidr)합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-147">Learn more about hello [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="688d0-148">hello 다음은 hello 게이트웨이에서 사용 되는 hello 정규화 된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-148">hello following are hello fully qualified domain names used by hello gateway.</span></span>

| <span data-ttu-id="688d0-149">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="688d0-149">Domain names</span></span> | <span data-ttu-id="688d0-150">아웃바운드 포트</span><span class="sxs-lookup"><span data-stu-id="688d0-150">Outbound ports</span></span> | <span data-ttu-id="688d0-151">설명</span><span class="sxs-lookup"><span data-stu-id="688d0-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="688d0-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="688d0-152">*.powerbi.com</span></span> |<span data-ttu-id="688d0-153">80</span><span class="sxs-lookup"><span data-stu-id="688d0-153">80</span></span> |<span data-ttu-id="688d0-154">HTTP은 toodownload hello 설치 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-154">HTTP used toodownload hello installer.</span></span> |
| <span data-ttu-id="688d0-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="688d0-155">*.powerbi.com</span></span> |<span data-ttu-id="688d0-156">443</span><span class="sxs-lookup"><span data-stu-id="688d0-156">443</span></span> |<span data-ttu-id="688d0-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="688d0-157">HTTPS</span></span> |
| <span data-ttu-id="688d0-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="688d0-158">*.analysis.windows.net</span></span> |<span data-ttu-id="688d0-159">443</span><span class="sxs-lookup"><span data-stu-id="688d0-159">443</span></span> |<span data-ttu-id="688d0-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="688d0-160">HTTPS</span></span> |
| <span data-ttu-id="688d0-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="688d0-161">*.login.windows.net</span></span> |<span data-ttu-id="688d0-162">443</span><span class="sxs-lookup"><span data-stu-id="688d0-162">443</span></span> |<span data-ttu-id="688d0-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="688d0-163">HTTPS</span></span> |
| <span data-ttu-id="688d0-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="688d0-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="688d0-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="688d0-165">5671-5672</span></span> |<span data-ttu-id="688d0-166">AMQP(고급 메시지 큐 프로토콜)</span><span class="sxs-lookup"><span data-stu-id="688d0-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="688d0-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="688d0-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="688d0-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="688d0-168">443, 9350-9354</span></span> |<span data-ttu-id="688d0-169">TCP의 서비스 버스 릴레이에 대한 수신기(액세스 제어 토큰 획득에 443 필요)</span><span class="sxs-lookup"><span data-stu-id="688d0-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="688d0-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="688d0-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="688d0-171">443</span><span class="sxs-lookup"><span data-stu-id="688d0-171">443</span></span> |<span data-ttu-id="688d0-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="688d0-172">HTTPS</span></span> |
| <span data-ttu-id="688d0-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="688d0-173">*.core.windows.net</span></span> |<span data-ttu-id="688d0-174">443</span><span class="sxs-lookup"><span data-stu-id="688d0-174">443</span></span> |<span data-ttu-id="688d0-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="688d0-175">HTTPS</span></span> |
| <span data-ttu-id="688d0-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="688d0-176">login.microsoftonline.com</span></span> |<span data-ttu-id="688d0-177">443</span><span class="sxs-lookup"><span data-stu-id="688d0-177">443</span></span> |<span data-ttu-id="688d0-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="688d0-178">HTTPS</span></span> |
| <span data-ttu-id="688d0-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="688d0-179">*.msftncsi.com</span></span> |<span data-ttu-id="688d0-180">443</span><span class="sxs-lookup"><span data-stu-id="688d0-180">443</span></span> |<span data-ttu-id="688d0-181">Hello 게이트웨이 hello Power BI 서비스에서 연결할 수 없는 경우 tootest 인터넷 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-181">Used tootest internet connectivity if hello gateway is unreachable by hello Power BI service.</span></span> |
| <span data-ttu-id="688d0-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="688d0-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="688d0-183">443</span><span class="sxs-lookup"><span data-stu-id="688d0-183">443</span></span> |<span data-ttu-id="688d0-184">구성에 따라 인증에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="688d0-185"><a name="force-https"></a>Azure Service Bus와의 HTTPS 통신 강제 적용</span><span class="sxs-lookup"><span data-stu-id="688d0-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="688d0-186">직접 TCP; 대신 HTTPS를 사용 하 여 Azure 서비스 버스 게이트웨이 toocommunicate hello를 강제할 수 있습니다. 그러나 이렇게 하면 지금 크게 줄일 수 있습니다 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-186">You can force hello gateway toocommunicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="688d0-187">Hello를 수정할 수 있습니다 *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* hello 값을 변경 하 여 파일 `AutoDetect` 너무`Https`합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-187">You can modify hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing hello value from `AutoDetect` too`Https`.</span></span> <span data-ttu-id="688d0-188">이 파일은 기본적으로 *C:\Program Files\On-premises data gateway*에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="688d0-189"><a name="faq"></a>질문과 대답</span><span class="sxs-lookup"><span data-stu-id="688d0-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="688d0-190">일반</span><span class="sxs-lookup"><span data-stu-id="688d0-190">General</span></span>

<span data-ttu-id="688d0-191">**Q:**: Azure SQL 데이터베이스 같은 hello 클라우드에서의 데이터 원본에는 게이트웨이 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="688d0-191">**Q**: Do I need a gateway for data sources in hello cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="688d0-192">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="688d0-192">
**A**: No.</span></span> <span data-ttu-id="688d0-193">게이트웨이는 tooon 온-프레미스 데이터 원본만 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-193">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="688d0-194">**Q:**: hello 게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 설치 되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-194">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="688d0-195">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="688d0-195">
**A**: No.</span></span> <span data-ttu-id="688d0-196">hello 게이트웨이 제공 된 hello 연결 정보를 사용 하 여 toohello 데이터 소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-196">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="688d0-197">이런이 의미에서 클라이언트 응용 프로그램으로 hello 게이트웨이 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-197">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="688d0-198">hello 게이트웨이 하기만 hello 기능 tooconnect toohello 서버 이름을 제공 된, 일반적으로 hello에 동일한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-198">hello gateway just needs hello capability tooconnect toohello server name that was provided, typically on hello same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="688d0-199">**Q:**: 이유 toouse 작업 필요 하거나 하에서 계정 toosign 학교?</span><span class="sxs-lookup"><span data-stu-id="688d0-199">**Q**: Why do I need toouse a work or school account toosign in?</span></span> <br/><span data-ttu-id="688d0-200">
**A**: Azure 작업을 사용 하 여 또는 학교 계정을 hello 온-프레미스 데이터 게이트웨이 설치할 때만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-200">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="688d0-201">로그인 계정은 Azure AD(Azure Active Directory)에서 관리하는 테넌트에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="688d0-202">일반적으로 Azure AD 계정의 사용자 계정 이름 (UPN)는 hello 전자 메일 주소와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-202">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="688d0-203">**Q**: 자격 증명은 어디에 저장되나요?</span><span class="sxs-lookup"><span data-stu-id="688d0-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="688d0-204">
**A**: hello 입력 한 자격 증명이 데이터 원본에 대 한 암호화 및 hello 게이트웨이 클라우드 서비스에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-204">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello Gateway Cloud Service.</span></span> <span data-ttu-id="688d0-205">hello 온-프레미스 데이터 게이트웨이에 hello 자격 증명의 암호가 해독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-205">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="688d0-206">**Q**: 네트워크 대역폭에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="688d0-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="688d0-207">
**A**: 네트워크 연결의 처리량이 높은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="688d0-208">모든 환경은 다름와 전송 중인 데이터 양을 hello hello 결과 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-208">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="688d0-209">ExpressRoute를 사용 하 여 온-프레미스 및 hello Azure 데이터 센터 간 처리량의 수준을 tooguarantee를 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-209">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="688d0-210">처리량 hello 타사 도구 Azure 속도 테스트 앱 toohelp 계기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-210">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="688d0-211">**Q:**: hello 게이트웨이에서 실행 중인 쿼리 tooa 데이터 원본에 대 한 hello 대기 시간 이란?</span><span class="sxs-lookup"><span data-stu-id="688d0-211">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="688d0-212">Hello 최상의 아키텍처는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-212">What is hello best architecture?</span></span> <br/><span data-ttu-id="688d0-213">
**A**: tooreduce 네트워크 대기 시간, 가능한 데이터 원본 닫기 toohello로 hello 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-213">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="688d0-214">Hello 실제 데이터 원본에 hello 게이트웨이 설치할 수 있습니다,이 근접 단어는 발생 하는 hello 대기 시간을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-214">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="688d0-215">너무 hello 데이터 센터를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-215">Consider hello datacenters too.</span></span> <span data-ttu-id="688d0-216">예를 들어 해당 서비스는 hello 미국 서 부 데이터 센터를 사용 하는 경우 Azure VM에서 호스팅되는 SQL Server 있으면 Azure VM에에서 있어야 hello West US 너무 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-216">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="688d0-217">이 근접 대기 시간을 최소화 하 고 hello Azure VM에서 송신 요금을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-217">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="688d0-218">**Q:**: 보낸 결과 백 toohello 클라우드 인가요?</span><span class="sxs-lookup"><span data-stu-id="688d0-218">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="688d0-219">
**A**: 결과 hello Azure 서비스 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-219">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="688d0-220">**Q:**: hello 클라우드에서 한 인바운드 연결 toohello 게이트웨이가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-220">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="688d0-221">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="688d0-221">
**A**: No.</span></span> <span data-ttu-id="688d0-222">hello 게이트웨이 아웃 바운드 연결 tooAzure 서비스 버스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-222">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="688d0-223">**Q**: 아웃바운드 연결을 차단하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="688d0-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="688d0-224">수행할 작업 tooopen 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-224">What do I need tooopen?</span></span> <br/><span data-ttu-id="688d0-225">
**A**: hello 포트 및 호스트 게이트웨이 사용 하 여 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="688d0-225">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="688d0-226">**Q:**: hello 실제 Windows 서비스 섞어?</span><span class="sxs-lookup"><span data-stu-id="688d0-226">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="688d0-227">
**A**: 서비스에서 hello 게이트웨이 온-프레미스 데이터 게이트웨이 서비스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-227">
**A**: In Services, hello gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="688d0-228">**Q:**: Azure Active Directory 계정으로 실행 하는 게이트웨이 Windows 서비스 hello 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-228">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="688d0-229">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="688d0-229">
**A**: No.</span></span> <span data-ttu-id="688d0-230">hello Windows 서비스에는 유효한 Windows 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-230">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="688d0-231">기본적으로 hello 서비스는 NT SERVICE\PBIEgwService hello 서비스 SID로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-231">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="688d0-232"><a name="high-availability"></a>고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="688d0-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="688d0-233">**Q**: 재해 복구를 위해 어떤 옵션을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="688d0-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="688d0-234">
**A**: hello 복구 키 toorestore 사용 하거나 게이트웨이 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-234">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="688d0-235">Hello 게이트웨이 설치할 때 hello 복구 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-235">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="688d0-236">**Q:**: hello 복구 키의 hello 이점은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-236">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="688d0-237">
**A**: hello 복구 키 방식으로 toomigrate 제공 하거나 재해가 발생 한 후 게이트웨이 설정을 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-237">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="688d0-238"><a name="troubleshooting"> </a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="688d0-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="688d0-239">**Q:**: 어떻게 하는 쿼리를 보내는 toohello 온-프레미스 데이터 원본을 볼 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-239">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="688d0-240">
**A**: hello 전송 된 쿼리를 포함 하는 쿼리 추적을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-240">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="688d0-241">Toochange 쿼리 문제 해결를 수행할 때 toohello 원래 값을 추적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-241">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="688d0-242">쿼리 추적 기능을 그대로 두면 큰 로그가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="688d0-243">또한 추적 쿼리를 위해 데이터 원본이 포함하는 도구를 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="688d0-244">예를 들어 SQL Server 및 Analysis Services의 경우 확장 이벤트 또는 SQL 프로파일러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="688d0-245">**Q:**: hello 게이트웨이 로그는 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="688d0-245">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="688d0-246">
**A**: 이 항목 뒷부분에 나오는 로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="688d0-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="688d0-247"><a name="update"></a>Toohello 최신 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-247"><a name="update"></a>Update toohello latest version</span></span>

<span data-ttu-id="688d0-248">Hello 게이트웨이 버전이 오래 되 면 많은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-248">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="688d0-249">좋은 일반 사례로 hello 최신 버전을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-249">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="688d0-250">한 달 이상 hello 게이트웨이 업데이트 하지 않은 경우 hello 최신 버전의 hello 게이트웨이 설치 하는 것이 좋습니다. 수도 있으며 hello 문제를 재현할 수 있는지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-250">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="688d0-251">오류: tooadd 사용자 toogroup을 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-251">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="688d0-252">(-2147463168 PBIEgwService 성능 로그 사용자)</span><span class="sxs-lookup"><span data-stu-id="688d0-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="688d0-253">지원 되지 않는 도메인 컨트롤러에 tooinstall hello 게이트웨이 시도 하면이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-253">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="688d0-254">도메인 컨트롤러가 아닌 컴퓨터에 hello 게이트웨이 배포 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-254">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="688d0-255"><a name="logs"></a>로그</span><span class="sxs-lookup"><span data-stu-id="688d0-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="688d0-256">로그 파일은 문제를 해결할 때 중요한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="688d0-257">엔터프라이즈 게이트웨이 서비스 로그</span><span class="sxs-lookup"><span data-stu-id="688d0-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="688d0-258">구성 로그</span><span class="sxs-lookup"><span data-stu-id="688d0-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="688d0-259">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="688d0-259">Event logs</span></span>

<span data-ttu-id="688d0-260">데이터 관리 게이트웨이 및 PowerBIGateway 로그 hello를 찾을 수 있습니다 **응용 프로그램 및 서비스 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-260">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="688d0-261"><a name="telemetry"></a>원격 분석</span><span class="sxs-lookup"><span data-stu-id="688d0-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="688d0-262">원격 분석은 모니터링 및 문제 해결에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="688d0-263">기본적으로</span><span class="sxs-lookup"><span data-stu-id="688d0-263">By default</span></span>

<span data-ttu-id="688d0-264">**원격 분석 tooturn**</span><span class="sxs-lookup"><span data-stu-id="688d0-264">**tooturn on telemetry**</span></span>

1.  <span data-ttu-id="688d0-265">Hello 온-프레미스 데이터 게이트웨이 클라이언트 컴퓨터의 디렉터리에 hello 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-265">Check hello On-premises data gateway client directory on hello computer.</span></span> <span data-ttu-id="688d0-266">일반적으로 **%systemdrive%\Program Files\On-premises data gateway**입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="688d0-267">또는 서비스 콘솔을 열고 hello 경로 tooexecutable를 확인할 수 있습니다: hello 온-프레미스 데이터 게이트웨이 서비스의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-267">Or, you can open a Services console and check hello Path tooexecutable: A property of hello On-premises data gateway service.</span></span>
2.  <span data-ttu-id="688d0-268">클라이언트 디렉터리에서 hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-268">In hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="688d0-269">Hello SendTelemetry 설정 tootrue를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-269">Change hello SendTelemetry setting tootrue.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="688d0-270">변경 내용을 저장 하 고 hello Windows 서비스를 다시 시작: 온-프레미스 데이터 게이트웨이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="688d0-270">Save your changes and restart hello Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="688d0-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="688d0-271">Next steps</span></span>
* [<span data-ttu-id="688d0-272">Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="688d0-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="688d0-273">Azure Analysis Services에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="688d0-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
