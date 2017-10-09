---
title: "MySQL용 Azure Database의 Compute 단위 설명 | Microsoft Docs"
description: "MySQL에 대 한 azure DB:이 문서에서는 계산 단위 및 작업에 도달 하면 어떤 일이 생기 hello 개념 hello 최대 계산 단위에 설명 합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>MySQL용 Azure Database의 Compute 단위 설명
Hello 단위 계산의 개념과 작업 도달 hello 계산 최대 단위는 경우이 문서에 설명 합니다.

## <a name="what-are-compute-units"></a>Compute 단위란?
단위는 사용 가능한 tooa toobe 보장 되는 CPU 처리 처리량의 측정값을 계산 MySQL server에 대 한 Azure 데이터베이스를 단일 합니다. Compute 단위는 CPU 및 메모리 리소스를 혼합해서 측정합니다. 일반적으로 50 명의 계산 단위 코어의 toohalf를 같습니다. 100 계산할 단위로 tooone 코어를 같습니다. 2000 계산 단위 tootwenty 코어를의 보장 된 처리 처리량 tooyour 사용 가능한 서버와 같습니다.

hello 메모리양 계산 단위당 Basic hello 및 표준 가격 책정 계층에 대해 최적화 되어 있습니다. Hello 성능 수준을 높여 hello 계산 단위를 두 배로 toodoubling hello 집합이 사용 가능한 리소스 toothat과 같습니다. MySQL 용 Azure 데이터베이스를 단일 합니다.

예를 들어 표준 800 Compute 단위는 표준 100 Compute 단위 구성보다 8배 더 많은 CPU 처리량 및 메모리를 제공합니다. 그러나 표준 100 계산 단위를 제공 하는 동안 hello 동일 CPU 처리량 단위를 계산 하는 100 tooBasic 비교, 미리 구성 된 표준 가격 책정 계층에에서 있는 메모리 양을 hello는 double hello 메모리 용량의 Basic 가격 책정 계층에 대해 구성 합니다. 따라서 표준 가격 책정 계층 작업 부하 성능이 향상 및 동일한 계산 단위 선택한 hello로 Basic 가격 책정 계층 보다 낮은 트랜잭션 대기 시간을 제공 합니다.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>내 작업에 필요한 계산 단위의 hello 수는 어떻게 확인할 수 있습니까?
Toomigrate 온-프레미스를 실행 하는 기존 MySQL 서버를 찾고 있는 경우 또는 가상 컴퓨터에서 작업에 필요한 처리 처리량의 코어 개수를 산정 하 여 hello 계산 단위 수를 확인할 수 있습니다. 

기존 온-프레미스 또는 가상 컴퓨터 서버에서 현재 4개 코어를 사용하는 경우(CPU 하이퍼스레드 제외) 먼저 MySQL 서버용 Azure Database에 대해 400 Compute 단위를 구성하여 시작합니다. Compute 단위는 응용 프로그램 가동 중지 시간이 거의 없이도 워크로드 필요량에 따라 동적으로 확장 또는 축소할 수 있습니다. 

Azure 포털 또는 쓰기 Azure CLI 명령-toomeasure hello에 모니터 hello 메트릭 그래프 단위를 계산 합니다. 관련 메트릭 toomonitor는 hello 단위 계산 백분율 및 단위 계산도 있습니다.

>[!IMPORTANT]
> 저장소 IOPS 없는 완전 하 게 활용 toohello 최대를 찾을 경우 hello 계산 단위 사용률도 모니터링 하는 것이 좋습니다. Hello 계산 단위를 발생 시키는 toolimited CPU 또는 메모리 인해 성능 병목 현상 hello를 절감 하 여 IO 처리량 허용할 수 있습니다.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>내 최대 Compute 단위에 도달한 경우 어떻게 되나요?
성능 수준에는 보정 및 tooprovide 리소스 toorun hello 선택한 가격 책정 계층 및 성능 수준에 대 한 최대 제한 toohello 데이터베이스 작업을 제어 합니다. 

작업 중 하나 hello 계산할 단위로 hello 최대 제한 또는 프로 비전 된 IOPS 제한에 도달 하면 hello 최대 허용 수준 tooutilize hello 리소스를 계속할 수 있지만 쿼리는 대기 시간이 증가 가능성이 toosee 합니다. 이러한 제한으로 나타나지 모든 오류가 발생 하지만 hello 작업에서 속도가 느려지는 대신 hello 속도가 느려지는 시간 초과 쿼리 하는 심각한 경우입니다. 

작업 hello에 대 한 연결 수가 최대 제한에 도달 하는 경우 명시적 오류가 발생 합니다. 리소스 제한에 대한 자세한 내용은 [MySQL용 Azure Database의 제한 사항](concepts-limits.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
가격 책정 계층에 대한 자세한 내용은 [MySQL용 Azure Database 가격 책정 계층](./concepts-service-tiers.md)을 참조하세요.
