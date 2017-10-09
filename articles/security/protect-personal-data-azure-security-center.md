---
title: "Azure 보안 센터를 사용 하 여 개인 데이터 aaaProtect | Microsoft Docs"
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="d2723-103">위반 및 공격으로부터 개인 데이터 보호: Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d2723-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="d2723-104">이 문서에서 toouse Azure 보안 센터 tooprotect 개인 데이터 침해 방법을 이해 하는 데 도움이 됩니다 하 고 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="d2723-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="d2723-105">Scenario</span></span> 

<span data-ttu-id="d2723-106">Hello 미국에서에서 본사는 큰 크루즈 회사 hello 영국 제도 뿐만 아니라 hello 지중해 발트어 바다에서 해당 작업 toooffer 일정 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="d2723-107">이러한 노력에 있어서 toohelp, 이탈리아, 독일, 덴마크, hello 영국에 따라 여러 개의 더 작은 크루즈 줄 획득</span><span class="sxs-lookup"><span data-stu-id="d2723-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="d2723-108">hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="d2723-109">여기에는 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="d2723-110">또한 다음과 같은 인적 자원 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="d2723-111">주소</span><span class="sxs-lookup"><span data-stu-id="d2723-111">Addresses</span></span>
- <span data-ttu-id="d2723-112">전화 번호</span><span class="sxs-lookup"><span data-stu-id="d2723-112">Phone numbers</span></span>
- <span data-ttu-id="d2723-113">납세자 번호</span><span class="sxs-lookup"><span data-stu-id="d2723-113">Tax identification numbers</span></span>
- <span data-ttu-id="d2723-114">의료 보험 정보</span><span class="sxs-lookup"><span data-stu-id="d2723-114">Medical information</span></span>

<span data-ttu-id="d2723-115">hello 크루즈 줄에는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="d2723-116">회사 직원 hello 네트워크 hello 회사의 원격 사무실 및 여행사에서 액세스 하는 hello world 주변에 있는 toosome 회사 리소스에 액세스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="d2723-117">이러한 위치 및 hello Microsoft 데이터 센터 간에 개인 데이터 hello 네트워크를 통해 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="d2723-118">문제 설명</span><span class="sxs-lookup"><span data-stu-id="d2723-118">Problem statement</span></span>

<span data-ttu-id="d2723-119">hello 회사는 Azure 리소스에 대 한 공격 위협을 hello에 대 한 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="d2723-120">고객의 및 직원의 개인 데이터 toounauthorized 인원 tooprevent 노출을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="d2723-121">방지 및 응답/업데이트 관리를 비롯해는 효과적인 방법은 toomonitor hello 대 한 지속적인 보안 클라우드 리소스에 대 한 지침을 원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="d2723-122">오늘날의 정교하고 조직화된 공격자들에 대한 강력한 방어선이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="d2723-123">회사 목표</span><span class="sxs-lookup"><span data-stu-id="d2723-123">Company goal</span></span>

<span data-ttu-id="d2723-124">Hello 회사의 목표 중 하나에 위협 으로부터 보호 하 여 고객의 및 직원의 개인 데이터의 tooensure hello 개인 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="d2723-125">Toosigns toomitigate 위반의 영향을 hello 즉시이 toorespond 팀의 목표 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="d2723-126">Tooassess hello 보안의 현재 상태는 방법, 취약 한 구성을 식별 되 고 재구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="d2723-127">솔루션</span><span class="sxs-lookup"><span data-stu-id="d2723-127">Solutions</span></span>

<span data-ttu-id="d2723-128">Microsoft ASC(Azure Security Center)에서는 통합된 보안 모니터링 및 정책 관리 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="d2723-129">사용하기 쉽고 효과적인 위협 방지, 검색 및 대응 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="d2723-130">방지</span><span class="sxs-lookup"><span data-stu-id="d2723-130">Prevention</span></span>

