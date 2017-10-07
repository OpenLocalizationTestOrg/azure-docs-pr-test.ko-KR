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
# <a name="runbook-input-parameters"></a>Runbook 입력 매개 변수
Runbook 입력된 매개 변수는 시작 될 때 toopass 데이터 tooit를 허용 하 여 runbook의 hello 유연성을 높이고 합니다. hello 매개 변수는 특정 시나리오 및 환경에 대 한 대상으로 하는 hello runbook 작업 toobe를 사용 합니다. 이 문서에서는 입력 매개 변수가 사용되는 Runbook의 다양한 시나리오를 살펴보겠습니다.

## <a name="configure-input-parameters"></a>입력 매개 변수 구성
PowerShell, PowerShell 워크플로 및 그래픽 Runbook에서 입력 매개 변수를 구성할 수 있습니다. Runbook에는 여러 데이터 형식을 가진 여러 매개 변수가 있거나 매개 변수가 전혀 없을 수 있습니다. 입력 매개 변수는 필수 또는 선택일 수 있으므로 선택적 매개 변수에 대한 기본값을 할당할 수 있습니다. Hello 사용 가능한 방법 중 하나를 통해 시작할 때 runbook에 대 한 toohello 입력된 매개 변수 값을 할당할 수 있습니다. 이러한 방법 hello 포털 또는 웹 서비스에서 runbook 시작 포함 됩니다. 또한 다른 Runbook에서 인라인으로 호출되는 하위 Runbook으로 시작할 수 있습니다.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>PowerShell 및 PowerShell 워크플로 Runbook에서 입력 매개 변수 구성
PowerShell 및 [PowerShell 워크플로 runbook](automation-first-runbook-textual.md) Azure 자동화에서 hello 다음 특성을 통해 정의 된 입력된 매개 변수를 지원 합니다.  

| **속성** | **설명** |
|:--- |:--- |
| 형식 |필수입니다. hello 데이터 형식이 hello 매개 변수 값에 대 한 필요 합니다. 모든 .NET 형식이 유효합니다. |
| 이름 |필수입니다. hello hello 매개 변수의 이름입니다. 이 해야 hello runbook 내에서 고유 하 고 또는 포함 될 수 문자, 숫자, 밑줄 문자입니다. 문자로 시작해야 합니다. |
| 필수 |선택 사항입니다. Hello 매개 변수에 대 한 값을 제공 해야 하는지 여부를 지정 합니다. 설정한 경우이 너무**$true**, hello runbook이 시작 될 때 값을 제공 해야 합니다. 설정한 경우이 너무**$false**, 값은 선택 사항입니다. |
| 기본값 |선택 사항입니다.  Hello runbook을 시작 하는 값에서 전달 되지 않은 경우 hello 매개 변수에 사용할 수 있는 값을 지정 합니다. 기본값은 모든 매개 변수에 대해 설정할 수 있으며를 자동으로 hello 매개 변수 hello 필수 설정에 관계 없이 (옵션). |

Windows PowerShell은 유효성 검사, 별칭, 매개 변수 설정과 같이 여기에 나열된 것 보다 많은 입력 매개 변수의 특성을 지원합니다. 그러나 Azure 자동화에는 현재 hello 입력된 매개 변수만 위에 나열 된 지원 합니다.

PowerShell 워크플로 runbook에 매개 변수 정의 hello 다음 일반 형식의 여러 매개 변수는 쉼표로 구분 하는 위치에 있습니다.

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
> Hello를 지정 하지 않으면 매개 변수를 정의 하는 경우 **필수** 특성을 기본적으로 hello 매개 변수는 선택 사항으로 간주 합니다. 또한 PowerShell 워크플로 runbook의 매개 변수에 대해 기본값을 설정 하면 것으로 간주 되며 PowerShell에서 hello에 관계 없이 선택적 매개 변수 **필수** 특성 값입니다.
> 
> 

예를 들어 hello 가상 컴퓨터를 단일 VM 또는 리소스 그룹 내의 모든 Vm에 대 한 세부 정보를 출력 하는 PowerShell 워크플로 runbook에 대 한 입력된 매개 변수를 구성 해 보겠습니다. 이 runbook에 두 개의 매개 변수는 hello 스크린 샷 뒤에 표시 된 대로: hello 리소스 그룹의 hello 이름과 가상 컴퓨터의 hello 이름입니다.

