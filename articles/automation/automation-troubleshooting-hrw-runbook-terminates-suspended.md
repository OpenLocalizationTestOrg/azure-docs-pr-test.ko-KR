---
title: "Hybrid Runbook Worker: Runbook 작업이 일시 중단됨 상태로 종료됨 | Microsoft Docs"
description: "Hybrid Runbook Worker 작업 종류 오류에 대한 증상, 원인 및 해결 방법."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 7c6365b729d73f1c5b9bc57952b1723255d9e9f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a><span data-ttu-id="38e78-103">Hybrid Runbook Worker: Runbook 작업이 일시 중단됨 상태로 종료됨</span><span class="sxs-lookup"><span data-stu-id="38e78-103">Hybrid Runbook Worker: A runbook job terminates with a status of Suspended</span></span>
## <a name="summary"></a><span data-ttu-id="38e78-104">요약</span><span class="sxs-lookup"><span data-stu-id="38e78-104">Summary</span></span>
<span data-ttu-id="38e78-105">Runbook이 3회 실행 시도 직후 일시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-105">Your runbook is suspended shortly after attempting to execute it three times.</span></span> <span data-ttu-id="38e78-106">Runbook이 성공적으로 완료되는 것을 막는 조건이 있으며 관련된 오류 메시지에 이유를 알리는 정보가 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-106">There are conditions which may interrupt the runbook from completing successfully and the related error message does not include any additional information indicating why.</span></span> <span data-ttu-id="38e78-107">이 문서는 Hybrid Runbook Worker Runbook 실행 실패와 관련된 문제를 해결하는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-107">This article provides troubleshooting steps for issues related to the Hybrid Runbook Worker runbook execution failures.</span></span>

