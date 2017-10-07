---
title: "Windows Azure 진단으로 서비스 패브릭 이벤트 집계 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터 모니터링 및 진단을 위해 MAD를 사용하여 이벤트를 집계 및 수집하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Miscrosoft Azure 진단을 사용하여 이벤트 집계 및 수집
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Azure 서비스 패브릭 클러스터를 실행 하는 경우 중앙 위치에 있는 모든 hello 노드에서 것이 좋습니다 toocollect hello가 있습니다. Hello 로그를 중앙 위치에 있는 분석 및 클러스터의 문제 또는 hello 응용 프로그램 및 해당 클러스터에서 실행 되는 서비스의 문제를 해결 하는 데 도움이 됩니다.

한 가지 방법은 tooupload 및 수집 로그는 로그 tooAzure 저장소에 업로드 하 고 hello 옵션 toosend 로그 tooAzure Application Insights 또는 이벤트 허브에는 toouse hello Windows WAD (Azure 진단) 확장입니다. 저장소에서 외부 프로세스 tooread hello 이벤트를 사용 하 고와 같은 분석 플랫폼 제품에 배치할 수도 있습니다 [OMS 로그 분석](../log-analytics/log-analytics-service-fabric.md) 또는 다른 로그 구문 분석 솔루션입니다.

## <a name="prerequisites"></a>필수 조건
이러한 도구는 사용 되는 tooperform hello 작업이 문서의 일부를 수행 합니다.

