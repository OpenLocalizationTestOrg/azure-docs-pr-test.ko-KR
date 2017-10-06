---
title: "Azure 리소스 상태를 통해 리소스 종류 aaaSupported | Microsoft Docs"
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
ms.openlocfilehash: a37d5c33f6ef6fdfbce0daf392bc7fa57853c7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a><span data-ttu-id="a836a-103">Azure Resource Health에서 리소스 유형 및 상태 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-103">Resource types and health checks in Azure resource health</span></span>
<span data-ttu-id="a836a-104">리소스 종류에서 리소스 상태를 통해 실행 되는 모든 hello 검사의 전체 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a836a-104">Below is a complete list of all hello checks executed through resource health by resource types.</span></span>

## <a name="microsoftcacheredisredis"></a><span data-ttu-id="a836a-105">Microsoft.CacheRedis/Redis</span><span class="sxs-lookup"><span data-stu-id="a836a-105">Microsoft.CacheRedis/Redis</span></span>
|<span data-ttu-id="a836a-106">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-106">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-107">모든 hello 캐시 노드가 고 실행?</span><span class="sxs-lookup"><span data-stu-id="a836a-107">Are all hello Cache nodes up and running?</span></span></li><li><span data-ttu-id="a836a-108">Hello 캐시 hello 데이터 센터 내에서 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-108">Can hello Cache be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="a836a-109">캐시 hello 최대 연결 수에 도달 하는 hello 했습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-109">Has hello Cache reached hello maximum number of connections?</span></span></li><li> <span data-ttu-id="a836a-110">Hello 캐시의 사용 가능한 메모리를 소진 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a836a-110">Has hello cache exhausted its available memory?</span></span> </li><li><span data-ttu-id="a836a-111">많은 수의 페이지 폴트 발생 캐시 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-111">Is hello Cache experiencing a high number of page faults?</span></span></li><li><span data-ttu-id="a836a-112">부하가 캐시 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-112">Is hello Cache under heavy load?</span></span></li></ul>|

