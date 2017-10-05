---
title: "Azure Automation에 대한 PowerShell 워크플로 학습 | Microsoft Docs"
description: "이 문서는 PowerShell에 익숙한 작성자가 PowerShell과 PowerShell 워크플로 간의 중대한 차이와 Automation Runbook에 적용되는 개념을 빠르게 이해하도록 하기 위해 제공됩니다."
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
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="918ee-103">Automation runbook에 대한 주요 Windows PowerShell 워크플로 개념 학습</span><span class="sxs-lookup"><span data-stu-id="918ee-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="918ee-104">Azure 자동화의 Runbook은 Windows PowerShell 워크플로로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="918ee-105">Windows PowerShell 워크플로는 Windows PowerShell 스크립트와 비슷해 보이지만 신규 사용자가 혼동할 수 있는 중요한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="918ee-106">이 문서는 PowerShell 워크플로를 사용하여 runbook을 작성하는 데 도움을 주기 위해 작성되었으나 검사점이 필요한 경우가 아니면 PowerShell을 사용하여 runbook을 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="918ee-107">PowerShell 워크플로 runbook을 작성할 경우 몇 가지 구문 차이가 있으며 이러한 차이점으로 인해 효과적인 워크플로를 작성하기 위해 좀 더 많은 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="918ee-108">워크플로는 장기 실행 작업을 수행하거나 여러 장치 또는 관리 노드에서 여러 단계를 조정해야 하는 프로그래밍 방식으로 연결된 일련의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="918ee-109">워크플로는 일반적인 스크립트에 비해 여러 장치에서 작업을 동시에 수행하고 오류로부터 자동으로 복구할 수 있다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="918ee-110">Windows PowerShell 워크플로는 Windows Workflow Foundation을 활용하는 Windows PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="918ee-111">워크플로는 Windows PowerShell 구문으로 작성되고 Windows PowerShell에서 시작되지만 Windows Workflow Foundation에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="918ee-112">이 기사의 항목에 대한 자세한 내용은 [Windows PowerShell 워크플로 시작](http://technet.microsoft.com/library/jj134242.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="918ee-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="918ee-113">워크플로의 기본 구조</span><span class="sxs-lookup"><span data-stu-id="918ee-113">Basic structure of a workflow</span></span>
<span data-ttu-id="918ee-114">PowerShell 스크립트를 PowerShell 워크플로로 변환하는 첫 단계는 **워크플로** 키워드로 둘러싸는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="918ee-115">워크플로는 **Workflow** 키워드와 그 뒤에 중괄호로 묶인 스크립트의 본문으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="918ee-116">워크플로 이름은 다음 구문과 같이 **Workflow** 키워드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="918ee-117">워크플로 이름은 자동화 Runbook의 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="918ee-118">Runbook을 가져오려면 파일 이름이 워크플로 이름과 일치하고 *.ps1*으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="918ee-119">워크플로에 매개 변수를 추가 하려면, 스크립트와 마찬가지로 **Param** 이 키워드 입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="918ee-120">코드 변경 내용</span><span class="sxs-lookup"><span data-stu-id="918ee-120">Code changes</span></span>
<span data-ttu-id="918ee-121">PowerShell 워크플로 코드는 몇 가지 중요한 변경 내용을 제외하고는 PowerShell 스크립트 코드와 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="918ee-122">다음 섹션에서 설명하는 변경 사항을 사용자가 워크플로에서 실행하려면 PowerShell 스크립트를 만들 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="918ee-123">활동</span><span class="sxs-lookup"><span data-stu-id="918ee-123">Activities</span></span>
<span data-ttu-id="918ee-124">활동은 워크플로의 특정 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="918ee-125">하나 이상의 명령으로 구성된 스크립트와 마찬가지로 워크플로는 시퀀스로 수행되는 하나 이상의 활동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="918ee-126">Windows PowerShell 워크플로는 워크플로를 실행할 때 많은 Windows PowerShell cmdlet을 활동으로 자동으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="918ee-127">Runbook에서 이러한 cmdlet 중 하나를 지정한 경우 해당 활동은 Windows Workflow Foundation에 의해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="918ee-128">해당 활동이 없는 cmdlet의 경우 Windows PowerShell 워크플로는 [InlineScript](#inlinescript) 활동 내에서 cmdlet을 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="918ee-129">InlineScript 블록에 명시적으로 포함하지 않으면 워크플로에서 제외되고 사용할 수 없는 cmdlet 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="918ee-130">이러한 개념에 자세한 내용은 [스크립트 워크플로에서 활동 사용](http://technet.microsoft.com/library/jj574194.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="918ee-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="918ee-131">워크플로 활동은 해당 작업을 구성하기 위해 일반 매개 변수 집합을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="918ee-132">워크플로 일반 매개 변수에 대한 자세한 내용은 [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="918ee-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="918ee-133">위치 매개 변수</span><span class="sxs-lookup"><span data-stu-id="918ee-133">Positional parameters</span></span>
<span data-ttu-id="918ee-134">워크플로에서 위치매개 변수는 활동 및 cmdlets와 같이 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="918ee-135">사용자가 매개 변수 이름을 사용해야 한다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="918ee-136">예를 들어, 다음 모든 실행 중인 서비스의 코드를 가져오는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="918ee-137">동일한 코드를 워크플로에서 실행하려고 한다면, 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="918ee-138">“지정한 명명된 매개 변수를 사용하여 매개 변수 집합을 확인할 수 없습니다.” 이 문제를 해결하려면 다음과 같은 매개 변수 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="918ee-139">역직렬화된 개체</span><span class="sxs-lookup"><span data-stu-id="918ee-139">Deserialized objects</span></span>
<span data-ttu-id="918ee-140">개체는 워크플로에서 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="918ee-141">즉, 이 말은 해당 속성은 사용할수 있지만 메서드는 사용할 수 없다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="918ee-142">서비스 개체의 stop 메서드를 사용하여 서비스를 중지시키는 다음의 Powershell 코드를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="918ee-143">워크플로에서 실행하는 경우, 다음과 같은 오류 메시지가 표시됩니다. “Windows PowerShell 워크플로에서는 메서드 호출이 지원되지 않습니다.”</span><span class="sxs-lookup"><span data-stu-id="918ee-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="918ee-144">한가지 옵션은 블록 내에서 case $Service가 서비스되는 [InlineScript](#inlinescript) 블록의 코드 두줄을 래핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="918ee-145">다른 옵션은 하나의 cmdlet가 사용 가능할 경우, 메서드와 동일한 기능을 수행하는 다른 cmdlet를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="918ee-146">이 샘플에서 Stop-Service cmdlet은 Stop 메서드와 같은 기능을 제공하며 워크플로에 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="918ee-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="918ee-147">InlineScript</span></span>
<span data-ttu-id="918ee-148">**InlineScript** 활동은 PowerShell 워크플로 대신 전통적인 PowerShell 스크립트처럼 하나 혹은 그 이상의 명령을 실행해야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="918ee-149">워크플로의 명령은 처리를 위해 Windows Workflow Foundation으로 전송되지만 InlineScript 블록의 명령은 Windows PowerShell에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="918ee-150">InlineScript에는 아래 표시된 구문이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="918ee-151">출력을 변수에 할당하여 InlineScript에서 출력을 반환 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="918ee-152">다음 예제에서는 서비스를 중지하고 서비스 이름을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="918ee-153">값을 InlineScript 블록으로 전달할 수 있지만, **$Using** 범위 한정자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="918ee-154">다음 예제는 변수에서 제공된 서비스 이름을 제외하고는 이전의 예제와 똑같습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

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


<span data-ttu-id="918ee-155">InlineScript 활동은 특정 워크플로에서 중요할 수 있지만 워크플로 구문을 지원하지 않으며 다음과 같은 이유로 필요한 경우에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="918ee-156">InlineScript 블록 내에서는 [검사점](#checkpoints)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="918ee-157">블록 내에서 오류가 발생한 경우 블록의 처음부터 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="918ee-158">InlineScriptBlock 내부에서는 [병렬 실행](#parallel-processing)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="918ee-159">InlineScript는 InlineScript 블록의 전체 길이 동안 Windows PowerShell 세션을 유지하므로 워크플로의 확장성에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="918ee-160">InlineScript 사용에 대한 자세한 내용은 [워크플로에서 Windows PowerShell 명령 실행](http://technet.microsoft.com/library/jj574197.aspx) 및 [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="918ee-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="918ee-161">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="918ee-161">Parallel processing</span></span>
<span data-ttu-id="918ee-162">Windows PowerShell 워크플로의 한 가지 장점은 일반적인 스크립트처럼 명령 집합을 순차적으로 수행하지 않고 병렬로 수행할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="918ee-163">**Parallel** 키워드를 사용하여 동시에 실행할 여러 명령이 포함된 스크립트 블록을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="918ee-164">여기서는 아래 표시된 구문이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="918ee-165">이 경우에는 Activity1과 Activity2가 동시에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="918ee-166">Activity3는 Activity1과 Activity2가 모두 완료된 후에만 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="918ee-167">네트워크 대상에 여러 파일을 복사하는 다음 PowerShell 명령을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="918ee-168">하나의 파일이 복사가 완전히 끝나야만 다음 복사가 시작되므로 이 명령은 순차적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="918ee-169">다음 워크플로는 복사를 동시에 시작하기 때문에 동일한 명령을 병렬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="918ee-170">복사가 완전히 끝난 후에만 완료 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-170">Only after they are all copied is the completion message displayed.</span></span>

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


<span data-ttu-id="918ee-171">**ForEach -Parallel** 구문을 사용하여 컬렉션의 각 항목에 대한 명령을 동시에 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="918ee-172">이 경우 컬렉션의 항목은 병렬로 처리되지만 스크립트 블록의 명령은 순차적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="918ee-173">여기서는 아래 표시된 구문이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="918ee-174">이 예제에서 Activity1은 컬렉션의 모든 항목에 대해 동시에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="918ee-175">각 항목에 대해 Activity2는 Activity1이 완료된 후에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="918ee-176">Activity3는 모든 항목에 대해 Activity1과 Activity2가 모두 완료된 후에만 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="918ee-177">다음 예제에서는 동시에 파일을 복사하는 이전 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="918ee-178">이 경우 복사한 후 각 파일에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="918ee-179">복사가 완전히 끝난 후 최종 완료 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-179">Only after they are all completely copied is the final completion message displayed.</span></span>

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
> <span data-ttu-id="918ee-180">자식 runbook을 병렬로 실행하는 것은 추천하지 않는 이유는 결과물이 신뢰할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="918ee-181">자식 runbook에서의 출력은 때때로 나타나지 않을 수도 있고, 한 자식 runbook의 설정이 다른 병렬 자식 runbook에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="918ee-182">검사점</span><span class="sxs-lookup"><span data-stu-id="918ee-182">Checkpoints</span></span>
<span data-ttu-id="918ee-183">*검사점* 은 워크플로의 현재 상태에 대한 스냅숏으로, 변수의 현재 값 및 해당 지점에 생성된 모든 출력을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="918ee-184">워크플로가 오류 때문에 종료되었거나 일시 중단한 다음 실행하면 워크플로 처음부터 시작하는 게 아니라 해당 마지막 검사점에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="918ee-185">**Checkpoint-Workflow** 활동을 사용하여 워크플로에서 검사점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="918ee-186">다음 샘플 코드에서는 Activity2 이후에 예외가 발생하여 워크플로가 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="918ee-187">설정된 마지막 검사점 직후이므로 워크플로를 다시 시작하면 Activity2를 실행하는 것으로 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="918ee-188">예외가 발생할 수 있으며 워크플로를 다시 시작한 경우 반복되지 않아야 하는 활동 뒤에 R워크플로의 검사점을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="918ee-189">예를 들어 Runbook에서 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="918ee-190">가상 컴퓨터를 만드는 명령 앞뒤 모두에 검사점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="918ee-191">만들기에 실패하면, 워크플로가 다시 시작하는 경우 명령을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="918ee-192">생성 후 워크플로가 실패하는 경우, 워크플로를 재시작할 때에도 가상 컴퓨터는 다시 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="918ee-193">다음 예제는 네트워크 위치에 여러 파일들을 복사하고 각 파일에 검사점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="918ee-194">네트워크 위치가 손실된 경우 워크플로가 오류로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="918ee-195">다시 시작될 경우 마지막 검사점에서 재시작되는 데 이것은 이미 복사된 파일만 생략된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="918ee-196">[Suspend-workflow](https://technet.microsoft.com/library/jj733586.aspx) 작업을 호출한 후 또는 마지막 검사점 이후에 사용자 이름 자격 증명을 유지하지 않기 때문에 자격 증명을 null로 설정하고 **Suspend-workflow** 또는 검사점을 호출한 후에 자산 저장소에서 다시 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="918ee-197">그렇지 않으면 다음과 같은 오류 메시지가 나타날 수 있습니다. *지속성 데이터를 완전히 저장할 수 없거나 저장된 지속성 데이터가 손상되었기 때문에 워크플로 작업을 다시 시작할 수 없습니다. 워크플로를 다시 시작해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="918ee-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="918ee-198">다음과 같은 코드에서는 PowerShell 워크플로 runbook에서 이를 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="918ee-199">서비스 주체로 구성된 실행 계정을 사용하여 인증하는 경우에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="918ee-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="918ee-200">검사점에 대한 자세한 내용은 [스크립트 워크플로에 검사점 추가](http://technet.microsoft.com/library/jj574114.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="918ee-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="918ee-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="918ee-201">Next steps</span></span>
* <span data-ttu-id="918ee-202">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="918ee-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
