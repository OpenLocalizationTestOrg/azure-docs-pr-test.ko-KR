---
title: "Azure Resource Health를 통해 지원되는 리소스 유형 | Microsoft Docs"
description: "Azure Resource Health를 통해 지원되는 리소스 유형"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: ece853d90f051828e07e48110c85dd9ad2dac5d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a><span data-ttu-id="2f05a-103">Azure Resource Health에서 리소스 유형 및 상태 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-103">Resource types and health checks in Azure resource health</span></span>
<span data-ttu-id="2f05a-104">다음은 리소스 유형별 리소스 상태를 통해 실행되는 모든 검사 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2f05a-104">Below is a complete list of all the checks executed through resource health by resource types.</span></span>

## <a name="microsoftcacheredisredis"></a><span data-ttu-id="2f05a-105">Microsoft.CacheRedis/Redis</span><span class="sxs-lookup"><span data-stu-id="2f05a-105">Microsoft.CacheRedis/Redis</span></span>
|<span data-ttu-id="2f05a-106">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-106">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-107">모든 캐시 노드가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-107">Are all the Cache nodes up and running?</span></span></li><li><span data-ttu-id="2f05a-108">데이터 센터 내에서 캐시에 도달할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-108">Can the Cache be reached from within the datacenter?</span></span></li><li><span data-ttu-id="2f05a-109">캐시가 최대 연결 수에 도달했는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-109">Has the Cache reached the maximum number of connections?</span></span></li><li> <span data-ttu-id="2f05a-110">캐시가 사용 가능한 메모리를 모두 소모했는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-110">Has the cache exhausted its available memory?</span></span> </li><li><span data-ttu-id="2f05a-111">캐시에 많은 수의 페이지 폴트가 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-111">Is the Cache experiencing a high number of page faults?</span></span></li><li><span data-ttu-id="2f05a-112">캐시에 부하가 큰가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-112">Is the Cache under heavy load?</span></span></li></ul>|

## <a name="microsoftcdnprofile"></a><span data-ttu-id="2f05a-113">Microsoft.CDN/profile</span><span class="sxs-lookup"><span data-stu-id="2f05a-113">Microsoft.CDN/profile</span></span>
|<span data-ttu-id="2f05a-114">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-114">Executed Checks</span></span>|
|---|
|<ul> <li><span data-ttu-id="2f05a-115">끝점이 중지, 제거 또는 잘못 구성되었는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-115">Has any of the endpoints been stopped, removed, or misconfigured?</span></span></li><li><span data-ttu-id="2f05a-116">CDN 구성 작업을 위해 보조 포털에 액세스할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-116">Is the supplemental portal accessible for CDN configuration operations?</span></span></li><li><span data-ttu-id="2f05a-117">CDN 끝점에서 진행 중인 배달 문제가 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-117">Are there ongoing delivery issues with the CDN endpoints?</span></span></li><li><span data-ttu-id="2f05a-118">사용자가 CDN 리소스의 구성을 변경할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-118">Can users change the configuration of their CDN resources?</span></span></li><li><span data-ttu-id="2f05a-119">구성 변경 내용이 예상된 속도로 전파되는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-119">Are configuration changes propagating at the expected rate?</span></span></li><li><span data-ttu-id="2f05a-120">사용자가 Azure Portal, PowerShell 또는 API를 사용하여 CDN 구성을 관리할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-120">Can users manage the CDN configuration using the Azure portal, PowerShell, or the API?</span></span></li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a><span data-ttu-id="2f05a-121">Microsoft.classiccompute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="2f05a-121">Microsoft.classiccompute/virtualmachines</span></span>
|<span data-ttu-id="2f05a-122">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-122">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-123">호스트 서버가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-123">Is the host server up and running?</span></span></li><li><span data-ttu-id="2f05a-124">호스트 OS 부팅이 완료되었는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-124">Has the host OS booting completed?</span></span></li><li><span data-ttu-id="2f05a-125">가상 컴퓨터 컨테이너가 프로비전되고 전원이 공급되는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-125">Is the virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="2f05a-126">호스트와 저장소 계정 간에 네트워크 연결이 되어 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-126">Is there network connectivity between the host and the storage account?</span></span></li><li><span data-ttu-id="2f05a-127">게스트 OS의 부팅이 완료되었는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-127">Has the booting of the guest OS completed?</span></span></li><li><span data-ttu-id="2f05a-128">진행 중인 계획된 유지 관리가 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-128">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a><span data-ttu-id="2f05a-129">Microsoft.cognitiveservices/accounts</span><span class="sxs-lookup"><span data-stu-id="2f05a-129">Microsoft.cognitiveservices/accounts</span></span>
|<span data-ttu-id="2f05a-130">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-130">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-131">데이터 센터 내에서 계정에 도달할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-131">Can the account be reached from within the datacenter?</span></span></li><li><span data-ttu-id="2f05a-132">Cognitive Services 리소스 공급자를 사용할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-132">Is the Cognitive Services Resource Provider available?</span></span></li><li><span data-ttu-id="2f05a-133">해당 지역에서 Cognitive Service를 사용할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-133">Is the Cognitive Service available in the appropriate region?</span></span></li><li><span data-ttu-id="2f05a-134">리소스 메타데이터가 있는 저장소 계정에서 읽기 작업을 수행할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-134">Can read operations be performed on the storage account holding the resource metadata?</span></span></li><li><span data-ttu-id="2f05a-135">API 호출 할당량에 도달했는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-135">Has the API call quota been reached?</span></span></li><li><span data-ttu-id="2f05a-136">API 호출 읽기 제한에 도달했는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-136">Has the API call read-limit been reached?</span></span></li></ul>|