<span data-ttu-id="d2723-131">ASC를 사용 하면 여 tooset 보안 정책 위반을 방지, 적시에 액세스를 제공 및 보안 권장 사항을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="d2723-132">지정 된 hello 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 하는 보안 정책을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="d2723-133">Just-in-time에서 액세스에 사용 되는 toolock 노출 tooattacks 감소 하 고 Azure Vm에서 인바운드 트래픽 tooyour 아래로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="d2723-134">Azure 리소스의 hello 보안 상태를 분석 한 후 asc 보안 권장 사항 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="d2723-135">ASC에서 보안 정책을 설정하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d2723-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="d2723-136">각 구독에 대한 보안 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="d2723-137">보안 정책 toomodify 소유자나 해당 구독에 대 한 참가자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="d2723-138">Hello Azure 포털에서에서 수행 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="d2723-139">선택 **정책** hello ASC 대시보드에.</span><span class="sxs-lookup"><span data-stu-id="d2723-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="d2723-140">Tooenable hello 정책 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="d2723-141">선택 **방지 정책** 구독 당 tooconfigure 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="d2723-142">**가상 컴퓨터에서 데이터를 수집** 설정할지 너무**에 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="d2723-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="d2723-143">Hello에 **방지 정책** 옵션을 선택 **에** hello 구독에 대 한 관련 된 tooenable hello 보안 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="d2723-144">명령과 각 사용할 수 있는 hello 정책 권장 사항에 대 한 설명을 자세한 [Azure 보안 센터에 보안 정책을 설정할](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="d2723-145">JIT(Just-In-Time) 액세스를 구성하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d2723-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="d2723-146">JIT를 사용 하는 보안 센터 NSG 규칙을 만들어 Azure Vm 인바운드 트래픽 tooyour 아래로 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="d2723-147">Hello 포트 선택 hello VM toowhich에 인바운드 트래픽을 잠기는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="d2723-148">JIT toouse 액세스, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="d2723-149">선택 hello **시간 VM 액세스 타일에 Just** hello ASC 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="d2723-150">선택 hello **권장** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="d2723-151">아래 **Vm**, 원하는 tooenable hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="d2723-152">확인 표시 다음 tooa VM을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="d2723-153">VM에서 **JIT 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="d2723-154">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-154">Select **Save**.</span></span>

<span data-ttu-id="d2723-155">그런 다음 ASC 권장 JIT를 사용 하도록 설정 하는 hello 기본 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="d2723-156">추가할 수 있으며 시간 솔루션에만 있는 tooenable hello 원하는 새 포트를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="d2723-157">hello **VM 액세스 시간에에서만** hello 보안 센터에서에서 타일 hello JIT 액세스용으로 구성 하는 Vm 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="d2723-158">또한 hello 지난주 hello에 대 한 액세스 승인 된 요청 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="d2723-159">방법에 대 한 지침은 toodo이를 마법사에 대 한 추가 정보에 대 한 런타임 액세스를 참조 하 고 [just-in-time에서를 사용 하 여 가상 컴퓨터 액세스 관리 합니다.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="d2723-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="d2723-160">ASC 보안 권장 사항을 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d2723-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="d2723-161">보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="d2723-162">hello 권장 사항이 필요한 hello 컨트롤 구성의 hello 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="d2723-163">선택 hello **권장 사항을** hello ASC 대시보드에서 타일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="d2723-164">여기서 각 줄은 한 가지 권장 하는 테이블 형식에 표시 된 대로 hello 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="d2723-165">toofilter 권장 사항을 선택 **필터** toosee 원하는 hello 심각도 및 상태 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="d2723-166">적용할 수 있는 권장 사항 toodismiss 마우스 오른쪽 단추로 클릭 하 고 선택할 수 **해제 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2723-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="d2723-167">먼저 어떤 권고 사항을 적용해야 하는지 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="d2723-168">Hello 권장 사항 우선 순위에 따라에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="d2723-169">가능한 권장 사항 및 방법에 대 한 연습 목록은 tooapply 각각 참조 [보안 권장 사항 Azure 보안 센터에서 관리 합니다.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="d2723-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="d2723-170">검색 및 대응</span><span class="sxs-lookup"><span data-stu-id="d2723-170">Detection and Response</span></span>

<span data-ttu-id="d2723-171">검색 및 응답 함께 이동 하려는 방법 그대로 toorespond 최대한 빨리 위협이 검색 된 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="d2723-172">ASC 위협 요소 탐지 자동으로 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 수집 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="d2723-173">공격자가 새롭고 점차 정교해지는 악용을 풀어 놓음에 따라 ASC에서는 검색 알고리즘을 빠르게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="d2723-174">ASC 위협 검색 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 검색 기능](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2723-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="d2723-175">관리 및 toosecurity 경고 응답 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d2723-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="d2723-176">Hello와 함께 보안 센터에서 우선 순위가 지정 된 보안 경고의 목록이 표시 됩니다 tooquickly 필요한 정보 hello 문제를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="d2723-177">보안 센터에도 방법에 대 한 권장 사항을 tooremediate 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="d2723-178">toomanage 보안 경고 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="d2723-179">선택 hello **보안 경고** hello ASC 대시보드 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="d2723-180">그러면 각 경고에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="d2723-181">날짜, 상태 및 심각도 기준으로 toofilter 알림을 선택 **필터** 한 다음 원하는 toosee hello 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="d2723-182">toorespond tooan 경고를 선택 하 고 및 hello 정보를 검토 하, 공격 된 hello 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="d2723-183">Hello에 **설명** 필드 권장된 업데이트 관리를 포함 한 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="d2723-184">응답 toosecurity 경고에 대 한 지침 보다 자세한 참조 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity 합니다.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="d2723-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="d2723-185">보안 경고를 조사 하려는 자세한 도움말 hello 회사와 통합할 수 ASC 경고는 자체 SIEM 솔루션을 사용 하 여 [Azure 로그 통합](https://aka.ms/AzLog)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="d2723-186">보안 인시던트를 관리하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d2723-186">How do I manage security incidents?</span></span>

<span data-ttu-id="d2723-187">ASC에서 보안 인시던트는 킬 체인(kill chain) 패턴과 일치하는 리소스에 대한 모든 경고의 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="d2723-188">인시던트 각 항목에 대 한 자세한 내용은 tooobtain 있습니다 수 있도록 하는 hello 목록이 관련된 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="d2723-189">인시던트 보안 경고 타일 hello 및 블레이드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="d2723-190">tooreview 및 보안 문제를 관리 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="d2723-191">선택 hello **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="d2723-192">보안 문제가 감지 되 면 hello 보안 경고 그래프 아래 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="d2723-193">다른 경고와 다른 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="d2723-194">이 보안 사고에 대 한 자세한 내용은 hello 인시던트 toosee를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="d2723-195">추가 세부 정보는 해당 전체 설명, 심각도, 현재 상태, 공격 hello 리소스, hello 인시던트에 대 한 업데이트 관리 단계가 hello 및 hello이 서비스에 포함 된 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="d2723-196">Toosee 필터링 할 수 있습니다 **인시던트만**, **만 경고**, 또는 **둘 다**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="d2723-197">Hello 위협 인텔리전스 보고서를 액세스 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d2723-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="d2723-198">ASC는 여러 소스 tooidentify 위협 요소 로부터 정보를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="d2723-199">tooassist 사고 대응 팀 조사 및 재구성 위협, 보안 센터 발견 된 hello 위협에 대 한 정보를 포함 하는 위협 인텔리전스 보고서에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="d2723-200">Security Center에는 공격에 따라 달라질 수 있는 세 가지 유형의 위협 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="d2723-201">사용할 수 있는 hello 보고서에는</span><span class="sxs-lookup"><span data-stu-id="d2723-201">hello reports available are:</span></span>

- <span data-ttu-id="d2723-202">활동 그룹 보고서: 공격자 및 이들의 목표와 전술에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="d2723-203">캠페인 보고서: 특정 공격 캠페인의 세부 정보에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="d2723-204">보고서를 요약 하는 위협: hello 이전 두 보고서에 있는 모든 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="d2723-205">Hello 사고 대응 프로세스 동안 이러한 종류의 정보는 매우 유용, 공격자의 동기 및 어떤 toodo toomitigate 앞으로이 문제는 진행 중인 조사 toounderstand hello 소스 hello 공격의 있는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="d2723-206">tooaccess hello 위협 인텔리전스 보고서, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="d2723-207">선택 hello **보안 경고** hello ASC 대시보드에서 타일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="d2723-208">자세한 내용은 tooobtain 원하는 hello 보안 경고를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="d2723-209">Hello에 **보고서** 필드 hello 링크 toohello 위협 인텔리전스 보고서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="d2723-210">Hello PDF 파일을 다운로드할 수 있는 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="d2723-211">Hello ASC 위협 인텔리전스 보고서에 대 한 자세한 내용은 참조 하십시오. [Azure 보안 센터 위협 인텔리전스 보고서입니다.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="d2723-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="d2723-212">평가</span><span class="sxs-lookup"><span data-stu-id="d2723-212">Assessment</span></span>

<span data-ttu-id="d2723-213">테스트, 평가 및의 보안 상태 평가 toohelp, ASC 제공 Qualys와 통합 된 취약성 평가 대 한 클라우드 에이전트는 가상 컴퓨터 권장 구성의 일부분으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="d2723-214">hello Qualys 에이전트 취약점 데이터 toohello Qualys 관리 플랫폼으로, 다음 백업 tooASC 취약점와 상태 모니터링 데이터를 전송 하는 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="d2723-215">취약성 평가 솔루션 hello에 표시 되는 권장 사항 tooadd hello **권장 사항을** hello ASC 대시보드에서 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="d2723-216">Hello 취약점 평가 솔루션 hello 대상 VM에 설치 된 후에 보안 센터 검색 VM toodetect hello 및 시스템 및 응용 프로그램 보안 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="d2723-217">문제는 hello 아래에 표시 된 검색 **가상 컴퓨터의 권장 사항을** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="d2723-218">취약성 평가 솔루션을 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d2723-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="d2723-219">통합된 취약성 평가 솔루션이 Virtual Machine에 아직 배포되지 않았으면 Security Center에 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="d2723-220">Hello ASC 대시보드 hello에서에서 **권장 사항을** 블레이드를 **취약점 평가 솔루션을 추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2723-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="d2723-221">Hello Vm tooinstall hello 취약점 평가 솔루션을 원하는 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="d2723-222">**[수]개 VM에 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="d2723-223">Hello Azure 마켓플레이스 또는 파트너 솔루션 선택 **기존 솔루션을 사용 하 여** 선택 **Qualys 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2723-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="d2723-224">Hello hello 자동 업데이트 설정 또는 해제를 해제할 수 **파트너 솔루션** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2723-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="d2723-225">자세한 방법에 대 한 tooimplement 취약점 평가 솔루션 참조 [Azure 보안 센터에 대 한 취약점 평가 합니다.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="d2723-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2723-226">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2723-226">Next steps</span></span>

- [<span data-ttu-id="d2723-227">Azure Security Center 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="d2723-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="d2723-228">소개 tooAzure 보안 센터</span><span class="sxs-lookup"><span data-stu-id="d2723-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="d2723-229">Azure 로그 통합에 Azure Security Center 경고 통합</span><span class="sxs-lookup"><span data-stu-id="d2723-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="d2723-230">통합된 취약성 평가를 통한 Azure Security Center 강화(영문)</span><span class="sxs-lookup"><span data-stu-id="d2723-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
