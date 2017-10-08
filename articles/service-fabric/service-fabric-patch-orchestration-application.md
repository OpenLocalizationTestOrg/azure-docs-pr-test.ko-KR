---
title: "서비스 패브릭 패치 오케스트레이션 응용 프로그램 aaaAzure | Microsoft Docs"
description: "응용 프로그램 tooautomate 운영 체제 서비스 패브릭 클러스터에 패치를 적용 합니다."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>서비스 패브릭 클러스터에 hello Windows 운영 체제 패치

hello 패치 오케스트레이션 응용 프로그램은 Azure에서 가동 중지 시간 없이 서비스 패브릭 클러스터에 패치를 적용 하는 운영 체제를 자동화 하는 Azure 서비스 패브릭 응용 프로그램.

hello 패치 오케스트레이션 앱 hello 다음을 제공합니다.

- **자동 운영 체제 업데이트 설치**. 운영 체제 업데이트가 자동으로 다운로드되고 설치됩니다. 클러스터 노드는 필요에 따라 클러스터 가동 중지 시간 없이 다시 부팅됩니다.

- **클러스터 인식 패치 및 상태 통합**. 업데이트를 적용 하는 동안 hello 패치 오케스트레이션 앱 hello 클러스터 노드의 hello 상태를 모니터링 합니다. 클러스터 노드는 한 번에 하나의 노드씩 또는 한 번에 하나의 업그레이드 도메인씩 업그레이드됩니다. Hello 클러스터의 hello 상태 toohello 패치 프로세스 인해 다운 되 면 hello 문제 만나볼 수도 중지 tooprevent은 패치를 적용 합니다.

## <a name="internal-details-of-hello-app"></a>Hello 응용 프로그램의 내부 세부 정보

hello 패치 오케스트레이션 앱 hello 하위 구성 요소를 다음으로 구성 됩니다.

- **코디네이터 서비스**: 이 상태 저장 서비스는 다음과 같은 역할을 합니다.
    - Hello 전체 클러스터에서 hello Windows 업데이트 작업을 조정 합니다.
    - 완료 된 Windows 업데이트 작업의 hello 결과 저장 합니다.
- **노드 에이전트 서비스**: 이 상태 비저장 서비스는 모든 Service Fabric 클러스터 노드에서 실행됩니다. hello 서비스는 담당 합니다.
    - Hello 에이전트 NTService 노드를 부트스트랩 합니다.
    - 노드 에이전트 NTService hello를 모니터링 합니다.
- **노드 에이전트 NTService**: 이 Windows NT 서비스는 더 높은 수준의 권한(시스템)에서 실행됩니다. 반면, hello 노드 에이전트 서비스 및 hello 코디네이터 서비스 하위 수준의 권한 (네트워크 서비스)에서 실행합니다. hello 서비스는 hello 모든 hello 클러스터 노드에서 Windows 업데이트 작업을 다음을 수행 합니다.
    - Hello 노드에서 자동 Windows Update를 사용 하지 않도록 설정 합니다.
    - 다운로드 및 설치 Windows Update toohello 정책 hello 사용자에 따라 제공 했습니다.
    - Hello 컴퓨터 post Windows 업데이트 설치를 다시 시작 합니다.
    - Windows 업데이트 toohello Coordinator 서비스의 hello 결과 업로드 합니다.
    - 모든 재시도가 끝난 다음 작업이 실패한 경우 상태 보고서 보고

> [!NOTE]
> hello 패치 오케스트레이션 응용 프로그램 사용 하 여 hello 서비스 패브릭 관리자 시스템 서비스 toodisable 복구 또는 hello 노드를 사용 하도록 설정 및 상태 확인을 수행 합니다. hello 패치 오케스트레이션 앱 트랙 hello 각 노드에 대 한 Windows Update 진행률 만든 hello 복구 작업입니다.

## <a name="prerequisites"></a>필수 조건

### <a name="minimum-supported-service-fabric-runtime-version"></a>지원되는 최소 Service Fabric 런타임 버전

#### <a name="azure-clusters"></a>Azure 클러스터
서비스 패브릭 런타임에서 버전 v 5.5 Azure 클러스터에서 실행 해야 하는 hello 패치 오케스트레이션 앱 이상.

