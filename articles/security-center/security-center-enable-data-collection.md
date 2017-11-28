---
title: "Azure Security Center에서 데이터 수집 활성화 | Microsoft Docs"
description: " Azure 보안 센터에서 데이터 수집을 활성화하는 방법을 알아봅니다. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 7e9ad8cd8c77c57c37dc208b86b3727a4e1dc7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a><span data-ttu-id="4cfc7-103">Azure 보안 센터에서 데이터 수집 활성화</span><span class="sxs-lookup"><span data-stu-id="4cfc7-103">Enable data collection in Azure Security Center</span></span>

> [!NOTE]
> <span data-ttu-id="4cfc7-104">2017년 6월 초를 시작으로 Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집 및 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-104">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="4cfc7-105">자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-105">To learn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="4cfc7-106">이 문서의 정보는 Microsoft Monitoring Agent로 전환된 후의 Security Center 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-106">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

<span data-ttu-id="4cfc7-107">Security Center는 해당 보안 상태를 평가하고 보안 권장 사항을 제공하며 위협에 경고하기 위해 VM(가상 컴퓨터)에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-107">Security Center collects data from your virtual machines (VMs) to assess their security state, provide security recommendations, and alert you to threats.</span></span> <span data-ttu-id="4cfc7-108">Security Center에 처음 액세스하는 경우 구독의 모든 VM에서 데이터 수집을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-108">When you first access Security Center, you have the option to enable data collection for all VMs in your subscription.</span></span> <span data-ttu-id="4cfc7-109">데이터 수집이 사용하도록 설정되지 않으면 Security Center는 해당 구독에 대한 보안 정책에서 데이터 수집을 켜도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-109">If data collection is not enabled, Security Center recommends that you turn on data collection in the security policy for that subscription.</span></span>

<span data-ttu-id="4cfc7-110">데이터 수집이 사용하도록 설정되면 Security Center는 지원되는 모든 기존 가상 컴퓨터 및 새로 만든 Azure 가상 컴퓨터에 Microsoft Monitoring Agent를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-110">When data collection is enabled, Security Center provisions the Microsoft Monitoring Agent on all existing supported Azure virtual machines and any new ones that are created.</span></span> <span data-ttu-id="4cfc7-111">Microsoft Monitoring Agent는 다양한 보안 관련 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-111">The Microsoft Monitoring Agent scans for various security-related configurations.</span></span> <span data-ttu-id="4cfc7-112">또한 운영 체제는 이벤트 로그 이벤트를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-112">In addition, the operating system raises event log events.</span></span> <span data-ttu-id="4cfc7-113">이러한 데이터의 예: 운영 체제 유형 및 버전, 운영 체제 로그(Windows 이벤트 로그), 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-113">Examples of such data are: operating system type and version, operating system logs (Windows event logs), running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span> <span data-ttu-id="4cfc7-114">Microsoft Monitoring Agent는 이벤트 로그 항목과 구성을 읽고 분석을 위해 작업 영역에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-114">The Microsoft Monitoring Agent reads event log entries and configurations and copies the data to your workspace for analysis.</span></span> <span data-ttu-id="4cfc7-115">또한 Microsoft Monitoring Agent는 작업 영역에 크래시 덤프 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-115">The Microsoft Monitoring Agent also copies crash dump files to your workspace.</span></span>

