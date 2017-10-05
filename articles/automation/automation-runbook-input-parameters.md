---
title: "Runbook 입력 매개 변수| Microsoft Docs"
description: "Runbook 입력 매개 변수는 Runbook이 시작될 때 Runbook에 데이터를 전달할 수 있도록 하여 Runbook의 유용성을 늘립니다. 이 문서에서는 입력 매개 변수가 사용되는 Runbook의 다양한 시나리오를 설명합니다."
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
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="3c15d-104">Runbook 입력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3c15d-104">Runbook input parameters</span></span>
<span data-ttu-id="3c15d-105">Runbook 입력 매개 변수는 Runbook이 시작될 때 Runbook에 데이터를 전달할 수 있도록 하여 Runbook의 유용성을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="3c15d-106">매개 변수는 Runbook 동작이 특정 시나리오 및 환경에 대한 대상이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="3c15d-107">이 문서에서는 입력 매개 변수가 사용되는 Runbook의 다양한 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="3c15d-108">입력 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="3c15d-108">Configure input parameters</span></span>
<span data-ttu-id="3c15d-109">PowerShell, PowerShell 워크플로 및 그래픽 Runbook에서 입력 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="3c15d-110">Runbook에는 여러 데이터 형식을 가진 여러 매개 변수가 있거나 매개 변수가 전혀 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="3c15d-111">입력 매개 변수는 필수 또는 선택일 수 있으므로 선택적 매개 변수에 대한 기본값을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="3c15d-112">사용 가능한 방법 중 하나를 통해 시작할 때 Runbook에 대한 입력 매개 변수에 값을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="3c15d-113">이러한 메서드는 포털 또는 웹 서비스에서 Runbook 시작하기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="3c15d-114">또한 다른 Runbook에서 인라인으로 호출되는 하위 Runbook으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="3c15d-115">PowerShell 및 PowerShell 워크플로 Runbook에서 입력 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="3c15d-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="3c15d-116">Azure 자동화에서 PowerShell 및 [PowerShell 워크플로 Runbook](automation-first-runbook-textual.md) 는 다음과 같은 특성을 통해 정의된 입력 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="3c15d-117">**속성**</span><span class="sxs-lookup"><span data-stu-id="3c15d-117">**Property**</span></span> | <span data-ttu-id="3c15d-118">**설명**</span><span class="sxs-lookup"><span data-stu-id="3c15d-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="3c15d-119">형식</span><span class="sxs-lookup"><span data-stu-id="3c15d-119">Type</span></span> |<span data-ttu-id="3c15d-120">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-120">Required.</span></span> <span data-ttu-id="3c15d-121">매개 변수 값에 필요한 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="3c15d-122">모든 .NET 형식이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="3c15d-123">이름</span><span class="sxs-lookup"><span data-stu-id="3c15d-123">Name</span></span> |<span data-ttu-id="3c15d-124">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-124">Required.</span></span> <span data-ttu-id="3c15d-125">매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-125">The name of the parameter.</span></span> <span data-ttu-id="3c15d-126">이름은 Runbook 내에서 고유해야 하고 문자, 숫자 또는 밑줄 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="3c15d-127">문자로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-127">It must start with a letter.</span></span> |
| <span data-ttu-id="3c15d-128">필수</span><span class="sxs-lookup"><span data-stu-id="3c15d-128">Mandatory</span></span> |<span data-ttu-id="3c15d-129">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-129">Optional.</span></span> <span data-ttu-id="3c15d-130">매개 변수에 대해 값을 제공해야 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="3c15d-131">이 값을 **$true**로 설정한 경우 Runbook이 시작될 때 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="3c15d-132">이 값을 **$false**로 설정한 경우 값은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="3c15d-133">기본값</span><span class="sxs-lookup"><span data-stu-id="3c15d-133">Default value</span></span> |<span data-ttu-id="3c15d-134">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-134">Optional.</span></span>  <span data-ttu-id="3c15d-135">Runbook이 시작될 때 값을 전달하지 않으면 매개 변수에 대해 사용될 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="3c15d-136">기본값을 매개 변수에 대해 설정할 수 있으며 필수 설정에 관계 없이 자동으로 매개 변수를 선택적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="3c15d-137">Windows PowerShell은 유효성 검사, 별칭, 매개 변수 설정과 같이 여기에 나열된 것 보다 많은 입력 매개 변수의 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="3c15d-138">그러나 Azure 자동화는 현재 위에 나열된 입력 매개 변수만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="3c15d-139">PowerShell 워크플로 Runbook의 매개 변수 정의에는 다음과 같은 일반 형식이 있으며 여러 매개 변수는 쉼표로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="3c15d-140">매개 변수를 정의할 때 **필수** 특성을 지정하지 않으면 기본적으로 매개 변수는 선택 사항으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="3c15d-141">또한 PowerShell 워크플로 Runbook의 매개 변수에 대한 기본값을 설정하는 경우 **필수** 특성 값과 관계 없이 PowerShell에서 선택적 매개 변수로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="3c15d-142">예를 들어 가상 컴퓨터(단일 VM 또는 리소스 그룹 내의 모든 VM)에 대한 세부 정보를 출력하는 PowerShell 워크플로 Runbook에 대한 입력 매개 변수를 구성해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="3c15d-143">다음 스크린샷에 보여준 대로 이 Runbook에는 가상 컴퓨터의 이름 및 리소스 그룹 이름이라는 두 가지 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![자동화 PowerShell 워크플로](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="3c15d-145">이 매개 변수 정의에서 매개 변수 **$VMName** 및 **$resourceGroupName**은 형식 문자열의 간단한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="3c15d-146">그러나 PowerShell 및 PowerShell 워크플로 Runbook은 입력 매개 변수에 대해 **개체** 또는 **PSCredential**과 같은 단순 형식 및 복합 형식을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="3c15d-147">Runbook에 object 형식 입력 매개 변수가 있는 경우 값에 전달하려면 (이름, 값) 쌍이 있는 PowerShell 해시 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="3c15d-148">예를 들어 Runbook에 다음 매개 변수가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="3c15d-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="3c15d-149">매개 변수에 다음 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="3c15d-150">그래픽 Runbook에서 입력 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="3c15d-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="3c15d-151">입력 매개 변수를 사용하여 그래픽 Runbook을 구성하려면 가상 컴퓨터(단일 VM 또는 리소스 그룹 내의 모든 VM)에 대한 세부 정보를 출력하는 [그래픽 Runbook](automation-first-runbook-graphical.md)을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="3c15d-152">아래 설명한 대로 Runbook이 두 가지 주요 작업으로 이루어지도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="3c15d-153">Azure로 인증하는 [**Azure 실행 계정으로 Runbook 인증**](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="3c15d-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="3c15d-154">가상 컴퓨터의 속성을 가져오는 [**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c15d-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="3c15d-155">[**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) 활동을 사용하여 가상 컴퓨터의 이름을 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="3c15d-156">**Get-AzureRmVm** 활동은 **가상 컴퓨터 이름** 및 **리소스 그룹 이름**과 같은 두 개의 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="3c15d-157">이러한 매개 변수가 Runbook을 시작할 때마다 다른 값을 필요할 수 있기 때문에 Runbook에 입력 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="3c15d-158">입력 매개 변수를 추가하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="3c15d-159">**Runbook** 블레이드에서 그래픽 Runbook을 선택한 다음 [**편집**](automation-graphical-authoring-intro.md)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="3c15d-160">Runbook 편집기에서 **입력 및 출력**을 클릭하여 **입력 및 출력** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![자동화 그래픽 Runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="3c15d-162">**입력 및 출력** 블레이드는 Runbook에 대해 정의된 입력 매개 변수 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="3c15d-163">이 블레이드에서 새 입력 매개 변수를 추가하거나 기존의 입력 매개 변수의 구성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="3c15d-164">Runbook에 새 매개 변수를 추가하려면 **입력 추가**를 클릭하여 **Runbook 입력 매개 변수** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="3c15d-165">거기서 다음 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="3c15d-166">**속성**</span><span class="sxs-lookup"><span data-stu-id="3c15d-166">**Property**</span></span> | <span data-ttu-id="3c15d-167">**설명**</span><span class="sxs-lookup"><span data-stu-id="3c15d-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="3c15d-168">이름</span><span class="sxs-lookup"><span data-stu-id="3c15d-168">Name</span></span> |<span data-ttu-id="3c15d-169">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-169">Required.</span></span>  <span data-ttu-id="3c15d-170">매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-170">The name of the parameter.</span></span> <span data-ttu-id="3c15d-171">이름은 Runbook 내에서 고유해야 하고 문자, 숫자 또는 밑줄 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="3c15d-172">문자로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="3c15d-173">설명</span><span class="sxs-lookup"><span data-stu-id="3c15d-173">Description</span></span> |<span data-ttu-id="3c15d-174">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-174">Optional.</span></span> <span data-ttu-id="3c15d-175">입력 매개 변수의 목적에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="3c15d-176">형식</span><span class="sxs-lookup"><span data-stu-id="3c15d-176">Type</span></span> |<span data-ttu-id="3c15d-177">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-177">Optional.</span></span> <span data-ttu-id="3c15d-178">매개 변수 값에 필요한 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="3c15d-179">지원되는 매개 변수 형식은 **문자열**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** 및 **개체**입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="3c15d-180">데이터 형식이 선택되어 있지 않으면 **문자열**에 대한 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="3c15d-181">필수</span><span class="sxs-lookup"><span data-stu-id="3c15d-181">Mandatory</span></span> |<span data-ttu-id="3c15d-182">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-182">Optional.</span></span> <span data-ttu-id="3c15d-183">매개 변수에 대해 값을 제공해야 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="3c15d-184">**예**를 선택한 경우 Runbook이 시작될 때 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="3c15d-185">**아니오**를 선택한 경우 Runbook이 시작될 때 값이 필요하지 않고 기본값이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="3c15d-186">기본값</span><span class="sxs-lookup"><span data-stu-id="3c15d-186">Default Value</span></span> |<span data-ttu-id="3c15d-187">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-187">Optional.</span></span> <span data-ttu-id="3c15d-188">Runbook이 시작될 때 값을 전달하지 않으면 매개 변수에 대해 사용될 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="3c15d-189">필수가 아닌 매개 변수에 기본값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="3c15d-190">기본값을 설정하려면 **사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="3c15d-191">Runbook이 시작될 때 다른 값을 지정하지 않으면 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="3c15d-192">기본값을 제공하지 않으려는 경우 **없음** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![새 입력 추가](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="3c15d-194">**Get-AzureRmVm** 활동에서 사용될 다음 속성을 가진 두 개의 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="3c15d-195">**매개 변수 1:**</span><span class="sxs-lookup"><span data-stu-id="3c15d-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="3c15d-196">이름 - VMName</span><span class="sxs-lookup"><span data-stu-id="3c15d-196">Name - VMName</span></span>
     * <span data-ttu-id="3c15d-197">형식 - String</span><span class="sxs-lookup"><span data-stu-id="3c15d-197">Type - String</span></span>
     * <span data-ttu-id="3c15d-198">필수 - 없음</span><span class="sxs-lookup"><span data-stu-id="3c15d-198">Mandatory - No</span></span>
   * <span data-ttu-id="3c15d-199">**매개 변수 2:**</span><span class="sxs-lookup"><span data-stu-id="3c15d-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="3c15d-200">이름 - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3c15d-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="3c15d-201">형식 - String</span><span class="sxs-lookup"><span data-stu-id="3c15d-201">Type - String</span></span>
     * <span data-ttu-id="3c15d-202">필수 - 없음</span><span class="sxs-lookup"><span data-stu-id="3c15d-202">Mandatory - No</span></span>
     * <span data-ttu-id="3c15d-203">기본값 - 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3c15d-203">Default value - Custom</span></span>
     * <span data-ttu-id="3c15d-204">사용자 지정 기본값 - \<가상 컴퓨터를 포함하는 리소스 그룹의 이름></span><span class="sxs-lookup"><span data-stu-id="3c15d-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="3c15d-205">매개 변수를 추가하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="3c15d-206">이제 **입력 및 출력 블레이드**에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="3c15d-207">다시 **확인**을 클릭한 다음 Runbook을 **저장**하고 **게시**하도록 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="3c15d-208">Runbook의 입력 매개 변수에 값 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="3c15d-209">다음과 같은 시나리오에서 Runbook의 매개 변수에 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="3c15d-210">Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="3c15d-211">Runbook은 Azure 포털, webhook, PowerShell cmdlet, REST API 또는 SDK 등 여러 가지 방법을 통해 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="3c15d-212">아래에서는 Runbook을 시작하고 매개 변수를 할당하는 여러 가지 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="3c15d-213">Azure 포털을 사용하여 게시된 Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="3c15d-214">[Runbook을 시작](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal)할 때 방금 만든 매개 변수에 대한 값을 구성할 수 있는 **Runbook 시작** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![포털을 사용하여 시작하기](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="3c15d-216">입력된 상자 아래에 있는 레이블에서 매개 변수에 대해 설정된 특성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="3c15d-217">특성은 필수 또는 선택적, 형식 및 기본값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="3c15d-218">매개 변수 이름 옆에 있는 도움말 풍선에서 매개 변수 입력 값에 대한 결정을 해야 할 모든 핵심 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="3c15d-219">이 정보는 매개 변수가 필수 또는 선택인지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="3c15d-220">형식 및 기본값(있는 경우) 및 기타 유용한 참고 사항도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![도움말 풍선](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="3c15d-222">문자열 형식 매개 변수는 **빈** 문자열 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="3c15d-223">입력 매개 변수 상자에 **[EmptyString]** 을 입력하면 빈 문자열을 매개 변수에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="3c15d-224">또한 문자열 형식 매개 변수는 전달되는 **Null** 값을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="3c15d-225">문자열 매개 변수에 값을 전달하지 않으면 PowerShell이 null로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="3c15d-226">PowerShell cmdlet을 사용하여 게시된 Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="3c15d-227">**Azure Resource Manager cmdlet:**[Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)을 사용하여 리소스 그룹에 생성된 자동화 Runbook을 시작할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="3c15d-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="3c15d-228">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c15d-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="3c15d-229">**Azure 서비스 관리 cmdlet:**[Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)을 사용하여 기본 리소스 그룹에 생성된 자동화 Runbook을 시작할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="3c15d-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="3c15d-230">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c15d-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="3c15d-231">PowerShell cmdlet을 사용하여 Runbook을 시작할 때 기본 매개 변수인 **MicrosoftApplicationManagementStartedBy**는 **PowerShell** 값을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="3c15d-232">**작업 세부 정보** 블레이드에서 이 매개 변수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="3c15d-233">SDK를 사용하여 Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="3c15d-234">**Azure Resource Manager 방법:** 프로그래밍 언어의 SDK를 사용하여 Runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="3c15d-235">다음은 자동화 계정의 Runbook을 시작하기 위한 C# 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="3c15d-236">[GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)에서 모든 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="3c15d-237">**Azure 서비스 관리 방법:** 프로그래밍 언어의 SDK를 사용하여 Runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="3c15d-238">다음은 자동화 계정의 Runbook을 시작하기 위한 C# 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="3c15d-239">[GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)에서 모든 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="3c15d-240">이 메서드를 시작하려면 사전을 만들어 Runbook 매개 변수, **VMName**, **resourceGroupName** 그리고 해당 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="3c15d-241">그런 다음 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-241">Then start the runbook.</span></span> <span data-ttu-id="3c15d-242">다음은 위에 정의된 메서드를 호출하기 위한 C# 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="3c15d-243">REST API를 사용하여 Runbook 시작 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="3c15d-244">다음 요청 URI가 있는 **PUT** 메서드를 사용하여 Azure 자동화 REST API를 통해 Runbook 작업을 만들고 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="3c15d-245">요청 URI에서 다음 매개 변수를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="3c15d-246">**subscription-id:** Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="3c15d-247">**cloud-service-name:** 요청을 보낼 클라우드 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="3c15d-248">**automation-account-name:** 지정된 클라우드 서비스 내에 호스트되는 자동화 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="3c15d-249">**job-id:** 작업에 대한 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="3c15d-250">**[GUID]::NewGuid().ToString()** 명령을 사용하여 PowerShell에서 GUID를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="3c15d-251">Runbook 작업에 매개 변수를 전달하기 위해 요청 본문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="3c15d-252">JSON 형식으로 제공되는 다음 두 가지 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="3c15d-253">**Runbook 이름:** 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-253">**Runbook name:** Required.</span></span> <span data-ttu-id="3c15d-254">시작할 작업 시작에 대한 Runbook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="3c15d-255">**Runbook 매개 변수:** 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="3c15d-256">이름이 문자열 형식이어야 하고 값은 유효한 JSON 값일 수 있는 (이름, 값) 형식인 매개 변수 목록의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="3c15d-257">이전에 **VMName** 및 **resourceGroupName**을 매개 변수로 만든 **Get-AzureVMTextual** Runbook을 시작하려는 경우 요청 본문에 다음 JSON 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

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

<span data-ttu-id="3c15d-258">작업이 성공적으로 만들어진 경우 HTTP 상태 코드 201이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="3c15d-259">응답 헤더 및 응답 본문에 대한 자세한 내용은 [REST API를 사용하여 Runbook 작업을 만드는](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="3c15d-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="3c15d-260">Runbook 테스트 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="3c15d-261">테스트 옵션을 사용하여 [Runbook의 초안 버전을 테스트](automation-testing-runbook.md) 할 때 **테스트** 블레이드가 열리고 방금 만든 매개 변수에 대한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![매개 변수 테스트 및 할당](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="3c15d-263">Runbook에 일정 연결 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="3c15d-264">Runbook이 특정 시간에 시작하도록 Runbook에 [일정을 연결](automation-schedules.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="3c15d-265">일정을 만드는 동안 입력 매개 변수를 할당하고 Runbook이 일정에 따라 시작될 때 이러한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="3c15d-266">모든 필수 매개 변수 값이 제공될 때까지 일정을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![매개 변수 예약 및 할당](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="3c15d-268">Runbook에 대한 webhook 만들기 및 매개 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3c15d-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="3c15d-269">Runbook에 대한 [webhook](automation-webhooks.md) 을 만들고 Runbook 입력 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="3c15d-270">모든 필수 매개 변수 값이 제공될 때까지 webhook을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Webhook 만들기 및 매개 변수 할당](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="3c15d-272">웹후크를 사용하여 Runbook을 실행할 때 미리 정의된 입력 매개 변수 **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** 가 사용자가 정의한 입력 매개 변수와 함께 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="3c15d-273">**WebhookData** 매개 변수를 클릭하여 확장하면 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c15d-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![WebhookData 매개 변수](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="3c15d-275">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c15d-275">Next steps</span></span>
* <span data-ttu-id="3c15d-276">Runbook 입력 및 출력에 대한 자세한 내용은 [Azure 자동화: Runbook 입력, 출력 및 중첩된 Runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c15d-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="3c15d-277">Runbook을 시작하는 다양한 방법에 대한 자세한 내용은 [Runbook 시작](automation-starting-a-runbook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c15d-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="3c15d-278">텍스트 Runbook을 편집하려면 [텍스트 Runbook 편집](automation-edit-textual-runbook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c15d-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="3c15d-279">그래픽 Runbook을 편집하려면 [Azure 자동화에서 그래픽 작성](automation-graphical-authoring-intro.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c15d-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

