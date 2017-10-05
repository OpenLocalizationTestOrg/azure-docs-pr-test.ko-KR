---
title: "Azure Automation Runbook 형식 | Microsoft Docs"
description: "Azure 자동화에서 사용할 수 있는 다양한 형식의 Runbook을 설명하고 사용할 형식을 결정할 때 고려해야 하는 사항을 설명합니다. "
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
ms.openlocfilehash: e859aef473b433fbf4efb639962f3a3ce0a23d7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-runbook-types"></a><span data-ttu-id="2595e-103">Azure 자동화 Runbook 형식</span><span class="sxs-lookup"><span data-stu-id="2595e-103">Azure Automation runbook types</span></span>
<span data-ttu-id="2595e-104">Azure 자동화는 네 가지 형식의 runbook을 지원하며 다음 테이블에 간략한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-104">Azure Automation supports four types of runbooks that are  briefly described in the following table.</span></span>  <span data-ttu-id="2595e-105">아래 섹션은 각각을 사용할 경우에 대한 고려 사항을 포함하여 각 형식에 대해 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-105">The sections below provide further information about each type including considerations on when to use each.</span></span>

| <span data-ttu-id="2595e-106">형식</span><span class="sxs-lookup"><span data-stu-id="2595e-106">Type</span></span> | <span data-ttu-id="2595e-107">설명</span><span class="sxs-lookup"><span data-stu-id="2595e-107">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="2595e-108">그래픽</span><span class="sxs-lookup"><span data-stu-id="2595e-108">Graphical</span></span>](#graphical-runbooks) |<span data-ttu-id="2595e-109">Windows PowerShell을 기반으로 하며 Azure 포털의 그래픽 편집기로 완전하게 생성 및 편집됩니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-109">Based on Windows PowerShell and created and edited completely in graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="2595e-110">그래픽 PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="2595e-110">Graphical PowerShell Workflow</span></span>](#graphical-runbooks) |<span data-ttu-id="2595e-111">Windows PowerShell 워크플로를 기반으로 하며 Azure 포털의 그래픽 편집기로 완전하게 생성 및 편집됩니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-111">Based on Windows PowerShell Workflow and created and edited completely in the graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="2595e-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2595e-112">PowerShell</span></span>](#powershell-runbooks) |<span data-ttu-id="2595e-113">Windows PowerShell 스크립트를 기반으로 하는 텍스트 Runbook</span><span class="sxs-lookup"><span data-stu-id="2595e-113">Text runbook based on Windows PowerShell script.</span></span> |
| [<span data-ttu-id="2595e-114">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="2595e-114">PowerShell Workflow</span></span>](#powershell-workflow-runbooks) |<span data-ttu-id="2595e-115">Windows PowerShell 워크플로를 기반으로 하는 텍스트 Runbook</span><span class="sxs-lookup"><span data-stu-id="2595e-115">Text runbook based on Windows PowerShell Workflow.</span></span> |

## <a name="graphical-runbooks"></a><span data-ttu-id="2595e-116">그래픽 Runbook</span><span class="sxs-lookup"><span data-stu-id="2595e-116">Graphical runbooks</span></span>
<span data-ttu-id="2595e-117">[그래픽](automation-runbook-types.md#graphical-runbooks) 및 그래픽 PowerShell 워크플로 Runbook은 Azure 포털의 그래픽 편집기로 생성 및 편집됩니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-117">[Graphical](automation-runbook-types.md#graphical-runbooks) and Graphical PowerShell Workflow runbooks are created and edited with the graphical editor in the Azure portal.</span></span>  <span data-ttu-id="2595e-118">파일로 내보내서 다른 자동화 계정으로 가져올 수 있지만 다른 도구에서 만들거나 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-118">You can export them to a file and then import them into another automation account, but you cannot create or edit them with another tool.</span></span>  <span data-ttu-id="2595e-119">그래픽 Runbook은 PowerShell 코드를 생성하지만 코드를 직접 보거나 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-119">Graphical runbooks generate PowerShell code, but you can't directly view or modify the code.</span></span> <span data-ttu-id="2595e-120">그래픽 Runbook은 [텍스트 형식](automation-runbook-types.md)중 하나로 변환될 수 없고 텍스트 Runbook은 그래픽 형식으로 변환될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-120">Graphical runbooks cannot be converted to one of the [text formats](automation-runbook-types.md), nor can a text runbook be converted to graphical format.</span></span> <span data-ttu-id="2595e-121">가져오는 동안 그래픽 Runbook을 그래픽 PowerShell 워크플로 Runbook으로 변환하거나 그 반대로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-121">Graphical runbooks can be converted to Graphical PowerShell Workflow runbooks during import and vice-versa.</span></span>

### <a name="advantages"></a><span data-ttu-id="2595e-122">장점</span><span class="sxs-lookup"><span data-stu-id="2595e-122">Advantages</span></span>
* <span data-ttu-id="2595e-123">시각적 삽입-링크-구성 제작 모델</span><span class="sxs-lookup"><span data-stu-id="2595e-123">Visual insert-link-configure authoring model</span></span>  
* <span data-ttu-id="2595e-124">프로세스를 통해 데이터가 흐르는 방식에 집중</span><span class="sxs-lookup"><span data-stu-id="2595e-124">Focus on how data flows through the process</span></span>  
* <span data-ttu-id="2595e-125">관리 프로세스를 시각적으로 표시</span><span class="sxs-lookup"><span data-stu-id="2595e-125">Visually represent management processes</span></span>  
* <span data-ttu-id="2595e-126">다른 Runbook을 자식 Runbook으로 포함하여 높은 수준의 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="2595e-126">Include other runbooks as child runbooks to create high level workflows</span></span>  
* <span data-ttu-id="2595e-127">모듈식 프로그래밍 장려</span><span class="sxs-lookup"><span data-stu-id="2595e-127">Encourages modular programming</span></span>  


### <a name="limitations"></a><span data-ttu-id="2595e-128">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2595e-128">Limitations</span></span>
* <span data-ttu-id="2595e-129">Azure 포털 외부에서 Runbook을 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-129">Can't edit runbook outside of Azure portal.</span></span>
* <span data-ttu-id="2595e-130">복잡한 논리를 수행기 위해 PowerShell 코드를 포함하는 코드 작업이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-130">May require a Code activity containing PowerShell code to perform complex logic.</span></span>
* <span data-ttu-id="2595e-131">그래픽 워크플로에 의해 만들어진 PowerShell 코드를 보거나 직접 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-131">Can't view or directly edit the PowerShell code that is created by the graphical workflow.</span></span> <span data-ttu-id="2595e-132">코드 작업에서 만든 코드는 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-132">Note that you can view the code you create in any Code activities.</span></span>

## <a name="powershell-runbooks"></a><span data-ttu-id="2595e-133">PowerShell Runbook</span><span class="sxs-lookup"><span data-stu-id="2595e-133">PowerShell runbooks</span></span>
<span data-ttu-id="2595e-134">PowerShell Runbook은 Windows PowerShell을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-134">PowerShell runbooks are based on Windows PowerShell.</span></span>  <span data-ttu-id="2595e-135">Azure 포털의 텍스트 편집기를 사용하여 Runbook을 직접 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-135">You directly edit the code of the runbook using the text editor in the Azure portal.</span></span>  <span data-ttu-id="2595e-136">오프라인 텍스트 편집기도 사용할 수 있고 Azure 자동화로 [Runbook 가져오기](http://msdn.microsoft.com/library/azure/dn643637.aspx) 가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-136">You can also use any offline text editor and [import the runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="2595e-137">장점</span><span class="sxs-lookup"><span data-stu-id="2595e-137">Advantages</span></span>
* <span data-ttu-id="2595e-138">PowerShell 워크플로의 부가적인 복잡성 없이 PowerShell 코드로 모든 복잡한 로직을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-138">Implement all complex logic with PowerShell code without the additional complexities of PowerShell Workflow.</span></span> 
* <span data-ttu-id="2595e-139">Runbook은 실행 전에 컴파일이 필요 없기 때문에 PowerShell 워크플로 Runbook보다 빨리 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-139">Runbook starts faster than PowerShell Workflow runbooks since it doesn't need to be compiled before running.</span></span>

### <a name="limitations"></a><span data-ttu-id="2595e-140">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2595e-140">Limitations</span></span>
* <span data-ttu-id="2595e-141">PowerShell 스크립팅에 대해 잘 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-141">Must be familiar with PowerShell scripting.</span></span>
* <span data-ttu-id="2595e-142">여러 작업을 병렬 수행하도록 [병렬 처리](automation-powershell-workflow.md#parallel-processing) 를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-142">Can't use [parallel processing](automation-powershell-workflow.md#parallel-processing) to perform multiple actions in parallel.</span></span>
* <span data-ttu-id="2595e-143">오류 발생 시 Runbook을 다시 시작하도록 [검사점](automation-powershell-workflow.md#checkpoints) 을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-143">Can't use [checkpoints](automation-powershell-workflow.md#checkpoints) to resume runbook in case of error.</span></span>
* <span data-ttu-id="2595e-144">PowerShell 워크플로 Runbook 및 그래픽 Runbook은 새 작업을 만드는 Start-AzureAutomationRunbook cmdlet을 사용해서만 자식 Runbook으로 포함시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-144">PowerShell Workflow runbooks and Graphical runbooks can only be included as child runbooks by using the Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

### <a name="known-issues"></a><span data-ttu-id="2595e-145">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="2595e-145">Known Issues</span></span>
<span data-ttu-id="2595e-146">PowerShell Runbook에 대해 현재 알려진 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-146">Following are current known issues with PowerShell runbooks.</span></span>

* <span data-ttu-id="2595e-147">PowerShell Runbook은 null 값으로 암호화되지 않은 [변수 자산](automation-variables.md) 을 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-147">PowerShell runbooks cannot cannot retrieve an unencrypted [variable asset](automation-variables.md) with a null value.</span></span>
* <span data-ttu-id="2595e-148">PowerShell Runbook은 이름에 [변수 자산](automation-variables.md) 을 사용하여 *~* 을 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-148">PowerShell runbooks cannot retrieve a [variable asset](automation-variables.md) with *~* in the name.</span></span>
* <span data-ttu-id="2595e-149">PowerShell Runbook의 반복적인 Get-Process는 80회 반복 후에 작동이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-149">Get-Process in a loop in a PowerShell runbook may crash after about 80 iterations.</span></span> 
* <span data-ttu-id="2595e-150">PowerShell Runbook은 한 번에 스트림을 출력하기 위해 매우 큰 데이터를 쓰려는 시도를 하면 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-150">A PowerShell runbook may fail if it attempts to write a very large amount of data to the output stream at once.</span></span>   <span data-ttu-id="2595e-151">일반적으로 큰 개체로 작업하는 경우 필요한 정보만 출력하면 이 문제를 극복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-151">You can typically work around this issue by outputting just the information you need when working with large objects.</span></span>  <span data-ttu-id="2595e-152">예를 들어 *Get-Process* 같은 출력 대신 *Get-Process | Select ProcessName, CPU*를 사용하여 필요한 필드만 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-152">For example, instead of outputting something like *Get-Process*, you can output just the required fields with *Get-Process | Select ProcessName, CPU*.</span></span>

## <a name="powershell-workflow-runbooks"></a><span data-ttu-id="2595e-153">PowerShell 워크플로 Runbook</span><span class="sxs-lookup"><span data-stu-id="2595e-153">PowerShell Workflow runbooks</span></span>
<span data-ttu-id="2595e-154">PowerShell 워크플로 Runbook은 [Windows PowerShell 워크플로](automation-powershell-workflow.md)를 기반으로 하는 텍스트 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-154">PowerShell Workflow runbooks are text runbooks based on [Windows PowerShell Workflow](automation-powershell-workflow.md).</span></span>  <span data-ttu-id="2595e-155">Azure 포털의 텍스트 편집기를 사용하여 Runbook을 직접 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-155">You directly edit the code of the runbook using the text editor in the Azure portal.</span></span>  <span data-ttu-id="2595e-156">오프라인 텍스트 편집기도 사용할 수 있고 Azure 자동화로 [Runbook 가져오기](http://msdn.microsoft.com/library/azure/dn643637.aspx) 가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-156">You can also use any offline text editor and [import the runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="2595e-157">장점</span><span class="sxs-lookup"><span data-stu-id="2595e-157">Advantages</span></span>
* <span data-ttu-id="2595e-158">PowerShell 워크플로 코드로 모든 복잡한 로직을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-158">Implement all complex logic with PowerShell Workflow code.</span></span>
* <span data-ttu-id="2595e-159">오류가 발생하면 [검사점](automation-powershell-workflow.md#checkpoints) 을 사용하여 Runbook을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-159">Use [checkpoints](automation-powershell-workflow.md#checkpoints) to resume runbook in case of error.</span></span>
* <span data-ttu-id="2595e-160">[병렬 처리](automation-powershell-workflow.md#parallel-processing) 를 사용하여 여러 작업을 병렬로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-160">Use [parallel processing](automation-powershell-workflow.md#parallel-processing) to perform multiple actions in parallel.</span></span>
* <span data-ttu-id="2595e-161">다른 그래픽 Runbook 및 PowerShell 워크플로 Runbook을 자식 Runbook으로 포함시켜 고급 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-161">Can include other Graphical runbooks and PowerShell Workflow runbooks as child runbooks to create high level workflows.</span></span>

### <a name="limitations"></a><span data-ttu-id="2595e-162">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2595e-162">Limitations</span></span>
* <span data-ttu-id="2595e-163">작성자는 PowerShell 워크플로를 잘 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-163">Author must be familiar with PowerShell Workflow.</span></span>
* <span data-ttu-id="2595e-164">Runbook은 [역직렬화된 개체](automation-powershell-workflow.md#code-changes)와 같은 PowerShell 워크플로의 부가적인 복잡성을 다루어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-164">Runbook must deal with the additional complexity of PowerShell Workflow such as [deserialized objects](automation-powershell-workflow.md#code-changes).</span></span>
* <span data-ttu-id="2595e-165">Runbook은 실행 전에 컴파일이 필요하기 때문에 PowerShell Runbook보다 시작 시간이 깁니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-165">Runbook takes longer to start than PowerShell runbooks since it needs to be compiled before running.</span></span>
* <span data-ttu-id="2595e-166">PowerShell Runbook은 새 작업을 만드는 Start-AzureAutomationRunbook cmdlet을 사용해서만 자식 Runbook으로 포함시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-166">PowerShell runbooks can only be included as child runbooks by using the Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

## <a name="considerations"></a><span data-ttu-id="2595e-167">고려 사항</span><span class="sxs-lookup"><span data-stu-id="2595e-167">Considerations</span></span>
<span data-ttu-id="2595e-168">특정한 Runbook에 사용할 형식을 결정할 때 다음과 같은 사항을 추가로 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-168">You should take into account the following additional considerations when determining which type to use for a particular runbook.</span></span>

* <span data-ttu-id="2595e-169">Runbook를 그래픽에서 텍스트 형식으로 또는 그 반대로 변환할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-169">You can't convert runbooks from graphical to textual type or vice-versa.</span></span>
* <span data-ttu-id="2595e-170">형식이 다른 Runbook을 자식 Runbook으로 사용하는 경우 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2595e-170">There are limitations using runbooks of different types as a child runbook.</span></span>  <span data-ttu-id="2595e-171">자세한 내용은 [Azure 자동화의 자식 Runbook](automation-child-runbooks.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2595e-171">See [Child runbooks in Azure Automation](automation-child-runbooks.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2595e-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2595e-172">Next steps</span></span>
* <span data-ttu-id="2595e-173">그래픽 Runbook 작성에 대해 자세히 알아보려면 [Azure 자동화에서 그래픽 작성](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="2595e-173">To learn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="2595e-174">Runbook용 PowerShell 및 PowerShell 워크플로 간의 차이점을 이해하려면 [Windows PowerShell 워크플로 학습](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="2595e-174">To understand the differences between PowerShell and PowerShell workflows for runbooks, see [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)</span></span>
* <span data-ttu-id="2595e-175">Runbook을 만들거나 가져오는 방법에 대한 자세한 내용은 [Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="2595e-175">For more information on how to create or import a Runbook, see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span>

