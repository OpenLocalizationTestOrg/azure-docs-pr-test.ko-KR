---
title: "aaaPen 테스트 | Microsoft Docs"
description: "hello 문서 hello 침투 테스트 (pentest) 프로세스의 개요를 제공 하 고 어떻게 pentest Azure 인프라에서 실행 중인 앱에 대해 수행 합니다."
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
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a><span data-ttu-id="9449d-103">펜 테스트</span><span class="sxs-lookup"><span data-stu-id="9449d-103">Pen Testing</span></span>
<span data-ttu-id="9449d-104">응용 프로그램 테스트 및 배포에 대 한 Microsoft Azure를 사용 하는 방법에 대 한 hello 뛰어난 기능 중 하나는 필요 하지 않습니다 tooput 함께 온-프레미스 인프라 toodevelop, 테스트 및 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-104">One of hello great things about using Microsoft Azure for application testing and deployment is that you don’t need tooput together an on-premises infrastructure toodevelop, test and deploy your applications.</span></span> <span data-ttu-id="9449d-105">모든 hello 인프라 hello Microsoft Azure 플랫폼 서비스에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-105">All hello infrastructure is taken care of by hello Microsoft Azure platform services.</span></span> <span data-ttu-id="9449d-106">참조, 취득 및 "획득 및 스택" 하는 방법에 대 한 tooworry 없는 자신의 온-프레미스 하드웨어가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-106">You don’t have tooworry about requisitioning, acquiring, and “racking and stacking” your own on-premises hardware.</span></span>

<span data-ttu-id="9449d-107">– 유용 하지만 toomake 일반 보안을 수행 해야 하 due 성실 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-107">This is great – but you still need toomake sure you perform your normal security due diligence.</span></span> <span data-ttu-id="9449d-108">하나 hello 일로 toodo가 침투 테스트 hello 응용 프로그램이 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-108">One of hello things you need toodo is penetration test hello applications you deploy in Azure.</span></span>

<span data-ttu-id="9449d-109">Microsoft가 [Azure 환경에서의 침투 테스트](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)를 수행하는 것에 관해 어쩌면 이미 알고 계실 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-109">You might already know that Microsoft performs [penetration testing of our Azure environment](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e).</span></span> <span data-ttu-id="9449d-110">이는 보안 제어를 개선하고, 신규 보안 제어를 소개하고, 보안 프로세스를 개선하는 관점에서 우리 작업을 이끌고 플랫폼을 개선하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-110">This helps us improve our platform and guides our actions in terms of improving security controls, introducing new security controls, and improving our security processes.</span></span>

<span data-ttu-id="9449d-111">펜 하지 않는 우리 원하는 사용자의 응용 프로그램에 대 한 테스트 tooperform 펜 필요 점을 이해 수행 하지만, 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-111">We don’t pen test your application for you, but we do understand that you will want and need tooperform pen testing on your own applications.</span></span> <span data-ttu-id="9449d-112">Hello 전체 Azure 에코 시스템을 보다 안전 하 게 도움말 hello 응용 프로그램의 보안을 강화 하는 경우 때문 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-112">That’s a good thing, because when you enhance hello security of your applications, you help make hello entire Azure ecosystem more secure.</span></span>

<span data-ttu-id="9449d-113">펜 하면 응용 프로그램을 테스트 하는 경우 공격 toous 유사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-113">When you pen test your applications, it might look like an attack toous.</span></span> <span data-ttu-id="9449d-114">우리는 공격 패턴에 대해 [지속적인 모니터링](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) 을 하며 필요에 따라 인시던트 대응 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-114">We [continuously monitor](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) for attack patterns and will initiate an incident response process if we need to.</span></span> <span data-ttu-id="9449d-115">하는 데 도움이 되지 않습니다 및 म 사고 대응을 트리거하는 경우 우리 도움이 되지 않습니다 due tooyour 성실 펜 테스트 인해 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-115">It doesn’t help you and it doesn’t help us if we trigger an incident response due tooyour own due diligence pen testing.</span></span>

