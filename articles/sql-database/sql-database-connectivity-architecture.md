---
title: "SQL 데이터베이스 연결 아키텍처 aaaAzure | Microsoft Docs"
description: "이 문서에서는 hello Azure SQLDB 연결 아키텍처에서 Azure 내에서 또는 Azure 외부에서."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="e8b35-103">Azure SQL Database 연결 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e8b35-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="e8b35-104">이 문서는 hello Azure SQL 데이터베이스 연결 아키텍처에 설명 하 고 hello 서로 다른 구성 요소에서 Azure SQL 데이터베이스 인스턴스의 트래픽 tooyour toodirect를 어떻게 작동 하는지 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="e8b35-105">이러한 Azure SQL 데이터베이스 연결 구성 요소는 Azure 내에서 연결 하는 클라이언트와 Azure 외부에서 연결 하는 클라이언트 toodirect 네트워크 트래픽 toohello Azure 데이터베이스를 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="e8b35-106">Hello 고려 사항 관련 toochanging hello 기본 연결 설정 및이 문서는 또한 스크립트 샘플 toochange 연결 발생 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="e8b35-107">이 문서를 읽은 후에 질문이 있는 경우에 dmalik@microsoft.com에서 Dhruv에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e8b35-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="e8b35-108">연결 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e8b35-108">Connectivity architecture</span></span>

