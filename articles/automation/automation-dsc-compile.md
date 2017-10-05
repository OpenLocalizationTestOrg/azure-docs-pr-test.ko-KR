---
title: Compiling configurations in Azure Automation DSC | Microsoft Docs
description: "이 문서에서는 Azure Automation에 대한 DSC(필요한 상태 구성) 구성을 컴파일하는 방법을 설명합니다."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="11657-103">Azure 자동화 DSC에서 구성을 컴파일</span><span class="sxs-lookup"><span data-stu-id="11657-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="11657-104">Azure Automation를 사용하여 두 가지 방법인 Azure Portal 및 Windows PowerShell을 사용하여 DSC(필요한 상태 구성) 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="11657-105">다음 테이블에서는 각각의 특징을 기반으로 어떤 방법을 언제 사용할지 결정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="11657-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="11657-106">Azure portal</span></span>

* <span data-ttu-id="11657-107">대화형 사용자 인터페이스를 사용하는 간단한 방법</span><span class="sxs-lookup"><span data-stu-id="11657-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="11657-108">단순한 매개 변수 값을 제공하는 양식</span><span class="sxs-lookup"><span data-stu-id="11657-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="11657-109">작업 상태를 쉽게 추적</span><span class="sxs-lookup"><span data-stu-id="11657-109">Easily track job state</span></span>
* <span data-ttu-id="11657-110">Azure 로그온을 사용하여 액세스 인증</span><span class="sxs-lookup"><span data-stu-id="11657-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="11657-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="11657-111">Windows PowerShell</span></span>

