---
title: "일괄 처리 이벤트-Azure의 진단 로깅 aaaEnable | Microsoft Docs"
description: "풀, 작업 등과 같은 Azure Batch 계정 리소스에 대해 진단 로그 이벤트를 기록 및 분석합니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Batch 솔루션의 진단 평가 및 모니터링에 대한 로그 이벤트

여러 Azure 서비스와 마찬가지로 hello 일괄 처리 서비스는 특정 리소스 중 hello hello 리소스 수명을 이벤트를 로그를 내보냅니다. 풀 및 작업을 같은 리소스에 대 한 Azure 배치 진단 로그 toorecord 이벤트를 활성화 하 고 진단 평가 및 모니터링에 대 한 hello 로그를 사용할 수 있습니다. 풀 만들기, 풀 삭제, 작업 시작, 작업 완료, 기타 등의 이벤트는 Batch 진단 로그에 포함됩니다.

> [!NOTE]
> 이 문서에서는 작업과 작업 출력 데이터가 아닌 배치 계정 리소스 자체에 대한 이벤트 로깅을 논의합니다. 작업 및 작업의 hello 출력 데이터 저장에 대 한 세부 정보를 참조 하십시오. [지속 Azure 일괄 처리 작업 및 태스크 출력](batch-task-output.md)합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
* [Azure Batch 계정](batch-account-create-portal.md)
* [Azure Storage 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  toopersist 일괄 처리 진단 로그를 Azure hello 로그를 저장 하는 Azure 저장소 계정을 만들어야 합니다. 배치 계정에 [진단 로깅을 사용](#enable-diagnostic-logging)할 때 이 저장소 계정을 지정합니다. 연결 된 저장소 계정 참조 tooin hello로 동일를 hello 로그 수집을 사용 하면 지정한 저장소 계정이 hello 하지 [응용 프로그램 패키지](batch-application-packages.md) 및 [작업 출력 지 속성](batch-task-output.md) 문서입니다.
  
  > [!WARNING]
  > **청구** Azure 저장소 계정에 저장 된 hello 데이터에 대 한 합니다. 이 문서에서 설명 하는 hello 진단 로그가 포함 됩니다. [로그 보존 정책](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)을 설계할 때는 이 점을 염두에 둡니다.
  > 
  > 

## <a name="enable-diagnostic-logging"></a>진단 로깅 사용
진단 로깅은 배치 계정에 기본적으로 활성화되지 않습니다. Toomonitor 원하는 각 일괄 처리 계정에 대 한 진단 로깅을 명시적으로 설정 해야 합니다.

[어떻게 진단 로그의 tooenable 컬렉션](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Hello 전체를 읽는 것이 좋습니다 [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 다양 한 Azure 서비스 hello에서 지 원하는 문서 toogain 뿐만 아니라 tooenable 로깅을 하지만 hello 로그 하는 방법은 범주를 이해 합니다. 예를 들어, 현재 Azure Batch는 **서비스 로그** 카테고리 하나만 지원합니다.

## <a name="service-logs"></a>서비스 로그
Azure 일괄 처리 서비스 로그 풀 또는 작업 처럼 일괄 처리 리소스의 hello 수명 동안 hello Azure 배치 서비스에서 내보내는 이벤트를 포함 합니다. 일괄 처리에 의해 발생 하는 각 이벤트는 지정 된 hello에 저장 된 JSON 형식으로 저장소 계정입니다. 예를 들어,이 샘플의 hello 본문 **풀 만들기 이벤트**:

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

.Json<에 각 이벤트 본문이 있는 파일 hello에 Azure 저장소 계정을 지정 합니다. Tooaccess 로그를 직접 hello를 원하는 경우 tooreview hello을 지정할 수 있습니다 [hello 저장소 계정에 진단 로그의 스키마](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account)합니다.

## <a name="service-log-events"></a>서비스 로그 이벤트
hello를 일괄 처리 서비스는 현재 hello를 다음 서비스 로그 이벤트를 내보냅니다. 이 목록은 전체가 아니며, 이 문서가 마지막으로 업데이트된 뒤 다른 이벤트가 추가되었을 수 있습니다.

| **서비스 로그 이벤트** |
| --- |
| [풀 만들기][pool_create] |
| [풀 삭제 시작][pool_delete_start] |
| [풀 삭제 완료][pool_delete_complete] |
| [풀 크기 조정 시작][pool_resize_start] |
| [풀 크기 조정 완료][pool_resize_complete] |
| [작업 시작][task_start] |
| [작업 완료][task_complete] |
| [작업 실패][task_fail] |

## <a name="next-steps"></a>다음 단계
또한 toostoring 진단 로그는 Azure 저장소 계정에 이벤트, 스트리밍할 수도 있습니다 일괄 처리 서비스 로그 이벤트 tooan [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md), 너무 보내도록[Azure 로그 분석](../log-analytics/log-analytics-overview.md)합니다.

* [Azure 진단 로그 tooEvent 허브 스트림](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  일괄 처리 진단 이벤트 toohello 확장성이 높은 데이터 유입 서비스를, 이벤트 허브를 스트리밍하십시오. 이벤트 허브는 초당 수백 건의 이벤트를 수집하여 모든 실시간 분석 공급자를 통해 변환 및 저장할 수 있습니다.
* [Log Analytics를 사용하여 Azure 진단 로그 분석 ](../log-analytics/log-analytics-azure-storage.md)
  
  사용자 진단 로그 tooLog hello Operations Management Suite (OMS) 포털에서이 분석 하거나 Power BI 또는 Excel에서 분석을 위해 내보낼 수 있는 분석을 보냅니다.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
