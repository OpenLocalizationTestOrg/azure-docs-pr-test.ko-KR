---
title: "온-프레미스 데이터 게이트웨이 | Microsoft Docs"
description: "Azure의 Analysis Services 서버가 온-프레미스 데이터 원본에 연결되는 경우 온-프레미스 게이트웨이가 필요합니다."
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
ms.openlocfilehash: 514b5404e8cbfa0baa657eb41736e20cad502638
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connecting-to-on-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="e2e0f-103">Azure 온-프레미스 데이터 게이트웨이를 사용하여 온-프레미스 데이터 원본에 연결</span><span class="sxs-lookup"><span data-stu-id="e2e0f-103">Connecting to on-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="e2e0f-104">온-프레미스 데이터 게이트웨이는 클라우드에서 온-프레미스 데이터 원본과 Azure Analysis Services 서버 간의 보안 데이터 전송을 제공하여 둘을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in the cloud.</span></span> <span data-ttu-id="e2e0f-105">동일한 지역에서 여러 Azure Analysis Services 서버를 사용하는 것 외에도 최신 버전의 게이트웨이는 Azure Logic Apps, Power BI, Power Apps, Microsoft Flow와도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-105">In addition to working with multiple Azure Analysis Services servers in the same region, the latest version of the gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="e2e0f-106">단일 게이트웨이 통해 동일한 지역에서 여러 서비스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-106">You can associate multiple services in the same region with a single gateway.</span></span> 

 <span data-ttu-id="e2e0f-107">Azure Analysis Services는 동일한 지역에서 게이트웨이 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-107">Azure Analysis Services requires a gateway resource in the same region.</span></span> <span data-ttu-id="e2e0f-108">예를 들어 Azure Analysis Services 서버가 미국 동부 2 지역에 있으면 미국 동부 2 지역에서 게이트웨이 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-108">For example, if you have Azure Analysis Services servers in the East US 2 region, you need a gateway resource in the East US 2 region.</span></span> <span data-ttu-id="e2e0f-109">미국 동부 2의 여러 서버에서 동일한 게이트웨이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-109">Multiple servers in East US 2 can use the same gateway.</span></span>

<span data-ttu-id="e2e0f-110">처음으로 게이트웨이 설치하기는 네 부분으로 이루어진 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-110">Getting setup with the gateway the first time is a four-part process:</span></span>

- <span data-ttu-id="e2e0f-111">**설치 프로그램 다운로드 및 실행** - 이 단계는 조직의 컴퓨터에 게이트웨이 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="e2e0f-112">**게이트웨이 등록** - 이 단계에서는 게이트웨이에 대한 이름 및 복구 키를 지정하고 게이트웨이 클라우드 서비스로 게이트웨이를 등록한 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with the Gateway Cloud Service.</span></span>

- <span data-ttu-id="e2e0f-113">**Azure에서 게이트웨이 리소스 만들기** - 이 단계에서는 Azure 구독에서 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="e2e0f-114">**게이트웨이 리소스에 서버 연결** - 구독에 게이트웨이 리소스가 있으면 서버 연결을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-114">**Connect your servers to your gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers to it.</span></span>

<span data-ttu-id="e2e0f-115">구독에 대해 구성된 게이트웨이 리소스가 있으면 여러 서버를 연결하고 이를 기타 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services to it.</span></span> <span data-ttu-id="e2e0f-116">다른 지역에 서버 또는 다른 서비스가 있는 경우 다른 게이트웨이를 설치하고 추가 게이트웨이 리소스를 만들기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-116">You only need to install a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="e2e0f-117">지금 바로 시작하려면 [온-프레미스 데이터 게이트웨이 설치 및 구성](analysis-services-gateway-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-117">To get started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="e2e0f-118"><a name="how-it-works"> </a>작동 방법</span><span class="sxs-lookup"><span data-stu-id="e2e0f-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="e2e0f-119">조직의 컴퓨터에 설치하는 게이트웨이는 Windows 서비스인 **온-프레미스 데이터 게이트웨이**로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-119">The gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="e2e0f-120">이 로컬 서비스는 Azure Service Bus를 통해 게이트웨이 클라우드 서비스로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-120">This local service is registered with the Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="e2e0f-121">그런 다음 Azure 구독에 대한 게이트웨이 리소스 게이트웨이 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="e2e0f-122">그러면 Azure Analysis Services 서버는 게이트웨이 리소스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-122">Your Azure Analysis Services servers are then connected to your gateway resource.</span></span> <span data-ttu-id="e2e0f-123">서버의 모델을 쿼리 또는 처리를 위해 온-프레미스 데이터 원본에 연결해야 하는 경우 쿼리 및 데이터 흐름은 게이트웨이 리소스, Azure Service Bus, 로컬 온-프레미스 데이터 게이트웨이 서비스 및 데이터 원본을 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-123">When models on your server need to connect to your on-premises data sources for queries or processing, a query and data flow traverses the gateway resource, Azure Service Bus, the local on-premises data gateway service, and your data sources.</span></span> 

