---
title: "클라우드 서비스 배포 문제 해결 | Microsoft Docs"
description: "Azure에 클라우드 서비스를 배포할 때 발생할 수 있는 몇 가지 일반적인 문제가 있습니다. 이 문서에서는 그 중 일부에 대한 솔루션을 제공합니다."
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
ms.openlocfilehash: 60e06ba292ff1e43d00cd69c1a422f9237d5e5a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a><span data-ttu-id="e3a03-104">클라우드 서비스 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e3a03-104">Troubleshoot cloud service deployment problems</span></span>
<span data-ttu-id="e3a03-105">Azure에 클라우드 서비스 응용 프로그램 패키지를 배포할 때 Azure 포털의 **속성** 창에서 배포에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-105">When you deploy a cloud service application package to Azure, you can obtain information about the deployment from the **Properties** pane in the Azure portal.</span></span> <span data-ttu-id="e3a03-106">클라우드 서비스에 발생한 문제를 해결하기 위해 이 창에서 세부 정보를 사용할 수 있고 새로운 지원 요청을 할 때 Azure 지원 센터에 이 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-106">You can use the details in this pane to help you troubleshoot problems with the cloud service, and you can provide this information to Azure Support when opening a new support request.</span></span>

<span data-ttu-id="e3a03-107">다음과 같이 **속성** 창을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-107">You can find the **Properties** pane as follows:</span></span>

* <span data-ttu-id="e3a03-108">Azure 포털에서 클라우드 서비스의 배포, **모든 설정**, **속성**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-108">In the Azure portal, click the deployment of your cloud service, click **All settings**, and then click **Properties**.</span></span>
* <span data-ttu-id="e3a03-109">Azure 클래식 포털에서: 클라우드 서비스의 배포, **대시보드**를 차례로 클릭하고 페이지의 오른쪽 아래로 이동합니다(**간략 상태** 아래).</span><span class="sxs-lookup"><span data-stu-id="e3a03-109">In the Azure classic portal, click the deployment of your cloud service, click **DASHBOARD**, located at the lower-right corner of the page (under **quick glance**).</span></span> <span data-ttu-id="e3a03-110">이 창에 대한 "속성" 레이블이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-110">Be aware that there's no "Properties" label on this pane.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a03-111">창의 오른쪽 위 모서리에 있는 아이콘을 클릭하여 **속성** 창의 내용을 클립보드에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-111">You can copy the contents of the **Properties** pane to the clipboard by clicking the icon in the upper-right corner of the pane.</span></span>
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a><span data-ttu-id="e3a03-112">문제: 내 배포가 시작되고 모든 역할 인스턴스가 준비되었지만 내 웹 사이트에 액세스할 수가 없어요</span><span class="sxs-lookup"><span data-stu-id="e3a03-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span></span>
<span data-ttu-id="e3a03-113">포털에 표시된 웹 사이트 URL 링크에는 포트가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-113">The website URL link shown in the portal does not include the port.</span></span> <span data-ttu-id="e3a03-114">웹 사이트의 기본 포트는 80입니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-114">The default port for websites is 80.</span></span> <span data-ttu-id="e3a03-115">응용 프로그램이 다른 포트에서 실행되도록 구성된 경우 웹 사이트에 액세스할 때 URL에 올바른 포트 번호를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-115">If your application is configured to run in a different port, you must add the correct port number to the URL when accessing the website.</span></span>

