---
title: "Azure 검색에 대 한 계획 aaaCapacity | Microsoft Docs"
description: "Azure Search에서 파티션 및 복제본 컴퓨터 리소스를 조정하고 이 곳에서 각 리소스가 청구 가능한 검색 단위로 가격이 책정됩니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Azure 검색의 쿼리 및 인덱싱 작업을 위한 리소스 수준 확장
후 [가격 책정 계층만 선택](search-sku-tier.md) 및 [검색 서비스를 프로 비전](search-create-service-portal.md), hello 다음 단계는 복제본 또는 서비스에 의해 사용 되는 파티션 toooptionally 증가 hello 수 있습니다. 각 계층은 고정된 개수의 청구 단위를 제공합니다. 이 문서에서는 설명 방법을 tooallocate 이러한 단위가 tooachieve 최적의 쿼리 실행, 인덱싱 및 저장소에 대 한 요구 사항을 균형을 구성 합니다.

리소스 구성이 hello에서 서비스를 설정할 때 사용 가능 [기본 계층](http://aka.ms/azuresearchbasic) hello 중 하나 또는 [표준 계층](search-limits-quotas-capacity.md)합니다. 이러한 계층에서 청구 가능한 서비스의 경우 각 파티션 및 복제본이 하나의 SU로 계산되는 SU(*검색 단위*)로 용량을 증분하여 구매합니다. 

더 적은 SU를 사용하면 비례적으로 청구 금액이 줄어듭니다. 청구는 hello 서비스 설정으로에 적용 됩니다. 경우 일시적으로 사용 하지 않는 hello 유일한 방법은 hello 서비스를 삭제 한 다음 다시 만들어이 필요할 때 여 tooavoid 청구 되는 서비스입니다.

> [!Note]
> 서비스를 삭제하면 해당 서비스에 있는 모든 것이 삭제됩니다. Azure Search에는 유지되는 검색 데이터를 백업하고 복원하는 기능이 없습니다. 새 서비스에서 기존 인덱스 tooredeploy hello 사용 프로그램 toocreate 실행를 원래 로드 합니다. 

## <a name="terminology-partitions-and-replicas"></a>용어: 파티션 및 복제본
파티션과 복제본은 다시 검색 서비스는 hello 기본 리소스입니다.

| 리소스 | 정의 |
|----------|------------|
|*파티션* | 읽기/쓰기 작업(예: 인덱스를 다시 작성하거나 새로 고치는 경우)을 위한 인덱스 저장소 및 I/O를 제공합니다.|
|*복제본* | Hello 검색 서비스의 인스턴스 tooload 분산 쿼리 작업에 주로 사용 합니다. 각 복제본은 인덱스의 사본 하나를 항상 실행합니다. 12 복제본을 설정한 경우 12 개 hello 서비스에 로드 된 모든 인덱스 갖습니다.|

> [!NOTE]
> 없기 toodirectly 조작 하거나 복제본에서 실행 하는 인덱스를 관리 합니다. 모든 복제본에 있는 각 인덱스의 복사본이 두 개는 hello 서비스 아키텍처의 일부입니다.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>어떻게 tooallocate 파티션 및 복제본
Azure 검색에서 서비스에는 1개 파티션과 1개 복제본으로 구성된 최소 수준의 리소스가 할당됩니다. 이것을 지원하는 계층에 대해 저장소 및 I/O가 더 필요하거나 쿼리 볼륨을 늘리거나 성능을 높이기 위해 복제본을 더 추가하는 경우 파티션을 늘려 계산 리소스를 증분 조정할 수 있습니다. 단일 서비스는 모든 작업 (인덱싱 및 쿼리) 충분 한 리소스 toohandle 있어야 합니다. 여러 서비스 간에 워크로드를 세분화할 수 없습니다.

복제 데이터베이스 및 파티션을 hello 할당 tooincrease 또는 변경, hello Azure 포털을 사용 하는 것이 좋습니다. hello 포털 최대 한도 유지 되는 허용 가능한 조합에 제한이 적용 됩니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) hello 검색 서비스를 선택 합니다.
2. **설정**개방형 hello **배율** 블레이드 및 사용 하 여 슬라이더 tooincrease hello 또는 파티션과 복제본 hello 수를 줄입니다.