<span data-ttu-id="4cfc7-116">Security Center의 무료 계층을 사용하는 경우 보안 정책에서 데이터 수집 설정을 해제하여 가상 컴퓨터에서 데이터 수집을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-116">If you are using the Free tier of Security Center, you can disable data collection from virtual machines by turning off data collection in the security policy.</span></span> <span data-ttu-id="4cfc7-117">데이터 수집을 사용하지 않도록 설정하면 VM의 보안 평가가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-117">Disabling data collection limits security assessments for your VMs.</span></span> <span data-ttu-id="4cfc7-118">자세한 내용은 [데이터 수집 비활성화](#disabling-data-collection)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-118">To learn more, see [Disabling data collection](#disabling-data-collection).</span></span> <span data-ttu-id="4cfc7-119">VM 디스크 스냅숏 및 아티팩트 컬렉션은 데이터 수집이 사용하지 않도록 설정된 경우에도 여전히 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-119">VM disk snapshots and artifact collection are enabled even if data collection has been disabled.</span></span> <span data-ttu-id="4cfc7-120">데이터 수집은 Security Center의 표준 계층에 대한 구독에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-120">Data collection is required for subscriptions on the Standard tier of Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="4cfc7-121">Security Center의 무료 및 표준 계층에 대한 자세한 내용은 [가격 책정 계층](security-center-pricing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-121">Learn more about Security Center's Free and Standard [pricing tiers](security-center-pricing.md).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="4cfc7-122">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="4cfc7-122">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="4cfc7-123">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-123">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="4cfc7-124">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-124">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="4cfc7-125">**권장 사항** 블레이드에서 **구독에 대한 데이터 수집 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-125">In the **Recommendations** blade, select **Enable data collection for subscriptions**.</span></span>  <span data-ttu-id="4cfc7-126">그러면 **데이터 수집 켜기** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-126">This opens the **Turn on data collection** blade.</span></span>
   <span data-ttu-id="4cfc7-127">![권장 사항 블레이드][2]</span><span class="sxs-lookup"><span data-stu-id="4cfc7-127">![Recommendations blade][2]</span></span>
2. <span data-ttu-id="4cfc7-128">**데이터 수집 켜기** 블레이드에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-128">On the **Turn on data collection** blade, select your subscription.</span></span> <span data-ttu-id="4cfc7-129">해당 구독에 대한 **보안 정책** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-129">The **Security policy** blade for that subscription opens.</span></span>
3. <span data-ttu-id="4cfc7-130">**보안 정책** 블레이드에서 자동으로 로그를 수집하도록 **데이터 컬렉션**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-130">On the **Security policy** blade, select **On** under **Data collection** to automatically collect logs.</span></span> <span data-ttu-id="4cfc7-131">데이터 컬렉션을 켜면 구독에 현재 포함된 VM과 지원되는 새 VM에 모니터링 확장이 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-131">Turning on data collection provisions the monitoring extension on all current and new supported VMs in the subscription.</span></span>
4. <span data-ttu-id="4cfc7-132">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-132">Select **Save**.</span></span>
5. <span data-ttu-id="4cfc7-133">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-133">Select **OK**.</span></span>

## <a name="disabling-data-collection"></a><span data-ttu-id="4cfc7-134">데이터 수집 비활성화</span><span class="sxs-lookup"><span data-stu-id="4cfc7-134">Disabling data collection</span></span>
<span data-ttu-id="4cfc7-135">Security Center의 무료 계층을 사용하는 경우 보안 정책에서 데이터 수집을 해제하여 언제든지 가상 컴퓨터에서 데이터 수집을 사용하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-135">If you are using the Free tier of Security Center, you can disable data collection from virtual machines at any time by turning off data collection in the security policy.</span></span> <span data-ttu-id="4cfc7-136">데이터 수집은 Security Center의 표준 계층에 대한 구독에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-136">Data collection is required for subscriptions on the Standard tier of Security Center.</span></span>

1. <span data-ttu-id="4cfc7-137">**Security Center** 블레이드로 돌아가서 **정책** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-137">Return to the **Security Center** blade and select the **Policy** tile.</span></span> <span data-ttu-id="4cfc7-138">그러면 **보안 정책–구독별로 정책 정의** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-138">This opens the **Security policy-Define policy per subscription** blade.</span></span>
   <span data-ttu-id="4cfc7-139">![정책 타일 선택][5]</span><span class="sxs-lookup"><span data-stu-id="4cfc7-139">![Select the policy tile][5]</span></span>
2. <span data-ttu-id="4cfc7-140">**보안 정책–구독별로 정책 정의** 블레이드에서 데이터 수집을 사용하지 않도록 설정하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-140">On the **Security policy-Define policy per subscription** blade, select the subscription that you wish to disable data collection.</span></span>
3. <span data-ttu-id="4cfc7-141">해당 구독에 대한 **보안 정책** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-141">The **Security policy** blade for that subscription opens.</span></span>  <span data-ttu-id="4cfc7-142">데이터 컬렉션에서 **끄기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-142">Select **Off** under Data collection.</span></span>
4. <span data-ttu-id="4cfc7-143">상단 리본에서 **저장** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-143">Select **Save** in the top ribbon.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cfc7-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4cfc7-144">Next steps</span></span>
<span data-ttu-id="4cfc7-145">이 문서에서는 보안 센터 권장 사항 "데이터 수집 활성화"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-145">This article showed you how to implement the Security Center recommendation "Enable data collection.”</span></span> <span data-ttu-id="4cfc7-146">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-146">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="4cfc7-147">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-147">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4cfc7-148">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-148">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4cfc7-149">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)--Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-149">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="4cfc7-150">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)--보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-150">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="4cfc7-151">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-151">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="4cfc7-152">[Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-152">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="4cfc7-153">[Azure 보안 센터 FAQ](security-center-faq.md)--서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-153">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="4cfc7-154">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cfc7-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