![자동화 PowerShell 워크플로](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

이 매개 변수 정의에서 매개 변수를 hello **$VMName** 및 **$resourceGroupName** 는 string 형식의 단순 매개 변수입니다. 그러나 PowerShell 및 PowerShell 워크플로 Runbook은 입력 매개 변수에 대해 **개체** 또는 **PSCredential**과 같은 단순 형식 및 복합 형식을 모두 지원합니다.

Runbook에는 개체 유형 입력된 매개 경우 다음 PowerShell 해시 테이블 (이름, 값)를 사용 하 여 toopass 값에서 쌍입니다. 예를 들어, hello 매개 변수는 runbook에서 다음 있는 경우:

     [Parameter (Mandatory = $true)]
     [object] $FullName

다음 값 toohello 매개 변수 다음 hello를 전달할 수 있습니다.

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>그래픽 Runbook에서 입력 매개 변수 구성
너무[그래픽 runbook 구성](automation-first-runbook-graphical.md) 입력된 매개 변수가 있는 만들겠습니다 그래픽 runbook 하거나 가상 컴퓨터에 대 한 세부 정보를 출력 하는 단일 VM 또는 리소스 그룹 내의 모든 Vm입니다. 아래 설명한 대로 Runbook이 두 가지 주요 작업으로 이루어지도록 구성합니다.

[**Azure 실행 계정으로 Runbook 인증** ](automation-sec-configure-azure-runas-account.md) azure tooauthenticate 합니다.

[**Get AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) 가상 컴퓨터의 tooget hello 속성입니다.

Hello를 사용할 수 있습니다 [ **Write-output** ](https://technet.microsoft.com/library/hh849921.aspx) 가상 컴퓨터의 활동 toooutput hello 이름입니다. 활동 hello **Get AzureRmVm** 두 개의 매개 변수를 받고 hello **가상 컴퓨터 이름** 및 hello **리소스 그룹 이름은**합니다. 이러한 매개 변수 값이 다른 hello runbook을 시작할 때 필요할 수, 이후 tooyour runbook 입력된 매개 변수를 추가할 수 있습니다. Hello 단계 tooadd 입력된 매개 변수는 다음과 같습니다.

1. 선택 hello hello에서 그래픽 runbook **Runbook** 블레이드에 대 한 클릭 [ **편집** ](automation-graphical-authoring-intro.md) 것입니다.
2. Hello runbook 편집기에서 클릭 **입력 및 출력** tooopen hello **입력 및 출력** 블레이드입니다.
   
    ![자동화 그래픽 Runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. hello **입력 및 출력** 블레이드 hello runbook에 대해 정의 된 입력된 매개 변수 목록이 표시 됩니다. 이 블레이드를 새 입력된 매개 변수를 추가 하거나 기존 입력된 매개 변수의 hello 구성을 편집 합니다. tooadd hello runbook에 대 한 새 매개 변수를 클릭 **입력 추가** tooopen hello **Runbook 입력된 매개 변수** 블레이드입니다. 여기에 매개 변수 뒤 hello를 구성할 수 있습니다.
   
   | **속성** | **설명** |
   |:--- |:--- |
   | 이름 |필수입니다.  hello hello 매개 변수의 이름입니다. 이 해야 hello runbook 내에서 고유 하 고 또는 포함 될 수 문자, 숫자, 밑줄 문자입니다. 문자로 시작해야 합니다. |
   | 설명 |선택 사항입니다. 입력된 매개 변수의 hello 용도 대 한 설명입니다. |
   | 형식 |선택 사항입니다. hello 매개 변수 값에 대 한 예상 되는 hello 데이터 형식입니다. 지원되는 매개 변수 형식은 **문자열**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** 및 **개체**입니다. 데이터 형식을 선택 하지 않으면 기본값 너무**문자열**합니다. |
   | 필수 |선택 사항입니다. Hello 매개 변수에 대 한 값을 제공 해야 하는지 여부를 지정 합니다. 선택 하면 **예**, hello runbook이 시작 될 때 값을 제공 해야 합니다. 선택 하면 **없습니다**, hello runbook을 시작 하 고 기본값을 설정할 수 있습니다 때 값이 필요 합니다. |
   | 기본값 |선택 사항입니다. Hello runbook을 시작 하는 값에서 전달 되지 않은 경우 hello 매개 변수에 사용할 수 있는 값을 지정 합니다. 필수가 아닌 매개 변수에 기본값을 설정할 수 있습니다. 기본 값, tooset 선택 **사용자 지정**합니다. Hello runbook이 시작 될 때 다른 값을 제공 하지 않으면이 값이 사용 됩니다. 선택 **None** tooprovide 않으려는 경우 모든 기본 값입니다. |
   
    ![새 입력 추가](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. 다음과 같은 hello에서 사용할 속성 hello로 두 개의 매개 변수를 만들 **Get AzureRmVm** 활동:
   
   * **매개 변수 1:**
     
     * 이름 - VMName
     * 형식 - String
     * 필수 - 없음
   * **매개 변수 2:**
     
     * 이름 - resourceGroupName
     * 형식 - String
     * 필수 - 없음
     * 기본값 - 사용자 지정
     * 사용자 지정 기본 값- \<hello 가상 컴퓨터를 포함 하는 hello 리소스 그룹의 이름 >
5. Hello 매개 변수를 추가한 후 클릭 **확인**합니다.  Hello에 이제 볼 수 **입력 및 출력 블레이드**합니다. 다시 **확인**을 클릭한 다음 Runbook을 **저장**하고 **게시**하도록 클릭합니다.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Runbook에서 tooinput 매개 변수 값 할당
다음 시나리오는 hello의 runbook에서 값 tooinput 매개 변수를 전달할 수 있습니다.

### <a name="start-a-runbook-and-assign-parameters"></a>Runbook 시작 및 매개 변수 할당
Runbook에 여러 가지 방법으로 시작할 수 있습니다: hello 여 webhook을 사용할지, PowerShell cmdlet을 통해, hello REST API 또는 hello SDK로 Azure 포털을 통해. 아래에서는 Runbook을 시작하고 매개 변수를 할당하는 여러 가지 방법을 설명합니다.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Hello Azure 포털을 사용 하 여 게시 된 runbook을 시작 하 고 매개 변수 지정
때 있습니다 [hello runbook을 시작](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Runbook 시작** 블레이드가 열리고 방금 만든 hello 매개 변수 값을 구성할 수 있습니다.

![Hello 포털을 사용 하 여 시작](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Hello 입력된 상자 아래 hello 레이블에서 hello 매개 변수에 대해 설정 된 hello 특성을 볼 수 있습니다. 특성은 필수 또는 선택적, 형식 및 기본값을 포함합니다. Hello 도움말 풍선 다음 toohello 매개 변수 이름, 매개 변수 입력된 값에 대 한 toomake 결정 필요한 모든 hello 키 정보를 볼 수 있습니다. 이 정보는 매개 변수가 필수 또는 선택인지를 포함합니다. Hello 형식 및 기본값 (있는 경우), 및 기타 유용한 정보에도 포함 됩니다.

![도움말 풍선](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> 문자열 형식 매개 변수는 **빈** 문자열 값을 지원합니다.  입력 **[EmptyString]** hello 입력된 매개 변수 상자는 빈 문자열 toohello 매개 변수를 전달 합니다. 또한 문자열 형식 매개 변수는 전달되는 **Null** 값을 지원하지 않습니다. 모든 값 toohello 문자열 매개 변수를 전달 하지 않으면, 다음 PowerShell 변환 합니다. null로 합니다.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>PowerShell cmdlet을 사용하여 게시된 Runbook 시작 및 매개 변수 할당
* **Azure Resource Manager cmdlet:**[Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)을 사용하여 리소스 그룹에 생성된 자동화 Runbook을 시작할 수 있습니다
  
  **예제:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Azure 서비스 관리 cmdlet:**[Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)을 사용하여 기본 리소스 그룹에 생성된 자동화 Runbook을 시작할 수 있습니다
  
  **예제:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> PowerShell cmdlet, 기본 매개 변수를 사용 하 여 runbook을 시작할 때 **MicrosoftApplicationManagementStartedBy** hello 값을 사용 하 여 만든 **PowerShell**합니다. Hello에이 매개 변수를 볼 수 있습니다 **작업 정보** 블레이드입니다.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>SDK를 사용하여 Runbook 시작 및 매개 변수 할당
* **Azure 리소스 관리자 메서드:** hello 프로그래밍 언어의 SDK를 사용 하 여 runbook을 시작할 수 있습니다. 다음은 자동화 계정의 Runbook을 시작하기 위한 C# 코드 조각입니다. 모든 hello 코드를 볼 수는 [GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)합니다.  
  
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
* **Azure 서비스 관리 방법:** hello 프로그래밍 언어의 SDK를 사용 하 여 runbook을 시작할 수 있습니다. 다음은 자동화 계정의 Runbook을 시작하기 위한 C# 코드 조각입니다. 모든 hello 코드를 볼 수는 [GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)합니다.
  
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
  
  toostart이이 방법에서는 사전 toostore hello runbook 매개 변수를 만들고 **VMName** 및 **resourceGroupName**, 및 해당 값입니다. Hello runbook을 시작 합니다. 다음은 위에 정의 된 hello 메서드를 호출 하는 것에 대 한 hello C# 코드 조각입니다.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Hello REST API를 사용 하 여 runbook을 시작 하 고 매개 변수를 할당 합니다.
Runbook 작업을 만든 hello를 사용 하 여 Azure 자동화 REST API hello로 시작 하 고 **배치** 다음 hello로 메서드 요청 URI입니다.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Hello 요청 URI에서에서 hello를 매개 변수를 다음 코드로 바꿉니다.

* **subscription-id:** Azure 구독 ID입니다.  
* **클라우드 서비스 이름:** hello 클라우드 서비스 toowhich hello 요청의 hello 이름을 전송 합니다.  
* **자동화 계정 이름:** hello 내에서 호스팅되는 자동화 계정 hello 이름은 클라우드 서비스를 지정 합니다.  
* **작업 id:** hello 작업에 대 한 GUID를 hello 합니다. Hello를 사용 하 여 PowerShell에서 Guid를 만들 수 있습니다 **[GUID]::NewGuid() 합니다. Tostring ()** 명령입니다.

순서 toopass 매개 변수 toohello runbook 작업을 hello 요청 본문을 사용 합니다. 다음 JSON 형식으로 제공 하는 두 개의 속성이 hello를 사용 합니다.

* **Runbook 이름:** 필수입니다. hello runbook의 이름 hello 작업 toostart hello입니다.  
* **Runbook 매개 변수:** 선택 사항입니다. Hello 매개 변수 목록 (이름, 값)에서 사전 이름 문자열 형식 이어야 하 고 유효한 모든 JSON 값 값일 수 있는 서식을 지정 합니다.

Toostart hello를 원하는 경우 **Get AzureVMTextual** 와 이전 작성 된 runbook **VMName** 및 **resourceGroupName** 를 매개 변수로 사용 하 여 JSON 형식에 따라 hello 에 대 한 hello 요청 본문입니다.

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

HTTP 상태 코드 201 hello 작업이 올바르게 만들어진 경우에 반환 됩니다. 응답 헤더 및 hello 응답 본문에 대 한 자세한 내용은 참조는 방법에 대 한 toohello 문서 너무[hello REST API를 사용 하 여 runbook 작업을 만듭니다.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Runbook 테스트 및 매개 변수 할당
때 있습니다 [runbook의 테스트 hello 초안 버전](automation-testing-runbook.md) hello 테스트 옵션을 사용 하 여 hello **테스트** 블레이드가 열리고 방금 만든 hello 매개 변수 값을 구성할 수 있습니다.

![매개 변수 테스트 및 할당](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>일정 tooa runbook을 연결 하 고 매개 변수를 할당 합니다.
할 수 있습니다 [일정 연결](automation-schedules.md) tooyour runbook 해당 hello runbook이 특정 시간에 시작 되도록 합니다. Hello 일정을 만들고 hello runbook는 hello 일정에 의해 시작 될 때 이러한 값을 사용 하는 경우에 입력된 매개 변수를 할당 합니다. 모든 필수 매개 변수 값이 제공 되어야만 hello 일정을 저장할 수 없습니다.

![매개 변수 예약 및 할당](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Runbook에 대한 webhook 만들기 및 매개 변수 할당
Runbook에 대한 [webhook](automation-webhooks.md) 을 만들고 Runbook 입력 매개 변수를 구성할 수 있습니다. 모든 필수 매개 변수 값이 제공 되어야만 hello webhook을 저장할 수 없습니다.

![Webhook 만들기 및 매개 변수 할당](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

미리 정의 된 입력된 매개 변수 hello 여 webhook을 사용할지를 사용 하 여 runbook을 실행할 때 ** [Webhookdata](automation-webhooks.md#details-of-a-webhook) ** 정의한 hello 입력된 매개 변수와 함께 전송 됩니다. 클릭할 수 있는 tooexpand hello **WebhookData** 자세한 내용은 매개 변수입니다.

![WebhookData 매개 변수](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>다음 단계
* Runbook 입력 및 출력에 대한 자세한 내용은 [Azure 자동화: Runbook 입력, 출력 및 중첩된 Runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)을 참조하세요.
* 다양 한 방법 toostart runbook에 대 한 세부 정보를 참조 하십시오. [runbook 시작](automation-starting-a-runbook.md)합니다.
* 텍스트 runbook tooedit 너무 참조[텍스트 runbook 편집](automation-edit-textual-runbook.md)합니다.
* 그래픽 runbook tooedit 너무 참조[Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.