<span data-ttu-id="9449d-116">어떤 toodo?</span><span class="sxs-lookup"><span data-stu-id="9449d-116">What toodo?</span></span>

<span data-ttu-id="9449d-117">준비가 끝나면 toopen Azure 호스팅 응용 프로그램을 테스트, 하는 옵션이 너무[알려주세요](https://portal.msrc.microsoft.com/en-us/engage/pentest)합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-117">When you’re ready toopen test your Azure-hosted applications, you have an option too[let us know](https://portal.msrc.microsoft.com/en-us/engage/pentest).</span></span> <span data-ttu-id="9449d-118">Toobe 특정 테스트를 수행 하는 것을 알고 있으므로 म 않습니다 실수로 (예:에서 테스트 하는 hello IP 주소를 차단 하는) 종료, 테스트 toohello Azure를 준수 상태로 펜 테스트 약관 에설명된[Microsoft 클라우드 통합 침투 업무 규칙 테스트](https://technet.microsoft.com/en-us/mt784683)합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-118">Once we know that you’re going toobe performing specific tests, we won’t inadvertently shut you down (such as blocking hello IP address that you’re testing from), as long as your tests conform toohello Azure pen testing terms and conditions described in [Microsoft Cloud Unified Penetration Testing Rules of Engagement](https://technet.microsoft.com/en-us/mt784683).</span></span>
<span data-ttu-id="9449d-119">여러분이 수행할 수 있는 표준 테스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-119">Standard tests you can perform include:</span></span>

* <span data-ttu-id="9449d-120">끝점 toouncover hello에 대 한 검사 [열기 웹 응용 프로그램 보안 프로젝트 (OWASP) 상위 10 개의 취약성](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span><span class="sxs-lookup"><span data-stu-id="9449d-120">Tests on your endpoints toouncover hello [Open Web Application Security Project (OWASP) top 10 vulnerabilities](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span></span>
* <span data-ttu-id="9449d-121">[퍼지 테스트](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) </span><span class="sxs-lookup"><span data-stu-id="9449d-121">[Fuzz testing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) of your endpoints</span></span>
* <span data-ttu-id="9449d-122">[포트 검색](https://en.wikipedia.org/wiki/Port_scanner) </span><span class="sxs-lookup"><span data-stu-id="9449d-122">[Port scanning](https://en.wikipedia.org/wiki/Port_scanner) of your endpoints</span></span>

<span data-ttu-id="9449d-123">여러분이 수행할 수 없는 한가지 유형의 테스트는 모든 종류의 [서비스 거부 (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-123">One type of test that you can’t perform is any kind of [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) attack.</span></span> <span data-ttu-id="9449d-124">이는 DoS 공격 자체를 시작하거나, 모든 종류의 DoS 공격을 결정, 시연 또는 시뮬레이션할 수도 있는 관련 테스트를 수행하는 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-124">This includes initiating a DoS attack itself, or performing related tests that might determine, demonstrate or simulate any type of DoS attack.</span></span>

<span data-ttu-id="9449d-125">Microsoft Azure에서 호스팅된 응용 프로그램을 테스트 하는 펜 시작 tooget 준비는?</span><span class="sxs-lookup"><span data-stu-id="9449d-125">Are you ready tooget started with pen testing your applications hosted in Microsoft Azure?</span></span> <span data-ttu-id="9449d-126">가 없으면, toohello 통해에 헤드 [침투 테스트 개요](https://technet.microsoft.com/library/mt784683.aspx) 페이지 (한 hello 만들기 hello hello 페이지 맨 아래에 요청 테스트 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-126">If so, then head on over toohello [Penetration Test Overview](https://technet.microsoft.com/library/mt784683.aspx) page (and click hello Create a Testing Request button at hello bottom of hello page.</span></span> <span data-ttu-id="9449d-127">계약 조건과 어떻게 결점 관련된 tooAzure 보안 또는 기타 Microsoft 서비스를 보고할 수 있습니다에 유용한 링크를 테스트 하는 hello 펜 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9449d-127">You’ll also find more information on hello pen testing terms and conditions and helpful links on how you can report security flaws related tooAzure or any other Microsoft service.</span></span>