## <a name="microsoftcdnprofile"></a><span data-ttu-id="a836a-113">Microsoft.CDN/profile</span><span class="sxs-lookup"><span data-stu-id="a836a-113">Microsoft.CDN/profile</span></span>
|<span data-ttu-id="a836a-114">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-114">Executed Checks</span></span>|
|---|
|<ul> <li><span data-ttu-id="a836a-115">Hello 끝점이 중지 되었습니다, 제거 또는 잘못 구성 된?</span><span class="sxs-lookup"><span data-stu-id="a836a-115">Has any of hello endpoints been stopped, removed, or misconfigured?</span></span></li><li><span data-ttu-id="a836a-116">Hello 보조 포털 CDN 구성 작업에 액세스할 수 있는?</span><span class="sxs-lookup"><span data-stu-id="a836a-116">Is hello supplemental portal accessible for CDN configuration operations?</span></span></li><li><span data-ttu-id="a836a-117">사항이 hello로 지속적인 배달 문제 CDN 끝점 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-117">Are there ongoing delivery issues with hello CDN endpoints?</span></span></li><li><span data-ttu-id="a836a-118">사용자가 CDN 리소스의 hello 구성을 변경할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-118">Can users change hello configuration of their CDN resources?</span></span></li><li><span data-ttu-id="a836a-119">예상 hello 속도로 구성 변경 내용을 전파 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-119">Are configuration changes propagating at hello expected rate?</span></span></li><li><span data-ttu-id="a836a-120">사용자가 hello Azure 포털, PowerShell 또는 hello API 사용 하 여 hello CDN 구성을 관리할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-120">Can users manage hello CDN configuration using hello Azure portal, PowerShell, or hello API?</span></span></li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a><span data-ttu-id="a836a-121">Microsoft.classiccompute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="a836a-121">Microsoft.classiccompute/virtualmachines</span></span>
|<span data-ttu-id="a836a-122">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-122">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-123">호스트 서버 hello 작동 중 이며 실행?</span><span class="sxs-lookup"><span data-stu-id="a836a-123">Is hello host server up and running?</span></span></li><li><span data-ttu-id="a836a-124">완료 hello 호스트 운영 체제 부팅는?</span><span class="sxs-lookup"><span data-stu-id="a836a-124">Has hello host OS booting completed?</span></span></li><li><span data-ttu-id="a836a-125">Hello 가상 컴퓨터 컨테이너 프로 비전 및 전원을?</span><span class="sxs-lookup"><span data-stu-id="a836a-125">Is hello virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="a836a-126">이 hello 호스트와 hello 저장소 계정 간에 네트워크 연결이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-126">Is there network connectivity between hello host and hello storage account?</span></span></li><li><span data-ttu-id="a836a-127">완료 hello hello 게스트 OS의 부팅는?</span><span class="sxs-lookup"><span data-stu-id="a836a-127">Has hello booting of hello guest OS completed?</span></span></li><li><span data-ttu-id="a836a-128">진행 중인 계획된 유지 관리가 있는가?</span><span class="sxs-lookup"><span data-stu-id="a836a-128">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a><span data-ttu-id="a836a-129">Microsoft.cognitiveservices/accounts</span><span class="sxs-lookup"><span data-stu-id="a836a-129">Microsoft.cognitiveservices/accounts</span></span>
|<span data-ttu-id="a836a-130">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-130">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-131">Hello 계정 hello 데이터 센터 내에서 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-131">Can hello account be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="a836a-132">사용 가능한 Cognitive 서비스 리소스 공급자 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-132">Is hello Cognitive Services Resource Provider available?</span></span></li><li><span data-ttu-id="a836a-133">hello 적절 한 지역에서 사용할 수 있는 Cognitive 서비스 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-133">Is hello Cognitive Service available in hello appropriate region?</span></span></li><li><span data-ttu-id="a836a-134">읽을 수 hello 리소스 메타 데이터를 보유 하는 hello 저장소 계정에서 작업을 수행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-134">Can read operations be performed on hello storage account holding hello resource metadata?</span></span></li><li><span data-ttu-id="a836a-135">Hello API 호출 할당량에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a836a-135">Has hello API call quota been reached?</span></span></li><li><span data-ttu-id="a836a-136">Hello API 호출 읽기 제한에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a836a-136">Has hello API call read-limit been reached?</span></span></li></ul>|

## <a name="microsoftcomputevirtualmachines"></a><span data-ttu-id="a836a-137">Microsoft.compute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="a836a-137">Microsoft.compute/virtualmachines</span></span>
|<span data-ttu-id="a836a-138">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-138">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-139">Hello 서버를이 가상 컴퓨터를 호스트 및 실행?</span><span class="sxs-lookup"><span data-stu-id="a836a-139">Is hello server hosting this virtual machine up and running?</span></span></li><li><span data-ttu-id="a836a-140">완료 hello 호스트 운영 체제 부팅는?</span><span class="sxs-lookup"><span data-stu-id="a836a-140">Has hello host OS booting completed?</span></span></li><li><span data-ttu-id="a836a-141">Hello 가상 컴퓨터 컨테이너 프로 비전 및 전원을?</span><span class="sxs-lookup"><span data-stu-id="a836a-141">Is hello virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="a836a-142">이 hello 호스트와 hello 저장소 계정 간에 네트워크 연결이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-142">Is there network connectivity between hello host and hello storage account?</span></span></li><li><span data-ttu-id="a836a-143">완료 hello hello 게스트 OS의 부팅는?</span><span class="sxs-lookup"><span data-stu-id="a836a-143">Has hello booting of hello guest OS completed?</span></span></li><li><span data-ttu-id="a836a-144">진행 중인 계획된 유지 관리가 있는가?</span><span class="sxs-lookup"><span data-stu-id="a836a-144">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a><span data-ttu-id="a836a-145">Microsoft.datalakeanalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="a836a-145">Microsoft.datalakeanalytics/accounts</span></span>
|<span data-ttu-id="a836a-146">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-146">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-147">전송 작업에서 tooData Lake 분석 하는 사용자 수 영역을 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-147">Can users submit jobs tooData Lake Analytics in hello region?</span></span></li><li><span data-ttu-id="a836a-148">기본 작업에 성공적으로 완료 및 실행 hello 지역 합니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-148">Do basic jobs run and complete successfully in hello region?</span></span></li><li><span data-ttu-id="a836a-149">사용자가 hello 지역에서 카탈로그 항목을 나열할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-149">Can users list catalog items in hello region?</span></span></li>|


