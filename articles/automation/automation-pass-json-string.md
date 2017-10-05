---
title: "Azure Automation Runbook에 JSON 개체 전달 | Microsoft Docs"
description: "Runbook에 매개 변수를 JSON 개체로 전달하는 방법"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell,  runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="00adb-104">Azure Automation Runbook에 JSON 개체 전달</span><span class="sxs-lookup"><span data-stu-id="00adb-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="00adb-105">JSON 파일에서 Runbook에 전달하려는 데이터를 저장하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="00adb-106">예를 들어 Runbook에 전달하려는 모든 매개 변수가 포함된 JSON 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="00adb-107">이렇게 하려면 JSON을 문자열로 변환한 다음 해당 문자열을 PowerShell 개체로 변환한 후에 해당 내용을 Runbook에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="00adb-108">이 예제에서는 [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)을 호출하여 PowerShell Runbook을 시작하고 JSON의 내용을 Runbook에 전달하는 PowerShell 스크립트를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="00adb-109">PowerShell Runbook은 Azure VM을 시작하고 전달된 JSON에서 VM에 대한 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00adb-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00adb-110">Prerequisites</span></span>
<span data-ttu-id="00adb-111">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="00adb-112">동작합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-112">Azure subscription.</span></span> <span data-ttu-id="00adb-113">계정이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 <a href="/pricing/free-account/" target="_blank">[무료 계정을 등록](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="00adb-114">[자동화 계정](automation-sec-configure-azure-runas-account.md) .</span><span class="sxs-lookup"><span data-stu-id="00adb-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="00adb-115">이 계정은 가상 컴퓨터를 시작하고 중지할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="00adb-116">Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="00adb-116">An Azure virtual machine.</span></span> <span data-ttu-id="00adb-117">프로덕션 VM이 되지 않도록 이 가상 컴퓨터를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="00adb-118">로컬 컴퓨터에 설치된 Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="00adb-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="00adb-119">Azure PowerShell을 얻는 방법에 대한 자세한 내용은 [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)(Azure Powershell 설치 및 구성)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00adb-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="00adb-120">JSON 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="00adb-120">Create the JSON file</span></span>

<span data-ttu-id="00adb-121">텍스트 파일에 다음 테스트를 입력하고 로컬 컴퓨터의 특정 위치에 `test.json`으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="00adb-122">Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="00adb-122">Create the runbook</span></span>

<span data-ttu-id="00adb-123">Azure Automation에서 "Test-Json"이라는 새 PowerShell Runbook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="00adb-124">새 PowerShell Runbook을 만드는 방법을 알아보려면 [내 첫 번째 PowerShell Runbook](automation-first-runbook-textual-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00adb-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="00adb-125">JSON 데이터를 허용하려면 Runbook에서 개체를 입력 매개 변수로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="00adb-126">그러면 Runbook에서 JSON에 정의된 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="00adb-127">이 Runbook을 Automation 계정에 저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="00adb-128">PowerShell에서 Runbook 호출</span><span class="sxs-lookup"><span data-stu-id="00adb-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="00adb-129">이제 로컬 컴퓨터에서 Azure PowerShell을 사용하여 Runbook을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="00adb-130">다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="00adb-131">Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="00adb-132">Azure 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="00adb-133">JSON 파일의 내용을 가져와 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="00adb-134">`JsonPath`는 JSON 파일을 저장한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="00adb-135">`$json`의 문자열 내용을 PowerShell 개체로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="00adb-136">`Start-AzureRmAutomstionRunbook`의 매개 변수에 대한 해시 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="00adb-137">`Parameters`의 값을 JSON 파일의 값이 포함된 PowerShell 개체로 설정하고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="00adb-138">Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="00adb-139">Runbook에서 JSON 파일의 값을 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00adb-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00adb-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00adb-140">Next steps</span></span>

* <span data-ttu-id="00adb-141">텍스트 편집기를 사용하여 PowerShell 및 PowerShell 워크플로 Runbook을 편집하는 방법을 알아보려면 [Azure 자동화에서 텍스트 Runbook 편집](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="00adb-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="00adb-142">Runbook을 만들고 가져오는 방법을 알아보려면 [Azure Automation에서 Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00adb-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


