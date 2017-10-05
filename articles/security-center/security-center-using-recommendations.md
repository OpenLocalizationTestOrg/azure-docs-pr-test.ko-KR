---
title: "Azure Security Center 권장 사항을 사용하여 보안 강화 | Microsoft Docs"
description: " Azure Security Center에서 보안 정책 및 권장 사항을 사용하여 보안 공격을 완화할 수 있는 방법을 알아봅니다. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: cb4a7db5666242576bf83abbf10682cc6f53ba69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-security-center-recommendations-to-enhance-security"></a><span data-ttu-id="64a73-103">Azure Security Center 권장 사항을 사용하여 보안 강화</span><span class="sxs-lookup"><span data-stu-id="64a73-103">Use Azure Security Center recommendations to enhance security</span></span>
<span data-ttu-id="64a73-104">보안 정책을 구성한 다음 Azure Security Center에서 제공한 권장 사항을 구현하여 중요한 보안 이벤트의 가능성을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-104">You can reduce the chances of a significant security event by configuring a security policy and then implementing the recommendations provided by Azure Security Center.</span></span> <span data-ttu-id="64a73-105">이 문서에서는 Security Center에서 보안 정책 및 권장 사항을 사용하여 보안 공격을 완화할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-105">This article shows you how to use security policies and recommendations in Security Center to help mitigate a security attack.</span></span>

> [!NOTE]
> <span data-ttu-id="64a73-106">이 문서는 Security Center [계획 및 운영 가이드](security-center-planning-and-operations-guide.md)에서 소개된 역할 및 개념을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-106">This article builds on the roles and concepts introduced in the Security Center [planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="64a73-107">계속하기 전에 계획 가이드를 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-107">It’s a good idea to review the planning guide before continuing.</span></span>
>
>

## <a name="managing-security-recommendations"></a><span data-ttu-id="64a73-108">보안 권장 사항 관리</span><span class="sxs-lookup"><span data-stu-id="64a73-108">Managing security recommendations</span></span>
<span data-ttu-id="64a73-109">보안 정책은 지정된 구독 또는 리소스 그룹 내에서 리소스에 대해 권장되는 제어 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-109">A security policy defines the set of controls that are recommended for resources within the specified subscription or resource group.</span></span> <span data-ttu-id="64a73-110">Security Center에서 회사의 보안 요구 사항에 따라 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-110">In Security Center, you define policies according to your company's security requirements.</span></span> <span data-ttu-id="64a73-111">자세한 내용은 [Security Center에서 보안 정책 설정](security-center-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64a73-111">To learn more, see [Set security policies in Security Center](security-center-policies.md).</span></span>

<span data-ttu-id="64a73-112">리소스 그룹에 대한 보안 정책은 구독 수준에서 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-112">Security policies for resource groups are inherited from the subscription level.</span></span>

![보안 정책 상속][1]

<span data-ttu-id="64a73-114">특정 리소스 그룹에서 사용자 지정 정책이 필요한 경우 리소스 그룹에서 상속을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-114">If you need custom policies in specific resource groups, you can disable inheritance in the resource group.</span></span> <span data-ttu-id="64a73-115">상속을 사용하지 않으려면 고유한 보안 정책 블레이드로 설정하고 Security Center에서 권장 사항을 표시하는 컨트롤을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-115">To disable, set Inheritance to Unique on the Security policy blade and customize the controls that Security Center shows recommendations for.</span></span>

<span data-ttu-id="64a73-116">예를 들어 SQL Database TDE(투명한 데이터 암호화) 정책이 필요하지 않은 워크로드의 경우, 구독 수준에서 정책을 해제하고 SQL TDE가 필요한 리소스 그룹에서만 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-116">For example, if you have workloads that do not require the SQL Database Transparent Data Encryption (TDE) policy, turn off the policy at the subscription level and enable it only in the resources groups where SQL TDE is required.</span></span>

> [!NOTE]
> <span data-ttu-id="64a73-117">구독 수준 정책과 리소스 그룹 수준 정책 간에 충돌이 발생한 경우 리소스 그룹 수준 정책이 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-117">If there is a conflict between subscription level policy and resource group level policy, the resource group level policy takes precedence.</span></span>
>
>

