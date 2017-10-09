---
title: "Azure 검색의 aaaService 제한 | Microsoft Docs"
description: "용량 계획에 사용되는 서비스 제한 및 Azure Search에 대한 요청 및 응답의 최대 제한입니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Azure 검색의 서비스 제한 사항
저장소, 워크로드 및 인덱스, 문서, 기타 개체의 수량에 대한 최대 제한은 Azure Search를 **무료**, **기본** 또는 **표준** 가격 책정 계층 중 [어디에 프로비전하는지](search-create-service-portal.md)에 따라 달라집니다.

* **무료** 는 Azure 구독과 함께 제공되는 다중 테넌트 공유 서비스입니다. 전용된 리소스에 등록 하기 전에 hello 서비스와 tooexperiment를 허용 하는 기존 구독자에 대 한 추가 비용 없음 옵션입니다.
* **기본**은 소규모의 프로덕션 워크로드를 위한 전용 컴퓨팅 리소스를 제공합니다.
* **표준**은 모든 수준에서 더 많은 저장소 및 처리 용량으로 전용 컴퓨터에서 실행됩니다. 표준은 4가지 수준인 S1, S2, S3 및 S3 HD(S3 고밀도)로 제공됩니다.

> [!NOTE]
> 서비스는 특정 계층에서 프로비전됩니다. Toojump 계층 tooget를 더 용량 해야 할 경우 (없습니다 전체 업그레이드는) 새 서비스를 프로 비전 해야 합니다. 자세한 내용은 [SKU 또는 계층 선택](search-sku-tier.md)을 참조하세요. 서비스 내에서 용량을 조정 하는 방법에 대 한 자세한 toolearn 했습니다 이미 프로 비전을 참조 하십시오. [확장 쿼리 및 인덱싱 작업에 대 한 리소스 수준](search-capacity-planning.md)합니다.
>

## <a name="per-subscription-limits"></a>구독당 제한
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>서비스당 제한
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>인덱스당 제한
인덱스에 대한 제한과 인덱서에 대한 제한 간에는 일대일 대응이 형성됩니다. 200 인덱스의 제한 들어 인덱서에 대 한 최대치 hello는 또한 200 hello에 대 한 동일한 서비스입니다.

| 리소스 | 무료 | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 인덱스: 인덱스당 최대 필드 |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| 인덱스: 인덱스당 최대 점수 매기기 프로필 |100 |100 |100 |100 |100 |100 |
| 인덱스: 프로필당 최대 함수 |8 |8 |8 |8 |8 |8 |
| 인덱서: 호출당 최대 인덱싱 로드 |10,000개 문서 |최대 문서에 의해서만 제한됨 |최대 문서에 의해서만 제한됨 |최대 문서에 의해서만 제한됨 |최대 문서에 의해서만 제한됨 |해당 없음<sup>2</sup> |
| 인덱서: 최대 실행 시간 | 1-3분 <sup>3</sup> |24시간 |24시간 |24시간 |24시간 |해당 없음<sup>2</sup> |
| Blob 인덱서: 최대 Blob 크기(MB) |16 |16 |128 |256 |256 |해당 없음<sup>2</sup> |
| Blob 인덱서: Blob에서 추출된 콘텐츠의 최대 문자 |32,000 |64,000 |400만 |400만 |400만 |해당 없음<sup>2</sup> |

<sup>1</sup> 기본 계층 인덱스 당 100 필드의 하한값으로 SKU만 hello 됩니다.

<sup>2</sup> S3 HD는 현재 인덱서를 지원하지 않습니다. 이 기능이 긴급하게 필요한 경우 Azure 지원 서비스에 문의하세요.

<sup>3</sup> hello 무료 계층에 대 한 최대 실행 시간 인덱서는 3 분 blob 원본 및 다른 모든 데이터 원본에 대해 1 분입니다.

## <a name="document-size-limits"></a>문서 크기 제한
| 리소스 | 무료 | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 인덱스 API당 개별 문서 크기 |16MB 미만 |16MB 미만 |16MB 미만 |16MB 미만 |16MB 미만 |16MB 미만 |

