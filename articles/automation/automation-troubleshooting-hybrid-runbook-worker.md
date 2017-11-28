---
title: "Azure 자동화 Hybrid Runbook Worker aaaTroubleshoot | Microsoft Docs"
description: "Hello 증상, 원인 및 hello Azure 자동화에서 Hybrid Runbook Worker 가장 일반적인 문제에 대 한 해결 방법에 설명 합니다."
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
ms.date: 07/25/2017
ms.author: magoedte
ms.openlocfilehash: 292af517c88d1ffd21262a286ccc079e7270bfad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a><span data-ttu-id="abc0c-103">Hybrid Runbook Worker에 대한 문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="abc0c-103">Troubleshooting tips for Hybrid Runbook Worker</span></span>

<span data-ttu-id="abc0c-104">이 문서에서는 자동화 하이브리드 Runbook 작업자를 경험할 수 및 가능한 해결 방법을 tooresolve 제안 오류 문제 해결 도움말을 제공 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-104">This article provides help troubleshooting errors you might experience with Automation Hybrid Runbook Workers and suggests possible solutions tooresolve them.</span></span>

## <a name="a-runbook-job-terminates-with-a-status-of-suspended"></a><span data-ttu-id="abc0c-105">Runbook 작업이 일시 중단됨 상태로 종료됨</span><span class="sxs-lookup"><span data-stu-id="abc0c-105">A runbook job terminates with a status of Suspended</span></span>

<span data-ttu-id="abc0c-106">Tooexecute 시도 직후 runbook이 일시 중단 세 번 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-106">Your runbook is suspended shortly after attempting tooexecute it three times.</span></span> <span data-ttu-id="abc0c-107">작업이 성공적으로 완료 hello runbook을 중단 시킬 수 있는 조건 있으며 hello 관련된 오류 메시지가 이유를 나타내는 추가 정보는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-107">There are conditions which may interrupt hello runbook from completing successfully and hello related error message does not include any additional information indicating why.</span></span> <span data-ttu-id="abc0c-108">이 문서는 문제 관련된 toohello Hybrid Runbook Worker runbook 실행 오류에 대 한 문제 해결 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-108">This article provides troubleshooting steps for issues related toohello Hybrid Runbook Worker runbook execution failures.</span></span>

