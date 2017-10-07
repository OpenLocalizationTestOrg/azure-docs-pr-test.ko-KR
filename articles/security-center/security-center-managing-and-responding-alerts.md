---
title: "Azure 보안 센터에서 보안 경고 aaaManage | Microsoft Docs"
description: "이 문서 있습니다 toouse Azure 보안 센터 기능 toomanage 주며 toosecurity 경고에 응답 합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="cf8f2-103">관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답</span><span class="sxs-lookup"><span data-stu-id="cf8f2-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="cf8f2-104">이 문서를 사용 하면 Azure 보안 센터 toomanage를 사용 하 여 고 toosecurity 경고 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8f2-105">보안 센터 표준 업그레이드 tooAzure 고급 tooenable 길어도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="cf8f2-106">무료 60일 평가판을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-106">A free 60-day trial is available.</span></span> <span data-ttu-id="cf8f2-107">tooupgrade, hello에서 가격 책정 계층을 선택 [보안 정책](security-center-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="cf8f2-108">참조 [Azure 보안 센터 가격](security-center-pricing.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="cf8f2-109">보안 경고란?</span><span class="sxs-lookup"><span data-stu-id="cf8f2-109">What are security alerts?</span></span>
<span data-ttu-id="cf8f2-110">보안 센터 자동으로 수집, 분석, 및 Azure 리소스로 hello 네트워크에서 로그 데이터를 통합 및 파트너 솔루션 방화벽 및 endpoint protection 솔루션과 toodetect 실제 위협 같은 연결 및 거짓 긍정을 줄일 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="cf8f2-111">Hello와 함께 보안 센터에서 우선 순위가 지정 된 보안 경고의 목록이 표시 됩니다 hello 문제 및 방법에 대 한 권장 사항 tooquickly 필요한 정보를 조사 tooremediate 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="cf8f2-112">보안 센터 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure 보안 센터 감지 기능](security-center-detection-capabilities.md)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="cf8f2-113">보안 경고 관리</span><span class="sxs-lookup"><span data-stu-id="cf8f2-113">Managing security alerts</span></span>
<span data-ttu-id="cf8f2-114">Hello 확인 하 여 현재 경고를 검토할 수 있습니다 **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="cf8f2-115">Azure 포털을 열고 각 경고에 대 한 자세한 내용은 아래 toosee hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="cf8f2-116">Hello 보안 센터 대시보드에서 hello 나타납니다 **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![보안 센터의 보안 경고 타일](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="cf8f2-118">Hello 타일 tooopen hello 클릭 **보안 경고** 블레이드 hello에 대 한 자세한 정보를 포함 하는 아래와 같이 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![보안 센터에 hello 보안 경고 블레이드](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="cf8f2-120">이 블레이드의 hello 아래쪽 부분에은 각 경고에 대 한 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="cf8f2-121">toosort, toosort 하 여 원하는 hello 열을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="cf8f2-122">각 열에 대 한 hello 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="cf8f2-123">**설명**: hello 경고에 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="cf8f2-124">**개수**: 특정 날짜에서 감지한 이 특정 형식의 모든 경고 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="cf8f2-125">**검색 된**: hello 서비스는 hello 경고 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="cf8f2-126">**날짜**: hello 날짜 해당 hello 이벤트가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="cf8f2-127">**상태**: hello 해당 경고에 대 한 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="cf8f2-128">다음과 같은 두 가지 종류의 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-128">There are two types of states:</span></span>
  * <span data-ttu-id="cf8f2-129">**활성**: hello 보안 경고가 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="cf8f2-130">**심각도**: hello 심각도 높음, 중간 또는 낮은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="cf8f2-131">경고 필터링</span><span class="sxs-lookup"><span data-stu-id="cf8f2-131">Filtering alerts</span></span>
<span data-ttu-id="cf8f2-132">날짜, 상태 및 심각도를 기반으로 경고를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="cf8f2-133">경고를 필터링 하는 것은 toonarrow hello 범위의 보안 경고 표시 해야 하는 시나리오에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="cf8f2-134">예를 들어 수 있습니다 있습니다에서 발생 한 hello 지난 24 시간 동안 hello 시스템에 잠재적 위반을 조사 하는 중 이므로 tooaddress 보안 경고를 발생 시킬 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="cf8f2-135">클릭 **필터** hello에 **보안 경고** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="cf8f2-136">hello **필터** 블레이드가 열리고 toosee 원하는 hello 날짜, 상태 및 심각도 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![보안 센터에서 경고 필터링](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="cf8f2-138">Toosecurity 경고에 응답</span><span class="sxs-lookup"><span data-stu-id="cf8f2-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="cf8f2-139">보안 경고 toolearn 선택 tootake tooremediate 공격 hello 캡처할 이벤트를 발생 시킨 hello 알림과 부분, any, 과정을 설명 하는 경우에 대 한 자세한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="cf8f2-140">보안 경고는 형식 및 날짜별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="cf8f2-141">보안 경고를 클릭 하면 그룹화 된 hello 경고 목록이 포함 된 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Azure 보안 센터에서 toosecurity 경고에 응답](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="cf8f2-143">이 경우 트리거된 hello 경고는 toosuspicious 프로토콜 RDP (원격 데스크톱) 활동을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="cf8f2-144">리소스 공격 받은; hello 첫 번째 열 표시 두 번째 hello hello 리소스 공격 했습니다; 실패 한 횟수 세 번째 hello hello 공격; hello 시간 네 번째 hello hello 경고;의 상태 하며 hello 다섯째 hello 공격의 hello 심각도 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="cf8f2-145">이 정보를 검토 한 후 공격 된 hello 리소스를 클릭 하 고는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Azure 보안 센터에서 어떤 toodo 보안에 대 한 경고에 대 한 제안](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="cf8f2-147">Hello에 **설명** 이 블레이드 필드이 이벤트에 대 한 자세한 내용은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="cf8f2-148">이러한 세부 정보는 해당 hello 원본 IP 주소 및 방법에 대 한 권장 사항을 때 어떤 트리거된 hello 보안 경고를 hello 대상 리소스에 대 한 정보를 제공 tooremediate 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="cf8f2-149">경우에 따라 hello 원본 IP 주소 수를 비우는 됩니다 (사용할 수 없음) 모든 Windows 보안 이벤트 로그 hello IP 주소를 포함 하기 때문에</span><span class="sxs-lookup"><span data-stu-id="cf8f2-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="cf8f2-150">보안 센터에 제안 된 hello 재구성 toohello 보안 경고에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="cf8f2-151">경우에 따라 할 수 있습니다 toouse 다른 Azure 기능 tooimplement hello 업데이트 관리를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="cf8f2-152">예를 들어이 공격 tooblacklist hello IP 주소를 사용 하 여 이러한 공격을 생성 하는 대 한 업데이트 관리를 hello는 [네트워크 ACL](../virtual-network/virtual-networks-acl.md) 또는 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8f2-153">경고의 hello 서로 다른 형식에 대 한 자세한 내용은 참조 하세요 [Azure 보안 센터에서 보안 경고](security-center-alerts-type.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="cf8f2-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cf8f2-154">See also</span></span>
<span data-ttu-id="cf8f2-155">이 문서에서는 방법에 대해 배웠습니다 tooconfigure 보안 정책 보안 센터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="cf8f2-156">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="cf8f2-157">Azure 보안 센터에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="cf8f2-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="cf8f2-158">Azure 보안 센터 감지 기능</span><span class="sxs-lookup"><span data-stu-id="cf8f2-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="cf8f2-159">Azure Security Center 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="cf8f2-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="cf8f2-160">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="cf8f2-161">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
