---
title: "보안 센터 위협 인텔리전스 보고서 aaaAzure | Microsoft Docs"
description: "이 문서를 사용 하면 toouse Azure 보안 센터 위협 지능형 보고서 조사 toofind 하는 동안 보안 경고에 대 한 자세한 정보."
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
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="de5be-103">Azure Security Center 위협 인텔리전스 보고서</span><span class="sxs-lookup"><span data-stu-id="de5be-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="de5be-104">이 문서에서는 Azure Security Center 위협 인텔리전스 보고서를 사용하여 보안 경고를 생성한 위협에 관한 자세한 정보를 확인하는 방식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="de5be-105">위협 인텔리전스 보고서란?</span><span class="sxs-lookup"><span data-stu-id="de5be-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="de5be-106">보안 센터 위협 요소 탐지 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 모니터링 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-106">Security Center threat detection works by monitoring security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="de5be-107">이 정보를 종종 tooidentify 위협 여러 소스의 정보 상관 관계를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-107">It analyzes this information, often correlating information from multiple sources, tooidentify threats.</span></span> <span data-ttu-id="de5be-108">이 프로세스는 hello 보안 센터의 일부 [검색 기능이](security-center-detection-capabilities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-108">This process is part of hello Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="de5be-109">Security Center에서 위협을 식별하면 [보안 경고](security-center-managing-and-responding-alerts.md)를 트리거하며, 여기에는 수정 제안을 포함하여 특정 이벤트와 관련된 자세한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="de5be-110">보안 센터 등의 정보를 비롯 하 여 검색 된 hello 위협에 대 한 정보를 포함 하는 위협 인텔리전스 보고서에 포함 되어 tooassist 사고 대응 팀 조사 및 재구성 위협은:</span><span class="sxs-lookup"><span data-stu-id="de5be-110">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="de5be-111">공격자의 ID 또는 연결(이 정보가 제공되는 경우)</span><span class="sxs-lookup"><span data-stu-id="de5be-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="de5be-112">공격자의 목표</span><span class="sxs-lookup"><span data-stu-id="de5be-112">Attackers’ objectives</span></span>
* <span data-ttu-id="de5be-113">현재 및 과거 공격 캠페인(이 정보가 제공되는 경우)</span><span class="sxs-lookup"><span data-stu-id="de5be-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="de5be-114">공격자의 전술, 도구 및 프로시저</span><span class="sxs-lookup"><span data-stu-id="de5be-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="de5be-115">URL, 파일 해시 등 관련 IoC(보안 침해 지표)</span><span class="sxs-lookup"><span data-stu-id="de5be-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="de5be-116">Hello 업계 및 지리적 널리 tooassist victimology 위험이 있습니다. Azure 리소스 하는지 여부를 확인 하면</span><span class="sxs-lookup"><span data-stu-id="de5be-116">Victimology, which is hello industry and geographic prevalence tooassist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="de5be-117">마이그레이션 및 수정 정보</span><span class="sxs-lookup"><span data-stu-id="de5be-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="de5be-118">특정 보고서의 정보 양을 hello 달라 집니다. hello 수준의 세부 정보는 hello 맬웨어 활동 및 보급을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-118">hello amount of information in any particular report will vary; hello level of detail is based on hello malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="de5be-119">보안 센터에 세 가지 유형의 toohello 공격에 따라 다를 수 있는 위협 보고서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-119">Security Center has three types of threat reports, which can vary according toohello attack.</span></span> <span data-ttu-id="de5be-120">사용할 수 있는 hello 보고서에는</span><span class="sxs-lookup"><span data-stu-id="de5be-120">hello reports available are:</span></span>

* <span data-ttu-id="de5be-121">**그룹 활동 보고서** - 공격자 및 이들의 목표와 전술에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="de5be-122">**캠페인 보고서**: 특정 공격 캠페인의 세부 정보에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="de5be-123">**요약 보고서 위협**: hello에 모든 항목의 hello 이전 두 보고서에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-123">**Threat Summary Report**: covers all of hello items in hello previous two reports.</span></span>

<span data-ttu-id="de5be-124">Hello 하는 동안 이러한 종류의 정보는 매우 유용 [사고 대응](security-center-incident-response.md) hello 공격, hello 공격자의 동기 및 작업의 진행 중인 조사 toounderstand hello 소스는 프로세스 toodo toomitigate이 문제를 앞으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-124">This type of information is very useful during hello [incident response](security-center-incident-response.md) process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

## <a name="how-tooaccess-hello-threat-intelligence-report"></a><span data-ttu-id="de5be-125">어떻게 tooaccess 위협 인텔리전스 보고서 hello?</span><span class="sxs-lookup"><span data-stu-id="de5be-125">How tooaccess hello threat intelligence report?</span></span>
<span data-ttu-id="de5be-126">Hello 확인 하 여 현재 경고를 검토할 수 있습니다 **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-126">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="de5be-127">Hello Azure 포털을 열고 각 경고에 대 한 자세한 내용은 아래 toosee hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-127">Open hello Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="de5be-128">Hello 보안 센터 대시보드에서 hello 나타납니다 **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-128">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>
2. <span data-ttu-id="de5be-129">Hello 타일 tooopen hello 클릭 **보안 경고** 블레이드 hello 경고에 대 한 자세한 내용은 포함 된 추가 정보를 원하는 tooobtain hello 보안 경고가 클릭에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-129">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts and click in hello security alert that you want tooobtain more information about.</span></span>

    ![보안 경고](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="de5be-131">이 경우 hello **실행 된 의심 스러운 프로세스** 블레이드 아래 hello 그림에 나와 있는 것 처럼 hello 경고에 대 한 hello 세부 정보를 표시 합니다.:</span><span class="sxs-lookup"><span data-stu-id="de5be-131">In this case hello **Suspicious process executed** blade shows hello details about hello alert as shown in hello figure below:</span></span>

    ![보안 경고 세부 정보](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="de5be-133">각 보안 경고에 대해 사용할 수 있는 정보의 양을 hello 경고 toohello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-133">hello amount of information available for each security alert will vary according toohello type of alert.</span></span> <span data-ttu-id="de5be-134">Hello에 **보고서** 링크 toohello 위협 인텔리전스 보고서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-134">In hello **REPORTS** field you have a link toohello threat intelligence report.</span></span> <span data-ttu-id="de5be-135">해당 링크를 클릭하면 다른 브라우저 창에서 PDF 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![저장소 선택](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="de5be-137">여기에서 hello이 보고서와을 발급할 보안 hello에 대 한 자세한 읽기에 대 한 PDF 검색 되었습니다를 다운로드 하 고 제공 하는 hello 정보에 따라 동작을 수행할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-137">From here you can download hello PDF for this report and read more about hello security issue that was detected and take actions based on hello information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="de5be-138">참고 항목</span><span class="sxs-lookup"><span data-stu-id="de5be-138">See also</span></span>
<span data-ttu-id="de5be-139">이 문서에서는 보안 경고에 대해 조사하는 중에 Azure Security Center 위협 인텔리전스 보고서를 사용 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="de5be-140">Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-140">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="de5be-141">[Azure Security Center FAQ](security-center-faq.md)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="de5be-142">Hello 서비스를 사용 하는 방법에 대 한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-142">Find frequently asked questions about using hello service.</span></span>
* [<span data-ttu-id="de5be-143">사고 대응에 Azure Security Center 활용</span><span class="sxs-lookup"><span data-stu-id="de5be-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="de5be-144">Azure Security Center 감지 기능</span><span class="sxs-lookup"><span data-stu-id="de5be-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="de5be-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="de5be-146">자세한 내용은 방법 tooplan hello 디자인 고려 사항 tooadopt Azure 보안 센터를 이해 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-146">Learn how tooplan and understand hello design considerations tooadopt Azure Security Center.</span></span>
* <span data-ttu-id="de5be-147">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-147">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="de5be-148">자세한 내용은 방법 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-148">Learn how toomanage and respond toosecurity alerts.</span></span>
* [<span data-ttu-id="de5be-149">Azure 보안 센터에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="de5be-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="de5be-150">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="de5be-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="de5be-151">Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="de5be-151">Find blog posts about Azure security and compliance.</span></span>
