---
title: "클라우드 서비스 배포 문제를 aaaTroubleshoot | Microsoft Docs"
description: "몇 가지 일반적인 문제는 클라우드 서비스 tooAzure를 배포할 때 발생할 수 있습니다. 이 문서에서는 그 중 솔루션 toosome 합니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a><span data-ttu-id="b1aba-104">클라우드 서비스 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b1aba-104">Troubleshoot cloud service deployment problems</span></span>
<span data-ttu-id="b1aba-105">클라우드 서비스 응용 프로그램 패키지 tooAzure를 배포할 때 hello에서 hello 배포에 대 한 정보를 얻을 수 있습니다 **속성** hello Azure 포털의에서 창.</span><span class="sxs-lookup"><span data-stu-id="b1aba-105">When you deploy a cloud service application package tooAzure, you can obtain information about hello deployment from hello **Properties** pane in hello Azure portal.</span></span> <span data-ttu-id="b1aba-106">Hello 세부 정보를 사용할 수 있습니다 hello 클라우드 서비스 문제를 해결 하는이 창 toohelp으로 및 새로운 지원 요청을 열 때이 정보 tooAzure 지원을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-106">You can use hello details in this pane toohelp you troubleshoot problems with hello cloud service, and you can provide this information tooAzure Support when opening a new support request.</span></span>

<span data-ttu-id="b1aba-107">Hello를 찾을 수 있습니다 **속성** 다음과 같이 창:</span><span class="sxs-lookup"><span data-stu-id="b1aba-107">You can find hello **Properties** pane as follows:</span></span>

* <span data-ttu-id="b1aba-108">에 hello Azure 포털 클라우드 서비스의 hello 배포를 클릭 하 고 **모든 설정을**, 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-108">In hello Azure portal, click hello deployment of your cloud service, click **All settings**, and then click **Properties**.</span></span>
* <span data-ttu-id="b1aba-109">에 Azure 클래식 포털 hello 클라우드 서비스의 hello 배포를 클릭 하 고 **대시보드**hello 페이지의 hello 오른쪽 아래 모서리에 있는 (아래 **눈에 보는**).</span><span class="sxs-lookup"><span data-stu-id="b1aba-109">In hello Azure classic portal, click hello deployment of your cloud service, click **DASHBOARD**, located at hello lower-right corner of hello page (under **quick glance**).</span></span> <span data-ttu-id="b1aba-110">이 창에 대한 "속성" 레이블이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-110">Be aware that there's no "Properties" label on this pane.</span></span>

> [!NOTE]
> <span data-ttu-id="b1aba-111">Hello의 hello 내용을 복사할 수는 있지만 **속성** hello hello 창 오른쪽 위 모서리에 hello 아이콘을 클릭 하 여 창 toohello 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-111">You can copy hello contents of hello **Properties** pane toohello clipboard by clicking hello icon in hello upper-right corner of hello pane.</span></span>
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a><span data-ttu-id="b1aba-112">문제: 내 배포가 시작되고 모든 역할 인스턴스가 준비되었지만 내 웹 사이트에 액세스할 수가 없어요</span><span class="sxs-lookup"><span data-stu-id="b1aba-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span></span>
<span data-ttu-id="b1aba-113">hello 웹 사이트 URL 링크 hello 포털에 표시 된 hello 포트를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-113">hello website URL link shown in hello portal does not include hello port.</span></span> <span data-ttu-id="b1aba-114">웹 사이트에 대 한 hello 기본 포트는 80입니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-114">hello default port for websites is 80.</span></span> <span data-ttu-id="b1aba-115">다른 포트에서 구성 된 toorun 응용 프로그램을 사용 하는 경우 hello 웹 사이트에 액세스할 때 hello 올바른 포트 번호 toohello URL에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-115">If your application is configured toorun in a different port, you must add hello correct port number toohello URL when accessing hello website.</span></span>