#### <a name="standalone-on-premises-clusters"></a>독립 실행형 온-프레미스 클러스터
서비스 패브릭 런타임에서 버전 v5.6 있는 독립 실행형 클러스터에서 실행 해야 하는 hello 패치 오케스트레이션 앱 이상.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>(아직 실행 되지 않는) 하는 경우에 hello 복구 관리자 서비스를 사용 하도록 설정

hello 패치 오케스트레이션 앱 hello 복구 관리자 시스템 서비스 toobe hello 클러스터에서 사용 하도록 설정 해야 합니다.

#### <a name="azure-clusters"></a>Azure 클러스터

Hello 은색 내구성 계층에 azure 클러스터에는 hello 복구 관리자 서비스를 기본적으로 사용 해야 합니다. Hello 골드 내구성 계층에 azure 클러스터 수 또는 hello 복구 관리자 서비스는 클러스터가 작성 된 경우에 따라 사용할 수 없을 수 있습니다. 기본적으로 hello 브론즈 내구성 계층에서 azure 클러스터 복구 관리자 서비스를 사용 하는 hello가 필요는 없습니다. Hello 서비스를 사용 하는 이미 실행 hello 서비스 패브릭 탐색기 hello 시스템 서비스 섹션에서 볼 수 있습니다.

##### <a name="azure-portal"></a>Azure portal
클러스터의 설정 hello 시 Azure 포털에서 복구 관리자를 설정할 수 있습니다. 선택 `Include Repair Manager` 옵션에서 `Add on features` hello 시 클러스터 구성.
![Azure Portal에서 복구 관리자 사용 이미지](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Azure Resource Manager 템플릿
Hello 또는 사용할 수 있습니다 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello 복구 관리자 서비스 신규 및 기존 서비스 패브릭 클러스터에 있습니다. 원하는 toodeploy hello 클러스터에 대 한 hello 서식 파일을 가져옵니다. Hello 예제 서식 파일을 사용 하거나 사용자 지정 리소스 관리자 템플릿을 만들 수 있습니다. 

tooenable hello 복구 관리자 서비스를 사용 하 여 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. 먼저 해당 hello 확인 `apiversion` 너무 설정`2017-07-01-preview` hello에 대 한 `Microsoft.ServiceFabric/clusters` 리소스를 hello 다음 코드 조각에에서 나와 있는 것 처럼 합니다. 다를 경우 tooupdate hello 필요한 `apiVersion` toohello 값 `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Hello 다음을 추가 하 여 hello 복구 관리자 서비스를 사용 하는 이제 `addonFeatures` hello 후 섹션 `fabricSettings` 섹션:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. 클러스터 서식 파일을 이러한 변경 내용으로 업데이트 한 후에 적용 하 고 hello 업그레이드를 완료 합니다. 이제 클러스터에서 실행 하는 hello 복구 관리자 시스템 서비스를 볼 수 있습니다. 호출 될 `fabric:/System/RepairManagerService` hello 서비스 패브릭 탐색기 hello 시스템 서비스 섹션에 있습니다. 

### <a name="standalone-on-premises-clusters"></a>독립 실행형 온-프레미스 클러스터

Hello를 사용할 수 있습니다 [독립 실행형 Windows 클러스터에 대 한 구성 설정을](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello 복구 관리자 서비스 신규 및 기존 서비스 패브릭 클러스터를 합니다.

tooenable hello 복구 관리자 서비스:

1. 먼저 해당 hello 확인 `apiversion` 에 [일반 클러스터 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) 너무 설정`04-2017` 이상:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Hello 다음을 추가 하 여 복구 관리자 서비스를 사용 하는 이제 `addonFeaturres` hello 후 섹션 `fabricSettings` 아래와 같이 섹션:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. 클러스터 매니페스트를 업데이트 하는 hello 클러스터 매니페스트를 사용 하 여 이러한 변경 내용으로 업데이트 [새 클러스터를 만들](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) 또는 [업그레이드 hello 클러스터 구성](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration)합니다. 업데이트 된 클러스터 매니페스트가 있는 hello 클러스터를 실행 하 고 볼 수 있습니다 hello 복구 관리자 시스템 서비스가 호출 하 여 클러스터에서 실행 되 고 `fabric:/System/RepairManagerService`아래에서 서비스 섹션 hello 서비스 패브릭 탐색기에서 시스템.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>모든 노드에서 자동 Windows 업데이트 사용 안 함

여러 개의 클러스터 노드를 다시 시작할 수 hello에서 동일 하기 때문에 Windows 자동 업데이트 tooavailability 손실이 발생할 수 있습니다 시간입니다. hello 패치 오케스트레이션 앱 시도 toodisable 기본적으로 각 클러스터 노드에서 Windows 업데이트 자동 hello 합니다. 그러나 경우 hello 설정을 관리자 또는 그룹 정책 관리, 정책 너무 "알림 다운로드 하기 전에" 명시적으로 Windows Update 설정을 hello 보세요.

### <a name="optional-enable-azure-diagnostics"></a>선택 사항: Azure 진단 사용

Service Fabric 런타임 버전 `5.6.220.9494` 이상을 실행하는 클러스터는 Service Fabric 로그의 일부로 패치 오케스트레이션 앱 로그를 수집합니다.
클러스터가 Service Fabric 런타임 버전 `5.6.220.9494` 이상에서 실행 중인 경우 이 단계를 건너뛸 수 있습니다.

서비스 패브릭 런타임 버전을 실행 하는 클러스터에 대 한 보다 작은 `5.6.220.9494`, 각 클러스터 노드에서 hello hello 패치 오케스트레이션 응용 프로그램에 대 한 로그는 로컬로 수집 됩니다.
모든 노드 tooa 중앙 위치에서 Azure 진단 tooupload 로그를 구성 하는 것이 좋습니다.

Azure 진단을 사용하도록 설정하는 방법에 대한 자세한 내용은 [Azure 진단을 사용하여 로그 수집](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad)을 참조하세요.

Hello 패치 오케스트레이션 응용 프로그램에 대 한 로그 Id 공급자를 고정 하는 hello에 생성 됩니다.

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

리소스 관리자 템플릿 goto에서 `EtwEventSourceProviderConfiguration` 섹션 아래 `WadCfg` hello 다음 항목을 추가 합니다.

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> 서비스 패브릭 클러스터에 여러 노드 유형에 경우 모든 hello에 대 한 hello 이전 섹션을 추가 해야 `WadCfg` 섹션.

## <a name="download-hello-app-package"></a>Hello 응용 프로그램 패키지를 다운로드 합니다.

Hello에서 hello 응용 프로그램을 다운로드 [다운로드 링크](https://go.microsoft.com/fwlink/P/?linkid=849590)합니다.

## <a name="configure-hello-app"></a>Hello 응용 프로그램 구성

hello hello 패치 오케스트레이션 응용 프로그램의 동작 구성된 toomeet 사용자 요구 될 수 있습니다. 응용 프로그램 만들기 또는 업데이트 중 hello 응용 프로그램 매개 변수를 전달 하 여 hello 기본값을 재정의 합니다. 응용 프로그램 매개 변수를 지정 하 여 제공 될 수 있습니다 `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` 또는 `New-ServiceFabricApplication` cmdlet.

|**매개 변수**        |**형식**                          | **세부 정보**|
|:-|-|-|
|MaxResultsToCache    |long                              | 캐시되어야 하는 Windows 업데이트 결과의 최대 수입니다. <br>기본값은 3000입니다. <br> - 노드 수는 20입니다. <br> - 매월 노드에서 발생하는 업데이트 수는 5입니다. <br> - 작업당 결과 수는 10일 수 있습니다. <br> -지난 3 달 동안 hello에 대 한 결과 저장 되어야 합니다. |
|TaskApprovalPolicy   |열거형 <br> { NodeWise, UpgradeDomainWise }                          |TaskApprovalPolicy는 toobe hello 서비스 패브릭 클러스터 노드 전체 hello 코디네이터 서비스 tooinstall Windows 업데이트에서 사용 하는 hello 정책을 나타냅니다.<br>                         허용되는 값은 다음과 같습니다. <br>                                                           <b>NodeWise</b>. Windows 업데이트가 한 번에 하나의 노드에 설치됩니다. <br>                                                           <b>UpgradeDomainWise</b>. Windows 업데이트가 한 번에 하나의 업그레이드 도메인에 설치됩니다. (최대 hello에서 tooan 업그레이드 도메인에 속하는 모든 hello 노드 이동할 수 있습니다 Windows Update에 대 한.)
|LogsDiskQuotaInMB   |long  <br> (기본값: 1024)               |패치 오케스트레이션 앱 로그의 최대 크기(MB)로, 노드에서 로컬로 유지될 수 있습니다.
| WUQuery               | string<br>(기본값: "IsInstalled = 0")                | 쿼리 tooget 창을 업데이트합니다. 자세한 내용은 [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)를 참조하세요.
| InstallWindowsOSOnlyUpdates | Bool <br> (기본값: True)                 | 이 플래그는 Windows를 운영 체제 업데이트 toobe 설치 되어 사용할 수 있습니다.            |
| WUOperationTimeOutInMinutes | int <br>(기본값: 90)                   | 모든 Windows 업데이트 작업 (예: 검색 또는 다운로드 또는 설치)에 대 한 hello 제한 시간을 지정합니다. Hello 작업 내에서 완료 되지 않은 경우 지정 된 시간 제한 hello, 중단 됩니다.       |
| WURescheduleCount     | int <br> (기본값: 5)                  | hello 최대 횟수 hello 서비스 다시 예약 하기 위해 hello 작업이 지속적으로 실패 하는 경우 Windows 업데이트 합니다.          |
| WURescheduleTimeInMinutes | int <br>(기본값: 30) | 서비스는 hello에 hello를 다시 예약 하는 hello 간격 오류가 계속 발생 하는 경우 Windows 업데이트 합니다. |
| WUFrequency           | 쉼표로 구분된 문자열(기본값: "매주, 수요일, 7시")     | Windows 업데이트를 설치 하기 위한 hello 빈도입니다. hello 형식 및 가능한 값은 같습니다. <br>-   매월, DD,HH:MM:SS(예: 매월, 5,12:22:32) <br> -   매주, DAY,HH:MM:SS(예: 매주, 화요일, 12:22:32)  <br> -   매일, HH:MM:SS(예: 매일, 12:22:32)  <br> -   [없음]은 Windows 업데이트를 수행하지 않음을 나타냅니다.  <br><br> Hello 항상 UTC에 있는지 확인 합니다.|
| AcceptWindowsUpdateEula | Bool <br>(기본값: True) | 이 플래그를 설정 하 여 hello 응용 프로그램 hello 컴퓨터의 hello 소유자를 대신 하 여 hello Windows Update에 대 한 최종 사용자 사용권 계약을 허용 합니다.              |

> [!TIP]
> 설정 하려는 경우 Windows Update toohappen 즉시, `WUFrequency` 상대 toohello 응용 프로그램 배포 시간입니다. 예를 들어, 약 오후 5시는 테스트 다섯 개 노드 클러스터와 계획 toodeploy hello 앱 있는지 UTC입니다. Hello 응용 프로그램 업그레이드 또는 배포에서 30 분 소요를 가정 하는 경우 "매일 17시 30분: 00입니다."로 설정 하 고 최대 hello WUFrequency hello

## <a name="deploy-hello-app"></a>Hello 앱 배포

1. 모든 hello 사전 요구 사항 단계 tooprepare hello 클러스터를 완료 합니다.
2. 서비스 패브릭 응용 프로그램 처럼 hello 패치 오케스트레이션 앱을 배포 합니다. PowerShell을 사용 하 여 hello 앱을 배포할 수 있습니다. Hello 단계에 따라 [PowerShell을 사용 하 여 배포 및 제거 응용 프로그램](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)합니다.
3. 패스 hello 배포의 hello 시 tooconfigure hello 응용 프로그램 `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet. 사용자 편의 위해 hello 스크립트 Deploy.ps1 hello 응용 프로그램과 함께 제공 했습니다. toouse hello 스크립트:

    - Tooa 서비스 패브릭 클러스터를 사용 하 여 연결 `Connect-ServiceFabricCluster`합니다.
    - 적절 한 hello로 hello PowerShell 스크립트 Deploy.ps1 실행 `ApplicationParameter` 값입니다.

> [!NOTE]
> Hello 스크립트와 hello 응용 프로그램 폴더 PatchOrchestrationApplication hello에 유지 동일한 디렉터리입니다.

## <a name="upgrade-hello-app"></a>Hello 응용 프로그램 업그레이드

PowerShell을 사용 하 여 기존 패치 오케스트레이션 앱 tooupgrade hello 단계에 따라 [PowerShell을 사용 하 여 서비스 패브릭 응용 프로그램 업그레이드](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell)합니다.

## <a name="remove-hello-app"></a>Hello 앱 제거

다음 단계에서 수행 hello tooremove hello 응용 프로그램 [PowerShell을 사용 하 여 배포 및 제거 응용 프로그램](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)합니다.

사용자 편의 위해 hello 스크립트 Undeploy.ps1 hello 응용 프로그램과 함께 제공 했습니다. toouse hello 스크립트:

  - Tooa 서비스 패브릭 클러스터를 사용 하 여 연결 ```Connect-ServiceFabricCluster```합니다.

  - Undeploy.ps1 hello PowerShell 스크립트를 실행 합니다.

> [!NOTE]
> Hello 스크립트와 hello 응용 프로그램 폴더 PatchOrchestrationApplication hello에 유지 동일한 디렉터리입니다.

## <a name="view-hello-windows-update-results"></a>Hello Windows Update 결과 보기

hello 패치 오케스트레이션 앱 REST Api toodisplay hello 기록 결과 toohello 사용자를 표시합니다. Hello 결과 JSON의 예:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
업데이트가 아직 예약 hello 결과 JSON 비어 있습니다.

결과 toohello 클러스터 tooquery Windows Update에에서 로그인 합니다. 그런 다음 hello Coordinator 서비스의 기본 hello에 대 한 hello 복제 주소를 확인 하 고 hello 브라우저에서 URL hello 적중: http://&lt;복제본 IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v 1 / GetWindowsUpdateResults 합니다.

hello 코디네이터 서비스에 대 한 hello REST 끝점에는 동적 포트를 있습니다. toocheck 정확한 URL hello, toohello 서비스 패브릭 탐색기를 참조 하십시오. 예를 들어 hello 결과에서 제공 됩니다 `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`합니다.

![REST 끝점의 이미지](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Hello 역방향 프록시 hello 클러스터에서 활성화 된 경우에 hello 클러스터 외부에서 hello URL을 액세스할 수 있습니다.
끝점에 필요한 toobe hello 적중은 http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults 합니다.

hello 클러스터에서 tooenable hello 역방향 프록시 hello 단계에 따라 [역방향 프록시 Azure 서비스 패브릭에서](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)합니다. 

> 
> [!WARNING]
> Hello 역방향 프록시를 구성한 후에 HTTP 끝점을 노출 하는 hello 클러스터의 모든 마이크로 서비스는 hello 클러스터 외부에서 주소 지정 가능 합니다.

## <a name="diagnosticshealth-events"></a>진단/상태 이벤트

### <a name="collect-patch-orchestration-app-logs"></a>패치 오케스트레이션 앱 로그 수집

런타임 버전 `5.6.220.9494` 이상에서는 Service Fabric 로그의 일부로 패치 오케스트레이션 앱 로그가 수집됩니다.
서비스 패브릭 런타임 버전을 실행 하는 클러스터에 대 한 보다 작은 `5.6.220.9494`, hello 메서드를 다음 중 하나를 사용 하 여 로그를 수집할 수 있습니다.

#### <a name="locally-on-each-node"></a>각 노드에 로컬로

Service Fabric 런타임 버전이 `5.6.220.9494` 미만인 경우 각 Service Fabric 클러스터 노드에서 로그가 로컬로 수집됩니다. hello tooaccess hello 로그 위치는 \[서비스 패브릭\_설치\_드라이브\]:\\PatchOrchestrationApplication\\로그 합니다.

예를 들어 서비스 패브릭 D 드라이브에 설치 된 경우 hello 경로 d:\\PatchOrchestrationApplication\\로그 합니다.

#### <a name="central-location"></a>중앙 위치

Azure 진단을 사전 요구 사항 단계의 일부로 구성 된 경우에 hello 패치 오케스트레이션 응용 프로그램에 대 한 로그는 Azure 저장소에서 사용할 수입니다.

### <a name="health-reports"></a>상태 보고서

hello 패치 오케스트레이션 응용 프로그램의 경우 다음 hello에 엔터티에도 hello 코디네이터 서비스 또는 hello 노드 에이전트 서비스에 대 한 상태 보고서:

#### <a name="a-windows-update-operation-failed"></a>Windows 업데이트 작업 실패

노드에서 Windows 업데이트 작업이 실패 하면 hello 노드 에이전트 서비스에 대 한 상태 보고서가 생성 됩니다. Hello 상태 보고서의 정보는 hello 문제가 있는 노드 이름을 포함합니다.

패치 hello 문제가 있는 노드에서 성공적으로 완료 되 면 후 hello 보고서 자동으로 지워집니다.

#### <a name="hello-node-agent-ntservice-is-down"></a>hello 노드 에이전트 NTService 다운 되었습니다.

Hello 노드 에이전트 NTService 노드에서 다운 되는 경우 경고 수준 상태 보고서는 hello 노드 에이전트 서비스에 대해 생성 됩니다.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>hello 복구 관리자 서비스는 사용할 수 없습니다.

Hello 복구 관리자 서비스는 hello 클러스터에서 찾을 수 없습니다, hello 코디네이터 서비스에 대 한 경고 수준 상태 보고서 생성 됩니다.

## <a name="frequently-asked-questions"></a>질문과 대답

Q. **Hello 패치 오케스트레이션 응용 프로그램을 실행 하는 경우 오류 상태에 클러스터 나타나는 이유는 무엇입니까?**

A. Hello 설치 과정에서 hello 패치 오케스트레이션 응용 프로그램을 선택 하거나 일시적으로 중지 될 hello 클러스터의 hello 상태에서 발행할 수 있는 노드를 다시 시작 합니다.

Hello 응용 프로그램에 대 한 hello 정책에 따라, 어느 한 노드에서 감소할 수 있습니다 패치 작업 중 *또는* 전체 업그레이드 도메인 동시에 감소할 수 있습니다.

Windows Update 설치 hello 끝날 때 hello, 노드는 다시 사용 하도록 설정 하는 hello 다시 시작을 게시 합니다.

다음 예제는 hello, hello 클러스터 tooan 오류 상태가 일시적으로 두 노드는 감소 하 고 hello MaxPercentageUnhealthNodes 정책 때문에 위반 했습니다. 패치 작업 hello 진행 될 때까지 hello 오류는 일시적입니다.

![비정상 클러스터의 이미지](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Hello 문제가 지속 되 면 toohello 문제 해결 섹션을 참조 하십시오.

Q. **패치 오케스트레이션 앱이 경고 상태입니다.**

A. Toosee hello 응용 프로그램에 대해 게시 된 상태 보고서가 hello 근본 원인을 확인 합니다. 일반적으로 hello 경고 hello 문제에 대 한 세부 정보를 포함합니다. Hello 문제가 일시적인 경우 hello 응용 프로그램은이 상태에서 예상된 tooauto 복구 합니다.

Q. **클러스터 손상 되었습니다. toodo 긴급 한 운영 체제 업데이트 해야 하는 경우 어떻게 해야 합니까?**

A. 반면 hello 클러스터는 정상인 hello 패치 오케스트레이션 앱 업데이트를 설치 하지 않습니다. 클러스터 tooa 정상 상태로 toounblock hello 패치 오케스트레이션 응용 프로그램 워크플로 toobring를 시도 하십시오.

Q. **이유는 클러스터 간에 패치 시간이 너무 오래 toorun?**

A. hello 패치 오케스트레이션 응용 프로그램에 필요한 hello 시간은 주로 hello 요소 뒤에 종속 됩니다.

- hello Coordinator 서비스의 hello 정책입니다. 
  - 기본 정책 hello `NodeWise`, 한 번에 하나의 노드만 패치 발생 합니다. 특히, 더 큰 클러스터의 hello 경우의에서 hello를 사용 하는 권장 `UpgradeDomainWise` 정책 tooachieve 빠른 클러스터 간에 패치를 적용 합니다.
- 업데이트 다운로드 및 설치에 사용할 수 있는 hello 수입니다. 
- 필요한 평균 시간 toodownload hello 하 고 몇 시간을 초과 하지 않아야 하는 업데이트를 설치 합니다.
- hello VM 및 네트워크 대역폭의 hello 성능입니다.

Q. **Windows Update 결과에 포함 되지 않은 컴퓨터에서 Windows Update 기록 hello 하지만 REST api를 통해 얻은에서 일부 업데이트가 나타나는 이유는 무엇입니까?**

A. 일부 제품 업데이트 해당 업데이트/패치 기록을 체크인 toobe가 필요 합니다. 예: Windows Defender 업데이트는 Windows Server 2016의 Windows 업데이트에서 표시되지 않습니다.

## <a name="disclaimers"></a>고지 사항

- hello 패치 오케스트레이션 앱 hello 사용자를 대신 하 여 hello Windows Update의 최종 사용자 사용권 계약을 수락합니다. 필요에 따라 hello 응용 프로그램의 hello 구성에서 hello 설정을 설정할 수 있습니다.

- hello 패치 오케스트레이션 앱 원격 분석 tootrack 사용량 및 성능 수집합니다. hello 응용 프로그램의 원격 분석 hello 서비스 패브릭 런타임 원격 분석 설정 (기본적으로 켜져)의 hello 설정을 따릅니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="a-node-is-not-coming-back-tooup-state"></a>노드 다시 발생 하지 않습니다 tooup 상태

**hello 노드 때문에 비활성화 된 상태에서 멈춰 있을 수 있습니다**:

안전 검사가 보류 중입니다. tooremedy 이러한 상황을 정상 상태로 사용할 수 있는 충분 한 노드가 있는지 확인 합니다.

**hello 노드 때문에 사용할 수 없는 상태에서 멈춰 있을 수 있습니다**:

- hello 노드는 수동으로 비활성화 되었습니다.
- hello 노드 tooan 진행 중인 Azure 인프라 작업 인해 비활성화 되었습니다.
- hello 노드 hello 패치 오케스트레이션 앱 toopatch hello 노드가 일시적으로 비활성화 되었습니다.

**hello 노드 멈춰 있을 수 있습니다 다운 상태에 있으므로**:

- hello 노드가 다운 상태에 수동으로 배치 되었습니다.
- hello 노드 (있음 hello 패치 오케스트레이션 앱에 의해 트리거될 수 있습니다)를 다시 시작이 진행 중입니다.
- hello 노드 tooa 결함이 있는 VM 또는 컴퓨터 또는 네트워크 연결 문제로 인해 작동이 중단 되었습니다.

### <a name="updates-were-skipped-on-some-nodes"></a>일부 노드에서 업데이트를 건너뛰었습니다.

hello 패치 오케스트레이션 앱 tooinstall Windows 업데이트에 따라 toohello 다시 예약 정책 하려고 시도합니다. hello 서비스 toorecover hello 노드를 시도 하 고 hello 업데이트에 따라 toohello 응용 프로그램 정책을 건너 뜁니다.

이 경우 경고 수준 상태 보고서는 hello 노드 에이전트 서비스에 대해 생성 됩니다. Windows Update에 대 한 hello 결과는 hello 실패에 대 한 가능한 이유 hello 포함 되어 있습니다.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>hello 클러스터의 hello 상태 보내고 tooerror hello 업데이트 설치

잘못 된 Windows update 응용 프로그램 또는 특정 노드 또는 업그레이드 도메인에 있는 클러스터의 hello 상태를 가져올 수 있습니다. hello 패치 오케스트레이션 앱 hello 클러스터가 다시 정상 상태가 될 때까지 후속 Windows 업데이트 작업을 중단 합니다.

관리자가 개입 하 고 이유 hello 응용 프로그램 또는 클러스터 비정상이 된 인해 결정 해야 tooWindows 업데이트 합니다.

## <a name="release-notes-"></a>릴리스 정보:

### <a name="version-110"></a>버전 1.1.0
- 공개 릴리스

### <a name="version-111"></a>버전 1.1.1
- NodeAgentNTService의 설치를 방지하는 NodeAgentService의 SetupEntryPoint에서 버그 수정

### <a name="version-120-latest"></a>버전 1.2.0(최신)

- 시스템 다시 시작 워크플로 관련 버그 수정
- 만들 복구 작업을 준비 하는 동안 toowhich 상태 검사에 예정 된 RM 작업의에서 버그 수정 예상 대로 발생 되지 않았습니다.
- Windows 서비스 POANodeSvc 자동 toodelayed 자동에서 변경 된 hello 시작 모드입니다.