## <a name="microsoftcomputevirtualmachines"></a><span data-ttu-id="2f05a-137">Microsoft.compute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="2f05a-137">Microsoft.compute/virtualmachines</span></span>
|<span data-ttu-id="2f05a-138">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-138">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-139">가상 컴퓨터를 호스팅하는 서버가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-139">Is the server hosting this virtual machine up and running?</span></span></li><li><span data-ttu-id="2f05a-140">호스트 OS 부팅이 완료되었는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-140">Has the host OS booting completed?</span></span></li><li><span data-ttu-id="2f05a-141">가상 컴퓨터 컨테이너가 프로비전되고 전원이 공급되는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-141">Is the virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="2f05a-142">호스트와 저장소 계정 간에 네트워크 연결이 되어 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-142">Is there network connectivity between the host and the storage account?</span></span></li><li><span data-ttu-id="2f05a-143">게스트 OS의 부팅이 완료되었는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-143">Has the booting of the guest OS completed?</span></span></li><li><span data-ttu-id="2f05a-144">진행 중인 계획된 유지 관리가 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-144">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a><span data-ttu-id="2f05a-145">Microsoft.datalakeanalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="2f05a-145">Microsoft.datalakeanalytics/accounts</span></span>
|<span data-ttu-id="2f05a-146">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-146">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-147">사용자가 지역의 Data Lake Analytics에 작업을 제출할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-147">Can users submit jobs to Data Lake Analytics in the region?</span></span></li><li><span data-ttu-id="2f05a-148">지역에서 기본 작업을 실행하여 성공적으로 완료되는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-148">Do basic jobs run and complete successfully in the region?</span></span></li><li><span data-ttu-id="2f05a-149">사용자가 지역에 카탈로그 항목을 나열할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-149">Can users list catalog items in the region?</span></span></li>|


## <a name="microsoftdatalakestoreaccounts"></a><span data-ttu-id="2f05a-150">Microsoft.datalakestore/accounts</span><span class="sxs-lookup"><span data-stu-id="2f05a-150">Microsoft.datalakestore/accounts</span></span>
|<span data-ttu-id="2f05a-151">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-151">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-152">사용자가 지역의 Data Lake Store에 데이터를 업로드할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-152">Can users upload data to Data Lake Store in the region?</span></span></li><li><span data-ttu-id="2f05a-153">사용자가 지역의 Data Lake Store에서 데이터를 다운로드할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-153">Can users download data from Data Lake Store in the region?</span></span></li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a><span data-ttu-id="2f05a-154">Microsoft.documentdb/databaseAccounts</span><span class="sxs-lookup"><span data-stu-id="2f05a-154">Microsoft.documentdb/databaseAccounts</span></span>
|<span data-ttu-id="2f05a-155">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-155">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-156">DocumentDB 서비스를 사용할 수 없어서 데이터베이스 또는 컬렉션 요청이 처리되지 않았는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-156">Have there been any database or collection requests not served due to a DocumentDB service unavailability?</span></span></li><li><span data-ttu-id="2f05a-157">DocumentDB 서비스를 사용할 수 없어서 문서 요청이 처리되지 않았는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-157">Have there been any document requests not served due to a DocumentDB service unavailability?</span></span></li></ul>|

