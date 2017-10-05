---
title: "Operations Management Suite 보안 및 감사 솔루션 데이터 보안 | Microsoft Docs"
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
ms.openlocfilehash: 3b6327b1f5150f32afd71639f32c55d823f1d1f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="7b303-103">Operations Management Suite 보안 및 감사 솔루션 데이터 보안</span><span class="sxs-lookup"><span data-stu-id="7b303-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="7b303-104">고객이 위협을 방지, 감지하고 위협에 응답할 수 있도록 하려면 [OMS(Operations Management Suite) 보안 및 감사 솔루션](operations-management-suite-overview.md)에서는 다음을 포함하여 리소스에 대한 데이터를 수집하고 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="7b303-105">보안 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="7b303-105">Security event log</span></span>
* <span data-ttu-id="7b303-106">Windows (ETW) 이벤트에 대한 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="7b303-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="7b303-107">AppLocker 감사 이벤트</span><span class="sxs-lookup"><span data-stu-id="7b303-107">AppLocker auditing events</span></span>
* <span data-ttu-id="7b303-108">Windows 방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="7b303-108">Windows Firewall log</span></span>
* <span data-ttu-id="7b303-109">고급 위협 분석 이벤트</span><span class="sxs-lookup"><span data-stu-id="7b303-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="7b303-110">기준 평가 결과</span><span class="sxs-lookup"><span data-stu-id="7b303-110">Results of baseline assessment</span></span>
* <span data-ttu-id="7b303-111">맬웨어 방지 평가 결과</span><span class="sxs-lookup"><span data-stu-id="7b303-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="7b303-112">업데이트/패치 평가 결과</span><span class="sxs-lookup"><span data-stu-id="7b303-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="7b303-113">에이전트에 명시적으로 설정되어 있는 Syslogs 스트림</span><span class="sxs-lookup"><span data-stu-id="7b303-113">Syslogs streams that are explicitly enabled on the agent</span></span>

<span data-ttu-id="7b303-114">이 데이터의 개인 정보 보호 및 보안을 보호하기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-114">We make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="7b303-115">Microsoft는 코딩부터 서비스에 이르기까지 엄격한 규정 준수 및 보안 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span>
<span data-ttu-id="7b303-116">이 문서에서는 OMS 보안 및 감사 솔루션에서 데이터를 관리하고 보호하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="7b303-117">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="7b303-117">Data sources</span></span>
<span data-ttu-id="7b303-118">OMS 보안 및 감사 솔루션에서는 OMS 에이전트가 설치되어 있는 Virtual Machines 및 물리적 컴퓨터에서 데이터를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span></span> <span data-ttu-id="7b303-119">OMS 보안 및 감사 솔루션에서는 Windows 이벤트, 감사 로그, IIS 로그 및 syslog 메시지와 같은 보안 이벤트에 대한 구성 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="7b303-120">이러한 데이터의 예: 운영 체제 유형 및 버전, 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="7b303-121">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="7b303-121">Data protection</span></span>
<span data-ttu-id="7b303-122">**데이터 분리:**데이터는 서비스 전체에서 각 구성 요소에 논리적으로 별도로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span></span> <span data-ttu-id="7b303-123">모든 데이터에는 조직별로 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-123">All data is tagged per organization.</span></span> <span data-ttu-id="7b303-124">이 태그는 데이터 수명 주기 동안 유지되며 서비스의 각 계층에서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span></span> 

<span data-ttu-id="7b303-125">**데이터 액세스**: Microsoft 직원은 보안 권장 사항을 제공하고 잠재적 보안 위협을 조사하기 위해 서비스에서 수집되고 분석된 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="7b303-126">[Microsoft Online Services 약관](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) 및 [개인 정보 취급 방침](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)을 준수합니다. 즉, Microsoft는 고객 데이터를 사용하거나 광고 또는 유사한 상업적 목적에서 정보를 파생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="7b303-127">Microsoft 직원은 보안 권장 사항을 제공하고 잠재적 보안 위협을 조사하기 위해 서비스에서 수집되고 분석된 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="7b303-128">필요에 따라 고객 데이터를 사용하여 해당 서비스를 제공하도록 호환할 수 있는 목적으로 Azure 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="7b303-129">고객은 고유한 데이터에 대한 모든 권한을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-129">You retain all rights to your own data.</span></span>

<span data-ttu-id="7b303-130">**데이터 사용**: Microsoft는 여러 테넌트에 발생하는 패턴 및 위협 인텔리전스를 사용하여 방지 및 검색 기능을 향상시킵니다. [개인 정보 취급 방침](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)에 설명된 개인 정보 취급 방침 약정에 따라 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7b303-131">데이터 위치는 초기 OMS 보안 및 감사 구성 프로세스의 일부인 작업 영역 만들기 중에 OMS 작업 영역 수준에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="7b303-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7b303-132">See also</span></span>
<span data-ttu-id="7b303-133">이 문서에서는 OMS에서 데이터를 관리하고 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b303-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="7b303-134">OMS 보안 및 감사 솔루션에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b303-134">To learn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="7b303-135">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="7b303-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="7b303-136">Operations Management Suite 보안 및 감사 솔루션의 보안 경고 모니터링 및 응답</span><span class="sxs-lookup"><span data-stu-id="7b303-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="7b303-137">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="7b303-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