* [Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) (관련 클라우드 서비스 tooAzure 않았으나 좋은 정보 및 예제)
* [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager 클라이언트](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager 템플릿](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>로그 및 이벤트 원본

### <a name="service-fabric-platform-events"></a>Service Fabric 플랫폼 이벤트
에 설명 된 대로 [이 여기서](service-fabric-diagnostics-event-generation-infra.md), 서비스 패브릭 설정 하면 기본적으로 로깅 채널의 몇 가지, hello는 다음과 같은 채널은 쉽게 구성 WAD toosend 모니터링 및 진단 데이터 tooa 저장소 테이블 또는 다른 곳에서:
  * 작업 이벤트: hello 서비스 패브릭 플랫폼을 수행 하는 상위 수준 작업입니다. 응용 프로그램 및 서비스 만들기, 노드 상태 변경, 업그레이드 정보 등을 예로 들 수 있습니다. 이러한 이벤트를 ETW(Windows용 이벤트 추적) 로그로 내보냅니다.
  * [Reliable Actors 프로그래밍 모델 이벤트](service-fabric-reliable-actors-diagnostics.md)
  * [Reliable Services 프로그래밍 모델 이벤트](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>응용 프로그램 이벤트
 Hello에 Visual Studio 템플릿 제공 하는 이벤트 hello EventSource 도우미 클래스를 사용 하 여 기록 및 응용 프로그램 및 서비스의 코드에서 내보내집니다. EventSource toowrite 응용 프로그램에서 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [모니터 하 고 서비스는 로컬 컴퓨터 개발 설정에서 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)합니다.

## <a name="deploy-hello-diagnostics-extension"></a>Hello 진단 확장 배포
로그를 수집 hello 첫 번째 단계는 hello 서비스 패브릭 클러스터에 있는 hello Vm의 각 toodeploy hello 진단 확장입니다. hello 진단 확장 각 VM에서 로그를 수집 하 고 사용자가 지정한 toohello 저장소 계정으로 업로드 합니다. hello 단계 hello Azure 포털 또는 Azure 리소스 관리자를 사용 하는 여부에 따라 약간 다릅니다. 또한 hello 단계 hello 배포의 클러스터 생성의 일부 인지 또는 이미 존재 하는 클러스터에 대 한 인지에 따라 달라 집니다. 각 시나리오에 대 한 hello 단계를 살펴 보겠습니다.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Azure 포털을 통해 클러스터 만들기의 일부로 hello 진단 확장 배포
hello 다음에 표시 된 hello 진단 설정 패널을 사용 하면 toodeploy hello 진단 확장 toohello Vm 클러스터 만들기의 일부로 hello 클러스터의, 이미지-진단 너무 설정 되어 있는지 확인**에** (기본 설정 hello) . Hello 클러스터를 만드는 hello 포털을 사용 하 여 이러한 설정을 변경할 수 없습니다.

![클러스터 만들기에 대 한 hello 포털의 azure 진단 설정](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Hello 포털을 사용 하 여 클러스터를 만들 때 매우 권장 hello 서식 파일을 다운로드 하는 **클릭 하기 전에** toocreate hello 클러스터입니다. 자세한 내용은 참조 너무[Azure 리소스 관리자 템플릿을 사용 하 여 서비스 패브릭 클러스터를 설정](service-fabric-cluster-creation-via-arm.md)합니다. 일부 변경 내용은 hello 포털을 사용 하 여 변경할 수 없으므로 나중 hello 템플릿 toomake 변경 필요 합니다.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Azure 리소스 관리자를 사용 하 여 클러스터 생성의 일환으로 hello 진단 확장을 배포 합니다.
리소스 관리자를 사용 하 여 클러스터 toocreate 있어야만 tooadd hello 진단 구성 JSON toohello 전체 클러스터 리소스 관리자 템플릿 hello 클러스터를 만듭니다. 추가 진단 구성을 사용 하 여 샘플 5-V 클러스터 리소스 관리자 템플릿을 제공 tooit 리소스 관리자 템플릿 샘플의 일부분으로 합니다. 이 위치 hello Azure 샘플 갤러리에서 확인할 수 있습니다.: [진단 리소스 관리자 템플릿 샘플 5 개 노드 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad)합니다.

hello 리소스 관리자 템플릿, 열기 hello azuredeploy.json 파일 및 검색에서 toosee hello 진단 설정을 **IaaSDiagnostics**합니다. 이 서식 파일을 선택 하는 hello를 사용 하 여 클러스터 toocreate **tooAzure 배포** hello 이전 링크에서 사용할 수 있는 단추입니다.

또는 hello 리소스 관리자 예제 추가 정보 다운로드, 변경 내용을 tooit 만들고 수 hello를 사용 하 여 hello 수정 된 템플릿을 사용 하 여 클러스터를 만들 `New-AzureRmResourceGroupDeployment` Azure PowerShell 창에서 명령을 합니다. Hello toohello 명령에 전달 하는 hello 매개 변수에 대 한 코드 다음을 참조 하십시오. PowerShell을 사용 하 여 리소스 toodeploy 그룹화 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [hello Azure 리소스 관리자 템플릿 사용 하 여 리소스 그룹 배포](../azure-resource-manager/resource-group-template-deploy.md)합니다.

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Hello 진단 확장 tooan 기존 클러스터 배포
기존 클러스터를 배포 하는 진단이 없는 경우 또는 toomodify 기존 구성 하려는 경우 추가 하거나 업데이트할 수 있습니다. Hello 리소스 관리자 템플릿을 사용 하는 toocreate hello 기존 클러스터를 수정 하거나 hello 템플릿을 앞에서 설명한 대로 hello 포털에서 다운로드 합니다. Hello 다음 작업을 수행 하 여 hello template.json 파일을 수정 합니다.

Toohello 리소스 섹션을 추가 하 여 새 저장소 리소스 toohello 서식 파일을 추가 합니다.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 다음으로, 중간 hello 저장소 계정 정의 바로 뒤 섹션 toohello 매개 변수를 추가 `supportLogStorageAccountName` 및 `vmNodeType0Name`합니다. Hello 개체 틀 텍스트 바꾸기 *저장소 계정 이름 입력* hello hello 저장소 계정의 이름으로 사용 합니다.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
그런 다음 업데이트 hello `VirtualMachineProfile` hello 코드 hello 확장 배열 내에서 다음을 추가 하 여 hello template.json 파일의 섹션입니다. 있는지 tooadd hello 시작 이나 삽입 되는 위치에 따라 hello 끝 쉼표 수 있습니다.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

설명 된 대로 hello template.json 파일을 수정한 후에 hello 리소스 관리자 템플릿을 다시 게시 합니다. Hello 서식 파일을 내보낸 경우 실행 중인 hello deploy.ps1 파일 hello 템플릿을 다시 게시 합니다. 배포 후에는 **ProvisioningState**가 **성공**했는지 확인합니다.

## <a name="collect-health-and-load-events"></a>상태 및 부하 이벤트 수집

릴리스부터 hello 5.4 서비스 패브릭의 상태 및 부하 메트릭 이벤트는 컬렉션에 사용할 수 있습니다. 이러한 이벤트 hello 상태를 사용 하 여 hello 시스템 또는 사용자 코드에 의해 생성 된 이벤트를 반영 하거나 보고 Api와 같은 로드 [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) 또는 [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx)합니다. 이를 통해 시간 경과에 따른 시스템 상태의 집계 및 확인과 상태 또는 부하 이벤트 기반의 경고가 가능합니다. 이러한 Visual Studio의 진단 이벤트 뷰어의이 이벤트에에서 추가 tooview "Microsoft-ServiceFabric:4:0x4000000000000008" toohello ETW 공급자 목록입니다.

toocollect hello 이벤트 hello 리소스 관리자 템플릿 tooinclude 수정

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>역방향 프록시 이벤트 수집

서비스 패브릭의 hello 5.7 릴리스에서 [역방향 프록시](service-fabric-reverseproxy.md) 이벤트는 컬렉션에 대해 사용할 수 있습니다.
역방향 프록시 포함 하는 하나의 오류 두 개의 채널에 이벤트를 내보냅니다 반영 하는 이벤트 처리 오류를 요청 하 고 다른 하나 hello 역방향 프록시에서 처리 하는 모든 hello 요청에 대 한 자세한 정보 표시 이벤트에 포함 된 hello 합니다. 

1. 오류 이벤트 수집: tooview 이러한 Visual Studio의 진단 이벤트 뷰어의이 이벤트에에서 추가 "Microsoft-ServiceFabric:4:0x4000000000000010" toohello ETW 공급자 목록입니다.
Azure의 클러스터에서 toocollect hello 이벤트 hello 리소스 관리자 템플릿 tooinclude 수정

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. 처리 중인 이벤트의 모든 요청 수집:에서 Visual Studio의 진단 이벤트 뷰어, 업데이트 hello Microsoft ServiceFabric 항목 hello ETW 공급자 목록이 너무 "Microsoft-ServiceFabric:4:0x4000000000000020"입니다.
Azure 서비스 패브릭 클러스터에 대 한 hello 리소스 관리자 템플릿 tooinclude 수정

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> Hello 역방향 프록시를 통해 모든 트래픽을 수집할지이 고 저장소 용량을 소비 신속 하 게 수 toojudiciously이이 채널에서 수집할 이벤트 기능 설정 좋습니다.

Azure 서비스 패브릭 클러스터에 대 한 모든 hello 노드에서 hello 이벤트 수집 및 SystemEventTable hello에 집계 합니다.
상세한 hello 역방향 프록시 이벤트의 문제 해결, 참조 hello [역방향 프록시 진단 가이드](service-fabric-reverse-proxy-diagnostics.md)합니다.

## <a name="collect-from-new-eventsource-channels"></a>새 EventSource 채널에서 수집

tooupdate 진단 toocollect 로그 toodeploy에 대 한 사용자가 있는 새 응용 프로그램을 나타내는 새 EventSource 채널에서 기존 클러스터에 대 한 진단의 hello 설치에 대 한 hello 앞에서 설명한 동일한 단계를 수행 합니다.

Hello 업데이트 `EtwEventSourceProviderConfiguration` hello 새로운 EventSource 채널 hello 구성을 적용 하기 전에 hello를 사용 하 여 업데이트에 대 한 hello template.json 파일 tooadd 항목 섹션 `New-AzureRmResourceGroupDeployment` PowerShell 명령입니다. hello 이벤트 소스의 hello 이름 hello ServiceEventSource.cs Visual Studio에서 생성 된 파일에 코드의 일부로 정의 됩니다.

예를 들어 이벤트 원본이 Eventsource 내 이름이 이면 hello MyDestinationTableName 라는 테이블로 tooplace hello 이벤트 코드 Eventsource 내에서 다음을 추가 합니다.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

toocollect 성능 카운터 또는 이벤트 로그에서 제공 하는 hello 예제를 사용 하 여 hello 리소스 관리자 템플릿을 수정 [는Azure리소스관리자템플릿을사용하여Windows가상컴퓨터를모니터링및진단을작성](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 그런 다음 hello 리소스 관리자 템플릿을 다시 게시 합니다.

## <a name="collect-performance-counters"></a>성능 카운터 수집

클러스터에서 toocollect 성능 메트릭을 클러스터에 대 한 리소스 관리자 템플릿을 hello에 hello 성능 카운터 tooyour "WadCfg > DiagnosticMonitorConfiguration"를 추가 합니다. 수집을 권장하는 성능 카운터에 대해서는 [Service Fabric 성능 카운터](service-fabric-diagnostics-event-generation-perf.md)를 참조하세요.

예를 들어 하나의 성능 카운터를 15 초 마다 샘플링 설정 여기 (이 변경 될 수 있으며 다음과 hello의 형식을 "PT\<시간 >\<단위 >"를 3 분 간격으로 PT3M 샘플은 예를 들어), toohello 전송 해당 하는 저장소 테이블 1 분 간격입니다.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
아래의 hello 섹션에 설명 된 대로 Application Insights 싱크를 사용 하는 경우 Application Insights에서 이러한 메트릭 tooshow를 원하는 위와 같이 hello "싱크" 섹션에 tooadd hello 싱크 이름이 있는지 확인 합니다. 또한 만드는 것이 좋습니다 별도 테이블 toosend 성능 카운터 hello 아웃 복잡해 지지 하지 하므로에서 가져온 데이터 hello 다른 로깅 채널을 설정한 상태 여야 합니다.


## <a name="send-logs-tooapplication-insights"></a>송신은 tooApplication 정보를 기록합니다.

모니터링 및 진단 데이터 tooApplication Insights (AI) 보내는 hello WAD 구성의 일부분으로 수행할 수 있습니다. 이벤트 분석 및 시각화에 대 한 AI toouse 결정 한 경우 확인 [이벤트 분석 및 Application Insights를 사용한 시각화](service-fabric-diagnostics-event-analysis-appinsights.md) tooset "WadCfg"의 일부로 AI 싱크를 합니다.

## <a name="next-steps"></a>다음 단계

Azure 진단을 올바르게 구성한 hello ETW 및 EventSource 로그에서 저장소 테이블에 데이터 표시 됩니다. OMS toouse을 선택 하면 Kibana, 또는 다른 데이터 분석 및 시각화 플랫폼 hello 리소스 관리자 서식 파일에서 직접 구성 되지 않은 hello 테이블의 데이터를 이러한 저장소에 있는지 tooset 선택 tooread의 hello 플랫폼을 확인 합니다. OMS에 대해 이 작업을 수행하는 방법은 비교적 간단하고 [OMS를 통해 이벤트 및 로그 분석](service-fabric-diagnostics-event-analysis-oms.md)에서 설명됩니다. Application Insights는 이런이 의미에서 특별 한 경우의 비트, toohello 참조 하도록 hello 진단 확장 구성의 일부로 구성할 수 있습니다, 때문 [적절 한 문서](service-fabric-diagnostics-event-analysis-appinsights.md) toouse AI를 선택 합니다.

>[!NOTE]
>Ľ ř ˝ 방법은 toofilter 또는 그루 밍 hello 이벤트가 toohello 테이블 전송 됩니다. Hello 테이블에서 프로세스 tooremove 이벤트를 구현 하지 않는 경우 hello 테이블 toogrow를 계속 됩니다. 현재 hello에서 실행 되는 데이터 그루 밍 서비스의 예는 [Watchdog 샘플](https://github.com/Azure-Samples/service-fabric-watchdog-service), 것이 좋습니다 작성 하는 자신에 대 한 하나도 좋은 이유가 있습니다 toostore 로그는 30 또는 90 일의 기간 보다 큰 경우를 제외 합니다.

* [Toocollect 성능 카운터 또는 로그를 사용 하 여 hello 진단 확장 방법에 대해 알아봅니다](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Application Insights를 사용하여 이벤트 분석 및 시각화](service-fabric-diagnostics-event-analysis-appinsights.md)
* [OMS를 사용하여 이벤트 분석 및 시각화](service-fabric-diagnostics-event-analysis-oms.md)