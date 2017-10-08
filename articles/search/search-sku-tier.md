---
title: "aaaChoose SKU Azure 검색에 대 한 가격 책정 계층 또는 | Microsoft Docs"
description: "Azure 검색은 무료, 기본 및 표준 SKU로 프로비전할 수 있습니다. 여기서 표준은 다양한 리소스 구성 및 용량 수준으로 사용 가능합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Azure 검색에 대한 SKU 또는 가격 책정 계층 선택
Azure Search에서는 특정 가격 책정 계층 또는 SKU에서 [서비스가 프로비전](search-create-service-portal.md)됩니다. 선택 사항에는 **무료**, **기본**, **표준**이 있으며 **표준**은 여러 구성 및 용량으로 사용 가능합니다.

hello이 문서의 목적은 toohelp 계층을 선택 합니다. 계층의 수용 작업량이 확인 toobe 너무 낮게, tooprovision hello 더 높은 계층에서 새 서비스를 필요 한 후 인덱스를 다시 로드 합니다. 동일한 SKU tooanother 하나에서 서비스는 hello의 전체 업그레이드가 없습니다.

> [!NOTE]
> 계층을 선택한 후 및 [검색 서비스를 프로 비전](search-create-service-portal.md), 복제를 늘릴 수 있습니다 및 hello 서비스 내에서 파티션을 계산 합니다. 자세한 내용은 [Azure Search의 쿼리 및 인덱싱 작업을 위한 리소스 수준 확장](search-capacity-planning.md) 을 참조하세요.
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>어떻게 tooapproach는 가격 책정 계층 의사 결정
Azure 검색 hello 계층 용량을 지원 하지 않습니다 확인합니다. 일반적으로 미리 보기 기능을 비롯한 모든 기능을 모든 계층에서 사용할 수 있습니다. 한 가지 예외 hello S3 HD에는 인덱서에 대 한 지원은 없습니다.

> [!TIP]
> 경량 프로젝트에 쉽게 사용할 수 있도록 항상 **무료** 서비스(만료 없이 구독당 하나)를 프로비전하는 것이 좋습니다. 사용 하 여 hello **무료** hello에서 두 번째 청구 가능 서비스를 만들 수는 테스트 및 평가 대 한 서비스 **기본** 또는 **표준** 프로덕션 또는 더 큰 작업 부하 테스트에 대 한 계층입니다.
>
>

용량 및 hello 서비스 실행 비용을 직접에서 직접 이동 합니다. 이 문서의 정보 결정 SKU hello 올바른 균형을 제공 하는 데 도움이 하지만 그 중 하나에 대 한 toobe 유용한 hello 다음에 대 한 이상 대략적인 예상 해야 합니다.

* 개수와 크기 toocreate 인덱스 계획
* 문서 tooupload의 수 및 크기
* QPS(초당 쿼리 수)를 기준으로 한 쿼리 볼륨에 대한 아이디어

개수와 크기는 인덱스 또는 문서에는 서비스의 hello 수 또는 hello 서비스에서 사용 되는 리소스 (저장소 또는 복제본)는 하드 한도 통해 최대 제한에 도달 하기 때문에 중요 합니다. hello 실제에 대 한 서비스 제한은 첫 번째로 사용 되는 중: 리소스 또는 개체입니다.

손에 예상치, 단계를 수행 하는 hello hello 프로세스를 간소화 해야 합니다.

* **1 단계** toolearn 사용할 수 있는 옵션에 대 한 아래 hello SKU 설명을 검토 합니다.
* **2 단계** 예비 의사 결정에 tooarrive 아래 hello 질문에 대답 합니다.
* **3단계** 저장소 및 가격 책정에 대한 고정 한도를 검토하여 최종적으로 의사를 결정합니다.

## <a name="sku-descriptions"></a>SKU 설명
hello 다음 표에 각 계층 설명 합니다.