## <a name="microsoftdatalakestoreaccounts"></a><span data-ttu-id="a836a-150">Microsoft.datalakestore/accounts</span><span class="sxs-lookup"><span data-stu-id="a836a-150">Microsoft.datalakestore/accounts</span></span>
|<span data-ttu-id="a836a-151">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-151">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-152">사용자가 hello 지역에서 데이터 tooData 레이크 저장소에 업로드할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-152">Can users upload data tooData Lake Store in hello region?</span></span></li><li><span data-ttu-id="a836a-153">사용자가 hello 지역에 데이터 레이크 저장소에서 데이터를 다운로드할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-153">Can users download data from Data Lake Store in hello region?</span></span></li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a><span data-ttu-id="a836a-154">Microsoft.documentdb/databaseAccounts</span><span class="sxs-lookup"><span data-stu-id="a836a-154">Microsoft.documentdb/databaseAccounts</span></span>
|<span data-ttu-id="a836a-155">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-155">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-156">Tooa DocumentDB 서비스 사용 불가 인해 제공 되지 않는 데이터베이스 또는 컬렉션 요청 있었는지가?</span><span class="sxs-lookup"><span data-stu-id="a836a-156">Have there been any database or collection requests not served due tooa DocumentDB service unavailability?</span></span></li><li><span data-ttu-id="a836a-157">Tooa DocumentDB 서비스 사용 불가 인해 제공 되지 않는 모든 문서 요청 있었는지가?</span><span class="sxs-lookup"><span data-stu-id="a836a-157">Have there been any document requests not served due tooa DocumentDB service unavailability?</span></span></li></ul>|

