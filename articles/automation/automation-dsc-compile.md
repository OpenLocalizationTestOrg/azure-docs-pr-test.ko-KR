---
title: "Azure 자동화 DSC의 aaaCompiling 구성 | Microsoft Docs"
description: "이 문서에서는 설명 방식을 Azure 자동화에 대 한 toocompile 구성 DSC (필요한 상태) 구성 합니다."
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
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="3c710-103">Azure 자동화 DSC에서 구성을 컴파일</span><span class="sxs-lookup"><span data-stu-id="3c710-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="3c710-104">두 가지 방법으로 Azure 자동화 원하는 상태 구성 (DSC) 구성을 컴파일할 수 있습니다: hello Azure 포털에서에서 및 Windows PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="3c710-105">hello 다음 표를 참조 시기를 결정 하 toouse 각 hello 특징을 기반으로 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="3c710-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3c710-106">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3c710-106">Azure portal</span></span>

* <span data-ttu-id="3c710-107">대화형 사용자 인터페이스를 사용하는 간단한 방법</span><span class="sxs-lookup"><span data-stu-id="3c710-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="3c710-108">양식 tooprovide 간단한 매개 변수 값</span><span class="sxs-lookup"><span data-stu-id="3c710-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="3c710-109">작업 상태를 쉽게 추적</span><span class="sxs-lookup"><span data-stu-id="3c710-109">Easily track job state</span></span>
* <span data-ttu-id="3c710-110">Azure 로그온을 사용하여 액세스 인증</span><span class="sxs-lookup"><span data-stu-id="3c710-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="3c710-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c710-111">Windows PowerShell</span></span>

* <span data-ttu-id="3c710-112">Windows PowerShell cmdlet을 사용하여 명령줄에서 호출</span><span class="sxs-lookup"><span data-stu-id="3c710-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="3c710-113">여러 단계로 구성된 자동화된 솔루션에 포함할 수 있음</span><span class="sxs-lookup"><span data-stu-id="3c710-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="3c710-114">단순한 매개 변수 값 및 복잡한 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="3c710-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="3c710-115">작업 상태 추적</span><span class="sxs-lookup"><span data-stu-id="3c710-115">Track job state</span></span>
* <span data-ttu-id="3c710-116">필요한 클라이언트 toosupport PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="3c710-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="3c710-117">ConfigurationData 전달</span><span class="sxs-lookup"><span data-stu-id="3c710-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="3c710-118">자격 증명을 사용하는 구성을 컴파일</span><span class="sxs-lookup"><span data-stu-id="3c710-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="3c710-119">컴파일 메서드에 결정 했으면, toostart 컴파일 아래 hello 해당 절차를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="3c710-120">Azure 포털 hello로 DSC 구성 컴파일</span><span class="sxs-lookup"><span data-stu-id="3c710-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="3c710-121">Automation 계정에서 **DSC 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="3c710-122">구성 tooopen 해당 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="3c710-123">**컴파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-123">Click **Compile**.</span></span>
4. <span data-ttu-id="3c710-124">Toocompile 할지 여부 증명된 tooconfirm hello 구성 매개 변수가 없는 경우, 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="3c710-125">Hello 구성 매개 변수가 있으면 hello **구성 컴파일** 매개 변수 값을 제공할 수 있도록 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="3c710-126">Hello 참조 [ **기본 매개 변수** ](#basic-parameters) 매개 변수에 대 한 자세한 내용은 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="3c710-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="3c710-127">hello **컴파일 작업** hello 노드 구성 (구성 MOF 문서)를 유발 하기 toobe hello Azure 자동화 DSC 끌어오기 서버에 배치 하 고 hello 컴파일 작업의 상태를 추적할 수 있도록 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="3c710-128">Windows PowerShell을 사용하여 DSC 구성을 컴파일</span><span class="sxs-lookup"><span data-stu-id="3c710-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="3c710-129">사용할 수 있습니다 [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart Windows PowerShell을 사용 하 여 컴파일할 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="3c710-130">다음 샘플 코드는 hello 이라고 하는 DSC 구성의 컴파일을 시작 **SampleConfig**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="3c710-131">`Start-AzureRmAutomationDscCompilationJob`컴파일 반환 작업 개체를 사용할 수 있는 tootrack 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="3c710-132">이 컴파일 작업 개체를 사용할 수 있습니다 [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) hello 컴파일 작업의 toodetermine hello 상태 및 [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview 해당 스트림 (output).</span><span class="sxs-lookup"><span data-stu-id="3c710-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="3c710-133">다음 샘플 코드는 hello hello의 컴파일을 시작 **SampleConfig** 구성, 완료 된 후 해당 스트림을 표시 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="3c710-134">기본 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3c710-134">Basic Parameters</span></span>
<span data-ttu-id="3c710-135">매개 변수 형식 및 속성을 작동을 비롯 한 DSC 구성에서 매개 변수 선언 Azure 자동화 runbook에서와 같이 동일한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="3c710-136">참조 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md) toolearn runbook 매개 변수에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="3c710-137">hello 다음 예제에서는 라는 두 개의 매개 변수가 **FeatureName** 및 **IsPresent**, toodetermine hello 속성 값에 hello **ParametersExample.sample** 노드 구성 컴파일 중에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="3c710-138">기본 매개 변수를 사용 하 여 hello Azure 자동화 DSC 포털에서 또는 Azure PowerShell을 사용 하는 DSC 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="3c710-139">포털</span><span class="sxs-lookup"><span data-stu-id="3c710-139">Portal</span></span>

