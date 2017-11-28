---
title: "Linux에 설치된 Azure Security Center 및 Azure Virtual Machines | Microsoft Docs"
description: "이 문서는 Azure Security Center에서 Azure Virtual Machines를 보호할 수 있는 방법을 이해하도록 돕습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: yurid
ms.openlocfilehash: 0df4fca59575bd8e18e91fea2066a9e694ed320d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-and-azure-virtual-machines-with-linux"></a><span data-ttu-id="d0a70-103">Linux에 설치된 Azure Security Center 및 Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d0a70-103">Azure Security Center and Azure Virtual Machines with Linux</span></span>
<span data-ttu-id="d0a70-104">[Azure Security Center](https://azure.microsoft.com/services/security-center/)를 통해 위협을 예방하고 감지하며 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-104">[Azure Security Center](https://azure.microsoft.com/services/security-center/) helps you prevent, detect, and respond to threats.</span></span> <span data-ttu-id="d0a70-105">이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-105">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="d0a70-106">이 문서에서는 Security Center가 Linux 운영 체제에서 실행되는 Azure VM(Virtual Machines)을 보호하는 데 어떻게 도움이 되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-106">This article shows how Security Center can help you secure your Azure Virtual Machines (VM) running Linux operating system.</span></span>

## <a name="why-use-security-center"></a><span data-ttu-id="d0a70-107">보안 센터를 사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="d0a70-107">Why use Security Center?</span></span>
<span data-ttu-id="d0a70-108">Security Center를 사용하면 가상 컴퓨터의 보안 설정에 가시성을 제공하고 위협을 모니터링하여 Azure에서 가상 컴퓨터의 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-108">Security Center helps you safeguard virtual machine data in Azure by providing visibility into your virtual machine’s security settings and monitoring for threats.</span></span> <span data-ttu-id="d0a70-109">Security Center는 다음의 목적으로 가상 컴퓨터를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-109">Security Center can monitor your virtual machines for:</span></span> 

* <span data-ttu-id="d0a70-110">권장된 구성 규칙으로 운영 체제(OS) 보안 설정</span><span class="sxs-lookup"><span data-stu-id="d0a70-110">Operating System (OS) security settings with the recommended configuration rules</span></span>
* <span data-ttu-id="d0a70-111">시스템 보안 및 누락된 중요 업데이트</span><span class="sxs-lookup"><span data-stu-id="d0a70-111">System security and critical updates that are missing</span></span>
* <span data-ttu-id="d0a70-112">끝점 보호 권장 사항</span><span class="sxs-lookup"><span data-stu-id="d0a70-112">Endpoint protection recommendations</span></span>
* <span data-ttu-id="d0a70-113">디스크 암호화 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="d0a70-113">Disk encryption validation</span></span>
* <span data-ttu-id="d0a70-114">네트워크 기반 공격([표준 버전](https://azure.microsoft.com/en-us/pricing/details/security-center/)에서만 사용할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="d0a70-114">Network based attacks (only available in [standard version](https://azure.microsoft.com/en-us/pricing/details/security-center/))</span></span>

<span data-ttu-id="d0a70-115">Security Center는 Azure VM을 보호하는 것 외에도, Cloud Services, App Services, 가상 네트워크 등에 대한 보안 모니터링 및 관리도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-115">In addition to helping protect your Azure VMs, Security Center also provides security monitoring and management for Cloud Services, App Services, Virtual Networks, and more.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0a70-116">Azure Security Center에 대한 자세한 내용은 [Azure Security Center 소개](security-center-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-116">See [Introduction to Azure Security Center](security-center-intro.md) to learn more about Azure Security Center.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d0a70-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d0a70-117">Prerequisites</span></span>
<span data-ttu-id="d0a70-118">Azure Security Center를 시작하려면 다음 사항을 이해하고 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-118">To get started with Azure Security Center, you’ll need to know and consider the following:</span></span>

* <span data-ttu-id="d0a70-119">Microsoft Azure를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-119">You must have a subscription to Microsoft Azure.</span></span> <span data-ttu-id="d0a70-120">보안 센터의 무료 및 표준 계층에 대한 자세한 내용은 [보안 센터 가격 책정](https://azure.microsoft.com/pricing/details/security-center/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-120">See [Security Center Pricing](https://azure.microsoft.com/pricing/details/security-center/) for more information on Security Center’s free and standard tiers.</span></span>
* <span data-ttu-id="d0a70-121">보안 센터 도입을 계획하는 경우 계획 및 작업 고려 사항에 대한 자세한 내용은 [Azure Security Center 계획 및 작업 가이드](security-center-planning-and-operations-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-121">Plan your Security Center adoption, see [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md) to learn more about planning and operations considerations.</span></span>
* <span data-ttu-id="d0a70-122">운영 체제 지원 가능성에 대한 정보는 [Azure Security Center FAQ(질문과 대답)](security-center-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-122">For information regarding operating system supportability, see [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md).</span></span> 

## <a name="set-security-policy"></a><span data-ttu-id="d0a70-123">보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="d0a70-123">Set security policy</span></span>
<span data-ttu-id="d0a70-124">Azure Security Center에서 구성한 보안 정책을 기반으로 생성된 권장 사항 및 경고를 제공하는 데 필요한 정보를 수집할 수 있도록 데이터 수집을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-124">Data collection needs to be enabled so that Azure Security Center can gather the information it needs to provide recommendations and alerts that are generated based on the security policy you configure.</span></span> <span data-ttu-id="d0a70-125">아래 그림에서 **데이터 수집**이 **사용**으로 설정된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-125">In the figure below, you can see that **Data collection** has been turned **On**.</span></span>

<span data-ttu-id="d0a70-126">보안 정책은 지정된 구독 또는 리소스 그룹 내에서 리소스에 대해 권장되는 제어 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-126">A security policy defines the set of controls which are recommended for resources within the specified subscription or resource group.</span></span> <span data-ttu-id="d0a70-127">보안 정책을 활성화하기 전에 데이터 수집을 활성화해야 합니다. 보안 센터는 해당 보안 상태를 평가하고 보안 권장 사항을 제공하며 위협에 경고하기 위해 가상 컴퓨터에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-127">Before enabling security policy, you must have data collection enabled, Security Center collects data from your virtual machines in order to assess their security state, provide security recommendations, and alert you to threats.</span></span> <span data-ttu-id="d0a70-128">보안 센터에서 회사의 보안 요구 사항 및 응용 프로그램 유형 또는 각 구독의 데이터 민감도에 따라 Azure 구독 또는 리소스 그룹에 대한 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-128">In Security Center, you define policies for your Azure subscriptions or resource groups according to your company’s security needs and the type of applications or sensitivity of the data in each subscription.</span></span> 

![보안 정책](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig1.png)

> [!NOTE]
> <span data-ttu-id="d0a70-130">사용 가능한 각 **방지 정책**을 알아보려면 [보안 정책 설정](security-center-policies.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-130">To learn more about each **Prevention policy** available, see [Set security policies](security-center-policies.md) article.</span></span>
> 

## <a name="manage-security-recommendations"></a><span data-ttu-id="d0a70-131">보안 권장 사항 관리</span><span class="sxs-lookup"><span data-stu-id="d0a70-131">Manage security recommendations</span></span>
<span data-ttu-id="d0a70-132">보안 센터에서는 Azure 리소스의 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-132">Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="d0a70-133">보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-133">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="d0a70-134">권장 사항은 필요한 컨트롤을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-134">The recommendations guide you through the process of configuring the needed controls.</span></span>

<span data-ttu-id="d0a70-135">보안 정책이 설정되면 보안 센터는 리소스의 보안 상태를 분석하여 잠재적인 취약성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-135">After setting a security policy, Security Center analyzes the security state of your resources to identify potential vulnerabilities.</span></span> <span data-ttu-id="d0a70-136">권장 사항은 각 줄이 한 가지 특정 권장을 나타내는 표 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-136">The recommendations are shown in a table format where each line represents one particular recommendation.</span></span> <span data-ttu-id="d0a70-137">아래 테이블에서는 Linux 운영 체제에서 실행되는 Azure VM에 대한 권장 사항의 일부 예제 및 이를 적용할 경우 권장 사항 각각의 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-137">The table below provides some examples of recommendations for Azure VMs running Linux operating system and what each one will do if you apply it.</span></span> <span data-ttu-id="d0a70-138">권장 사항을 선택하면 보안 센터에서 권장 사항을 구현하는 방법을 보여 주는 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-138">When you select a recommendation, you will be provided information that shows you how to implement the recommendation in Security Center.</span></span>

| <span data-ttu-id="d0a70-139">권장 사항</span><span class="sxs-lookup"><span data-stu-id="d0a70-139">Recommendation</span></span> | <span data-ttu-id="d0a70-140">설명</span><span class="sxs-lookup"><span data-stu-id="d0a70-140">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="d0a70-141">구독에 대해 데이터 수집 활성화</span><span class="sxs-lookup"><span data-stu-id="d0a70-141">Enable data collection for subscriptions</span></span>](security-center-enable-data-collection.md) |<span data-ttu-id="d0a70-142">구독 또는 구독의 VM(가상 컴퓨터) 각각에 대해 보안 정책에서 데이터 수집을 켜는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-142">Recommends that you turn on data collection in the security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span></span> |
| [<span data-ttu-id="d0a70-143">OS 취약성 해결</span><span class="sxs-lookup"><span data-stu-id="d0a70-143">Remediate OS vulnerabilities</span></span>](security-center-remediate-os-vulnerabilities.md) |<span data-ttu-id="d0a70-144">OS 구성을 권장 구성 규칙과 정렬하라는 권장 사항입니다. 예를 들어 암호 저장을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-144">Recommends that you align your OS configurations with the recommended configuration rules, e.g. do not allow passwords to be saved.</span></span> |
| [<span data-ttu-id="d0a70-145">시스템 업데이트 적용</span><span class="sxs-lookup"><span data-stu-id="d0a70-145">Apply system updates</span></span>](security-center-apply-system-updates.md) |<span data-ttu-id="d0a70-146">누락된 시스템 보안 및 중요 업데이트를 VM에 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-146">Recommends that you deploy missing system security and critical updates to VMs.</span></span> |
| [<span data-ttu-id="d0a70-147">시스템 업데이트 후 다시 부팅</span><span class="sxs-lookup"><span data-stu-id="d0a70-147">Reboot after system updates</span></span>](security-center-apply-system-updates.md#reboot-after-system-updates) |<span data-ttu-id="d0a70-148">시스템 업데이트 적용 프로세스를 완료하려면 VM을 다시 부팅하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-148">Recommends that you reboot a VM to complete the process of applying system updates.</span></span> |
| [<span data-ttu-id="d0a70-149">VM 에이전트 사용</span><span class="sxs-lookup"><span data-stu-id="d0a70-149">Enable VM Agent</span></span>](security-center-enable-vm-agent.md) |<span data-ttu-id="d0a70-150">VM 에이전트가 필요한 VM을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-150">Enables you to see which VMs require the VM Agent.</span></span> <span data-ttu-id="d0a70-151">패치 검색, 기준 검색 및 맬웨어 방지 프로그램을 프로비전하려면 VM에 VM 에이전트가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-151">The VM Agent must be installed on VMs in order to provision patch scanning, baseline scanning, and antimalware programs.</span></span> <span data-ttu-id="d0a70-152">Azure 마켓플레이스에서 배포된 VM에 VM 에이전트가 기본적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-152">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="d0a70-153">[VM 에이전트 및 확장 - 2부](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) 문서에 VM 에이전트 설치 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-153">The article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span> |
| [<span data-ttu-id="d0a70-154">디스크 암호화 적용</span><span class="sxs-lookup"><span data-stu-id="d0a70-154">Apply disk encryption</span></span>](security-center-apply-disk-encryption.md) |<span data-ttu-id="d0a70-155">Azure 디스크 암호화(Windows 및 Linux VM)를 사용하여 VM 디스크를 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-155">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span></span> <span data-ttu-id="d0a70-156">VM에서 OS 및 데이터 볼륨에 암호화를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-156">Encryption is recommended for both the OS and data volumes on your VM.</span></span> |


> [!NOTE]
> <span data-ttu-id="d0a70-157">권장 사항에 대한 자세한 내용은 [보안 권장 사항 관리](security-center-recommendations.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-157">To learn more about recommendations, see [Managing security recommendations](security-center-recommendations.md) article.</span></span>
> 

## <a name="monitor-security-health"></a><span data-ttu-id="d0a70-158">보안 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="d0a70-158">Monitor security health</span></span>
<span data-ttu-id="d0a70-159">구독의 리소스에 대한 [보안 정책](security-center-policies.md) 을 활성화한 후에 보안 센터는 리소스의 보안을 분석하여 잠재적 취약성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-159">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center will analyze the security of your resources to identify potential vulnerabilities.</span></span>  <span data-ttu-id="d0a70-160">**리소스 보안 상태** 블레이드의 문제와 함께 리소스의 보안 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-160">You can view the security state of your resources, along with any issues in the **Resource security health** blade.</span></span> <span data-ttu-id="d0a70-161">**리소스 보안** 상태 타일에서 **가상 컴퓨터**를 클릭하면 VM에 대한 권장 사항이 포함된 **가상 컴퓨터** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-161">When you click **Virtual machines** in the **Resource security** health tile, the **Virtual machines** blade will open with recommendations for your VMs.</span></span> 

![보안 상태](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-to-security-alerts"></a><span data-ttu-id="d0a70-163">보안 경고 관리 및 응답</span><span class="sxs-lookup"><span data-stu-id="d0a70-163">Manage and respond to security alerts</span></span>
<span data-ttu-id="d0a70-164">보안 센터는 방화벽 및 끝점 보호 솔루션과 같은 Azure 리소스, 네트워크 및 연결된 파트너 솔루션의 로그 데이터를 자동으로 수집하고 분석하며 통합하여 실제 위협을 감지하고 가양성을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-164">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions (like firewall and endpoint protection solutions), to detect real threats and reduce false positives.</span></span> <span data-ttu-id="d0a70-165">[검색 기능](security-center-detection-capabilities.md)의 다양한 집계를 활용하여 보안 센터는 신속하게 문제를 조사하고 가능한 공격을 해결하는 방법에 대한 권장 사항을 제공할 수 있도록 우선 순위가 지정된 보안 경고를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-165">By leveraging a diverse aggregation of [detection capabilities](security-center-detection-capabilities.md), Security Center is able to generate prioritized security alerts to help you quickly investigate the problem and provide recommendations for how to remediate possible attacks.</span></span>

![보안 경고](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

<span data-ttu-id="d0a70-167">보안 경고를 선택하여 해당 경고를 트리거하는 이벤트 및 공격을 완화하기 위해 수행해야 하는 단계(있는 경우)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-167">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="d0a70-168">보안 경고는 [형식](security-center-alerts-type.md) 및 날짜별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-168">Security alerts are grouped by [type](security-center-alerts-type.md) and date.</span></span>

## <a name="monitor-security-health"></a><span data-ttu-id="d0a70-169">보안 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="d0a70-169">Monitor security health</span></span>
<span data-ttu-id="d0a70-170">구독의 리소스에 대한 [보안 정책](security-center-policies.md) 을 활성화한 후에 보안 센터는 리소스의 보안을 분석하여 잠재적 취약성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-170">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center will analyze the security of your resources to identify potential vulnerabilities.</span></span>  <span data-ttu-id="d0a70-171">**리소스 보안 상태** 블레이드의 문제와 함께 리소스의 보안 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-171">You can view the security state of your resources, along with any issues in the **Resource security health** blade.</span></span> <span data-ttu-id="d0a70-172">**리소스 보안** 상태 타일에서 **가상 컴퓨터**를 클릭하면 VM에 대한 권장 사항이 포함된 **가상 컴퓨터** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-172">When you click **Virtual machines** in the **Resource security** health tile, the **Virtual machines** blade will open with recommendations for your VMs.</span></span> 

![보안 상태](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig4.png)

<span data-ttu-id="d0a70-174">이 권장 사항을 클릭하면 해당 문제를 해결하기 위해 취해야 하는 특정 작업에 대한 자세한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-174">If you click on this recommendation, you will see more details about the specific actions that should be taken to address those issues.</span></span> <span data-ttu-id="d0a70-175">**권장 사항**의 블레이드 아래쪽에 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-175">The details will appear in the bottom of the blade, under **Recommendations**.</span></span> 

![보안 상태 2](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig5.png)


## <a name="see-also"></a><span data-ttu-id="d0a70-177">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d0a70-177">See also</span></span>
<span data-ttu-id="d0a70-178">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0a70-178">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="d0a70-179">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-179">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d0a70-180">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-180">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d0a70-181">[Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a70-181">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>

