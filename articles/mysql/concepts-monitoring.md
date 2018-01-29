---
title: "Azure Database for MySQL에서 모니터링 | Microsoft Docs"
description: "이 문서에서는 CPU, 제한, 저장소 및 연결 통계를 포함하여 Azure Database for MySQL을 모니터링하고 경고하는 메트릭에 대해 설명합니다."
services: mysql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 10/24/2017
ms.openlocfilehash: 9af447d54faa8ee96e4b79beb274b437eea57626
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2017
---
# <a name="monitoring-in-azure-database-for-mysql"></a>Azure Database for MySQL에서 모니터링
서버에 대한 데이터를 모니터링하면 워크로드에 대한 문제를 해결하고 최적화할 수 있습니다. Azure Database for MySQL은 MySQL 서버를 지원하는 리소스의 동작에 대한 통찰력을 제공하는 다양한 메트릭을 제공합니다. 

## <a name="metrics"></a>메트릭
모든 Azure 메트릭의 빈도는 1분이고 각 메트릭은 30일의 기록을 제공합니다. 

메트릭에 대한 경고를 구성할 수 있습니다. 단계별 지침은 [How to set up alerts](howto-alert-on-metric.md)(경고를 설정하는 방법)를 참조하세요. 

다른 작업에는 자동화된 작업 설정, 고급 분석 수행 및 기록 보관이 포함됩니다. 자세한 내용은 [Azure 메트릭 개요](../monitoring-and-diagnostics/monitoring-overview-metrics.md)를 참조하세요.

### <a name="list-of-metrics"></a>메트릭 목록
Azure Database for MySQL에서는 다음 메트릭을 사용할 수 있습니다.

|메트릭|메트릭 표시 이름|단위|설명|
|---|---|---|---|---|
|cpu_percent|CPU 백분율|백분율|사용 중인 CPU의 비율|
|compute_limit|계산 단위 제한|개수|이 서버의 최대 계산 단위 수|
|compute_consumption_percent|계산 단위 백분율|백분율|서버의 최대값을 초과하여 사용된 계산 단위의 비율|
|memory_percent|메모리 백분율|백분율|사용 중인 메모리의 비율|
|io_consumption_percent|IO 백분율|백분율|사용 중인 IO의 비율|
|storage_percent|저장소 비율|백분율|서버의 최대값을 초과하여 사용된 저장소의 비율|
|storage_used|저장소 사용됨|바이트|사용 중인 저장소의 양 서비스에서 사용되는 저장소에는 데이터베이스 파일, 트랜잭션 로그 및 서버 로그가 포함됩니다.|
|storage_limit|저장소 제한|바이트|이 서버의 최대 저장소|
|active_connections|전체 활성 연결|개수|서버에 대한 활성 연결 수|
|connections_failed|실패한 전체 연결|개수|서버에 대해 실패한 연결 수|


> [!NOTE]
> 계산 단위는 메모리와 CPU로 구성됩니다. 계산 단위 비율은 최대값(memory%, cpu%)입니다. 계산 단위 비율 변경에 기여하는 요소를 찾으려면 메모리 및 CPU 차트를 검사합니다. 자세한 내용은 [계산 단위](concepts-compute-unit-and-storage.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
- 단계별 지침은 [How to set up alerts](howto-alert-on-metric.md)(경고를 설정하는 방법)를 참조하세요. 
- Azure Portal, REST API 또는 CLI를 사용하여 메트릭에 액세스하고 내보내는 방법에 대한 자세한 내용은 [Azure 메트릭 개요](../monitoring-and-diagnostics/monitoring-overview-metrics.md)를 참조하세요.
