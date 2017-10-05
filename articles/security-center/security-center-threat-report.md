---
title: "Azure Security Center 위협 인텔리전스 보고서 | Microsoft Docs"
description: "이 문서는 조사하는 중에 Azure Security Center 위협 인텔리전스 보고서를 사용하여 보안 경고에 관한 자세한 정보를 확인하는 데 도움이 됩니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: b4310cf4e6849c67031b3ec8b1fd5957e35f7ea6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="7e5a3-103">Azure Security Center 위협 인텔리전스 보고서</span><span class="sxs-lookup"><span data-stu-id="7e5a3-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="7e5a3-104">이 문서에서는 Azure Security Center 위협 인텔리전스 보고서를 사용하여 보안 경고를 생성한 위협에 관한 자세한 정보를 확인하는 방식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="7e5a3-105">위협 인텔리전스 보고서란?</span><span class="sxs-lookup"><span data-stu-id="7e5a3-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="7e5a3-106">Security Center 위협 감지는 Azure 리소스, 네트워크 및 연결된 파트너 솔루션의 보안 정보를 모니터링함으로써 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="7e5a3-107">위협을 식별하도록 종종 여러 소스의 정보를 상호 연결하는 이 정보를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span> <span data-ttu-id="7e5a3-108">이 프로세스는 Security Center [감지 기능](security-center-detection-capabilities.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="7e5a3-109">Security Center에서 위협을 식별하면 [보안 경고](security-center-managing-and-responding-alerts.md)를 트리거하며, 여기에는 수정 제안을 포함하여 특정 이벤트와 관련된 자세한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="7e5a3-110">사고 대응 팀이 위협을 조사하고 수정하도록 지원하기 위해 Security Center에는 아래와 같은 정보를 포함하여 감지된 위협에 관한 정보를 포함하고 있는 위협 인텔리전스 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="7e5a3-111">공격자의 ID 또는 연결(이 정보가 제공되는 경우)</span><span class="sxs-lookup"><span data-stu-id="7e5a3-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="7e5a3-112">공격자의 목표</span><span class="sxs-lookup"><span data-stu-id="7e5a3-112">Attackers’ objectives</span></span>
* <span data-ttu-id="7e5a3-113">현재 및 과거 공격 캠페인(이 정보가 제공되는 경우)</span><span class="sxs-lookup"><span data-stu-id="7e5a3-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="7e5a3-114">공격자의 전술, 도구 및 프로시저</span><span class="sxs-lookup"><span data-stu-id="7e5a3-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="7e5a3-115">URL, 파일 해시 등 관련 IoC(보안 침해 지표)</span><span class="sxs-lookup"><span data-stu-id="7e5a3-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="7e5a3-116">피해자 유형(Azure 리소스가 위험한 상태에 있는지 결정하는 데 도움이 되는 산업적 유행 및 지리적 유행)</span><span class="sxs-lookup"><span data-stu-id="7e5a3-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="7e5a3-117">마이그레이션 및 수정 정보</span><span class="sxs-lookup"><span data-stu-id="7e5a3-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="7e5a3-118">세부 수준이 맬웨어 활동 및 유행에 기반하기 때문에 특정 보고서의 정보 량은 다양하게 변합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="7e5a3-119">Security Center에는 세 가지 유형의 위협 보고서가 있는데 공격에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-119">Security Center has three types of threat reports, which can vary according to the attack.</span></span> <span data-ttu-id="7e5a3-120">제공되는 보고서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-120">The reports available are:</span></span>

* <span data-ttu-id="7e5a3-121">**그룹 활동 보고서** - 공격자 및 이들의 목표와 전술에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="7e5a3-122">**캠페인 보고서**: 특정 공격 캠페인의 세부 정보에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="7e5a3-123">**위협 요약 보고서**: 이전 두 보고서의 모든 항목을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span></span>

<span data-ttu-id="7e5a3-124">이러한 종류의 정보는 지속적인 조사를 통해 공격의 원천, 공격자의 동기 및 계속 진행되는 문제를 완화하기 위해 수행할 작업을 파악하는 [사고 대응](security-center-incident-response.md) 프로세스에서 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

## <a name="how-to-access-the-threat-intelligence-report"></a><span data-ttu-id="7e5a3-125">어떻게 위협 인텔리전스 보고서에 액세스하는가?</span><span class="sxs-lookup"><span data-stu-id="7e5a3-125">How to access the threat intelligence report?</span></span>
<span data-ttu-id="7e5a3-126">**보안 경고** 타일을 확인하여 현재 경고를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-126">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="7e5a3-127">Azure Portal을 열고 다음 단계를 수행하여 각 경고에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="7e5a3-128">보안 센터 대시보드에서 **보안 경고** 타일을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>
2. <span data-ttu-id="7e5a3-129">해당 타일을 클릭하여 경고에 대한 자세한 정보를 포함한 **보안 경고** 블레이드를 연 다음 자세한 정보를 가져오려는 보안 경고를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span></span>

    ![보안 경고](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="7e5a3-131">이 경우 아래 그림에서 보여 주듯이 **의심스러운 프로세스 실행** 블레이드에서 경고에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span></span>

    ![보안 경고 세부 정보](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="7e5a3-133">각 보안 경고에 제공되는 정보 량은 경고 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-133">The amount of information available for each security alert will vary according to the type of alert.</span></span> <span data-ttu-id="7e5a3-134">**보고서** 필드에는 위협 인텔리전스 보고서에 대한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-134">In the **REPORTS** field you have a link to the threat intelligence report.</span></span> <span data-ttu-id="7e5a3-135">해당 링크를 클릭하면 다른 브라우저 창에서 PDF 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![저장소 선택](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="7e5a3-137">여기서는 해당 보고서의 PDF 파일을 다운로드하여 감지된 보안 문제에 대해 자세히 파악하고 제공된 정보에 기반한 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="7e5a3-138">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7e5a3-138">See also</span></span>
<span data-ttu-id="7e5a3-139">이 문서에서는 보안 경고에 대해 조사하는 중에 Azure Security Center 위협 인텔리전스 보고서를 사용 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="7e5a3-140">Azure 보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-140">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="7e5a3-141">[Azure 보안 센터 FAQ](security-center-faq.md)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="7e5a3-142">서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-142">Find frequently asked questions about using the service.</span></span>
* [<span data-ttu-id="7e5a3-143">사고 대응에 Azure Security Center 활용</span><span class="sxs-lookup"><span data-stu-id="7e5a3-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="7e5a3-144">Azure Security Center 감지 기능</span><span class="sxs-lookup"><span data-stu-id="7e5a3-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="7e5a3-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="7e5a3-146">디자인 고려 사항을 계획하고 이해하여 Azure Security Center를 채택하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="7e5a3-147">[Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7e5a3-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="7e5a3-148">보안 경고를 관리하고 응답하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-148">Learn how to manage and respond to security alerts.</span></span>
* [<span data-ttu-id="7e5a3-149">Azure 보안 센터에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="7e5a3-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="7e5a3-150">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="7e5a3-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="7e5a3-151">Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a3-151">Find blog posts about Azure security and compliance.</span></span>
