---
title: "Azure Security Center에서 웹 응용 프로그램 방화벽 추가 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **웹 응용 프로그램 방화벽 추가** 및 **응용 프로그램 보호 완료**를 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: d04a07237029953d8a9b20704d85e852ce45d867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="5b547-103">Azure 보안 센터에서 웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="5b547-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="5b547-104">Azure Security Center에서는 웹 응용 프로그램을 보호하기 위해 Microsoft 파트너의 WAF(웹 응용 프로그램 방화벽)를 추가하도록 권장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span></span> <span data-ttu-id="5b547-105">이 문서에서는 이 권장 사항을 적용하는 방법의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-105">This document walks you through an example of how to apply this recommendation.</span></span>

<span data-ttu-id="5b547-106">공개 인바운드 웹 포트(80,443)으로 연결된 네트워크 보안 그룹에 있는 모든 공용 연결 IP(인스턴스 수준 IP 또는 부하 분산된 IP)에 대해 WAF 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="5b547-107">Security Center에서는 가상 컴퓨터와 App Service 환경에 있는 웹 응용 프로그램을 대상으로 한 공격을 방어할 수 있도록 WAF를 프로비전할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="5b547-108">ASE(App Service 환경)는 Azure App Service의 [프리미엄](https://azure.microsoft.com/pricing/details/app-service/) 서비스 계획 옵션으로, Azure App Service 앱의 안전한 실행을 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="5b547-109">ASE에 대한 자세한 내용을 보려면 [App Service Environment 설명서](../app-service/app-service-app-service-environments-readme.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b547-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5b547-110">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="5b547-111">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="5b547-112">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="5b547-112">Implement the recommendation</span></span>
1. <span data-ttu-id="5b547-113">**권장 사항** 블레이드에서 **웹 응용 프로그램 방화벽을 사용하여 웹 응용 프로그램 보호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="5b547-114">![웹 응용 프로그램 보안][1]</span><span class="sxs-lookup"><span data-stu-id="5b547-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="5b547-115">**웹 응용 프로그램 방화벽을 사용하여 웹 응용 프로그램을 보호** 블레이드에서 웹 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="5b547-116">**웹 응용 프로그램 방화벽 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-116">The **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="5b547-117">![Add a web application firewall][2]</span><span class="sxs-lookup"><span data-stu-id="5b547-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="5b547-118">기존 웹 응용 프로그램 방화벽(사용 가능한 경우)을 사용하도록 선택하거나, 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-118">You can choose to use an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="5b547-119">이 예제에서는 기존 WAF가 없으므로 WAF를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="5b547-120">WAF를 만들려면 통합 파트너 목록에서 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-120">To create a WAF, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="5b547-121">이 예제에서는 **Barracuda Web Application Firewall**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="5b547-122">파트너 솔루션에 대한 정보를 제공하는 **Barracuda Web Application Firewall** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="5b547-123">정보 블레이드에서 **만들기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-123">Select **Create** in the information blade.</span></span>

   ![방화벽 정보 블레이드][3]

6. <span data-ttu-id="5b547-125">**새 웹 응용 프로그램 방화벽** 블레이드가 열립니다 이 블레이드에서 **VM 구성** 단계를 수행하고 **WAF 정보**를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="5b547-126">**VM 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="5b547-127">**VM 구성** 블레이드에서 WAF를 실행할 가상 컴퓨터를 스핀업하는 데 필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span></span>
   <span data-ttu-id="5b547-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="5b547-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="5b547-129">**새 웹 응용 프로그램 방화벽** 블레이드로 돌아가서 **WAF 정보**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="5b547-130">**WAF 정보** 블레이드에서 WAF 자체를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-130">In the **WAF Information** blade, you configure the WAF itself.</span></span> <span data-ttu-id="5b547-131">7단계에서는 WAF가 실행되는 가상 컴퓨터를 구성하고 8단계에서는 WAF 자체를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="5b547-132">응용 프로그램 보호 완료</span><span class="sxs-lookup"><span data-stu-id="5b547-132">Finalize application protection</span></span>
1. <span data-ttu-id="5b547-133">**권장 사항** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-133">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="5b547-134">WAF를 만든 후에 **응용 프로그램 보호 완료**라고 하는 새 항목이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="5b547-135">새 항목을 사용하면 Azure 가상 네트워크 내에서 WAF를 연결하는 프로세스를 완료하여 응용 프로그램을 보호할 수 있다는 점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span></span>

   ![응용 프로그램 보호 완료][5]

2. <span data-ttu-id="5b547-137">**응용 프로그램 보호 완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="5b547-138">새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-138">A new blade opens.</span></span> <span data-ttu-id="5b547-139">해당 트래픽 경로를 전환해야 하는 웹 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-139">You can see that there is a web application that needs to have its traffic rerouted.</span></span>
3. <span data-ttu-id="5b547-140">웹 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-140">Select the web application.</span></span> <span data-ttu-id="5b547-141">웹 응용 프로그램 방화벽 설정을 완료하는 단계를 알려주는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span></span> <span data-ttu-id="5b547-142">단계를 완료한 다음 **트래픽 제한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-142">Complete the steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="5b547-143">그려면 Security Center가 연결을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-143">Security Center then does the wiring-up for you.</span></span>

   ![트래픽 제한][6]

> [!NOTE]
> <span data-ttu-id="5b547-145">기존 WAF 배포에 이러한 응용 프로그램을 추가하여 보안 센터에서 여러 웹 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span>
>
>

<span data-ttu-id="5b547-146">이제 해당 WAF의 로그가 완전히 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-146">The logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="5b547-147">보안 센터에서 자동으로 로그를 수집 및 분석하기 시작하여 중요한 보안 경고를 사용자에게 드러낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b547-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b547-148">Next steps</span></span>
<span data-ttu-id="5b547-149">이 문서에서는 보안 센터 권장 사항 "웹 응용 프로그램 추가"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="5b547-150">웹 응용 프로그램 방화벽 구성에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b547-150">To learn more about configuring a web application firewall, see the following:</span></span>

* [<span data-ttu-id="5b547-151">앱 서비스 환경에 대한 웹 응용 프로그램 방화벽(WAF) 구성</span><span class="sxs-lookup"><span data-stu-id="5b547-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="5b547-152">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b547-152">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="5b547-153">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5b547-154">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="5b547-155">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="5b547-156">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5b547-157">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="5b547-158">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5b547-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
