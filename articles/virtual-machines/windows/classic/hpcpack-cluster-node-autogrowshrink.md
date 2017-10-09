---
title: "HPC Pack 클러스터 노드 aaaAutoscale | Microsoft Docs"
description: "자동으로 증가 하 고 hello Azure의 HPC Pack 클러스터 계산 노드 수를 축소 합니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>자동으로 증가 하 고 toohello 클러스터 워크 로드에 따라 Azure의 hello HPC 팩 클러스터 리소스를 축소 합니다.
HPC 팩 클러스터의 Azure "전환" 노드를 배포할 Azure Vm에서 HPC Pack 클러스터를 만드는 경우, 자동으로 확대 하거나 축소할 노드 또는 hello 클러스터에서 hello 작업 부하에 따라 코어와 같은 hello 클러스터 리소스를 방법이 필요할 수도 있습니다. 이러한 방식으로 hello 클러스터 리소스를 크기 조정 하면 toouse Azure 리소스 보다 효율적으로 하 고 해당 비용을 제어 합니다.

이 문서는 HPC Pack tooautoscale 계산 리소스를 제공 하는 두 가지 방법을 보여 줍니다.

* HPC 팩 클러스터 속성이 hello **AutoGrowShrink**

* hello **AzureAutoGrowShrink.ps1** HPC PowerShell 스크립트

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

현재 Windows Server 운영 체제를 실행하는 HPC 팩 계산 리소스만 자동으로 증가 및 축소할 수 있습니다.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Hello AutoGrowShrink 클러스터 속성 설정
### <a name="prerequisites"></a>필수 조건

