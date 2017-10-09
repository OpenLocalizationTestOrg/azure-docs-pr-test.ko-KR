---
title: "Azure의 aaaAzure 보안 센터 및 Linux 가상 컴퓨터 | Microsoft Docs"
description: "Azure Security Center를 사용하여 Azure Linux 가상 컴퓨터의 보안을 유지하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="291b5-103">Azure Security Center를 사용하여 가상 컴퓨터 보안 모니터링</span><span class="sxs-lookup"><span data-stu-id="291b5-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="291b5-104">Azure Security Center를 사용하면 Azure 리소스 보안 사례에 대한 가시성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="291b5-105">Security Center는 통합 보안 모니터링 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="291b5-106">다른 방법으로는 눈에 띄지 않을 수 있는 위협을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="291b5-107">이 자습서에서는 Azure Security Center에 대해 알아보고 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="291b5-108">데이터 수집 설정</span><span class="sxs-lookup"><span data-stu-id="291b5-108">Set up data collection</span></span>
> * <span data-ttu-id="291b5-109">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="291b5-109">Set up security policies</span></span>
> * <span data-ttu-id="291b5-110">구성 상태 문제 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="291b5-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="291b5-111">검색된 위협 검토</span><span class="sxs-lookup"><span data-stu-id="291b5-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="291b5-112">Security Center 개요</span><span class="sxs-lookup"><span data-stu-id="291b5-112">Security Center overview</span></span>

<span data-ttu-id="291b5-113">Security Center는 잠재적인 VM(가상 컴퓨터) 구성 문제 및 대상이 되는 보안 위협을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="291b5-114">여기에는 네트워크 보안 그룹이 누락된 VM, 암호화되지 않은 디스크 및 RDP(원격 데스크톱 프로토콜) 무차별 암호 대입 공격이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="291b5-115">hello 정보는 읽기 쉬운 그래프의 hello 보안 센터 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="291b5-116">tooaccess hello hello hello 메뉴에서 Azure 포털의에서 보안 센터 대시보드에서 **보안 센터**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="291b5-117">Hello 대시보드에서 Azure 환경의 hello 보안 상태를 볼 현재 권장 사항 수를 찾을 고 hello 위협 경고의 현재 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="291b5-118">자세한 내용은 각 수준 높은 toosee를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-118">You can expand each high-level chart toosee more detail.</span></span>