## <a name="microsoftnetworkconnections"></a><span data-ttu-id="2f05a-158">Microsoft.network/connections</span><span class="sxs-lookup"><span data-stu-id="2f05a-158">Microsoft.network/connections</span></span>
|<span data-ttu-id="2f05a-159">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-159">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-160">VPN 터널이 연결되어 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-160">Is the VPN tunnel connected?</span></span></li><li><span data-ttu-id="2f05a-161">연결에 구성 충돌이 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-161">Are there configuration conflicts in the connection?</span></span></li><li><span data-ttu-id="2f05a-162">미리 공유한 키를 적절히 구성하였는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-162">Are the pre-shared keys properly configured?</span></span></li><li><span data-ttu-id="2f05a-163">VPN 온-프레미스 장치에 연결할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-163">Is the VPN on-premise device reachable?</span></span></li><li><span data-ttu-id="2f05a-164">IPSec/IKE 보안 정책에 일치하지 않는 사항이 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-164">Are there mismatches in the IPSec/IKE security policy?</span></span></li><li><span data-ttu-id="2f05a-165">S2S VPN 연결이 적절히 프로비전되었는가 아니면 실패한 상태인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-165">Is the S2S VPN connection properly provisioned or in a failed state?</span></span></li><li><span data-ttu-id="2f05a-166">VNET-VNET 연결이 적절히 프로비전되었는가 아니면 실패한 상태인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-166">Is the VNET-to-VNET connection properly provisioned or in a failed state?</span></span></li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a><span data-ttu-id="2f05a-167">Microsoft.network/virtualNetworkGateways</span><span class="sxs-lookup"><span data-stu-id="2f05a-167">Microsoft.network/virtualNetworkGateways</span></span>
|<span data-ttu-id="2f05a-168">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-168">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-169">인터넷에서 VPN Gateway에 연결할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-169">Is the VPN gateway reachable from the internet?</span></span></li><li><span data-ttu-id="2f05a-170">VPN Gateway가 대기 모드인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-170">Is the VPN Gateway in standby mode?</span></span></li><li><span data-ttu-id="2f05a-171">VPN 서비스가 게이트웨이에서 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-171">Is the VPN service running on the gateway?</span></span></li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a><span data-ttu-id="2f05a-172">Microsoft.NotificationHubs/namespace</span><span class="sxs-lookup"><span data-stu-id="2f05a-172">Microsoft.NotificationHubs/namespace</span></span>
|<span data-ttu-id="2f05a-173">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-173">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="2f05a-174">네임스페이스에서 등록, 설치 또는 전송과 같은 런타임 작업을 수행 할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-174">Can runtime operations like registration, installation, or send be performed on the namespace?</span></span></li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a><span data-ttu-id="2f05a-175">Microsoft.PowerBI/workspaceCollections</span><span class="sxs-lookup"><span data-stu-id="2f05a-175">Microsoft.PowerBI/workspaceCollections</span></span>
|<span data-ttu-id="2f05a-176">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-176">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-177">호스트 OS가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-177">Is the host OS up and running?</span></span></li><li><span data-ttu-id="2f05a-178">데이터 센터 외부에서 workspaceCollection에 연결할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-178">Is the workspaceCollection reachable from outside the datacenter?</span></span></li><li><span data-ttu-id="2f05a-179">PowerBI 리소스 공급자를 사용할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-179">Is the PowerBI Resource Provider available?</span></span></li><li><span data-ttu-id="2f05a-180">해당 지역에서 PowerBI 서비스를 사용할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-180">Is the PowerBI Service available in the appropriate region?</span></span></li></ul>|

## <a name="microsoftsearchsearchservices"></a><span data-ttu-id="2f05a-181">Microsoft.search/searchServices</span><span class="sxs-lookup"><span data-stu-id="2f05a-181">Microsoft.search/searchServices</span></span>
|<span data-ttu-id="2f05a-182">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-182">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-183">클러스터에서 진단 작업을 수행할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-183">Can diagnostics operations be performed on the cluster?</span></span></li></ul>|

