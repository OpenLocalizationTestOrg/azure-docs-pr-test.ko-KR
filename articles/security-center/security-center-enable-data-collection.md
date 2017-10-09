---
title: "Azure 보안 센터에서 데이터 수집 aaaEnable | Microsoft Docs"
description: " 자세한 내용은 방법 Azure 보안 센터에서 tooenable 데이터 컬렉션입니다. "
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
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a><span data-ttu-id="3e641-103">Azure 보안 센터에서 데이터 수집 활성화</span><span class="sxs-lookup"><span data-stu-id="3e641-103">Enable data collection in Azure Security Center</span></span>

> [!NOTE]
> <span data-ttu-id="3e641-104">보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-104">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="3e641-105">toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-105">toolearn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="3e641-106">이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-106">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>
>

<span data-ttu-id="3e641-107">보안 센터에서에서 데이터를 수집한 가상 컴퓨터 (Vm) tooassess 자신의 보안 상태, 보안 권장 사항을 제공 하 고 있습니다 toothreats 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-107">Security Center collects data from your virtual machines (VMs) tooassess their security state, provide security recommendations, and alert you toothreats.</span></span> <span data-ttu-id="3e641-108">보안 센터를 처음 사용할 때는 구독에서 모든 Vm에 대 한 hello 옵션 tooenable 데이터 수집을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-108">When you first access Security Center, you have hello option tooenable data collection for all VMs in your subscription.</span></span> <span data-ttu-id="3e641-109">데이터 수집을 사용 하지 않는 경우 해당 구독에 대 한 보안 정책 hello 데이터 수집을 켭니다 보안 센터 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-109">If data collection is not enabled, Security Center recommends that you turn on data collection in hello security policy for that subscription.</span></span>

<span data-ttu-id="3e641-110">데이터 수집을 사용 하는 경우 Azure 가상 컴퓨터 및 만들어진 새로 프로 비전 hello Microsoft Monitoring Agent에 모든 기존 보안 센터 지원.</span><span class="sxs-lookup"><span data-stu-id="3e641-110">When data collection is enabled, Security Center provisions hello Microsoft Monitoring Agent on all existing supported Azure virtual machines and any new ones that are created.</span></span> <span data-ttu-id="3e641-111">Microsoft Monitoring Agent hello 다양 한 보안 관련 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-111">hello Microsoft Monitoring Agent scans for various security-related configurations.</span></span> <span data-ttu-id="3e641-112">또한 hello 운영 체제 이벤트 로그 이벤트를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-112">In addition, hello operating system raises event log events.</span></span> <span data-ttu-id="3e641-113">이러한 데이터의 예: 운영 체제 유형 및 버전, 운영 체제 로그(Windows 이벤트 로그), 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-113">Examples of such data are: operating system type and version, operating system logs (Windows event logs), running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span> <span data-ttu-id="3e641-114">Microsoft Monitoring Agent hello 이벤트 로그 항목 및 구성 읽고 분석용 hello 데이터 tooyour 작업 영역을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-114">hello Microsoft Monitoring Agent reads event log entries and configurations and copies hello data tooyour workspace for analysis.</span></span> <span data-ttu-id="3e641-115">또한 Microsoft Monitoring Agent hello 크래시 덤프 파일 tooyour 작업 영역을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-115">hello Microsoft Monitoring Agent also copies crash dump files tooyour workspace.</span></span>

