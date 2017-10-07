---
title: "aaaStarting 및 가상 컴퓨터를 중지 하는 중-그래프 | Microsoft Docs"
description: "Runbook 중지 및 toostart 클래식 가상 컴퓨터를 포함 하 여 Azure 자동화 시나리오의 PowerShell 워크플로 버전입니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Azure 자동화 시나리오 - 가상 컴퓨터 시작 및 중지
이 Azure 자동화 시나리오 runbook toostart 및 중지 클래식 가상 컴퓨터를 포함합니다.  Hello 다음 중 하나에 대 한이 시나리오를 사용할 수 있습니다.  

* 사용자 환경에 수정 하지 않고 runbook을 hello를 사용 합니다.
* Hello runbook tooperform 사용자 지정 기능을 수정 합니다.  
* 전체 솔루션의 일부로 다른 runbook에서 hello runbook을 호출 합니다.
* 자습서 toolearn runbook 제작 개념으로 hello runbook을 사용 합니다.

> [!div class="op_single_selector"]
> * [그래픽](automation-solution-startstopvm-graphical.md)
> * [PowerShell 워크플로](automation-solution-startstopvm-psworkflow.md)
>
>

이 시나리오의 hello 그래픽 runbook 버전입니다. [PowerShell 워크플로 Runbook](automation-solution-startstopvm-psworkflow.md)을 사용하여 사용할 수도 있습니다.

## <a name="getting-hello-scenario"></a>Hello 시나리오를 가져오기
이 시나리오는 두 개의 이루어져 다음 링크에서 다운로드할 수 있는 두 가지 그래픽 runbook hello 합니다.  Hello 참조 [PowerShell 워크플로 버전](automation-solution-startstopvm-psworkflow.md) 링크 toohello PowerShell 워크플로 runbook에 대 한이 시나리오의 합니다.