| 계층 | 기본 시나리오 |
| --- | --- |
| **Free** |공유 서비스, 무료, 평가, 조사 또는 소규모 워크로드에 사용됨. 다른 구독자와 공유 하는 때문에 쿼리 처리량 및 인덱싱 hello 서비스를 사용 하는 다른 사용자에 따라 다릅니다. 용량이 작습니다(각각 최대 10,000개의 문서가 있는 50MB 또는 3개의 인덱스). |
| **Basic** |전용 하드웨어에서 소규모 프로덕션 워크로드. 고가용성. 용량은 too3 복제본과 1 파티션 (2GB) 제공 됩니다. |
| **S1** |표준 1은 파티션(12) 및 복제본(12)의 유연한 조합을 지원, 전용 하드웨어에서 중간 규모 프로덕션 워크로드에 사용됩니다. 최대 36개의 청구 가능한 검색 단위로 지원되는 파티션 및 복제본의 조합을 할당할 수 있습니다. 이 수준에서 파티션은 각각 25GB이며 QPS는 초당 쿼리 수가 약 15개입니다. |
| **S2** |표준 2 S1 하지만 더 큰 크기의 파티션과 복제본 hello 동일한 36 검색 단위를 사용 하 여 더 큰 프로덕션 작업을 실행 합니다. 이 수준에서 파티션은 각각 100GB이며 QPS는 초당 쿼리 수가 약 60개입니다. |
| **S3** |표준 3 실행 비율에 따라 더 큰 프로덕션 작업 고성능 시스템의 too12 파티션 또는 12 복제본을 구성에서 검색 단위 제한인 36의 합니다. 이 수준에서 파티션은 각각 200GB이며 QPS는 초당 쿼리 수가 60개 이상입니다. |
| **S3 HD** |표준 3 고밀도는 더 많은 수의 더 작은 인덱스에 맞게 설계 되었습니다. 최대 200 g B에서 too3 파티션을 보유할 수 있습니다. QPS는 초당 쿼리 수가 60개 이상입니다. |

> [!NOTE]
> 복제 데이터베이스 및 파티션 최대값으로 어떤 hello 최대 외견상 의미 보다 낮은 유효 제한을 적용 하는 검색 단위 36 단위로 서비스 당 최대 아웃 요금이 청구 됩니다. 예를 들어, 12 복제본 toouse hello 최대 3 파티션을 최대 있을 수 있습니다 (12 * 3 = 36 단위가). 마찬가지로, toouse 최대 파티션, 복제본 too3을 줄입니다. 허용 가능한 조합에 대한 차트는 [Azure 검색의 쿼리 및 인덱싱 작업을 위한 리소스 수준 확장](search-capacity-planning.md) 을 참조하세요.
>
>

## <a name="review-limits-per-tier"></a>계층당 제한 검토
hello 다음 차트의 하위 집합인 hello 제한에서 [Azure 검색에서 서비스 제한](search-limits-quotas-capacity.md)합니다. Hello 요소 가능성이 가장 높은 tooimpact SKU 의사 결정을 나열합니다. Toothis 차트 아래 hello 질문을 검토할 때 참조할 수 있습니다.

| 리소스 | 무료 | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| SLA(서비스 수준 계약) |아니요 <sup>1</sup> |예 |예 |예 |예 |예 |
| 인덱스 제한 |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| 문서 제한 |총 10,000개 |서비스당 1백만 |파티션당 15백만 |파티션당 6천만 |파티션당 1억 2천만 |인덱스당 1백만 |
| 최대 파티션 |해당 없음 |1 |12 |12 |12 |3 <sup>2</sup> |
| 파티션 크기 |총 50MB |서비스당 2GB |파티션당 25GB |파티션 (위쪽 tooa 1.2 TB 당 최대 서비스) 당 100 GB |파티션 (위쪽 tooa 2.4 TB 당 최대 서비스) 당 200GB |200GB (위쪽 tooa 최대 600GB 서비스 당) |
| 최대 복제본 |해당 없음 |3 |12 |12 |12 |12 |
| 초당 쿼리 수 |해당 없음 |복제본당 3이하 |복제본당 15이하 |복제본당 60이하 |복제본당 60 초과 |복제본당 60 초과 |

<sup>1</sup> 무료 계층 및 미리 보기 기능에는 SLA(서비스 수준 계약)이 제공되지 않습니다. 모든 청구 가능 계층에 대해 서비스에 충분한 중복성을 프로비전할 때 SLA가 적용됩니다. 쿼리(읽기) SLA에는 두 개 이상의 복제본이 필요합니다. 쿼리 및 인덱싱(읽기/쓰기) SLA에는 세 개 이상의 복제본이 필요합니다. 파티션 수가 hello는 SLA 고려 사항 않습니다. 

<sup>2</sup> S3과 S3 HD는 동일한 대용량 인프라에서 지원되지만 각각 서로 다른 방식으로 최대 한도에 도달합니다. S3은 더 적은 수의 매우 큰 인덱스를 대상으로 합니다. 따라서 최대 한도는 리소스에 종속됩니다(서비스당 2.4TB). S3 HD는 많은 수의 매우 작은 인덱스를 대상으로 합니다. 1, 000 인덱스에 S3 HD에 인덱스 제약 조건의 hello 형태로 제한에 도달합니다. 1000 개 이상의 인덱스를 필요로 하 S3 HD 고객 인 경우는 방법에 대 한 내용은 Microsoft 지원에 문의 tooproceed 합니다.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>요구 사항에 맞지 않는 SKU를 제거합니다.
다음 질문 hello 도착 하는 작업에 대 한 올바른 SKU 결정 hello 수 있습니다.