1. <span data-ttu-id="b1aba-116">Hello Azure 포털에서에서 클라우드 서비스의 hello 배포를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-116">In hello Azure portal, click hello deployment of your cloud service.</span></span>
2. <span data-ttu-id="b1aba-117">Hello에 **속성** hello 역할 인스턴스에 대 한 hello 포트를 확인 하는 hello Azure 포털의 창 (아래 **입력 끝점**).</span><span class="sxs-lookup"><span data-stu-id="b1aba-117">In hello **Properties** pane of hello Azure portal, check hello ports for hello role instances (under **Input Endpoints**).</span></span>
3. <span data-ttu-id="b1aba-118">Hello 포트 80 없으면 hello 응용 프로그램에 액세스할 때 hello 올바른 포트 값 toohello URL을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-118">If hello port is not 80, add hello correct port value toohello URL when you access hello application.</span></span> <span data-ttu-id="b1aba-119">toospecify 기본이 아닌 포트 공백 없이 hello 포트 번호 뒤에 오는 콜론 (:) 다음 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-119">toospecify a non-default port, type hello URL, followed by a colon (:), followed by hello port number, with no spaces.</span></span>

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a><span data-ttu-id="b1aba-120">문제: 아무 것도 하지 않았는데 내 역할 인스턴스가 재활용되었어요</span><span class="sxs-lookup"><span data-stu-id="b1aba-120">Problem: My role instances recycled without me doing anything</span></span>
<span data-ttu-id="b1aba-121">서비스 복구는 Azure에서 문제 노드를 검색 하 고 따라서 역할 인스턴스 toonew 노드를 이동 하는 경우 자동으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances toonew nodes.</span></span> <span data-ttu-id="b1aba-122">이 경우 역할 인스턴스가 자동으로 재활용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-122">When this occurs, you might see your role instances recycling automatically.</span></span> <span data-ttu-id="b1aba-123">했는지 toofind 서비스 오류가 발생 했습니다 복구:</span><span class="sxs-lookup"><span data-stu-id="b1aba-123">toofind out if service healing occurred:</span></span>

1. <span data-ttu-id="b1aba-124">Hello Azure 포털에서에서 클라우드 서비스의 hello 배포를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-124">In hello Azure portal, click hello deployment of your cloud service.</span></span>
2. <span data-ttu-id="b1aba-125">Hello에 **속성** hello Azure 포털의 창 hello 정보를 검토 하 고 hello 역할 재활용을 관찰 하는 hello 시간 동안 발생 한 서비스 복구 것인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-125">In hello **Properties** pane of hello Azure portal, review hello information and determine whether service healing occurred during hello time that you observed hello roles recycling.</span></span>