<span data-ttu-id="abc0c-109">이 문서의 Azure 문제 해결 되지 않으면 방문 하 여 Azure 포럼에 hello [MSDN 스택 오버플로 hello 및](https://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-109">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="abc0c-110">이러한 포럼에 문제를 게시할 수 있습니다 또는 너무[ @AzureSupport Twitter에서](https://twitter.com/AzureSupport)합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-110">You can post your issue on these forums or too[@AzureSupport on Twitter](https://twitter.com/AzureSupport).</span></span> <span data-ttu-id="abc0c-111">또한 선택 하 여 Azure 지원 요청을 제출할 수 있습니다 **지원을 받는** hello에 [Azure 지원](https://azure.microsoft.com/support/options/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-111">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

### <a name="symptom"></a><span data-ttu-id="abc0c-112">증상</span><span class="sxs-lookup"><span data-stu-id="abc0c-112">Symptom</span></span>
<span data-ttu-id="abc0c-113">Runbook 실행이 실패 하 고 반환 된 hello 오류는 "hello 작업이 'Activate' 실행할 수 없습니다, hello 프로세스가 예기치 않게 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-113">Runbook execution fails and hello error returned is, "hello job action 'Activate' cannot be run, because hello process stopped unexpectedly.</span></span> <span data-ttu-id="abc0c-114">hello 작업 동작 "시도 했습니다. 3 회입니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-114">hello job action was attempted 3 times."</span></span>

<span data-ttu-id="abc0c-115">여러 hello 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-115">There are several possible causes for hello error:</span></span> 

1. <span data-ttu-id="abc0c-116">hello 하이브리드 작업자는 뒤에 프록시 또는 방화벽</span><span class="sxs-lookup"><span data-stu-id="abc0c-116">hello hybrid worker is behind a proxy or firewall</span></span>
2. <span data-ttu-id="abc0c-117">hello 컴퓨터 hello 하이브리드 작업자에서 실행 되 고 적습니다 hello 최소 보다 [하드웨어 요구 사항](automation-offering-get-started.md#hybrid-runbook-worker)</span><span class="sxs-lookup"><span data-stu-id="abc0c-117">hello computer hello hybrid worker is running on has less than hello minimum [hardware  requirements](automation-offering-get-started.md#hybrid-runbook-worker)</span></span>  
3. <span data-ttu-id="abc0c-118">hello runbook이 로컬 리소스를 인증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-118">hello runbooks cannot authenticate with local resources</span></span>

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a><span data-ttu-id="abc0c-119">원인 1: Hybrid Runbook Worker가 프록시 또는 방화벽 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-119">Cause 1: Hybrid Runbook Worker is behind proxy or firewall</span></span>
<span data-ttu-id="abc0c-120">하이브리드 Runbook 작업자에서 실행 되 고 hello 컴퓨터 hello는 방화벽 또는 프록시 서버 뒤에 및 아웃 바운드 네트워크 액세스 허용 또는 올바르게 구성 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-120">hello computer hello Hybrid Runbook Worker is running on is behind a firewall or proxy server and outbound network access may not be permitted or configured correctly.</span></span>

#### <a name="solution"></a><span data-ttu-id="abc0c-121">해결 방법</span><span class="sxs-lookup"><span data-stu-id="abc0c-121">Solution</span></span>
<span data-ttu-id="abc0c-122">Hello 컴퓨터는 포트 443에서 아웃 바운드 액세스 too*.azure automation.net 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-122">Verify hello computer has outbound access too*.azure-automation.net on port 443.</span></span> 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a><span data-ttu-id="abc0c-123">원인 2: 컴퓨터가 최소 하드웨어 요구 사항을 충족하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-123">Cause 2: Computer has less than minimum hardware requirements</span></span>
<span data-ttu-id="abc0c-124">Hybrid Runbook Worker 충족 해야 하는 hello를 실행 하는 컴퓨터는 최소 하드웨어 요구 사항을 toohost 지정 하기 전에 hello이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-124">Computers running hello Hybrid Runbook Worker should meet hello minimum hardware requirements before designating it toohost this feature.</span></span> <span data-ttu-id="abc0c-125">그렇지 않은 경우 다른 백그라운드 프로세스 및 실행 하는 동안 runbook에서 발생 한 경합 hello 리소스 사용률을 따라 hello 컴퓨터 됩니다 될 과도 하 게 및 runbook 작업 지연 또는 시간 초과 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-125">Otherwise, depending on hello resource utilization of other background processes and contention caused by runbooks during execution, hello computer will become over utilized and cause runbook job delays or timeouts.</span></span> 

#### <a name="solution"></a><span data-ttu-id="abc0c-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="abc0c-126">Solution</span></span>
<span data-ttu-id="abc0c-127">먼저 hello 컴퓨터 toorun hello Hybrid Runbook Worker 기능 지정 hello 최소 하드웨어 요구 사항을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-127">First confirm hello computer designated toorun hello Hybrid Runbook Worker feature meets hello minimum hardware requirements.</span></span>  <span data-ttu-id="abc0c-128">그렇지 않으면 CPU 및 메모리 사용률 toodetermine 하이브리드 Runbook 작업자 프로세스의 성능을 hello와 Windows 간에 상관 관계를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-128">If it does, monitor CPU and memory utilization toodetermine any correlation between hello performance of Hybrid Runbook Worker processes and Windows.</span></span>  <span data-ttu-id="abc0c-129">메모리 또는 CPU 부담이 있는 경우이 hello 필요 tooupgrade을 나타내거나 추가 프로세서를 추가할 수 있습니다 또는 증가 메모리 tooaddress hello 리소스 병목 상태가 발생 하 고 hello 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-129">If there is memory or CPU pressure, this may indicate hello need tooupgrade or add additional processors, or increase memory tooaddress hello resource bottleneck and resolve hello error.</span></span> <span data-ttu-id="abc0c-130">또는 작업 부하 요구 증가 되기 나타낼 때의 크기를 조정 하 고 hello 최소 요구 사항을 지원할 수 있는 다른 컴퓨터 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-130">Alternatively, select a different compute resource that can support hello minimum requirements and scale when workload demands indicate an increase is necessary.</span></span>         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a><span data-ttu-id="abc0c-131">원인 3: 로컬 리소스를 사용하여 Runbook을 인증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-131">Cause 3: Runbooks cannot authenticate with local resources</span></span>

#### <a name="solution"></a><span data-ttu-id="abc0c-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="abc0c-132">Solution</span></span>
<span data-ttu-id="abc0c-133">Hello 확인 **Microsoft SMA** 설명과 함께 해당 이벤트에 대 한 이벤트 로그 *[4294967295] 코드로 프로세스가 종료 된 Win32*합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-133">Check hello **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span></span>  <span data-ttu-id="abc0c-134">hello이이 오류는 runbook에서 인증을 구성 또는 hello 실행 자격 증명에 대 한 hello Hybrid worker 그룹을 지정 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-134">hello cause of this error is you haven't configured authentication in your runbooks or specified hello Run As credentials for hello Hybrid worker group.</span></span>  <span data-ttu-id="abc0c-135">검토 하십시오 [Runbook 사용 권한](automation-hrw-run-runbooks.md#runbook-permissions) tooconfirm runbook에 대 한 인증을 올바르게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abc0c-135">Please review [Runbook permissions](automation-hrw-run-runbooks.md#runbook-permissions) tooconfirm you have correctly configured authentication for your runbooks.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="abc0c-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="abc0c-136">Next steps</span></span>

<span data-ttu-id="abc0c-137">Automation의 다른 문제 해결에 대해 도움이 필요한 경우 [일반적인 Azure Automation 문제 해결](automation-troubleshooting-automation-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abc0c-137">For help troubleshooting other issues in Automation, see [Troubleshooting common Azure Automation issues](automation-troubleshooting-automation-errors.md)</span></span> 