<span data-ttu-id="e8b35-109">다음 다이어그램 hello hello Azure SQL 데이터베이스 연결 아키텍처의 대략적인 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![아키텍처 개요](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="e8b35-111">hello 다음과 같은 단계로 진행 방법을 hello Azure SQL 데이터베이스 소프트웨어 부하 분산 장치 (SLB) 및 hello Azure SQL 데이터베이스 게이트웨이 통해 설정 된 tooan Azure SQL 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="e8b35-112">Azure 내에서 또는 Azure 외부의 클라이언트 연결 toohello SLB는 공용 IP 주소를 포함 하 고 포트 1433에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="e8b35-113">SLB hello toohello Azure SQL 데이터베이스 게이트웨이 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="e8b35-114">hello 게이트웨이 hello 트래픽 toohello 올바른 프록시 미들웨어를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="e8b35-115">hello 프록시 미들웨어 hello 트래픽 toohello 적절 한 Azure SQL 데이터베이스를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8b35-116">이러한 각 구성이 요소는 서비스 거부 (DDoS) 서비스 보호 hello 네트워크 및 hello 응용 프로그램 계층에서 기본 제공 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="e8b35-117">Azure 내부에서 연결</span><span class="sxs-lookup"><span data-stu-id="e8b35-117">Connectivity from within Azure</span></span>

<span data-ttu-id="e8b35-118">Azure 내부에서 연결하는 경우 연결에는 기본적으로 **리디렉션** 연결 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="e8b35-119">에 대 한 정책을 **리디렉션** hello TCP 세션이 설정 된 toohello Azure SQL 데이터베이스 후 연결을 hello 클라이언트 세션 임을 의미 다음에서 변경 toohello 대상 가상 IP 사용 하 여 toohello 프록시 미들웨어 리디렉션 hello Azure SQL 데이터베이스 게이트웨이 toothat hello 프록시 미들웨어의입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="e8b35-120">그런 후 모든 후속 패킷이 hello Azure SQL 데이터베이스 게이트웨이 무시 hello 프록시 미들웨어를 통해 직접 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="e8b35-121">다음 다이어그램 hello이 트래픽 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-121">hello following diagram illustrates this traffic flow.</span></span>

![아키텍처 개요](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="e8b35-123">Azure 외부에서 연결</span><span class="sxs-lookup"><span data-stu-id="e8b35-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="e8b35-124">Azure 외부에서 연결하는 경우 연결에는 기본적으로 **프록시** 연결 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="e8b35-125">에 대 한 정책을 **프록시** hello TCP 세션이 hello Azure SQL 데이터베이스 게이트웨이 통해 설정 되 고 모든 후속 패킷이 흐름을 통해 의미 hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="e8b35-126">다음 다이어그램 hello이 트래픽 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-126">hello following diagram illustrates this traffic flow.</span></span>

![아키텍처 개요](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="e8b35-128">Azure SQL Database 게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e8b35-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="e8b35-129">온-프레미스 리소스에서 tooconnect tooan Azure SQL 데이터베이스, Azure 지역에 대 한 tooallow 아웃 바운드 네트워크 트래픽은 toohello Azure SQL 데이터베이스 게이트웨이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="e8b35-130">온-프레미스 리소스에서 연결할 때 hello 기본 설정인 프록시 모드에서는 연결할 때 연결에만 hello 게이트웨이 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="e8b35-131">다음 표에 hello hello 모든 데이터 영역에 대 한 hello Azure SQL 데이터베이스 게이트웨이의 Ip 기본 및 보조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="e8b35-132">일부 지역에는 두 개의 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="e8b35-133">이 영역에 hello 기본 IP 주소는 hello 게이트웨이의 hello 현재 IP 주소가 고 hello 두 번째 IP 주소는 장애 조치 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="e8b35-134">hello 장애 조치 주소는 hello 주소 toowhich tookeep hello 서비스 서버 가용성 높은 이동 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="e8b35-135">이러한 영역에 대 한 허용 아웃 바운드 tooboth hello IP 주소 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="e8b35-136">hello 두 번째 IP 주소에서 수신 하지 않습니다 모든 서비스를 Azure SQL 데이터베이스 tooaccept 연결에 의해 활성화 될 때까지 Microsoft가 소유 하 고 하 고</span><span class="sxs-lookup"><span data-stu-id="e8b35-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="e8b35-137">지역 이름</span><span class="sxs-lookup"><span data-stu-id="e8b35-137">Region Name</span></span> | <span data-ttu-id="e8b35-138">기본 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e8b35-138">Primary IP address</span></span> | <span data-ttu-id="e8b35-139">보조 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e8b35-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="e8b35-140">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="e8b35-140">Australia East</span></span> | <span data-ttu-id="e8b35-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="e8b35-141">191.238.66.109</span></span> | <span data-ttu-id="e8b35-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="e8b35-142">13.75.149.87</span></span> |
| <span data-ttu-id="e8b35-143">오스트레일리아 동남부</span><span class="sxs-lookup"><span data-stu-id="e8b35-143">Australia South East</span></span> | <span data-ttu-id="e8b35-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="e8b35-144">191.239.192.109</span></span> | <span data-ttu-id="e8b35-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="e8b35-145">13.73.109.251</span></span> |
| <span data-ttu-id="e8b35-146">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="e8b35-146">Brazil South</span></span> | <span data-ttu-id="e8b35-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="e8b35-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="e8b35-148">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="e8b35-148">Canada Central</span></span> | <span data-ttu-id="e8b35-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="e8b35-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="e8b35-150">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="e8b35-150">Canada East</span></span> | <span data-ttu-id="e8b35-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="e8b35-151">40.86.226.166</span></span> | |
| <span data-ttu-id="e8b35-152">미국 중부</span><span class="sxs-lookup"><span data-stu-id="e8b35-152">Central US</span></span> | <span data-ttu-id="e8b35-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="e8b35-153">23.99.160.139</span></span> | <span data-ttu-id="e8b35-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="e8b35-154">13.67.215.62</span></span> |
| <span data-ttu-id="e8b35-155">동아시아</span><span class="sxs-lookup"><span data-stu-id="e8b35-155">East Asia</span></span> | <span data-ttu-id="e8b35-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="e8b35-156">191.234.2.139</span></span> | <span data-ttu-id="e8b35-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="e8b35-157">52.175.33.150</span></span> |
| <span data-ttu-id="e8b35-158">미국 동부 1</span><span class="sxs-lookup"><span data-stu-id="e8b35-158">East US 1</span></span> | <span data-ttu-id="e8b35-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="e8b35-159">191.238.6.43</span></span> | <span data-ttu-id="e8b35-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="e8b35-160">40.121.158.30</span></span> |
| <span data-ttu-id="e8b35-161">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="e8b35-161">East US 2</span></span> | <span data-ttu-id="e8b35-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="e8b35-162">191.239.224.107</span></span> | <span data-ttu-id="e8b35-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="e8b35-163">40.79.84.180</span></span> |
| <span data-ttu-id="e8b35-164">인도 중부</span><span class="sxs-lookup"><span data-stu-id="e8b35-164">India Central</span></span> | <span data-ttu-id="e8b35-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="e8b35-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="e8b35-166">인도 남부</span><span class="sxs-lookup"><span data-stu-id="e8b35-166">India South</span></span> | <span data-ttu-id="e8b35-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="e8b35-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="e8b35-168">인도 서부</span><span class="sxs-lookup"><span data-stu-id="e8b35-168">India West</span></span> | <span data-ttu-id="e8b35-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="e8b35-169">104.211.160.80</span></span> | |
| <span data-ttu-id="e8b35-170">일본 동부</span><span class="sxs-lookup"><span data-stu-id="e8b35-170">Japan East</span></span> | <span data-ttu-id="e8b35-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="e8b35-171">191.237.240.43</span></span> | <span data-ttu-id="e8b35-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="e8b35-172">13.78.61.196</span></span> |
| <span data-ttu-id="e8b35-173">일본 서부</span><span class="sxs-lookup"><span data-stu-id="e8b35-173">Japan West</span></span> | <span data-ttu-id="e8b35-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="e8b35-174">191.238.68.11</span></span> | <span data-ttu-id="e8b35-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="e8b35-175">104.214.148.156</span></span> |
| <span data-ttu-id="e8b35-176">한국 중부</span><span class="sxs-lookup"><span data-stu-id="e8b35-176">Korea Central</span></span> | <span data-ttu-id="e8b35-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="e8b35-177">52.231.32.42</span></span> | |
| <span data-ttu-id="e8b35-178">한국 남부</span><span class="sxs-lookup"><span data-stu-id="e8b35-178">Korea South</span></span> | <span data-ttu-id="e8b35-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="e8b35-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="e8b35-180">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="e8b35-180">North Central US</span></span> | <span data-ttu-id="e8b35-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="e8b35-181">23.98.55.75</span></span> | <span data-ttu-id="e8b35-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="e8b35-182">23.96.178.199</span></span> |
| <span data-ttu-id="e8b35-183">북유럽</span><span class="sxs-lookup"><span data-stu-id="e8b35-183">North Europe</span></span> | <span data-ttu-id="e8b35-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="e8b35-184">191.235.193.75</span></span> | <span data-ttu-id="e8b35-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="e8b35-185">40.113.93.91</span></span> |
| <span data-ttu-id="e8b35-186">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="e8b35-186">South Central US</span></span> | <span data-ttu-id="e8b35-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="e8b35-187">23.98.162.75</span></span> | <span data-ttu-id="e8b35-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="e8b35-188">13.66.62.124</span></span> |
| <span data-ttu-id="e8b35-189">동남아시아</span><span class="sxs-lookup"><span data-stu-id="e8b35-189">South East Asia</span></span> | <span data-ttu-id="e8b35-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="e8b35-190">23.100.117.95</span></span> | <span data-ttu-id="e8b35-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="e8b35-191">104.43.15.0</span></span> |
| <span data-ttu-id="e8b35-192">영국 북부</span><span class="sxs-lookup"><span data-stu-id="e8b35-192">UK North</span></span> | <span data-ttu-id="e8b35-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="e8b35-193">13.87.97.210</span></span> | |
| <span data-ttu-id="e8b35-194">영국 남부 1</span><span class="sxs-lookup"><span data-stu-id="e8b35-194">UK South 1</span></span> | <span data-ttu-id="e8b35-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="e8b35-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="e8b35-196">영국 남부 2</span><span class="sxs-lookup"><span data-stu-id="e8b35-196">UK South 2</span></span> | <span data-ttu-id="e8b35-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="e8b35-197">13.87.34.7</span></span> | |
| <span data-ttu-id="e8b35-198">영국 서부</span><span class="sxs-lookup"><span data-stu-id="e8b35-198">UK West</span></span> | <span data-ttu-id="e8b35-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="e8b35-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="e8b35-200">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="e8b35-200">West Central US</span></span> | <span data-ttu-id="e8b35-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="e8b35-201">13.78.145.25</span></span> | |
| <span data-ttu-id="e8b35-202">서유럽</span><span class="sxs-lookup"><span data-stu-id="e8b35-202">West Europe</span></span> | <span data-ttu-id="e8b35-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="e8b35-203">191.237.232.75</span></span> | <span data-ttu-id="e8b35-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="e8b35-204">40.68.37.158</span></span> |
| <span data-ttu-id="e8b35-205">미국 서부 1</span><span class="sxs-lookup"><span data-stu-id="e8b35-205">West US 1</span></span> | <span data-ttu-id="e8b35-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="e8b35-206">23.99.34.75</span></span> | <span data-ttu-id="e8b35-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="e8b35-207">104.42.238.205</span></span> |
| <span data-ttu-id="e8b35-208">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="e8b35-208">West US 2</span></span> | <span data-ttu-id="e8b35-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="e8b35-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="e8b35-210">SQL Database 연결 정책 변경</span><span class="sxs-lookup"><span data-stu-id="e8b35-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="e8b35-211">Azure SQL 데이터베이스 서버를 사용 하 여 hello에 대 한 Azure SQL 데이터베이스 연결 정책 toochange hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="e8b35-212">연결 정책을 너무 설정 되어 있으면**프록시**, 패킷 흐름 hello Azure SQL 데이터베이스 게이트웨이 통해 모든 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="e8b35-213">이 설정은 tooallow 아웃 바운드 tooonly hello Azure SQL 데이터베이스 게이트웨이 IP 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="e8b35-214">**프록시** 설정을 사용하면 **리디렉션** 설정보다 대기 시간이 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="e8b35-215">연결 정책을 설정 하는 경우 **리디렉션**, 모든 네트워크 패킷 흐름 직접 toohello 미들웨어 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="e8b35-216">이 설정은 tooallow 아웃 바운드 toomultiple Ip 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="e8b35-217">스크립트 toochange 연결 설정</span><span class="sxs-lookup"><span data-stu-id="e8b35-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8b35-218">이 스크립트는 hello 필요 [Azure PowerShell 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="e8b35-219">PowerShell 스크립트 뒤 hello toochange 연결 정책을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="e8b35-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8b35-220">Next steps</span></span>

- <span data-ttu-id="e8b35-221">참조 toochange Azure SQL 데이터베이스 서버에 대 한 Azure SQL 데이터베이스 연결 정책을 hello 하는 방법에 대 한 내용은 [REST API를 hello 만들기 또는 업데이트 서버 연결 정책을 사용 하 여](https://msdn.microsoft.com/library/azure/mt604439.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b35-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="e8b35-222">ADO.NET 4.5 이상 버전을 사용하는 클라이언트의 Azure SQL Database 연결 동작에 대한 자세한 정보는 [ADO.NET 4.5에 대한 1433 이외 포트](sql-database-develop-direct-route-ports-adonet-v12.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8b35-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="e8b35-223">일반 응용 프로그램 개발 개요 정보는 [SQL Database 응용 프로그램 개발 개요](sql-database-develop-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8b35-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
