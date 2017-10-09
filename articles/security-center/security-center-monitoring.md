---
title: "Azure 보안 센터에서 aaaSecurity 모니터링 | Microsoft Docs"
description: "이 문서에서는 tooget 모니터링 기능에 Azure 보안 센터를 시작 합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a><span data-ttu-id="c5c5b-103">Azure Security Center에서 보안 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="c5c5b-103">Security health monitoring in Azure Security Center</span></span>
<span data-ttu-id="c5c5b-104">이 문서에서는 hello Azure 보안 센터 toomonitor 준수 정책 사용 하 여 모니터링 기능을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-104">This article helps you use hello monitoring capabilities in Azure Security Center toomonitor compliance with policies.</span></span>

## <a name="what-is-security-health-monitoring"></a><span data-ttu-id="c5c5b-105">보안 상태 모니터링이란?</span><span class="sxs-lookup"><span data-stu-id="c5c5b-105">What is security health monitoring?</span></span>
<span data-ttu-id="c5c5b-106">우리는 종종를 감시 하 고 म toohello 상황 반응할 수 있도록 이벤트 toooccur에 대 한 대기로 모니터링 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-106">We often think of monitoring as watching and waiting for an event toooccur so that we can react toohello situation.</span></span> <span data-ttu-id="c5c5b-107">보안 모니터링 toohaving 조직의 표준 또는 모범 사례를 충족 하지 않는 리소스 tooidentify 시스템을 감사 하는 자동 관리 전략을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-107">Security monitoring refers toohaving a proactive strategy that audits your resources tooidentify systems that do not meet organizational standards or best practices.</span></span>

## <a name="monitoring-security-health"></a><span data-ttu-id="c5c5b-108">보안 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="c5c5b-108">Monitoring security health</span></span>
<span data-ttu-id="c5c5b-109">사용 하도록 설정한 후 [보안 정책](security-center-policies.md) 구독의 리소스에 대 한 보안 센터를 hello 보안 리소스 tooidentify 잠재적인 취약점을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-109">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center analyzes hello security of your resources tooidentify potential vulnerabilities.</span></span> <span data-ttu-id="c5c5b-110">네트워크 구성 정보는 즉시 이용할 수 있지만,</span><span class="sxs-lookup"><span data-stu-id="c5c5b-110">Information about your network configuration is available instantly.</span></span> <span data-ttu-id="c5c5b-111">1 시간 걸릴 수 있습니다 또는 상태 및 운영 체제 구성, 사용 가능한 toobecome 보안 등의 가상 컴퓨터 구성에 대 한 정보에 대 한 추가 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-111">It may take an hour or more for information about virtual machine configuration, such as security update status and operating system configuration, toobecome available.</span></span> <span data-ttu-id="c5c5b-112">Hello에서 모든 문제와 리소스의 hello 보안 상태를 볼 수 있습니다 **방지** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-112">You can view hello security state of your resources and any issues in hello **Prevention** section.</span></span> <span data-ttu-id="c5c5b-113">Hello에도 이러한 문제의 목록을 볼 수 있습니다 **권장 사항을** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-113">You can also view a list of those issues on hello **Recommendations** tile.</span></span>

