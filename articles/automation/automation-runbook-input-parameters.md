---
title: "입력 매개 변수를 aaaRunbook | Microsoft Docs"
description: "Runbook 입력된 매개 변수는 시작 될 때 toopass 데이터 tooa runbook를 허용 하 여 runbook의 hello 유연성을 높이고 합니다. 이 문서에서는 입력 매개 변수가 사용되는 Runbook의 다양한 시나리오를 설명합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="76f39-104">Runbook 입력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="76f39-104">Runbook input parameters</span></span>
<span data-ttu-id="76f39-105">Runbook 입력된 매개 변수는 시작 될 때 toopass 데이터 tooit를 허용 하 여 runbook의 hello 유연성을 높이고 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="76f39-106">hello 매개 변수는 특정 시나리오 및 환경에 대 한 대상으로 하는 hello runbook 작업 toobe를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="76f39-107">이 문서에서는 입력 매개 변수가 사용되는 Runbook의 다양한 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="76f39-108">입력 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="76f39-108">Configure input parameters</span></span>
<span data-ttu-id="76f39-109">PowerShell, PowerShell 워크플로 및 그래픽 Runbook에서 입력 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="76f39-110">Runbook에는 여러 데이터 형식을 가진 여러 매개 변수가 있거나 매개 변수가 전혀 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="76f39-111">입력 매개 변수는 필수 또는 선택일 수 있으므로 선택적 매개 변수에 대한 기본값을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="76f39-112">Hello 사용 가능한 방법 중 하나를 통해 시작할 때 runbook에 대 한 toohello 입력된 매개 변수 값을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="76f39-113">이러한 방법 hello 포털 또는 웹 서비스에서 runbook 시작 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="76f39-114">또한 다른 Runbook에서 인라인으로 호출되는 하위 Runbook으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="76f39-115">PowerShell 및 PowerShell 워크플로 Runbook에서 입력 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="76f39-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="76f39-116">PowerShell 및 [PowerShell 워크플로 runbook](automation-first-runbook-textual.md) Azure 자동화에서 hello 다음 특성을 통해 정의 된 입력된 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="76f39-117">**속성**</span><span class="sxs-lookup"><span data-stu-id="76f39-117">**Property**</span></span> | <span data-ttu-id="76f39-118">**설명**</span><span class="sxs-lookup"><span data-stu-id="76f39-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="76f39-119">형식</span><span class="sxs-lookup"><span data-stu-id="76f39-119">Type</span></span> |<span data-ttu-id="76f39-120">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-120">Required.</span></span> <span data-ttu-id="76f39-121">hello 데이터 형식이 hello 매개 변수 값에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="76f39-122">모든 .NET 형식이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="76f39-123">이름</span><span class="sxs-lookup"><span data-stu-id="76f39-123">Name</span></span> |<span data-ttu-id="76f39-124">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-124">Required.</span></span> <span data-ttu-id="76f39-125">hello hello 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-125">hello name of hello parameter.</span></span> <span data-ttu-id="76f39-126">이 해야 hello runbook 내에서 고유 하 고 또는 포함 될 수 문자, 숫자, 밑줄 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="76f39-127">문자로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-127">It must start with a letter.</span></span> |
| <span data-ttu-id="76f39-128">필수</span><span class="sxs-lookup"><span data-stu-id="76f39-128">Mandatory</span></span> |<span data-ttu-id="76f39-129">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-129">Optional.</span></span> <span data-ttu-id="76f39-130">Hello 매개 변수에 대 한 값을 제공 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="76f39-131">설정한 경우이 너무**$true**, hello runbook이 시작 될 때 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="76f39-132">설정한 경우이 너무**$false**, 값은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="76f39-133">기본값</span><span class="sxs-lookup"><span data-stu-id="76f39-133">Default value</span></span> |<span data-ttu-id="76f39-134">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-134">Optional.</span></span>  <span data-ttu-id="76f39-135">Hello runbook을 시작 하는 값에서 전달 되지 않은 경우 hello 매개 변수에 사용할 수 있는 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="76f39-136">기본값은 모든 매개 변수에 대해 설정할 수 있으며를 자동으로 hello 매개 변수 hello 필수 설정에 관계 없이 (옵션).</span><span class="sxs-lookup"><span data-stu-id="76f39-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="76f39-137">Windows PowerShell은 유효성 검사, 별칭, 매개 변수 설정과 같이 여기에 나열된 것 보다 많은 입력 매개 변수의 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="76f39-138">그러나 Azure 자동화에는 현재 hello 입력된 매개 변수만 위에 나열 된 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="76f39-139">PowerShell 워크플로 runbook에 매개 변수 정의 hello 다음 일반 형식의 여러 매개 변수는 쉼표로 구분 하는 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="76f39-140">Hello를 지정 하지 않으면 매개 변수를 정의 하는 경우 **필수** 특성을 기본적으로 hello 매개 변수는 선택 사항으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="76f39-141">또한 PowerShell 워크플로 runbook의 매개 변수에 대해 기본값을 설정 하면 것으로 간주 되며 PowerShell에서 hello에 관계 없이 선택적 매개 변수 **필수** 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="76f39-142">예를 들어 hello 가상 컴퓨터를 단일 VM 또는 리소스 그룹 내의 모든 Vm에 대 한 세부 정보를 출력 하는 PowerShell 워크플로 runbook에 대 한 입력된 매개 변수를 구성 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="76f39-143">이 runbook에 두 개의 매개 변수는 hello 스크린 샷 뒤에 표시 된 대로: hello 리소스 그룹의 hello 이름과 가상 컴퓨터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![자동화 PowerShell 워크플로](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="76f39-145">이 매개 변수 정의에서 매개 변수를 hello **$VMName** 및 **$resourceGroupName** 는 string 형식의 단순 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="76f39-146">그러나 PowerShell 및 PowerShell 워크플로 Runbook은 입력 매개 변수에 대해 **개체** 또는 **PSCredential**과 같은 단순 형식 및 복합 형식을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="76f39-147">Runbook에는 개체 유형 입력된 매개 경우 다음 PowerShell 해시 테이블 (이름, 값)를 사용 하 여 toopass 값에서 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="76f39-148">예를 들어, hello 매개 변수는 runbook에서 다음 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="76f39-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="76f39-149">다음 값 toohello 매개 변수 다음 hello를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="76f39-150">그래픽 Runbook에서 입력 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="76f39-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="76f39-151">너무[그래픽 runbook 구성](automation-first-runbook-graphical.md) 입력된 매개 변수가 있는 만들겠습니다 그래픽 runbook 하거나 가상 컴퓨터에 대 한 세부 정보를 출력 하는 단일 VM 또는 리소스 그룹 내의 모든 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="76f39-152">아래 설명한 대로 Runbook이 두 가지 주요 작업으로 이루어지도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="76f39-153">[**Azure 실행 계정으로 Runbook 인증** ](automation-sec-configure-azure-runas-account.md) azure tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="76f39-154">[**Get AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) 가상 컴퓨터의 tooget hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="76f39-155">Hello를 사용할 수 있습니다 [ **Write-output** ](https://technet.microsoft.com/library/hh849921.aspx) 가상 컴퓨터의 활동 toooutput hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="76f39-156">활동 hello **Get AzureRmVm** 두 개의 매개 변수를 받고 hello **가상 컴퓨터 이름** 및 hello **리소스 그룹 이름은**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="76f39-157">이러한 매개 변수 값이 다른 hello runbook을 시작할 때 필요할 수, 이후 tooyour runbook 입력된 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="76f39-158">Hello 단계 tooadd 입력된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="76f39-159">선택 hello hello에서 그래픽 runbook **Runbook** 블레이드에 대 한 클릭 [ **편집** ](automation-graphical-authoring-intro.md) 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="76f39-160">Hello runbook 편집기에서 클릭 **입력 및 출력** tooopen hello **입력 및 출력** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![자동화 그래픽 Runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="76f39-162">hello **입력 및 출력** 블레이드 hello runbook에 대해 정의 된 입력된 매개 변수 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="76f39-163">이 블레이드를 새 입력된 매개 변수를 추가 하거나 기존 입력된 매개 변수의 hello 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="76f39-164">tooadd hello runbook에 대 한 새 매개 변수를 클릭 **입력 추가** tooopen hello **Runbook 입력된 매개 변수** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="76f39-165">여기에 매개 변수 뒤 hello를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="76f39-166">**속성**</span><span class="sxs-lookup"><span data-stu-id="76f39-166">**Property**</span></span> | <span data-ttu-id="76f39-167">**설명**</span><span class="sxs-lookup"><span data-stu-id="76f39-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="76f39-168">이름</span><span class="sxs-lookup"><span data-stu-id="76f39-168">Name</span></span> |<span data-ttu-id="76f39-169">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-169">Required.</span></span>  <span data-ttu-id="76f39-170">hello hello 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-170">hello name of hello parameter.</span></span> <span data-ttu-id="76f39-171">이 해야 hello runbook 내에서 고유 하 고 또는 포함 될 수 문자, 숫자, 밑줄 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="76f39-172">문자로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="76f39-173">설명</span><span class="sxs-lookup"><span data-stu-id="76f39-173">Description</span></span> |<span data-ttu-id="76f39-174">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-174">Optional.</span></span> <span data-ttu-id="76f39-175">입력된 매개 변수의 hello 용도 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="76f39-176">형식</span><span class="sxs-lookup"><span data-stu-id="76f39-176">Type</span></span> |<span data-ttu-id="76f39-177">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-177">Optional.</span></span> <span data-ttu-id="76f39-178">hello 매개 변수 값에 대 한 예상 되는 hello 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="76f39-179">지원되는 매개 변수 형식은 **문자열**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** 및 **개체**입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="76f39-180">데이터 형식을 선택 하지 않으면 기본값 너무**문자열**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="76f39-181">필수</span><span class="sxs-lookup"><span data-stu-id="76f39-181">Mandatory</span></span> |<span data-ttu-id="76f39-182">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-182">Optional.</span></span> <span data-ttu-id="76f39-183">Hello 매개 변수에 대 한 값을 제공 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="76f39-184">선택 하면 **예**, hello runbook이 시작 될 때 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="76f39-185">선택 하면 **없습니다**, hello runbook을 시작 하 고 기본값을 설정할 수 있습니다 때 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="76f39-186">기본값</span><span class="sxs-lookup"><span data-stu-id="76f39-186">Default Value</span></span> |<span data-ttu-id="76f39-187">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-187">Optional.</span></span> <span data-ttu-id="76f39-188">Hello runbook을 시작 하는 값에서 전달 되지 않은 경우 hello 매개 변수에 사용할 수 있는 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="76f39-189">필수가 아닌 매개 변수에 기본값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="76f39-190">기본 값, tooset 선택 **사용자 지정**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="76f39-191">Hello runbook이 시작 될 때 다른 값을 제공 하지 않으면이 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="76f39-192">선택 **None** tooprovide 않으려는 경우 모든 기본 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![새 입력 추가](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="76f39-194">다음과 같은 hello에서 사용할 속성 hello로 두 개의 매개 변수를 만들 **Get AzureRmVm** 활동:</span><span class="sxs-lookup"><span data-stu-id="76f39-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="76f39-195">**매개 변수 1:**</span><span class="sxs-lookup"><span data-stu-id="76f39-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="76f39-196">이름 - VMName</span><span class="sxs-lookup"><span data-stu-id="76f39-196">Name - VMName</span></span>
     * <span data-ttu-id="76f39-197">형식 - String</span><span class="sxs-lookup"><span data-stu-id="76f39-197">Type - String</span></span>
     * <span data-ttu-id="76f39-198">필수 - 없음</span><span class="sxs-lookup"><span data-stu-id="76f39-198">Mandatory - No</span></span>
   * <span data-ttu-id="76f39-199">**매개 변수 2:**</span><span class="sxs-lookup"><span data-stu-id="76f39-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="76f39-200">이름 - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="76f39-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="76f39-201">형식 - String</span><span class="sxs-lookup"><span data-stu-id="76f39-201">Type - String</span></span>
     * <span data-ttu-id="76f39-202">필수 - 없음</span><span class="sxs-lookup"><span data-stu-id="76f39-202">Mandatory - No</span></span>
     * <span data-ttu-id="76f39-203">기본값 - 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="76f39-203">Default value - Custom</span></span>
     * <span data-ttu-id="76f39-204">사용자 지정 기본 값- \<hello 가상 컴퓨터를 포함 하는 hello 리소스 그룹의 이름 ></span><span class="sxs-lookup"><span data-stu-id="76f39-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="76f39-205">Hello 매개 변수를 추가한 후 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="76f39-206">Hello에 이제 볼 수 **입력 및 출력 블레이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="76f39-207">다시 **확인**을 클릭한 다음 Runbook을 **저장**하고 **게시**하도록 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="76f39-208">Runbook에서 tooinput 매개 변수 값 할당</span><span class="sxs-lookup"><span data-stu-id="76f39-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="76f39-209">다음 시나리오는 hello의 runbook에서 값 tooinput 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="76f39-210">Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="76f39-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="76f39-211">Runbook에 여러 가지 방법으로 시작할 수 있습니다: hello 여 webhook을 사용할지, PowerShell cmdlet을 통해, hello REST API 또는 hello SDK로 Azure 포털을 통해.</span><span class="sxs-lookup"><span data-stu-id="76f39-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="76f39-212">아래에서는 Runbook을 시작하고 매개 변수를 할당하는 여러 가지 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="76f39-213">Hello Azure 포털을 사용 하 여 게시 된 runbook을 시작 하 고 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="76f39-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="76f39-214">때 있습니다 [hello runbook을 시작](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Runbook 시작** 블레이드가 열리고 방금 만든 hello 매개 변수 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Hello 포털을 사용 하 여 시작](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="76f39-216">Hello 입력된 상자 아래 hello 레이블에서 hello 매개 변수에 대해 설정 된 hello 특성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="76f39-217">특성은 필수 또는 선택적, 형식 및 기본값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="76f39-218">Hello 도움말 풍선 다음 toohello 매개 변수 이름, 매개 변수 입력된 값에 대 한 toomake 결정 필요한 모든 hello 키 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="76f39-219">이 정보는 매개 변수가 필수 또는 선택인지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="76f39-220">Hello 형식 및 기본값 (있는 경우), 및 기타 유용한 정보에도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![도움말 풍선](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="76f39-222">문자열 형식 매개 변수는 **빈** 문자열 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="76f39-223">입력 **[EmptyString]** hello 입력된 매개 변수 상자는 빈 문자열 toohello 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="76f39-224">또한 문자열 형식 매개 변수는 전달되는 **Null** 값을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="76f39-225">모든 값 toohello 문자열 매개 변수를 전달 하지 않으면, 다음 PowerShell 변환 합니다. null로 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="76f39-226">PowerShell cmdlet을 사용하여 게시된 Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="76f39-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="76f39-227">**Azure Resource Manager cmdlet:**[Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)을 사용하여 리소스 그룹에 생성된 자동화 Runbook을 시작할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="76f39-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="76f39-228">**예제:**</span><span class="sxs-lookup"><span data-stu-id="76f39-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="76f39-229">**Azure 서비스 관리 cmdlet:**[Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)을 사용하여 기본 리소스 그룹에 생성된 자동화 Runbook을 시작할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="76f39-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="76f39-230">**예제:**</span><span class="sxs-lookup"><span data-stu-id="76f39-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="76f39-231">PowerShell cmdlet, 기본 매개 변수를 사용 하 여 runbook을 시작할 때 **MicrosoftApplicationManagementStartedBy** hello 값을 사용 하 여 만든 **PowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="76f39-232">Hello에이 매개 변수를 볼 수 있습니다 **작업 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="76f39-233">SDK를 사용하여 Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="76f39-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="76f39-234">**Azure 리소스 관리자 메서드:** hello 프로그래밍 언어의 SDK를 사용 하 여 runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="76f39-235">다음은 자동화 계정의 Runbook을 시작하기 위한 C# 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="76f39-236">모든 hello 코드를 볼 수는 [GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="76f39-237">**Azure 서비스 관리 방법:** hello 프로그래밍 언어의 SDK를 사용 하 여 runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="76f39-238">다음은 자동화 계정의 Runbook을 시작하기 위한 C# 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="76f39-239">모든 hello 코드를 볼 수는 [GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="76f39-240">toostart이이 방법에서는 사전 toostore hello runbook 매개 변수를 만들고 **VMName** 및 **resourceGroupName**, 및 해당 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="76f39-241">Hello runbook을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-241">Then start hello runbook.</span></span> <span data-ttu-id="76f39-242">다음은 위에 정의 된 hello 메서드를 호출 하는 것에 대 한 hello C# 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="76f39-243">Hello REST API를 사용 하 여 runbook을 시작 하 고 매개 변수를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="76f39-244">Runbook 작업을 만든 hello를 사용 하 여 Azure 자동화 REST API hello로 시작 하 고 **배치** 다음 hello로 메서드 요청 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="76f39-245">Hello 요청 URI에서에서 hello를 매개 변수를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="76f39-246">**subscription-id:** Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="76f39-247">**클라우드 서비스 이름:** hello 클라우드 서비스 toowhich hello 요청의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="76f39-248">**자동화 계정 이름:** hello 내에서 호스팅되는 자동화 계정 hello 이름은 클라우드 서비스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="76f39-249">**작업 id:** hello 작업에 대 한 GUID를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="76f39-250">Hello를 사용 하 여 PowerShell에서 Guid를 만들 수 있습니다 **[GUID]::NewGuid() 합니다. Tostring ()** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="76f39-251">순서 toopass 매개 변수 toohello runbook 작업을 hello 요청 본문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="76f39-252">다음 JSON 형식으로 제공 하는 두 개의 속성이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="76f39-253">**Runbook 이름:** 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-253">**Runbook name:** Required.</span></span> <span data-ttu-id="76f39-254">hello runbook의 이름 hello 작업 toostart hello입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="76f39-255">**Runbook 매개 변수:** 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="76f39-256">Hello 매개 변수 목록 (이름, 값)에서 사전 이름 문자열 형식 이어야 하 고 유효한 모든 JSON 값 값일 수 있는 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="76f39-257">Toostart hello를 원하는 경우 **Get AzureVMTextual** 와 이전 작성 된 runbook **VMName** 및 **resourceGroupName** 를 매개 변수로 사용 하 여 JSON 형식에 따라 hello 에 대 한 hello 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="76f39-258">HTTP 상태 코드 201 hello 작업이 올바르게 만들어진 경우에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="76f39-259">응답 헤더 및 hello 응답 본문에 대 한 자세한 내용은 참조는 방법에 대 한 toohello 문서 너무[hello REST API를 사용 하 여 runbook 작업을 만듭니다.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="76f39-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="76f39-260">Runbook 테스트 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="76f39-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="76f39-261">때 있습니다 [runbook의 테스트 hello 초안 버전](automation-testing-runbook.md) hello 테스트 옵션을 사용 하 여 hello **테스트** 블레이드가 열리고 방금 만든 hello 매개 변수 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![매개 변수 테스트 및 할당](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="76f39-263">일정 tooa runbook을 연결 하 고 매개 변수를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="76f39-264">할 수 있습니다 [일정 연결](automation-schedules.md) tooyour runbook 해당 hello runbook이 특정 시간에 시작 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="76f39-265">Hello 일정을 만들고 hello runbook는 hello 일정에 의해 시작 될 때 이러한 값을 사용 하는 경우에 입력된 매개 변수를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="76f39-266">모든 필수 매개 변수 값이 제공 되어야만 hello 일정을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![매개 변수 예약 및 할당](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="76f39-268">Runbook에 대한 webhook 만들기 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="76f39-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="76f39-269">Runbook에 대한 [webhook](automation-webhooks.md) 을 만들고 Runbook 입력 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="76f39-270">모든 필수 매개 변수 값이 제공 되어야만 hello webhook을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Webhook 만들기 및 매개 변수 할당](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="76f39-272">미리 정의 된 입력된 매개 변수 hello 여 webhook을 사용할지를 사용 하 여 runbook을 실행할 때 ** [Webhookdata](automation-webhooks.md#details-of-a-webhook) ** 정의한 hello 입력된 매개 변수와 함께 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="76f39-273">클릭할 수 있는 tooexpand hello **WebhookData** 자세한 내용은 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![WebhookData 매개 변수](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="76f39-275">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76f39-275">Next steps</span></span>
* <span data-ttu-id="76f39-276">Runbook 입력 및 출력에 대한 자세한 내용은 [Azure 자동화: Runbook 입력, 출력 및 중첩된 Runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76f39-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="76f39-277">다양 한 방법 toostart runbook에 대 한 세부 정보를 참조 하십시오. [runbook 시작](automation-starting-a-runbook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="76f39-278">텍스트 runbook tooedit 너무 참조[텍스트 runbook 편집](automation-edit-textual-runbook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="76f39-279">그래픽 runbook tooedit 너무 참조[Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76f39-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

