---
title: "aaa \"PostgreSQL에 대 한 Azure 데이터베이스의 가격 책정 계층\""
description: "PostgreSQL용 Azure 데이터베이스의 가격 책정 계층"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: article
ms.date: 05/31/2017
ms.openlocfilehash: f10389dd2ad1ff04e83b02786a407c10140a007b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>PostgreSQL용 Azure 데이터베이스 옵션 및 성능: 각 가격 책정 계층에서 사용할 수 있는 항목 이해
PostgreSQL 서버에 대 한 Azure 데이터베이스를 만들 때 결정 세 가지 주요 선택 사항 해당 서버에 할당 된 tooconfigure hello 리소스입니다. 이러한 선택 hello 성능과 hello 서버 확장성에 영향을 줄 합니다.
- 가격 책정 계층 
- 계산 단위
- 저장소(GB)

각 가격 책정 계층에는 다양 한 작업 부하 요구 사항에 따라, 성능 수준 (계산 단위) toochoose에 있습니다. 더 높은 성능 수준을 서버 디자인 된 toodeliver 높은 처리량을 위한 추가 리소스를 제공합니다. 응용 프로그램 중단 시간 없이 거의 가격 책정 계층 내에서 hello 서버의 성능 수준을 변경할 수 있습니다.

> [!IMPORTANT]
> Hello 서비스 공개 미리 보기 상태인 동안 않습니다 보장 된 서비스 수준 계약 (SLA).

PostgreSQL 서버용 Azure 데이터베이스 내에서 하나 이상의 데이터베이스를 포함할 수 있습니다. 모든 hello 리소스 toocreate 서버 tooutilize 당 단일 데이터베이스를 선택 하거나 여러 데이터베이스 tooshare hello 리소스를 만들 수 있습니다. 

## <a name="choose-a-pricing-tier"></a>가격 책정 계층 선택
미리 보기 상태에서 PostgreSQL용 Azure 데이터베이스는 두 가지 가격 책정 계층(기본 및 표준)을 제공합니다. 프리미엄 계층은 아직 사용할 수 없지만 곧 제공됩니다. 

hello 다음 표에서 가격 책정 계층이 가장 다양 한 응용 프로그램 워크 로드에 적합 한 hello의 예제.

| 가격 책정 계층  | 대상 워크로드 |
| :----------- | :----------------|
| Basic | IOPS 보장 없이 확장 가능한 Compute 및 저장 단위를 필요로 하는 작은 작업에 가장 적합합니다. 예를 들어 개발 또는 시험, 또는 자주 사용하지 않는 소규모 응용 프로그램에 사용되는 서버가 이에 해당합니다. |
| Standard | 클라우드에 대 한 go toooption hello 처리량이 많은 IOPS를 필요로 하는 응용 프로그램을 보장 합니다. 예제에는 웹 또는 분석 응용 프로그램이 포함됩니다. |
| Premium | 트랜잭션 및 IO의 대기 시간이 짧아야 하는 워크로드에 가장 적합합니다. 많은 동시 사용자에 대 한 hello 최상의 지원을 제공합니다. 업무용 응용 프로그램을 지 원하는 toodatabases 적용할 수 있습니다.<br />hello 프리미엄 가격 책정 계층을 미리 보기에서 사용할 수 없는 경우 |

가격 책정에 toodecide 계층 워크 로드는 IOPS 보장 해야 하는 경우를 확인 하 여 첫 번째 시작 합니다. 필요한 경우 표준 가격 책정 계층을 사용합니다.

| **가격 책정 계층 기능** | **Basic** | **Standard** |
| :------------------------ | :-------- | :----------- |
| 최대 Compute 단위 | 100 | 800 | 
| 최대 총 저장소 | 1TB | 1TB | 
| 저장소 IOPS 보장 | 해당 없음 | 예 | 
| 최대 저장소 IOPS | 해당 없음 | 3,000 | 
| 데이터베이스 백업 보존 기간 | 7 일 | 35일 | 

