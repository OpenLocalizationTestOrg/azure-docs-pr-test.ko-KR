---
title: "aaaPass JSON 개체 tooan Azure 자동화 runbook | Microsoft Docs"
description: "어떻게 JSON 개체로 toopass 매개 변수 tooa runbook"
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
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="b27be-104">JSON 개체 tooan Azure 자동화 runbook을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="b27be-105">JSON 파일에 toopass tooa runbook 유용한 toostore 데이터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="b27be-106">예를 들어 모든 hello 매개 변수를 포함 하는 JSON 파일을 만들 수 있습니다 toopass tooa runbook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="b27be-107">toodo이 tooconvert hello JSON tooa 문자열이 한 다음 해당 내용을 toohello runbook을 전달 하기 전에 hello 문자열 tooa PowerShell 개체를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="b27be-108">이 예제에서는 만들어 호출 하는 PowerShell 스크립트 [시작 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart PowerShell runbook hello JSON toohello runbook의 내용을 hello를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="b27be-109">hello PowerShell runbook hello에서 전달 된 JSON에서 hello VM hello 매개 변수를 가져와 Azure VM을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b27be-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b27be-110">Prerequisites</span></span>
<span data-ttu-id="b27be-111">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="b27be-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b27be-112">동작합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-112">Azure subscription.</span></span> <span data-ttu-id="b27be-113">계정이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 <a href="/pricing/free-account/" target="_blank">[무료 계정을 등록](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b27be-114">[자동화 계정](automation-sec-configure-azure-runas-account.md) toohold runbook hello 및 tooAzure 리소스를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="b27be-115">이 계정은 권한 toostart 있고 hello 가상 컴퓨터를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="b27be-116">Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="b27be-116">An Azure virtual machine.</span></span> <span data-ttu-id="b27be-117">프로덕션 VM이 되지 않도록 이 가상 컴퓨터를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="b27be-118">로컬 컴퓨터에 설치된 Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="b27be-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="b27be-119">참조 [설치 Azure Powershell을 구성 하 고](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) 방법에 대 한 정보에 대 한 Azure PowerShell tooget 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="b27be-120">Hello JSON 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="b27be-120">Create hello JSON file</span></span>

<span data-ttu-id="b27be-121">텍스트 파일에 테스트 하 고로 저장 하는 형식 hello 다음 `test.json` 로컬 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="b27be-122">Hello runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="b27be-122">Create hello runbook</span></span>

<span data-ttu-id="b27be-123">Azure Automation에서 "Test-Json"이라는 새 PowerShell Runbook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="b27be-124">toocreate 새 PowerShell runbook을 확인 하려면 어떻게 해야 toolearn [내 첫 번째 PowerShell runbook](automation-first-runbook-textual-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="b27be-125">tooaccept hello JSON 데이터를 hello runbook 입력된 매개 변수로 개체를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="b27be-126">hello runbook hello JSON에에서 정의 된 hello 속성을 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="b27be-127">이 Runbook을 Automation 계정에 저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="b27be-128">PowerShell에서 hello runbook을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="b27be-129">이제 Azure PowerShell을 사용 하 여 로컬 컴퓨터에서 hello runbook을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="b27be-130">Hello 다음 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="b27be-131">TooAzure 로그인:</span><span class="sxs-lookup"><span data-stu-id="b27be-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="b27be-132">하면 Azure 자격 증명 프롬프트 tooenter 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="b27be-133">Hello JSON 파일의 내용을 hello 가져오고 tooa 문자열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="b27be-134">`JsonPath`hello JSON 파일을 저장 하는 hello 경로가입니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="b27be-135">Hello 문자열 내용을 변환 `$json` tooa PowerShell 개체:</span><span class="sxs-lookup"><span data-stu-id="b27be-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="b27be-136">Hello 매개 변수에 대 한 hashtable을 만들 `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="b27be-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="b27be-137">Hello 값을 설정 하 고 있다는 것을 알 `Parameters` hello JSON 파일에서 hello 값이 포함 된 toohello PowerShell 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="b27be-138">Hello runbook 시작</span><span class="sxs-lookup"><span data-stu-id="b27be-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="b27be-139">hello runbook hello JSON 파일 toostart VM hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27be-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b27be-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b27be-140">Next steps</span></span>

* <span data-ttu-id="b27be-141">텍스트 편집기를 사용 하 여 PowerShell 및 PowerShell 워크플로 runbook 편집에 대 한 더 toolearn 참조 [Azure 자동화의 텍스트 runbook 편집](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="b27be-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="b27be-142">만들기 및 가져오기 runbook에 대해 자세히 toolearn 참조 [만들기 또는 Azure 자동화에서 runbook 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="b27be-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