<span data-ttu-id="b1aba-126">또한 역할은 호스트 OS와 게스트 OS를 업데이트하는 동안 대략 한 달에 한 번 정도 재활용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span></span>  
<span data-ttu-id="b1aba-127">자세한 내용은 hello 블로그 게시물을 참조 하십시오. [tooOS 업그레이드를 다시 시작 인 한 역할 인스턴스](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span><span class="sxs-lookup"><span data-stu-id="b1aba-127">For more information, see hello blog post [Role Instance Restarts Due tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span></span>

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a><span data-ttu-id="b1aba-128">문제: VIP 교환을 수행하고 오류를 받을 수 없어요</span><span class="sxs-lookup"><span data-stu-id="b1aba-128">Problem: I cannot do a VIP swap and receive an error</span></span>
<span data-ttu-id="b1aba-129">배포 업데이트가 진행 중인 경우 VIP 교환이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-129">A VIP swap is not allowed if a deployment update is in progress.</span></span> <span data-ttu-id="b1aba-130">배포 업데이트가 다음과 같은 경우 자동으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-130">Deployment updates can occur automatically when:</span></span>

* <span data-ttu-id="b1aba-131">새 게스트 운영 체제를 사용할 수 있고 자동 업데이트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-131">A new guest operating system is available and you are configured for automatic updates.</span></span>
* <span data-ttu-id="b1aba-132">서비스 복구가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-132">Service healing occurs.</span></span>

<span data-ttu-id="b1aba-133">out toofind 자동 업데이트 하는 경우로 인해 VIP 교체를 수행:</span><span class="sxs-lookup"><span data-stu-id="b1aba-133">toofind out if an automatic update is preventing you from doing a VIP swap:</span></span>

1. <span data-ttu-id="b1aba-134">Hello Azure 포털에서에서 클라우드 서비스의 hello 배포를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-134">In hello Azure portal, click hello deployment of your cloud service.</span></span>
2. <span data-ttu-id="b1aba-135">Hello에 **속성** hello Azure 포털의 창 hello 값을 살펴보고 **상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-135">In hello **Properties** pane of hello Azure portal, look at hello value of **Status**.</span></span> <span data-ttu-id="b1aba-136">이 경우 **준비**, 다음 확인 **마지막 작업** toosee 최근에 발생 한 경우에 hello VIP swap 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-136">If it is **Ready**, then check **Last operation** toosee if one recently happened that might prevent hello VIP swap.</span></span>
3. <span data-ttu-id="b1aba-137">Hello 프로덕션 배포에 대 한 1 및 2 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-137">Repeat steps 1 and 2 for hello production deployment.</span></span>
4. <span data-ttu-id="b1aba-138">자동 업데이트 프로세스에 있으면 대기 동안 toodo hello VIP 교체 하기 전에 toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-138">If an automatic update is in process, wait for it toofinish before trying toodo hello VIP swap.</span></span>

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a><span data-ttu-id="b1aba-139">문제: 역할 인스턴스가 시작됨, 초기화 중, 사용 중 및 중지됨 사이를 반복해요</span><span class="sxs-lookup"><span data-stu-id="b1aba-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span></span>
<span data-ttu-id="b1aba-140">이 상태는 응용 프로그램 코드, 패키지 또는 구성 파일에 문제가 있음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-140">This condition could indicate a problem with your application code, package, or configuration file.</span></span> <span data-ttu-id="b1aba-141">이 경우 몇 분 마다 변경 수 toosee hello 상태 수 있으며 hello Azure 포털 이라는 메시지가 표시와 같은 **재활용**, **Busy**, 또는 **Initializing**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-141">In that case, you should be able toosee hello status changing every few minutes and hello Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span></span> <span data-ttu-id="b1aba-142">이 hello 역할 인스턴스가 실행에서 상태를 유지 하는 hello 응용 프로그램 문제가 된다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-142">This indicates that there is something wrong with hello application that is keeping hello role instance from running.</span></span>

<span data-ttu-id="b1aba-143">방법에 대 한 자세한 내용은 hello 블로그 게시물을 참조 하는이 문제에 대 한 tootroubleshoot [Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) 및 [일반적인 문제가 그 원인 역할 toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-143">For more information on how tootroubleshoot for this problem, see hello blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

## <a name="problem-my-application-stopped-working"></a><span data-ttu-id="b1aba-144">문제: 내 응용 프로그램의 작동이 중지되었어요</span><span class="sxs-lookup"><span data-stu-id="b1aba-144">Problem: My application stopped working</span></span>
1. <span data-ttu-id="b1aba-145">Azure 포털 hello hello 역할 인스턴스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-145">In hello Azure portal, click hello role instance.</span></span>
2. <span data-ttu-id="b1aba-146">Hello에 **속성** hello Azure 포털의 창 hello 조건 tooresolve 다음 문제를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-146">In hello **Properties** pane of hello Azure portal, consider hello following conditions tooresolve your problem:</span></span>
   * <span data-ttu-id="b1aba-147">Hello 역할 인스턴스가 최근에 중지 된 경우 (의 hello 값을 확인할 수 있습니다 **중단 횟수**), hello 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-147">If hello role instance has recently stopped (you can check hello value of **Abort count**), hello deployment could be updating.</span></span> <span data-ttu-id="b1aba-148">Hello 역할 인스턴스는 자체에서 작동 하 고 다시 시작 하면 toosee를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-148">Wait toosee if hello role instance resumes functioning on its own.</span></span>
   * <span data-ttu-id="b1aba-149">Hello 역할 인스턴스가 **Busy**, 응용 프로그램 코드 toosee 경우 확인 hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-149">If hello role instance is **Busy**, check your application code toosee if hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span></span> <span data-ttu-id="b1aba-150">이 이벤트를 처리 하는 일부 코드를 수정 또는 tooadd 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-150">You might need tooadd or fix some code that handles this event.</span></span>
   * <span data-ttu-id="b1aba-151">Hello 진단 데이터를 통해 이동 하 고 문제 해결 시나리오 hello 블로그 게시물에서 [Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-151">Go through hello diagnostic data and troubleshooting scenarios in hello blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="b1aba-152">클라우드 서비스를 재활용 하는 경우 다시 설정 hello 배포에 대 한 hello 속성 지워집니다 hello 원래 문제에 대 한 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-152">If you recycle your cloud service, you reset hello properties for hello deployment, effectively erasing hello information for hello original problem.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b1aba-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1aba-153">Next steps</span></span>
<span data-ttu-id="b1aba-154">클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="b1aba-155">Azure PaaS 컴퓨터 진단 데이터를 사용 하 여 tootroubleshoot 클라우드 서비스 역할을 발급 하는 방법을 toolearn 참조 [Kevin Williamson 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1aba-155">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