스크립트 또는 코드 기반 프로비저닝 방법이 필요한 경우 hello [관리 REST API](https://msdn.microsoft.com/library/azure/dn832687.aspx) 은 대체 toohello 포털입니다.

일반적으로 검색 응용 프로그램 쿼리 워크 로드가 hello 서비스 작업은 중심 하는 경우에 특히 파티션, 복제본이 더 많이 필요 합니다. 섹션에 hello [고가용성](#HA) 그 이유에 대해 설명 합니다.

> [!NOTE]
> 업그레이드 된 tooa 않아야 서비스 프로 비전 되 면 더 높은 SKU입니다. 필요한 toocreate hello 새 계층에서 검색 서비스 되 고 인덱스를 다시 로드 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 서비스 프로 비전에 대 한 도움말입니다.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>고가용성
있기 때문에 쉽게 비교적 tooscale를 빠른, 일반적으로 하나의 파티션을 하나와 시작 또는 두 개의 복제본 및 다음으로 쿼리 볼륨이 스케일 업 빌드 권장 합니다. Hello Basic 또는 S1 계층에서 여러 서비스에 대 한 하나의 파티션 (파티션당 15 백만 문서)에 대해 충분 한 저장소 및 I/O 제공합니다.

쿼리 작업은 복제본에서 주로 실행됩니다. 고가용성이나 처리량이 더 필요한 경우에는 추가 복제본이 필요할 가능성이 높습니다.

고가용성을 위한 일반적인 권장 사항은 다음과 같습니다.

* 읽기 전용 작업(쿼리)의 고가용성을 위한 복제본 두 개
* 읽기/쓰기 워크로드의 고가용성을 위한 복제본 세 개 이상(개별 문서가 추가, 업데이트 또는 삭제됨에 따라 쿼리 및 인덱싱)

Azure Search에 대한 Service Level Agreement(서비스 수준 약정)는 문서 추가, 업데이트 또는 삭제로 구성된 쿼리 작업 및 인덱스 업데이트를 대상으로 합니다.

### <a name="index-availability-during-a-rebuild"></a>인덱스 다시 작성 중 가용성

Azure 검색에 대 한 고가용성 관련 된 인덱스를 다시 포함 하지 않으며 tooqueries 및 인덱스 업데이트 합니다. 필드를 삭제, 데이터 형식을 변경 하거나 필드 이름 바꾸기 toorebuild hello 인덱스를 해야 합니다. toorebuild hello 인덱스 hello 삭제 해야 인덱스를 다시 hello 인덱스를 만들어 hello 데이터 다시 로드 합니다.

> [!NOTE]
> Hello 인덱스 다시 작성 하지 않고 새 필드 tooan Azure 검색 인덱스를 추가할 수 있습니다. hello 새 필드의 hello 값 hello 인덱스에 이미 있는 모든 문서에 대해 null이 됩니다.

다시 작성 중 toomaintain 인덱스 가용성, 다른 이름으로 hello 인덱스의 복사본을 같은 다른 서비스에 이름을 지정 하 고 다음 코드에서 리디렉션 또는 장애 조치 논리를 제공 하는 hello로 hello 인덱스 동일한 서비스 또는 hello의 복사본에 있어야 합니다.

## <a name="disaster-recovery"></a>재해 복구
현재, 재해 복구를 위한 기본 제공 메커니즘은 없습니다. 추가 파티션/복제본 하거나 재해 복구 목표를 충족 하는 것에 대 한 잘못 된 전략 hello 것입니다. hello 가장 일반적인 방법은 다른 지역에 두 번째 검색 서비스를 설정 하 여 hello 서비스 수준에서 tooadd 중복을입니다. 인덱스 다시 작성 하는 동안 가용성와 마찬가지로 hello 리디렉션 또는 장애 조치 논리도 사용자 코드에서 가져와야 합니다.

## <a name="increase-query-performance-with-replicas"></a>복제본으로 쿼리 성능 향상
쿼리 대기 시간을 통해 추가 복제본의 필요성을 알 수 있습니다. 일반적으로 쿼리 성능을 향상 시키기 위한 첫 번째 단계는이 리소스의 자세한 tooadd 합니다. 복제본을 추가한 것 처럼 hello 인덱스의 추가 복사본이 온라인 toosupport 더 큰 쿼리 작업에 가져오는 및 tooload 균형 hello 요청이 hello 여러 복제본입니다.

Queries / sec (QPS)에 하드 예측을 제공할 수 없습니다: 쿼리 성능은 hello의 hello 복잡성에 따라 다릅니다 쿼리 및 경쟁 작업 합니다. 평균적으로 기본 또는 S1 SKU의 복제본 하나에서는 약 15개의 QPS를 서비스할 수 있지만 쿼리의 복잡성과(패킷 쿼리가 더 복잡) 네트워크 대기 시간에 따라 처리량이 더 높거나 낮을 수도 있습니다. 또한 변수는 중요 한 복제 추가 추가 하면 용량이 확장 및 성능, 있지만 hello 결과 toorecognize는 엄격 하 게 선형이 아니므로: 세 개의 복제본 추가 삼중 처리량을 보장 하지 않습니다.

toolearn QPS 트 작업에 대 한 예측 하기 위한 방법을 포함 하 여 QPS에 대 한 참조 [검색 서비스 관리](search-manage.md)합니다.

## <a name="increase-indexing-performance-with-partitions"></a>파티션으로 인덱싱 성능 향상
거의 실시간으로 진행되는 데이터 새로 고침을 필요로 하는 검색 응용 프로그램은 복제본보다 비례적으로 더 많은 파티션이 필요합니다. 파티션을 추가하면 많은 수의 계산 리소스로 읽기/쓰기 작업이 분산됩니다. 또한 추가 인덱스와 문서를 저장하기 위한 더 많은 디스크 공간이 보장됩니다.

더 큰 인덱스 긴 tooquery를 수행합니다. 따라서 파티션을 증분 방식으로 증가시킬 때마다 더 작지만 비례적으로 복제본도 늘려야 합니다. 쿼리 및 쿼리 볼륨의 hello 복잡성 쿼리 실행을 돌리면 속도에 영향을 미치게 됩니다.

## <a name="basic-tier-partition-and-replica-combinations"></a>기본 계층: 파티션 및 복제본 조합
기본 서비스 정확히 하나의 파티션만 포함할 수 및 최대 3 개의 SUs 최대 제한에 대 한 toothree 복제본 합니다. hello만 조정 가능한 리소스는 복제본입니다. 쿼리에서 고가용성을 위해 최소 두 개의 복제본이 필요합니다.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>표준 계층: 파티션 및 복제본 조합
이 테이블에는 복제 데이터베이스 및 파티션, 모든 표준 계층에 대해 주체 toohello 36 SU 제한, hello SUs 필요한 toosupport 조합을 보여 줍니다.

|   | **파티션 1개** | **파티션 2개** | **파티션 3개** | **파티션 4개** | **파티션 6개** | **파티션 12개** |
| --- | --- | --- | --- | --- | --- | --- |
| **복제본 1개.** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **복제본 2개** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **복제본 3개** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **복제본 4개** |4 SU |8 SU |12 SU |16 SU |24 SU |해당 없음 |
| **복제본 5개** |5 SU |10 SU |15 SU |20 SU |30 SU |해당 없음 |
| **복제본 6개** |6 SU |12 SU |18 SU |24 SU |36 SU |해당 없음 |
| **복제본 12개** |12 SU |24 SU |36 SU |해당 없음 |해당 없음 |해당 없음 |

SUs, 가격 및 용량 hello Azure 웹 사이트에 자세히 설명 되어 있습니다. 자세한 내용은 [가격 정보](https://azure.microsoft.com/pricing/details/search/)를 참조하세요.

> [!NOTE]
> 복제본과 파티션 hello 수가 12를 균등 하 게 나눕니다. (특히, 1, 2, 3, 4, 6, 12). Azure 검색에서 각 인덱스를 모든 파티션 사이에 고르게 분할할 수 있도록 12개의 부분으로 미리 나누기 때문입니다. 예를 들어 서비스는 세 개의 파티션이 경우 인덱스를 만들면 각 파티션에 hello 인덱스의 분할 4 개의 영역이 포함 됩니다. Azure 검색에서 인덱스를 분할 구현 정보를 어떻게 주체 toochange 나중에 해제 합니다. Hello는 분할 수가 12 오늘, 있지만 tooalways 번호는 hello 12 미래 여야 기대 하지는 마십시오.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>복제본 및 파티션 리소스에 대한 청구 수식
hello 수식을 계산 개수 SUs 특정 조합에 사용 되는 복제본과 파티션 hello 제품 또는 (R X P = SU). 예를 들어 복제본 3개에 파티션 3개를 곱하여 SU 9개가 청구됩니다.

SU 당 비용 단위 청구 속도가 느린 표준에 대 한 보다 basic hello 계층에 의해 결정 됩니다. 각 계층에 대한 요금은 [가격 정보](https://azure.microsoft.com/pricing/details/search/)에서 확인할 수 있습니다.