<span data-ttu-id="c5c5b-114">방법에 대 한 자세한 내용은 tooapply 권장 사항, 읽을 [Azure 보안 센터에서 보안 권장 사항 구현](security-center-recommendations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-114">For more information about how tooapply recommendations, read [Implementing security recommendations in Azure Security Center](security-center-recommendations.md).</span></span>

<span data-ttu-id="c5c5b-115">Hello에서 **방지** 섹션 hello 보안 리소스 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-115">Under hello **Prevention** section, you can monitor hello security state of your resources.</span></span> <span data-ttu-id="c5c5b-116">다음 예제는 hello에서 볼 수 있습니다 (계산, 네트워킹, 저장소 및 데이터 및 응용 프로그램)의 각 리소스의 타일에 있는 식별 된 문제의 hello 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-116">In hello following example, you can see that in each resource's tile (Compute, Networking, Storage & data, and Application) has hello total number of issues that were identified.</span></span>

![리소스 보안 상태 타일](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a><span data-ttu-id="c5c5b-118">모니터 계산</span><span class="sxs-lookup"><span data-stu-id="c5c5b-118">Monitor compute</span></span>
<span data-ttu-id="c5c5b-119">클릭할 때 **계산** 타일을 hello **계산** 열리는 블레이드 세 개의 탭을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-119">When you click **Compute** tile, hello **Compute** blade that opens shows three tabs:</span></span>

- <span data-ttu-id="c5c5b-120">**개요**: 모니터링 및 가상 컴퓨터 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-120">**Overview**: monitoring and virtual machine recommendations.</span></span>
- <span data-ttu-id="c5c5b-121">**Virtual Machines**: 모든 가상 컴퓨터와 현재 보안 상태를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-121">**Virtual Machines**: list all all virtual machines and its current security state.</span></span>
- <span data-ttu-id="c5c5b-122">**Cloud Services**: Security Center에서 모니터링하는 모든 웹 및 작업자 역할의 목록을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-122">**Cloud Services**: list of all web and worker roles monitored by Security Center.</span></span>

![가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

<span data-ttu-id="c5c5b-124">각 탭에서 섹션이 여러 개 있을 수 있으며 각 섹션에서 개별 옵션 toosee를 선택할 수 있습니다 hello에 대 한 자세한 내용은 단계 tooaddress 특정 문제를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-124">In each tab you can have multiple sections, and in each section, you can select an individual option toosee more details about hello recommended steps tooaddress that particular issue.</span></span> 

#### <a name="monitoring-recommendations"></a><span data-ttu-id="c5c5b-125">권장 사항 모니터링</span><span class="sxs-lookup"><span data-stu-id="c5c5b-125">Monitoring recommendations</span></span>
<span data-ttu-id="c5c5b-126">이 섹션에서는 hello 데이터 수집 및 현재 상태에 대 한 초기화 된 가상 컴퓨터의 총 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-126">This section shows hello total number of virtual machines that were initialized for data collection and their current statuses.</span></span> <span data-ttu-id="c5c5b-127">모든 가상 컴퓨터, 데이터 컬렉션을 초기화 한 다음 준비 tooreceive 보안 센터 보안 정책이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-127">After all virtual machines have data collection initialized, they will be ready tooreceive Security Center security policies.</span></span> <span data-ttu-id="c5c5b-128">이 항목을 클릭할 때 hello **VM 에이전트가 없거나 응답 하지 않는** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-128">When you click this entry, hello **VM Agent is missing or not responding** blade opens.</span></span> 

![가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a><span data-ttu-id="c5c5b-130">가상 컴퓨터 권장 사항</span><span class="sxs-lookup"><span data-stu-id="c5c5b-130">Virtual machine recommendations</span></span>
<span data-ttu-id="c5c5b-131">이 섹션에는 Azure Security Center에서 모니터링하는 [각 VM에 대한 권장 사항](security-center-virtual-machine-recommendations.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-131">This section has a set of [recommendations for each virtual machine](security-center-virtual-machine-recommendations.md) that Azure Security Center monitors.</span></span> <span data-ttu-id="c5c5b-132">hello 첫 번째 열에는 hello 권장 사항을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-132">hello first column lists hello recommendation.</span></span> <span data-ttu-id="c5c5b-133">hello 두 번째 열 hello 해당 권장 구성의 영향을 받는 가상 컴퓨터의 총 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-133">hello second column shows hello total number of virtual machines that are affected by that recommendation.</span></span> <span data-ttu-id="c5c5b-134">hello 세 번째 열 hello 스크린 샷 다음에 설명 된 대로 hello 문제의 hello 심각도 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-134">hello third column shows hello severity of hello issue as illustrated in hello following screenshot.</span></span>

![가상 컴퓨터 권장 사항](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> <span data-ttu-id="c5c5b-136">Hello에 공용 끝점을 하나 이상 가상 컴퓨터만 표시 되어 **네트워킹 상태** hello 블레이드 **네트워크 토폴로지** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-136">Only virtual machines that have at least one public endpoint are shown in hello **Networking Health** blade in hello **Network topology** list.</span></span>
>
>

<span data-ttu-id="c5c5b-137">각 권장 사항에는 클릭하면 수행되는 작업 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-137">Each recommendation has a set of actions that you can perform after you click it.</span></span> <span data-ttu-id="c5c5b-138">예를 들어, 클릭 하면 **누락 된 시스템 업데이트**, hello **누락 된 시스템 업데이트** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-138">For example, if you click **Missing system updates**, hello **Missing system updates** blade opens.</span></span> <span data-ttu-id="c5c5b-139">Hello 고 가상 컴퓨터를 패치 누락 된 hello 다음과 같이 hello 누락 된 업데이트의 심각도 hello 나열 스크린 샷 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-139">It lists hello virtual machines that are missing patches and hello severity of hello missing update as shown in hello following screenshot.</span></span>

![가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

<span data-ttu-id="c5c5b-141">hello **누락 된 시스템 업데이트** 블레이드 hello 다음 정보로 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-141">hello **Missing system updates** blade shows a table with hello following information:</span></span>

* <span data-ttu-id="c5c5b-142">**가상 컴퓨터**: 업데이트가 설치 되어 있지 hello 가상 컴퓨터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-142">**VIRTUAL MACHINE**: hello name of hello virtual machine that is missing updates.</span></span>
* <span data-ttu-id="c5c5b-143">**시스템 업데이트**: hello 누락 된 시스템 업데이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-143">**SYSTEM UPDATES**: hello number of system updates that are missing.</span></span>
* <span data-ttu-id="c5c5b-144">**마지막 검사 시간**: hello 시간 보안 센터 마지막 업데이트에 대 한 hello 가상 컴퓨터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-144">**LAST SCAN TIME**: hello time that Security Center last scanned hello virtual machine for updates.</span></span>
* <span data-ttu-id="c5c5b-145">**상태**: hello hello 권장 구성의 현재 상태:</span><span class="sxs-lookup"><span data-stu-id="c5c5b-145">**STATE**: hello current state of hello recommendation:</span></span>
  * <span data-ttu-id="c5c5b-146">**열기**: hello 권장 사항 해결 하지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-146">**Open**: hello recommendation has not been addressed yet.</span></span>
  * <span data-ttu-id="c5c5b-147">**진행 중인**: hello 권장 구성이 현재 적용 된 toothose 리소스를 생성할 수 있으며 사용자가 아무 작업도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-147">**In Progress**: hello recommendation is currently being applied toothose resources, and no action is required by you.</span></span>
  * <span data-ttu-id="c5c5b-148">**해결**: hello 권장 사항이 이미 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-148">**Resolved**: hello recommendation was already finished.</span></span> <span data-ttu-id="c5c5b-149">(Hello 문제를 해결 hello 항목이 흐리게 표시 됩니다).</span><span class="sxs-lookup"><span data-stu-id="c5c5b-149">(When hello issue has been resolved, hello entry is dimmed).</span></span>
* <span data-ttu-id="c5c5b-150">**심각도**: hello 심각도입니다. 해당 특정 권장 사항 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-150">**SEVERITY**: Describes hello severity of that particular recommendation:</span></span>
  * <span data-ttu-id="c5c5b-151">**높음**: 중요한 리소스(응용 프로그램, VM 또는 네트워크 보안 그룹)에 취약점이 있으며 주의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-151">**High**: A vulnerability exists with a meaningful resource (application, virtual machine, or network security group) and requires attention.</span></span>
  * <span data-ttu-id="c5c5b-152">**보통**: 단순한 또는 추가 단계는 필요한 toocomplete 프로세스 또는 문제를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-152">**Medium**: Non-critical or additional steps are required toocomplete a process or eliminate a vulnerability.</span></span>
  * <span data-ttu-id="c5c5b-153">**낮음**: 취약점을 해결해야 하지만 즉각적인 주의가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-153">**Low**: A vulnerability should be addressed but does not require immediate attention.</span></span> <span data-ttu-id="c5c5b-154">(기본적으로 낮은 권장 사항 표시 되지 않은, 하지만 tooview 하려는 경우 낮은 권장 사항에 필터링 할 수 있습니다 이러한.)</span><span class="sxs-lookup"><span data-stu-id="c5c5b-154">(By default, low recommendations are not presented, but you can filter on low recommendations if you want tooview them.)</span></span>

<span data-ttu-id="c5c5b-155">tooview hello 권장 사항 세부 정보에는 hello 가상 컴퓨터의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-155">tooview hello recommendation details, click hello name of hello virtual machine.</span></span> <span data-ttu-id="c5c5b-156">Hello 스크린 샷 다음 그림과 같이 hello 업데이트 목록이 해당 가상 컴퓨터는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-156">A new blade for that virtual machine opens with hello list of updates as shown in hello following screenshot.</span></span>

![특정 가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> <span data-ttu-id="c5c5b-158">hello 보안 권장 사항 여기는 hello의 것과 동일한 hello **권장 사항을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-158">hello security recommendations here are hello same as those in hello **Recommendations** blade.</span></span> <span data-ttu-id="c5c5b-159">Hello 참조 [Azure 보안 센터에서 보안 권장 사항 구현](security-center-recommendations.md) 방법에 대 한 자세한 내용은 문서 tooresolve 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-159">See hello [Implementing security recommendations in Azure Security Center](security-center-recommendations.md) article for more information about how tooresolve recommendations.</span></span> <span data-ttu-id="c5c5b-160">뿐만 아니라 hello에서 사용할 수 있는 모든 리소스를 뿐만 아니라 가상 컴퓨터에 적용 됩니다 **리소스 상태** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-160">This is applicable not only for virtual machines but also for all resources that are available in hello **Resource Health** tile.</span></span>
>
>

#### <a name="virtual-machines-section"></a><span data-ttu-id="c5c5b-161">가상 컴퓨터 섹션</span><span class="sxs-lookup"><span data-stu-id="c5c5b-161">Virtual machines section</span></span>
<span data-ttu-id="c5c5b-162">hello 가상 컴퓨터 섹션에서는 모든 가상 컴퓨터 및 권장 사항에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-162">hello virtual machines section gives you an overview of all virtual machines and recommendations.</span></span> <span data-ttu-id="c5c5b-163">각 열 hello 스크린 샷 뒤에 표시 된 대로의 권장 구성 하나의 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-163">Each column represents one set of recommendations as shown in hello following screenshot:</span></span>

![모든 가상 컴퓨터 및 권장 사항 개요](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

<span data-ttu-id="c5c5b-165">각 권장 사항 사용 하면 아래에 표시 되는 hello 아이콘 tooquickly 하면 주의가 필요한 및 유형 권장 구성의 hello는 hello 가상 컴퓨터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-165">hello icon that appears under each recommendation helps you tooquickly identify hello virtual machines that need attention and hello type of recommendation.</span></span>

<span data-ttu-id="c5c5b-166">Hello 이전 예제에서는 하나의 가상 컴퓨터에는 끝점 보호와 관련 된 중요 한 권장 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-166">In hello previous example, one virtual machine has a critical recommendation regarding endpoint protection.</span></span> <span data-ttu-id="c5c5b-167">tooget hello 가상 컴퓨터에 대 한 자세한 내용은 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-167">tooget more information about hello virtual machine, click it.</span></span> <span data-ttu-id="c5c5b-168">열리는 새 블레이드의 스크린 샷 다음 hello와 같이이 가상 컴퓨터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-168">A new blade that opens represents this virtual machine as shown in hello following screenshot.</span></span>

![가상 컴퓨터 보안 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

<span data-ttu-id="c5c5b-170">이 블레이드는 hello 가상 컴퓨터에 대 한 hello 보안 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-170">This blade has hello security details for hello virtual machine.</span></span> <span data-ttu-id="c5c5b-171">이 블레이드의 hello 아래쪽 hello 권장 작업 및 각 문제의 hello 심각도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-171">At hello bottom of this blade, you can see hello recommended action and hello severity of each issue.</span></span>

#### <a name="cloud-services-section"></a><span data-ttu-id="c5c5b-172">클라우드 서비스 섹션</span><span class="sxs-lookup"><span data-stu-id="c5c5b-172">Cloud services section</span></span>
<span data-ttu-id="c5c5b-173">클라우드 서비스에 대 한 권장 사항은 hello 운영 체제 버전은 오래 된 hello 스크린 샷 뒤에 표시 된 대로 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-173">For cloud services, a recommendation is created when hello operating system version is out of date as shown in hello following screenshot:</span></span>

![클라우드 서비스 상태](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

<span data-ttu-id="c5c5b-175">권장 사항 (하지 hello에 대 한 경우 hello 앞의 예제) 권한이 시나리오에서는 hello 권장 tooupdate hello 운영 체제 버전의 hello 단계 toofollow 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-175">In a scenario where you do have recommendation (which is not hello case for hello previous example), you need toofollow hello steps in hello recommendation tooupdate hello operating system version.</span></span> <span data-ttu-id="c5c5b-176">업데이트를 사용할 수 있는 경고 해야 합니다 (빨간색-주황색 했는지에 따라 또는 hello 문제의 hello 심각도).</span><span class="sxs-lookup"><span data-stu-id="c5c5b-176">When an update is available, you will have an alert (red or orange - depends on hello severity of hello issue).</span></span> <span data-ttu-id="c5c5b-177">WebRole1 (Windows Server 웹 응용 프로그램을 자동으로 배포 tooIIS로 실행) 또는 (Windows Server 웹 응용 프로그램을 자동으로 배포 tooIIS로 실행) WorkerRole1 hello 행에서이 경고를 클릭 하면이 대 한 자세한 정보는 새 블레이드가 열립니다. hello 스크린 샷 뒤에 표시 된 대로 권장 사항:</span><span class="sxs-lookup"><span data-stu-id="c5c5b-177">When you click on this alert in hello WebRole1 (runs Windows Server with your web app automatically deployed tooIIS) or WorkerRole1 (runs Windows Server with your web app automatically deployed tooIIS) rows, a new blade opens with more details about this recommendation as shown in hello following screenshot:</span></span>

![클라우드 서비스 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

<span data-ttu-id="c5c5b-179">이 권장 구성에 대 한 규정 설명을 toosee 클릭 **업데이트 OS 버전** hello에서 **설명** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-179">toosee a more prescriptive explanation about this recommendation, click **Update OS version** under hello **DESCRIPTION** column.</span></span> <span data-ttu-id="c5c5b-180">hello **업데이트 OS 버전 (미리 보기)** 자세한 정보와 함께 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-180">hello **Update OS version (Preview)** blade opens with more details.</span></span>

![클라우드 서비스 권장 사항](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a><span data-ttu-id="c5c5b-182">가상 네트워크 모니터링</span><span class="sxs-lookup"><span data-stu-id="c5c5b-182">Monitor virtual networks</span></span>
<span data-ttu-id="c5c5b-183">클릭할 때 **네트워킹** 타일을 hello **네트워킹** hello 스크린 샷 뒤에 표시 된 대로 자세한 정보 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-183">When you click **Networking** tile, hello **Networking** blade opens with more details as shown in hello following screenshot:</span></span>

![네트워킹 블레이드](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a><span data-ttu-id="c5c5b-185">네트워킹 권장 사항</span><span class="sxs-lookup"><span data-stu-id="c5c5b-185">Networking recommendations</span></span>
<span data-ttu-id="c5c5b-186">가상 컴퓨터의 리소스 상태 정보를 hello, 처럼이 블레이드 hello 아래쪽에 요약 된 hello 블레이드 맨 hello 및 모니터링 되는 네트워크의 목록이 문제 목록이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-186">Like hello virtual machine's resource health information, this blade provides a summarized list of issues at hello top of hello blade and a list of monitored networks on hello bottom.</span></span>

<span data-ttu-id="c5c5b-187">상태 분류 섹션 네트워킹 hello 잠재적인 보안 문제를 나열 하 고 제공 [권장 사항을](security-center-network-recommendations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-187">hello networking status breakdown section lists potential security issues and offers [recommendations](security-center-network-recommendations.md).</span></span> <span data-ttu-id="c5c5b-188">가능한 문제는 다음을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-188">Possible issues can include:</span></span>

* <span data-ttu-id="c5c5b-189">차세대 방화벽(NGFW)이 설치되지 않음</span><span class="sxs-lookup"><span data-stu-id="c5c5b-189">Next-Generation Firewall (NGFW) not installed</span></span>
* <span data-ttu-id="c5c5b-190">서브넷에서 NSG(네트워크 보안 그룹) 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c5c5b-190">Network security groups on subnets not enabled</span></span>
* <span data-ttu-id="c5c5b-191">VM에서 NSG 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c5c5b-191">Network security groups on virtual machines not enabled</span></span>
* <span data-ttu-id="c5c5b-192">공용 외부 끝점을 통한 외부 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="c5c5b-192">Restrict external access through public external endpoint</span></span>
* <span data-ttu-id="c5c5b-193">정상 인터넷 연결 끝점</span><span class="sxs-lookup"><span data-stu-id="c5c5b-193">Healthy Internet facing endpoints</span></span>

<span data-ttu-id="c5c5b-194">권장 사항을 클릭 hello 다음 예제와 같이 hello 권장 사항에 대 한 자세한 정보는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-194">When you click a recommendation, a new blade opens with more details about hello recommendation as shown in hello following example.</span></span>

![Hello 네트워킹 블레이드에서 권장 사항에 대 한 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

<span data-ttu-id="c5c5b-196">이 예제에서는 hello **누락 된 네트워크 보안 그룹 구성 서브넷에 대 한** 블레이드는 서브넷 목록 및 누락 된 가상 컴퓨터를 네트워크 보안 그룹을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-196">In this example, hello **Configure Missing Network Security Groups for Subnets** blade has a list of subnets and virtual machines that are missing network security group protection.</span></span> <span data-ttu-id="c5c5b-197">Hello 서브넷 toowhich tooapply hello 네트워크 보안 그룹을 클릭 하면 다른 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-197">If you click hello subnet toowhich you want tooapply hello network security group, another blade opens.</span></span>

<span data-ttu-id="c5c5b-198">Hello에 **네트워크 보안 그룹 선택** 블레이드에서 hello 서브넷에 대 한 hello 가장 적합 한 네트워크 보안 그룹 선택 하거나 새 네트워크 보안 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-198">In hello **Choose network security group** blade, you can select hello most appropriate network security group for hello subnet, or you can create a new network security group.</span></span>

#### <a name="internet-facing-endpoints-section"></a><span data-ttu-id="c5c5b-199">인터넷 연결 끝점 섹션</span><span class="sxs-lookup"><span data-stu-id="c5c5b-199">Internet facing endpoints section</span></span>
<span data-ttu-id="c5c5b-200">Hello에 **인터넷 연결 끝점** 섹션은 현재는 인터넷 끝점 및 서버 인스턴스의 현재 상태를 연결로 구성 된 hello 가상 컴퓨터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-200">In hello **Internet facing endpoints** section, you can see hello virtual machines that are currently configured with an Internet facing endpoint and its current status.</span></span>

![인터넷 연결 끝점으로 구성된 가상 컴퓨터 및 상태](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

<span data-ttu-id="c5c5b-202">이 테이블 hello 끝점을 나타내는 이름 hello 가상 컴퓨터를 hello 인터넷 연결 IP 주소 및 hello 네트워크 보안 그룹의 현재 심각도 상태 hello 않았으며 NGFW hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-202">This table has hello endpoint name that represents hello virtual machine, hello Internet facing IP address, and hello current severity status of hello network security group and hello NGFW.</span></span> <span data-ttu-id="c5c5b-203">hello 테이블 심각도 별로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-203">hello table is sorted by severity:</span></span>

* <span data-ttu-id="c5c5b-204">빨간색(최우선): 높은 우선 순위이며 즉시 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-204">Red (on top): High priority and should be addressed immediately</span></span>
* <span data-ttu-id="c5c5b-205">주황색: 보통 우선 순위이며 가능한 한 빨리 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-205">Orange: Medium priority and should be addressed as soon as possible</span></span>
* <span data-ttu-id="c5c5b-206">녹색(마지막): 정상 상태</span><span class="sxs-lookup"><span data-stu-id="c5c5b-206">Green (last one): Healthy state</span></span>

#### <a name="networking-topology-section"></a><span data-ttu-id="c5c5b-207">네트워킹 토폴로지 섹션</span><span class="sxs-lookup"><span data-stu-id="c5c5b-207">Networking topology section</span></span>
<span data-ttu-id="c5c5b-208">hello **네트워킹 토폴로지** hello 스크린 샷 뒤에 표시 된 대로 섹션에 hello 리소스의 계층적 보기:</span><span class="sxs-lookup"><span data-stu-id="c5c5b-208">hello **Networking topology** section has a hierarchical view of hello resources as shown in hello following screenshot:</span></span>

![네트워킹 토폴로지 섹션의 계층적 리소스 보기](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

<span data-ttu-id="c5c5b-210">다음과 같이 심각도 별로 테이블이 정렬됩니다(VM 및 서브넷).</span><span class="sxs-lookup"><span data-stu-id="c5c5b-210">This table is sorted (virtual machines and subnets) by severity:</span></span>

* <span data-ttu-id="c5c5b-211">빨간색(최우선): 높은 우선 순위이며 즉시 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-211">Red (on top): High priority and should be addressed immediately</span></span>
* <span data-ttu-id="c5c5b-212">주황색: 보통 우선 순위이며 가능한 한 빨리 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-212">Orange: Medium priority and should be addressed as soon as possible</span></span>
* <span data-ttu-id="c5c5b-213">녹색(마지막): 정상 상태</span><span class="sxs-lookup"><span data-stu-id="c5c5b-213">Green (last one): Healthy state</span></span>

<span data-ttu-id="c5c5b-214">Hello 첫 번째 수준에는이 토폴로지 뷰에서 [가상 네트워크](../virtual-network/virtual-networks-overview.md), [가상 네트워크 게이트웨이](/vpn-gateway/vpn-gateway-site-to-site-create.md), 및 [가상 네트워크 (클래식)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-214">In this topology view, hello first level has [virtual networks](../virtual-network/virtual-networks-overview.md), [virtual network gateways](/vpn-gateway/vpn-gateway-site-to-site-create.md), and [virtual networks (classic)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> <span data-ttu-id="c5c5b-215">두 번째 수준 hello 서브넷이 많고 hello 세 번째 수준 toothose 서브넷에 속하는 hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-215">hello second level has subnets, and hello third level has hello virtual machines that belong toothose subnets.</span></span> <span data-ttu-id="c5c5b-216">hello 오른쪽 열에 다음 예제는 hello와 같이 hello 해당 리소스에 대 한 hello 네트워크 보안 그룹의 현재 상태:</span><span class="sxs-lookup"><span data-stu-id="c5c5b-216">hello right column has hello current status of hello network security group for those resources, as shown in hello following example:</span></span>

![네트워킹 토폴로지 섹션에 hello 네트워크 보안 그룹의 상태](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

<span data-ttu-id="c5c5b-218">hello이 블레이드의 아래 부분에 hello 권장 사항이 비슷한이 가상 컴퓨터에 대 한 toowhat 이전에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-218">hello bottom part of this blade has hello recommendations for this virtual machine, which is similar toowhat is described previously.</span></span> <span data-ttu-id="c5c5b-219">자세한 권장 사항을 toolearn를 클릭 하거나 필요한 hello 보안 제어 또는 구성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-219">You can click a recommendation toolearn more or apply hello needed security control or configuration.</span></span>

### <a name="monitor-storage--data"></a><span data-ttu-id="c5c5b-220">저장소 및 데이터 모니터링</span><span class="sxs-lookup"><span data-stu-id="c5c5b-220">Monitor Storage & data</span></span>

<span data-ttu-id="c5c5b-221">클릭할 때 **데이터 및 저장소** hello에 **방지** 섹션 hello **데이터 리소스** SQL 및 저장소에 대 한 권장 사항과 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-221">When you click **Storage & data** in hello **Prevention** section, hello **Data Resources** blade opens with recommendations for SQL and Storage.</span></span> <span data-ttu-id="c5c5b-222">또한 [권장 사항을](security-center-sql-service-recommendations.md) hello 데이터베이스의 hello 일반 성능 상태에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-222">It also has [recommendations](security-center-sql-service-recommendations.md) for hello general health state of hello database.</span></span> <span data-ttu-id="c5c5b-223">저장소 암호화에 대한 자세한 내용은 [Azure Security Center에서 Azure Storage 계정에 대한 암호화 사용](security-center-enable-encryption-for-storage-account.md)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-223">For more information about storage encryption, read [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md).</span></span>

![데이터 리소스](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

<span data-ttu-id="c5c5b-225">아래 **SQL 권장 사항**, 모든 권장 사항을 클릭 수 및 get 대 한 자세한 내용은 추가 작업 tooresolve 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-225">Under **SQL Recommendations**, You can click any recommendation and get more details about further action tooresolve an issue.</span></span> <span data-ttu-id="c5c5b-226">hello 다음 예제에서는 hello의 hello 확장 **SQL 데이터베이스에서 데이터베이스 감사 및 위협 검색** 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-226">hello following example shows hello expansion of hello **Database Auditing & Threat detection on SQL databases** recommendation.</span></span>

![SQL 권장 사항에 대한 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

<span data-ttu-id="c5c5b-228">hello **SQL 데이터베이스에서 감사를 사용 하도록 설정 및 위협 검색** 블레이드는 hello 다음 정보:</span><span class="sxs-lookup"><span data-stu-id="c5c5b-228">hello **Enable Auditing & Threat detection on SQL databases** blade has hello following information:</span></span>

* <span data-ttu-id="c5c5b-229">SQL 데이터베이스의 목록</span><span class="sxs-lookup"><span data-stu-id="c5c5b-229">A list of SQL databases</span></span>
* <span data-ttu-id="c5c5b-230">있는 hello 서버</span><span class="sxs-lookup"><span data-stu-id="c5c5b-230">hello server on which they are located</span></span>
* <span data-ttu-id="c5c5b-231">이 설정은 hello 서버에서 상속 된 여부 또는이 데이터베이스에 고유한 경우에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="c5c5b-231">Information about whether this setting was inherited from hello server or if it is unique in this database</span></span>
* <span data-ttu-id="c5c5b-232">hello 현재 상태</span><span class="sxs-lookup"><span data-stu-id="c5c5b-232">hello current state</span></span>
* <span data-ttu-id="c5c5b-233">hello 문제의 hello 심각도</span><span class="sxs-lookup"><span data-stu-id="c5c5b-233">hello severity of hello issue</span></span>

<span data-ttu-id="c5c5b-234">이 권장 사항은 hello 데이터베이스 tooaddress을 클릭할 때 hello **감사 및 위협 검색** hello 다음 화면에에서 표시 된 대로 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-234">When you click hello database tooaddress this recommendation, hello **Auditing & Threat detection** blade opens as shown in hello following screen.</span></span>

![감사 및 위협 감지 블레이드](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

<span data-ttu-id="c5c5b-236">tooenable 감사를 위해 선택 **ON** hello에서 **감사** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-236">tooenable auditing, select **ON** under hello **Auditing** option.</span></span>

### <a name="monitor-applications"></a><span data-ttu-id="c5c5b-237">응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="c5c5b-237">Monitor applications</span></span>

<span data-ttu-id="c5c5b-238">Azure 작업에 응용 프로그램에 있는 경우 [(Azure 리소스 관리자를 통해 만든) 가상 컴퓨터](../azure-resource-manager/resource-manager-deployment-model.md) 보안 센터 노출 된 웹 포트 (TCP 포트 80 및 443)를 함께 이러한 tooidentify 잠재적인 보안 문제를 모니터링할 수 있습니다 및 해결 단계는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-238">If your Azure workload has applications located in [virtual machines (created through Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) with exposed web ports (TCP ports 80 and 443), Security Center can monitor those tooidentify potential security issues and recommend remediation steps.</span></span> <span data-ttu-id="c5c5b-239">Hello를 클릭할 때 **응용 프로그램** 타일을 hello **응용 프로그램** 일련의 hello에 대 한 권장 사항 블레이드에서 열립니다 **응용 프로그램 권장 사항을** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-239">When you click hello **Applications** tile, hello **Applications** blade opens with a series of recommendations in hello **Application recommendations** section.</span></span> <span data-ttu-id="c5c5b-240">또한 hello 스크린 샷 뒤에 표시 된 대로 각 호스트/가상 IP hello 응용 프로그램 작업 분석을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-240">It also shows hello application breakdown per host/virtual IP as shown in hello following screenshot.</span></span>

![응용프로그램 보안 상태](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

<span data-ttu-id="c5c5b-242">하면 않은와 hello 기타 권장 사항, 하는 것 처럼 클릭할 수 있는 권장 사항을 toosee hello 문제에 대 한 자세한 내용은 방법과 tooremediate 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-242">Just like you did with hello other recommendations, you can click a recommendation toosee more details about hello issue and how tooremediate.</span></span> <span data-ttu-id="c5c5b-243">hello 다음 그림에에서 표시 된 hello 예는 응용 프로그램 보안 되지 않은 웹 응용 프로그램으로 확인 됨입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-243">hello example shown in hello following figure is an application that was identified as an unsecure web application.</span></span> <span data-ttu-id="c5c5b-244">보안 고려 되었지만 hello 응용 프로그램을 선택 하는 경우 hello 다음 옵션을 사용할 수 있는 다른 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-244">When you select hello application that was considered not secure, another blade opens with hello following option available:</span></span>

![안전하지 않은 응용 프로그램에 대한 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

<span data-ttu-id="c5c5b-246">이 블레이드에는 해당 응용 프로그램에 대한 모든 권장 사항을 보여 주는 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-246">This blade will have a list of all recommendations for this application.</span></span> <span data-ttu-id="c5c5b-247">Hello를 클릭할 때 **추가 웹 응용 프로그램 방화벽** 권장 사항, hello **추가 웹 응용 프로그램 방화벽** 블레이드 옵션이 열립니다 tooinstall 있습니다에 대 한 웹 응용 프로그램 방화벽 (WAF)으로 파트너에서 다음 스크린 샷 hello에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-247">When you click hello **Add a web application firewall** recommendation, hello **Add a Web Application Firewall** blade opens with options for you tooinstall a web application firewall (WAF) from a partner as shown in hello following screenshot.</span></span>

![웹 응용 프로그램 방화벽 추가 대화 상자](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a><span data-ttu-id="c5c5b-249">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c5c5b-249">See also</span></span>
<span data-ttu-id="c5c5b-250">이 문서에서는 방법에 대해 배웠습니다 toouse Azure 보안 센터의 기능을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-250">In this article, you learned how toouse monitoring capabilities in Azure Security Center.</span></span> <span data-ttu-id="c5c5b-251">Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-251">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="c5c5b-252">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md): 자세한 방법을 Azure 보안 센터의 tooconfigure 보안 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-252">[Setting security policies in Azure Security Center](security-center-policies.md): Learn how tooconfigure security settings in Azure Security Center.</span></span>
* <span data-ttu-id="c5c5b-253">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md): 자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-253">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md): Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c5c5b-254">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md): toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-254">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md): Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c5c5b-255">[Azure 보안 센터 FAQ](security-center-faq.md): 찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-255">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c5c5b-256">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c5b-256">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>
