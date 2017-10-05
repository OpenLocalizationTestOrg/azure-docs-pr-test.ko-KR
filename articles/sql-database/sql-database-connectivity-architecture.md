---
title: "Azure SQL Database 연결 아키텍처 | Microsoft Docs"
description: "이 문서에서는 Azure 내부 또는 Azure 외부의 Azure SQLDB 연결 아키텍처에 대해 설명합니다."
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
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="8ac85-103">Azure SQL Database 연결 아키텍처</span><span class="sxs-lookup"><span data-stu-id="8ac85-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="8ac85-104">이 문서에서는 Azure SQL Database 연결 아키텍처에 대해 설명하고 다양한 구성 요소가 Azure SQL Database의 인스턴스에 트래픽을 전달하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="8ac85-105">이러한 Azure SQL Database 연결 구성 요소는 Azure 내에서 연결하는 클라이언트와 Azure 외부에서 연결하는 클라이언트를 사용하여 Azure 데이터베이스에 네트워크 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="8ac85-106">또한 이 문서에서는 연결되는 방법을 변경하는 스크립트 샘플 및 기본 연결 설정을 변경하는 데 관련된 고려 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="8ac85-107">이 문서를 읽은 후에 질문이 있는 경우에 dmalik@microsoft.com에서 Dhruv에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8ac85-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="8ac85-108">연결 아키텍처</span><span class="sxs-lookup"><span data-stu-id="8ac85-108">Connectivity architecture</span></span>