인덱스 API를 호출할 때 toohello 최대 문서 크기를 참조 합니다. 문서 크기는 실제로 hello 인덱스 API 요청 본문의 hello 크기 제한입니다. 여러 문서 toohello 인덱스 API 일괄 처리를 한 번에 전달할 수 있습니다, 때문 hello 크기 제한을 실제로 hello 일괄 처리에 있는 문서에 따라 다릅니다. 단일 문서와 일괄 처리에 대 한 hello 최대 문서 크기는 16MB JSON입니다.

아래로 tookeep 문서 크기 hello 요청에서 tooexclude 쿼리할 수 없는 데이터를 기억 합니다. 이미지 및 기타 이진 데이터 직접 쿼리 가능 되며 hello 인덱스에 저장 하지 않아야 합니다. 검색 결과를 쿼리할 수 없는 데이터 toointegrate URL 참조 toohello 리소스를 저장 하는 검색할 수 없는 필드를 정의 합니다.

## <a name="workload-limits-queries-per-second"></a>작업 제한(초당 쿼리 수)
| 리소스 | 무료 | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |해당 없음 |복제본당 3이하 |복제본당 15이하 |복제본당 60이하 |복제본당 60 초과 |복제본당 60 초과 |

Queries / sec (QPS)은 시뮬레이션 및 실제 고객 작업 부하 예상 tooderive 값을 사용 하 여 추론에 따라 추정치입니다. 정확한 QPS 처리량 hello 쿼리의 데이터 hello 특성에 따라 달라 집니다.

대략적인 예상 값으로, 위에서 제공 되지만 실제 속도가 hello 무료 공유 서비스의 시스템 리소스 경합 및 사용 가능한 대역폭에 따라 처리 위치에 특히 어려울 toodetermine입니다. Hello 무료 계층, 계산 및 저장소 리소스 공유 여러 구독자가 하므로 솔루션의 QPS은 hello에 실행 하는 다른 작업 수에 따라 다 항상 같은 시간입니다.

Hello 표준 수준에서 예측할 수 있습니다 QPS 더 밀접 하 게 하므로 hello 매개 변수를 자세히 제어할 수 있습니다. Hello의 모범 사례 섹션을 참조 [검색 솔루션 관리](search-manage.md) 방법에 대 한 지침은 toocalculate QPS 트 작업에 대 한 합니다.

## <a name="api-request-limits"></a>API 요청 제한
* 요청당 최대 16MB <sup>1</sup>
* URL 길이 최대 8KB
* 인덱스 업로드, 병합 또는 삭제 배치당 최대 1000개의 문서
* $orderby 절에 최대 32개의 필드
* 최대 검색어 크기는 UTF-8 인코딩된 텍스트로 32,766바이트(32KB에서 2바이트를 뺀 값)입니다.

<sup>1</sup> Azure 검색에서는 요청의 hello 본문 주체 tooan 상한값이 개별 필드 또는 이론적 제한으로 제한 되지 않으며 컬렉션의 hello 내용에 실질적 제한을 부과 16mb (참조 [지원 됨 데이터 형식](https://msdn.microsoft.com/library/azure/dn798938.aspx) 필드 컴퍼지션 및 제한 사항에 대 한 자세한 내용은).

## <a name="api-response-limits"></a>API 응답 제한
* 검색 결과 페이지당 반환되는 문서 최대 1000개
* 제안 API 요청당 반환되는 제안 최대 100개

## <a name="api-key-limits"></a>API 키 제한
API 키는 서비스 인증에 사용됩니다. 두 가지 형식이 있습니다. 관리자 키는 hello 요청 헤더에 지정 하 고 toohello 서비스 읽기 / 쓰기 액세스를 부여 합니다. 쿼리 키가 읽기 전용 hello URL 및 일반적으로 분산된 tooclient 응용 프로그램을 지정 합니다.

* 서비스당 최대 2개의 관리자 키
* 서비스당 최대 50개의 쿼리 키