## <a name="microsoftnetworkconnections"></a><span data-ttu-id="a836a-158">Microsoft.network/connections</span><span class="sxs-lookup"><span data-stu-id="a836a-158">Microsoft.network/connections</span></span>
|<span data-ttu-id="a836a-159">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-159">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-160">Hello VPN 터널 연결 되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-160">Is hello VPN tunnel connected?</span></span></li><li><span data-ttu-id="a836a-161">Hello 연결에서 구성 충돌 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-161">Are there configuration conflicts in hello connection?</span></span></li><li><span data-ttu-id="a836a-162">Hello 사전 공유 키 제대로 구성 되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-162">Are hello pre-shared keys properly configured?</span></span></li><li><span data-ttu-id="a836a-163">Hello VPN 온-프레미스 장치를 연결할 수 있는?</span><span class="sxs-lookup"><span data-stu-id="a836a-163">Is hello VPN on-premise device reachable?</span></span></li><li><span data-ttu-id="a836a-164">Hello IPSec/IKE 보안 정책에 불일치 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-164">Are there mismatches in hello IPSec/IKE security policy?</span></span></li><li><span data-ttu-id="a836a-165">제대로 프로 비전 되거나 실패 한 상태로 hello S2S VPN 연결을 이란?</span><span class="sxs-lookup"><span data-stu-id="a836a-165">Is hello S2S VPN connection properly provisioned or in a failed state?</span></span></li><li><span data-ttu-id="a836a-166">제대로 프로 비전 되거나 실패 한 상태로 hello VNET 대 VNET 연결 이란?</span><span class="sxs-lookup"><span data-stu-id="a836a-166">Is hello VNET-to-VNET connection properly provisioned or in a failed state?</span></span></li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a><span data-ttu-id="a836a-167">Microsoft.network/virtualNetworkGateways</span><span class="sxs-lookup"><span data-stu-id="a836a-167">Microsoft.network/virtualNetworkGateways</span></span>
|<span data-ttu-id="a836a-168">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-168">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-169">hello VPN 게이트웨이에서 연결할 수 있는 인터넷 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-169">Is hello VPN gateway reachable from hello internet?</span></span></li><li><span data-ttu-id="a836a-170">이 대기 모드에서 VPN 게이트웨이 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-170">Is hello VPN Gateway in standby mode?</span></span></li><li><span data-ttu-id="a836a-171">Hello VPN 서비스가 hello 게이트웨이에서 실행 중 입니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-171">Is hello VPN service running on hello gateway?</span></span></li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a><span data-ttu-id="a836a-172">Microsoft.NotificationHubs/namespace</span><span class="sxs-lookup"><span data-stu-id="a836a-172">Microsoft.NotificationHubs/namespace</span></span>
|<span data-ttu-id="a836a-173">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-173">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="a836a-174">등록, 설치 또는 송신과 같은 런타임 작업 hello 네임 스페이스에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a836a-174">Can runtime operations like registration, installation, or send be performed on hello namespace?</span></span></li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a><span data-ttu-id="a836a-175">Microsoft.PowerBI/workspaceCollections</span><span class="sxs-lookup"><span data-stu-id="a836a-175">Microsoft.PowerBI/workspaceCollections</span></span>
|<span data-ttu-id="a836a-176">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-176">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-177">hello 호스트 운영 체제를 실행 한?</span><span class="sxs-lookup"><span data-stu-id="a836a-177">Is hello host OS up and running?</span></span></li><li><span data-ttu-id="a836a-178">Hello workspaceCollection hello 데이터 센터 외부에서 연결할 수 있는?</span><span class="sxs-lookup"><span data-stu-id="a836a-178">Is hello workspaceCollection reachable from outside hello datacenter?</span></span></li><li><span data-ttu-id="a836a-179">hello PowerBI 리소스 공급자를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-179">Is hello PowerBI Resource Provider available?</span></span></li><li><span data-ttu-id="a836a-180">hello 적절 한 지역에서 사용할 수 있는 PowerBI 서비스 hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-180">Is hello PowerBI Service available in hello appropriate region?</span></span></li></ul>|

## <a name="microsoftsearchsearchservices"></a><span data-ttu-id="a836a-181">Microsoft.search/searchServices</span><span class="sxs-lookup"><span data-stu-id="a836a-181">Microsoft.search/searchServices</span></span>
|<span data-ttu-id="a836a-182">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-182">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-183">Hello 클러스터에서 진단 작업을 수행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-183">Can diagnostics operations be performed on hello cluster?</span></span></li></ul>|

## <a name="microsoftsqlserverdatabase"></a><span data-ttu-id="a836a-184">Microsoft.SQL/Server/database</span><span class="sxs-lookup"><span data-stu-id="a836a-184">Microsoft.SQL/Server/database</span></span>
|<span data-ttu-id="a836a-185">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-185">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="a836a-186">로그인 toohello 데이터베이스 있었는지가?</span><span class="sxs-lookup"><span data-stu-id="a836a-186">Have there been logins toohello database?</span></span></li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a><span data-ttu-id="a836a-187">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="a836a-187">Microsoft.StreamAnalytics/streamingjobs</span></span>
|<span data-ttu-id="a836a-188">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-188">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-189">Hello 작업은를 실행 하 고 실행 중인 모든 hello 호스트?</span><span class="sxs-lookup"><span data-stu-id="a836a-189">Are all hello hosts where hello job is executing up and running?</span></span></li><li><span data-ttu-id="a836a-190">Hello 작업이 없습니다 toostart 되었습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-190">Was hello job unable toostart?</span></span></li><li><span data-ttu-id="a836a-191">진행 중인 런타임 업데이트가 있는가?</span><span class="sxs-lookup"><span data-stu-id="a836a-191">Are there ongoing runtime upgrades?</span></span></li><li><span data-ttu-id="a836a-192">(예: 실행 중 또는 고객에 의해 중지) 예상 되는 상태에서 hello 작업은?</span><span class="sxs-lookup"><span data-stu-id="a836a-192">Is hello job in an expected state (for example running or stopped by customer)?</span></span></li><li><span data-ttu-id="a836a-193">Hello 작업이 발생 했습니다 아웃 메모리 예외의?</span><span class="sxs-lookup"><span data-stu-id="a836a-193">Has hello job encountered out of memory exceptions?</span></span></li><li><span data-ttu-id="a836a-194">진행 중인 예약된 계산 업데이트가 있는가?</span><span class="sxs-lookup"><span data-stu-id="a836a-194">Are there ongoing scheduled compute updates?</span></span></li><li><span data-ttu-id="a836a-195">사용할 수 있는 실행 관리자 (제어 계획) hello?</span><span class="sxs-lookup"><span data-stu-id="a836a-195">Is hello Execution Manager (control plan) available?</span></span></li></ul>|