* **HPC Pack 2012 R2 업데이트 2 또는 이상의 클러스터** -hello 클러스터 헤드 노드 수 온-프레미스 배포 나 Azure VM에서 합니다. 참조 [HPC Pack을 사용한 하이브리드 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget 온-프레미스 헤드 노드와 Azure "전환" 노드를 시작 합니다. Hello 참조 [HPC Pack IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md) tooquickly Azure Vm에서 HPC Pack 클러스터를 배포 합니다.

* **Azure Resource Manager 배포 모델에서 헤드 노드를 사용하는 클러스터의 경우** - HPC 팩 2016부터 Azure Active Directory 응용 프로그램의 인증서 인증은 Azure Resource Manager를 사용하여 배포된 클러스터 VM을 자동으로 증가 및 축소시키는 데 사용됩니다. 인증서를 다음과 같이 구성합니다.

  1. 클러스터 배포 후 원격 데스크톱 tooone 헤드 노드에 연결 합니다.

  2. 헤드 노드를 tooeach hello 인증서 (개인 키로 PFX 형식)를 업로드 하 고 tooCert:\LocalMachine\My 및 Cert: \LocalMachine\Root을 설치 합니다.

  3. 관리자 권한으로 Azure PowerShell을 시작 하 고 hello 명령을 헤드 노드 하나에서 다음을 실행 합니다.

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    계정이 둘 이상의 Azure Active Directory 테 넌 트 또는 Azure 구독에 포함 된 경우에 hello 다음을 실행할 수 있습니다 명령 tooselect hello 올바른 테 넌 트 구독:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    다음 명령은 tooview hello hello 현재 선택 항목 실행 테 넌 트 및 구독:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Hello 다음 스크립트를 실행 합니다.

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    여기서,

    **DisplayName** - Azure 활성 응용 프로그램 표시 이름입니다. Hello 응용 프로그램이 없는 경우 Azure Active Directory에 생성 됩니다.

    **홈 페이지** -hello 응용 프로그램의 hello 홈 페이지입니다. Hello 이전 예제와 같이 더미 URL을 구성할 수 있습니다.

    **IdentifierUri** -hello 응용 프로그램의 식별자입니다. Hello 이전 예제와 같이 더미 URL을 구성할 수 있습니다.

    **CertificateThumbprint** -1 단계에서에서 hello 헤드 노드에 설치 하는 hello 인증서의 지문입니다.

    **TenantId** - Azure Active Directory의 테넌트 ID입니다. Hello Azure Active Directory 포털에서 hello 테 넌 트 ID를 가져올 수 **속성** 페이지.

    **ConfigARMAutoGrowShrinkCert.ps1**에 대한 자세한 내용은 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`을 실행합니다.


* **(클래식 배포 모델) Azure에서 헤드 노드를 사용 하 여 클러스터에 대 한** hello 클래식 배포 모델에서 사용 하도록 설정 hello hello HPC Pack IaaS 배포 스크립트 toocreate hello 클러스터를 사용 하는 경우- **AutoGrowShrink** 클러스터 hello 클러스터 구성 파일에서 hello AutoGrowShrink 옵션을 설정 하 여 속성입니다. 자세한 내용은 hello와 함께 제공 되는 hello 설명서를 참조 하십시오. [스크립트 다운로드](https://www.microsoft.com/download/details.aspx?id=44949)합니다.

    Hello 또는 활성화할 **AutoGrowShrink** HPC PowerShell을 사용 하 여 hello 클러스터를 배포한 후 클러스터의 속성 명령이 hello 다음 섹션에서에서 설명 합니다. 첫 번째 전체 hello 다음 단계를이 tooprepare, 합니다.

  1. Hello Azure 구독 및 헤드 노드 hello에는 Azure 관리 인증서를 구성 합니다. 테스트 배포에 대 한 hello 헤드 노드에서 HPC Pack을 설치 하는 hello Microsoft 기본 HPC Azure 자체 서명 된 인증서를 사용 하 여 한 다음 해당 인증서 tooyour Azure 구독을 업로드할 수 있습니다. 옵션 및 단계에 대 한 참조 hello [TechNet 라이브러리 지침](https://technet.microsoft.com/library/gg481759.aspx)합니다.

  2. 실행 **regedit** hello 헤드 노드에서 tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo를 이동 하 고 문자열 값을 추가 합니다. 너무 hello 값 이름 설정 "지문" 및 값 데이터 toohello 인증서 지 문으로 hello 1 단계.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>HPC PowerShell 명령 tooset hello AutoGrowShrink 속성
다음은 샘플 HPC PowerShell 명령을 tooset **AutoGrowShrink** 및 tootune 동작 추가 매개 변수를 사용 합니다. 참조 [AutoGrowShrink 매개 변수](#AutoGrowShrink-parameters) 이 문서의 뒷부분에 있는이 설정의 전체 목록은 hello에 대 한 합니다.

toorun 이러한의 명령을 관리자 권한으로 hello 클러스터 헤드 노드에 HPC PowerShell를 시작 합니다.

**tooenable hello AutoGrowShrink 속성**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**toodisable hello AutoGrowShrink 속성**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**toochange hello 분의 간격을 증가**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**toochange hello 분 단위로 간격을 축소**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**tooview hello AutoGrowShrink의 현재 구성**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**AutoGrowShrink에서 tooexclude 노드 그룹**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> 이 매개 변수는 HPC 팩 2016부터 지원됩니다.
>

### <a name="autogrowshrink-parameters"></a>AutoGrowShrink 매개 변수
hello 다음 AutoGrowShrink 매개 변수는 hello를 사용 하 여 수정할 수 있는 **집합 HpcClusterProperty** 명령입니다.

* **EnableGrowShrink** tooenable 전환-hello를 사용 하지 않도록 설정 하거나 **AutoGrowShrink** 속성입니다.
* **ParamSweepTasksPerCore** -파라메트릭 스윕 수가 toogrow 한 코어 작업 합니다. hello 기본값이 toogrow 작업당 한 코어입니다.

  > [!NOTE]
  > HPC 팩 QFE KB3134307 변경 **ParamSweepTasksPerCore** 너무**TasksPerResourceUnit**합니다. 노드, 소켓 또는 코어 수 있으며 hello 작업 리소스 형식을 기반으로 합니다.
  >
  >
* **GrowThreshold** -큐에 대기 중인된 작업 tootrigger 자동 증가 임계값입니다. hello 기본값은 1 또는 더 많은 작업의 상태 큐에 대기 중인된 hello 됨을 의미 하는 1을, 노드를 자동으로 증가 합니다.
* **GrowInterval** -tootrigger 자동 증가 값 분의 간격입니다. hello 기본 간격은 5 분입니다.
* **ShrinkInterval** -간격 (분) tootrigger 자동 축소 합니다. hello 기본 간격은 5 분입니다. |
* **ShrinkIdleTimes** -연속 검사 tooshrink tooindicate hello 노드 수는 유휴 상태입니다. hello 기본값은 3 회입니다. 예를 들어 경우 hello, **ShrinkInterval** 은 5 분, HPC 팩 hello 노드가 인지 유휴 5 분 마다 확인 합니다. Hello 노드가 연속 3 (15 분)을 확인 한 후 hello 유휴 상태에 있는, HPC Pack 해당 노드를 축소 합니다.
* **ExtraNodesGrowRatio** -추가 노드 toogrow 인터페이스 MPI (Message Passing) 작업에 대 한 비율입니다. hello 기본값은 1 HPC Pack 증가 MPI 작업에 대 한 1% 노드 함을 의미 합니다.
* **GrowByMin** -hello 자동 증가 정책이 hello 작업에 필요한 hello 최소 리소스 기반 여부 tooindicate를 전환 합니다. HPC Pack hello 작업에 필요한 hello 최대 리소스를 기준으로 작업에 대 한 노드를 증가 함을 의미 하는 hello 기본값은 false입니다.
* **SoaJobGrowThreshold** -임계값의 들어오는 SOA tootrigger hello 요청 템플릿 자동 프로세스를 확장 합니다. hello 기본값은 50000입니다.

  > [!NOTE]
  > 이 매개 변수는 HPC 팩 2012 R2 업데이트 3부터 지원됩니다.
  >
  >
* **SoaRequestsPerCore** -toogrow 단일 코어를 요청 하는 들어오는 SOA 수 있습니다. hello 기본값은 20000입니다.

  > [!NOTE]
  > 이 매개 변수는 HPC 팩 2012 R2 업데이트 3부터 지원됩니다.
  >
* **ExcludeNodeGroups** – hello에 대 한 노드 노드 그룹 않는 자동으로 확장 및 축소를 지정 합니다.
  
  > [!NOTE]
  > 이 매개 변수는 HPC 팩 2016부터 지원됩니다.
  >

### <a name="mpi-example"></a>MPI 예제
기본적으로 HPC Pack 증가 1 %MPI 작업에 대 한 추가 노드 (**ExtraNodesGrowRatio** too1 설정). hello 원인은 MPI 여러 노드에 필요할 수 있습니다 및 모든 노드 준비 되 면 hello 작업 에서만 실행할 수 있습니다. Azure 노드 시작 되 면 한 노드에 다른 노드가 toobe 해당 노드 tooget 준비 될 때까지 기다리는 동안 유휴 상태를 발생 시키는 다른 항목 보다 더 많은 시간 toostart 해야 할 수 가끔. HPC 팩은 추가 노드를 증가시켜 이 리소스 대기 시간을 줄이며 잠재적으로 비용을 절감합니다. 비슷한 명령을 실행 하는 MPI 작업 (예: too10%)에 대 한 추가 노드의 tooincrease hello 백분율

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>SOA 예제
기본적으로 **SoaJobGrowThreshold** too50000 설정 및 **SoaRequestsPerCore** too200000 설정 됩니다. 70000개의 요청을 가진 하나의 SOA 작업을 제출하는 경우 대기열에 저장된 하나의 태스크가 있으며 수신 요청 수는 70000개입니다. Hello 작업, 지연 되 고 들어오는 요청에 대 한 증가 (70000 50000)에 대 한 1 코어 HPC Pack 증가 하는 경우 / 20000 = 1 코어에 총 2 개 코어가 SOA 작업에 대해 증가 합니다.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Hello AzureAutoGrowShrink.ps1 스크립트 실행
### <a name="prerequisites"></a>필수 조건

* **HPC Pack 2012 R2 업데이트 1 또는 이후 클러스터** -hello **AzureAutoGrowShrink.ps1** 스크립트 hello % CCP_HOME %bin 폴더에 설치 됩니다. hello 클러스터 헤드 노드 수 온-프레미스 배포 나 Azure VM에서 합니다. 참조 [HPC Pack을 사용한 하이브리드 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget 온-프레미스 헤드 노드와 Azure "전환" 노드를 시작 합니다. Hello 참조 [HPC Pack IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md) tooquickly Azure Vm에서 HPC Pack 클러스터를 배포 하거나 사용할는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)합니다.
* **Azure PowerShell 1.4.0** -hello 스크립트는 현재 특정 버전의 Azure PowerShell이에 따라 다릅니다.
* **Azure 사용 하 여 클러스터에 대 한 버스트 노드** -또는 hello 헤드 노드에서 HPC Pack 설치 되어 있는 클라이언트 컴퓨터에서 hello 스크립트를 실행 합니다. 클라이언트 컴퓨터에서 실행 하는 경우 설정 확인 hello 변수 $env: CCP_SCHEDULER toopoint toohello 헤드 노드. hello Azure "전환" 노드 toohello 클러스터를 추가 해야 하지만 hello 된 상태에에서 있을 수 있습니다.
* **Azure Vm (리소스 관리자 배포 모델)에 배포 된 클러스터에 대 한** -hello 리소스 관리자 배포 모델에서 배포 된 Azure Vm의 클러스터에 대 한 hello 스크립트에서는 Azure 인증을 위한 두 가지 방법: tooyour Azure 계정에에서 로그인 toorun hello 스크립트 될 때마다 (실행 하 여 `Login-AzureRmAccount`, 하거나 서비스 보안 주체 tooauthenticate 인증서로 구성 합니다. HPC Pack hello 스크립트를 제공 합니다. **ConfigARMAutoGrowShrinkCert.ps** toocreate 인증서로 서비스 사용자입니다. hello 스크립트는 Azure Active Directory (Azure AD) 응용 프로그램 및 서비스 사용자를 만들고 hello 참가자 역할 toohello 서비스 사용자를 할당 합니다. toorun hello 스크립트를 관리자 권한으로 Azure PowerShell을 시작 하 고 hello 다음 명령을 실행:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    **ConfigARMAutoGrowShrinkCert.ps1**에 대한 자세한 내용은 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`을 실행합니다.

* **Azure Vm (클래식 배포 모델)에 배포 된 클러스터에 대 한** -hello에 따라 달라 지므로 hello 헤드 노드 VM에서 hello 스크립트를 실행 **Start-hpciaasnode.ps1** 및 **중지-HpcIaaSNode.ps1**설치 되는 스크립트입니다. 이러한 스크립트는 추가적으로 Azure 관리 인증서 또는 게시 설정 파일이 필요합니다( [Azure의 HPC 팩 클러스터에서 계산 노드 관리](hpcpack-cluster-node-manage.md)참조). 모든 hello 계산 노드 Vm 필요한 toohello 클러스터에 이미 추가 되어 있는지 확인 하십시오. Hello 중지 됨 상태에에서 있을 수 있습니다.



### <a name="syntax"></a>구문
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>매개 변수
* **NodeTemplates** -hello 노드 템플릿 toodefine 형태의 노드 toogrow hello에 대 한 범위 hello 및 축소 합니다. 지정 하지 않으면 (hello 기본값은 @()) hello의 모든 노드에서 **AzureNodes** 노드 그룹 범위에 포함 되 **NodeType** hello에 AzureNodes 이면와 모든 노드가 값 **ComputeNodes** 노드 그룹 범위에 포함 되 **NodeType** ComputeNodes 값입니다.
* **Jobtemplate은** -hello 형태의 노드 toogrow hello에 대 한 템플릿 toodefine hello 범위 작업입니다.
* **NodeType** -유형의 노드 toogrow hello 및 축소 합니다. 지원되는 값은 다음과 같습니다.

  * **AzureNodes** – 온-프레미스 또는 Azure IaaS 클러스터의 Azure PaaS(버스트) 노드에 사용합니다.
  * **ComputeNodes** - Azure IaaS 클러스터의 계산 노드 VM에만 사용합니다.

* **NumOfQueuedJobsPerNodeToGrow** -toogrow 한 노드에 데 필요한 대기 중인된 작업의 수입니다.
* **NumOfQueuedJobsToGrowThreshold** -hello 임계값 수가 대기 중인된 작업 toostart hello 프로세스를 증가 합니다.
* **NumOfActiveQueuedTasksPerNodeToGrow** -toogrow 한 노드에 데 필요한 hello 대기 중인된 활성 태스크 수입니다. **NumOfQueuedJobsPerNodeToGrow** 가 0보다 큰 값으로 지정된 경우 이 매개 변수가 무시됩니다.
* **NumOfActiveQueuedTasksToGrowThreshold** -hello 임계값 수가 대기 중인된 활성 태스크 toostart hello 프로세스를 증가 합니다.
* **NumOfInitialNodesToGrow** -hello 범위에 모든 hello 노드가 노드 toogrow의 최소 수를 초기 **된** 또는 **중지 (할당 취소)**합니다.
* **GrowCheckIntervalMins** -hello 간격 (분) toogrow를 확인 합니다.
* **ShrinkCheckIntervalMins** -hello 간격 (분) tooshrink를 확인 합니다.
* **ShrinkCheckIdleTimes** -연속 축소 확인 횟수가 hello (구분 하 여 **ShrinkCheckIntervalMins**) tooindicate hello 노드는 유휴 상태입니다.
* **UseLastConfigurations** -hello 인수 파일에 저장 된 이전 구성을 hello 합니다.
* **ArgFile**-hello hello 인수 사용 되는 파일 toosave의 이름 및 hello 구성 toorun hello 스크립트를 업데이트 합니다.
* **LogFilePrefix** -hello 로그 파일의 hello 접두사 이름입니다. 경로를 지정할 수 있습니다. 기본 hello 로그 toohello 작성 된 현재 작업 디렉터리입니다.

### <a name="example-1"></a>예 1
hello 다음 예제에서는 구성 hello Azure 버스트 노드 기본 AzureNode 템플릿을 toogrow와 함께 배포 하 고 자동으로 축소 합니다. 모든 노드는 처음 hello 경우 **된** 상태 이면 3 개 이상의 노드가 시작 됩니다. Hello 스크립트의 수에는 큐에 대기 중인된 작업의 hello 비율을 초과할 때까지 노드를 시작 hello 큐 작업 수 8 개를 초과 하는 경우 **NumOfQueuedJobsPerNodeToGrow**합니다. 노드 toobe 3 유휴 회 연속으로 유휴, 있으면 중지 됩니다.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>예 2
hello 다음 예제에서는 구성 hello Azure 계산 노드 Vm 기본 ComputeNode 템플릿을 toogrow hello 사용 하 여 배포와 자동으로 축소 합니다.
hello 기본 작업 템플릿을 통해 구성 된 hello 작업이 hello 클러스터에서 작업 부하의 hello 범위를 정의 합니다. 모든 hello 노드가 초기에 중지 되어 최소 5 개의 노드가 시작 됩니다. Hello 스크립트의 수에는 너무 대기 중인된 활성 태스크의 hello 비율을 초과할 때까지 노드를 시작 대기 중인된 활성 태스크의 hello 수가 15 개를 초과 하는 경우**NumOfActiveQueuedTasksPerNodeToGrow**합니다. 노드 toobe 10 유휴 회 연속으로 유휴, 있으면 중지 됩니다.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
