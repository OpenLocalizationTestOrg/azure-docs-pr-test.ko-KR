---
title: "자동화 Runbook 형식 aaaAzure | Microsoft Docs"
description: "Azure 자동화 및 어떤 유형 toouse 결정할 때 고려해 야 하면 고려 사항에서 사용할 수 있는 runbook의 hello 다른 형식에 설명 합니다. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a><span data-ttu-id="ec937-103">Azure 자동화 Runbook 형식</span><span class="sxs-lookup"><span data-stu-id="ec937-103">Azure Automation runbook types</span></span>
<span data-ttu-id="ec937-104">Azure 자동화는 다음 표에 hello의 네 가지 유형의 간략하게 설명 하는 runbook 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-104">Azure Automation supports four types of runbooks that are  briefly described in hello following table.</span></span>  <span data-ttu-id="ec937-105">hello 아래 섹션에서는 추가 정보를 제공 될 때 고려 사항 포함 하 여 각 형식에 대 한 각 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-105">hello sections below provide further information about each type including considerations on when toouse each.</span></span>

| <span data-ttu-id="ec937-106">형식</span><span class="sxs-lookup"><span data-stu-id="ec937-106">Type</span></span> | <span data-ttu-id="ec937-107">설명</span><span class="sxs-lookup"><span data-stu-id="ec937-107">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="ec937-108">그래픽</span><span class="sxs-lookup"><span data-stu-id="ec937-108">Graphical</span></span>](#graphical-runbooks) |<span data-ttu-id="ec937-109">Windows PowerShell을 기반으로 하며 Azure 포털의 그래픽 편집기로 완전하게 생성 및 편집됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-109">Based on Windows PowerShell and created and edited completely in graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="ec937-110">그래픽 PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="ec937-110">Graphical PowerShell Workflow</span></span>](#graphical-runbooks) |<span data-ttu-id="ec937-111">Azure 포털에서 생성 되 고 완전 하 게 편집한 hello 그래픽 편집기 및 Windows PowerShell 워크플로 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-111">Based on Windows PowerShell Workflow and created and edited completely in hello graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="ec937-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec937-112">PowerShell</span></span>](#powershell-runbooks) |<span data-ttu-id="ec937-113">Windows PowerShell 스크립트를 기반으로 하는 텍스트 Runbook</span><span class="sxs-lookup"><span data-stu-id="ec937-113">Text runbook based on Windows PowerShell script.</span></span> |
| [<span data-ttu-id="ec937-114">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="ec937-114">PowerShell Workflow</span></span>](#powershell-workflow-runbooks) |<span data-ttu-id="ec937-115">Windows PowerShell 워크플로를 기반으로 하는 텍스트 Runbook</span><span class="sxs-lookup"><span data-stu-id="ec937-115">Text runbook based on Windows PowerShell Workflow.</span></span> |

## <a name="graphical-runbooks"></a><span data-ttu-id="ec937-116">그래픽 Runbook</span><span class="sxs-lookup"><span data-stu-id="ec937-116">Graphical runbooks</span></span>
<span data-ttu-id="ec937-117">[그래픽](automation-runbook-types.md#graphical-runbooks) 및 그래픽 PowerShell 워크플로 runbook에서 생성 되 고 hello hello Azure 포털의에서 그래픽 편집기로 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-117">[Graphical](automation-runbook-types.md#graphical-runbooks) and Graphical PowerShell Workflow runbooks are created and edited with hello graphical editor in hello Azure portal.</span></span>  <span data-ttu-id="ec937-118">Tooa 파일을 내보내야 하 고 다른 자동화 계정으로 가져올 수 있지만 만들거나 다른 도구로 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-118">You can export them tooa file and then import them into another automation account, but you cannot create or edit them with another tool.</span></span>  <span data-ttu-id="ec937-119">그래픽 runbook에는 PowerShell 코드를 생성 하지만 직접 확인 하거나 hello 코드를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-119">Graphical runbooks generate PowerShell code, but you can't directly view or modify hello code.</span></span> <span data-ttu-id="ec937-120">그래픽 runbook hello의 변환 된 tooone 안 [텍스트 형식](automation-runbook-types.md), 또는 텍스트 runbook 변환된 toographical 형식의 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-120">Graphical runbooks cannot be converted tooone of hello [text formats](automation-runbook-types.md), nor can a text runbook be converted toographical format.</span></span> <span data-ttu-id="ec937-121">그래픽 runbook 가져오기 및 반대로 하는 동안 변환 된 tooGraphical PowerShell 워크플로 runbook 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-121">Graphical runbooks can be converted tooGraphical PowerShell Workflow runbooks during import and vice-versa.</span></span>

### <a name="advantages"></a><span data-ttu-id="ec937-122">장점</span><span class="sxs-lookup"><span data-stu-id="ec937-122">Advantages</span></span>
* <span data-ttu-id="ec937-123">시각적 삽입-링크-구성 제작 모델</span><span class="sxs-lookup"><span data-stu-id="ec937-123">Visual insert-link-configure authoring model</span></span>  
* <span data-ttu-id="ec937-124">Hello 프로세스를 통해 데이터 흐름에 집중</span><span class="sxs-lookup"><span data-stu-id="ec937-124">Focus on how data flows through hello process</span></span>  
* <span data-ttu-id="ec937-125">관리 프로세스를 시각적으로 표시</span><span class="sxs-lookup"><span data-stu-id="ec937-125">Visually represent management processes</span></span>  
* <span data-ttu-id="ec937-126">자식 runbook toocreate 높은 수준의 워크플로로 다른 runbook을 포함</span><span class="sxs-lookup"><span data-stu-id="ec937-126">Include other runbooks as child runbooks toocreate high level workflows</span></span>  
* <span data-ttu-id="ec937-127">모듈식 프로그래밍 장려</span><span class="sxs-lookup"><span data-stu-id="ec937-127">Encourages modular programming</span></span>  


### <a name="limitations"></a><span data-ttu-id="ec937-128">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ec937-128">Limitations</span></span>
* <span data-ttu-id="ec937-129">Azure 포털 외부에서 Runbook을 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-129">Can't edit runbook outside of Azure portal.</span></span>
* <span data-ttu-id="ec937-130">PowerShell 코드 tooperform 복잡 한 논리를 포함 하는 코드 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-130">May require a Code activity containing PowerShell code tooperform complex logic.</span></span>
* <span data-ttu-id="ec937-131">Hello 그래픽 워크플로 의해 만들어진 hello PowerShell 코드를 직접 편집 하거나 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-131">Can't view or directly edit hello PowerShell code that is created by hello graphical workflow.</span></span> <span data-ttu-id="ec937-132">참고 모든 코드 활동에서 생성 되는 hello 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-132">Note that you can view hello code you create in any Code activities.</span></span>

## <a name="powershell-runbooks"></a><span data-ttu-id="ec937-133">PowerShell Runbook</span><span class="sxs-lookup"><span data-stu-id="ec937-133">PowerShell runbooks</span></span>
<span data-ttu-id="ec937-134">PowerShell Runbook은 Windows PowerShell을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-134">PowerShell runbooks are based on Windows PowerShell.</span></span>  <span data-ttu-id="ec937-135">직접 hello 텍스트 편집기를 사용 하 여 hello Azure 포털에서에서 하는 hello runbook의 hello 코드를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-135">You directly edit hello code of hello runbook using hello text editor in hello Azure portal.</span></span>  <span data-ttu-id="ec937-136">또한 오프 라인 텍스트 편집기를 사용할 수 있습니다 및 [hello runbook 가져오기](http://msdn.microsoft.com/library/azure/dn643637.aspx) Azure 자동화로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-136">You can also use any offline text editor and [import hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="ec937-137">장점</span><span class="sxs-lookup"><span data-stu-id="ec937-137">Advantages</span></span>
* <span data-ttu-id="ec937-138">PowerShell 워크플로 hello 추가 복잡성 없이 PowerShell 코드와 함께 모든 복잡 한 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-138">Implement all complex logic with PowerShell code without hello additional complexities of PowerShell Workflow.</span></span> 
* <span data-ttu-id="ec937-139">Runbook 실행 하기 전에 컴파일된 toobe 필요 하지 않습니다 이후 PowerShell 워크플로 runbook 보다 더 빨리 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-139">Runbook starts faster than PowerShell Workflow runbooks since it doesn't need toobe compiled before running.</span></span>

### <a name="limitations"></a><span data-ttu-id="ec937-140">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ec937-140">Limitations</span></span>
* <span data-ttu-id="ec937-141">PowerShell 스크립팅에 대해 잘 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-141">Must be familiar with PowerShell scripting.</span></span>
* <span data-ttu-id="ec937-142">사용할 수 없는 [병렬 처리](automation-powershell-workflow.md#parallel-processing) tooperform 병렬로 여러 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-142">Can't use [parallel processing](automation-powershell-workflow.md#parallel-processing) tooperform multiple actions in parallel.</span></span>
* <span data-ttu-id="ec937-143">사용할 수 없는 [검사점](automation-powershell-workflow.md#checkpoints) 오류 시 runbook tooresume 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-143">Can't use [checkpoints](automation-powershell-workflow.md#checkpoints) tooresume runbook in case of error.</span></span>
* <span data-ttu-id="ec937-144">PowerShell 워크플로 runbook 및 그래픽 runbook만 포함할 수 자식 runbook으로 새 작업을 만듭니다는 hello Start-azureautomationrunbook cmdlet을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-144">PowerShell Workflow runbooks and Graphical runbooks can only be included as child runbooks by using hello Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

### <a name="known-issues"></a><span data-ttu-id="ec937-145">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="ec937-145">Known Issues</span></span>
<span data-ttu-id="ec937-146">PowerShell Runbook에 대해 현재 알려진 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-146">Following are current known issues with PowerShell runbooks.</span></span>

* <span data-ttu-id="ec937-147">PowerShell Runbook은 null 값으로 암호화되지 않은 [변수 자산](automation-variables.md) 을 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-147">PowerShell runbooks cannot cannot retrieve an unencrypted [variable asset](automation-variables.md) with a null value.</span></span>
* <span data-ttu-id="ec937-148">PowerShell runbook을 검색할 수 없습니다는 [변수 자산](automation-variables.md) 와  *~*  hello 이름에서입니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-148">PowerShell runbooks cannot retrieve a [variable asset](automation-variables.md) with *~* in hello name.</span></span>
* <span data-ttu-id="ec937-149">PowerShell Runbook의 반복적인 Get-Process는 80회 반복 후에 작동이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-149">Get-Process in a loop in a PowerShell runbook may crash after about 80 iterations.</span></span> 
* <span data-ttu-id="ec937-150">PowerShell runbook은 한 번에 매우 많은 양의 데이터 toohello 출력 스트림에 toowrite 시도 하는 경우 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-150">A PowerShell runbook may fail if it attempts toowrite a very large amount of data toohello output stream at once.</span></span>   <span data-ttu-id="ec937-151">일반적으로 큰 개체로 작업할 때 필요한 hello 정보만 출력 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-151">You can typically work around this issue by outputting just hello information you need when working with large objects.</span></span>  <span data-ttu-id="ec937-152">예를 들어 다음과 같이 출력 대신 *Get-process*, 방금 hello 필수 필드를 출력할 수 *Get-process | ProcessName, CPU 선택*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-152">For example, instead of outputting something like *Get-Process*, you can output just hello required fields with *Get-Process | Select ProcessName, CPU*.</span></span>

## <a name="powershell-workflow-runbooks"></a><span data-ttu-id="ec937-153">PowerShell 워크플로 Runbook</span><span class="sxs-lookup"><span data-stu-id="ec937-153">PowerShell Workflow runbooks</span></span>
<span data-ttu-id="ec937-154">PowerShell 워크플로 Runbook은 [Windows PowerShell 워크플로](automation-powershell-workflow.md)를 기반으로 하는 텍스트 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-154">PowerShell Workflow runbooks are text runbooks based on [Windows PowerShell Workflow](automation-powershell-workflow.md).</span></span>  <span data-ttu-id="ec937-155">직접 hello 텍스트 편집기를 사용 하 여 hello Azure 포털에서에서 하는 hello runbook의 hello 코드를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-155">You directly edit hello code of hello runbook using hello text editor in hello Azure portal.</span></span>  <span data-ttu-id="ec937-156">또한 오프 라인 텍스트 편집기를 사용할 수 있습니다 및 [hello runbook 가져오기](http://msdn.microsoft.com/library/azure/dn643637.aspx) Azure 자동화로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-156">You can also use any offline text editor and [import hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="ec937-157">장점</span><span class="sxs-lookup"><span data-stu-id="ec937-157">Advantages</span></span>
* <span data-ttu-id="ec937-158">PowerShell 워크플로 코드로 모든 복잡한 로직을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-158">Implement all complex logic with PowerShell Workflow code.</span></span>
* <span data-ttu-id="ec937-159">사용 하 여 [검사점](automation-powershell-workflow.md#checkpoints) 오류 시 runbook tooresume 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-159">Use [checkpoints](automation-powershell-workflow.md#checkpoints) tooresume runbook in case of error.</span></span>
* <span data-ttu-id="ec937-160">사용 하 여 [병렬 처리](automation-powershell-workflow.md#parallel-processing) tooperform 병렬로 여러 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-160">Use [parallel processing](automation-powershell-workflow.md#parallel-processing) tooperform multiple actions in parallel.</span></span>
* <span data-ttu-id="ec937-161">자식 runbook toocreate 높은 수준의 워크플로로 다른 그래픽 runbook 및 PowerShell 워크플로 runbook을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-161">Can include other Graphical runbooks and PowerShell Workflow runbooks as child runbooks toocreate high level workflows.</span></span>

### <a name="limitations"></a><span data-ttu-id="ec937-162">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ec937-162">Limitations</span></span>
* <span data-ttu-id="ec937-163">작성자는 PowerShell 워크플로를 잘 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-163">Author must be familiar with PowerShell Workflow.</span></span>
* <span data-ttu-id="ec937-164">Runbook hello PowerShell 워크플로 복잡성이 추가 같은 처리 해야 [개체를 역직렬화 할](automation-powershell-workflow.md#code-changes)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-164">Runbook must deal with hello additional complexity of PowerShell Workflow such as [deserialized objects](automation-powershell-workflow.md#code-changes).</span></span>
* <span data-ttu-id="ec937-165">Runbook 실행 하기 전에 컴파일된 toobe 해야 하므로 PowerShell runbook 보다 더 긴 toostart를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-165">Runbook takes longer toostart than PowerShell runbooks since it needs toobe compiled before running.</span></span>
* <span data-ttu-id="ec937-166">새 작업을 만듭니다는 hello Start-azureautomationrunbook cmdlet을 사용 하 여 PowerShell runbook를 자식 runbook으로 포함할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-166">PowerShell runbooks can only be included as child runbooks by using hello Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

## <a name="considerations"></a><span data-ttu-id="ec937-167">고려 사항</span><span class="sxs-lookup"><span data-stu-id="ec937-167">Considerations</span></span>
<span data-ttu-id="ec937-168">계정 hello 추가로 고려해 야 할 특정 runbook에 대 한 어떤 유형 toouse 결정할 때 다음을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-168">You should take into account hello following additional considerations when determining which type toouse for a particular runbook.</span></span>

* <span data-ttu-id="ec937-169">그래픽 tootextual 형식 또는 그 반대로에서 runbook을 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-169">You can't convert runbooks from graphical tootextual type or vice-versa.</span></span>
* <span data-ttu-id="ec937-170">형식이 다른 Runbook을 자식 Runbook으로 사용하는 경우 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec937-170">There are limitations using runbooks of different types as a child runbook.</span></span>  <span data-ttu-id="ec937-171">자세한 내용은 [Azure 자동화의 자식 Runbook](automation-child-runbooks.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec937-171">See [Child runbooks in Azure Automation](automation-child-runbooks.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec937-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec937-172">Next steps</span></span>
* <span data-ttu-id="ec937-173">그래픽 runbook 제작에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ec937-173">toolearn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="ec937-174">toounderstand hello 차이점 PowerShell 및 PowerShell 워크플로 runbook에 대 한 자세한 내용은 [학습 Windows PowerShell 워크플로](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="ec937-174">toounderstand hello differences between PowerShell and PowerShell workflows for runbooks, see [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)</span></span>
* <span data-ttu-id="ec937-175">Toocreate 또는 가져오기 Runbook 참조 하는 방법에 대 한 자세한 내용은 [만들거나 Runbook 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="ec937-175">For more information on how toocreate or import a Runbook, see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span>