1. **SLA(서비스 수준 약정)** 요구 사항이 있나요? 청구 가능 계층(기본 이상)이면 무엇이든 사용할 수 있지만 서비스는 백업을 위해 구성해야 합니다. 쿼리(읽기) SLA에는 두 개 이상의 복제본이 필요합니다. 쿼리 및 인덱싱(읽기/쓰기) SLA에는 세 개 이상의 복제본이 필요합니다. 파티션 수가 hello는 SLA 고려 사항 않습니다.
2. **얼마나 많은 인덱스** 가 필요한가요? Hello 가장 큰 변수를 만들 경우 SKU 의사 결정 중 하나에 각 SKU에서 지원 되는 인덱스의 hello 수입니다. 인덱스 지원 가격 계층 hello 낮은의 많이 다른 수준으로 됩니다. 인덱스 수에 대한 요구 사항은 SKU 결정의 기본 결정자일 수 있습니다.
3. **개수에 대해 설명** 각 인덱스에 로드 됩니다? hello 번호와 문서의 크기는 hello hello 인덱스의 최종 크기를 결정 합니다. 예상할 수 있는 것으로 가정 hello hello 인덱스의 예상된 크기를 해당 크기의 인덱스 파티션 필요한 toostore hello 수로 확장 SKU 당 hello 파티션 크기에 대해 해당 숫자를 비교할 수 있습니다.
4. **Hello 예상된 쿼리 부하를 이란**? 저장소 요구 사항을 이해했으면 쿼리 워크로드를 고려합니다. S2 및 두 S3 SKU는 거의 동등한 처리량을 제공하지만 SLA 요구 사항에서는 미리 보기 SKU를 배제합니다.
5. Hello S2 또는 S3 계층을 고려 하는 경우 필요 여부 결정 [인덱서](search-indexer-overview.md)합니다. 인덱서는 아직 hello S3 HD 계층에 사용할 수 있습니다. 대체 방법은 toouse 인덱스 업데이트에 대 한 밀어넣기 모델 응용 프로그램 코드 toopush를 쓰는 위치는 데이터 집합 tooan 인덱스입니다.

대부분의 고객에 위의 질문의 답변 toohello에 따라 한 특정 SKU 또는 축소 규칙 수입니다. 아직 모를 경우와 어떤 SKU toogo, 질문 tooMSDN 또는 StackOverflow 포럼 게시물 수도 있고 필요한 추가 지침에 대 한 Azure 지원에 문의할 수 있습니다.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>유효성 검사를 의사 결정:는 hello SKU 제공 충분 한 저장소 및 QPS?
마지막 단계로, hello 다시 방문 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/search/) 및 hello [서비스 제한의 서비스별 및 인덱스 당 섹션](search-limits-quotas-capacity.md) toodouble 검사 구독 및 서비스 제한에 대해 예상 작업량을 계산 합니다.

Hello 가격 또는 저장소 요구 사항 중 하나가 범위를 벗어나는 경우에 여러 개의 더 작은 서비스 간의 toorefactor hello 워크 로드 (예) 할 수 있습니다. 보다 세부적인 수준에 인덱스 toobe 작지만 다시 디자인할 수 또는 사용 toomake 쿼리를 보다 효율적으로 필터링 합니다.

> [!NOTE]
> 문서가 불필요한 데이터를 포함하는 경우 저장소 요구 사항이 지나치게 높을 수 있습니다. 이상적으로 문서는 검색 가능한 데이터 또는 메타데이터로만 구성됩니다. 이진 데이터는 검색할 수 없는 이며 hello 인덱스 toohold URL 참조 toohello 외부 데이터에에서 필드가 포함 된 (아마도 Azure 테이블 또는 blob 저장소)에 개별적으로 저장 되어야 합니다. 개별 문서의 hello 최대 크기는 16MB (또는 경우 덜 대량 한 요청에 대 한 여러 문서 업로드 중인). 자세한 내용은 [Azure 검색의 서비스 제한 사항](search-limits-quotas-capacity.md) 을 참조하세요.
>
>

## <a name="next-step"></a>다음 단계
SKU는 hello 오른쪽 맞춤 하는 것을 알고 있다면 다음이 단계를 계속 합니다.

* [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md)
* [서비스 파티션 및 복제본 tooscale의 hello 할당 변경](search-capacity-planning.md)