| Runbook | 링크 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Azure 클래식 VM 그래픽 Runbook 시작](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |그래픽 |Azure 구독의 모든 기존 가상 컴퓨터 또는 특정 서비스의 모든 가상 컴퓨터를 시작합니다. |
| StopAzureClassicVM |[Azure 클래식 VM 그래픽 Runbook 중지](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |그래픽 |자동화 계정의 모든 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 중지합니다. |

## <a name="installing-and-configuring-hello-scenario"></a>설치 하 고 hello 시나리오를 구성 합니다.
### <a name="1-install-hello-runbooks"></a>1. Hello runbook을 설치 합니다.
Hello runbook에 다운로드 한 후에 가져올 수의 hello 절차를 사용 하 여 [그래픽 runbook 프로시저](automation-graphical-authoring-intro.md#graphical-runbook-procedures)합니다.

### <a name="2-review-hello-description-and-requirements"></a>2. 검토 hello 설명 및 요구 사항
hello runbook 이라는 활동을 포함할 **추가 정보** 에 대 한 설명과 필요한 자산을 포함 하는 합니다.  Hello를 선택 하 여이 정보를 볼 수 **추가 정보** 활동 및 hello **워크플로 스크립트** 매개 변수입니다.  가져올 수도 있습니다 hello이 문서에서 동일한 정보입니다.

### <a name="3-configure-assets"></a>3. 자산 구성
hello runbook 자산을 만들고 적절 한 값으로 채우는 해야 다음 hello를 요구 합니다.  hello 이름은 기본 됩니다.  Hello에 대 한 이러한 이름을 지정 하면 다른 이름으로 자산을 사용할 수 있습니다 [입력 매개 변수](#using-the-runbooks) hello runbook을 시작 하는 경우.

| 자산 형식 | 기본 이름 | 설명 |
|:--- |:--- |:--- |:--- |
| [자격 증명](automation-credentials.md) |AzureCredential |Azure 구독 hello 기관 toostart 및 중지할 가상 컴퓨터에 있는 계정의 자격 증명을 포함 합니다. |
| [변수](automation-variables.md) |AzureSubscriptionId |Azure 구독 hello 구독 ID를 포함합니다. |

## <a name="using-hello-scenario"></a>Hello 시나리오를 사용 하 여
### <a name="parameters"></a>매개 변수
hello 각 runbook hello 다음 항목이 [입력 매개 변수](automation-starting-a-runbook.md#runbook-parameters)합니다.  모든 필수 매개 변수에 대한 값을 제공해야 하며 요구 사항에 따라 다른 매개 변수에 대한 값을 선택적으로 제공할 수 있습니다.

| 매개 변수 | 형식 | 필수 | 설명 |
|:--- |:--- |:--- |:--- |
| ServiceName |string |아니요 |값이 제공되면 해당 서비스 이름의 모든 가상 컴퓨터가 시작되거나 중지됩니다.  값이 제공 하는 경우 다음 hello Azure 구독이 있는 모든 클래식 가상 컴퓨터의 시작 또는 중지 합니다. |
| AzureSubscriptionIdAssetName |string |아니요 |Hello의 hello 이름을 포함 [변수 자산](#installing-and-configuring-the-scenario) Azure 구독 hello 구독 ID가 포함 된 합니다.  값을 지정하지 않으면 *AzureSubscriptionId* 가 사용됩니다. |
| AzureCredentialAssetName |string |아니요 |Hello의 hello 이름을 포함 [자격 증명 자산](#installing-and-configuring-the-scenario) runbook toouse hello에 대 한 hello 자격 증명을 포함 하는 합니다.  값을 지정하지 않으면 *AzureCredential* 이 사용됩니다. |

### <a name="starting-hello-runbooks"></a>Hello runbook 시작
Hello 방법 중 하나를 사용할 수 있습니다 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md) toostart이 문서의 hello runbook 중 하나입니다.

Windows PowerShell toorun을 사용 하 여 다음 명령 예제는 hello **StartAzureClassicVM** toostart hello 서비스 이름으로 모든 가상 컴퓨터 *MyVMService*합니다.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>출력
hello runbook은 [메시지를 출력](automation-runbook-output-and-messages.md) 시작 hello 여부 각 가상 컴퓨터를 나타내는 또는 stop 명령이 성공적으로 전송 합니다.  각 runbook에 대 한 hello 출력 toodetermine hello 결과에서 특정 문자열을 찾을 수 있습니다.  hello 가능한 출력 문자열은 다음 표에 hello에 나열 됩니다.

| Runbook | 조건 | Message |
|:--- |:--- |:--- |
| StartAzureClassicVM |가상 컴퓨터 이미 실행 중 |MyVM 이미 실행 중 |
| StartAzureClassicVM |가상 컴퓨터에 대한 시작 요청이 성공적으로 제출됨 |MyVM 시작됨 |
| StartAzureClassicVM |가상 컴퓨터에 대한 시작 요청 실패 |MyVM toostart를 실패 했습니다. |
| StopAzureClassicVM |가상 컴퓨터 이미 실행 중 |MyVM 이미 중지됨 |
| StopAzureClassicVM |가상 컴퓨터에 대한 시작 요청이 성공적으로 제출됨 |MyVM 시작됨 |
| StopAzureClassicVM |가상 컴퓨터에 대한 시작 요청 실패 |MyVM toostart를 실패 했습니다. |

다음은 hello를 사용 하 여 이미지 **StartAzureClassicVM** 로 [자식 runbook](automation-child-runbooks.md) 샘플 그래픽 runbook에서 합니다.  이 다음 표에 hello에 hello 조건부 링크를 사용 합니다.

| 링크 | 조건 |
|:--- |:--- |
| 성공 링크 |$ActivityOutput['StartAzureClassicVM'] -like "\* has been started" |
| 오류 링크 |$ActivityOutput['StartAzureClassicVM'] -notlike "\* has been started" |

![자식 runbook 예제](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>자세한 분석
다음은이 시나리오에서는 hello runbook의 상세한 분석 합니다.  이 정보를 사용 하면 tooeither hello runbook 또는 임원의 정당한 toolearn 작성 직접 자동화 시나리오에 대 한 사용자 지정 합니다.

### <a name="authentication"></a>인증
![인증](media/automation-solution-startstopvm/graphical-authentication.png)

hello runbook을 시작 활동 tooset hello로 [자격 증명](automation-credentials.md) 및 hello 나머지 hello runbook에 사용할 Azure 구독.

처음 두 개의 활동 hello **구독 Id 가져오기** 및 **Azure 자격 증명 가져오기**, hello 검색 [자산](#installing-the-runbook) hello 다음 두 작업에서 사용 하는 합니다.  활동 hello 자산을 직접 지정 하지만 hello 에셋 이름입니다.  수 hello 사용자 toospecify 이러한 이름을 hello에 있으므로 [입력 매개 변수](#using-the-runbooks), 입력된 매개 변수로 지정 된 이름으로 이러한 활동 tooretrieve hello 자산이 필요 합니다.

**추가 AzureAccount** 집합 hello hello 나머지 hello runbook에 사용 될 자격 증명입니다.  검색 하는 hello 자격 증명 자산 **Azure 자격 증명 가져오기** hello Azure 구독에에서 대 한 액세스 toostart 및 중지할 가상 컴퓨터를 포함 해야 합니다.  hello 사용 되는 구독으로 선택 되어 **Select-azuresubscription** hello 구독 Id를 사용 하 여에서 **구독 Id 가져오기**합니다.

### <a name="get-virtual-machines"></a>가상 컴퓨터 가져오기
![VM 가져오기](media/automation-solution-startstopvm/graphical-getvms.png)

hello runbook toodetermine 가상 컴퓨터는 해당 작업 하 고 여부은 이미 시작 또는 중지 (에 따라 hello runbook) 필요 합니다.   두 작업 중 하나는 hello Vm을 검색 합니다.  **서비스에서 Vm 가져오기** 경우 hello에 실행 됩니다 *ServiceName* hello runbook에 대 한 입력된 매개 변수 값을 포함 합니다.  **모든 Vm 가져오기** 경우 hello에 실행 됩니다 *ServiceName* hello runbook에 대 한 입력된 매개 변수 값이 포함 되지 않습니다.  이 논리는 각 활동 앞에 오는 hello 조건부 링크를 통해 수행 됩니다.

Hello를 사용 하 여 두 활동 모두 **Get-azurevm** cmdlet.  **모든 Vm 가져오기** 사용 하 여 hello **ListAllVMs** 매개 변수는 tooreturn 모든 가상 컴퓨터를 설정 합니다.  **서비스에서 Vm 가져오기** 사용 하 여 hello **GetVMByServiceAndVMName** 매개 변수는 설정 하 고 hello 제공 **ServiceName** hello에 대 한 입력된 매개 변수 **ServiceName**매개 변수입니다.  

### <a name="merge-vms"></a>VM 병합
![VM 병합](media/automation-solution-startstopvm/graphical-mergevms.png)

hello **병합 Vm** 활동은 입력 너무 필요한 tooprovide**Start-azurevm** hello 이름과 서비스 이름이 hello vm(s) toostart의 요구에 있는 합니다.  입력은 **Get All VMs**(모든 VM 가져오기) 또는 **Get VMs in Service**(서비스의 VM 가져오기)에서 가져올 수 있지만 **Start-AzureVM**은 입력에 대해 하나의 활동만 지정할 수 있습니다.   

hello 시나리오는 toocreate **병합 Vm** hello를 실행 하는 **Write-output** cmdlet.  hello **InputObject** 해당 cmdlet에 대 한 매개 변수는 hello 이전 두 활동의 hello 입력을 결합 하는 PowerShell 식입니다.  이들 활동 중 하나만 실행되기 때문에 하나의 출력 세트만 예상됩니다.  **Start-AzureVM** 은 입력 매개 변수에 이 출력을 사용할 수 있습니다.

### <a name="startstop-virtual-machines"></a>가상 컴퓨터 시작/중지
![VM 시작](media/automation-solution-startstopvm/graphical-startvm.png) ![VM 중지](media/automation-solution-startstopvm/graphical-stopvm.png)

Hello runbook에 따른 다음 활동 hello toostart 시도 또는 사용 하 여 hello runbook 중지 **Start-azurevm** 또는 **Stop-azurevm**합니다.  파이프라인 링크가 hello 활동 앞, 이후 실행 됩니다 한 번에서 반환 된 각 개체에 대 한 **병합 Vm**합니다.  hello 링크는 조건부 경우 hello hello 활동 실행만 *RunningState* hello의 가상 컴퓨터는 *Stopped* 에 대 한 **Start-azurevm** 및  *시작* 에 대 한 **Stop-azurevm**합니다. 이 조건이 충족 되지 않으면, 다음 **알림 이미 시작 되었습니다** 또는 **이미 중지 알림** 실행 toosend 사용 하 여 메시지 **Write-output**합니다.

### <a name="send-output"></a>출력 보내기
![VM 시작 알림](media/automation-solution-startstopvm/graphical-notifystart.png) ![VM 중지 알림](media/automation-solution-startstopvm/graphical-notifystop.png)

hello hello runbook의 최종 단계 toosend 출력 시작을 여부 hello 되었거나 각 가상 컴퓨터에 대 한 중지 요청이 제출 했습니다. 별도 **Write-output** 활동에 대해 각각, 조건부 링크와 함께 어떤 하나의 toorun을 결정 하 고 있습니다.  *OperationStatus*가 *성공*하면 **Notify VM Started**(VM 시작 알림) 또는 **Notify VM Stopped**(VM 중지 알림)가 실행됩니다.  경우 *OperationStatus* 다른 값이 **실패 알림 tooStart** 또는 **실패 알림 tooStop** 를 실행 합니다.

## <a name="next-steps"></a>다음 단계
* [Azure 자동화에서 그래픽 작성](automation-graphical-authoring-intro.md)
* [Azure 자동화의 자식 runbook](automation-child-runbooks.md)
* [Azure 자동화에서 Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)
