---
title: "Azure 네트워크 감시자의 연결 문제 해결 aaaIntroduction tooresource | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 리소스 문제 해결 기능에 대 한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="94dfc-103">Azure 네트워크 감시자의 연결 문제 해결 소개 tooresource</span><span class="sxs-lookup"><span data-stu-id="94dfc-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="94dfc-104">Virtual Network 게이트웨이는 온-프레미스 리소스 및 Azure 내 다른 가상 네트워크 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="94dfc-105">이러한 게이트웨이 및 해당 연결을 모니터링 하는 것은 중요 한 tooensuring 통신 손상 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="94dfc-106">네트워크 감시자 제공 hello 기능 tootroubleshoot 가상 네트워크 게이트웨이 및 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="94dfc-107">이 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="94dfc-108">호출 되 면 네트워크 감시자 hello 가상 네트워크 게이트웨이 또는 연결 및 반환 hello 적절 한 결과의 hello 상태를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="94dfc-109">이 요청이 장기 실행 트랜잭션으로 인 hello 진단 완료 되 면 hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="94dfc-111">결과</span><span class="sxs-lookup"><span data-stu-id="94dfc-111">Results</span></span>

<span data-ttu-id="94dfc-112">반환 된 hello 예비 결과 hello 리소스의 hello 상태의 전반적인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="94dfc-113">Hello 섹션 다음에 표시 된 대로 리소스에 대 한 심층 정보를 제공:</span><span class="sxs-lookup"><span data-stu-id="94dfc-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="94dfc-114">hello 다음 목록은 API를 해결 하는 hello로 반환 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="94dfc-115">**startTime** -이 값은 hello 시간이 hello 해결 API 호출을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="94dfc-116">**endTime** -이 값은 hello 시간이 hello 문제 해결이 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="94dfc-117">**code** - 이 값은 단일 진단 오류가 발생할 경우 이 값은 UnHealthy입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="94dfc-118">**결과** -결과 hello 연결 또는 hello 가상 네트워크 게이트웨이 반환 된 결과의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="94dfc-119">**id** -이 값은 hello 오류 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="94dfc-120">**요약** -이 값은 hello 오류의 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="94dfc-121">**자세한** -이 값은 hello 오류에 대 한 자세한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="94dfc-122">**recommendedActions** -이 속성은 tootake 권장 되는 작업의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="94dfc-123">**actionText** -이 값에는 어떤 작업 tootake를 설명 하는 hello 텍스트 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="94dfc-124">**actionUri** -이 값은 방법에 hello URI toodocumentation 제공 tooact 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="94dfc-125">**actionUriText** -이 값은 간단한 설명 hello 동작 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="94dfc-126">hello 테이블 hello 서로 다른 오류 형식 표시 (id가 결과 목록 앞에 오는 hello에서) 사용할 수 있는 다음을 선택 하 고 경우 hello 오류 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="94dfc-127">게이트웨이</span><span class="sxs-lookup"><span data-stu-id="94dfc-127">Gateway</span></span>

