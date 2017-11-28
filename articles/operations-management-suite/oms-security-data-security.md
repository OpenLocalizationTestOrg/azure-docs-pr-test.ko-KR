---
title: "관리 도구 모음 보안 및 감사 솔루션 데이터 보안 aaaOperations | Microsoft Docs"
description: "이 문서에서는 데이터를 Operations Management Suite 보안 및 감사 솔루션에서 데이터를 관리하고 보호하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="6eaaa-103">Operations Management Suite 보안 및 감사 솔루션 데이터 보안</span><span class="sxs-lookup"><span data-stu-id="6eaaa-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="6eaaa-104">toohelp 고객 방지 감지 하 고 toothreats, 응답 [Operations Management Suite (OMS) 보안 및 감사 솔루션](operations-management-suite-overview.md) 수집 하 고 포함 하는 리소스에 대 한 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="6eaaa-105">보안 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="6eaaa-105">Security event log</span></span>
* <span data-ttu-id="6eaaa-106">Windows (ETW) 이벤트에 대한 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="6eaaa-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="6eaaa-107">AppLocker 감사 이벤트</span><span class="sxs-lookup"><span data-stu-id="6eaaa-107">AppLocker auditing events</span></span>
* <span data-ttu-id="6eaaa-108">Windows 방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="6eaaa-108">Windows Firewall log</span></span>
* <span data-ttu-id="6eaaa-109">고급 위협 분석 이벤트</span><span class="sxs-lookup"><span data-stu-id="6eaaa-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="6eaaa-110">기준 평가 결과</span><span class="sxs-lookup"><span data-stu-id="6eaaa-110">Results of baseline assessment</span></span>
* <span data-ttu-id="6eaaa-111">맬웨어 방지 평가 결과</span><span class="sxs-lookup"><span data-stu-id="6eaaa-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="6eaaa-112">업데이트/패치 평가 결과</span><span class="sxs-lookup"><span data-stu-id="6eaaa-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="6eaaa-113">Hello 에이전트에 명시적으로 설정 되어 있는 Syslogs 스트림</span><span class="sxs-lookup"><span data-stu-id="6eaaa-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="6eaaa-114">강력한 약정 tooprotect hello 개인 정보 및이 데이터의 보안으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="6eaaa-115">Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="6eaaa-116">이 문서에서는 OMS 보안 및 감사 솔루션에서 데이터를 관리하고 보호하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="6eaaa-117">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="6eaaa-117">Data sources</span></span>
<span data-ttu-id="6eaaa-118">OMS 보안 및 감사 솔루션에는 hello OMS 에이전트를 설치한 가상 컴퓨터와 물리적 컴퓨터에서 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="6eaaa-119">OMS 보안 및 감사 솔루션에서는 Windows 이벤트, 감사 로그, IIS 로그 및 syslog 메시지와 같은 보안 이벤트에 대한 구성 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="6eaaa-120">이러한 데이터의 예: 운영 체제 유형 및 버전, 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="6eaaa-121">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="6eaaa-121">Data protection</span></span>
<span data-ttu-id="6eaaa-122">**데이터 분리**: 데이터 hello 서비스 전체에서 각 구성 요소에 논리적으로 별도로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="6eaaa-123">모든 데이터에는 조직별로 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-123">All data is tagged per organization.</span></span> <span data-ttu-id="6eaaa-124">이 태그 hello 데이터 수명 주기 동안 유지 되며 hello 서비스의 각 계층에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="6eaaa-125">**데이터 액세스**: tooprovide 보안 권장 사항 및 보안 위협 조사, Microsoft 담당자 수집 또는 서비스에 의해 분석 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="6eaaa-126">Toohello 준수 우리 [Microsoft 온라인 서비스 약관](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) 및 [개인정보취급방침](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), Microsoft가 고객 데이터를 사용 하 여 만들어지거나 한 보급 또는 유사한에서 정보를 파생 되지 않습니다 상태 상업적 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="6eaaa-127">tooprovide 보안 권장 사항 및 보안 위협 조사, Microsoft 담당자 수집 또는 서비스에 의해 분석 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="6eaaa-128">만 고객 데이터를 사용 하 여 필요한 tooprovide 목적으로 서비스를 제공 호환 비롯 하 여 서비스는 Azure로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="6eaaa-129">모든 권한 tooyour 직접 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="6eaaa-130">**데이터 사용**: 패턴을 사용 하 여 Microsoft 및 위협 인텔리전스 표시를 여러 테 넌 트에서 tooenhance 취급 예방 및 감지 기능;에 설명 된 hello 개인 정보 행에 따라 이렇게 우리의 [개인 정보 문](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6eaaa-131">데이터 위치 hello 작업 영역을 만드는 동안 hello 초기 OMS 보안 및 감사 구성 프로세스의 일부인 hello OMS 작업 영역 수준에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="6eaaa-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6eaaa-132">See also</span></span>
<span data-ttu-id="6eaaa-133">이 문서에서는 OMS에서 데이터를 관리하고 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6eaaa-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="6eaaa-134">OMS 보안 및 감사 솔루션에 대해 자세히 toolearn 참조:</span><span class="sxs-lookup"><span data-stu-id="6eaaa-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="6eaaa-135">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="6eaaa-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="6eaaa-136">모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고</span><span class="sxs-lookup"><span data-stu-id="6eaaa-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="6eaaa-137">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="6eaaa-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

