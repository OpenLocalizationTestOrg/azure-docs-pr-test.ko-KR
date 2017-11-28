---
title: "aaaIntroduction tooAzure 보안 센터 | Microsoft Docs"
description: "Azure 보안 센터, 주요 기능 및 작동 방법에 대해 알아봅니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a><span data-ttu-id="cfcc7-103">소개 tooAzure 보안 센터</span><span class="sxs-lookup"><span data-stu-id="cfcc7-103">Introduction tooAzure Security Center</span></span>
<span data-ttu-id="cfcc7-104">Azure 보안 센터, 주요 기능 및 작동 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="cfcc7-105">보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-105">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="cfcc7-106">참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) toolearn more.</span></span> <span data-ttu-id="cfcc7-107">이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-107">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="cfcc7-108">Azure 보안 센터란?</span><span class="sxs-lookup"><span data-stu-id="cfcc7-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="cfcc7-109">보안 센터를 사용 하면 방지 하 고 검색에 대 한 향상 된 가시성 및 Azure 리소스의 보안을 hello에 대 한 제어를 사용 하 여 toothreats 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-109">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="cfcc7-110">이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="cfcc7-111">주요 기능</span><span class="sxs-lookup"><span data-stu-id="cfcc7-111">Key capabilities</span></span>
 <span data-ttu-id="cfcc7-112">보안 센터 사용 하기 쉬운이 고 효과적인 위협 tooAzure 제공 된 예방, 감지, 및 대처 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in tooAzure.</span></span> <span data-ttu-id="cfcc7-113">주요 기능:</span><span class="sxs-lookup"><span data-stu-id="cfcc7-113">Key capabilities are:</span></span>