* <span data-ttu-id="11657-112">Windows PowerShell cmdlet을 사용하여 명령줄에서 호출</span><span class="sxs-lookup"><span data-stu-id="11657-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="11657-113">여러 단계로 구성된 자동화된 솔루션에 포함할 수 있음</span><span class="sxs-lookup"><span data-stu-id="11657-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="11657-114">단순한 매개 변수 값 및 복잡한 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="11657-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="11657-115">작업 상태 추적</span><span class="sxs-lookup"><span data-stu-id="11657-115">Track job state</span></span>
* <span data-ttu-id="11657-116">클라이언트에서 PowerShell cmdlet을 지원해야 함</span><span class="sxs-lookup"><span data-stu-id="11657-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="11657-117">ConfigurationData 전달</span><span class="sxs-lookup"><span data-stu-id="11657-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="11657-118">자격 증명을 사용하는 구성을 컴파일</span><span class="sxs-lookup"><span data-stu-id="11657-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="11657-119">컴파일 방법을 결정했다면 컴파일을 시작하기 위해 아래의 해당 절차를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="11657-120">Azure 포털을 사용하여 DSC 구성 컴파일</span><span class="sxs-lookup"><span data-stu-id="11657-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="11657-121">Automation 계정에서 **DSC 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="11657-122">구성을 클릭하여 해당 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="11657-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="11657-123">**컴파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-123">Click **Compile**.</span></span>
4. <span data-ttu-id="11657-124">구성에 매개 변수가 없는 경우 컴파일할지 확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11657-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="11657-125">구성에 매개 변수가 있는 경우 **컴파일 구성** 블레이드를 열어 매개 변수 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="11657-126">매개 변수에 대한 자세한 내용은 아래의 [**기본 매개 변수**](#basic-parameters) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11657-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="11657-127">**컴파일 작업** 블레이드를 열어서 컴파일 작업의 상태 및 노드 구성(MOF 구성 문서)을 추적할 수 있습니다. Azure 자동화 DSC 끌어오기 서버에 배치되게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11657-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="11657-128">Windows PowerShell을 사용하여 DSC 구성을 컴파일</span><span class="sxs-lookup"><span data-stu-id="11657-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="11657-129">Windows PowerShell을 사용하여 컴파일하기 시작하는 데 [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="11657-130">다음 샘플 코드는 **SampleConfig**이라는 DSC 구성의 컴파일을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="11657-131">`Start-AzureRmAutomationDscCompilationJob` 는 해당 상태를 추적하는 데 사용할 수 있는 컴파일 작업 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="11657-132">[`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob)과 함께 이 컴파일 작업 개체를 사용하여 컴파일 작업의 상태를 확인하고 [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput)로 해당 스트림(출력)을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="11657-133">다음 샘플 코드는 **SampleConfig** 구성의 컴파일을 시작하고 완료될 때까지 대기한 다음 해당 스트림을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="11657-134">기본 매개 변수</span><span class="sxs-lookup"><span data-stu-id="11657-134">Basic Parameters</span></span>
<span data-ttu-id="11657-135">매개 변수 형식 및 속성을 포함하는 DSC 구성의 매개 변수 선언은 Azure 자동화 runbook과 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="11657-136">[Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md) 을 참조하여 runbook 매개 변수에 대한 자세한 내용을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11657-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="11657-137">다음 예제에서는 **FeatureName** 및 **IsPresent**라는 두 개의 매개 변수를 사용하여 **ParametersExample.sample** 노드 구에서 속성의 값을 결정하며 이는 컴파일하는 동안 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11657-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="11657-138">Azure 자동화 DSC 포털 또는 Azure PowerShell로 기본 매개 변수를 사용하는 DSC 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="11657-139">포털</span><span class="sxs-lookup"><span data-stu-id="11657-139">Portal</span></span>

<span data-ttu-id="11657-140">포털에서 **컴파일**을 클릭한 후에 매개 변수 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![대체 텍스트](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="11657-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11657-142">PowerShell</span></span>

<span data-ttu-id="11657-143">PowerShell은 키와 매개 변수 이름이 일치하고 매개 변수 값과 값이 같은 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) 에 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="11657-144">PSCredentials을 매개 변수로 전달하는 방법에 대한 정보는 아래의 <a href="#credential-assets">**자격 증명 자산**</a> 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11657-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="11657-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="11657-145">ConfigurationData</span></span>
<span data-ttu-id="11657-146">**ConfigurationData** 를 사용하면 PowerShell DSC를 사용하는 동안 환경의 특정 구성에서 구조적 구성을 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="11657-147">[PowerShell DSC의 "위치"에서 "대상" 분리](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) 를 참조하여 **ConfigurationData**에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11657-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="11657-148">Azure PowerShell을 사용하여 Azure 포털이 아닌 Azure 자동화 DSC에서 컴파일하는 경우 **ConfigurationData** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="11657-149">다음 예제 DSC 구성은 **$ConfigurationData** 및 **$AllNodes** 키워드를 통해 **ConfigurationData**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="11657-150">또한 다음과 같이 예를 들어 [**xWebAdministration** 모듈](https://www.powershellgallery.com/packages/xWebAdministration/)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="11657-151">PowerShell로 위의 DSC 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="11657-152">아래 PowerShell은 Azure 자동화 DSC 끌어오기 서버에 **ConfigurationDataSample.MyVM1** 및 **ConfigurationDataSample.MyVM3**과 같은 두 개의 노드 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="11657-153">자산</span><span class="sxs-lookup"><span data-stu-id="11657-153">Assets</span></span>

<span data-ttu-id="11657-154">자산 참조는 Azure 자동화 DSC 구성 및 runbook에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="11657-155">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11657-155">See the following for more information:</span></span>

* [<span data-ttu-id="11657-156">인증서</span><span class="sxs-lookup"><span data-stu-id="11657-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="11657-157">연결</span><span class="sxs-lookup"><span data-stu-id="11657-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="11657-158">자격 증명</span><span class="sxs-lookup"><span data-stu-id="11657-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="11657-159">변수</span><span class="sxs-lookup"><span data-stu-id="11657-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="11657-160">자격 증명 자산</span><span class="sxs-lookup"><span data-stu-id="11657-160">Credential Assets</span></span>

<span data-ttu-id="11657-161">Azure Automation에서 DSC 구성은 **Get-AzureRmAutomationCredential**을 사용하여 자격 증명 자산을 참조할 수 있지만 원하는 경우 자격 증명 자산은 매개 변수를 통해 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="11657-162">구성이 **PSCredential** 형식의 매개 변수를 사용하는 경우 PSCredential 개체가 아닌 Azure 자동화 자격 증명 자산의 문자열 이름을 해당 매개 변수 값으로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="11657-163">내부적으로 해당 이름을 가진 Azure 자동화 자격 증명 자산은 검색되고 구성에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="11657-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="11657-164">자격 증명을 노드 구성(MOF 구성 문서)에서 안전하게 유지하려면 노드 구성 MOF 파일에 자격 증명을 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="11657-165">Azure 자동화는 이 한 단계를 추가로 수행하고 전체 MOF 파일을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="11657-166">그러나 현재 PowerShell DSC가 노드 구성 MOF을 생성하는 동안 자격 증명을 일반 텍스트로 출력해도 되는지 알아야 합니다. PowerShell DSC은 Azure 자동화가 컴파일 작업을 통해 생성된 후에 전체 MOF 파일을 암호화한다는 것을 모르기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="11657-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="11657-167">PowerShell DSC가 [**ConfigurationData**](#configurationdata)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="11657-168">DSC 구성에 표시되고 자격 증명을 사용하는 각 노드 블록 이름의 경우 **ConfigurationData**를 통해 `PSDscAllowPlainTextPassword = $true`을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="11657-169">다음 예제에서는 자동화 자격 증명 자산을 사용하는 DSC 구성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="11657-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="11657-170">PowerShell로 위의 DSC 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="11657-171">아래 PowerShell은 Azure 자동화 DSC 끌어오기 서버에 **CredentialSample.MyVM1** 및 **CredentialSample.MyVM2**와 같은 두 개의 노드 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="11657-172">노드 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="11657-172">Importing node configurations</span></span>

<span data-ttu-id="11657-173">Azure 외부에서 컴파일한 노드 구성(MOF)을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="11657-174">이 경우 장점 중 하나는 노드 구성을 서명할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="11657-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="11657-175">서명된 노드 구성은 DSC 에이전트에 의해 관리되는 노드에서 로컬로 확인되어 인증된 출처에서 가져온 노드에 구성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="11657-176">서명된 구성을 Azure Automation 계정으로 가져오기를 사용할 수 있지만 Azure Automation에서는 현재 서명된 구성의 컴파일을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="11657-177">노드 구성 파일은 Azure Automation으로 가져오기 위해 1MB보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="11657-178">다음 위치에서 노드 구성을 서명하는 방법을 알아볼 수 있습니다. https://msdn.microsoft.com/ko-kr/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module</span><span class="sxs-lookup"><span data-stu-id="11657-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="11657-179">Azure Portal에서 노드 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="11657-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="11657-180">Automation 계정에서 **DSC 노드 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC 노드 구성](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="11657-182">**DSC 노드 구성** 블레이드에서 **노드 구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="11657-183">**가져오기** 블레이드에서 **노드 구성 파일** 텍스트 상자 옆의 폴더 아이콘을 클릭하여 로컬 컴퓨터에서 노드 구성 파일(MOF)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![로컬 파일 찾기](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="11657-185">**구성 이름** 텍스트 상자에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="11657-186">이 이름은 노드 구성이 컴파일된 구성 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="11657-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11657-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="11657-188">PowerShell을 사용하여 노드 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="11657-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="11657-189">[Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet을 사용하여 노드 구성을 Automation 계정으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11657-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



