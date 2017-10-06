---
title: "aaaApplication 및 서비스 가용성 문제를 Microsoft Azure 클라우드 서비스 FAQ | Microsoft Docs"
description: "이 문서는 질문과 대답 응용 프로그램 및 서비스 가용성에 대 한 Microsoft Azure 클라우드 서비스에 대 한 hello를 나열 합니다."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="4cd5a-103">Azure Cloud Services의 응용 프로그램 및 서비스 사용 가능성 문제: FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="4cd5a-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="4cd5a-104">이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 응용 프로그램 및 서비스 사용 가능성 문제에 대한 질문과 대답을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="4cd5a-105">Hello를 참조할 수 있습니다 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 크기 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="4cd5a-106">내 역할은 재활용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-106">My role got recycled.</span></span> <span data-ttu-id="4cd5a-107">클라우드 서비스에 롤아웃된 업데이트가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4cd5a-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="4cd5a-108">Microsoft에서는 대략 한 달에 한 번 Windows Azure PaaS VM에 대한 새 게스트 OS 버전을 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="4cd5a-109"> 게스트 OS는 hello 파이프라인에서 이러한 하나만 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-109"> The Guest OS is only one such update in hello pipeline.</span></span> <span data-ttu-id="4cd5a-110">릴리스는 다른 요인에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="4cd5a-111">또한 Azure는 수 천만 대의 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="4cd5a-112">따라서 사용자 역할이 다시 부팅 되 면 불가능 한 toopredict hello 정확한 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-112">Therefore, it's impossible toopredict hello exact date and time when your roles will reboot.</span></span> <span data-ttu-id="4cd5a-113">게스트 OS 업데이트 RSS 피드 hello을 hello 최신 정보로 업데이트 되지만 하는 시간 toobe 대략적인 값을 보고 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-113">We update hello Guest OS Update RSS Feed with hello latest information that we have, but you should consider that reported time toobe an approximate value.</span></span> <span data-ttu-id="4cd5a-114">이 고객에 대 한 문제가 인식 하 고 계획 toolimit 또는 정확 하 게 번 재부팅에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-114">We are aware that this is problematic for customers and are working on a plan toolimit or precisely time reboots.</span></span>

<span data-ttu-id="4cd5a-115">최신 게스트 OS 업데이트에 대한 자세한 내용은 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](cloud-services-guestos-update-matrix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="4cd5a-116">게스트 및 호스트 OS 업데이트의 다시 시작 및 포인터 tootechnical 세부 사항에서 유용한 정보 hello MSDN 블로그 게시물을 참조 하십시오. [역할 인 인스턴스 다시 시작 tooOS 업그레이드](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-116">For helpful information on restarts and pointers tootechnical details of Guest and Host OS updates, see hello MSDN blog post [Role Instance Restarts Due tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="4cd5a-117">Hello 첫 번째 요청 toomy 클라우드 서비스 hello 서비스 얼마 동안 유휴 상태가 된 후 않습니다 이유 평소 보다 오래 걸릴?</span><span class="sxs-lookup"><span data-stu-id="4cd5a-117">Why does hello first request toomy cloud service after hello service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="4cd5a-118">웹 서버 hello hello 첫 번째 요청을 받으면 먼저 hello 코드를 다시 컴파일하 하 고 hello 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-118">When hello Web Server receives hello first request, it first recompiles hello code and then processes hello request.</span></span> <span data-ttu-id="4cd5a-119">하는 이유 hello hello 보다 긴 첫 번째 요청은 다른 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-119">That's why hello first request takes longer than hello others.</span></span> <span data-ttu-id="4cd5a-120">기본적으로 hello 응용 프로그램 풀 사용자 일정의 경우에서 종료를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-120">By default, hello app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="4cd5a-121">hello 응용 프로그램 풀은 또한 재활용 기본적으로 모든 1,740 분 (29 시간) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-121">hello app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="4cd5a-122">인터넷 정보 서비스 (IIS) 응용 프로그램 풀 tooapplication 충돌, 중단 또는 메모리 누수를 발생 시킬 수 있는 정기적으로 재활용된 tooavoid 불안정 한 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-122">Internet Information Services (IIS) application pools can be periodically recycled tooavoid unstable states that can lead tooapplication crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="4cd5a-123">다음 문서는 hello 이해 및이 문제를 완화 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-123">hello following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="4cd5a-124">IIS에서 느린 초기 로드 수정</span><span class="sxs-lookup"><span data-stu-id="4cd5a-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="4cd5a-125">앱 풀 재활용이 느려진 후 IIS 7.5 웹 응용 프로그램 첫 번째 요청</span><span class="sxs-lookup"><span data-stu-id="4cd5a-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="4cd5a-126">IIS의 toochange hello 기본 동작을 사용 하도록 하려는 경우 변경 내용을 toohello 웹 역할 인스턴스를 수동으로 적용 하는 경우 hello 변경 결국 없어집니다 때문에 toouse 시작 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-126">If you want toochange hello default behavior of IIS, you will need toouse startup tasks, because if you manually apply changes toohello Web Role instances, hello changes will eventually be lost.</span></span>

<span data-ttu-id="4cd5a-127">자세한 내용은 참조 [방식과 tooconfigure 또는 실행 시작을 클라우드 서비스에 대 한 작업](cloud-services-startup-tasks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd5a-127">For more information, see [How tooconfigure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
