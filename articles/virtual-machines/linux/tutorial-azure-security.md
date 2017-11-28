---
title: "Azure의 Azure Security Center 및 Linux 가상 컴퓨터 | Microsoft Docs"
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
ms.openlocfilehash: 7f76da8cd5f4299c64c6e99d0521829c454d8c6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="f6f78-103">Azure Security Center를 사용하여 가상 컴퓨터 보안 모니터링</span><span class="sxs-lookup"><span data-stu-id="f6f78-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="f6f78-104">Azure Security Center를 사용하면 Azure 리소스 보안 사례에 대한 가시성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="f6f78-105">Security Center는 통합 보안 모니터링 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="f6f78-106">다른 방법으로는 눈에 띄지 않을 수 있는 위협을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="f6f78-107">이 자습서에서는 Azure Security Center에 대해 알아보고 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="f6f78-108">데이터 수집 설정</span><span class="sxs-lookup"><span data-stu-id="f6f78-108">Set up data collection</span></span>
> * <span data-ttu-id="f6f78-109">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="f6f78-109">Set up security policies</span></span>
> * <span data-ttu-id="f6f78-110">구성 상태 문제 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="f6f78-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="f6f78-111">검색된 위협 검토</span><span class="sxs-lookup"><span data-stu-id="f6f78-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="f6f78-112">Security Center 개요</span><span class="sxs-lookup"><span data-stu-id="f6f78-112">Security Center overview</span></span>

<span data-ttu-id="f6f78-113">Security Center는 잠재적인 VM(가상 컴퓨터) 구성 문제 및 대상이 되는 보안 위협을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="f6f78-114">여기에는 네트워크 보안 그룹이 누락된 VM, 암호화되지 않은 디스크 및 RDP(원격 데스크톱 프로토콜) 무차별 암호 대입 공격이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="f6f78-115">이 정보는 Azure Security Center 대시보드에서 읽기 쉬운 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="f6f78-116">Security Center 대시보드에 액세스하려면 Azure Portal의 메뉴에서 **Security Center**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="f6f78-117">이 대시보드에서 Azure 환경의 보안 상태를 보고, 현재 권장되는 구성의 수를 찾고, 현재의 위협 경고 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="f6f78-118">각 상위 수준의 차트를 펼쳐 세부 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-118">You can expand each high-level chart to see more detail.</span></span>

