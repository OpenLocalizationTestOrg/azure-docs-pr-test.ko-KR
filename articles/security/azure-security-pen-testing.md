---
title: "펜 테스트 | Microsoft Docs"
description: "이 문서는 침투 테스트 (pentest) 프로세스의 개요와 Azure 인프라에서 실행 중인 앱에 대해 pentest를 수행하는 방법을 제공합니다."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 070e848f753452953b9e5dfe94799e7c0a314530
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="pen-testing"></a><span data-ttu-id="c5b27-103">펜 테스트</span><span class="sxs-lookup"><span data-stu-id="c5b27-103">Pen Testing</span></span>
<span data-ttu-id="c5b27-104">응용 프로그램 테스트 및 배포를 위해 Microsoft Azure를 사용하는 장점은 응용 프로그램을 개발하고, 테스트하고, 배포하기 위해 온-프레미스 인프라를 준비할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-104">One of the great things about using Microsoft Azure for application testing and deployment is that you don’t need to put together an on-premises infrastructure to develop, test and deploy your applications.</span></span> <span data-ttu-id="c5b27-105">모든 인프라는 Microsoft Azure Platform 서비스에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-105">All the infrastructure is taken care of by the Microsoft Azure platform services.</span></span> <span data-ttu-id="c5b27-106">자신의 온-프레미스 하드웨어 요청, 구입, “래킹과 스태킹(racking and stacking)”에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-106">You don’t have to worry about requisitioning, acquiring, and “racking and stacking” your own on-premises hardware.</span></span>

<span data-ttu-id="c5b27-107">이것은 좋은 일입니다 – 그렇지만 여전히 일반적인 보안 실사는 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-107">This is great – but you still need to make sure you perform your normal security due diligence.</span></span> <span data-ttu-id="c5b27-108">수행해야 할 일 중 하나는 Azure에서 배포하는 응용 프로그램에 대한 침투 테스트를 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-108">One of the things you need to do is penetration test the applications you deploy in Azure.</span></span>

<span data-ttu-id="c5b27-109">Microsoft가 [Azure 환경에서의 침투 테스트](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)를 수행하는 것에 관해 어쩌면 이미 알고 계실 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-109">You might already know that Microsoft performs [penetration testing of our Azure environment](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e).</span></span> <span data-ttu-id="c5b27-110">이는 보안 제어를 개선하고, 신규 보안 제어를 소개하고, 보안 프로세스를 개선하는 관점에서 우리 작업을 이끌고 플랫폼을 개선하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-110">This helps us improve our platform and guides our actions in terms of improving security controls, introducing new security controls, and improving our security processes.</span></span>

<span data-ttu-id="c5b27-111">우리는 여러분을 위해 응용 프로그램을 펜 테스트하지는 않지만, 여러분이 자신의 응용 프로그램에 펜 테스트를 수행하기를 원하며 그럴 필요가 있다는 것을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-111">We don’t pen test your application for you, but we do understand that you will want and need to perform pen testing on your own applications.</span></span> <span data-ttu-id="c5b27-112">응용 프로그램의 보안을 강화할 때 Azure 전체 에코시스템을 보다 안전하게 보호하는데 도움이 되기 때문에 그렇게 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-112">That’s a good thing, because when you enhance the security of your applications, you help make the entire Azure ecosystem more secure.</span></span>

<span data-ttu-id="c5b27-113">응용 프로그램을 펜 테스트할 때, 우리가 공격받고 있는 것처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-113">When you pen test your applications, it might look like an attack to us.</span></span> <span data-ttu-id="c5b27-114">우리는 공격 패턴에 대해 [지속적인 모니터링](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) 을 하며 필요에 따라 인시던트 대응 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-114">We [continuously monitor](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) for attack patterns and will initiate an incident response process if we need to.</span></span> <span data-ttu-id="c5b27-115">여러분 자신의 펜 테스트 실사 때문에 인시턴트 대응을 트리거한다면 여러분과 우리에게 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-115">It doesn’t help you and it doesn’t help us if we trigger an incident response due to your own due diligence pen testing.</span></span>

