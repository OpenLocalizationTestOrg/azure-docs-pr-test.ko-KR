---
title: "Azure 자동화에 대 한 PowerShell 워크플로 aaaLearning | Microsoft Docs"
description: "이 문서는 PowerShell toounderstand hello PowerShell 및 PowerShell 워크플로 및 적용 가능한 tooAutomation runbook 개념 간의 구체적인 차이점에 잘 알고 저자에 대 한 간략 한 설명은로 제공 됩니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="56213-103">Automation runbook에 대한 주요 Windows PowerShell 워크플로 개념 학습</span><span class="sxs-lookup"><span data-stu-id="56213-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="56213-104">Azure 자동화의 Runbook은 Windows PowerShell 워크플로로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="56213-105">Windows PowerShell 워크플로 비슷한 tooa Windows PowerShell 스크립트 했으나 tooa 새 사용자를 혼동 될 수 있는 몇 가지 중요 한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="56213-106">이 문서는 PowerShell 워크플로 사용 하 여 runbook을 작성 하는 의도 한 toohelp 상태인 동안에 검사점 필요 하지 않으면 PowerShell을 사용 하 여 runbook을 작성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="56213-107">다음과 같이 차이가 구문 PowerShell 워크플로 runbook을 작성할 때 및 이러한 차이점 작업 toowrite 효과적인 워크플로 좀 더 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="56213-108">워크플로 장기 실행 작업을 수행 하거나 여러 장치 또는 관리 되는 노드 사이에서 여러 단계의 조정을 hello를 해야 하는 프로그래밍 방식의 연결 된 단계의 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="56213-109">hello의 표준 스크립트에서 워크플로의 점으로 hello 기능이 포함 toosimultaneously 여러 장치에 대해 작업을 수행 하 고 hello 기능 tooautomatically 오류를 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="56213-110">Windows PowerShell 워크플로는 Windows Workflow Foundation을 활용하는 Windows PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="56213-111">Hello 워크플로 Windows PowerShell 구문을 사용 하 여 작성 하 고 Windows PowerShell에서 실행 하는 동안 Windows Workflow Foundation에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="56213-112">이 문서의 hello 항목에 대 한 자세한 내용은 참조 하십시오. [Windows PowerShell 워크플로 시작](http://technet.microsoft.com/library/jj134242.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="56213-113">워크플로의 기본 구조</span><span class="sxs-lookup"><span data-stu-id="56213-113">Basic structure of a workflow</span></span>
<span data-ttu-id="56213-114">hello 첫 번째 단계 tooconverting PowerShell 스크립트 tooa PowerShell 워크플로 빠뜨렸거나 hello **워크플로** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="56213-115">워크플로 hello로 시작 **워크플로** 키워드 다음에 오는 중괄호 hello 스크립트의 hello 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="56213-116">hello 워크플로의 hello 이름은 hello **워크플로** hello 구문 다음에 표시 된 대로 키워드:</span><span class="sxs-lookup"><span data-stu-id="56213-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="56213-117">hello 워크플로의 hello 이름을 hello 자동화 runbook의 hello 이름이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="56213-118">Hello runbook을 가져오는 경우 hello filename hello 워크플로 이름과 일치 해야 하 고 끝나야 합니다. *.ps1*합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="56213-119">tooadd 매개 변수 toohello 워크플로 사용 하 여 hello **Param** tooa 스크립트와 마찬가지로 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="56213-120">코드 변경 내용</span><span class="sxs-lookup"><span data-stu-id="56213-120">Code changes</span></span>
<span data-ttu-id="56213-121">PowerShell 워크플로 코드에서는 몇 가지 중요 한 변경 제외 하 고 거의 동일한 tooPowerShell 스크립트 코드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="56213-122">hello 다음 섹션에서는 할 toomake tooa PowerShell 스크립트에 대 한 워크플로에서 toorun 변경에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="56213-123">활동</span><span class="sxs-lookup"><span data-stu-id="56213-123">Activities</span></span>
<span data-ttu-id="56213-124">활동은 워크플로의 특정 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="56213-125">하나 이상의 명령으로 구성된 스크립트와 마찬가지로 워크플로는 시퀀스로 수행되는 하나 이상의 활동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="56213-126">Windows PowerShell 워크플로 자동으로 다양 한 Windows PowerShell cmdlet tooactivities hello 때 변환는 워크플로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="56213-127">Runbook에서 이러한 cmdlet 중 하나를 지정 하면 Windows Workflow foundation hello 해당 작업이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="56213-128">해당 하는 활동 없이 이러한 cmdlet에 대 한 Windows PowerShell 워크플로 자동으로 실행 내에서 hello cmdlet는 [InlineScript](#inlinescript) 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="56213-129">InlineScript 블록에 명시적으로 포함하지 않으면 워크플로에서 제외되고 사용할 수 없는 cmdlet 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="56213-130">이러한 개념에 자세한 내용은 [스크립트 워크플로에서 활동 사용](http://technet.microsoft.com/library/jj574194.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56213-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="56213-131">워크플로 활동 일반 매개 변수 tooconfigure 집합이 자신의 작업을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="56213-132">Hello 워크플로 일반 매개 변수에 대 한 세부 정보를 참조 하십시오. [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="56213-133">위치 매개 변수</span><span class="sxs-lookup"><span data-stu-id="56213-133">Positional parameters</span></span>
<span data-ttu-id="56213-134">워크플로에서 위치매개 변수는 활동 및 cmdlets와 같이 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="56213-135">사용자가 매개 변수 이름을 사용해야 한다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="56213-136">예를 들어, 코드를 실행 중인 모든 서비스를 가져오는 다음 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="56213-137">"지정 된 hello를 사용 하 여 집합을 확인할 수 없는 매개 변수 명명 된 매개 변수입니다."와 같은 메시지가 나타나면이 동일한 코드 워크플로에서 toorun 하면</span><span class="sxs-lookup"><span data-stu-id="56213-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="56213-138">toocorrect이 hello 다음과 같이 hello 매개 변수 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="56213-139">역직렬화된 개체</span><span class="sxs-lookup"><span data-stu-id="56213-139">Deserialized objects</span></span>
<span data-ttu-id="56213-140">개체는 워크플로에서 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="56213-141">즉, 이 말은 해당 속성은 사용할수 있지만 메서드는 사용할 수 없다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="56213-142">예를 들어 hello를 hello 서비스 개체의 hello Stop 메서드를 사용 하 여 서비스를 중지 하는 PowerShell 코드를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="56213-143">이 작업을 수행할 toorun 워크플로에서 "메서드 호출에서 Windows PowerShell 워크플로 지원 되지 않습니다." 라는 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="56213-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="56213-144">한 가지 옵션은 toowrap이 두 줄의 코드는 [InlineScript](#inlinescript) 어떤 $Service 되는 경우가 hello 블록 내에서 서비스 개체의 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="56213-145">두 번째 방법은 toouse 사용 가능한 경우 hello 메서드와 같은 기능을 수행 하는 또 다른 cmdlet에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="56213-146">이 샘플에서는 hello Stop-service cmdlet 제공 hello hello 중지 메서드를와 동일한 기능을 워크플로에 대 한 hello 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="56213-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="56213-147">InlineScript</span></span>
<span data-ttu-id="56213-148">hello **InlineScript** 활동은 PowerShell 워크플로 대신 기존 PowerShell 스크립트로 toorun 명령을 하나 이상 필요한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="56213-149">워크플로의 명령을 처리를 위해 tooWindows Workflow Foundation 보내는 동안 InlineScript 블록의 명령은 Windows PowerShell에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="56213-150">InlineScript는 아래 표시 된 구문 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="56213-151">InlineScript에서 hello 출력 tooa 변수를 할당 하 여 출력을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="56213-152">hello 다음 예제에서는 서비스를 중지 하 고 출력 hello 서비스 이름.</span><span class="sxs-lookup"><span data-stu-id="56213-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="56213-153">값을 InlineScript 블록으로 전달할 수 있지만, **$Using** 범위 한정자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="56213-154">hello 다음 예제는 이전 예제와 동일한 toohello hello 서비스 이름이 제공 된 변수에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="56213-155">InlineScript 활동 특정 워크플로가에 중요 한 수 있지만, 워크플로 구성체를 지원 하지 않습니다 하며 이유 뒤 hello에 대 한 필요한 경우에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="56213-156">InlineScript 블록 내에서는 [검사점](#checkpoints)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="56213-157">Hello 블록 내에서 실패 한 경우 hello 블록의 hello 시작 부분에서 재개 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="56213-158">InlineScriptBlock 내부에서는 [병렬 실행](#parallel-processing)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="56213-159">InlineScript은 hello hello InlineScript 블록의 전체 길이 대 한 hello Windows PowerShell 세션을 유지 하므로 hello 워크플로의 확장성을 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56213-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="56213-160">InlineScript 사용에 대한 자세한 내용은 [워크플로에서 Windows PowerShell 명령 실행](http://technet.microsoft.com/library/jj574197.aspx) 및 [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56213-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="56213-161">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="56213-161">Parallel processing</span></span>
<span data-ttu-id="56213-162">Windows PowerShell 워크플로의 장점 중 하나는 hello 기능 tooperform 대신 병렬로 명령 집합을 순차적으로 일반적인 스크립트와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="56213-163">Hello를 사용할 수 있습니다 **병렬** 키워드 toocreate 여러 명령 동시에 실행 되는 스크립트 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="56213-164">이 구문 아래에 표시 된 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="56213-165">Y 1과 Activity2 hello에서 시작 하는 경우에 한 번입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="56213-166">Activity3는 Activity1과 Activity2가 모두 완료된 후에만 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="56213-167">예를 들어 hello를 다음 PowerShell 명령을 여러 파일 tooa 네트워크 대상에 복사 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="56213-168">이 명령은 순차적으로 실행 되므로 파일 하나만 다음 hello를 시작 하기 전에 복사 완료 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="56213-169">hello 다음 워크플로 실행를 모두 복사를 시작할 hello 동일 동시에 명령을 동일 이러한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="56213-170">모든 후에 복사 hello 완료 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-170">Only after they are all copied is hello completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="56213-171">Hello를 사용할 수 있습니다 **ForEach-Parallel** 동시에 컬렉션의 각 항목에 대 한 tooprocess 명령을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="56213-172">hello 컬렉션의 항목 hello hello 스크립트 블록의 hello 명령은 순차적으로 실행 하는 반면 병렬로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="56213-173">이 구문 아래에 표시 된 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="56213-174">이 경우 Activity1부터 hello에 대해 동일한 시간 hello 컬렉션의 모든 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="56213-175">각 항목에 대해 Activity2는 Activity1이 완료된 후에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="56213-176">Activity3는 모든 항목에 대해 Activity1과 Activity2가 모두 완료된 후에만 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="56213-177">다음 예제는 hello는 동시에 파일을 복사 하는 유사한 toohello 이전 예입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="56213-178">이 경우 복사한 후 각 파일에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="56213-179">모든 후에 완전히 복사 hello 최종 완료 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="56213-180">Toogive 신뢰할 수 없는 결과 표시 된이 이후 동시에 자식 runbook을 실행 하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="56213-181">hello 때로는 hello 자식 runbook의 출력 표시 되지 않으면, 한 자식 runbook의 설정에 영향을 줄 수 및 기타 병렬 자식 runbook hello</span><span class="sxs-lookup"><span data-stu-id="56213-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="56213-182">검사점</span><span class="sxs-lookup"><span data-stu-id="56213-182">Checkpoints</span></span>
<span data-ttu-id="56213-183">A *검사점* hello hello 변수에 대 한 현재 값을 포함 하는 hello 워크플로의 현재 상태 스냅숏을 이며 생성 된 toothat 지점 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="56213-184">워크플로 오류에서 종료 되거나 일시 중단, 한 다음 hello 다음 그가 실행 될 때 시작 됩니다 hello 워크플로의 hello 시작 하는 대신, 마지막 검사점.</span><span class="sxs-lookup"><span data-stu-id="56213-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="56213-185">Hello 사용 하 여 워크플로에서 검사점을 설정할 수 있습니다 **Checkpoint-workflow** 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="56213-186">다음 샘플 코드는 hello, 워크플로 tooend hello Activity2 발생 후 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="56213-187">Hello 워크플로 다시 실행 하는 경우 마지막 검사점 hello 설정 후에 바로이 된 이후 Activity2를 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="56213-188">Hello 워크플로 다시 시작한 경우 발생 하기 쉬운 tooexception 수 있으며 되지 않아야 하는 활동 반복 후 워크플로에서 검사점을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="56213-189">예를 들어 Runbook에서 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="56213-190">이전과 이후에 hello 명령 toocreate hello 가상 컴퓨터 검사점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="56213-191">Hello 만들기에 실패 하면 다음 hello 명령은 반복 될 hello 워크플로 다시 시작 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="56213-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="56213-192">Hello 워크플로 hello 만들기가 성공 후 오류가 발생 하면 다음 hello 가상 컴퓨터가 만들어지지 않습니다 다시 hello 워크플로 다시 시작할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="56213-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="56213-193">다음 예제는 hello 여러 파일 tooa 네트워크 위치에 복사 하 고 각 파일 다음 검사점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="56213-194">Hello 네트워크 위치를 잃어버린 경우 hello 워크플로 오류에서 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="56213-195">다시 시작 되 면 이미 복사 된 hello 파일만 건너뜁니다 의미 hello 마지막 검사점에서 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56213-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="56213-196">Username 자격 증명은 hello를 호출한 후 지속 되지 않으므로 [Suspend-workflow](https://technet.microsoft.com/library/jj733586.aspx) 활동 hello 마지막 검사점 이후에 tooset hello 자격 증명 toonull 필요 하 고이 다음 검색 하 다시 hello 자산 저장소에서 후또는 **Suspend-workflow** 또는 검사점을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="56213-197">그렇지 않으면 hello 다음과 같은 오류 메시지가 나타날 수 있습니다: *hello 워크플로 작업을 다시 시작할 수 없습니다, 하거나 지 속성 데이터를 완전히 저장 하거나 저장할 수 없습니다 때문에 지 속성 데이터 손상 되었습니다. Hello 워크플로 다시 시작 해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="56213-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="56213-198">동일한 코드 다음 hello 보여 줍니다. 방법을 toohandle PowerShell 워크플로 runbook의이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="56213-199">서비스 주체로 구성된 실행 계정을 사용하여 인증하는 경우에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56213-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="56213-200">검사점에 대 한 자세한 내용은 참조 [스크립트 워크플로에 검사점 추가 tooa](http://technet.microsoft.com/library/jj574114.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56213-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="56213-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56213-201">Next steps</span></span>
* <span data-ttu-id="56213-202">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="56213-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