![Security Center 대시보드](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="291b5-120">보안 센터가 발견 되는 문제에 대 한 데이터 검색 tooprovide 권장 사항을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="291b5-121">예를 들어 연결된 네트워크 보안 그룹 없이 VM을 배포한 경우 Security Center에서 수행할 수 있는 재구성 단계와 함께 권장 사항을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="291b5-122">보안 센터의 hello 컨텍스트를 벗어나지 않고 자동화 된 업데이트 관리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![권장 사항](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="291b5-124">데이터 수집 설정</span><span class="sxs-lookup"><span data-stu-id="291b5-124">Set up data collection</span></span>

<span data-ttu-id="291b5-125">VM 보안 구성으로 파악할 수 있습니다, 전에 tooset 보안 센터 데이터 컬렉션을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="291b5-126">Azure 저장소 계정 toohold 수집 된 데이터를 만들고 데이터 컬렉션을 켠 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="291b5-127">Hello 보안 센터 대시보드에서 **보안 정책**, 한 다음 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="291b5-128">**데이터 수집**에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="291b5-129">저장소 계정 toocreate 선택 **저장소 계정을 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="291b5-130">그런 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="291b5-131">Hello에 **보안 정책** 블레이드를 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="291b5-132">hello 보안 센터 데이터 수집 에이전트는 다음 모든 Vm에 설치 하 고 데이터 수집을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="291b5-133">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="291b5-133">Set up a security policy</span></span>

<span data-ttu-id="291b5-134">보안 정책은 사용 되는 toodefine hello 항목을 보안 센터 데이터를 수집 하 고 필요한 사항을 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="291b5-135">Azure 리소스의 다양 한 보안 정책을 toodifferent 집합을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="291b5-136">기본적으로 Azure 리소스가 모든 정책 항목에 대해 평가되지만, 모든 Azure 리소스 또는 리소스 그룹에 대해 개별 정책 항목을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="291b5-137">Azure Security Center 보안 정책에 대한 자세한 내용은 [Azure Security Center에서 보안 정책 설정](../../security-center/security-center-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="291b5-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="291b5-138">모든 Azure 리소스에 대 한 보안 정책을 tooset:</span><span class="sxs-lookup"><span data-stu-id="291b5-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="291b5-139">Hello 보안 센터 대시보드에서 선택 **보안 정책**, 한 다음 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="291b5-140">**방지 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="291b5-141">켜기 또는 Azure 리소스 tooapply tooall 정책 항목을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="291b5-142">설정 선택 작업을 완료했으면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="291b5-143">Hello에 **보안 정책** 블레이드를 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="291b5-144">특정 리소스 그룹에 대 한 정책을 tooset:</span><span class="sxs-lookup"><span data-stu-id="291b5-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="291b5-145">Hello 보안 센터 대시보드에서 선택 **보안 정책**, 한 다음 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="291b5-146">**방지 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="291b5-147">켜기 또는 원하는 tooapply toohello 리소스 그룹 정책 항목을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="291b5-148">**상속**에서 **고유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="291b5-149">설정 선택 작업을 완료했으면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="291b5-150">Hello에 **보안 정책** 블레이드를 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="291b5-151">또한 이 페이지에서 특정 리소스 그룹에 대한 데이터 수집도 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="291b5-152">다음 예제는 hello, 명명 된 리소스 그룹에 대 한 고유한 정책을 만든 후 *myResoureGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="291b5-153">이 정책에서는 디스크 암호화 및 웹 응용 프로그램 방화벽 권장 사항이 모두 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![고유 정책](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="291b5-155">VM 구성 상태 보기</span><span class="sxs-lookup"><span data-stu-id="291b5-155">View VM configuration health</span></span>

<span data-ttu-id="291b5-156">데이터 수집 설정 되었으며 보안 정책을 설정, 보안 센터 tooprovide 알림 및 권장 사항을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="291b5-157">Vm이 배포 된 대로 hello 데이터 컬렉션 에이전트가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="291b5-158">보안 센터 hello에 대 한 데이터 채운 다음 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="291b5-159">VM 구성 상태에 대한 자세한 내용은 [Security Center에서 VM 보호](../../security-center/security-center-virtual-machine-recommendations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="291b5-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="291b5-160">데이터 수집 되 면 각 VM 및 관련된 Azure 리소스에 대 한 리소스 상태 hello 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="291b5-161">hello 정보는 읽기 쉬운 차트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="291b5-162">tooview 리소스 상태:</span><span class="sxs-lookup"><span data-stu-id="291b5-162">tooview resource health:</span></span>

1.  <span data-ttu-id="291b5-163">Hello 보안 센터 대시보드에서 **리소스 보안 상태**선택, **계산**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="291b5-164">Hello에 **계산** 블레이드를 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="291b5-165">이 보기에는 모든 Vm에 대 한 hello 구성 상태 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![상태 계산](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="291b5-167">toosee는 VM에 대 한 모든 권장 사항을 hello VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="291b5-168">권장 사항 및 업데이트 관리는 hello이이 자습서의 다음 섹션에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="291b5-169">구성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="291b5-169">Remediate configuration issues</span></span>

<span data-ttu-id="291b5-170">보안 센터 구성 데이터로 toopopulate 시작 된 후 권장 사항은 수행 됨 기반 hello 보안 정책 설정.</span><span class="sxs-lookup"><span data-stu-id="291b5-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="291b5-171">예를 들어, VM으로 설정 된 연결된 네트워크 보안 그룹 없이 권장 하나 toocreate를 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="291b5-172">모든 권장 사항 목록 toosee:</span><span class="sxs-lookup"><span data-stu-id="291b5-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="291b5-173">Hello 보안 센터 대시보드에서 선택 **권장 사항을**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="291b5-174">특정 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-174">Select a specific recommendation.</span></span> <span data-ttu-id="291b5-175">Hello 권장 구성에 적용 되는 대 한 모든 리소스의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="291b5-176">tooapply 권장 사항, 특정 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="291b5-177">수정 단계에 대 한 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="291b5-178">실행 가능한 단계는 보안 센터 대부분의 경우에서 보안 센터를 종료 하지 않고 tooaddress 권장을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="291b5-179">다음 예제는 hello, 보안 센터 무제한 인바운드 규칙이 있는 네트워크 보안 그룹을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="291b5-180">Hello hello 권장 구성 페이지에서 선택할 수 있습니다 **인바운드 규칙 편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="291b5-181">hello 필요한 toomodify hello 규칙 되는 UI에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![권장 사항](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="291b5-183">권장 사항이 해결되면 해결되었다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="291b5-184">검색된 위협 보기</span><span class="sxs-lookup"><span data-stu-id="291b5-184">View detected threats</span></span>

<span data-ttu-id="291b5-185">또한 tooresource 구성 권장 사항, 보안 센터 위협 검색 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="291b5-186">hello 보안 경고 기능은 각 VM, Azure 네트워킹 로그 및 Azure 리소스에 대 한 연결 된 파트너 솔루션 toodetect 보안 위협을에서 수집 된 데이터를 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="291b5-187">Security Center 위협 검색 기능에 대한 자세한 내용은 [Azure Security Center 검색 기능](../../security-center/security-center-detection-capabilities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="291b5-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="291b5-188">hello 보안 경고 기능을 사용 하려면 hello 보안 센터에서 증가 하는 계층 toobe 가격 *무료* 너무*표준*합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="291b5-189">30 일 **무료 평가판** 은 toothis 더 높은 가격 책정 계층을 이동 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="291b5-190">toochange hello 가격 책정 계층:</span><span class="sxs-lookup"><span data-stu-id="291b5-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="291b5-191">Hello 보안 센터 대시보드에서 **보안 정책**, 한 다음 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="291b5-192">**가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="291b5-193">Hello 새 계층을 선택한 다음 선택 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="291b5-194">Hello에 **보안 정책** 블레이드를 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="291b5-195">Hello 가격 책정 계층을 변경 했으면 보안 위협을 감지 되 면 hello 보안 경고 그래프 toopopulate를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![보안 경고](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="291b5-197">경고 tooview 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-197">Select an alert tooview information.</span></span> <span data-ttu-id="291b5-198">예를 들어 hello 위협, hello 검색 시간, 모든 위협 시도에 대 한 설명을 참조할 수 있으며 hello 권장된 업데이트 관리.</span><span class="sxs-lookup"><span data-stu-id="291b5-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="291b5-199">다음 예제는 hello에 RDP 무차별 암호 대입 공격 294 실패 한 RDP 시도와 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="291b5-200">권장되는 해결 방법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-200">A recommended resolution is provided.</span></span>

![RDP 공격](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="291b5-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="291b5-202">Next steps</span></span>
<span data-ttu-id="291b5-203">이 자습서에서는 Azure Security Center를 설정한 다음 Security Center에서 VM을 검토했습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="291b5-204">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="291b5-205">데이터 수집 설정</span><span class="sxs-lookup"><span data-stu-id="291b5-205">Set up data collection</span></span>
> * <span data-ttu-id="291b5-206">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="291b5-206">Set up security policies</span></span>
> * <span data-ttu-id="291b5-207">구성 상태 문제 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="291b5-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="291b5-208">검색된 위협 검토</span><span class="sxs-lookup"><span data-stu-id="291b5-208">Review detected threats</span></span>

<span data-ttu-id="291b5-209">Jenkins, GitHub 및 Docker를 사용 하 여 CI/CD 파이프라인 만들기에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="291b5-209">Advance toohello next tutorial toolearn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="291b5-210">Jenkins, GitHub 및 Docker를 사용하여 CI/CD 인프라 만들기</span><span class="sxs-lookup"><span data-stu-id="291b5-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