<span data-ttu-id="3c710-140">Hello 포털에서 입력할 수 있는 매개 변수 값을 클릭 한 후 **컴파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![대체 텍스트](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="3c710-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c710-142">PowerShell</span></span>

<span data-ttu-id="3c710-143">PowerShell에서 매개 변수를 필요는 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) 여기서 hello 키는 hello 매개 변수 이름과 일치 하 고 hello 매개 변수 값과 같은 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="3c710-144">PSCredentials을 매개 변수로 전달하는 방법에 대한 정보는 아래의 <a href="#credential-assets">**자격 증명 자산**</a> 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c710-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="3c710-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="3c710-145">ConfigurationData</span></span>
<span data-ttu-id="3c710-146">**ConfigurationData** PowerShell DSC를 사용 하는 동안 모든 환경 특정 구성에서 구조적 구성 tooseparate 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="3c710-147">참조 [PowerShell DSC에 있는 "Where"에서 "작업" 분리](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn에 대 한 자세한 **ConfigurationData**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="3c710-148">사용할 수 있습니다 **ConfigurationData** hello Azure 포털 있지만 Azure PowerShell을 사용 하 여 Azure 자동화 DSC에 컴파일할 때.</span><span class="sxs-lookup"><span data-stu-id="3c710-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="3c710-149">hello 다음 예제에서는 DSC 구성을 사용 하 여 **ConfigurationData** hello를 통해 **$ConfigurationData** 및 **$AllNodes** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="3c710-150">또한 hello 해야 [ **xWebAdministration** 모듈](https://www.powershellgallery.com/packages/xWebAdministration/) 이 예제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="3c710-151">PowerShell 사용한 위의 hello DSC 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="3c710-152">두 개의 노드 구성을 toohello Azure 자동화 DSC 끌어오기 서버를 추가 하는 PowerShell 아래의 hello: **ConfigurationDataSample.MyVM1** 및 **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="3c710-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="3c710-153">자산</span><span class="sxs-lookup"><span data-stu-id="3c710-153">Assets</span></span>

<span data-ttu-id="3c710-154">자산 참조의 경우 Azure 자동화 DSC 구성 및 runbook 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="3c710-155">Hello 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c710-155">See hello following for more information:</span></span>

* [<span data-ttu-id="3c710-156">인증서</span><span class="sxs-lookup"><span data-stu-id="3c710-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="3c710-157">연결</span><span class="sxs-lookup"><span data-stu-id="3c710-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="3c710-158">자격 증명</span><span class="sxs-lookup"><span data-stu-id="3c710-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="3c710-159">변수</span><span class="sxs-lookup"><span data-stu-id="3c710-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="3c710-160">자격 증명 자산</span><span class="sxs-lookup"><span data-stu-id="3c710-160">Credential Assets</span></span>

<span data-ttu-id="3c710-161">Azure Automation에서 DSC 구성은 **Get-AzureRmAutomationCredential**을 사용하여 자격 증명 자산을 참조할 수 있지만 원하는 경우 자격 증명 자산은 매개 변수를 통해 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="3c710-162">구성 매개 변수를 사용 하는 경우 **PSCredential** 형식, PSCredential 개체를 사용 하지 않고 해당 매개 변수의 값은 Azure 자동화 자격 증명 자산의 toopass hello 문자열 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="3c710-163">Hello 백그라운드 해당 이름의 hello Azure 자동화 자격 증명 자산 검색 하 고 toohello 구성을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="3c710-164">자격 증명을 유지 노드 구성 (구성 MOF 문서)에서 보안 필요 hello 노드 구성 MOF 파일에 hello 자격 증명을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="3c710-165">Azure 자동화는이 한 단계를 더 이상 사용 하 고 hello 전체 MOF 파일을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="3c710-166">그러나 현재 알려야 PowerShell DSC 괜찮습니다 자격 증명 toobe 노드 구성 MOF 생성 하는 동안 일반 텍스트로 출력에 대 한 PowerShell DSC Azure 자동화 후 hello 전체 MOF 파일 암호화 될 알 없기 때문 해당 컴파일 작업을 통해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="3c710-167">생성 된 hello 노드 구성 Mof에에서 일반 텍스트로 출력 하는 자격 증명 toobe 두어도 되는 PowerShell DSC 알 수 있습니다를 사용 하 여 [ **ConfigurationData**](#configurationdata)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="3c710-168">전달 해야 `PSDscAllowPlainTextPassword = $true` 통해 **ConfigurationData** hello DSC 구성에 표시 되 고 자격 증명을 사용 하는 각 노드 블록의 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="3c710-169">hello 다음 예제에서는 자동화 자격 증명 자산을 사용 하는 DSC 구성</span><span class="sxs-lookup"><span data-stu-id="3c710-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="3c710-170">PowerShell 사용한 위의 hello DSC 구성을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="3c710-171">두 개의 노드 구성을 toohello Azure 자동화 DSC 끌어오기 서버를 추가 하는 PowerShell 아래의 hello: **CredentialSample.MyVM1** 및 **CredentialSample.MyVM2**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="3c710-172">노드 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="3c710-172">Importing node configurations</span></span>

<span data-ttu-id="3c710-173">Azure 외부에서 컴파일한 노드 구성(MOF)을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="3c710-174">이 경우 장점 중 하나는 노드 구성을 서명할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="3c710-175">서명 된 노드 구성 적용된 toohello 노드 되 고 해당 hello 구성 인증된 된 출처에서 제공 되었는지 확인 하는 hello DSC 에이전트에 의해 관리 되는 노드에서 로컬로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="3c710-176">서명된 구성을 Azure Automation 계정으로 가져오기를 사용할 수 있지만 Azure Automation에서는 현재 서명된 구성의 컴파일을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="3c710-177">노드 구성 파일을 1MB tooallow 보다 작은 해야 것 Azure 자동화에 가져와서 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="3c710-178">학습할 수 있는 방법을 toosign 노드 구성을 https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="3c710-179">Hello Azure 포털에서에서 노드 구성을 가져오기</span><span class="sxs-lookup"><span data-stu-id="3c710-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="3c710-180">Automation 계정에서 **DSC 노드 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC 노드 구성](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="3c710-182">Hello에 **DSC 노드 구성을** 블레이드에서 클릭 **는 NodeConfiguration 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="3c710-183">Hello에 **가져오기** 블레이드에서 hello 폴더 아이콘 다음 toohello 클릭 **노드 구성 파일** 로컬 컴퓨터에는 노드 구성 파일 (MOF)에 대 한 textbox toobrowse 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![로컬 파일 찾기](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="3c710-185">Hello에 이름을 입력 **구성 이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="3c710-186">이 이름은 hello 노드 구성을 컴파일한 hello 구성의 hello 이름을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="3c710-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="3c710-188">PowerShell을 사용하여 노드 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="3c710-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="3c710-189">Hello를 사용할 수 있습니다 [가져오기 AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport 자동화 계정으로 노드 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c710-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



