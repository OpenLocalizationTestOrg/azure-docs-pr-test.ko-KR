---
title: "Azure 자동화에서 aaaVariable 자산 | Microsoft Docs"
description: "변수 자산은 값을 사용할 수 있는 tooall runbook과 Azure 자동화에서 DSC 구성 합니다.  이 문서에서는 변수의 hello 세부 정보를 설명 및 방법을 텍스트와 그래픽 제작에 이러한 toowork 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Azure 자동화의 변수 자산

변수 자산은 값을 사용할 수 있는 tooall runbook과 자동화 계정에서 DSC 구성 합니다. 작성, 수정 및 내에서 그리고 hello Azure 포털, Windows PowerShell에서에서 검색 된 runbook 또는 DSC 구성 합니다. 자동화 변수는 hello 다음 시나리오에 유용 합니다.

- 여러 runbook 또는 DSC 구성 간에 값을 공유합니다.

- Hello의 여러 작업 간에 값을 공유 동일한 runbook 또는 DSC 구성 합니다.

- Hello 포털에서 또는 runbook 또는 VM 이름, 특정 리소스 그룹, AD 도메인 이름, 등의 특정 목록와 같은 일반적인 구성 항목 집합 등의 DSC 구성에서 사용 되는 hello Windows PowerShell 명령줄에서 값을 관리 합니다.  

자동화 변수는 hello runbook 또는 DSC 구성에 오류가 발생 해도 계속 toobe 사용할 수 있도록 유지 됩니다.  다른가 사용 되거나 hello에서 사용 되는 하나의 runbook에서 설정한 값 toobe 또한이 통해 동일한 runbook 또는 DSC 구성 hello 다음에 실행 됩니다.

변수를 만들 때 암호화된 상태로 저장되도록 지정할 수 있습니다.  변수가 암호화 되 Azure 자동화에 안전 하 게 저장 하 고 hello에서 해당 값을 검색할 수 없는 경우 [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) hello Azure PowerShell 모듈의 일부로 제공 되는 cmdlet입니다.  hello 암호화 된 값을 검색할 수 있는 유일한 방법은 hello에서 **Get-automationvariable** runbook 또는 DSC 구성에서 작업 합니다.

> [!NOTE]
> Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다. 이러한 자산 암호화 및 hello 각 자동화 계정에 대해 생성 되는 고유 키를 사용 하 여 Azure 자동화에에서 저장 됩니다. 이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다. 보안 자산을 저장 하기 전에 hello 자동화 계정에 대 한 hello 키 hello 마스터 인증서를 사용 하 여 암호가 해독 됩니다와 tooencrypt hello 자산을 사용 합니다.

## <a name="variable-types"></a>변수 형식