<span data-ttu-id="38e78-108">Azure 문제와 관련된 정보가 이 문서에 없을 경우 [MSDN 및 Stack Overflow](https://azure.microsoft.com/support/forums/)에서 Azure 포럼을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="38e78-108">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="38e78-109">이러한 포럼이나 [@AzureSupportTwitter의](https://twitter.com/AzureSupport) 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-109">You can post your issue on these forums or to [@AzureSupport on Twitter](https://twitter.com/AzureSupport).</span></span> <span data-ttu-id="38e78-110">또한 **Azure 지원** 사이트에서 [지원 받기](https://azure.microsoft.com/support/options/) 를 선택하여 Azure 지원 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-110">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptom"></a><span data-ttu-id="38e78-111">증상</span><span class="sxs-lookup"><span data-stu-id="38e78-111">Symptom</span></span>
<span data-ttu-id="38e78-112">Runbook 실행에 실패하고 “프로세스가 예기치 않게 중지되어서 '활성화' 작업을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-112">Runbook execution fails and the error returned is, "The job action 'Activate' cannot be run, because the process stopped unexpectedly.</span></span> <span data-ttu-id="38e78-113">작업을 3번 시도했습니다.”라는 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-113">The job action was attempted 3 times."</span></span>

## <a name="cause"></a><span data-ttu-id="38e78-114">원인</span><span class="sxs-lookup"><span data-stu-id="38e78-114">Cause</span></span>
<span data-ttu-id="38e78-115">오류의 잠재적 원인에는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-115">There are several possible causes for the error:</span></span> 

1. <span data-ttu-id="38e78-116">Hybrid Worker가 프록시 또는 방화벽 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-116">The hybrid worker is behind a proxy or firewall</span></span>
2. <span data-ttu-id="38e78-117">Hybrid Worker가 실행되는 컴퓨터가 최소 하드웨어 [요구 사항](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements)</span><span class="sxs-lookup"><span data-stu-id="38e78-117">The computer the hybrid worker is running on has less than the minimum hardware [requirements](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements)</span></span> 
3. <span data-ttu-id="38e78-118">로컬 리소스를 사용하여 Runbook을 인증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-118">The runbooks cannot authenticate with local resources</span></span>

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a><span data-ttu-id="38e78-119">원인 1: Hybrid Runbook Worker가 프록시 또는 방화벽 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-119">Cause 1: Hybrid Runbook Worker is behind proxy or firewall</span></span>
<span data-ttu-id="38e78-120">Hybrid Runbook Worker가 실행되는 컴퓨터가 프록시 또는 방화벽 뒤에 있고, 아웃바운드 네트워크 액세스가 허용되지 않았거나 제대로 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-120">The computer the Hybrid Runbook Worker is running on is behind a firewall or proxy server and outbound network access may not be permitted or configured correctly.</span></span>

### <a name="solution"></a><span data-ttu-id="38e78-121">해결 방법</span><span class="sxs-lookup"><span data-stu-id="38e78-121">Solution</span></span>
<span data-ttu-id="38e78-122">컴퓨터가 포트 443, 9354, 및 30000-30199의 *.cloudapp.net에 대한 아웃바운드 액세스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-122">Verify the computer has outbound access to *.cloudapp.net on ports 443, 9354, and 30000-30199.</span></span> 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a><span data-ttu-id="38e78-123">원인 2: 컴퓨터가 최소 하드웨어 요구 사항을 충족하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-123">Cause 2: Computer has less than minimum hardware requirements</span></span>
<span data-ttu-id="38e78-124">Hybrid Runbook Worker가 실행되는 컴퓨터는 이 기능을 호스트하도록 지정하기 전에, 최소 하드웨어 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-124">Computers running the Hybrid Runbook Worker should meet the minimum hardware requirements before designating it to host this feature.</span></span> <span data-ttu-id="38e78-125">그렇지 않으면, 실행 중 Runbook에 의해 유발되는 다른 백그라운드 프로세스 및 경합의 리소스 사용률에 따라, 컴퓨터가 과도하게 사용되거나 Runbook 작업이 지연되거나 시간이 초과되는 원인이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-125">Otherwise, depending on the resource utilization of other background processes and contention caused by runbooks during execution, the computer will become over utilized and cause runbook job delays or timeouts.</span></span> 

### <a name="solution"></a><span data-ttu-id="38e78-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="38e78-126">Solution</span></span>
<span data-ttu-id="38e78-127">먼저, Hybrid Runbook Worker 기능을 실행하도록 지정된 컴퓨터가 최소 하드웨어 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-127">First confirm the computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span></span>  <span data-ttu-id="38e78-128">그렇다면, CPU 및 메모리 사용률을 모니터링하여 Hybrid Runbook Worker 프로세스와 Windows 사이에 어떠한 상관 관계가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-128">If it does, monitor CPU and memory utilization to determine any correlation between the performance of Hybrid Runbook Worker processes and Windows.</span></span>  <span data-ttu-id="38e78-129">메모리 또는 CPU가 과도하게 사용된다면, 리소스 디스크 병목 현상에 대처하고 오류를 해결하기 위해 메모리를 증가시키거나 프로세서를 업그레이드 또는 추가해야 한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-129">If there is memory or CPU pressure, this may indicate the need to upgrade or add additional processors, or increase memory to address the resource bottleneck and resolve the error.</span></span> <span data-ttu-id="38e78-130">아니면, 최소 요구 사항을 지원할 수 있는 다른 계산 리소스를 선택하고 필요한 워크로드에 증가가 필요하다는 것이 나타나면 규모를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-130">Alternatively, select a different compute resource that can support the minimum requirements and scale when workload demands indicate an increase is necessary.</span></span>         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a><span data-ttu-id="38e78-131">원인 3: 로컬 리소스를 사용하여 Runbook을 인증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-131">Cause 3: Runbooks cannot authenticate with local resources</span></span>
### <a name="solution"></a><span data-ttu-id="38e78-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="38e78-132">Solution</span></span>
<span data-ttu-id="38e78-133">**Microsoft-SMA** 이벤트 로그에 *Win32 프로세스가[4294967295] 코드와 함께 종료되었습니다.*라고 설명하는 이벤트가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-133">Check the **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span></span>  <span data-ttu-id="38e78-134">이 오류의 원인은 Runbook에 인증을 구성하지 않았거나 Hybrid Worker 그룹에 대해 실행 자격 증명을 지정하지 않았기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-134">The cause of this error is you haven't configured authentication in your runbooks or specified the Run As credentials for the Hybrid worker group.</span></span>  <span data-ttu-id="38e78-135">[Runbook 권한](automation-hybrid-runbook-worker.md#runbook-permissions) 을 검토하여 Runbook에 대한 인증을 올바르게 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e78-135">Please review [Runbook permissions](automation-hybrid-runbook-worker.md#runbook-permissions) to confirm you have correctly configured authentication for your runbooks.</span></span>  

