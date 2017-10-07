---
title: "Azure 사이트 복구의 aaaAdd Azure 자동화 runbook toorecovery 계획 | Microsoft Docs"
description: "Azure Site Recovery가 Azure Automation을 사용하여 복구 계획을 확장하는 데 어떻게 도움이 되는지 알아봅니다. 복구 tooAzure 중 toocomplete 복잡 한 작업 하는 방법에 대해 알아봅니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Azure 자동화 runbook toorecovery 계획 추가
이 문서에서는 Azure Site Recovery Azure 자동화 toohelp와 통합 하는 방법을 설명 복구 계획을 확장 합니다. 복구 계획으로 Site Recovery로 보호되는 VM의 복구를 오케스트레이션할 수 있습니다. 복구 계획에는 복제 tooa 보조 클라우드 계정과 복제 tooAzure 모두 작동합니다. 복구 계획 hello 복구를 만들어 줍니다 **일관 되 게 정확한**, **반복 가능한**, 및 **자동화 된**합니다. 를 장애 조치 Vm tooAzure Azure 자동화와의 통합에서는 복구 계획을 확장 합니다. 강력한 자동화 작업을 제공 하는 tooexecute runbook을 사용할 수 있습니다.

새 tooAzure 자동화 인 경우 다음을 할 수 있습니다 [등록](https://azure.microsoft.com/services/automation/) 및 [샘플 스크립트를 다운로드할](https://azure.microsoft.com/documentation/scripts/)합니다. 대 한 자세한 내용과 toolearn 방법을 사용 하 여 tooorchestrate 복구 tooAzure [복구 계획](https://azure.microsoft.com/blog/?p=166264), 참조 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)합니다.

이 문서에서는 Azure Automation Runbook을 복구 계획에 어떻게 통합할 수 있는지 설명합니다. 수동 작업이 필요 했던 예제 tooautomate 기본 작업을 사용 합니다. 어떻게 tooconvert multi-step 복구 tooa 단일 클릭 복구 작업을 설명 하기도 합니다.

## <a name="customize-hello-recovery-plan"></a>Hello 복구 계획 사용자 지정
1. Toohello 이동 **사이트 복구** 계획 리소스 블레이드를 복구 합니다. 예를 들어 hello 복구 계획에 복구를 위해 두 개의 Vm 추가 tooit 합니다. runbook을 추가 하는 toobegin 클릭 hello **사용자 지정** 탭 합니다.

    ![Hello 사용자 지정 단추를 클릭 합니다.](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. **그룹 1: 시작**을 마우스 오른쪽 단추로 클릭한 후 **사후 작업 추가**를 선택합니다.

    ![그룹 1: 시작을 마우스 오른쪽 단추로 클릭하고 사후 작업 추가](media/site-recovery-runbook-automation-new/customize-rp.png)

3. **스크립트 선택**을 클릭합니다.

4. Hello에 **업데이트 동작** 블레이드, 이름 hello 스크립트 **Hello World**합니다.

    ![hello 업데이트 작업 블레이드](media/site-recovery-runbook-automation-new/update-rp.png)

5. Automation 계정 이름을 입력합니다.
    >[!NOTE]
    > 모든 Azure 지역에서 자동화 계정을 hello 될 수 있습니다. 자동화 계정 hello hello에 있어야 합니다. hello Azure Site Recovery 자격 증명 모음과 동일한 구독 합니다.

6. Automation 계정에서 Runbook을 선택합니다. 이 runbook은 hello 첫 번째 그룹의 hello 복구 후 hello 복구 계획의 hello 실행 하는 동안 실행 하는 hello 스크립트입니다.

7. toosave hello 스크립트 클릭 **확인**합니다. hello 스크립트가 추가 되 고 너무**그룹 1: 사후 단계**합니다.

    ![사후 작업 그룹 1: 시작](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>스크립트를 추가하기 위한 고려 사항

* 옵션에 대 한 너무**단계를 삭제** 또는 **업데이트 hello 스크립트**, hello 스크립트를 마우스 오른쪽 단추로 클릭 합니다.
* 스크립트를 온-프레미스 컴퓨터 tooAzure에서 장애 조치 하는 동안 Azure에서 실행할 수 있습니다. 또한 실행할 있습니다 Azure에서 종료 하기 전에 기본 사이트 스크립트로 Azure tooan 온-프레미스 컴퓨터에서 장애 복구 하는 동안.
* 스크립트가 실행되면 복구 계획 컨텍스트가 삽입됩니다. 다음 예제는 hello 컨텍스트 변수를 보여 줍니다.

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    다음 표에서 hello hello 컨텍스트에서 각 변수에의 hello 이름 및 설명을 나열 합니다.

    | **변수 이름** | **설명** |
    | --- | --- |
    | RecoveryPlanName |실행 되 고 hello 계획의 hello 이름입니다. 이 변수를 사용 하 여 hello 복구 계획 이름에 따라 다른 작업을 수행할 수 있습니다. 또한 hello 스크립트 다시 사용할 수 있습니다. |
    | FailoverType |Hello 장애 조치 인지 테스트 지정, 계획 된, 또는 계획 되지 않은 합니다. |
    | FailoverDirection |복구 tooa 기본 또는 보조 사이트를 지정 합니다. |
    | GroupID |Hello 계획 실행 중일 때 hello 복구 계획의 hello 그룹 번호를 식별 합니다. |
    | VmMap |Hello 그룹의 모든 Vm의 배열입니다. |
    | VMMap key |각 VM에 대한 고유 키(GUID)입니다. 해당 되는 VM을 hello 하는 hello Azure Virtual Machine Manager (VMM) ID의 hello와 동일 합니다. |
    | SubscriptionId |hello Azure 구독 ID는 hello VM을 만들었습니다. |
    | RoleName |hello 복구 중인 Azure VM의 hello 이름입니다. |
    | CloudServiceName |VM이 생성 되었고 어떤 hello에서 hello Azure 클라우드 서비스 이름입니다. |
    | ResourceGroupName|hello Azure 리소스 그룹 이름은는 hello VM을 만들었습니다. |
    | RecoveryPointId|VM hello를 복구에 대 한 hello 타임 스탬프입니다. |

* 해당 hello 자동화 계정에 모듈을 따라 hello 확인 합니다.
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

모든 모듈은 호환되는 버전이어야 합니다. 모든 모듈은 호환 되는 쉽게 tooensure toouse hello 모든 hello 모듈의 최신 버전입니다.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Hello VMMap 루프에서의 모든 Vm에 액세스
Hello 코드 tooloop hello Microsoft VMMap의 모든 Vm에서 다음을 사용 합니다.

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> hello 리소스 그룹 이름 및 역할 이름 값은 hello 스크립트는 이전 tooa 부팅 그룹 경우 비어 있습니다. hello 값은 hello 해당 그룹의 VM을 성공적으로 장애 조치 하는 경우에 채워집니다. hello 스크립트는 hello 부팅 그룹의 작업 후입니다.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>사용 하 여 hello 동일한 여러 복구 계획에서 자동화 runbook

단일 스크립트는 외부 변수를 사용하여 여러 복구 계획에서 사용할 수 있습니다. 사용할 수 있습니다 [Azure 자동화 변수](../automation/automation-variables.md) toostore 매개 변수는 복구에 전달할 수 있는 계획 실행 합니다. Hello 복구 계획 이름은 접두사 toohello 변수를 추가 하 여 각 복구 계획에 대 한 개별 변수를 만들 수 있습니다. 그런 다음 hello 변수를 매개 변수로 사용 합니다. Hello 스크립트를 변경 하지 않고 매개 변수를 변경할 수는 있지만 변경 hello 스크립트의 작동 방식으로 hello 되는 계속 합니다.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Runbook 스크립트에서 단순 문자열 변수 사용

이 예제에서는 스크립트 hello 입력의는 보안 그룹 NSG (네트워크)을 복구 계획의 toohello Vm 적용 됩니다.

Hello 스크립트 toodetect 어떤 복구 계획이 실행 되 고, 복구 계획 컨텍스트 hello를 사용 합니다.

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

기존 NSG tooapply hello NSG 이름 및 hello NSG 리소스 그룹 이름을 알고 있어야 합니다. 복구 계획 스크립트에 대한 입력으로 이러한 변수를 사용합니다. toodo이 자동화 계정 자산 hello에 두 개의 변수를 만듭니다. 접두사 toohello 변수 이름으로 hello 매개 변수를 만들고 있는 hello 복구 계획의 hello 이름을 추가 합니다.

1. 변수 toostore hello NSG 이름을 만듭니다. Hello 복구 계획의 hello 이름을 사용 하 여 접두사 toohello 변수 이름을 추가 합니다.

    ![NSG 이름 변수 만들기](media/site-recovery-runbook-automation-new/var1.png)

2. 리소스 그룹 이름은 변수 toostore hello NSG를 만듭니다. Hello 복구 계획의 hello 이름을 사용 하 여 접두사 toohello 변수 이름을 추가 합니다.

    ![NSG 리소스 그룹 이름 만들기](media/site-recovery-runbook-automation-new/var2.png)


3.  Hello 스크립트에 다음 참조 코드 tooget hello 변수 값에는 hello를 사용 합니다.

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Hello runbook tooapply hello NSG toohello 네트워크 인터페이스의 hello에 hello 변수를 사용 하 여 실패 한 VM:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

각 복구 계획에 대 한 hello 스크립트를 다시 사용할 수 있도록 독립 변수를 만듭니다. 복구 계획 이름은 hello를 사용 하 여 접두사를 추가 합니다. 이 시나리오에 대 한 완전 한 종단 간 스크립트를 참조 하십시오. [사이트 복구는 복구 계획의 테스트 장애 조치 중 공용 IP와 NSG tooVMs 추가](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee)합니다.


### <a name="use-a-complex-variable-toostore-more-information"></a>자세한 내용은 복합 변수 toostore를 사용 하 여

특정 Vm에서 공용 IP에서 단일 스크립트 tooturn 원하는 시나리오를 살펴보겠습니다. 다른 시나리오에서는 tooapply 할 수 있습니다 (모든 Vm)에 없는 다른 Vm에서 다른 Nsg 합니다. 모든 복구 계획에 다시 사용할 수 있는 스크립트를 만들 수 있습니다. 각 복구 계획에는 다양한 수의 VM이 포함될 수 있습니다. 예를 들어 SharePoint 복구에는 두 개의 프런트 엔드가 있습니다. 기본 LOB(기간 업무) 응용 프로그램에는 하나의 프런트 엔드만 있습니다. 각 복구 계획에 별도의 변수를 만들 수 없습니다. 

다음 예제는 hello,에서는 새 기법을 사용 하 고 만들는 [복합 변수](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) hello Azure 자동화 계정 자산에 있습니다. 여러 값을 지정하여 이 작업을 수행합니다. 다음 단계는 Azure PowerShell toocomplete hello를 사용 해야 합니다.

1. PowerShell에서 tooyour Azure 구독에에서 로그인 합니다.

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. toostore hello 매개 변수는 hello 복구 계획의 hello 이름을 사용 하 여 hello 복잡 한 변수를 만듭니다.

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. 이 복잡 한 변수에 **VMDetails** 는 hello VM 보호 된 hello VM ID입니다. hello Azure 포털에서에서 VM ID tooget hello는 hello VM 속성을 표시 합니다. hello 다음 스크린 샷에서 두 개의 Vm hello 세부 정보를 저장 하는 변수

    ![GUID hello hello VM ID 사용](media/site-recovery-runbook-automation-new/vmguid.png)

4. Runbook에서 이 변수를 사용합니다. Hello 지정 된 경우 VM GUID를 hello 복구 계획 컨텍스트에서 찾을 수, hello VM에 NSG hello를 적용 합니다.

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. runbook을 hello 복구 계획 컨텍스트의 hello Vm을 반복 합니다. Hello VM의 존재 여부 확인 **$VMDetailsObj**합니다. 이 특성이 있으면 hello 변수 tooapply hello NSG의 hello 속성에 액세스 합니다.

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

다른 복구 계획에 대 한 hello 동일한 스크립트를 사용할 수 있습니다. 다른 변수에서 tooa 복구 계획에 해당 하는 hello 값을 저장 하 여 서로 다른 매개 변수를 입력 합니다.

## <a name="sample-scripts"></a>샘플 스크립트

toodeploy 샘플 스크립트 tooyour 자동화 계정을 클릭 hello **tooAzure 배포** 단추입니다.

[![TooAzure 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

또 다른 예로, hello 다음 비디오를 참조 하세요. 코드를 보여 줍니다 방법을 2 계층 WordPress 응용 프로그램 tooAzure toorecover:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>추가 리소스
* [Azure Automation 서비스 실행 계정](../automation/automation-sec-configure-azure-runas-account.md)
* [Azure Automation 개요](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation 개요")
* [Azure Automation 샘플 스크립트](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation 샘플 스크립트")