![작동 방법](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="e2e0f-125">쿼리 및 데이터 흐름:</span><span class="sxs-lookup"><span data-stu-id="e2e0f-125">Queries and data flow:</span></span>

1. <span data-ttu-id="e2e0f-126">쿼리는 온-프레미스 데이터 원본의 암호화된 자격 증명을 사용하여 클라우드 서비스에서 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-126">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="e2e0f-127">그런 다음 처리할 게이트웨이의 큐로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-127">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="e2e0f-128">게이트웨이 클라우드 서비스에서 쿼리를 분석하고 [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/)에 대한 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-128">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="e2e0f-129">온-프레미스 데이터 게이트웨이가 보류 중인 요청을 위해 Azure 서비스 버스를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-129">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="e2e0f-130">게이트웨이가 쿼리를 가져오고, 자격 증명의 암호를 해독하고, 해당 자격 증명으로 데이터 원본에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-130">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="e2e0f-131">게이트웨이가 실행을 위해 데이터 원본에 쿼리를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-131">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="e2e0f-132">결과가 데이터 원본에서 게이트웨이로 다시 전송된 후 클라우드 서비스 및 서버로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-132">The results are sent from the data source, back to the gateway, and then onto the cloud service and your server.</span></span>

## <span data-ttu-id="e2e0f-133"><a name="windows-service-account"> </a>Windows 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="e2e0f-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="e2e0f-134">온-프레미스 데이터 게이트웨이는 Windows 서비스 로그온 자격 증명에 대해 *NT SERVICE\PBIEgwService*를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-134">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="e2e0f-135">기본적으로 게이트웨이를 설치하는 컴퓨터의 컨텍스트에서 서비스로 로그온할 권리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-135">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="e2e0f-136">이 자격 증명은 온-프레미스 데이터 원본 또는 Azure 계정에 연결하는 데 사용되는 동일한 계정이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-136">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="e2e0f-137">인증으로 인해 프록시 서버와 함께 문제가 발생하는 경우 Windows 서비스 계정을 도메인 사용자 또는 관리되는 서비스 계정으로 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-137">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <span data-ttu-id="e2e0f-138"><a name="ports"> </a>포트</span><span class="sxs-lookup"><span data-stu-id="e2e0f-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="e2e0f-139">게이트웨이는 Azure 서비스 버스에 대한 아웃바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-139">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="e2e0f-140">아웃바운드 포트 TCP 443(기본값), 5671, 5672, 9350-9354에서 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="e2e0f-141">게이트웨이에는 인바운드 포트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-141">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="e2e0f-142">방화벽에서 사용자 데이터 영역에 대한 IP 주소를 허용 목록에 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-142">We recommend you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="e2e0f-143">[Microsoft Azure 데이터 센터 IP 목록](https://www.microsoft.com/download/details.aspx?id=41653)을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-143">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="e2e0f-144">이 목록은 매주 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="e2e0f-145">Azure 데이터 센터 IP 목록에 나열된 IP 주소는 CIDR 표기법으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-145">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="e2e0f-146">예를 들어, 10.0.0.0/24는 10.0.0.0-10.0.0.24를 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="e2e0f-147">[CIDR 표기법](http://whatismyipaddress.com/cidr)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-147">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="e2e0f-148">다음은 게이트웨이에서 사용하는 정규화된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-148">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="e2e0f-149">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="e2e0f-149">Domain names</span></span> | <span data-ttu-id="e2e0f-150">아웃바운드 포트</span><span class="sxs-lookup"><span data-stu-id="e2e0f-150">Outbound ports</span></span> | <span data-ttu-id="e2e0f-151">설명</span><span class="sxs-lookup"><span data-stu-id="e2e0f-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2e0f-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="e2e0f-152">*.powerbi.com</span></span> |<span data-ttu-id="e2e0f-153">80</span><span class="sxs-lookup"><span data-stu-id="e2e0f-153">80</span></span> |<span data-ttu-id="e2e0f-154">설치 프로그램을 다운로드하는 데 사용되는 HTTP입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-154">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="e2e0f-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="e2e0f-155">*.powerbi.com</span></span> |<span data-ttu-id="e2e0f-156">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-156">443</span></span> |<span data-ttu-id="e2e0f-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e2e0f-157">HTTPS</span></span> |
| <span data-ttu-id="e2e0f-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2e0f-158">*.analysis.windows.net</span></span> |<span data-ttu-id="e2e0f-159">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-159">443</span></span> |<span data-ttu-id="e2e0f-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e2e0f-160">HTTPS</span></span> |
| <span data-ttu-id="e2e0f-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2e0f-161">*.login.windows.net</span></span> |<span data-ttu-id="e2e0f-162">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-162">443</span></span> |<span data-ttu-id="e2e0f-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e2e0f-163">HTTPS</span></span> |
| <span data-ttu-id="e2e0f-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2e0f-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="e2e0f-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="e2e0f-165">5671-5672</span></span> |<span data-ttu-id="e2e0f-166">AMQP(고급 메시지 큐 프로토콜)</span><span class="sxs-lookup"><span data-stu-id="e2e0f-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="e2e0f-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2e0f-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="e2e0f-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="e2e0f-168">443, 9350-9354</span></span> |<span data-ttu-id="e2e0f-169">TCP의 서비스 버스 릴레이에 대한 수신기(액세스 제어 토큰 획득에 443 필요)</span><span class="sxs-lookup"><span data-stu-id="e2e0f-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="e2e0f-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="e2e0f-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="e2e0f-171">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-171">443</span></span> |<span data-ttu-id="e2e0f-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e2e0f-172">HTTPS</span></span> |
| <span data-ttu-id="e2e0f-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2e0f-173">*.core.windows.net</span></span> |<span data-ttu-id="e2e0f-174">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-174">443</span></span> |<span data-ttu-id="e2e0f-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e2e0f-175">HTTPS</span></span> |
| <span data-ttu-id="e2e0f-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e2e0f-176">login.microsoftonline.com</span></span> |<span data-ttu-id="e2e0f-177">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-177">443</span></span> |<span data-ttu-id="e2e0f-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e2e0f-178">HTTPS</span></span> |
| <span data-ttu-id="e2e0f-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="e2e0f-179">*.msftncsi.com</span></span> |<span data-ttu-id="e2e0f-180">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-180">443</span></span> |<span data-ttu-id="e2e0f-181">Power BI 서비스에서 게이트웨이에 연결할 수 없는 경우 인터넷 연결을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-181">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="e2e0f-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="e2e0f-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="e2e0f-183">443</span><span class="sxs-lookup"><span data-stu-id="e2e0f-183">443</span></span> |<span data-ttu-id="e2e0f-184">구성에 따라 인증에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="e2e0f-185"><a name="force-https"></a>Azure Service Bus와의 HTTPS 통신 강제 적용</span><span class="sxs-lookup"><span data-stu-id="e2e0f-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="e2e0f-186">직접 TCP 대신 HTTPS를 사용하여 Azure Service Bus와 통신하도록 게이트웨이 강제할 수 있지만 성능이 크게 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-186">You can force the gateway to communicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="e2e0f-187">값을 `AutoDetect`에서 `Https`로 변경하여 *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-187">You can modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="e2e0f-188">이 파일은 기본적으로 *C:\Program Files\On-premises data gateway*에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="e2e0f-189"><a name="faq"></a>질문과 대답</span><span class="sxs-lookup"><span data-stu-id="e2e0f-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="e2e0f-190">일반</span><span class="sxs-lookup"><span data-stu-id="e2e0f-190">General</span></span>

<span data-ttu-id="e2e0f-191">**Q**: Azure SQL Database와 같은 클라우드에서 데이터 원본에 대한 게이트웨이가 필요하나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-191">**Q**: Do I need a gateway for data sources in the cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="e2e0f-192">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-192">
**A**: No.</span></span> <span data-ttu-id="e2e0f-193">게이트웨이는 온-프레미스 데이터 원본에만 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-193">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="e2e0f-194">**Q**: 데이터 원본과 동일한 컴퓨터에 게이트웨이를 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-194">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="e2e0f-195">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-195">
**A**: No.</span></span> <span data-ttu-id="e2e0f-196">게이트웨이는 제공된 연결 정보를 사용하여 데이터 원본에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-196">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="e2e0f-197">이러한 의미에서 게이트웨이를 클라이언트 응용 프로그램이라고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-197">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="e2e0f-198">게이트웨이는 일반적으로 동일한 네트워크에서 제공된 서버 이름에 연결할 수 있는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-198">The gateway just needs the capability to connect to the server name that was provided, typically on the same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="e2e0f-199">**Q:**: 회사 또는 학교 계정을 사용하여 로그인해야 하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-199">**Q**: Why do I need to use a work or school account to sign in?</span></span> <br/><span data-ttu-id="e2e0f-200">
**A**: 온-프레미스 데이터 게이트웨이를 설치할 때만 Azure 회사 또는 학교 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-200">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="e2e0f-201">로그인 계정은 Azure AD(Azure Active Directory)에서 관리하는 테넌트에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e2e0f-202">일반적으로 Azure AD 계정의 UPN(사용자 계정 이름)은 이메일 주소와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-202">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="e2e0f-203">**Q**: 자격 증명은 어디에 저장되나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="e2e0f-204">
**A**: 데이터 원본에 입력한 자격 증명은 게이트웨이 클라우드 서비스에 암호화되어 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-204">
**A**: The credentials that you enter for a data source are encrypted and stored in the Gateway Cloud Service.</span></span> <span data-ttu-id="e2e0f-205">자격 증명은 온-프레미스 데이터 게이트웨이에서 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-205">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="e2e0f-206">**Q**: 네트워크 대역폭에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="e2e0f-207">
**A**: 네트워크 연결의 처리량이 높은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="e2e0f-208">모든 환경은 다르며 전송되는 데이터의 양은 결과에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-208">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="e2e0f-209">ExpressRoute를 사용하면 온-프레미스 및 Azure 데이터 센터 간의 처리량 수준을 보장하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-209">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="e2e0f-210">타사 도구인 Azure Speed Test 앱을 사용하면 처리량을 측정하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-210">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="e2e0f-211">**Q**: 게이트웨이에서 데이터 원본으로의 쿼리를 실행할 때 나타나는 대기 시간은 얼마나 되나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-211">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="e2e0f-212">최선의 아키텍처는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-212">What is the best architecture?</span></span> <br/><span data-ttu-id="e2e0f-213">
**A**: 네트워크 대기 시간을 줄이려면 게이트웨이를 데이터 원본에 최대한 가깝게 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-213">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="e2e0f-214">실제 데이터 원본에 게이트웨이를 설치할 수 있는 경우 이 근접성으로 인해 발생하는 대기 시간이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-214">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="e2e0f-215">데이터 센터도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-215">Consider the datacenters too.</span></span> <span data-ttu-id="e2e0f-216">예를 들어 서비스에서 미국 서부 데이터 센터를 사용하고 Azure VM에서 SQL Server가 호스트되는 경우 Azure VM도 미국 서부에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-216">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="e2e0f-217">이 근접성으로 인해 대기 시간이 최소화되고 Azure VM에서 송신 요금이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-217">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="e2e0f-218">**Q**: 결과가 클라우드로 어떻게 다시 전송되나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-218">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="e2e0f-219">
**A**: Azure Service Bus를 통해 결과가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-219">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="e2e0f-220">**Q**: 클라우드에서 게이트웨이로의 인바운드 연결이 있나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-220">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="e2e0f-221">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-221">
**A**: No.</span></span> <span data-ttu-id="e2e0f-222">게이트웨이는 Azure 서비스 버스에 대해 아웃바운드 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-222">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="e2e0f-223">**Q**: 아웃바운드 연결을 차단하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="e2e0f-224">이러한 연결을 열려면 무엇이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-224">What do I need to open?</span></span> <br/><span data-ttu-id="e2e0f-225">
**A**: 게이트웨이가 사용하는 포트 및 호스트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-225">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="e2e0f-226">**Q**: 실제 Windows 서비스를 어떻게 지칭하나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-226">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="e2e0f-227">
**A**: 서비스에서 게이트웨이를 온-프레미스 게이트웨이 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-227">
**A**: In Services, the gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="e2e0f-228">**Q**: Azure Active Directory 계정으로 게이트웨이 Windows 서비스를 실행할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-228">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="e2e0f-229">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-229">
**A**: No.</span></span> <span data-ttu-id="e2e0f-230">Windows 서비스에는 유효한 Windows 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-230">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="e2e0f-231">기본적으로 서비스는 서비스 SID, NT SERVICE\PBIEgwService를 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-231">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="e2e0f-232"><a name="high-availability"></a>고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="e2e0f-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="e2e0f-233">**Q**: 재해 복구를 위해 어떤 옵션을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="e2e0f-234">
**A**: 복구 키를 사용하여 게이트웨이를 복원하거나 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-234">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="e2e0f-235">게이트웨이를 설치할 때 복구 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-235">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="e2e0f-236">**Q**: 복구 키를 사용할 경우의 이점은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-236">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="e2e0f-237">
**A**: 복구 키는 재해 발생 후 게이트웨이 설정을 마이그레이션하거나 복구할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-237">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="e2e0f-238"><a name="troubleshooting"> </a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="e2e0f-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="e2e0f-239">**Q**: 온-프레미스 데이터 원본으로 어떤 쿼리가 전송되고 있는지를 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-239">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="e2e0f-240">
**A**: 전송 중인 쿼리를 포함하는 쿼리 추적을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-240">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="e2e0f-241">문제 해결이 끝나면 쿼리 추적을 원래 값으로 다시 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-241">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="e2e0f-242">쿼리 추적 기능을 그대로 두면 큰 로그가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="e2e0f-243">또한 추적 쿼리를 위해 데이터 원본이 포함하는 도구를 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="e2e0f-244">예를 들어 SQL Server 및 Analysis Services의 경우 확장 이벤트 또는 SQL 프로파일러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="e2e0f-245">**Q**: 게이트웨이 로그는 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="e2e0f-245">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="e2e0f-246">
**A**: 이 항목 뒷부분에 나오는 로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="e2e0f-247"><a name="update"></a>최신 버전으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="e2e0f-247"><a name="update"></a>Update to the latest version</span></span>

<span data-ttu-id="e2e0f-248">게이트웨이 버전이 오래되면 여러 가지 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-248">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="e2e0f-249">일반적으로는 최신 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-249">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="e2e0f-250">한 달 동안 게이트웨이를 업데이트하지 않은 경우 최신 버전의 게이트웨이를 설치하고 문제가 재현되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-250">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="e2e0f-251">오류: 그룹에 사용자를 추가하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-251">Error: Failed to add user to group.</span></span> <span data-ttu-id="e2e0f-252">(-2147463168 PBIEgwService 성능 로그 사용자)</span><span class="sxs-lookup"><span data-stu-id="e2e0f-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="e2e0f-253">지원되지 않는 도메인 컨트롤러에 게이트웨이 설치하려고 하면 이 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-253">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="e2e0f-254">도메인 컨트롤러가 아닌 컴퓨터에 게이트웨이를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-254">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="e2e0f-255"><a name="logs"></a>로그</span><span class="sxs-lookup"><span data-stu-id="e2e0f-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="e2e0f-256">로그 파일은 문제를 해결할 때 중요한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="e2e0f-257">엔터프라이즈 게이트웨이 서비스 로그</span><span class="sxs-lookup"><span data-stu-id="e2e0f-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="e2e0f-258">구성 로그</span><span class="sxs-lookup"><span data-stu-id="e2e0f-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="e2e0f-259">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="e2e0f-259">Event logs</span></span>

<span data-ttu-id="e2e0f-260">데이터 관리 게이트웨이 및 PowerBIGateway 로그를 **응용 프로그램 및 서비스 로그** 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-260">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="e2e0f-261"><a name="telemetry"></a>원격 분석</span><span class="sxs-lookup"><span data-stu-id="e2e0f-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="e2e0f-262">원격 분석은 모니터링 및 문제 해결에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="e2e0f-263">기본적으로</span><span class="sxs-lookup"><span data-stu-id="e2e0f-263">By default</span></span>

<span data-ttu-id="e2e0f-264">**원격 분석을 켜려면**</span><span class="sxs-lookup"><span data-stu-id="e2e0f-264">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="e2e0f-265">컴퓨터에서 온-프레미스 데이터 게이트웨이 클라이언트 디렉터리를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-265">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="e2e0f-266">일반적으로 **%systemdrive%\Program Files\On-premises data gateway**입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="e2e0f-267">또는 서비스 콘솔을 열고 실행 파일 경로 즉, 온-프레미스 데이터 게이트웨이 서비스의 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-267">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="e2e0f-268">클라이언트 디렉터리의 Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config 파일에서</span><span class="sxs-lookup"><span data-stu-id="e2e0f-268">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="e2e0f-269">SendTelemetry 설정을 true로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-269">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="e2e0f-270">변경 내용을 저장하고 Windows 서비스 온-프레미스 데이터 게이트웨이 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e0f-270">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="e2e0f-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2e0f-271">Next steps</span></span>
* [<span data-ttu-id="e2e0f-272">Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="e2e0f-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="e2e0f-273">Azure Analysis Services에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="e2e0f-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