Azure 포털 hello로는 변수를 만들 때 hello 포털 hello hello 변수 값을 입력 하기 위한 적절 한 컨트롤을 표시할 수 있도록 hello 드롭 다운 목록에서 데이터 형식을 지정 해야 합니다. hello 변수가 없는 제한 된 toothis 데이터 형식에 변수를 설정 해야 hello toospecify 하려는 경우 Windows PowerShell을 사용 하 여 다른 종류의 값입니다. 지정 하는 경우 **정의 되어 있지**, hello hello 변수 값이 너무 설정 됩니다**$null**, hello로 hello 값을 설정 해야 하 고 [Set-azureautomationvariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet 또는 **Set-automationvariable** 활동입니다.  만들거나 hello hello 포털에서 복합 변수 형식의 값을 변경할 수 없습니다 되지만 Windows PowerShell을 사용 하 여 모든 형식의 값을 제공할 수 있습니다. 복잡한 형식은 [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx)로 반환됩니다.

배열이 나 해시 테이블을 만들고 toohello 변수를 저장 하 여 여러 값 tooa 단일 변수에 저장할 수 있습니다.

hello 다음은 자동화에서 사용할 수 있는 변수 유형의 목록입니다.

* 문자열
* Integer
* DateTime
* Boolean
* Null

## <a name="cmdlets-and-workflow-activities"></a>Cmdlet 및 워크플로 활동

다음 표에 hello의 hello cmdlet은 사용 되는 toocreate 하 고 Windows PowerShell을 사용 하 여 자동화 변수를 관리 합니다. Hello의 일부분으로 제공 [Azure PowerShell 모듈](../powershell-install-configure.md) 자동화 runbook 및 DSC 구성에서 사용 하기 위해 사용할 수 있습니다.

|Cmdlet|설명|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|기존 변수의 hello 값을 검색합니다.|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|새 변수를 만들고 해당 값을 설정합니다.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|기존 변수를 제거합니다.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|기존 변수의 hello 값을 설정합니다.|

다음 표에 hello에 hello 워크플로 활동에는 사용 되는 tooaccess runbook에서 자동화 변수입니다. Runbook 또는 DSC 구성에서 사용할 수 있고 hello Azure PowerShell 모듈의 일부로 제공 되지 않습니다.

|워크플로 활동|설명|
|:---|:---|
|Get-AutomationVariable|기존 변수의 hello 값을 검색합니다.|
|Set-AutomationVariable|기존 변수의 hello 값을 설정합니다.|

> [!NOTE] 
> 변수를 사용 하면 안 hello – Name 매개 변수에 **Get-automationvariable** runbook 또는 runbook 또는 DSC 구성 및 자동화 간의 종속성을 검색 하기가 어려워질 수 DSC 구성에서 디자인 타임에 변수입니다.

## <a name="creating-a-new-automation-variable"></a>새 자동화 변수 만들기

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate hello Azure 포털 사용 하 여 새 변수

1. 자동화 계정에서 클릭 hello **자산** 타일 hello에서 **자산** 블레이드를 **변수**합니다.
2. Hello에 **변수** 타일을 **변수 추가**합니다.
3. Hello 옵션 hello 대 완료 **새 변수** 블레이드에 대 한 클릭 **만들기** hello 새 변수에 저장 합니다.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 새 변수 toocreate

hello [새로 AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet은 새 변수를 만들고 해당 초기 값을 설정 합니다. 사용 하 여 hello 값을 검색할 수 있습니다 [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)합니다. 단순 형식의 hello 값은 같은 형식이 반환 됩니다. 복잡한 형식이면 **PSCustomObject**가 반환됩니다.

hello 다음 샘플 명령은 표시 방법을 toocreate 형식의 변수 문자열을 해당 값을 반환 합니다.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

hello 다음 샘플 명령은 표시 방법을 toocreate 복잡 한 변수에 입력 한 다음 해당 속성을 반환 합니다. 이 예제에서는 **Get-AzureRmVm**의 가상 컴퓨터 개체가 사용되었습니다.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>runbook 또는 DSC 구성에서 변수 사용

사용 하 여 hello **Set-automationvariable** 활동 tooset hello 변수 값을 자동화 runbook 또는 DSC 구성 및 hello **Get-automationvariable** tooretrieve 것입니다.  사용 하는 hello **Set-azureautomationvariable** 또는 **Get-azureautomationvariable** runbook 또는 DSC 구성 되므로 보다는 hello 워크플로 활동에서 cmdlet.  보안 변수 hello 값 검색할 수 없습니다 **Get-azureautomationvariable**합니다.  hello만 방법은 toocreate runbook 내에서 새 변수 또는 DSC 구성은 toouse hello [New-azureautomationvariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.


### <a name="textual-runbook-samples"></a>텍스트 Runbook 샘플

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>변수에서 단순한 값 설정 및 검색

hello 다음 샘플 명령은 표시 방법을 tooset 텍스트 runbook에서 변수를 검색 합니다. 이 예제에서는 *NumberOfIterations* 및 *NumberOfRunnings*라는 정수 형식의 변수와 *SampleMessage*라는 문자열 형식의 변수가 이미 만들어진 것으로 가정합니다.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>변수에서 복잡한 개체 설정 및 검색

hello 다음 샘플 코드에서 보여 주는 방법을 tooupdate 텍스트 runbook의 복잡 한 값이 있는 변수입니다. 이 샘플에서는 Azure 가상 컴퓨터를 검색 **Get-azurevm** 및 기존 자동화 변수에 저장 된 tooan 합니다.  [변수 형식](#variable-types)에 설명된 대로 이 변수는 PSCustomObject로 저장됩니다.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


코드 다음 hello, hello 값 hello 변수 및 사용 되는 toostart hello 가상 컴퓨터에서 검색 됩니다.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>변수에서 컬렉션 설정 및 검색

hello 다음 샘플 코드에서 보여 주는 방법을 toouse 텍스트 runbook에서 복합 값의 컬렉션을 사용 하 여 변수입니다. 이 샘플에서는 여러 Azure 가상 컴퓨터를 통해 검색 됩니다 **Get-azurevm** 및 기존 자동화 변수에 저장 된 tooan 합니다.  [변수 형식](#variable-types)에 설명된 대로 이 변수는 PSCustomObject 컬렉션으로 저장됩니다.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

코드 다음 hello, hello 컬렉션 hello 변수에서 검색 되 고 toostart 각 가상 컴퓨터를 사용 합니다.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>그래픽 Runbook 샘플

Hello 그래픽 runbook에서 추가 **Get-automationvariable** 또는 **Set-automationvariable** hello 변수 hello 그래픽 편집기의 hello 라이브러리 창에서 마우스 오른쪽 단추로 클릭 하 고 hello를 선택 하 여 원하는 작업입니다.

![변수 toocanvas 추가](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>변수에서 값 설정
hello 다음 이미지에서는 샘플 활동 tooupdate 단순 값으로 변수 그래픽 runbook입니다. 이 샘플에서는 단일 Azure 가상 컴퓨터를 검색 **Get AzureRmVM** hello 컴퓨터 이름을 문자열 형식을 가진 tooan 기존 자동화 변수에 저장 됩니다.  뿐 아니라 hello [링크는 파이프라인 또는 시퀀스](automation-graphical-authoring-intro.md#links-and-workflow) hello 출력에만 단일 개체를 기대 때문입니다.

![단순한 변수 설정](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>다음 단계

* 그래픽 제작에 활동을 함께 연결에 대해 자세히 toolearn 참조 [그래픽 제작에 대 한 링크](automation-graphical-authoring-intro.md#links-and-workflow)
* 그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md) 

