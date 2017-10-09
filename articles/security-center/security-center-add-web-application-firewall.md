---
title: "Azure 보안 센터에서 웹 응용 프로그램 방화벽 aaaAdd | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 추가 웹 응용 프로그램 방화벽 * * 및 * * 응용 프로그램 보호 * * 마무리 합니다."
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
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="84911-103">Azure 보안 센터에서 웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="84911-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="84911-104">Azure 보안 센터를 추가 하는 웹 응용 프로그램 방화벽 (WAF)는 Microsoft 파트너 toosecure에서 웹 응용 프로그램을 권장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner toosecure your web applications.</span></span> <span data-ttu-id="84911-105">이 문서 과정을 안내 하는 방법의 예 tooapply이이 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-105">This document walks you through an example of how tooapply this recommendation.</span></span>

<span data-ttu-id="84911-106">공개 인바운드 웹 포트(80,443)으로 연결된 네트워크 보안 그룹에 있는 모든 공용 연결 IP(인스턴스 수준 IP 또는 부하 분산된 IP)에 대해 WAF 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="84911-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="84911-107">보안 센터 앱 서비스 환경 및 가상 컴퓨터에서 웹 응용 프로그램을 대상으로 하는 공격 방어 WAF toohelp 구축 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-107">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="84911-108">ASE(App Service 환경)는 Azure App Service의 [프리미엄](https://azure.microsoft.com/pricing/details/app-service/) 서비스 계획 옵션으로, Azure App Service 앱의 안전한 실행을 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="84911-109">toolearn ASE에 대 한 자세한 참조 hello [앱 서비스 환경 설명서](../app-service/app-service-app-service-environments-readme.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-109">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="84911-110">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="84911-111">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="84911-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="84911-112">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="84911-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="84911-113">Hello에 **권장 사항을** 블레이드를 **웹 응용 프로그램 방화벽을 사용 하 여 웹 응용 프로그램을 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-113">In hello **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="84911-114">![웹 응용 프로그램 보안][1]</span><span class="sxs-lookup"><span data-stu-id="84911-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="84911-115">Hello에 **웹 응용 프로그램 방화벽을 사용 하 여 웹 응용 프로그램을 보호** 블레이드를 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-115">In hello **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="84911-116">hello **추가 웹 응용 프로그램 방화벽** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="84911-116">hello **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="84911-117">![웹 응용 프로그램 방화벽 추가][2]</span><span class="sxs-lookup"><span data-stu-id="84911-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="84911-118">선택할 수 있습니다 toouse 기존 웹 응용 프로그램 방화벽 사용 가능한 경우 또는 새를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-118">You can choose toouse an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="84911-119">이 예제에서는 기존 WAF가 없으므로 WAF를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="84911-120">WAF toocreate hello 통합된 파트너 목록에서 솔루션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-120">toocreate a WAF, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="84911-121">이 예제에서는 **Barracuda Web Application Firewall**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="84911-122">hello **Barracuda 웹 응용 프로그램 방화벽** 블레이드에서 열립니다 hello 업체 솔루션에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-122">hello **Barracuda Web Application Firewall** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="84911-123">선택 **만들기** hello 정보 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-123">Select **Create** in hello information blade.</span></span>

   ![방화벽 정보 블레이드][3]

6. <span data-ttu-id="84911-125">hello **새 웹 응용 프로그램 방화벽** 수행할 수 있는 블레이드 열리고 **VM 구성** 제공 하 여 단계 **WAF 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-125">hello **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="84911-126">**VM 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="84911-127">Hello에 **VM 구성** 정보를 실행 하는 hello 가상 컴퓨터를 필요한 toospin hello WAF 입력 블레이드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84911-127">In hello **VM Configuration** blade, you enter information required toospin up hello virtual machine that runs hello WAF.</span></span>
   <span data-ttu-id="84911-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="84911-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="84911-129">Toohello 반환 **새 웹 응용 프로그램 방화벽** 블레이드에 대 한 선택 **WAF 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-129">Return toohello **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="84911-130">Hello에 **WAF 정보** 블레이드에서 hello WAF 자체를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-130">In hello **WAF Information** blade, you configure hello WAF itself.</span></span> <span data-ttu-id="84911-131">7 단계는 hello WAF에서 실행 되 고 8 단계 사용 하면 자체 WAF tooprovision hello tooconfigure hello 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-131">Step 7 allows you tooconfigure hello virtual machine on which hello WAF runs and step 8 enables you tooprovision hello WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="84911-132">응용 프로그램 보호 완료</span><span class="sxs-lookup"><span data-stu-id="84911-132">Finalize application protection</span></span>
1. <span data-ttu-id="84911-133">Toohello 반환 **권장 사항을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="84911-133">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="84911-134">새 항목을 호출 하는 hello WAF를 만든 후 생성 된 **응용 프로그램 보호 완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-134">A new entry was generated after you created hello WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="84911-135">이 항목에는 toocomplete hello 과정 실제로 hello 응용 프로그램을 보호할 수 있도록 hello Azure 가상 네트워크 내에서 WAF hello를 연결 해야 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-135">This entry lets you know that you need toocomplete hello process of actually wiring up hello WAF within hello Azure Virtual Network so that it can protect hello application.</span></span>

   ![응용 프로그램 보호 완료][5]

2. <span data-ttu-id="84911-137">**응용 프로그램 보호 완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="84911-138">새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="84911-138">A new blade opens.</span></span> <span data-ttu-id="84911-139">Toohave 해 해당 트래픽을 하는 웹 응용 프로그램 있다는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-139">You can see that there is a web application that needs toohave its traffic rerouted.</span></span>
3. <span data-ttu-id="84911-140">Hello 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-140">Select hello web application.</span></span> <span data-ttu-id="84911-141">블레이드는 hello 웹 응용 프로그램 방화벽 설치를 완료 하는 중에 단계 수 있게 해 주는 열립니다.</span><span class="sxs-lookup"><span data-stu-id="84911-141">A blade opens that gives you steps for finalizing hello web application firewall setup.</span></span> <span data-ttu-id="84911-142">Hello 단계를 완료 한 다음 선택 **트래픽을 제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-142">Complete hello steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="84911-143">다음 보안 센터 배선 접속 드립니다 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-143">Security Center then does hello wiring-up for you.</span></span>

   ![트래픽 제한][6]

> [!NOTE]
> <span data-ttu-id="84911-145">이러한 응용 프로그램 tooyour 기존 WAF 배포를 추가 하 여 보안 센터에서 여러 웹 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-145">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span>
>
>

<span data-ttu-id="84911-146">이제 해당 WAF에서 hello 로그 완전히 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84911-146">hello logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="84911-147">보안 센터 자동으로 수집 하 고 중요 한 보안 경고 tooyou를 표면 수 있도록 hello 로그 분석을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-147">Security Center can start automatically gathering and analyzing hello logs so that it can surface important security alerts tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84911-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84911-148">Next steps</span></span>
<span data-ttu-id="84911-149">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "웹 응용 프로그램을 추가 합니다."</span><span class="sxs-lookup"><span data-stu-id="84911-149">This document showed you how tooimplement hello Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="84911-150">웹 응용 프로그램 방화벽 구성에 대 한 더 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-150">toolearn more about configuring a web application firewall, see hello following:</span></span>

* [<span data-ttu-id="84911-151">앱 서비스 환경에 대한 웹 응용 프로그램 방화벽(WAF) 구성</span><span class="sxs-lookup"><span data-stu-id="84911-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="84911-152">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-152">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="84911-153">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="84911-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="84911-154">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="84911-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="84911-155">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="84911-155">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="84911-156">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="84911-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="84911-157">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="84911-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="84911-158">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="84911-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