<span data-ttu-id="64a73-118">보안 센터에서는 Azure 리소스의 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-118">Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="64a73-119">Security Center가 잠재적인 보안 취약점을 식별하는 경우 보안 정책에서 설정된 컨트롤에 따라 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-119">When Security Center identifies potential security vulnerabilities, it creates recommendations based on the controls set in the security policy.</span></span> <span data-ttu-id="64a73-120">권장 사항은 필요한 보안 컨트롤을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-120">The recommendations guide you through the process of configuring the needed security controls.</span></span>

<span data-ttu-id="64a73-121">현재 Security Center의 정책 권장 사항은 시스템 업데이트, OS 구성, 네트워크 서브넷 및 VM(가상 컴퓨터)의 네트워크 보안 그룹, SQL Database 감사, SQL Database TDE 및 웹 응용 프로그램 방화벽에 집중되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-121">Current policy recommendations in Security Center focus on system updates, OS configuration, network security groups on subnets and virtual machines (VMs), SQL Database Auditing, SQL Database TDE, and web application firewalls.</span></span> <span data-ttu-id="64a73-122">Security Center 권장 사항의 최신 적용 범위는 [Security Center에서 보안 권장 사항 관리](security-center-recommendations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64a73-122">For the most up-to-date coverage of Security Center recommendations, see [Managing security recommendations in Security Center](security-center-recommendations.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="64a73-123">시나리오</span><span class="sxs-lookup"><span data-stu-id="64a73-123">Scenario</span></span>
<span data-ttu-id="64a73-124">이 시나리오에서는 Security Center 권장 사항을 모니터링하고 조치를 취하여 중요한 보안 인시던트가 발생할 가능성을 줄일 수 있도록 Security Center를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-124">This scenario shows you how to use Security Center to help reduce the chances of a significant security incident by monitoring Security Center recommendations and taking action.</span></span> <span data-ttu-id="64a73-125">시나리오는 Security Center [계획 및 운영 가이드](security-center-planning-and-operations-guide.md#security-roles-and-access-controls)에서 제공된 가상의 회사, Contoso 및 역할을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-125">The scenario uses the fictitious company, Contoso, and roles presented in the Security Center [planning and operations guide](security-center-planning-and-operations-guide.md#security-roles-and-access-controls).</span></span> <span data-ttu-id="64a73-126">역할은 Security Center를 사용하여 다른 보안 관련 작업을 수행할 수 있는 개인 및 팀을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-126">The roles represent individuals and teams that may use Security Center to perform different security-related tasks.</span></span> <span data-ttu-id="64a73-127">역할은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-127">The roles are:</span></span>

![시나리오 역할][2]

<span data-ttu-id="64a73-129">Contoso는 최근 해당 온-프레미스 리소스의 일부를 Azure로 마이그레이션했습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-129">Contoso recently migrated some of their on-premises resources to Azure.</span></span> <span data-ttu-id="64a73-130">Contoso는 클라우드에서 해당 리소스의 보안 공격에 대한 해당 취약점을 줄이는 보호 방법을 구현 및 유지 관리하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-130">Contoso wants to implement and maintain protections that reduce their vulnerability to a security attack of their resources in the cloud.</span></span>

## <a name="recommended-solution"></a><span data-ttu-id="64a73-131">권장된 솔루션</span><span class="sxs-lookup"><span data-stu-id="64a73-131">Recommended solution</span></span>
<span data-ttu-id="64a73-132">솔루션은 Security Center를 사용하여 보안 취약점을 방지하고 감지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-132">A solution is to use Security Center to prevent and detect security vulnerabilities.</span></span> <span data-ttu-id="64a73-133">Contoso는 Azure 구독을 통해 Security Center에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-133">Contoso has access to Security Center via their Azure subscription.</span></span> <span data-ttu-id="64a73-134">Security Center의 [무료 계층](security-center-pricing.md)은 모든 Azure 구독에서 자동으로 활성화되고 해당 구독의 모든 VM에서 데이터 수집을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-134">The [Free tier](security-center-pricing.md) of Security Center is automatically enabled on all Azure subscriptions and data collection is enabled on all VMs in their subscription.</span></span>

<span data-ttu-id="64a73-135">Contoso의 IT 보안에서 David는 Security Center를 사용하여 **보안 정책**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-135">David, in Contoso’s IT Security, configures a **security policy** using Security Center.</span></span> <span data-ttu-id="64a73-136">Security Center에서는 Contoso의 Azure 리소스 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-136">Security Center analyzes the security state of Contoso’s Azure resources.</span></span> <span data-ttu-id="64a73-137">Security Center가 잠재적인 보안 취약점을 식별하는 경우 보안 정책에서 설정된 컨트롤에 따라 **권장 사항**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-137">When Security Center identifies potential security vulnerabilities, it creates **recommendations** based on the controls set in the security policy.</span></span>

<span data-ttu-id="64a73-138">클라우드 워크로드 소유자인 Jeff는 Contoso의 보안 정책에 따라 보호 방법을 구현하고 유지 관리하는 업무를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-138">Jeff, a cloud workload owner, is responsible for implementing and maintaining protections in accordance with Contoso’s security policies.</span></span> <span data-ttu-id="64a73-139">Jeff는 Security Center에서 만든 권장 사항을 모니터링하여 보호를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-139">Jeff can monitor the recommendations created by Security Center to apply protections.</span></span> <span data-ttu-id="64a73-140">권장 사항은 Jeff가 필요한 보안 컨트롤을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-140">The recommendations guide Jeff through the process of configuring the needed security controls.</span></span>

<span data-ttu-id="64a73-141">Jeff가 보호를 구현 및 유지하고 보안 취약점을 제거하기 위해 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-141">In order for Jeff to implement and maintain protections and eliminate security vulnerabilities, he needs to:</span></span>

- <span data-ttu-id="64a73-142">Security Center에서 제공한 보안 권장 사항 모니터링</span><span class="sxs-lookup"><span data-stu-id="64a73-142">Monitor security recommendations provided by Security Center</span></span>
- <span data-ttu-id="64a73-143">보안 권장 사항을 평가하고 적용하거나 해제해야 할지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-143">Evaluate security recommendations and decide if he should apply or dismiss</span></span>
- <span data-ttu-id="64a73-144">보안 권장 사항 적용</span><span class="sxs-lookup"><span data-stu-id="64a73-144">Apply security recommendations</span></span>

<span data-ttu-id="64a73-145">Jeff가 Security Center 권장 사항을 사용하여 보안 취약점을 제거하는 컨트롤을 구성하는 과정을 보기 위해 Jeff가 수행한 단계를 따라가겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-145">Let’s follow Jeff’s steps to see how he uses Security Center recommendations to guide him through the process of configuring controls to eliminate security vulnerabilities.</span></span>

## <a name="how-to-implement-this-solution"></a><span data-ttu-id="64a73-146">이 솔루션을 구현하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a73-146">How to implement this solution</span></span>
<span data-ttu-id="64a73-147">Jeff는 [Azure Portal](https://azure.microsoft.com/features/azure-portal/)에 로그인하고 Security Center 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-147">Jeff signs in to [Azure portal](https://azure.microsoft.com/features/azure-portal/) and opens the Security Center console.</span></span> <span data-ttu-id="64a73-148">일상적인 모니터링 작업의 일환으로 다음 단계를 수행하여 보안 권장 사항이 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-148">As part of his daily monitoring activities, he checks to see if there are security recommendations by performing the following steps:</span></span>

1. <span data-ttu-id="64a73-149">Jeff는 **권장 사항** 타일을 선택하여 **권장 사항** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-149">Jeff selects the **Recommendations** tile to open the **Recommendations** blade.</span></span>
   <span data-ttu-id="64a73-150">![권장 사항 타일 선택][3]</span><span class="sxs-lookup"><span data-stu-id="64a73-150">![Select the recommendations tile][3]</span></span>
2. <span data-ttu-id="64a73-151">Jeff는 권장 사항 목록을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-151">Jeff reviews the list of recommendations.</span></span> <span data-ttu-id="64a73-152">또한 Security Center에서 우선 순위에 따라 우선 순위가 가장 높은 것부터 낮은 순으로 권장 사항 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-152">He sees that Security Center has provided the list of recommendations in priority order, from highest priority to lowest priority.</span></span> <span data-ttu-id="64a73-153">목록에서 우선 순위가 높은 항목을 해결하기로 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-153">He decides to address a High priority recommendation on the list.</span></span> <span data-ttu-id="64a73-154">**권장 사항** 블레이드에서 **Endpoint Protection 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-154">He selects **Install Endpoint Protection** on the **Recommendations** blade.</span></span>
3. <span data-ttu-id="64a73-155">맬웨어 방지 프로그램을 사용하지 않는 VM의 목록을 표시하는 **Endpoint Protection 설치** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-155">The **Install Endpoint Protection** blade opens displaying a list of VMs without antimalware enabled.</span></span> <span data-ttu-id="64a73-156">Jeff는 VM 목록을 검토하고 모든 VM을 선택한 다음 **3개의 VM에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-156">Jeff reviews the list of VMs, selects all VMs, and then selects **Install on 3 VMs**.</span></span>
   <span data-ttu-id="64a73-157">![Endpoint Protection 설치][4]</span><span class="sxs-lookup"><span data-stu-id="64a73-157">![Install endpoint protection][4]</span></span>
4. <span data-ttu-id="64a73-158">**Endpoint Protection 선택** 블레이드가 열리고 Jeff에게 두 가지 맬웨어 방지 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-158">The **Select Endpoint Protection** blade opens providing Jeff with two antimalware solutions.</span></span> <span data-ttu-id="64a73-159">Jeff는 **Microsoft 맬웨어 방지** 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-159">Jeff selects the **Microsoft Antimalware** solution.</span></span>
5. <span data-ttu-id="64a73-160">맬웨어 방지 솔루션에 대한 추가 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-160">Additional information about the antimalware solution is displayed.</span></span> <span data-ttu-id="64a73-161">Jeff는 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-161">Jeff selects **Create**.</span></span>
   <span data-ttu-id="64a73-162">![Microsoft 맬웨어 방지][5]</span><span class="sxs-lookup"><span data-stu-id="64a73-162">![Microsoft antimalware][5]</span></span>
6. <span data-ttu-id="64a73-163">Jeff는 **설치** 블레이드에서 필수 구성 설정을 입력하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-163">Jeff enters the required configuration settings on the **Install** blade and selects **OK**.</span></span>

<span data-ttu-id="64a73-164">선택한 VM에서 [Microsoft 맬웨어 방지 프로그램](../security/azure-security-antimalware.md)이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-164">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

<span data-ttu-id="64a73-165">Jeff는 계속해서 높은 우선 순위 및 보통 우선 순위 권장 사항을 살펴보고 구현할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-165">Jeff continues to move through the high priority and medium priority recommendations, making decisions on implementation.</span></span> <span data-ttu-id="64a73-166">Jeff는 [보안 권장 사항 관리](security-center-recommendations.md) 문서를 참조하여 권장 사항 및 적용 시 역할을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-166">Jeff references the [Managing security recommendations](security-center-recommendations.md) article to understand the recommendations and what each one does if he applies it.</span></span>

<span data-ttu-id="64a73-167">Jeff는 [MSRC(Microsoft Security Response Center)](../security/azure-security-response-center.md)가 Azure 네트워크 및 인프라의 선택 보안 모니터링을 수행하고 타사에서 위협 인텔리전스 및 남용 불만 사항을 받는다는 것을 알았습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-167">Jeff learns that [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span> <span data-ttu-id="64a73-168">Jeff가 Contoso의 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 경우 MSRC가 Contoso의 고객 데이터에 불법적이거나 권한이 없는 당사자에 의한 액세스를 검색하게 되면 Microsoft는 Contoso에 이를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-168">If Jeff provides security contact details for Contoso’s Azure subscription, Microsoft contacts Contoso if the MSRC discovers that Contoso’s customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="64a73-169">Jeff가 **보안 연락처 세부 정보 제공** 권장 사항(위의 권장 사항 목록 중 보통 심각도인 권장 사항)을 적용하는 과정을 따라서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-169">Let’s follow Jeff as he applies the **Provide security contact details** recommendation (a recommendation with severity of Medium in the list of recommendations above).</span></span>

1. <span data-ttu-id="64a73-170">Jeff가 **권장 사항** 블레이드에서 **보안 연락처 세부 정보 제공**을 선택하면 **보안 연락처 세부 정보 제공** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-170">Jeff selects **Provide security contact details** on the **Recommendations** blade, which opens the **Provide security contact details** blade.</span></span>
2. <span data-ttu-id="64a73-171">Jeff는 연락처 정보를 제공할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-171">Jeff selects the Azure subscription to provide contact information on.</span></span> <span data-ttu-id="64a73-172">두 번째 **보안 연락처 세부 정보 제공** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-172">A second **Provide security contact details** blade opens.</span></span>
   <span data-ttu-id="64a73-173">![보안 연락처 세부 정보][6]</span><span class="sxs-lookup"><span data-stu-id="64a73-173">![Security contact details][6]</span></span>
3. <span data-ttu-id="64a73-174">Jeff는 두 번째 **보안 연락처 세부 정보 제공** 블레이드에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-174">On the second **Provide security contact details** blade, Jeff enters:</span></span>

  - <span data-ttu-id="64a73-175">쉼표로 구분된 보안 연락처 전자 메일 주소(입력할 수 있는 전자 메일 주소 수에 제한이 없음)</span><span class="sxs-lookup"><span data-stu-id="64a73-175">the security contact email addresses separated by commas (there is not a limit to the number of email addresses that he can enter)</span></span>
  - <span data-ttu-id="64a73-176">보안 연락처 전화 번호</span><span class="sxs-lookup"><span data-stu-id="64a73-176">one security contact phone number</span></span>

4. <span data-ttu-id="64a73-177">또한 Jeff는 **경고에 대한 전자 메일 받기**옵션을 설정하여 심각도 높은 경고에 대한 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-177">Jeff also turns on the option **Send me emails about alerts** to receive emails about high severity alerts.</span></span>
5. <span data-ttu-id="64a73-178">그리고 **확인**을 선택하여 보안 연락처 정보를 Contoso의 구독에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-178">Jeff selects **OK** to apply the security contact information to Contoso’s subscription.</span></span>

<span data-ttu-id="64a73-179">Jeff는 마지막으로 우선 순위가 낮은 권장 사항 **OS 취약점 재구성**을 검토하고 이 권장 사항을 적용할 수 없다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-179">Finally, Jeff reviews the low priority recommendation **Remediate OS vulnerabilities** and determines that this recommendation is not applicable.</span></span> <span data-ttu-id="64a73-180">권장 구성을 해제하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-180">He wants to dismiss the recommendation.</span></span> <span data-ttu-id="64a73-181">Jeff는 오른쪽에 표시되는 점 세 개를 선택한 다음 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-181">Jeff selects the three dots that appear to the right, and then selects **Dismiss**.</span></span>
   <span data-ttu-id="64a73-182">![권장 사항 해제][7]</span><span class="sxs-lookup"><span data-stu-id="64a73-182">![Dismiss recommendation][7]</span></span>

## <a name="conclusion"></a><span data-ttu-id="64a73-183">결론</span><span class="sxs-lookup"><span data-stu-id="64a73-183">Conclusion</span></span>
<span data-ttu-id="64a73-184">Security Center에서 권장 사항을 모니터링하면 공격이 발생하기 전에 보안 취약점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-184">Monitoring recommendations in Security Center may help you eliminate security vulnerabilities before an attack occurs.</span></span> <span data-ttu-id="64a73-185">Security Center에서 보안 정책을 사용하여 보호를 구현하고 유지 관리하여 보안 인시던트를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a73-185">You can prevent a security incident by implementing and maintaining protections with security policies in Security Center.</span></span>

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