<span data-ttu-id="c5b27-116">그렇다면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="c5b27-116">What to do?</span></span>

<span data-ttu-id="c5b27-117">Azure 호스팅 응용 프로그램을 펜 테스트할 준비가 되면 [Microsoft에 알려주시기 바랍니다](https://portal.msrc.microsoft.com/en-us/engage/pentest).</span><span class="sxs-lookup"><span data-stu-id="c5b27-117">When you’re ready to pen test your Azure-hosted applications, you have an option to [let us know](https://portal.msrc.microsoft.com/en-us/engage/pentest).</span></span> <span data-ttu-id="c5b27-118">특정 테스트를 수행할 것이라고 알게 되면 [Microsoft Cloud 통합 침투 테스트 참여 규칙(영문)](https://technet.microsoft.com/en-us/mt784683)에서 설명한 대로 테스트에서 Azure 펜 테스트 조건을 따르는 한 테스트가 실수로 종료되지 않을 것입니다(예: 여러분이 테스트 중인 IP 주소 차단).</span><span class="sxs-lookup"><span data-stu-id="c5b27-118">Once we know that you’re going to be performing specific tests, we won’t inadvertently shut you down (such as blocking the IP address that you’re testing from), as long as your tests conform to the Azure pen testing terms and conditions described in [Microsoft Cloud Unified Penetration Testing Rules of Engagement](https://technet.microsoft.com/en-us/mt784683).</span></span>
<span data-ttu-id="c5b27-119">여러분이 수행할 수 있는 표준 테스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-119">Standard tests you can perform include:</span></span>

* <span data-ttu-id="c5b27-120">[OWASP(Open Web Application Security Project) 취약점 상위 10개](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span><span class="sxs-lookup"><span data-stu-id="c5b27-120">Tests on your endpoints to uncover the [Open Web Application Security Project (OWASP) top 10 vulnerabilities](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span></span>
* <span data-ttu-id="c5b27-121">[퍼지 테스트](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) </span><span class="sxs-lookup"><span data-stu-id="c5b27-121">[Fuzz testing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) of your endpoints</span></span>
* <span data-ttu-id="c5b27-122">[포트 검색](https://en.wikipedia.org/wiki/Port_scanner) </span><span class="sxs-lookup"><span data-stu-id="c5b27-122">[Port scanning](https://en.wikipedia.org/wiki/Port_scanner) of your endpoints</span></span>

<span data-ttu-id="c5b27-123">여러분이 수행할 수 없는 한가지 유형의 테스트는 모든 종류의 [서비스 거부 (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-123">One type of test that you can’t perform is any kind of [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) attack.</span></span> <span data-ttu-id="c5b27-124">이는 DoS 공격 자체를 시작하거나, 모든 종류의 DoS 공격을 결정, 시연 또는 시뮬레이션할 수도 있는 관련 테스트를 수행하는 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-124">This includes initiating a DoS attack itself, or performing related tests that might determine, demonstrate or simulate any type of DoS attack.</span></span>

<span data-ttu-id="c5b27-125">Microsoft Azure에서 호스팅된 응용 프로그램의 펜 테스트를 시작할 준비가 되셨습니까?</span><span class="sxs-lookup"><span data-stu-id="c5b27-125">Are you ready to get started with pen testing your applications hosted in Microsoft Azure?</span></span> <span data-ttu-id="c5b27-126">그렇다면, [침투 테스트 개요](https://technet.microsoft.com/library/mt784683.aspx) 페이지를 참조하고 (페이지 맨 아래에 있는 테스트 요청 만들기 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-126">If so, then head on over to the [Penetration Test Overview](https://technet.microsoft.com/library/mt784683.aspx) page (and click the Create a Testing Request button at the bottom of the page.</span></span> <span data-ttu-id="c5b27-127">또한 펜 테스트 조건에 대한 더 많은 정보와 Azure 또는 다른 모든 Microsoft 서비스와 관련된 보안 결함을 보고할 수 방법에 대한 유용한 링크도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b27-127">You’ll also find more information on the pen testing terms and conditions and helpful links on how you can report security flaws related to Azure or any other Microsoft service.</span></span>