| <span data-ttu-id="94dfc-128">오류 유형</span><span class="sxs-lookup"><span data-stu-id="94dfc-128">Fault Type</span></span> | <span data-ttu-id="94dfc-129">이유</span><span class="sxs-lookup"><span data-stu-id="94dfc-129">Reason</span></span> | <span data-ttu-id="94dfc-130">로그</span><span class="sxs-lookup"><span data-stu-id="94dfc-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="94dfc-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="94dfc-131">NoFault</span></span> | <span data-ttu-id="94dfc-132">오류가 발견되지 않은 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-132">When no error is detected.</span></span> |<span data-ttu-id="94dfc-133">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-133">Yes</span></span>|
| <span data-ttu-id="94dfc-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="94dfc-134">GatewayNotFound</span></span> | <span data-ttu-id="94dfc-135">게이트웨이를 찾을 수 없거나 게이트웨이가 프로비저닝되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="94dfc-136">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-136">No</span></span>|
| <span data-ttu-id="94dfc-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="94dfc-137">PlannedMaintenance</span></span> |  <span data-ttu-id="94dfc-138">게이트웨이 인스턴스가 유지 관리되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="94dfc-139">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-139">No</span></span>|
| <span data-ttu-id="94dfc-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="94dfc-140">UserDrivenUpdate</span></span> | <span data-ttu-id="94dfc-141">사용자 업데이트를 진행 중인 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-141">When a user update is in progress.</span></span> <span data-ttu-id="94dfc-142">크기 조정 작업일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-142">This could be a resize operation.</span></span> | <span data-ttu-id="94dfc-143">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-143">No</span></span> |
| <span data-ttu-id="94dfc-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="94dfc-144">VipUnResponsive</span></span> | <span data-ttu-id="94dfc-145">Hello hello 게이트웨이의 기본 인스턴스를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="94dfc-146">이 hello 상태 검색에 실패할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="94dfc-147">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-147">No</span></span> |
| <span data-ttu-id="94dfc-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="94dfc-148">PlatformInActive</span></span> | <span data-ttu-id="94dfc-149">Hello 플랫폼에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="94dfc-150">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-150">No</span></span>|
| <span data-ttu-id="94dfc-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="94dfc-151">ServiceNotRunning</span></span> | <span data-ttu-id="94dfc-152">hello 기본 서비스가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-152">hello underlying service is not running.</span></span> | <span data-ttu-id="94dfc-153">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-153">No</span></span>|
| <span data-ttu-id="94dfc-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="94dfc-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="94dfc-155">연결이 없는 hello 게이트웨이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="94dfc-156">단지 경고일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-156">This is only a warning.</span></span>| <span data-ttu-id="94dfc-157">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-157">No</span></span>|
| <span data-ttu-id="94dfc-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="94dfc-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="94dfc-159">연결이 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-159">Connections are not connected.</span></span> <span data-ttu-id="94dfc-160">단지 경고일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-160">This is only a warning.</span></span>| <span data-ttu-id="94dfc-161">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-161">Yes</span></span>|
| <span data-ttu-id="94dfc-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="94dfc-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="94dfc-163">hello 현재 게이트웨이 CPU 사용량은 > 95%입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="94dfc-164">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="94dfc-165">연결</span><span class="sxs-lookup"><span data-stu-id="94dfc-165">Connection</span></span>

| <span data-ttu-id="94dfc-166">오류 유형</span><span class="sxs-lookup"><span data-stu-id="94dfc-166">Fault Type</span></span> | <span data-ttu-id="94dfc-167">이유</span><span class="sxs-lookup"><span data-stu-id="94dfc-167">Reason</span></span> | <span data-ttu-id="94dfc-168">로그</span><span class="sxs-lookup"><span data-stu-id="94dfc-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="94dfc-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="94dfc-169">NoFault</span></span> | <span data-ttu-id="94dfc-170">오류가 발견되지 않은 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-170">When no error is detected.</span></span> |<span data-ttu-id="94dfc-171">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-171">Yes</span></span>|
| <span data-ttu-id="94dfc-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="94dfc-172">GatewayNotFound</span></span> | <span data-ttu-id="94dfc-173">게이트웨이를 찾을 수 없거나 게이트웨이가 프로비저닝되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="94dfc-174">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-174">No</span></span>|
| <span data-ttu-id="94dfc-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="94dfc-175">PlannedMaintenance</span></span> | <span data-ttu-id="94dfc-176">게이트웨이 인스턴스가 유지 관리되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="94dfc-177">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-177">No</span></span>|
| <span data-ttu-id="94dfc-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="94dfc-178">UserDrivenUpdate</span></span> | <span data-ttu-id="94dfc-179">사용자 업데이트를 진행 중인 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-179">When a user update is in progress.</span></span> <span data-ttu-id="94dfc-180">크기 조정 작업일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-180">This could be a resize operation.</span></span>  | <span data-ttu-id="94dfc-181">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-181">No</span></span> |
| <span data-ttu-id="94dfc-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="94dfc-182">VipUnResponsive</span></span> | <span data-ttu-id="94dfc-183">Hello hello 게이트웨이의 기본 인스턴스를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="94dfc-184">Hello 상태 검색이 실패 하면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="94dfc-185">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-185">No</span></span> |
| <span data-ttu-id="94dfc-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="94dfc-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="94dfc-187">연결 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-187">Connection configuration is missing.</span></span> | <span data-ttu-id="94dfc-188">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-188">No</span></span> |
| <span data-ttu-id="94dfc-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="94dfc-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="94dfc-190">hello 연결 "연결이 끊긴 된"으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="94dfc-191">아니요</span><span class="sxs-lookup"><span data-stu-id="94dfc-191">No</span></span>|
| <span data-ttu-id="94dfc-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="94dfc-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="94dfc-193">hello 기본 서비스 연결을 구성 하는 hello를 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="94dfc-194">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-194">Yes</span></span> |
| <span data-ttu-id="94dfc-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="94dfc-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="94dfc-196">기본 서비스가 hello 대기로 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="94dfc-197">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-197">Yes</span></span>|
| <span data-ttu-id="94dfc-198">인증</span><span class="sxs-lookup"><span data-stu-id="94dfc-198">Authentication</span></span> | <span data-ttu-id="94dfc-199">미리 공유한 키가 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="94dfc-200">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-200">Yes</span></span>|
| <span data-ttu-id="94dfc-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="94dfc-201">PeerReachability</span></span> | <span data-ttu-id="94dfc-202">hello 피어 게이트웨이 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="94dfc-203">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-203">Yes</span></span>|
| <span data-ttu-id="94dfc-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="94dfc-204">IkePolicyMismatch</span></span> | <span data-ttu-id="94dfc-205">hello 피어 게이트웨이 Azure에서 지원 되지 않는 IKE 정책에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="94dfc-206">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-206">Yes</span></span>|
| <span data-ttu-id="94dfc-207">WfpParse 오류</span><span class="sxs-lookup"><span data-stu-id="94dfc-207">WfpParse Error</span></span> | <span data-ttu-id="94dfc-208">Hello WFP 로그 구문 분석 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="94dfc-209">예</span><span class="sxs-lookup"><span data-stu-id="94dfc-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="94dfc-210">지원되는 게이트웨이 유형</span><span class="sxs-lookup"><span data-stu-id="94dfc-210">Supported Gateway types</span></span>