<span data-ttu-id="8ac85-109">다음 다이어그램은 Azure SQL Database 연결 아키텍처의 대략적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![아키텍처 개요](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="8ac85-111">다음 단계는 Azure SQL Database SLB(소프트웨어 부하 분산 장치) 및 Azure SQL Database 게이트웨이를 통해 Azure SQL Database에 연결이 설정되는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="8ac85-112">Azure 내부 또는 Azure 외부의 클라이언트는 공용 IP 주소를 포함하고 포트 1433에서 수신 대기하는 SLB에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="8ac85-113">SLB는 Azure SQL Database 게이트웨이에 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="8ac85-114">게이트웨이는 트래픽을 올바른 프록시 미들웨어로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="8ac85-115">프록시 미들웨어는 적절한 Azure SQL Database에 트래픽을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac85-116">이러한 각 구성 요소는 보호 네트워크 및 앱 계층에서 기본 제공되는 DDoS(distributed denial of service)를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="8ac85-117">Azure 내부에서 연결</span><span class="sxs-lookup"><span data-stu-id="8ac85-117">Connectivity from within Azure</span></span>

<span data-ttu-id="8ac85-118">Azure 내부에서 연결하는 경우 연결에는 기본적으로 **리디렉션** 연결 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="8ac85-119">**리디렉션** 정책의 경우 TCP 세션 이후 연결이 Azure SQL Database로 설정되고 대상 가상 IP가 Azure SQL Database 게이트웨이에서 프록시 미들웨어의 대상 가상 IP로 변경되어 클라이언트 세션이 프록시 미들웨어로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="8ac85-120">그런 다음 모든 후속 패킷은 Azure SQL Database 게이트웨이를 무시하고 프록시 미들웨어를 통해 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="8ac85-121">아래 다이어그램은 이 트래픽 흐름을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-121">The following diagram illustrates this traffic flow.</span></span>

![아키텍처 개요](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="8ac85-123">Azure 외부에서 연결</span><span class="sxs-lookup"><span data-stu-id="8ac85-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="8ac85-124">Azure 외부에서 연결하는 경우 연결에는 기본적으로 **프록시** 연결 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="8ac85-125">**프록시** 정책의 경우 TCP 세션이 Azure SQL Database 게이트웨이를 통해 설정되고 모든 후속 패킷이 게이트웨이를 통합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="8ac85-126">아래 다이어그램은 이 트래픽 흐름을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-126">The following diagram illustrates this traffic flow.</span></span>

![아키텍처 개요](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="8ac85-128">Azure SQL Database 게이트웨이 IP 주소</span><span class="sxs-lookup"><span data-stu-id="8ac85-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="8ac85-129">온-프레미스 리소스에서 Azure SQL Database에 연결하려면 Azure 지역의 Azure SQL Database 게이트웨이에 아웃바운드 네트워크 트래픽을 허용하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="8ac85-130">온-프레미스 리소스에서 연결할 때 기본 설정인 프록시 모드에서는 연결할 경우 연결은 게이트웨이를 통합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="8ac85-131">다음 표에서는 모든 데이터 지역에 있는 Azure SQL Database 게이트웨이의 기본 및 보조 IP를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="8ac85-132">일부 지역에는 두 개의 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="8ac85-133">이러한 지역에서 기본 IP 주소는 게이트웨이의 현재 IP 주소이고 두 번째 IP 주소는 장애 조치 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="8ac85-134">장애 조치 주소는 높은 서비스 가용성을 유지하기 위해 서버를 이동할 수 있는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="8ac85-135">이러한 지역의 경우 두 IP 주소에 아웃바운드를 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="8ac85-136">두 번째 IP 주소는 Microsoft가 소유하고 있으며 Azure SQL Database에서 연결을 허용하기 위해 활성화될 때까지 어떤 서비스도 수신하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="8ac85-137">지역 이름</span><span class="sxs-lookup"><span data-stu-id="8ac85-137">Region Name</span></span> | <span data-ttu-id="8ac85-138">기본 IP 주소</span><span class="sxs-lookup"><span data-stu-id="8ac85-138">Primary IP address</span></span> | <span data-ttu-id="8ac85-139">보조 IP 주소</span><span class="sxs-lookup"><span data-stu-id="8ac85-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="8ac85-140">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="8ac85-140">Australia East</span></span> | <span data-ttu-id="8ac85-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="8ac85-141">191.238.66.109</span></span> | <span data-ttu-id="8ac85-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="8ac85-142">13.75.149.87</span></span> |
| <span data-ttu-id="8ac85-143">오스트레일리아 동남부</span><span class="sxs-lookup"><span data-stu-id="8ac85-143">Australia South East</span></span> | <span data-ttu-id="8ac85-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="8ac85-144">191.239.192.109</span></span> | <span data-ttu-id="8ac85-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="8ac85-145">13.73.109.251</span></span> |
| <span data-ttu-id="8ac85-146">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="8ac85-146">Brazil South</span></span> | <span data-ttu-id="8ac85-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="8ac85-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="8ac85-148">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="8ac85-148">Canada Central</span></span> | <span data-ttu-id="8ac85-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="8ac85-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="8ac85-150">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="8ac85-150">Canada East</span></span> | <span data-ttu-id="8ac85-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="8ac85-151">40.86.226.166</span></span> | |
| <span data-ttu-id="8ac85-152">미국 중부</span><span class="sxs-lookup"><span data-stu-id="8ac85-152">Central US</span></span> | <span data-ttu-id="8ac85-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="8ac85-153">23.99.160.139</span></span> | <span data-ttu-id="8ac85-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="8ac85-154">13.67.215.62</span></span> |
| <span data-ttu-id="8ac85-155">동아시아</span><span class="sxs-lookup"><span data-stu-id="8ac85-155">East Asia</span></span> | <span data-ttu-id="8ac85-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="8ac85-156">191.234.2.139</span></span> | <span data-ttu-id="8ac85-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="8ac85-157">52.175.33.150</span></span> |
| <span data-ttu-id="8ac85-158">미국 동부 1</span><span class="sxs-lookup"><span data-stu-id="8ac85-158">East US 1</span></span> | <span data-ttu-id="8ac85-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="8ac85-159">191.238.6.43</span></span> | <span data-ttu-id="8ac85-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="8ac85-160">40.121.158.30</span></span> |
| <span data-ttu-id="8ac85-161">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="8ac85-161">East US 2</span></span> | <span data-ttu-id="8ac85-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="8ac85-162">191.239.224.107</span></span> | <span data-ttu-id="8ac85-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="8ac85-163">40.79.84.180</span></span> |
| <span data-ttu-id="8ac85-164">인도 중부</span><span class="sxs-lookup"><span data-stu-id="8ac85-164">India Central</span></span> | <span data-ttu-id="8ac85-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="8ac85-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="8ac85-166">인도 남부</span><span class="sxs-lookup"><span data-stu-id="8ac85-166">India South</span></span> | <span data-ttu-id="8ac85-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="8ac85-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="8ac85-168">인도 서부</span><span class="sxs-lookup"><span data-stu-id="8ac85-168">India West</span></span> | <span data-ttu-id="8ac85-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="8ac85-169">104.211.160.80</span></span> | |
| <span data-ttu-id="8ac85-170">일본 동부</span><span class="sxs-lookup"><span data-stu-id="8ac85-170">Japan East</span></span> | <span data-ttu-id="8ac85-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="8ac85-171">191.237.240.43</span></span> | <span data-ttu-id="8ac85-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="8ac85-172">13.78.61.196</span></span> |
| <span data-ttu-id="8ac85-173">일본 서부</span><span class="sxs-lookup"><span data-stu-id="8ac85-173">Japan West</span></span> | <span data-ttu-id="8ac85-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="8ac85-174">191.238.68.11</span></span> | <span data-ttu-id="8ac85-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="8ac85-175">104.214.148.156</span></span> |
| <span data-ttu-id="8ac85-176">한국 중부</span><span class="sxs-lookup"><span data-stu-id="8ac85-176">Korea Central</span></span> | <span data-ttu-id="8ac85-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="8ac85-177">52.231.32.42</span></span> | |
| <span data-ttu-id="8ac85-178">한국 남부</span><span class="sxs-lookup"><span data-stu-id="8ac85-178">Korea South</span></span> | <span data-ttu-id="8ac85-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="8ac85-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="8ac85-180">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="8ac85-180">North Central US</span></span> | <span data-ttu-id="8ac85-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="8ac85-181">23.98.55.75</span></span> | <span data-ttu-id="8ac85-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="8ac85-182">23.96.178.199</span></span> |
| <span data-ttu-id="8ac85-183">북유럽</span><span class="sxs-lookup"><span data-stu-id="8ac85-183">North Europe</span></span> | <span data-ttu-id="8ac85-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="8ac85-184">191.235.193.75</span></span> | <span data-ttu-id="8ac85-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="8ac85-185">40.113.93.91</span></span> |
| <span data-ttu-id="8ac85-186">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="8ac85-186">South Central US</span></span> | <span data-ttu-id="8ac85-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="8ac85-187">23.98.162.75</span></span> | <span data-ttu-id="8ac85-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="8ac85-188">13.66.62.124</span></span> |
| <span data-ttu-id="8ac85-189">동남아시아</span><span class="sxs-lookup"><span data-stu-id="8ac85-189">South East Asia</span></span> | <span data-ttu-id="8ac85-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="8ac85-190">23.100.117.95</span></span> | <span data-ttu-id="8ac85-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="8ac85-191">104.43.15.0</span></span> |
| <span data-ttu-id="8ac85-192">영국 북부</span><span class="sxs-lookup"><span data-stu-id="8ac85-192">UK North</span></span> | <span data-ttu-id="8ac85-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="8ac85-193">13.87.97.210</span></span> | |
| <span data-ttu-id="8ac85-194">영국 남부 1</span><span class="sxs-lookup"><span data-stu-id="8ac85-194">UK South 1</span></span> | <span data-ttu-id="8ac85-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="8ac85-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="8ac85-196">영국 남부 2</span><span class="sxs-lookup"><span data-stu-id="8ac85-196">UK South 2</span></span> | <span data-ttu-id="8ac85-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="8ac85-197">13.87.34.7</span></span> | |
| <span data-ttu-id="8ac85-198">영국 서부</span><span class="sxs-lookup"><span data-stu-id="8ac85-198">UK West</span></span> | <span data-ttu-id="8ac85-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="8ac85-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="8ac85-200">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="8ac85-200">West Central US</span></span> | <span data-ttu-id="8ac85-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="8ac85-201">13.78.145.25</span></span> | |
| <span data-ttu-id="8ac85-202">서유럽</span><span class="sxs-lookup"><span data-stu-id="8ac85-202">West Europe</span></span> | <span data-ttu-id="8ac85-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="8ac85-203">191.237.232.75</span></span> | <span data-ttu-id="8ac85-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="8ac85-204">40.68.37.158</span></span> |
| <span data-ttu-id="8ac85-205">미국 서부 1</span><span class="sxs-lookup"><span data-stu-id="8ac85-205">West US 1</span></span> | <span data-ttu-id="8ac85-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="8ac85-206">23.99.34.75</span></span> | <span data-ttu-id="8ac85-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="8ac85-207">104.42.238.205</span></span> |
| <span data-ttu-id="8ac85-208">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="8ac85-208">West US 2</span></span> | <span data-ttu-id="8ac85-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="8ac85-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="8ac85-210">SQL Database 연결 정책 변경</span><span class="sxs-lookup"><span data-stu-id="8ac85-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="8ac85-211">Azure SQL Database 서버에 대한 Azure SQL Database 연결 정책을 변경하려면 [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="8ac85-212">연결 정책을 **프록시**로 설정한 경우 모든 네트워크 패킷은 Azure SQL Database 게이트웨이를 통합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="8ac85-213">이 설정에서 Azure SQL Database 게이트웨이 IP로만 아웃바운드를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="8ac85-214">**프록시** 설정을 사용하면 **리디렉션** 설정보다 대기 시간이 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="8ac85-215">연결 정책을 **리디렉션**으로 설정하는 경우 모든 네트워크 패킷은 미들웨어 프록시에 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="8ac85-216">이 설정에서 여러 IP에 대한 아웃바운드를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="8ac85-217">연결 설정을 변경하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="8ac85-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac85-218">이 스크립트에는 [Azure PowerShell 모듈](/powershell/azure/install-azurerm-ps)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="8ac85-219">다음 PowerShell 스크립트에서는 연결 정책을 변경하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ac85-219">The following PowerShell script shows how to change the connection policy.</span></span>

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

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="8ac85-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ac85-220">Next steps</span></span>

- <span data-ttu-id="8ac85-221">Azure SQL Database 서버의 Azure SQL Database 연결 정책을 변경하는 방법에 대한 정보는 [REST API를 사용하여 서버 연결 정책 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt604439.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ac85-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="8ac85-222">ADO.NET 4.5 이상 버전을 사용하는 클라이언트의 Azure SQL Database 연결 동작에 대한 자세한 정보는 [ADO.NET 4.5에 대한 1433 이외 포트](sql-database-develop-direct-route-ports-adonet-v12.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ac85-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="8ac85-223">일반 응용 프로그램 개발 개요 정보는 [SQL Database 응용 프로그램 개발 개요](sql-database-develop-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ac85-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
