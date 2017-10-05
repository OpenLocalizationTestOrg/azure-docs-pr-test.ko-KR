---
title: "Microsoft Azure Cloud Services FAQ에 대한 응용 프로그램 및 서비스 사용 가능성 문제 | Microsoft Docs"
description: "이 문서는 Microsoft Azure Cloud Services의 응용 프로그램 및 서비스 사용 가능성에 대한 질문과 대답을 나열합니다."
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
ms.openlocfilehash: a893a6d009dd018ad440964419e0a5a1963084b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="f9d13-103">Azure Cloud Services의 응용 프로그램 및 서비스 사용 가능성 문제: FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="f9d13-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="f9d13-104">이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 응용 프로그램 및 서비스 사용 가능성 문제에 대한 질문과 대답을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="f9d13-105">크기 정보는 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="f9d13-106">내 역할은 재활용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-106">My role got recycled.</span></span> <span data-ttu-id="f9d13-107">클라우드 서비스에 롤아웃된 업데이트가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f9d13-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="f9d13-108">Microsoft에서는 대략 한 달에 한 번 Windows Azure PaaS VM에 대한 새 게스트 OS 버전을 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="f9d13-109"> 이러한 업데이트로 게스트 OS가 파이프라인에서 유일합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-109"> The Guest OS is only one such update in the pipeline.</span></span> <span data-ttu-id="f9d13-110">릴리스는 다른 요인에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="f9d13-111">또한 Azure는 수 천만 대의 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="f9d13-112">따라서 역할이 다시 부팅되는 정확한 날짜와 시간을 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-112">Therefore, it's impossible to predict the exact date and time when your roles will reboot.</span></span> <span data-ttu-id="f9d13-113">최신 정보로 게스트 OS 업데이트 RSS 피드를 업데이트하지만 보고된 시간은 대략적인 값을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-113">We update the Guest OS Update RSS Feed with the latest information that we have, but you should consider that reported time to be an approximate value.</span></span> <span data-ttu-id="f9d13-114">고객에 문제가 있어 정확하게 재부팅 시간을 제한하도록 작업 중인 것으로 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-114">We are aware that this is problematic for customers and are working on a plan to limit or precisely time reboots.</span></span>

<span data-ttu-id="f9d13-115">최신 게스트 OS 업데이트에 대한 자세한 내용은 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](cloud-services-guestos-update-matrix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d13-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="f9d13-116">게스트 및 호스트 OS 업데이트의 기술 세부 정보에 대한 다시 시작 및 포인터에 도움이 되는 정보는 [OS 업그레이드로 인한 역할 인스턴스 다시 시작](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)이라는 MSDN 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d13-116">For helpful information on restarts and pointers to technical details of Guest and Host OS updates, see the MSDN blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-the-first-request-to-my-cloud-service-after-the-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="f9d13-117">서비스가 일정 시간 동안 유휴 상태가 된 후에 클라우드 서비스에 대한 첫 번째 요청이 평소보다 오래 걸리는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f9d13-117">Why does the first request to my cloud service after the service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="f9d13-118">웹 서버가 첫 번째 요청을 받으면 먼저 코드를 다시 컴파일하고 다음 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-118">When the Web Server receives the first request, it first recompiles the code and then processes the request.</span></span> <span data-ttu-id="f9d13-119">바로 이러한 이유로 첫 번째 요청은 다른 항목보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-119">That's why the first request takes longer than the others.</span></span> <span data-ttu-id="f9d13-120">기본적으로 앱 풀은 사용자가 휴지하는 경우에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-120">By default, the app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="f9d13-121">또한 앱 풀은 기본적으로 1,740분(29시간)마다 재활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-121">The app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="f9d13-122">응용 프로그램, 중단 또는 메모리 누수를 일으킬 수 있는 불안정한 경우 상태를 방지하기 위해 IIS(인터넷 정보 서비스) 응용 프로그램 풀을 정기적으로 재활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-122">Internet Information Services (IIS) application pools can be periodically recycled to avoid unstable states that can lead to application crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="f9d13-123">다음 문서는 이 문제를 이해하고 완화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-123">The following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="f9d13-124">IIS에서 느린 초기 로드 수정</span><span class="sxs-lookup"><span data-stu-id="f9d13-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="f9d13-125">앱 풀 재활용이 느려진 후 IIS 7.5 웹 응용 프로그램 첫 번째 요청</span><span class="sxs-lookup"><span data-stu-id="f9d13-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="f9d13-126">IIS의 기본 동작을 변경하려는 경우 웹 역할 인스턴스에 변경 내용을 수동으로 적용하면 변경 내용이 손실되기 때문에 시작 작업을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d13-126">If you want to change the default behavior of IIS, you will need to use startup tasks, because if you manually apply changes to the Web Role instances, the changes will eventually be lost.</span></span>

<span data-ttu-id="f9d13-127">자세한 내용은 [클라우드 서비스에 대한 시작 작업 구성 및 실행 방법](cloud-services-startup-tasks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d13-127">For more information, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
