---
title: "Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링 | Microsoft Docs"
description: "이 문서는 OMS 보안 및 감사 기능을 사용하여 리소스를 모니터링하고 보안 문제를 식별하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 2f73266b65a4eda6c8751a2d56bc3f11bf4e6a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="3cc45-103">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="3cc45-103">Monitoring resources in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="3cc45-104">이 문서는 OMS 보안 및 감사 기능을 사용하여 리소스를 모니터링하고 보안 문제를 식별하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-104">This document helps you use OMS Security and Audit capabilities to monitor your resources and identify security issues.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="3cc45-105">OMS란?</span><span class="sxs-lookup"><span data-stu-id="3cc45-105">What is OMS?</span></span>
<span data-ttu-id="3cc45-106">Microsoft Operations Management Suite(OMS)란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="3cc45-107">OMS에 대한 자세한 내용은 [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cc45-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="monitoring-resources"></a><span data-ttu-id="3cc45-108">리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="3cc45-108">Monitoring resources</span></span>
<span data-ttu-id="3cc45-109">보안 문제는 가능하면 처음부터 발생하지 않도록 예방해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-109">Whenever is possible, you will want to prevent security incidents from happening in the first place.</span></span> <span data-ttu-id="3cc45-110">하지만 모든 보안 문제를 방지하는 것은 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-110">However, it is impossible to prevent all security incidents.</span></span> <span data-ttu-id="3cc45-111">보안 문제가 발생하면 영향을 최소화하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-111">When a security incident does happen, you will need to ensure that its impact is minimized.</span></span>  <span data-ttu-id="3cc45-112">보안 문제의 수와 영향을 최소화하기 위해 세 가지 중요 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-112">There are three critical recommendations that can be used to minimize the number and the impact of security incidents:</span></span>

* <span data-ttu-id="3cc45-113">사용자 환경의 취약성을 정기적으로 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-113">Routinely assess vulnerabilities in your environment.</span></span>
* <span data-ttu-id="3cc45-114">모든 컴퓨터 시스템과 네트워크 장치를 정기적으로 검사하여 최신 패치가 모두 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-114">Routinely check all computer systems and network devices to ensure that they have all of the latest patches installed.</span></span>
* <span data-ttu-id="3cc45-115">운영 시스템 이벤트 로그, 응용 프로그램별 로그, 침입 검색 시스템 로그를 포함한 모든 로그와 로깅 메커니즘을 정기적으로 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-115">Routinely check all logs and logging mechanisms, including operating system event logs, application specific logs and intrusion detection system logs.</span></span>

<span data-ttu-id="3cc45-116">OMS 보안 및 감사 솔루션을 사용하면 IT가 모든 리소스를 능동적으로 모니터링하여 보안 문제의 영향을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-116">OMS Security and Audit solution enables IT to actively monitor all resources, which can help minimize the impact of security incidents.</span></span> <span data-ttu-id="3cc45-117">OMS 보안 및 감사에는 리소스 모니터링에 사용할 수 있는 보안 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-117">OMS Security and Audit has security domains that can be used for monitoring resources.</span></span> <span data-ttu-id="3cc45-118">보안 도메인을 통해 옵션에 빠르게 액세스할 수 있으며, 여기서는 보안 모니터링과 관려된 다음 도메인에 대해 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-118">The security domains provides quick access to a options, for security monitoring the following domains will be covered in more details:</span></span>

* <span data-ttu-id="3cc45-119">맬웨어 평가</span><span class="sxs-lookup"><span data-stu-id="3cc45-119">Malware assessment</span></span>
* <span data-ttu-id="3cc45-120">업데이트 평가</span><span class="sxs-lookup"><span data-stu-id="3cc45-120">Update assessment</span></span>
* <span data-ttu-id="3cc45-121">ID 및 액세스</span><span class="sxs-lookup"><span data-stu-id="3cc45-121">Identity and Access</span></span>

> [!NOTE]
> <span data-ttu-id="3cc45-122">모든 옵션에 대한 개요는 [Operations Management Suite 보안 및 감사 솔루션 시작](oms-security-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cc45-122">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="monitoring-system-protection"></a><span data-ttu-id="3cc45-123">시스템 보호 모니터링</span><span class="sxs-lookup"><span data-stu-id="3cc45-123">Monitoring system protection</span></span>
<span data-ttu-id="3cc45-124">심층 방어 수단에서는 자산의 전반적 보안 상태를 위해 모든 보호 계층이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-124">In a defense in depth approach, every layer of protection is important for the overall security state of your asset.</span></span> <span data-ttu-id="3cc45-125">위협이 검색된 컴퓨터와 적절히 보호되지 않은 컴퓨터는 보안 도메인의 맬웨어 평가 타일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-125">Computers with detected threats and computers with insufficient protection are shown in the Malware Assessment tile under Security Domains.</span></span> <span data-ttu-id="3cc45-126">맬웨어 평가의 정보를 사용하면 보호가 필요한 서버를 보호하는 계획을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-126">By using the information on the Malware Assessment, you can identify a plan to apply protection to the servers that need it.</span></span> <span data-ttu-id="3cc45-127">이 옵션에 액세스하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-127">To access this option follow the steps below:</span></span>

1. <span data-ttu-id="3cc45-128">**Microsoft Operations Management Suite** 기본 대시보드에서 **보안 및 감사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-128">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![보안 및 감사](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="3cc45-130">**보안 및 감사** 대시보드에서 **보안 도메인**의 **맬웨어 평가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-130">In the **Security and Audit** dashboard, click **Antimalware Assessment** under **Security Domains**.</span></span> <span data-ttu-id="3cc45-131">**맬웨어 평가** 대시보드가 아래와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-131">The **Antimalware Assessment** dashboard appears as shown below:</span></span>

![맬웨어 평가](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

<span data-ttu-id="3cc45-133">**맬웨어 평가** 대시보드를 사용하여 다음과 같은 보안 문제를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-133">You can use the **Malware Assessment** dashboard to identify the following security issues:</span></span>

* <span data-ttu-id="3cc45-134">**미해결 위협**: 손상된 상태이며 시스템에 미해결 위협이 있는 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3cc45-134">**Active threats**: computers that were compromised and have active threats in the system.</span></span>
* <span data-ttu-id="3cc45-135">**해결된 위협**: 손상되었지만 위협이 해결된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3cc45-135">**Remediated threats**: computers that were compromised but the threats were remediated.</span></span>
* <span data-ttu-id="3cc45-136">**서명 만료**: 맬웨어 보호를 사용하지만 서명이 만료된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3cc45-136">**Signature out of date**: computers that have malware protection enabled but the signature is out of date.</span></span>
* <span data-ttu-id="3cc45-137">**실시간 보호하지 않음**: 맬웨어 방지 프로그램이 설치되지 않은 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3cc45-137">**No real time protection**: computers that don’t have antimalware installed.</span></span>

### <a name="monitoring-updates"></a><span data-ttu-id="3cc45-138">업데이트 모니터링</span><span class="sxs-lookup"><span data-stu-id="3cc45-138">Monitoring updates</span></span>
<span data-ttu-id="3cc45-139">최신 보안 업데이트를 적용하는 것이 보안 모범 사례이며 업데이트 관리 전략에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-139">Applying the most recent security updates is a security best practice and it should be incorporated in your update management strategy.</span></span> <span data-ttu-id="3cc45-140">Microsoft Monitoring Agent 서비스(HealthService.exe)는 모니터링되는 컴퓨터에서 업데이트 정보를 읽은 다음 업데이트된 이 정보를 클라우드의 OMS 서비스로 전송하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-140">Microsoft Monitoring Agent service (HealthService.exe) reads update information from monitored computers and then sends this updated information to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="3cc45-141">Microsoft Monitoring Agent 서비스는 자동 서비스로 구성되며 대상 컴퓨터에 항상 실행되고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-141">The Microsoft Monitoring Agent service is configured as an automatic service and it should be always running in the target computer.</span></span>

![업데이트 모니터링](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

<span data-ttu-id="3cc45-143">논리는 업데이트 데이터에 적용되며 클라우드 서비스는 데이터를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-143">Logic is applied to the update data and the cloud service records the data.</span></span> <span data-ttu-id="3cc45-144">누락된 업데이트가 발견되면 **업데이트** 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-144">If missing updates are found, they are shown on the **Updates** dashboard.</span></span> <span data-ttu-id="3cc45-145">**업데이트** 대시보드를 사용하여 누락된 업데이트를 작업하고 필요로 하는 서버에 적용하도록 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-145">You can use the **Updates** dashboard to work with missing updates and develop a plan to apply them to the servers that need them.</span></span> <span data-ttu-id="3cc45-146">아래 단계를 따라 **업데이트** 대시보드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-146">Follow the steps below to access the **Updates** dashboard:</span></span>

1. <span data-ttu-id="3cc45-147">**Microsoft Operations Management Suite** 기본 대시보드에서 **보안 및 감사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-147">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="3cc45-148">**보안 및 감사** 대시보드에서 **보안 도메인**의 **업데이트 평가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-148">In the **Security and Audit** dashboard, click **Update Assessment** under **Security Domains**.</span></span> <span data-ttu-id="3cc45-149">업데이트 대시보드가 아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-149">The Update dashboard appears as shown below:</span></span>

![업데이트 평가](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

<span data-ttu-id="3cc45-151">이 대시보드에서 업데이트 평가를 수행하여 컴퓨터의 현재 상태를 확인하고 가장 위험한 위협을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-151">In this dashboard you can perform an update assessment to understand the current state of your computers and address the most critical threats.</span></span> <span data-ttu-id="3cc45-152">IT 관리자는 **위험 또는 중요 업데이트** 타일을 사용하여 다음과 같이 누락된 업데이트에 대한 상세 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-152">By using the **Critical or Security Updates** tile, IT administrators will be able to access detailed information about the updates that are missing as shown below:</span></span>

![검색 결과](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

<span data-ttu-id="3cc45-154">이 보고서에는 이 시스템이 취약한 위협의 유형을 식별하는 데 사용할 수 있는 중요 정보가 포함됩니다. 예를 들면 보안 업데이트와 관련된 Microsoft KB 문서, 취약성에 대한 상세 정보가 포함된 MS 게시판이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-154">This report include critical information that can be used to identify the type of threat this system is vulnerable to, which includes the Microsoft KB articles associated with the security update and the MS Bulletin that has more details about the vulnerability.</span></span>

### <a name="monitoring-identity-and-access"></a><span data-ttu-id="3cc45-155">ID 및 액세스 모니터링</span><span class="sxs-lookup"><span data-stu-id="3cc45-155">Monitoring identity and access</span></span>
<span data-ttu-id="3cc45-156">사용자들이 어디에서나 다양한 장치를 사용하여 많은 클라우드 및 온-프레미스 앱에 액세스함에 따라 자격 증명을 보호하는 것이 매우 중요해졌습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-156">With users working from anywhere, using different devices and accessing a vast amount of cloud and on-premises apps, it is imperative that their credentials are protected.</span></span> <span data-ttu-id="3cc45-157">자격 증명 도난 공격은 공격자가 처음에 일반 사용자의 자격 증명에 대한 액세스 권한을 얻은 다음 네트워크 내 시스템에 액세스하는 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-157">Credential theft attacks are those in which an attacker initially gains access to a regular user’s credentials to access a system within the network.</span></span> <span data-ttu-id="3cc45-158">대부분의 경우 이러한 최초 공격은 네트워크에 대한 액세스 권한을 얻기 위한 한 가지 방법에 불과하며 궁극적 목적은 권한이 있는 계정을 발견하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-158">Many times, this initial attack is only a way to get access to the network, the ultimate goal is to discover privilege accounts.</span></span> 

<span data-ttu-id="3cc45-159">공격자는 네트워크 안에 남아 도구를 자유롭게 사용하면서 로그온된 다른 계정의 세션에서 자격 증명을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-159">Attackers will stay in the network, using freely available tooling to extract credentials from the sessions of other logged-on accounts.</span></span> <span data-ttu-id="3cc45-160">시스템 구성에 따라 이러한 자격 증명은 해시, 티켓으로 추출하거나 심지어 일반 텍스트 비밀번호의 형태로도 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-160">Depending on the system configuration, these credentials can be extracted in the form of hashes, tickets, or even plaintext passwords.</span></span>  

> [!NOTE]
> <span data-ttu-id="3cc45-161">인터넷에 직접 노출된 컴퓨터에서는 모든 종류의 잘 알려진 사용자 이름(예: Administrator)을 사용하여 로그인하려는 시도가 여러 번 실패하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-161">machines that are directly exposed to the Internet will see many failed attempts that try to login using all kind of well-known usernames (e.g. Administrator).</span></span> <span data-ttu-id="3cc45-162">대부분의 경우 잘 알려진 사용자 이름을 사용하지 않고 강력한 비밀번호를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-162">In most cases it is OK if the well-known usernames are not used and if the password is strong enough.</span></span>
> 
> 

<span data-ttu-id="3cc45-163">침입자가 권한이 있는 계정을 손상하기 전에 그러한 침입자를 식별하는 것이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-163">It is possible to identify these intruders before they compromise a privilege account.</span></span> <span data-ttu-id="3cc45-164">**OMS 보안 및 감사 솔루션** 을 사용하여 ID 및 액세스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-164">You can leverage **OMS Security and Audit Solution** to monitor identity and access.</span></span> <span data-ttu-id="3cc45-165">아래 단계를 따라 **ID 및 액세스** 대시보드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-165">Follow the steps below to access the **Identity and Access** dashboard:</span></span>

1. <span data-ttu-id="3cc45-166">**Microsoft Operations Management Suite** 기본 대시보드에서 보안 및 감사 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-166">In the **Microsoft Operations Management Suite** main dashboard click Security and Audit tile.</span></span>
2. <span data-ttu-id="3cc45-167">**보안 및 감사** 대시보드에서 **보안 도메인**의 **ID 및 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-167">In the **Security and Audit** dashboard, click **Identity and Access** under **Security Domains**.</span></span> <span data-ttu-id="3cc45-168">**ID 및 액세스** 대시보드가 아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-168">The **Identity and Access** dashboard appears as shown below:</span></span>

![ID 및 액세스](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

<span data-ttu-id="3cc45-170">일반 모니터링 전략에 반드시 ID 모니터링을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-170">As part of your regular monitoring strategy, you must include identity monitoring.</span></span> <span data-ttu-id="3cc45-171">IT 관리자는 유효한 특정 사용자 이름에 여러 번의 시도가 있었는지 살펴보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-171">IT Admin should look if there is a specific valid username that has many attempts.</span></span> <span data-ttu-id="3cc45-172">그럴 경우 실제 사용자 이름을 확보한 공격자가 무차별 공격을 시도하고 있거나 자동 도구가 만료된 하드 코딩 비밀번호를 사용하는 있는 경우일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-172">This might indicate either attacker that acquired the real username and try to brute force or an automatic tool that uses hard-coded password that expired.</span></span>

<span data-ttu-id="3cc45-173">IT는 이 대시보드를 사용하여 회사 리소스에 잠재적 위협이 될 수 있는 ID 및 액세스를 빠르게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-173">This dashboard enable IT to quickly identify potential threats related to identity and access to company’s resources.</span></span> <span data-ttu-id="3cc45-174">잠재적 동향을 식별하는 것도 특히 중요합니다. 예를 들어 시간별 로그온 타일에서는 실패한 로그온 시도가 수행된 시간 및 횟수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-174">It is particular important to also identify potential trends, for example in the Logons Over Time tile, you can see over period of time how many times a failed logon attempt was performed.</span></span> <span data-ttu-id="3cc45-175">이 경우에는 **FileServer** 컴퓨터에 35회의 로그온 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-175">In this case the computer **FileServer** received 35 logon attempts.</span></span> <span data-ttu-id="3cc45-176">이 컴퓨터를 클릭하여 자세한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-176">You can explore more details about this computer by clicking on it.</span></span> 

![자세한 내용](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

<span data-ttu-id="3cc45-178">이 컴퓨터에 대해 생성된 보고서는 이 패턴에 대해 중요한 정보를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-178">The report generated for this computer brings valuable details about this pattern.</span></span> <span data-ttu-id="3cc45-179">**ACCOUNT** 열에는 시스템에 액세스를 시도하는 데 사용된 사용자 계정, **TIMEGENERATED** 열에는 시도가 수행된 시간 간격, **LOGONTYPENAME** 열에는 이 시도가 수행된 위치가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-179">Noticed that the **ACCOUNT** column gives you the user account that was used to try to access the system, the **TIMEGENERATED** column gives you the time interval in which the attempt was done and the **LOGONTYPENAME** column gives you the location where this attempt was done.</span></span> <span data-ttu-id="3cc45-180">이러한 시도가 시스템 안에서 프로그램에 의해 로컬로 수행된 경우 **PROCESS** 열에 프로세스 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-180">If these attempts were performed locally in the system by a program, the **PROCESS** column would be showing the process’s name.</span></span> <span data-ttu-id="3cc45-181">프로그램이 로그온 시도를 하는 시나리오에서는 이미 프로세스 이름을 알고 있으므로 대상 시스템에서 추가 조사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-181">In scenarios where the logon attempt is coming from a program, you already have the process name available and now you can perform further investigation in the target system.</span></span>

## <a name="see-also"></a><span data-ttu-id="3cc45-182">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3cc45-182">See also</span></span>
<span data-ttu-id="3cc45-183">이 문서에서는 OMS 보안 및 감사 솔루션을 사용하여 리소스를 모니터링하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc45-183">In this document, you learned how to use OMS Security and Audit solution to monitor your resources.</span></span> <span data-ttu-id="3cc45-184">OMS 보안에 대해 자세히 알아보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cc45-184">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="3cc45-185">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="3cc45-185">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="3cc45-186">Operations Management Suite 보안 및 감사 솔루션 시작</span><span class="sxs-lookup"><span data-stu-id="3cc45-186">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="3cc45-187">Operations Management Suite 보안 및 감사 솔루션의 보안 경고 모니터링 및 응답</span><span class="sxs-lookup"><span data-stu-id="3cc45-187">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)