## <a name="microsoftsqlserverdatabase"></a><span data-ttu-id="2f05a-184">Microsoft.SQL/Server/database</span><span class="sxs-lookup"><span data-stu-id="2f05a-184">Microsoft.SQL/Server/database</span></span>
|<span data-ttu-id="2f05a-185">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-185">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="2f05a-186">데이터베이스에 로그인했는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-186">Have there been logins to the database?</span></span></li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a><span data-ttu-id="2f05a-187">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="2f05a-187">Microsoft.StreamAnalytics/streamingjobs</span></span>
|<span data-ttu-id="2f05a-188">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-188">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-189">작업이 실행 중인 모든 호스트가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-189">Are all the hosts where the job is executing up and running?</span></span></li><li><span data-ttu-id="2f05a-190">작업을 시작할 수 없는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-190">Was the job unable to start?</span></span></li><li><span data-ttu-id="2f05a-191">진행 중인 런타임 업데이트가 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-191">Are there ongoing runtime upgrades?</span></span></li><li><span data-ttu-id="2f05a-192">작업이 예상된 상태인가(예: 실행 중 또는 고객에 의해 중지)?</span><span class="sxs-lookup"><span data-stu-id="2f05a-192">Is the job in an expected state (for example running or stopped by customer)?</span></span></li><li><span data-ttu-id="2f05a-193">작업에 메모리 부족 예외가 발생했는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-193">Has the job encountered out of memory exceptions?</span></span></li><li><span data-ttu-id="2f05a-194">진행 중인 예약된 계산 업데이트가 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-194">Are there ongoing scheduled compute updates?</span></span></li><li><span data-ttu-id="2f05a-195">실행 관리자(제어 계획)를 사용할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-195">Is the Execution Manager (control plan) available?</span></span></li></ul>|

## <a name="microsoftwebserverfarms"></a><span data-ttu-id="2f05a-196">Microsoft.web/serverFarms</span><span class="sxs-lookup"><span data-stu-id="2f05a-196">Microsoft.web/serverFarms</span></span>
|<span data-ttu-id="2f05a-197">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-197">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-198">호스트 서버가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-198">Is the host server up and running?</span></span></li><li><span data-ttu-id="2f05a-199">인터넷 정보 서비스를 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-199">Is Internet Information Services running?</span></span></li><li><span data-ttu-id="2f05a-200">부하 분산 장치를 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-200">Is the Load balancer running?</span></span></li><li><span data-ttu-id="2f05a-201">데이터 센터 내에서 웹 서비스 계획에 도달할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-201">Can the Web Service Plan be reached from within the datacenter?</span></span></li><li><span data-ttu-id="2f05a-202">serverFarm에 대한 사이트 콘텐츠를 호스팅하는 저장소 계정이 제공되는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-202">Is the storage account hosting the sites content for the serverFarm  available??</span></span></li></ul>|

## <a name="microsoftwebsites"></a><span data-ttu-id="2f05a-203">Microsoft.web/sites</span><span class="sxs-lookup"><span data-stu-id="2f05a-203">Microsoft.web/sites</span></span>
|<span data-ttu-id="2f05a-204">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="2f05a-204">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="2f05a-205">호스트 서버가 작동 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-205">Is the host server up and running?</span></span></li><li><span data-ttu-id="2f05a-206">인터넷 정보 서버를 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-206">Is Internet Information server running?</span></span></li><li><span data-ttu-id="2f05a-207">부하 분산 장치를 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-207">Is the Load balancer running?</span></span></li><li><span data-ttu-id="2f05a-208">데이터 센터 내에서 Web App에 도달할 수 있는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-208">Can the Web App be reached from within the datacenter?</span></span></li><li><span data-ttu-id="2f05a-209">사이트 콘텐츠를 호스팅하는 저장소 계정이 제공되는가?</span><span class="sxs-lookup"><span data-stu-id="2f05a-209">Is the storage account hosting the site content available?</span></span></li></ul>|

<span data-ttu-id="2f05a-210">리소스 상태에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f05a-210">See these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="2f05a-211">Azure Resource Health 소개</span><span class="sxs-lookup"><span data-stu-id="2f05a-211">Introduction to Azure resource health</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="2f05a-212">Azure Resource Health에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="2f05a-212">Frequently asked questions about Azure resource health</span></span>](Resource-health-faq.md)