1. <span data-ttu-id="e3a03-116">Azure 포털에서 클라우드 서비스의 배포를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-116">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="e3a03-117">Azure 포털의 **속성** 창에서 역할 인스턴스에 대한 포트를 확인합니다(**입력 끝점**에서).</span><span class="sxs-lookup"><span data-stu-id="e3a03-117">In the **Properties** pane of the Azure portal, check the ports for the role instances (under **Input Endpoints**).</span></span>
3. <span data-ttu-id="e3a03-118">포트가 80인 경우 응용 프로그램에 액세스할 때 URL에 올바른 포트 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-118">If the port is not 80, add the correct port value to the URL when you access the application.</span></span> <span data-ttu-id="e3a03-119">기본이 아닌 포트를 지정하려면 뒤에 콜론(:)과 공백 없이 포트 번호를 붙인 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-119">To specify a non-default port, type the URL, followed by a colon (:), followed by the port number, with no spaces.</span></span>

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a><span data-ttu-id="e3a03-120">문제: 아무 것도 하지 않았는데 내 역할 인스턴스가 재활용되었어요</span><span class="sxs-lookup"><span data-stu-id="e3a03-120">Problem: My role instances recycled without me doing anything</span></span>
<span data-ttu-id="e3a03-121">Azure에서 문제가 있는 노드를 검색하고 따라서 역할 인스턴스를 새 노드로 이동하는 경우 서비스 복구가 자동으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances to new nodes.</span></span> <span data-ttu-id="e3a03-122">이 경우 역할 인스턴스가 자동으로 재활용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-122">When this occurs, you might see your role instances recycling automatically.</span></span> <span data-ttu-id="e3a03-123">서비스 복구가 수행되었는지 검색하려면</span><span class="sxs-lookup"><span data-stu-id="e3a03-123">To find out if service healing occurred:</span></span>

1. <span data-ttu-id="e3a03-124">Azure 포털에서 클라우드 서비스의 배포를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-124">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="e3a03-125">Azure 포털의 **속성** 창에서 정보를 검토하고 역할이 재활용된 것을 관찰하는 동안 서비스 복구가 발생했는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-125">In the **Properties** pane of the Azure portal, review the information and determine whether service healing occurred during the time that you observed the roles recycling.</span></span>