![Security Center 대시보드](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="f6f78-120">Security Center는 데이터 검색 외에도 검색된 문제에 대한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="f6f78-121">예를 들어 연결된 네트워크 보안 그룹 없이 VM을 배포한 경우 Security Center에서 수행할 수 있는 재구성 단계와 함께 권장 사항을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="f6f78-122">Security Center의 컨텍스트를 벗어나지 않으면서 자동화된 재구성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![추천](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="f6f78-124">데이터 수집 설정</span><span class="sxs-lookup"><span data-stu-id="f6f78-124">Set up data collection</span></span>

<span data-ttu-id="f6f78-125">VM 보안 구성을 확인하려면 먼저 Security Center 데이터 수집을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="f6f78-126">여기에는 데이터 수집을 설정하고 수집된 데이터를 저장할 Azure 저장소 계정을 만드는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="f6f78-127">Azure Security Center 대시보드에서 **보안 정책**을 클릭한 다음 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="f6f78-128">**데이터 수집**에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="f6f78-129">저장소 계정을 만들려면 **저장소 계정 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="f6f78-130">그런 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="f6f78-131">**보안 정책** 블레이드에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="f6f78-132">그러면 Security Center 데이터 수집 에이전트가 모든 VM에 설치되고 데이터 수집이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="f6f78-133">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="f6f78-133">Set up a security policy</span></span>

<span data-ttu-id="f6f78-134">보안 정책은 Security Center에서 데이터를 수집하고 권장할 항목을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="f6f78-135">서로 다른 보안 정책을 Azure 리소스 집합마다 개별적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="f6f78-136">기본적으로 Azure 리소스가 모든 정책 항목에 대해 평가되지만, 모든 Azure 리소스 또는 리소스 그룹에 대해 개별 정책 항목을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="f6f78-137">Azure Security Center 보안 정책에 대한 자세한 내용은 [Azure Security Center에서 보안 정책 설정](../../security-center/security-center-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f78-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="f6f78-138">모든 Azure 리소스에 대한 보안 정책을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="f6f78-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="f6f78-139">Security Center 대시보드에서 **보안 정책**을 클릭한 다음 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="f6f78-140">**방지 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="f6f78-141">모든 Azure 리소스에 적용하려는 정책 항목을 설정하거나 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="f6f78-142">설정 선택 작업을 완료했으면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="f6f78-143">**보안 정책** 블레이드에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="f6f78-144">특정 리소스 그룹에 대한 정책을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="f6f78-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="f6f78-145">Security Center 대시보드에서 **보안 정책**을 선택한 다음 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="f6f78-146">**방지 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="f6f78-147">리소스 그룹에 적용하려는 정책 항목을 설정하거나 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="f6f78-148">**상속**에서 **고유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="f6f78-149">설정 선택 작업을 완료했으면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="f6f78-150">**보안 정책** 블레이드에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="f6f78-151">또한 이 페이지에서 특정 리소스 그룹에 대한 데이터 수집도 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="f6f78-152">다음 예제에서는 *myResoureGroup*이라는 리소스 그룹에 대한 고유 정책을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="f6f78-153">이 정책에서는 디스크 암호화 및 웹 응용 프로그램 방화벽 권장 사항이 모두 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![고유 정책](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="f6f78-155">VM 구성 상태 보기</span><span class="sxs-lookup"><span data-stu-id="f6f78-155">View VM configuration health</span></span>

<span data-ttu-id="f6f78-156">데이터 수집을 설정하고 보안 정책을 설정하면 Security Center에서 경고 및 권장 사항을 제공하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="f6f78-157">VM이 배포되면 데이터 수집 에이전트가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="f6f78-158">그러면 Security Center가 새 VM에 대한 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="f6f78-159">VM 구성 상태에 대한 자세한 내용은 [Security Center에서 VM 보호](../../security-center/security-center-virtual-machine-recommendations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f78-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="f6f78-160">데이터가 수집되면 각 VM 및 관련 Azure 리소스에 대한 리소스 상태가 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="f6f78-161">이 정보는 읽기 쉬운 차트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="f6f78-162">리소스 상태를 보려면</span><span class="sxs-lookup"><span data-stu-id="f6f78-162">To view resource health:</span></span>

1.  <span data-ttu-id="f6f78-163">Security Center 대시보드의 **리소스 보안 상태**에서 **계산**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="f6f78-164">**계산** 블레이드에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="f6f78-165">이 보기는 모든 VM의 구성 상태에 대한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![상태 계산](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="f6f78-167">VM에 대한 모든 권장 사항을 보려면 해당 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="f6f78-168">권장 사항 및 재구성에 대해서는 이 자습서의 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="f6f78-169">구성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f6f78-169">Remediate configuration issues</span></span>

<span data-ttu-id="f6f78-170">Azure Security Center가 구성 데이터로 채워지기 시작하면 설정한 보안 정책에 따라 권장 사항이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="f6f78-171">예를 들어 연결된 네트워크 보안 그룹 없이 VM을 설정한 경우 네트워크 보안 그룹을 만들도록 제안하는 권장 사항이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="f6f78-172">모든 권장 사항 목록을 보려면:</span><span class="sxs-lookup"><span data-stu-id="f6f78-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="f6f78-173">Security Center 대시보드에서 **권장 사항**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="f6f78-174">특정 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-174">Select a specific recommendation.</span></span> <span data-ttu-id="f6f78-175">해당 권장 사항이 적용되는 모든 리소스에 대한 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="f6f78-176">권장 사항을 적용하려면 특정 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="f6f78-177">재구성 단계의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="f6f78-178">대부분의 경우 Security Center에서는 Security Center의 컨텍스트를 벗어나지 않으면서 권장 사항을 처리하기 위해 취할 수 있는 실행 가능한 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="f6f78-179">다음 예제에서는 Security Center에서 무제한 인바운드 규칙이 있는 네트워크 보안 그룹을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="f6f78-180">권장 사항 페이지에서 **인바운드 규칙 편집** 단추를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="f6f78-181">규칙을 수정하는 데 필요한 UI가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-181">The UI that is needed to modify the rule appears.</span></span> 

![추천](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="f6f78-183">권장 사항이 해결되면 해결되었다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="f6f78-184">검색된 위협 보기</span><span class="sxs-lookup"><span data-stu-id="f6f78-184">View detected threats</span></span>

<span data-ttu-id="f6f78-185">Security Center에서는 리소스 구성 권장 사항 외에도 위협 검색 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="f6f78-186">보안 경고 기능은 각 VM, Azure 네트워킹 로그 및 연결된 파트너 솔루션에서 수집된 데이터를 집계하여 Azure 리소스에 대한 보안 위협을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="f6f78-187">Security Center 위협 검색 기능에 대한 자세한 내용은 [Azure Security Center 검색 기능](../../security-center/security-center-detection-capabilities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f78-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="f6f78-188">보안 경고 기능을 사용하려면 Azure Security Center 가격 책정 계층을 *체험*에서 *표준*으로 높여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="f6f78-189">이 가격 책정 계층으로 이동하면 30일 **평가판**을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="f6f78-190">가격 책정 계층을 변경하려면:</span><span class="sxs-lookup"><span data-stu-id="f6f78-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="f6f78-191">Azure Security Center 대시보드에서 **보안 정책**을 클릭한 다음 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="f6f78-192">**가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="f6f78-193">새 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="f6f78-194">**보안 정책** 블레이드에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="f6f78-195">가격 책정 계층을 변경하면 보안 위협이 검색될 때 보안 경고 그래프가 채워지기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![보안 경고](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="f6f78-197">경고를 선택하여 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-197">Select an alert to view information.</span></span> <span data-ttu-id="f6f78-198">예를 들어 위협, 검색 시간, 모든 위협 시도 및 권장되는 재구성에 대한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="f6f78-199">다음 예제에서는 RDP 무차별 암호 대입 공격이 검색되었으며, 실패한 RDP 시도 횟수는 294회입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="f6f78-200">권장되는 해결 방법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-200">A recommended resolution is provided.</span></span>

![RDP 공격](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="f6f78-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6f78-202">Next steps</span></span>
<span data-ttu-id="f6f78-203">이 자습서에서는 Azure Security Center를 설정한 다음 Security Center에서 VM을 검토했습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="f6f78-204">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f6f78-205">데이터 수집 설정</span><span class="sxs-lookup"><span data-stu-id="f6f78-205">Set up data collection</span></span>
> * <span data-ttu-id="f6f78-206">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="f6f78-206">Set up security policies</span></span>
> * <span data-ttu-id="f6f78-207">구성 상태 문제 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="f6f78-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="f6f78-208">검색된 위협 검토</span><span class="sxs-lookup"><span data-stu-id="f6f78-208">Review detected threats</span></span>

<span data-ttu-id="f6f78-209">Jenkins, GitHub 및 Docker를 사용하여 CI/CD 파이프라인을 만드는 방법에 대해 알아보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f78-209">Advance to the next tutorial to learn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6f78-210">Jenkins, GitHub 및 Docker를 사용하여 CI/CD 인프라 만들기</span><span class="sxs-lookup"><span data-stu-id="f6f78-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