<span data-ttu-id="94dfc-211">hello 다음 목록은 hello 지원 표시는 게이트웨이 및 연결은 지원 네트워크 감시자 문제 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="94dfc-212">**게이트웨이 유형**</span><span class="sxs-lookup"><span data-stu-id="94dfc-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="94dfc-213">VPN</span><span class="sxs-lookup"><span data-stu-id="94dfc-213">VPN</span></span>      | <span data-ttu-id="94dfc-214">지원됨</span><span class="sxs-lookup"><span data-stu-id="94dfc-214">Supported</span></span>        |
|<span data-ttu-id="94dfc-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="94dfc-215">ExpressRoute</span></span> | <span data-ttu-id="94dfc-216">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="94dfc-216">Not Supported</span></span> |
|<span data-ttu-id="94dfc-217">HyperNet</span><span class="sxs-lookup"><span data-stu-id="94dfc-217">Hypernet</span></span> | <span data-ttu-id="94dfc-218">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="94dfc-218">Not Supported</span></span>|
|<span data-ttu-id="94dfc-219">**VPN 유형**</span><span class="sxs-lookup"><span data-stu-id="94dfc-219">**VPN types**</span></span> | |
|<span data-ttu-id="94dfc-220">경로 기반</span><span class="sxs-lookup"><span data-stu-id="94dfc-220">Route Based</span></span> | <span data-ttu-id="94dfc-221">지원됨</span><span class="sxs-lookup"><span data-stu-id="94dfc-221">Supported</span></span>|
|<span data-ttu-id="94dfc-222">정책 기반</span><span class="sxs-lookup"><span data-stu-id="94dfc-222">Policy Based</span></span> | <span data-ttu-id="94dfc-223">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="94dfc-223">Not Supported</span></span>|
|<span data-ttu-id="94dfc-224">**연결 유형**</span><span class="sxs-lookup"><span data-stu-id="94dfc-224">**Connection types**</span></span>||
|<span data-ttu-id="94dfc-225">IPSec</span><span class="sxs-lookup"><span data-stu-id="94dfc-225">IPSec</span></span>| <span data-ttu-id="94dfc-226">지원됨</span><span class="sxs-lookup"><span data-stu-id="94dfc-226">Supported</span></span>|
|<span data-ttu-id="94dfc-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="94dfc-227">VNet2Vnet</span></span>| <span data-ttu-id="94dfc-228">지원됨</span><span class="sxs-lookup"><span data-stu-id="94dfc-228">Supported</span></span>|
|<span data-ttu-id="94dfc-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="94dfc-229">ExpressRoute</span></span>| <span data-ttu-id="94dfc-230">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="94dfc-230">Not Supported</span></span>|
|<span data-ttu-id="94dfc-231">HyperNet</span><span class="sxs-lookup"><span data-stu-id="94dfc-231">Hypernet</span></span>| <span data-ttu-id="94dfc-232">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="94dfc-232">Not Supported</span></span>|
|<span data-ttu-id="94dfc-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="94dfc-233">VPNClient</span></span>| <span data-ttu-id="94dfc-234">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="94dfc-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="94dfc-235">로그 파일</span><span class="sxs-lookup"><span data-stu-id="94dfc-235">Log files</span></span>