<span data-ttu-id="3e641-116">보안 센터의 무료 계층 hello를 사용 하는 경우에 hello 보안 정책에서 데이터 수집을 해제 하 여 가상 컴퓨터에서 데이터 수집을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-116">If you are using hello Free tier of Security Center, you can disable data collection from virtual machines by turning off data collection in hello security policy.</span></span> <span data-ttu-id="3e641-117">데이터 수집을 사용하지 않도록 설정하면 VM의 보안 평가가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-117">Disabling data collection limits security assessments for your VMs.</span></span> <span data-ttu-id="3e641-118">toolearn 더 참조 [데이터 수집을 사용 하지 않도록 설정](#disabling-data-collection)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-118">toolearn more, see [Disabling data collection](#disabling-data-collection).</span></span> <span data-ttu-id="3e641-119">VM 디스크 스냅숏 및 아티팩트 컬렉션은 데이터 수집이 사용하지 않도록 설정된 경우에도 여전히 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-119">VM disk snapshots and artifact collection are enabled even if data collection has been disabled.</span></span> <span data-ttu-id="3e641-120">데이터 컬렉션 보안 센터의 hello 표준 계층에 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-120">Data collection is required for subscriptions on hello Standard tier of Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="3e641-121">Security Center의 무료 및 표준 계층에 대한 자세한 내용은 [가격 책정 계층](security-center-pricing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e641-121">Learn more about Security Center's Free and Standard [pricing tiers](security-center-pricing.md).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="3e641-122">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="3e641-122">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="3e641-123">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-123">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="3e641-124">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-124">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="3e641-125">Hello에 **권장 사항을** 블레이드를 **구독에 대 한 데이터 컬렉션 활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-125">In hello **Recommendations** blade, select **Enable data collection for subscriptions**.</span></span>  <span data-ttu-id="3e641-126">Hello 열립니다 **데이터 컬렉션 켜기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-126">This opens hello **Turn on data collection** blade.</span></span>
   <span data-ttu-id="3e641-127">![권장 사항 블레이드][2]</span><span class="sxs-lookup"><span data-stu-id="3e641-127">![Recommendations blade][2]</span></span>
2. <span data-ttu-id="3e641-128">Hello에 **데이터 컬렉션 켜기** 블레이드에서 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-128">On hello **Turn on data collection** blade, select your subscription.</span></span> <span data-ttu-id="3e641-129">hello **보안 정책** 해당 구독에 대 한 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-129">hello **Security policy** blade for that subscription opens.</span></span>
3. <span data-ttu-id="3e641-130">Hello에 **보안 정책** 블레이드를 **에** 아래 **데이터 수집** tooautomatically 로그를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-130">On hello **Security policy** blade, select **On** under **Data collection** tooautomatically collect logs.</span></span> <span data-ttu-id="3e641-131">모든 현재와 새 데이터 컬렉션 프로 비전 hello 확장에 대 한 모니터링 설정 hello 구독에서는 Vm을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-131">Turning on data collection provisions hello monitoring extension on all current and new supported VMs in hello subscription.</span></span>
4. <span data-ttu-id="3e641-132">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-132">Select **Save**.</span></span>
5. <span data-ttu-id="3e641-133">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-133">Select **OK**.</span></span>

## <a name="disabling-data-collection"></a><span data-ttu-id="3e641-134">데이터 수집 비활성화</span><span class="sxs-lookup"><span data-stu-id="3e641-134">Disabling data collection</span></span>
<span data-ttu-id="3e641-135">보안 센터의 무료 계층 hello를 사용 하는 경우에 hello 보안 정책에서 데이터 수집을 해제 하 여 언제 든 지 가상 컴퓨터에서 데이터 수집을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-135">If you are using hello Free tier of Security Center, you can disable data collection from virtual machines at any time by turning off data collection in hello security policy.</span></span> <span data-ttu-id="3e641-136">데이터 컬렉션 보안 센터의 hello 표준 계층에 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-136">Data collection is required for subscriptions on hello Standard tier of Security Center.</span></span>

1. <span data-ttu-id="3e641-137">Toohello 반환 **보안 센터** 블레이드에 대 한 선택 hello **정책** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-137">Return toohello **Security Center** blade and select hello **Policy** tile.</span></span> <span data-ttu-id="3e641-138">Hello 열립니다 **구독 당 정책 보안 정책-정의** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-138">This opens hello **Security policy-Define policy per subscription** blade.</span></span>
   <span data-ttu-id="3e641-139">![Hello 정책 타일을 선택 합니다.][5]</span><span class="sxs-lookup"><span data-stu-id="3e641-139">![Select hello policy tile][5]</span></span>
2. <span data-ttu-id="3e641-140">Hello에 **구독 당 정책 보안 정책-정의** 블레이드, 선택 hello 구독 toodisable 데이터 수집 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-140">On hello **Security policy-Define policy per subscription** blade, select hello subscription that you wish toodisable data collection.</span></span>
3. <span data-ttu-id="3e641-141">hello **보안 정책** 해당 구독에 대 한 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-141">hello **Security policy** blade for that subscription opens.</span></span>  <span data-ttu-id="3e641-142">데이터 컬렉션에서 **끄기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-142">Select **Off** under Data collection.</span></span>
4. <span data-ttu-id="3e641-143">선택 **저장** hello 위쪽 리본 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-143">Select **Save** in hello top ribbon.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e641-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e641-144">Next steps</span></span>
<span data-ttu-id="3e641-145">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "사용 데이터 컬렉션입니다."</span><span class="sxs-lookup"><span data-stu-id="3e641-145">This article showed you how tooimplement hello Security Center recommendation "Enable data collection.”</span></span> <span data-ttu-id="3e641-146">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-146">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="3e641-147">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-147">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3e641-148">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-148">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3e641-149">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)-toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-149">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="3e641-150">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)-자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-150">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="3e641-151">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-151">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="3e641-152">[Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-152">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="3e641-153">[Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-153">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="3e641-154">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3e641-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
