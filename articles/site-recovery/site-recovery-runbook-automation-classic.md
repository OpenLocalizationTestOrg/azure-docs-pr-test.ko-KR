---
title: "hello 클래식 포털에서 Azure 자동화 runbook toorecovery 계획 aaaAdd | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 지금 사용 하 여 방법을 tooAzure 복구 하는 동안 Azure 자동화 toocomplete 복잡 한 작업을 사용 하 여 tooextend 복구 계획 설명"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Hello 클래식 포털에서 Azure 자동화 runbook toorecovery 계획 추가
이 자습서에서는 Azure 자동화 tooprovide 확장성 toorecovery 계획과 Azure Site Recovery 통합 하는 방법을 설명 합니다. 복구 계획에는 가상 컴퓨터 복제 toosecondary 클라우드와 복제 tooAzure 시나리오 둘 다에 대 한 Azure Site Recovery를 사용 하 여 보호의 복구를 조정할 수 있습니다. 또한 hello 복구 될 때 지원할 **일관 되 게 정확한**, **반복 가능한**, 및 **자동화 된**합니다. 가상 컴퓨터 tooAzure를 통해 실패 하는 경우 Azure 자동화와의 통합 복구 계획을 확장 하 고 강력한 자동화 작업 수 있도록 기능 tooexecute runbook을 제공 합니다.

