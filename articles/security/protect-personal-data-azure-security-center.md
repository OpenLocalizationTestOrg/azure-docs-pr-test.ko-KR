---
title: "Azure Security Center를 사용하여 개인 데이터 보호 | Microsoft Docs"
description: "Azure Security Center를 사용하여 개인 데이터를 보호합니다."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="c41da-103">위반 및 공격으로부터 개인 데이터 보호: Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c41da-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="c41da-104">이 문서는 Azure Security Center를 사용하여 위반 및 공격으로부터 개인 데이터를 보호하는 방법을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="c41da-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="c41da-105">Scenario</span></span> 

<span data-ttu-id="c41da-106">미국에 본사를 둔 대형 크루즈 회사는 영국 제도뿐만 아니라 지중해 및 발트해 연안의 여정도 제공하도록 사업을 확장하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="c41da-107">이러한 노력을 지원하기 위해 이탈리아, 독일, 덴마크 및 영국에 기반을 둔 몇 개의 소형 크루즈 라인을 인수했습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="c41da-108">회사에서 Microsoft Azure를 사용하여 클라우드에 회사 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="c41da-109">여기에는 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="c41da-110">또한 다음과 같은 인적 자원 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="c41da-111">주소</span><span class="sxs-lookup"><span data-stu-id="c41da-111">Addresses</span></span>
- <span data-ttu-id="c41da-112">전화 번호</span><span class="sxs-lookup"><span data-stu-id="c41da-112">Phone numbers</span></span>
- <span data-ttu-id="c41da-113">납세자 번호</span><span class="sxs-lookup"><span data-stu-id="c41da-113">Tax identification numbers</span></span>
- <span data-ttu-id="c41da-114">의료 보험 정보</span><span class="sxs-lookup"><span data-stu-id="c41da-114">Medical information</span></span>

<span data-ttu-id="c41da-115">또한 크루즈 라인에서 보상 및 충성도 프로그램 구성원에 대한 대규모 데이터베이스를 유지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="c41da-116">회사 직원은 회사의 원격 사무실에서 네트워크에 액세스하고 전 세계에 위치한 여행사는 일부 회사 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="c41da-117">개인 데이터는 이러한 위치와 Microsoft 데이터 센터 간에 네트워크를 통해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="c41da-118">문제 설명</span><span class="sxs-lookup"><span data-stu-id="c41da-118">Problem statement</span></span>

<span data-ttu-id="c41da-119">회사에서 Azure 리소스에 대한 공격의 위협에 대해 우려하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="c41da-120">권한 없는 사람에게 고객과 직원의 개인 데이터가 노출되지 않도록 방지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="c41da-121">클라우드 리소스에 대한 지속적인 보안을 모니터링하는 효과적인 방법뿐만 아니라 방지 및 대응/수정에 대한 지침도 원합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="c41da-122">오늘날의 정교하고 조직화된 공격자들에 대한 강력한 방어선이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="c41da-123">회사 목표</span><span class="sxs-lookup"><span data-stu-id="c41da-123">Company goal</span></span>

<span data-ttu-id="c41da-124">회사의 목표 중 하나는 고객 및 직원의 개인 데이터를 위협으로부터 보호하여 개인 정보를 보호하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="c41da-125">이러한 목표 중 하나는 영향을 완화하기 위해 위반의 증상에 즉시 대응하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="c41da-126">보안의 현재 상태를 평가하고, 취약한 구성을 식별하고, 이를 수정하는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="c41da-127">솔루션</span><span class="sxs-lookup"><span data-stu-id="c41da-127">Solutions</span></span>

<span data-ttu-id="c41da-128">Microsoft ASC(Azure Security Center)에서는 통합된 보안 모니터링 및 정책 관리 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="c41da-129">사용하기 쉽고 효과적인 위협 방지, 검색 및 대응 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="c41da-130">방지</span><span class="sxs-lookup"><span data-stu-id="c41da-130">Prevention</span></span>