Hello 미리 보기 기간 동안 hello 서버 만들어지면 가격 책정 계층을 변경할 수 없습니다. Hello 이후에서 가능한 tooupgrade 되거나 됩니다 한 가격 책정 계층 tooanother 계층에서 서버를 다운 그레이드 합니다.

## <a name="understand-hello-price"></a>Hello 가격 이해
데이터베이스를 만들 때를 새 Azure PostgreSQL에 대 한 hello 내 [Azure 포털](https://portal.azure.com/#create/Microsoft.PostgreSQLServer), hello 클릭 **가격 책정 계층** 블레이드에서 하 고 월간 비용 hello에 표시 될 따라 hello 선택한 옵션을 합니다. Azure 구독이 없는 경우 Azure 가격 계산기 tooget 예상된 가격 hello를 사용 합니다. Hello 방문 [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/) 웹 사이트를 클릭 한 다음 **항목 추가**, hello 확장 **데이터베이스** 범주를 선택 하 고 **Azure 데이터베이스에 대 한 PostgreSQL** toocustomize hello 옵션입니다.

## <a name="choose-a-performance-level-compute-units"></a>성능 수준(계산 단위) 선택
Hello PostgreSQL 서버에 대 한 Azure 데이터베이스에 대 한 가격 책정 계층을 결정 했으면 필요한 계산 단위의 hello 수를 선택 하 여 준비 toodetermine hello 성능 수준 됩니다. 웹 또는 분석 워크로드를 위해 더 높은 사용자 동시성을 요구하는 응용 프로그램에 대한 좋은 시작점은 200 또는 400 Compute 단위이며 필요에 따라 증분 방식으로 조정합니다. 

단위는 사용 가능한 tooa toobe 보장 되는 CPU 처리 처리량의 측정값을 계산 PostgreSQL 서버에 대 한 Azure 데이터베이스를 단일 합니다. Compute 단위는 CPU 및 메모리 리소스를 혼합해서 측정합니다.  자세한 내용은 [계산 단위 설명](concepts-compute-unit-and-storage.md)을 참조하세요.

### <a name="basic-pricing-tier-performance-levels"></a>기본 가격 책정 계층 성능 수준:

| **성능 수준** | **50** | **100** |
| :-------------------- | :----- | :------ |
| 최대 Compute 단위 | 50 | 100 |
| 포함된 저장소 크기 | 50GB | 50GB |
| 최대 서버 저장소 크기\* | 1TB | 1TB |

### <a name="standard-pricing-tier-performance-levels"></a>표준 가격 책정 계층 성능 수준:

| **성능 수준** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| 최대 Compute 단위 | 100 | 200 | 400 | 800 |
| 포함된 저장소 크기 및 프로비전된 IOPS | 125GB,<br/> 375 IOPS | 125GB,<br/> 375 IOPS | 125GB,<br/> 375 IOPS | 125GB,<br/> 375 IOPS |
| 최대 서버 저장소 크기\* | 1TB | 1TB | 1TB | 1TB |
| 프로비전된 최대 서버 IOPS | 3,000 IOPS | 3,000 IOPS | 3,000 IOPS | 3,000 IOPS |
| GB당 프로비전된 최대 서버 IOPS | GB당 고정된 3 IOPS | GB당 고정된 3 IOPS | GB당 고정된 3 IOPS | GB당 고정된 3 IOPS |

\*최대 서버 저장소 크기는 서버에 대 한 toohello 최대 프로 비전 된 저장소 크기를 나타냅니다.

## <a name="storage"></a>저장소 
hello 저장소 구성은 저장소 용량 사용 가능한 tooan Azure 데이터베이스 PostgreSQL 서버에 대 한 hello 양을 정의합니다. hello 서비스에서 사용 하는 hello 저장소 hello 데이터베이스 파일, 트랜잭션 로그 및 hello PostgreSQL 서버 로그를 포함 합니다. Hello 저장소 구성을 선택 하는 경우 성능 요구 사항 (IOPS) hello 및 데이터베이스 저장소에 필요한 크기 toohost의 hello 크기를 고려 하세요.

각 가격 책정 계층에서는 hello "포함 된 저장소 크기입니다."로 테이블을 앞에서 언급 된 일부 저장소 용량이 여기에 최소한 포함 되어 Toohello 최대 허용된 저장소를 125 GB 단위로 hello 서버를 만든 경우에 추가 저장 용량을 추가할 수 있습니다. hello 스토리지 용량 단위 계산 구성 hello와 독립적으로 구성할 수 있습니다. hello 양의 저장소가 선택에 따라 hello 가격 변경 합니다.

각 성능 수준에서 hello IOPS 구성 toohello 가격 책정 계층 및 선택한 hello 저장소 크기 관련 됩니다. 기본 계층에서는 IOPS 보장을 제공하지 않습니다. Hello 표준 가격 책정 계층 내에서 IOPS hello 비례적으로 toomaximum 저장소 크기에서에서 확장 고정된 3:1 비율로. 375에 대 한 보장 125 GB의 포함 하는 hello 저장소 IOPS의 too256 KB IO 크기는 각각를 프로 비전 합니다. 추가 저장소 too1 TB 최대를 선택할 수 있습니다, 3, 000 tooguarantee IOPS를 프로 비전 합니다.

Azure 포털 또는 쓰기 Azure CLI 명령 toomeasure hello 소비 IOPS 및 저장소의 hello에서 hello 메트릭 그래프를 모니터링 합니다. 관련 메트릭 toomonitor은 저장소 용량 한도, 저장소 백분율, 저장소, 사용 및 IO 백분율입니다.

>[!IMPORTANT]
> 미리 보기에 있는 동안 hello 서버를 만들 때는 hello 시 hello 저장소 크기를 선택 합니다. 기존 서버에 hello 저장소 크기를 변경 아직 지원 되지 않습니다. 

## <a name="scaling-a-server-up-or-down"></a>서버 확장 또는 축소
처음 hello PostgreSQL에 대 한 Azure 데이터베이스를 만들면 가격 계층 및 성능 수준을 선택 합니다. 이상에서는 계산 단위를 위나 아래로 동적으로 hello hello 범위 내에서 동일한 hello를 확장할 수 있습니다 가격 책정 계층입니다. 에서는 hello Azure 포털, hello 서버의 가격 책정 계층 블레이드에서 hello 계산 단위를 이동 하거나이 예제를 수행 하 여 스크립트: [모니터 및 배율 Azure CLI를 사용 하 여 단일 PostgreSQL 서버](scripts/sample-scale-server-up-or-down.md)

배율 단위를 계산 하는 hello 선택한 hello 최대 저장소 크기와 독립적으로 수행 됩니다.

Hello 백그라운드 hello 데이터베이스 성능 수준을 변경할 hello 원래 데이터베이스의 복제본 hello 새로운 성능 수준에서 만들고 toohello 복제를 통해 연결을 전환 합니다. 이 프로세스 중에는 데이터가 손실되지 않습니다. Hello 잠시 toohello 복제본으로 전환 우리는 때를 하는 동안 연결 toohello 데이터베이스 사용할 이동 중인 일부 트랜잭션이 롤백될 수 있습니다. 하지만 평균 4초 이내 또 사례의 99% 이상에서 30초 미만으로 이 창이 달라집니다. 큰는 hello 현재 연결에서 항공편의 트랜잭션 수를 사용할 수 없습니다. 면이 창을 더 길 수 있습니다.

hello 전체 눈금 프로세스의 소요 시간은 hello hello 크기와 hello 변경 후 및 하기 전에 hello 서버의 가격 책정 계층에 따라 달라 집니다. 예를 들어 hello 표준 가격 책정 계층 내에서 계산 단위를 변경 하 고 있는 서버는 몇 분 내에 완료 해야 합니다. 서버 hello에 대 한 새 속성 hello hello 변경이 완료 될 때까지 적용 되지 않습니다.

## <a name="next-steps"></a>다음 단계
- Compute 단위에 대한 자세한 내용은 [Compute 단위 설명](concepts-compute-unit-and-storage.md)을 참조하세요.
- 너무 방법에 대해 알아봅니다[모니터 및 배율 Azure CLI를 사용 하 여 단일 PostgreSQL 서버](scripts/sample-scale-server-up-or-down.md)