Azure Automation에 대해 아직 들어보지 못한 경우 [여기](https://azure.microsoft.com/services/automation/)에 등록하여 [여기](https://azure.microsoft.com/documentation/scripts/)에서 샘플 스크립트를 다운로드합니다. 에 대해 자세히 알아보세요 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) tooorchestrate 복구 tooAzure 복구를 사용 하 여 계획 하는 방법 및 [여기](https://azure.microsoft.com/blog/?p=166264)합니다.

이 짧은 자습서에서는 Azure Automation runbook을 복구 계획에 통합하는 방법에 대해 살펴봅니다. 이전 직접 이동 해야 하는 간단한 작업을 자동화 하 고 tooconvert 다중 복구 단일 클릭 복구 작업을 실행 하는 방법을 참조 합니다. 문제가 발생하는 경우 간단한 스크립트 문제를 해결하는 방법에 대해서도 살펴보겠습니다.

## <a name="protect-hello-application-tooazure"></a>Hello 응용 프로그램 tooAzure 보호
두 가상 컴퓨터로 구성되는 간단한 응용프로그램으로 시작해 보겠습니다. 여기서는 Fabrikam의 HRweb 응용프로그램을 사용합니다. Fabrikam-HRweb-프런트 엔드 및 백 엔드 Hrweb-Fabrikam-hello 두 개의 가상 컴퓨터가 Azure Site Recovery를 사용 하 여 tooAzure 보호 됩니다. Azure Site Recovery를 사용 하 여 tooprotect hello 가상 컴퓨터는 아래의 hello 단계를 수행 합니다.

1. 가상 컴퓨터의 보호를 활성화합니다.
2. Hello 가상 컴퓨터 초기 복제를 완료 하 고 복제 중인지 확인 합니다.
3. Hello 초기 복제가 완료 되 고 복제 상태 hello은 보호 된 때까지 기다립니다.

## ![](media/site-recovery-runbook-automation/01.png)
이 자습서에서는 Fabrikam HRweb 응용 프로그램 toofailover hello 응용 프로그램 tooAzure hello에 대 한 복구 계획을 만듭니다. 다음 우리는와 통합 하 runbook이 Azure 가상 컴퓨터에서 포트 80 웹 페이지를 tooserve 조치할 hello에 끝점을 만듭니다.

먼저, 응용프로그램에 대한 복구 계획을 만들어 보겠습니다.

## <a name="create-hello-recovery-plan"></a>Hello 복구 계획 만들기
toorecover hello 응용 프로그램 tooAzure toocreate 복구 계획 해야합니다.
가상 컴퓨터의 복구의 hello 순서를 지정할 수는 복구 계획을 사용 하 여 합니다. 그룹 1에에서 배치 하는 hello 가상 컴퓨터에서 복구 하 고, 첫 번째 실행 합니다 및 다음 그룹 2의에서 가상 컴퓨터 hello 다룰 것입니다.

아래와 같이 복구 계획을 만듭니다.

![](media/site-recovery-runbook-automation/12.png)

설명서를 참조 하는 복구 계획에 대 한 자세한 tooread [여기](https://msdn.microsoft.com/library/azure/dn788799.aspx "여기")합니다.

다음으로, 보겠습니다 Azure 자동화 hello 필요한 아티팩트를 만듭니다.

## <a name="create-hello-automation-account-and-its-assets"></a>Hello 자동화 계정 및 관련 자산 만들기
Azure 자동화 계정 toocreate runbook이 필요합니다. 계정이 아직 없는 경우 tooAzure 자동화 탭으로 표시 된 이동 ![](media/site-recovery-runbook-automation/02.png)새 계정을 만듭니다.

1. 와 이름이 tooidentify hello 계정에 부여 합니다.
2. 저장할 tooplace hello 계정에서 지리적 위치 영역을 지정 합니다.

Hello에 tooplace hello 계정 것이 좋습니다 hello ASR 자격 증명 모음과 동일한 지역입니다.

![](media/site-recovery-runbook-automation/03.png)

다음으로 hello 다음 hello 계정에에서 자산을 만듭니다.

### <a name="add-a-subscription-name-as-asset"></a>자산으로 구독 이름 추가
1. 새 설정을 추가 ![](media/site-recovery-runbook-automation/04.png) 너무 선택한에 hello Azure 자동화 자산![](media/site-recovery-runbook-automation/05.png)
2. Hello 변수 유형으로 **문자열**
3. 변수 이름으로 **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Hello 변수 값으로 실제 Azure 구독 이름을 지정 합니다.

   ![](media/site-recovery-runbook-automation/07_1.png)

Hello hello hello Azure 포털에서 사용자의 계정 설정 페이지에서에서 구독의 이름을 식별할 수 있습니다.

### <a name="add-an-azure-login-credential-as-asset"></a>Azure 로그인 자격 증명을 자산으로 추가
Azure 자동화 tooconnect toothe 구독 Azure PowerShell을 사용 하 고 있는 hello 아티팩트에 작동 합니다. 이를 위해 Microsoft 계정 또는 회사나 학교 계정을 사용하여 인증을 받아야 합니다.
Hello runbook에서 안전 하 게 사용 하는 자산 toobe에 hello 계정 자격 증명을 저장할 수 있습니다.

1. 새 설정을 추가 ![](media/site-recovery-runbook-automation/04.png) 에서 Azure 자동화 자산 hello 및 선택![](media/site-recovery-runbook-automation/09.png)
2. 자격 증명 유형으로 hello **Windows PowerShell 자격 증명**
3. Hello 이름으로 지정 **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Hello 사용자 이름 및 toosign에 암호를 지정 합니다.

이제 이러한 두 설정을 자산에서 사용할 수 있습니다.

![](media/site-recovery-runbook-automation/11.png)

PowerShell 통해 tooconnect tooyour 구독 지정 방법에 대 한 자세한 내용은 [여기](/powershell/azure/overview)합니다.

다음으로 장애 조치 후 hello 프런트 엔드 가상 컴퓨터에 대 한 끝점을 추가할 수 있는 Azure 자동화에서 runbook을 만들어집니다.

## <a name="azure-automation-context"></a>Azure 자동화 컨텍스트
ASR 전달 컨텍스트 변수 toohello runbook toohelp 결정적 스크립트를 작성 합니다. Hello 클라우드 서비스 및 가상 컴퓨터 hello hello 이름을 예측할 수 있고 아닌지 항상 여기서 hello 가상 컴퓨터 이름의 hello 이름을 변경 했을 수 기한 하나 hello 같은 toocertain 시나리오 소유 하 고 있는 hello 경우 발생 하는 주장 수 하나 Azure에 toounsupported 문자가 있습니다. 따라서이 정보는 toohello ASR 복구 계획의 일부로 전달 되 hello *컨텍스트*합니다.

다음은 hello 컨텍스트 변수의 표시 하는 방법의 예입니다.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


hello 아래 표에서 이름 및 hello 컨텍스트에서 각 변수에 대해 설명 합니다.

| **변수 이름** | **설명** |
| --- | --- |
| RecoveryPlanName |실행되는 계획의 이름입니다. 사용 하 여 이름에 따라 작업을 수행 하는 데 도움이 됩니다. 동일한 hello 스크립트 |
| FailoverType |계획 되거나 계획 되지 않은 hello 장애 조치는 테스트 하는지 여부를 지정 합니다. |
| FailoverDirection |복구 tooprimary 또는 secondary 상태 인지 여부를 지정 합니다. |
| GroupID |Hello 계획 실행 중일 때 hello 복구 계획 내에서 hello 그룹 번호를 식별 합니다. |
| VmMap |Hello 그룹의 모든 hello 가상 컴퓨터의 배열 |
| VMMap key |각 VM에 대한 고유 키(GUID)입니다. 해당 되는 hello 가상 컴퓨터의 VMM ID hello와 같을 hello 했습니다. |
| RoleName |Hello 복구 되는 Azure VM의 이름 |
| CloudServiceName |가상 컴퓨터를 만들 때 어떤 hello에서 azure 클라우드 서비스 이름입니다. |

tooidentify hello VmMap 키 hello 컨텍스트에 ASR의 toohello VM 속성 페이지로 이동 하 고 hello VM GUID 속성을 살펴볼 수 있습니다.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>자동화 Runbook 작성
이제 hello 프런트 엔드 가상 컴퓨터에 hello runbook tooopen 포트를 80을 만듭니다.

1. Hello hello 이름의 Azure 자동화 계정에서에서 새 runbook을 만들려면 **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Hello runbook의 작성자 보기 toohello 이동한 hello 초안 모드를 입력 합니다.
3. 먼저 hello 변수 toouse hello 복구 계획 컨텍스트로 지정

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. 그런 다음 toohello 구독 hello 자격 증명 및 구독 이름을 사용 하 여 연결

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   사용 하는 hello Azure 자산 – **AzureCredential** 및 **AzureSubscriptionName** 여기 합니다.
5. 이제 hello 끝점 세부 정보를 지정 하 고 hello tooexpose hello 끝점을 구하려는 hello 가상 컴퓨터의 GUID입니다. 이 사례 hello 프런트 엔드 가상 컴퓨터에 있습니다.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Azure 끝점 프로토콜 hello, hello VM에서 로컬 포트와 해당 매핑된 공용 포트를 지정합니다. 이러한 변수는 매개 변수 hello에 필요한 끝점 tooVMs 추가 Azure 명령입니다. hello VMGUID hello에서 toooperate가 필요한 hello 가상 컴퓨터의 GUID를 포함 합니다.
6. hello 스크립트 이제 VM GUID를 지정 하는 hello에 대 한 hello 컨텍스트를 추출 여기에서 참조 하는 hello 가상 컴퓨터에 끝점을 만듭니다.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. 이 작업이 완료 되 면 게시 적중 ![](media/site-recovery-runbook-automation/20.png) tooallow 사용자 스크립트 toobe 실행에 사용할 수 있습니다.

hello 전체 스크립트는 아래에 지정 된 참조

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Hello 스크립트 toohello 복구 계획 추가
Hello 스크립트 준비 되 면 앞서 만든 toohello 복구 계획을 추가할 수 있습니다.

1. 만든 hello 복구 계획 선택 tooadd 스크립트 그룹 2 후 합니다. ![](media/site-recovery-runbook-automation/15.png)
2. 스크립트 이름을 지정합니다. 이 스크립트의 hello 복구 계획 내에서 표시 하기 위한 친숙 한 이름 뿐입니다.
3. 장애 조치 tooAzure 스크립트 hello –에 hello Azure 자동화 계정 이름을 선택 합니다.
4. Hello Azure Runbook을 작성 하는 hello runbook을 선택 합니다.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>기본 측 스크립트
장애 조치 tooAzure를 실행 하는 경우 tooexecute를 기본 측 스크립트도 선택할 수 있습니다. 이러한 스크립트는 장애 조치 중 hello VMM 서버에서 실행 됩니다.
기본 측 스크립트는 종료 전 및 종료 후 단계에만 사용할 수 있습니다. B hello 주 사이트 toobe 일반적으로 사용할 수 없는 재해가 발생 하는 경우입니다.
계획 되지 않은 장애 조치 중에 주 사이트 작업을 위해 선택 하는 경우에 시도 합니다 toorun hello 기본 측 스크립트. 제한 시간 hello 장애 조치는 계속 연결할 수 없는 경우 toorecover hello 가상 컴퓨터.
기본 측 스크립트 tooAzure 장애 조치 하는 동안 보호 된 VMM tooAzure-없는 VMware/물리적/하이퍼-v 사이트에 사용할 수 있지 않습니다.
그러나 때 장애 복구 Azure tooon 온-프레미스, 기본 측 스크립트 (Runbook)에서 사용할 수 VMware 제외한 모든 대상에 대 한 합니다.

## <a name="test-hello-recovery-plan"></a>테스트 hello 복구 계획
Hello runbook toohello 계획을 추가한 후 테스트 장애 조치를 시작 하 고 동작에 나타납니다. 항상 테스트 장애 조치 tootest toorun 권장 프로그램 응용 프로그램 및 hello 복구 계획 tooensure 오류가 없는 합니다.

1. Hello 복구 계획을 선택 하 고 테스트 장애 조치를 시작 합니다.
2. Hello 계획 실행 중 hello runbook은 실행 여부 또는 통해 상태를 확인할 수 있습니다.

   ![](media/site-recovery-runbook-automation/17.png)
3. 또한 볼 수 있습니다 hello hello runbook에 대 한 hello Azure 자동화 작업 페이지에서 runbook 실행 상태를 자세히 설명 합니다.

   ![](media/site-recovery-runbook-automation/18.png)
4. Hello runbook 실행 결과는 별도로 hello 장애 조치가 완료 된 후에 hello 실행이 성공 여부 또는 hello Azure 가상 컴퓨터 페이지를 방문 하 고 hello 끝점을 살펴보면가 아니라를 확인할 수 있습니다.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>샘플 스크립트
안내 하는 동안이 자습서에서는 끝점 tooan Azure 가상 컴퓨터를 추가 하는 작업에 사용 되는 일반적으로 하나 자동화, 다양 한 Azure 자동화를 사용 하 여 다른 강력한 자동화 작업을 수행할 수 있습니다. Microsoft 및 hello Azure 자동화 커뮤니티 사용자 고유의 솔루션 및 보다 큰 자동화 작업에 대 한 빌딩 블록으로 사용할 수 있는 유틸리티 runbook을 만들기 전에 수 있는 샘플 runbook을 제공 합니다. Hello 갤러리에서 사용을 시작 하 고 Azure Site Recovery를 사용 하 여 응용 프로그램에 대 한 강력한 한 번의 클릭 복구 계획을 빌드하십시오.

## <a name="additional-resources"></a>추가 리소스
[Azure 자동화 개요](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 자동화 개요")

[Azure 자동화 스크립트 샘플](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 자동화 스크립트 샘플")