## <a name="microsoftwebserverfarms"></a><span data-ttu-id="a836a-196">Microsoft.web/serverFarms</span><span class="sxs-lookup"><span data-stu-id="a836a-196">Microsoft.web/serverFarms</span></span>
|<span data-ttu-id="a836a-197">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-197">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-198">호스트 서버 hello 작동 중 이며 실행?</span><span class="sxs-lookup"><span data-stu-id="a836a-198">Is hello host server up and running?</span></span></li><li><span data-ttu-id="a836a-199">인터넷 정보 서비스를 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="a836a-199">Is Internet Information Services running?</span></span></li><li><span data-ttu-id="a836a-200">부하 분산 장치 hello 실행 중 입니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-200">Is hello Load balancer running?</span></span></li><li><span data-ttu-id="a836a-201">웹 서비스를 계획 하는 hello hello 데이터 센터 내에서 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-201">Can hello Web Service Plan be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="a836a-202">서버 팜 hello에 대 한 hello 저장소 계정 호스팅 hello 사이트 콘텐츠를 사용할 수??</span><span class="sxs-lookup"><span data-stu-id="a836a-202">Is hello storage account hosting hello sites content for hello serverFarm  available??</span></span></li></ul>|

## <a name="microsoftwebsites"></a><span data-ttu-id="a836a-203">Microsoft.web/sites</span><span class="sxs-lookup"><span data-stu-id="a836a-203">Microsoft.web/sites</span></span>
|<span data-ttu-id="a836a-204">실행된 검사</span><span class="sxs-lookup"><span data-stu-id="a836a-204">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="a836a-205">호스트 서버 hello 작동 중 이며 실행?</span><span class="sxs-lookup"><span data-stu-id="a836a-205">Is hello host server up and running?</span></span></li><li><span data-ttu-id="a836a-206">인터넷 정보 서버를 실행 중인가?</span><span class="sxs-lookup"><span data-stu-id="a836a-206">Is Internet Information server running?</span></span></li><li><span data-ttu-id="a836a-207">부하 분산 장치 hello 실행 중 입니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-207">Is hello Load balancer running?</span></span></li><li><span data-ttu-id="a836a-208">Hello 웹 응용 프로그램 hello 데이터 센터 내에서 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a836a-208">Can hello Web App be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="a836a-209">Hello 저장소 계정 hello 사용 가능한 사이트 콘텐츠를 호스팅하는?</span><span class="sxs-lookup"><span data-stu-id="a836a-209">Is hello storage account hosting hello site content available?</span></span></li></ul>|

<span data-ttu-id="a836a-210">이러한 리소스 toolearn 리소스 상태에 대 한 자세한 참조:</span><span class="sxs-lookup"><span data-stu-id="a836a-210">See these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="a836a-211">소개 tooAzure 리소스 상태</span><span class="sxs-lookup"><span data-stu-id="a836a-211">Introduction tooAzure resource health</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="a836a-212">Azure Resource Health에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="a836a-212">Frequently asked questions about Azure resource health</span></span>](Resource-health-faq.md)