<span data-ttu-id="c41da-131">ASC를 사용하면 보안 정책을 설정하고, JIT(Just-In-Time) 액세스를 제공하며, 보안 권장 사항을 구현할 수 있게 하여 위반을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="c41da-132">보안 정책은 지정된 구독 내에 있는 리소스에 권장되는 제어 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="c41da-133">JIT 액세스는 Azure VM에 대한 인바운드 트래픽을 잠궈 공격에 대한 노출을 줄이는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="c41da-134">보안 권장 사항은 Azure 리소스의 보안 상태를 분석한 후 ASC에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="c41da-135">ASC에서 보안 정책을 설정하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="c41da-136">각 구독에 대한 보안 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="c41da-137">보안 정책을 수정하려면 해당 구독의 소유자 또는 참여자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="c41da-138">Azure Portal에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="c41da-139">ASC 대시보드에서 **정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="c41da-140">정책을 사용하도록 설정하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="c41da-141">**방지 정책**을 선택하여 구독당 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="c41da-142">**가상 컴퓨터에서 데이터 수집**은 **설정**으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="c41da-143">**방지 정책**  옵션에서 **설정**을 선택하여 구독과 관련된 보안 권장 사항을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="c41da-144">사용하도록 설정할 수 있는 각 정책 권장 사항에 대한 자세한 지침과 설명은 [Azure Security Center에서 보안 정책 설정](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="c41da-145">JIT(Just-In-Time) 액세스를 구성하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="c41da-146">JIT를 사용하도록 설정되면 Security Center에서 NSG 규칙을 만들어 Azure VM에 대한 인바운드 트래픽을 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="c41da-147">VM에서 인바운드 트래픽을 잠글 포트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="c41da-148">JIT 액세스를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="c41da-149">ASC 블레이드에서 **Just-In-Time VM 액세스 타일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="c41da-150">**권장** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="c41da-151">**VM** 아래에서 사용하도록 설정할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="c41da-152">그러면 VM 옆에 있는 확인 표시가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="c41da-153">VM에서 **JIT 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="c41da-154">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-154">Select **Save**.</span></span>

<span data-ttu-id="c41da-155">그런 다음 ASC에서 JIT에 사용하도록 권장하는 기본 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="c41da-156">Just-In-Time 솔루션을 사용하도록 설정하려는 새 포트를 추가 및 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="c41da-157">Security Center의 **Just-In-Time VM 액세스** 타일에서는 JIT 액세스를 수행하도록 구성된 VM 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="c41da-158">지난 주에 승인된 액세스 요청 수도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="c41da-159">이를 수행하는 방법에 대한 지침 및 Just-In-Time 액세스에 대한 자세한 내용은 [Just-In-Time을 사용하여 가상 컴퓨터 액세스 관리](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="c41da-160">ASC 보안 권장 사항을 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="c41da-161">보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="c41da-162">권장 사항은 필요한 컨트롤을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="c41da-163">ASC 대시보드에서 **권장 사항** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="c41da-164">각 줄이 하나의 권장 사항을 나타내는 테이블 형식으로 표시된 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="c41da-165">권장 사항을 필터링하려면 **필터**를 선택하고 표시할 심각도 및 상태 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="c41da-166">적용할 수 없는 권장 사항을 해제하려면 마우스 오른쪽 단추를 클릭하고 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="c41da-167">먼저 어떤 권고 사항을 적용해야 하는지 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="c41da-168">우선 순위에 따라 권장 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="c41da-169">가능한 권장 사항 목록 및 각각을 적용하는 방법에 대한 연습은 [Azure Security Center에서 보안 권장 사항 관리](https://docs.microsoft.com/azure/security-center/security-center-recommendations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="c41da-170">검색 및 대응</span><span class="sxs-lookup"><span data-stu-id="c41da-170">Detection and Response</span></span>

<span data-ttu-id="c41da-171">위협이 검색된 후 최대한 빨리 대응하므로 검색과 대응이 거의 동시에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="c41da-172">ASC 위협 검색은 Azure 리소스, 네트워크 및 연결된 파트너 솔루션에서 보안 정보를 자동으로 수집하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="c41da-173">공격자가 새롭고 점차 정교해지는 악용을 풀어 놓음에 따라 ASC에서는 검색 알고리즘을 빠르게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="c41da-174">ASC 위협 검색 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 검색 기능](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="c41da-175">보안 경고를 관리하고 이에 대응하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="c41da-176">우선 순위가 지정된 보안 경고 목록은 문제를 빠르게 조사하는 데 필요한 정보와 함께 Security Center에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="c41da-177">Security Center에는 공격을 해결하는 방법에 대한 권장 사항도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="c41da-178">보안 경고를 관리하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="c41da-179">ASC 대시보드에서 **보안 경고** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="c41da-180">그러면 각 경고에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="c41da-181">날짜, 상태 및 심각도에 따라 경고를 필터링하려면 **필터**를 선택한 다음 확인하려는 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="c41da-182">경고에 대응하려면 정보를 선택하고 검토한 다음 공격받은 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="c41da-183">**설명** 필드에서 권장되는 수정 방법을 포함한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="c41da-184">경고를 관리하는 방법에 대한 자세한 내용은 [Azure Security Center에서 보안 경고 관리 및 대응](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="c41da-185">보안 경고 조사에 대한 추가 지원을 받기 위해 회사에서 [Azure 로그 통합](https://aka.ms/AzLog)을 사용하여 ASC 경고를 자체의 SIEM 솔루션과 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="c41da-186">보안 인시던트를 관리하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-186">How do I manage security incidents?</span></span>

<span data-ttu-id="c41da-187">ASC에서 보안 인시던트는 킬 체인(kill chain) 패턴과 일치하는 리소스에 대한 모든 경고의 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="c41da-188">인시던트는 관련된 경고 목록을 표시하므로 각 항목에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="c41da-189">[보안 경고] 타일 및 블레이드에서 인시던트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="c41da-190">보안 인시던트를 검토하고 관리하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="c41da-191">**보안 경고** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="c41da-192">보안 인시던트가 검색되면 보안 경고 그래프 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="c41da-193">다른 경고와 다른 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="c41da-194">이 보안 인시던트에 대한 자세한 내용을 보려면 해당 인시던트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="c41da-195">추가 세부 정보에는 전체 설명, 심각도, 현재 상태, 공격받은 리소스, 인시던트에 대한 수정 단계 및 이 인시던트에 포함된 경고가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="c41da-196">필터링하여 **인시던트만**, **경고만**, **둘 다**를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="c41da-197">위협 인텔리전스 보고서에 액세스하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="c41da-198">ASC는 여러 원본의 정보를 분석하여 위협을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="c41da-199">인시던트 대응 팀에서 위협을 조사하고 수정하도록 지원하기 위해 Security Center에는 검색된 위협에 관한 정보를 포함한 위협 인텔리전스 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="c41da-200">Security Center에는 공격에 따라 달라질 수 있는 세 가지 유형의 위협 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="c41da-201">제공되는 보고서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-201">The reports available are:</span></span>

- <span data-ttu-id="c41da-202">활동 그룹 보고서: 공격자 및 이들의 목표와 전술에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="c41da-203">캠페인 보고서: 특정 공격 캠페인의 세부 정보에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="c41da-204">위협 요약 보고서: 이전 두 보고서의 모든 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="c41da-205">이러한 유형의 정보는 공격의 출처, 공격자의 동기 및 이 문제를 완화하기 위한 조치를 파악하기 위한 지속적인 조사가 있는 인시던트 대응 프로세스에서 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="c41da-206">위협 인텔리전스 보고서에 액세스하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="c41da-207">ASC 대시보드에서 **보안 경고** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="c41da-208">자세한 정보를 얻으려는 보안 경고를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="c41da-209">**보고서** 필드에서 위협 인텔리전스 보고서에 대한 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="c41da-210">그러면 다운로드할 수 있는 PDF 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="c41da-211">ASC 위협 인텔리전스 보고서에 대한 자세한 내용은 [Azure Security Center 위협 인텔리전스 보고서](https://docs.microsoft.com/azure/security-center/security-center-threat-report)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="c41da-212">평가</span><span class="sxs-lookup"><span data-stu-id="c41da-212">Assessment</span></span>

<span data-ttu-id="c41da-213">ASC는 보안 상태에 대한 테스트, 판단 및 평가를 지원하기 위해 가상 컴퓨터 권장 구성 요소의 일부로 Qualys 클라우드 에이전트와 통합된 취약성 평가를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="c41da-214">Qualys 에이전트는 Qualys 관리 플랫폼에 취약성 데이터를 보고한 다음, 취약성 및 상태 모니터링 데이터를 ASC로 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="c41da-215">취약성 평가 솔루션을 추가하도록 제안되는 권장 사항은 ASC 대시보드의 **권장 사항** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="c41da-216">취약성 평가 솔루션이 대상 VM에 설치된 후에 Security Center는 VM을 스캔하여 시스템 및 응용 프로그램 취약성을 감지하고 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="c41da-217">감지된 문제는 **Virtual Machines 권장 사항** 옵션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="c41da-218">취약성 평가 솔루션을 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c41da-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="c41da-219">통합된 취약성 평가 솔루션이 Virtual Machine에 아직 배포되지 않았으면 Security Center에 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="c41da-220">ASC 대시보드의 **권장 사항** 블레이드에서 **취약성 평가 솔루션 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="c41da-221">취약성 평가 솔루션을 설치하려는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="c41da-222">**[수]개 VM에 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="c41da-223">Azure Marketplace에서 파트너 솔루션을 선택하거나 **기존 솔루션 사용** 아래에서 **Qualys**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="c41da-224">**파트너 솔루션** 블레이드에서 자동 업데이트 설정을 설정하거나 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41da-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="c41da-225">취약성 평가 솔루션을 구현하는 방법에 대한 자세한 지침은 [Azure Security Center의 취약성 평가](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41da-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c41da-226">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c41da-226">Next steps</span></span>

- [<span data-ttu-id="c41da-227">Azure Security Center 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="c41da-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="c41da-228">Azure Security Center 소개</span><span class="sxs-lookup"><span data-stu-id="c41da-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="c41da-229">Azure 로그 통합에 Azure Security Center 경고 통합</span><span class="sxs-lookup"><span data-stu-id="c41da-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="c41da-230">통합된 취약성 평가를 통한 Azure Security Center 강화(영문)</span><span class="sxs-lookup"><span data-stu-id="c41da-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