| <span data-ttu-id="cfcc7-114">단계</span><span class="sxs-lookup"><span data-stu-id="cfcc7-114">Stage</span></span> | <span data-ttu-id="cfcc7-115">기능</span><span class="sxs-lookup"><span data-stu-id="cfcc7-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="cfcc7-116">예방</span><span class="sxs-lookup"><span data-stu-id="cfcc7-116">Prevent</span></span> |<span data-ttu-id="cfcc7-117">모니터 hello Azure 리소스의 보안 상태</span><span class="sxs-lookup"><span data-stu-id="cfcc7-117">Monitors hello security state of your Azure resources</span></span> |
| <span data-ttu-id="cfcc7-118">예방</span><span class="sxs-lookup"><span data-stu-id="cfcc7-118">Prevent</span></span> | <span data-ttu-id="cfcc7-119">Hello 유형의 응용 프로그램을 사용 하 고 데이터의 민감도 hello 회사의 보안 요구 사항에 기반 하 여 Azure 구독에 대 한 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-119">Defines policies for your Azure subscriptions based on your company’s security requirements, hello types of applications that you use, and hello sensitivity of your data</span></span> |
| <span data-ttu-id="cfcc7-120">예방</span><span class="sxs-lookup"><span data-stu-id="cfcc7-120">Prevent</span></span> | <span data-ttu-id="cfcc7-121">사용 하 여 정책 기반 보안 권장 사항 tooguide 서비스 소유자 구현의 hello 프로세스를 통해 필요한 컨트롤</span><span class="sxs-lookup"><span data-stu-id="cfcc7-121">Uses policy-driven security recommendations tooguide service owners through hello process of implementing needed controls</span></span> |
| <span data-ttu-id="cfcc7-122">예방</span><span class="sxs-lookup"><span data-stu-id="cfcc7-122">Prevent</span></span> | <span data-ttu-id="cfcc7-123">Microsoft 및 파트너의 보안 서비스 및 어플라이언스를 빠르게 배포</span><span class="sxs-lookup"><span data-stu-id="cfcc7-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="cfcc7-124">감지</span><span class="sxs-lookup"><span data-stu-id="cfcc7-124">Detect</span></span> |<span data-ttu-id="cfcc7-125">자동으로 수집 하 여 Azure 리소스, hello 네트워크 및 맬웨어 방지 프로그램 및 방화벽와 같은 파트너 솔루션에서 보안 데이터를 분석 하 고</span><span class="sxs-lookup"><span data-stu-id="cfcc7-125">Automatically collects and analyzes security data from your Azure resources, hello network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="cfcc7-126">감지</span><span class="sxs-lookup"><span data-stu-id="cfcc7-126">Detect</span></span> | <span data-ttu-id="cfcc7-127">전역 사용 하 여 위협 인텔리전스에서 Microsoft 제품 및 서비스를 Microsoft Digital Crimes 단위 (DCU), hello hello Microsoft 보안 대응 센터 (MSRC), 및 외부 피드</span><span class="sxs-lookup"><span data-stu-id="cfcc7-127">Uses global threat intelligence from Microsoft products and services, hello Microsoft Digital Crimes Unit (DCU), hello Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="cfcc7-128">감지</span><span class="sxs-lookup"><span data-stu-id="cfcc7-128">Detect</span></span> | <span data-ttu-id="cfcc7-129">기계 학습 및 행동 분석을 비롯한 고급 분석 적용</span><span class="sxs-lookup"><span data-stu-id="cfcc7-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="cfcc7-130">대응</span><span class="sxs-lookup"><span data-stu-id="cfcc7-130">Respond</span></span> |<span data-ttu-id="cfcc7-131">우선 순위가 지정된 보안 문제/경고 제공</span><span class="sxs-lookup"><span data-stu-id="cfcc7-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="cfcc7-132">대응</span><span class="sxs-lookup"><span data-stu-id="cfcc7-132">Respond</span></span> | <span data-ttu-id="cfcc7-133">Hello 소스 hello 공격 및 영향을 받는 리소스에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-133">Offers insights into hello source of hello attack and impacted resources</span></span> |
| <span data-ttu-id="cfcc7-134">대응</span><span class="sxs-lookup"><span data-stu-id="cfcc7-134">Respond</span></span> | <span data-ttu-id="cfcc7-135">Toostop 현재 공격 hello 및 향후 공격을 방지 하는 방법을 제안합니다</span><span class="sxs-lookup"><span data-stu-id="cfcc7-135">Suggests ways toostop hello current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="cfcc7-136">기능 소개 연습</span><span class="sxs-lookup"><span data-stu-id="cfcc7-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="cfcc7-137">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-137">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="cfcc7-138">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="cfcc7-139">보안 센터 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-139">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="cfcc7-140">[Toohello 포털에 로그인](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-140">[Sign in toohello portal](https://portal.azure.com).</span></span> <span data-ttu-id="cfcc7-141">Hello 주 포털 메뉴에서 toohello 스크롤합니다 **보안 센터** 옵션 또는 선택 hello **보안 센터** toohello 포털 대시보드에서 고정 했던 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-141">Under hello main portal menu, scroll toohello **Security Center** option or select hello **Security Center** tile that you previously pinned toohello portal dashboard.</span></span>

![Azure 포털의 보안 타일][1]

<span data-ttu-id="cfcc7-143">보안 센터에서 보안 정책을 설정하고 보안 구성을 모니터링하며 보안 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="cfcc7-144">보안 정책</span><span class="sxs-lookup"><span data-stu-id="cfcc7-144">Security policies</span></span>
<span data-ttu-id="cfcc7-145">Tooyour 회사의 보안 요구 사항에 따라 Azure 구독에 대 한 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-145">You can define policies for your Azure subscriptions according tooyour company's security requirements.</span></span> <span data-ttu-id="cfcc7-146">조정할 수 있습니다 이러한 toohello 유형의 사용 하는 응용 프로그램 또는 toohello 민감도 hello 데이터의 각 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-146">You can also tailor them toohello types of applications you're using or toohello sensitivity of hello data in each subscription.</span></span> <span data-ttu-id="cfcc7-147">예를 들어 개발 또는 테스트에 사용되는 리소스의 요구사항은 프로덕션 응용 프로그램에 사용되는 보안 요구 사항과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="cfcc7-148">마찬가지로 PII 같은 규제된 데이터를 가진 응용 프로그램에 대해서는 더 높은 수준의 보안이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="cfcc7-149">보안 정책 toomodify hello 또는 보안 관리자가 구독 소유자 또는 참가자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-149">toomodify a security policy, you must be a Security Administrator or hello subscription's Owner or Contributor.</span></span> <span data-ttu-id="cfcc7-150">역할 및 보안 센터에서 허용 되는 작업에 대해 자세히 toolearn 참조 [Azure 보안 센터에서 사용 권한을](security-center-permissions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-150">toolearn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="cfcc7-151">Hello에 **보안 센터** 블레이드, 선택 hello **정책** 구독 / 리소스 그룹의 목록에 대 한 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-151">On hello **Security Center** blade, select hello **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![보안 센터 블레이드][2]

<span data-ttu-id="cfcc7-153">Hello에 **보안 정책** 블레이드에서 구독 tooview hello 정책 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-153">On hello **Security policy** blade, select a subscription tooview hello policy details.</span></span>

<span data-ttu-id="cfcc7-154">**데이터 수집**은 보안 정책에 대한 데이터 수집을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="cfcc7-155">사용하도록 설정하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-155">Enabling provides:</span></span>

* <span data-ttu-id="cfcc7-156">보안 모니터링 및 권장 사항을 위해 지원되는 가상 컴퓨터(VM)를 매일 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="cfcc7-157">분석 및 위협 감지를 위해 보안 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="cfcc7-158">데이터 수집 hello 구독 수준에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-158">Data collection is configured at hello subscription level.</span></span>
>
>

<span data-ttu-id="cfcc7-159">선택 **방지 정책** tooopen hello **방지 정책** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-159">Select **Prevention policy** tooopen hello **Prevention policy** blade.</span></span> <span data-ttu-id="cfcc7-160">**에 대 한 권장 사항 표시** toosee hello 구독 내 hello 리소스의 hello 보안 요구 사항에 따라 원하는 toomonitor 및 hello 권장 사항을 원하는 hello 보안 컨트롤을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-160">**Show recommendations for** lets you choose hello security controls that you want toomonitor and hello recommendations that you want toosee based on hello security needs of hello resources within hello subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="cfcc7-161">보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="cfcc7-161">Security recommendations</span></span>
 <span data-ttu-id="cfcc7-162">보안 센터에 Azure 리소스 tooidentify 잠재적인 보안 취약점의 hello 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-162">Security Center analyzes hello security state of your Azure resources tooidentify potential security vulnerabilities.</span></span> <span data-ttu-id="cfcc7-163">권장 사항 목록 hello 필요한 컨트롤을 구성 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-163">A list of recommendations guides you through hello process of configuring needed controls.</span></span> <span data-ttu-id="cfcc7-164">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-164">Examples include:</span></span>

* <span data-ttu-id="cfcc7-165">맬웨어 방지 프로 비전 toohelp 식별 하 고 악성 소프트웨어를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-165">Provisioning antimalware toohelp identify and remove malicious software</span></span>
* <span data-ttu-id="cfcc7-166">네트워크 보안 그룹 및 규칙 toocontrol 트래픽 tooVMs 구성</span><span class="sxs-lookup"><span data-stu-id="cfcc7-166">Configuring network security groups and rules toocontrol traffic tooVMs</span></span>
* <span data-ttu-id="cfcc7-167">웹 응용 프로그램 방화벽 toohelp 웹 응용 프로그램을 대상으로 하는 공격을 방어할의 프로 비전</span><span class="sxs-lookup"><span data-stu-id="cfcc7-167">Provisioning of web application firewalls toohelp defend against attacks that target your web applications</span></span>
* <span data-ttu-id="cfcc7-168">누락된 시스템 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="cfcc7-168">Deploying missing system updates</span></span>
* <span data-ttu-id="cfcc7-169">초기 권장 hello와 일치 하지 않는 운영 체제 구성을 주소 지정</span><span class="sxs-lookup"><span data-stu-id="cfcc7-169">Addressing OS configurations that do not match hello recommended baselines</span></span>

<span data-ttu-id="cfcc7-170">Hello 클릭 **권장 사항을** 권장 사항 목록에 대 한 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-170">Click hello **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="cfcc7-171">각 권장 사항 tooview 추가 정보 또는 tootake 작업 tooresolve hello 문제를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-171">Click each recommendation tooview additional information or tootake action tooresolve hello issue.</span></span>

![Azure 보안 센터의 보안 권장 사항][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="cfcc7-173">Azure 리소스의 보안 상태</span><span class="sxs-lookup"><span data-stu-id="cfcc7-173">Security state of Azure resources</span></span>
<span data-ttu-id="cfcc7-174">hello **방지** hello 대시보드의 리소스 종류, Vm, 웹 응용 프로그램 및 기타 리소스를 포함 하 여 hello 환경의 전반적인 보안 상태를 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-174">hello **Prevention** section of hello dashboard shows hello overall security posture of hello environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="cfcc7-175">리소스 종류 선택 **방지** tooview 목록이 표시 되는 모든 잠재적인 보안 취약점을 비롯 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-175">Select a resource type under **Prevention** tooview more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="cfcc7-176">(**계산** hello 예제 아래에서 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="cfcc7-176">(**Compute** is selected in hello example below.)</span></span>

![리소스 상태 타일][6]

### <a name="security-alerts"></a><span data-ttu-id="cfcc7-178">보안 경고</span><span class="sxs-lookup"><span data-stu-id="cfcc7-178">Security alerts</span></span>
 <span data-ttu-id="cfcc7-179">보안 센터 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 맬웨어 방지 프로그램 및 방화벽와 같은 파트너 솔루션에서 로그 데이터를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="cfcc7-180">위협이 감지되었을 때 보안 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="cfcc7-181">감지되는 사항의 예:</span><span class="sxs-lookup"><span data-stu-id="cfcc7-181">Examples include detection of:</span></span>

* <span data-ttu-id="cfcc7-182">알려진 악성 IP 주소와 통신하는 손상된 VM</span><span class="sxs-lookup"><span data-stu-id="cfcc7-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="cfcc7-183">Windows 오류 보고를 사용하여 감지된 고급 맬웨어 프로그램</span><span class="sxs-lookup"><span data-stu-id="cfcc7-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="cfcc7-184">VM에 대한 무작위 공격</span><span class="sxs-lookup"><span data-stu-id="cfcc7-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="cfcc7-185">통합 맬웨어 방지 프로그램 및 방화벽에서의 보안 경고</span><span class="sxs-lookup"><span data-stu-id="cfcc7-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="cfcc7-186">클릭 하 여 hello **보안 경고** 타일에는 우선 순위가 지정 된 경고 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-186">Clicking hello **Security alerts** tile displays a list of prioritized alerts.</span></span>

![보안 경고][7]

<span data-ttu-id="cfcc7-188">경고를 선택 하면 hello 공격 및 방법에 대 한 제안 사항에 대 한 자세한 정보 표시 tooremediate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-188">Selecting an alert shows more information about hello attack and suggestions for how tooremediate it.</span></span>

![보안 경고 세부 정보][8]

### <a name="partner-solutions"></a><span data-ttu-id="cfcc7-190">파트너 솔루션</span><span class="sxs-lookup"><span data-stu-id="cfcc7-190">Partner solutions</span></span>
<span data-ttu-id="cfcc7-191">hello **파트너 솔루션** 파트너 솔루션의 한 눈에 보기 hello 보안 상태에 모니터링 하는 타일 사용 하면 Azure 구독와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-191">hello **Partner solutions** tile lets you monitor at a glance hello security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="cfcc7-192">보안 센터 들어오는 hello 솔루션에서 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-192">Security Center displays alerts coming from hello solutions.</span></span>

<span data-ttu-id="cfcc7-193">선택 hello **파트너 솔루션** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-193">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="cfcc7-194">블레이드가 열리고 연결된 모든 파트너 솔루션의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![파트너 솔루션][9]

## <a name="get-started"></a><span data-ttu-id="cfcc7-196">시작</span><span class="sxs-lookup"><span data-stu-id="cfcc7-196">Get started</span></span>
<span data-ttu-id="cfcc7-197">보안 센터와 시작 tooget, 구독 tooMicrosoft Azure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-197">tooget started with Security Center, you need a subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="cfcc7-198">보안 센터는 Azure 구독을 사용하여 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="cfcc7-199">구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="cfcc7-200">보안 센터 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-200">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="cfcc7-201">Hello 참조 [포털 설명서](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-201">See hello [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn more.</span></span>

<span data-ttu-id="cfcc7-202">[Azure 보안 센터를 시작 하기](security-center-get-started.md) 보안 센터의 hello 보안 모니터링 및 정책 관리 구성 요소를 통해 신속 하 게 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through hello security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfcc7-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfcc7-203">Next steps</span></span>
<span data-ttu-id="cfcc7-204">이 문서에 도입 된 tooSecurity 센터의 주요 기능 및 tooget 시작 하는 방법이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-204">In this document, you were introduced tooSecurity Center, its key capabilities, and how tooget started.</span></span> <span data-ttu-id="cfcc7-205">toolearn hello 다음 리소스를 더, 참조:</span><span class="sxs-lookup"><span data-stu-id="cfcc7-205">toolearn more, see hello following resources:</span></span>

* <span data-ttu-id="cfcc7-206">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="cfcc7-207">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="cfcc7-208">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="cfcc7-209">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-209">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="cfcc7-210">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="cfcc7-211">[Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="cfcc7-212">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="cfcc7-213">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cfcc7-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
