---
title: "Azure Security Center 소개 | Microsoft Docs"
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
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="f0d3f-103">Azure 보안 센터 소개</span><span class="sxs-lookup"><span data-stu-id="f0d3f-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="f0d3f-104">Azure 보안 센터, 주요 기능 및 작동 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d3f-105">2017년 6월 초를 시작으로 Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집 및 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="f0d3f-106">자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="f0d3f-107">이 문서의 정보는 Microsoft Monitoring Agent로 전환된 후의 Security Center 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="f0d3f-108">Azure 보안 센터란?</span><span class="sxs-lookup"><span data-stu-id="f0d3f-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="f0d3f-109">보안 센터는 Azure 리소스의 보안에 대한 향상된 가시성과 제어권을 통해 위협을 예방하고 감지하며 위협에 대응하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-109">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="f0d3f-110">이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="f0d3f-111">주요 기능</span><span class="sxs-lookup"><span data-stu-id="f0d3f-111">Key capabilities</span></span>
 <span data-ttu-id="f0d3f-112">보안 센터는 Azure에 기본 제공되는 사용하기 쉽고 효과적인 위협 예방, 감지 및 대응 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="f0d3f-113">주요 기능:</span><span class="sxs-lookup"><span data-stu-id="f0d3f-113">Key capabilities are:</span></span>