<span data-ttu-id="94dfc-236">hello 리소스 문제 해결 로그 파일은 리소스 문제 해결 완료 된 후 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="94dfc-237">hello 다음 이미지 hello 예의 내용을 보여줍니다 오류가 발생 하는 호출.</span><span class="sxs-lookup"><span data-stu-id="94dfc-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![Zip 파일][1]

> [!NOTE]
> <span data-ttu-id="94dfc-239">경우에 따라 hello 로그 파일의 하위 집합만 toostorage를 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="94dfc-240">Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="94dfc-241">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="94dfc-242">저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="94dfc-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="94dfc-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="94dfc-243">ConnectionStats.txt</span></span>

<span data-ttu-id="94dfc-244">hello **ConnectionStats.txt** 파일 hello 송 / 수신 바이트, 연결 상태 및 연결 하는 hello 시간 hello를 포함 하 여 연결의 전체 통계를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="94dfc-245">API 문제를 해결 하는 hello 호출 toohello 정상 상태를 반환 하면 hello hello zip 파일에 반환 되는는 **ConnectionStats.txt** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="94dfc-246">hello이이 파일의 내용이 다음 예제와 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="94dfc-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="94dfc-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="94dfc-247">CPUStats.txt</span></span>

<span data-ttu-id="94dfc-248">hello **CPUStats.txt** CPU 사용량과 메모리가 테스트 hello 시점에서 사용 가능한 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="94dfc-249">이 파일의 내용을 hello은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="94dfc-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="94dfc-250">IKEErrors.txt</span></span>

<span data-ttu-id="94dfc-251">hello **IKEErrors.txt** 파일 모니터링 하는 동안 발견 된 IKE 오류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="94dfc-252">hello 다음 예제에서는 IKEErrors.txt 파일의 내용을 hello</span><span class="sxs-lookup"><span data-stu-id="94dfc-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="94dfc-253">오류는 hello 문제에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="94dfc-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="94dfc-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="94dfc-255">hello **Scrubbed wfpdiag.txt** hello wfp 로그를 포함 하는 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="94dfc-256">이 로그에는 패킷 삭제 및 IKE/AuthIP 오류에 대한 기록이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="94dfc-257">hello 다음 예제에서는 hello Scrubbed wfpdiag.txt 파일의 내용을 hello</span><span class="sxs-lookup"><span data-stu-id="94dfc-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="94dfc-258">이 예제에서는 연결의 공유 키 hello hello hello 아래에서 세 번째 줄에서 볼 수 있듯이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="94dfc-259">다음 예제는 hello hello 전체 로그의 코드 조각은 방금는 hello 로그 hello 문제에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="94dfc-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="94dfc-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="94dfc-261">hello **wfpdiag.txt.sum** hello 버퍼 및 처리 된 이벤트를 표시 하는 로그 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="94dfc-262">hello 다음 예제는 hello 내용의 wfpdiag.txt.sum 파일.</span><span class="sxs-lookup"><span data-stu-id="94dfc-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="94dfc-263">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94dfc-263">Next steps</span></span>

<span data-ttu-id="94dfc-264">어떻게 toodiagnose VPN 게이트웨이 및 연결을 통해 hello 포털 방문 하 여 자세한 [게이트웨이 문제 해결-Azure 포털](network-watcher-troubleshoot-manage-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94dfc-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