<span data-ttu-id="e3a03-126">또한 역할은 호스트 OS와 게스트 OS를 업데이트하는 동안 대략 한 달에 한 번 정도 재활용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span></span>  
<span data-ttu-id="e3a03-127">자세한 내용은 [OS 업그레이드로 인해 역할 인스턴스 다시 시작](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span><span class="sxs-lookup"><span data-stu-id="e3a03-127">For more information, see the blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span></span>

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a><span data-ttu-id="e3a03-128">문제: VIP 교환을 수행하고 오류를 받을 수 없어요</span><span class="sxs-lookup"><span data-stu-id="e3a03-128">Problem: I cannot do a VIP swap and receive an error</span></span>
<span data-ttu-id="e3a03-129">배포 업데이트가 진행 중인 경우 VIP 교환이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-129">A VIP swap is not allowed if a deployment update is in progress.</span></span> <span data-ttu-id="e3a03-130">배포 업데이트가 다음과 같은 경우 자동으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-130">Deployment updates can occur automatically when:</span></span>

* <span data-ttu-id="e3a03-131">새 게스트 운영 체제를 사용할 수 있고 자동 업데이트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-131">A new guest operating system is available and you are configured for automatic updates.</span></span>
* <span data-ttu-id="e3a03-132">서비스 복구가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-132">Service healing occurs.</span></span>

<span data-ttu-id="e3a03-133">자동 업데이트가 VIP 교체를 수행을 방해하는지 알아보려면:</span><span class="sxs-lookup"><span data-stu-id="e3a03-133">To find out if an automatic update is preventing you from doing a VIP swap:</span></span>

1. <span data-ttu-id="e3a03-134">Azure 포털에서 클라우드 서비스의 배포를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-134">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="e3a03-135">Azure 포털의 **속성** 창에서 **상태** 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-135">In the **Properties** pane of the Azure portal, look at the value of **Status**.</span></span> <span data-ttu-id="e3a03-136">**준비**인 경우 **마지막 작업**을 확인하여 최근에 VIP 교체를 방해한 작업이 발생했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-136">If it is **Ready**, then check **Last operation** to see if one recently happened that might prevent the VIP swap.</span></span>
3. <span data-ttu-id="e3a03-137">프로덕션 배포에 1단계와 2단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-137">Repeat steps 1 and 2 for the production deployment.</span></span>
4. <span data-ttu-id="e3a03-138">자동 업데이트가 실행 중인 경우 VIP 교체를 시도하기 전에 완료되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-138">If an automatic update is in process, wait for it to finish before trying to do the VIP swap.</span></span>

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a><span data-ttu-id="e3a03-139">문제: 역할 인스턴스가 시작됨, 초기화 중, 사용 중 및 중지됨 사이를 반복해요</span><span class="sxs-lookup"><span data-stu-id="e3a03-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span></span>
<span data-ttu-id="e3a03-140">이 상태는 응용 프로그램 코드, 패키지 또는 구성 파일에 문제가 있음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-140">This condition could indicate a problem with your application code, package, or configuration file.</span></span> <span data-ttu-id="e3a03-141">이 경우 몇 분마다 상태가 변경되는 것을 확인할 수 있어야 하고 Azure 포털은 **재활용 중**, **사용 중** 또는 **초기화 중**과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-141">In that case, you should be able to see the status changing every few minutes and the Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span></span> <span data-ttu-id="e3a03-142">역할 인스턴스의 실행을 방해하는 응용 프로그램에 문제가 있다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-142">This indicates that there is something wrong with the application that is keeping the role instance from running.</span></span>

<span data-ttu-id="e3a03-143">이 문제를 해결하는 방법에 대한 자세한 내용은 [Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) 및 [역할을 재활용하는 일반적인 문제](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md) 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3a03-143">For more information on how to troubleshoot for this problem, see the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles to recycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

## <a name="problem-my-application-stopped-working"></a><span data-ttu-id="e3a03-144">문제: 내 응용 프로그램의 작동이 중지되었어요</span><span class="sxs-lookup"><span data-stu-id="e3a03-144">Problem: My application stopped working</span></span>
1. <span data-ttu-id="e3a03-145">Azure 포털에서 역할 인스턴스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-145">In the Azure portal, click the role instance.</span></span>
2. <span data-ttu-id="e3a03-146">Azure 포털의 **속성** 창에서 다음 조건을 고려하여 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-146">In the **Properties** pane of the Azure portal, consider the following conditions to resolve your problem:</span></span>
   * <span data-ttu-id="e3a03-147">역할 인스턴스가 최근에 중지된 경우 ( **중단 횟수**의 값을 확인할 수 있음) 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-147">If the role instance has recently stopped (you can check the value of **Abort count**), the deployment could be updating.</span></span> <span data-ttu-id="e3a03-148">역할 인스턴스가 다시 스스로 작동하는지 확인하기 위해 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-148">Wait to see if the role instance resumes functioning on its own.</span></span>
   * <span data-ttu-id="e3a03-149">역할 인스턴스가 **사용 중**인 경우 응용 프로그램 코드가 [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) 이벤트를 처리하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-149">If the role instance is **Busy**, check your application code to see if the [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span></span> <span data-ttu-id="e3a03-150">이 이벤트를 처리하는 일부 코드를 추가하거나 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-150">You might need to add or fix some code that handles this event.</span></span>
   * <span data-ttu-id="e3a03-151">[Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)블로그 게시물에서 진단 데이터 및 문제 해결 시나리오를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-151">Go through the diagnostic data and troubleshooting scenarios in the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="e3a03-152">클라우드 서비스를 재활용하면 배포에 대한 속성을 다시 설정하며 이렇게 하면 원래 문제에 대한 정보가 효과적으로 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-152">If you recycle your cloud service, you reset the properties for the deployment, effectively erasing the information for the original problem.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e3a03-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3a03-153">Next steps</span></span>
<span data-ttu-id="e3a03-154">클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e3a03-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="e3a03-155">Azure PaaS 컴퓨터 진단 데이터를 사용하여 클라우드 서비스 역할 문제를 해결하는 방법을 알아보려면 [Kevin Williamson의 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3a03-155">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
