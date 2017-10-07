---
title: "모니터 자동 크기 조정에 대 한 일반 메트릭 aaaAzure | Microsoft Docs"
description: "클라우드 서비스, 가상 컴퓨터 및 웹앱의 자동 크기 조정에 일반적으로 사용되는 메트릭에 대해 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Azure Monitor 자동 크기 조정 공용 메트릭
Azure 모니터의 자동 크기 조정이 있습니다 tooscale hello 실행 중인 인스턴스 수를를 위 또는 아래로 원격 분석 데이터 (메트릭)를 기반으로 합니다. 이 문서에서는 공통 메트릭을 toouse 알았으므로 설명 합니다. Azure 포털 클라우드 서비스 및 서버 팜 hello에 하 여 hello 리소스 tooscale의 hello 메트릭을 선택할 수 있습니다. 그러나 하 여 다른 리소스 tooscale에서 모든 메트릭을 선택할 수도 있습니다.

Azure 모니터의 자동 크기 조정 적용만 너무[가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다. 다른 Azure 서비스에는 다른 크기 조정 방법이 사용됩니다.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Resource Manager 기반 VM용 메트릭 계산
기본적으로 Resource Manager 기반 Virtual Machines 및 Virtual Machine Scale Sets는 기본(호스트 수준) 메트릭을 내보냅니다. 또한 Azure VM 및 VMSS에 대 한 진단 데이터 수집을 구성한 경우 Azure 진단 확장 hello 게스트 OS 성능 카운터를 (일반적으로 "게스트 OS 메트릭" 라고 함)도 내보냅니다.  자동 크기 조정 규칙에서 이러한 모든 메트릭을 사용합니다.

Hello를 사용할 수 있습니다 `Get MetricDefinitions` CLI PoSH/API/tooview hello 메트릭을 VMSS 리소스에 대해 사용할 수 있습니다.

VM 규모 집합을 사용 중인데 특정 메트릭이 목록에 표시되지 않는 경우, 이는 진단 확장에서 *사용하지 않도록 설정*되었을 수 있습니다.

특정 메트릭에 샘플링 또는에서 전송 된 hello 빈도 되 고 있지 않습니다, hello 진단 구성을 업데이트할 수 있습니다.

위의 두 경우 모두 true 이면 다음 검토 [Windows를 실행 하는 가상 컴퓨터에서 PowerShell 사용 하 여 tooenable Azure 진단](../virtual-machines/windows/ps-extensions-diagnostics.md) PowerShell tooconfigure 및 업데이트에 대 한 Azure VM 진단 확장 tooenable hello 메트릭을 합니다. 이 문서에는 샘플 진단 구성 파일도 포함되어 있습니다.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Resource Manager 기반 Windows 및 Linux VM용 호스트 메트릭
다음 호스트 수준 메트릭 hello는 Windows와 Linux의 경우에서 Azure VM 및 VMSS 기본적으로 내보냅니다. 이러한 메트릭은 Azure VM에 설명 하지만 hello 게스트 VM에 설치 된 에이전트를 통해 대신 hello Azure VM 호스트에서 수집 됩니다. 자동 크기 조정 규칙에서 이러한 메트릭을 사용할 수 있습니다.

- [Resource Manager 기반 Windows 및 Linux VM용 호스트 메트릭](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Resource Manager 기반 Windows 및 Linux VM Scale Sets용 호스트 메트릭](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>게스트 OS 메트릭 Resource Manager 기반 Windows VM
Azure에서 VM을 만들 진단 hello 진단 확장을 사용 하 여 활성화 됩니다. hello 진단 확장 hello VM 내부에서 가져온 메트릭 집합을을 내보냅니다. 즉, 기본적으로 내보내지 않도록 메트릭의 자동 크기 조정을 해제할 수 있습니다.

다음 powershell에서 명령을 hello를 사용 하 여 hello 메트릭 목록은 생성할 수 있습니다.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

다음 메트릭 hello에 대 한 경고를 만들 수 있습니다.

| 메트릭 이름 | 단위 |
| --- | --- |
| \Processor(_Total)\% 프로세서 시간 |백분율 |
| \Processor(_Total)\% 시스템 시간 |백분율 |
| \Processor(_Total)\% 사용자 시간 |백분율 |
| \Processor Information(_Total)\Processor Frequency |개수 |
| \System\Processes |개수 |
| \Process(_Total)\Thread Count |개수 |
| \Process(_Total)\Handle Count |개수 |
| \Memory\% 사용 중인 커밋된 바이트 |백분율 |
| \Memory\Available Bytes |바이트 |
| \Memory\Committed Bytes |바이트 |
| \Memory\Commit Limit |바이트 |
| \Memory\Pool Paged Bytes |바이트 |
| \Memory\Pool Nonpaged Bytes |바이트 |
| \PhysicalDisk(_Total)\% 디스크 시간 |백분율 |
| \PhysicalDisk(_Total)\% 디스크 읽기 시간 |백분율 |
| \PhysicalDisk(_Total)\% 디스크 쓰기 시간 |백분율 |
| \PhysicalDisk(_Total)\디스크 전송/초 |초당 개수 |
| \PhysicalDisk(_Total)\Disk Reads/sec |초당 개수 |
| \PhysicalDisk(_Total)\Disk Writes/sec |초당 개수 |
| \PhysicalDisk(_Total)\Disk Bytes/sec |초당 바이트 수 |
| \PhysicalDisk(_Total)\Disk Read Bytes/sec |초당 바이트 수 |
| \PhysicalDisk(_Total)\Disk Write Bytes/sec |초당 바이트 수 |
| \PhysicalDisk(_Total)\Avg. 디스크 큐 길이 |개수 |
| \PhysicalDisk(_Total)\Avg. 디스크 읽기 큐 길이 |개수 |
| \PhysicalDisk(_Total)\Avg. 디스크 쓰기 큐 길이 |개수 |
| \LogicalDisk(_Total)\% 사용 가능한 공간 |백분율 |
| \LogicalDisk(_Total)\Free Megabytes |개수 |

### <a name="guest-os-metrics-linux-vms"></a>게스트 OS 메트릭 Linux VM
Azure에서 VM을 만들 때 진단 확장을 사용하여 기본적으로 진단을 사용하도록 설정합니다.

다음 powershell에서 명령을 hello를 사용 하 여 hello 메트릭 목록은 생성할 수 있습니다.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 다음 메트릭 hello에 대 한 경고를 만들 수 있습니다.

| 메트릭 이름 | 단위 |
| --- | --- |
| \Memory\AvailableMemory |바이트 |
| \Memory\PercentAvailableMemory |백분율 |
| \Memory\UsedMemory |바이트 |
| \Memory\PercentUsedMemory |백분율 |
| \Memory\PercentUsedByCache |백분율 |
| \Memory\PagesPerSec |초당 개수 |
| \Memory\PagesReadPerSec |초당 개수 |
| \Memory\PagesWrittenPerSec |초당 개수 |
| \Memory\AvailableSwap |바이트 |
| \Memory\PercentAvailableSwap |백분율 |
| \Memory\UsedSwap |바이트 |
| \Memory\PercentUsedSwap |백분율 |
| \Processor\PercentIdleTime |백분율 |
| \Processor\PercentUserTime |백분율 |
| \Processor\PercentNiceTime |백분율 |
| \Processor\PercentPrivilegedTime |백분율 |
| \Processor\PercentInterruptTime |백분율 |
| \Processor\PercentDPCTime |백분율 |
| \Processor\PercentProcessorTime |백분율 |
| \Processor\PercentIOWaitTime |백분율 |
| \PhysicalDisk\BytesPerSecond |초당 바이트 수 |
| \PhysicalDisk\ReadBytesPerSecond |초당 바이트 수 |
| \PhysicalDisk\WriteBytesPerSecond |초당 바이트 수 |
| \PhysicalDisk\TransfersPerSecond |초당 개수 |
| \PhysicalDisk\ReadsPerSecond |초당 개수 |
| \PhysicalDisk\WritesPerSecond |초당 개수 |
| \PhysicalDisk\AverageReadTime |초 |
| \PhysicalDisk\AverageWriteTime |초 |
| \PhysicalDisk\AverageTransferTime |초 |
| \PhysicalDisk\AverageDiskQueueLength |개수 |
| \NetworkInterface\BytesTransmitted |바이트 |
| \NetworkInterface\BytesReceived |바이트 |
| \NetworkInterface\PacketsTransmitted |개수 |
| \NetworkInterface\PacketsReceived |개수 |
| \NetworkInterface\BytesTotal |바이트 |
| \NetworkInterface\TotalRxErrors |개수 |
| \NetworkInterface\TotalTxErrors |개수 |
| \NetworkInterface\TotalCollisions |개수 |

## <a name="commonly-used-web-server-farm-metrics"></a>일반적으로 사용되는 웹(서버 팜) 메트릭
Hello Http 큐 길이 등 일반적인 웹 서버 메트릭을 기반으로 하는 자동 크기 조정을 수행할 수도 있습니다. 메트릭 이름은 **HttpQueueLength**입니다.  다음 섹션 목록 사용 가능한 서버 팜 (웹 앱) 메트릭 번호입니다.

### <a name="web-apps-metrics"></a>웹앱 메트릭
다음 powershell에서 명령을 hello를 사용 하 여 hello 웹 응용 프로그램 메트릭 목록은 생성할 수 있습니다.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

다음 메트릭에 대한 경고를 만들거나 크기를 조정할 수 있습니다.

| 메트릭 이름 | 단위 |
| --- | --- |
| CpuPercentage |백분율 |
| MemoryPercentage |백분율 |
| DiskQueueLength |개수 |
| HttpQueueLength |개수 |
| BytesReceived |바이트 |
| BytesSent |바이트 |

## <a name="commonly-used-storage-metrics"></a>일반적으로 사용되는 저장소 메트릭
저장소 큐 길이 hello hello 저장소 큐의 메시지 수를으로 확장할 수 있습니다. 저장소 큐 길이 특별 한 메트릭 및 hello 임계값은 hello 인스턴스 당 메시지 수입니다. 예를 들어 두 개의 인스턴스가 있는 및 hello 임계값 too100 설정 되 면 hello hello 큐에 메시지의 총 수는 200 때 발생 크기 조정 합니다. 인스턴스 당 100 개의 메시지, 120 및 80, 또는 모든 기타 조합을 too200 이상의를 추가 하는 일 수 있는 합니다.

이 설정은 hello hello에서 Azure 포털 구성 **설정을** 블레이드입니다. VM 크기 집합에 대 한 리소스 관리자 템플릿 toouse hello에에서 hello 자동 크기 조정 설정을 업데이트할 수 있습니다 *metricName* 으로 *ApproximateMessageCount* 으로 hello 저장소 큐의 hello ID 전달  *metricResourceUri*합니다.

예를 들어 클래식 저장소 계정을 hello로 자동 크기 조정 설정을 metricTrigger 포함:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

(비 클래식) 저장소 계정에 대 한 hello metricTrigger 다음과 같습니다.

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>자주 사용되는 서비스 버스 메트릭
서비스 버스 큐 길이 hello hello 서비스 버스 큐의 메시지 수를 확장할 수 있습니다. 서비스 버스 큐 길이 특별 한 메트릭 및 hello 임계값은 hello 인스턴스 당 메시지 수입니다. 예를 들어 두 개의 인스턴스가 있는 및 hello 임계값 too100 설정 되 면 hello hello 큐에 메시지의 총 수는 200 때 발생 크기 조정 합니다. 인스턴스 당 100 개의 메시지, 120 및 80, 또는 모든 기타 조합을 too200 이상의를 추가 하는 일 수 있는 합니다.

VM 크기 집합에 대 한 리소스 관리자 템플릿 toouse hello에에서 hello 자동 크기 조정 설정을 업데이트할 수 있습니다 *metricName* 으로 *ApproximateMessageCount* 으로 hello 저장소 큐의 hello ID 전달  *metricResourceUri*합니다.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> 서비스 버스에 대 한 hello 리소스 그룹 개념 존재 하지 않는 있지만 Azure 리소스 관리자 / 지역당 기본 리소스 그룹을 만듭니다. hello 리소스 그룹은 일반적으로 hello 'Default-ServiceBus-[region]' 형태로 표시 합니다. 예를 들어 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' 등입니다.
>
>