| <span data-ttu-id="f0d3f-114">단계</span><span class="sxs-lookup"><span data-stu-id="f0d3f-114">Stage</span></span> | <span data-ttu-id="f0d3f-115">기능</span><span class="sxs-lookup"><span data-stu-id="f0d3f-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="f0d3f-116">예방</span><span class="sxs-lookup"><span data-stu-id="f0d3f-116">Prevent</span></span> |<span data-ttu-id="f0d3f-117">Azure 리소스의 보안 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="f0d3f-117">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="f0d3f-118">예방</span><span class="sxs-lookup"><span data-stu-id="f0d3f-118">Prevent</span></span> | <span data-ttu-id="f0d3f-119">회사의 보안 요구 사항, 사용할 응용 프로그램 형식 및 데이터의 민감도에 따라 Azure 구독에 대한 정책 정의</span><span class="sxs-lookup"><span data-stu-id="f0d3f-119">Defines policies for your Azure subscriptions based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="f0d3f-120">예방</span><span class="sxs-lookup"><span data-stu-id="f0d3f-120">Prevent</span></span> | <span data-ttu-id="f0d3f-121">정책 기반 보안 권장 사항을 사용하여 서비스 소유자에게 필요한 제어를 구현하는 과정 안내</span><span class="sxs-lookup"><span data-stu-id="f0d3f-121">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="f0d3f-122">예방</span><span class="sxs-lookup"><span data-stu-id="f0d3f-122">Prevent</span></span> | <span data-ttu-id="f0d3f-123">Microsoft 및 파트너의 보안 서비스 및 어플라이언스를 빠르게 배포</span><span class="sxs-lookup"><span data-stu-id="f0d3f-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="f0d3f-124">감지</span><span class="sxs-lookup"><span data-stu-id="f0d3f-124">Detect</span></span> |<span data-ttu-id="f0d3f-125">Azure 리소스, 네트워크 및 맬웨어 방지 프로그램과 방화벽 같은 파트너 솔루션에서 자동으로 보안 데이터 수집 및 분석</span><span class="sxs-lookup"><span data-stu-id="f0d3f-125">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="f0d3f-126">감지</span><span class="sxs-lookup"><span data-stu-id="f0d3f-126">Detect</span></span> | <span data-ttu-id="f0d3f-127">Microsoft 제품과 서비스, Microsoft DCU(Digital Crimes Unit), MSRC(Microsoft 보안 대응 센터) 및 외부 피드에서 글로벌 위협 인텔리전스 사용</span><span class="sxs-lookup"><span data-stu-id="f0d3f-127">Uses global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="f0d3f-128">감지</span><span class="sxs-lookup"><span data-stu-id="f0d3f-128">Detect</span></span> | <span data-ttu-id="f0d3f-129">기계 학습 및 행동 분석을 비롯한 고급 분석 적용</span><span class="sxs-lookup"><span data-stu-id="f0d3f-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="f0d3f-130">대응</span><span class="sxs-lookup"><span data-stu-id="f0d3f-130">Respond</span></span> |<span data-ttu-id="f0d3f-131">우선 순위가 지정된 보안 문제/경고 제공</span><span class="sxs-lookup"><span data-stu-id="f0d3f-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="f0d3f-132">대응</span><span class="sxs-lookup"><span data-stu-id="f0d3f-132">Respond</span></span> | <span data-ttu-id="f0d3f-133">공격 출처 및 영향을 받는 리소스에 대한 정보 제공</span><span class="sxs-lookup"><span data-stu-id="f0d3f-133">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="f0d3f-134">대응</span><span class="sxs-lookup"><span data-stu-id="f0d3f-134">Respond</span></span> | <span data-ttu-id="f0d3f-135">현재 공격을 중지하고 미래 공격을 예방하는 데 도움이 되는 방법 제안</span><span class="sxs-lookup"><span data-stu-id="f0d3f-135">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="f0d3f-136">기능 소개 연습</span><span class="sxs-lookup"><span data-stu-id="f0d3f-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="f0d3f-137">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-137">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="f0d3f-138">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="f0d3f-139">[Azure 포털](https://azure.microsoft.com/features/azure-portal/)에서 보안 센터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-139">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="f0d3f-140">[포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-140">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="f0d3f-141">주 포털 메뉴에서 **Security Center** 옵션으로 스크롤하거나 이전에 포털 대시보드에 고정한 **Security Center** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-141">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Azure 포털의 보안 타일][1]

<span data-ttu-id="f0d3f-143">보안 센터에서 보안 정책을 설정하고 보안 구성을 모니터링하며 보안 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="f0d3f-144">보안 정책</span><span class="sxs-lookup"><span data-stu-id="f0d3f-144">Security policies</span></span>
<span data-ttu-id="f0d3f-145">회사의 보안 요구 사항에 따라 Azure 구독에 대한 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-145">You can define policies for your Azure subscriptions according to your company's security requirements.</span></span> <span data-ttu-id="f0d3f-146">또한 사용하는 응용 프로그램의 형식 또는 각 구독에서 데이터의 민감도에 대해 정책을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-146">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="f0d3f-147">예를 들어 개발 또는 테스트에 사용되는 리소스의 요구사항은 프로덕션 응용 프로그램에 사용되는 보안 요구 사항과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="f0d3f-148">마찬가지로 PII 같은 규제된 데이터를 가진 응용 프로그램에 대해서는 더 높은 수준의 보안이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d3f-149">보안 정책을 수정하려면 보안 관리자이거나 구독의 소유자 또는 참가자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-149">To modify a security policy, you must be a Security Administrator or the subscription's Owner or Contributor.</span></span> <span data-ttu-id="f0d3f-150">Security Center의 역할 및 허용된 작업에 대해 알아보려면 [Azure Security Center의 권한](security-center-permissions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-150">To learn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="f0d3f-151">**Security Center** 블레이드에서 구독 및 리소스 그룹 목록에 대한 **정책** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-151">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![보안 센터 블레이드][2]

<span data-ttu-id="f0d3f-153">**보안 정책** 블레이드에서 정책 세부 정보를 볼 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-153">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

<span data-ttu-id="f0d3f-154">**데이터 수집**은 보안 정책에 대한 데이터 수집을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="f0d3f-155">사용하도록 설정하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-155">Enabling provides:</span></span>

* <span data-ttu-id="f0d3f-156">보안 모니터링 및 권장 사항을 위해 지원되는 가상 컴퓨터(VM)를 매일 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="f0d3f-157">분석 및 위협 감지를 위해 보안 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d3f-158">데이터 수집은 구독 수준에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-158">Data collection is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="f0d3f-159">**방지 정책**을 선택하여 **방지 정책** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-159">Select **Prevention policy** to open the **Prevention policy** blade.</span></span> <span data-ttu-id="f0d3f-160">**권장 사항 표시**를 사용하면 구독 내에서 리소스의 보안 요구를 기반으로 모니터링하려는 보안 컨트롤과 보려는 권장 지침을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-160">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="f0d3f-161">보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="f0d3f-161">Security recommendations</span></span>
 <span data-ttu-id="f0d3f-162">보안 센터는 Azure 리소스의 보안 상태를 분석하여 잠재적인 보안 취약성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-162">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="f0d3f-163">권장 사항 목록은 필요한 컨트롤 구성 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-163">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="f0d3f-164">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-164">Examples include:</span></span>

* <span data-ttu-id="f0d3f-165">맬웨어 방지 프로그램을 프로비전하여 악성 소프트웨어 식별 및 제거 지원</span><span class="sxs-lookup"><span data-stu-id="f0d3f-165">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="f0d3f-166">네트워크 보안 그룹 및 VM에 대한 트래픽 제어 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="f0d3f-166">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="f0d3f-167">웹 응용 프로그램 방화벽을 프로비전하여 웹 응용 프로그램의 대상이 되는 공격에 대한 방어 지원</span><span class="sxs-lookup"><span data-stu-id="f0d3f-167">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="f0d3f-168">누락된 시스템 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="f0d3f-168">Deploying missing system updates</span></span>
* <span data-ttu-id="f0d3f-169">권장 기준과 일치하지 않는 OS 구성 해결</span><span class="sxs-lookup"><span data-stu-id="f0d3f-169">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="f0d3f-170">권장 사항 목록에 대한 **권장 사항** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-170">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="f0d3f-171">각 권장 사항을 클릭하여 추가 정보를 보거나 문제를 해결하기 위한 조치를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-171">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Azure 보안 센터의 보안 권장 사항][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="f0d3f-173">Azure 리소스의 보안 상태</span><span class="sxs-lookup"><span data-stu-id="f0d3f-173">Security state of Azure resources</span></span>
<span data-ttu-id="f0d3f-174">대시보드의 **방지**섹션은 환경의 전체 보안 상태를 VM, 웹 응용 프로그램 및 다른 리소스를 비롯한 리소스 형식별로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-174">The **Prevention** section of the dashboard shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="f0d3f-175">**방지**에서 리소스 형식을 선택하여 식별된 잠재적 보안 취약성 목록을 비롯한 자세한 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-175">Select a resource type under **Prevention** to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="f0d3f-176">(아래 예제에서**계산**을 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="f0d3f-176">(**Compute** is selected in the example below.)</span></span>

![리소스 상태 타일][6]

### <a name="security-alerts"></a><span data-ttu-id="f0d3f-178">보안 경고</span><span class="sxs-lookup"><span data-stu-id="f0d3f-178">Security alerts</span></span>
 <span data-ttu-id="f0d3f-179">보안 센터는 Azure 리소스, 네트워크 및 맬웨어 방지 프로그램과 방화벽 같은 파트너 솔루션에서 자동으로 로그 데이터를 수집, 분석 및 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="f0d3f-180">위협이 감지되었을 때 보안 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="f0d3f-181">감지되는 사항의 예:</span><span class="sxs-lookup"><span data-stu-id="f0d3f-181">Examples include detection of:</span></span>

* <span data-ttu-id="f0d3f-182">알려진 악성 IP 주소와 통신하는 손상된 VM</span><span class="sxs-lookup"><span data-stu-id="f0d3f-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="f0d3f-183">Windows 오류 보고를 사용하여 감지된 고급 맬웨어 프로그램</span><span class="sxs-lookup"><span data-stu-id="f0d3f-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="f0d3f-184">VM에 대한 무작위 공격</span><span class="sxs-lookup"><span data-stu-id="f0d3f-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="f0d3f-185">통합 맬웨어 방지 프로그램 및 방화벽에서의 보안 경고</span><span class="sxs-lookup"><span data-stu-id="f0d3f-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="f0d3f-186">**보안 경고** 타일을 클릭하면 우선 순위가 지정된 경고의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-186">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![보안 경고][7]

<span data-ttu-id="f0d3f-188">경고를 선택하면 공격 및 공격을 해결하는 방법 제안에 대한 더 자세한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-188">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![보안 경고 세부 정보][8]

### <a name="partner-solutions"></a><span data-ttu-id="f0d3f-190">파트너 솔루션</span><span class="sxs-lookup"><span data-stu-id="f0d3f-190">Partner solutions</span></span>
<span data-ttu-id="f0d3f-191">**파트너 솔루션** 타일을 통해 Azure 구독과 통합된 파트너 솔루션의 보안 상태를 한 눈에 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-191">The **Partner solutions** tile lets you monitor at a glance the security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="f0d3f-192">보안 센터에는 솔루션에서 가져온 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-192">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="f0d3f-193">**파트너 솔루션** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-193">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="f0d3f-194">블레이드가 열리고 연결된 모든 파트너 솔루션의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![파트너 솔루션][9]

## <a name="get-started"></a><span data-ttu-id="f0d3f-196">시작</span><span class="sxs-lookup"><span data-stu-id="f0d3f-196">Get started</span></span>
<span data-ttu-id="f0d3f-197">보안 센터를 시작하려면 Microsoft Azure에 대한 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-197">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="f0d3f-198">보안 센터는 Azure 구독을 사용하여 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="f0d3f-199">구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="f0d3f-200">[Azure 포털](https://azure.microsoft.com/features/azure-portal/)에서 보안 센터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-200">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="f0d3f-201">자세한 내용은 [포털 설명서](https://azure.microsoft.com/documentation/services/azure-portal/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-201">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="f0d3f-202">[Azure 보안 센터 시작](security-center-get-started.md)은 보안 센터의 보안 모니터링 및 정책 관리 구성 요소를 빠르게 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0d3f-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0d3f-203">Next steps</span></span>
<span data-ttu-id="f0d3f-204">이 문서에서는 보안 센터, 주요 기능 및 시작하는 방법을 소개하였습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-204">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="f0d3f-205">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-205">To learn more, see the following resources:</span></span>

* <span data-ttu-id="f0d3f-206">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f0d3f-207">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f0d3f-208">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="f0d3f-209">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-209">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f0d3f-210">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) — 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="f0d3f-211">[Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="f0d3f-212">[Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f0d3f-213">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0d3f-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

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
