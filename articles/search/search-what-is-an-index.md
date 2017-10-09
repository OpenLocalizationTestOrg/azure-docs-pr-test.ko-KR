---
title: "Azure 검색 인덱스 aaaCreate | Microsoft Azure | 호스 티 드 클라우드 검색 서비스"
description: "Azure 검색의 인덱스란 무엇이고 어떻게 사용됩니까?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Azure 검색 인덱스 만들기
> [!div class="op_single_selector"]
> * [개요](search-what-is-an-index.md)
> * [포털](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>인덱스란?
*인덱스*는 Azure 검색 서비스에서 사용되는 *문서* 및 기타 구조의 지속형 저장소입니다. 문서는 인덱스에서 검색 가능한 데이터의 단일 단위입니다. 예를 들어 전자 상거래 소매점은 판매하는 각 항목에 대한 문서를 포함할 수 있으며 뉴스 조직은 각 기사에 대한 문서를 포함할 수 있습니다. 이러한 개념 toomore 친숙 한 데이터베이스 형식 매핑:는 *인덱스* 은 개념적으로 유사한 tooa *테이블*, 및 *문서* 너무 가지 방식은 거의 동일*행* 테이블에 있습니다.

때 하면 추가/업로드 문서 및 요청 tooa 특정 인덱스 검색 서비스에 제출 검색 쿼리 tooAzure 검색을 제출 합니다.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Azure 검색 인덱스에서 필드 형식 및 속성
스키마를 정의 하면 인덱스의 hello 이름, 형식 및 특성의 각 필드를 지정 해야 합니다. hello 필드 형식에는 해당 필드에 저장 된 hello 데이터 분류 됩니다. 특성이는 hello 필드 사용량 toospecify 개별 필드에 설정 됩니다. hello 다음 표에서 열거 hello 유형 및 속성을 지정할 수 있습니다.

### <a name="field-types"></a>필드 형식
| 메시지를 입력한 다음 | 설명 |
| --- | --- |
| *Edm.String* |전체 텍스트 검색을 위해 선택적으로 토큰화할 수 있는 텍스트입니다(단어 분리, 형태소 분석 등). |
| *Collection(Edm.String)* |전체 텍스트 검색을 위해 선택적으로 토큰화할 수 있는 문자열 목록입니다. Hello, 컬렉션의 항목 수에 이론적인 제한이 없어집니다 있지만 hello 16MB 상한 페이로드 크기 toocollections 적용 됩니다. |
| *Edm.Boolean* |true/false 값을 포함합니다. |
| *Edm.Int32* |32비트 정수 값입니다. |
| *Edm.Int64* |64비트 정수 값입니다. |
| *Edm.Double* |배정밀도 숫자 데이터입니다. |
| *Edm.DateTimeOffset* |날짜 시간 값 hello OData V4 형식으로 표현 됩니다 (예: `yyyy-MM-ddTHH:mm:ss.fffZ` 또는 `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Hello 전 세계의 지리적 위치를 나타내는 지점입니다. |

Azure Search의 [지원되는 데이터 형식에 대한 자세한 내용은 여기서](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 확인할 수 있습니다.

### <a name="field-attributes"></a>필드 특성
| 특성 | 설명 |
| --- | --- |
| *키* |문서 조회에 사용 되는 각 문서의 hello 고유 ID를 제공 하는 문자열입니다. 모든 인덱스에는 하나의 키가 있어야 합니다. 필드를 하나만 hello 키가 될 수 있습니다 및 tooEdm.String 해당 유형을 설정 해야 합니다. |
| *조회 가능* |검색 결과에서 필드를 반환할 수 있는지 여부를 지정합니다. |
| *필터링 가능* |Hello 필드 toobe를 필터 쿼리에서 사용할 수 있습니다. |
| *정렬 가능* |이 필드를 사용 하 여 toosort 검색 결과 쿼리를 허용 합니다. |
| *패싯 가능* |사용 되는 필드 toobe 허용는 [패싯 탐색](search-faceted-navigation.md) 사용자 자체 방향이 지정 된 필터링에 대 한 구조입니다. 일반적으로 toogroup를 사용할 수 있는 반복적인 값을 포함 하는 필드 함께 여러 문서 (예를 들어 여러 문서 단일 브랜드 또는 서비스 범주에 속하는) 적합 패싯으로 합니다. |
| *검색 가능* |전체 텍스트 검색 가능한 필드를 hello 하는 표시 합니다. |

Azure Search의 [인덱스 특성은 여기서](https://docs.microsoft.com/rest/api/searchservice/Create-Index) 확인할 수 있습니다.

## <a name="guidance-for-defining-an-index-schema"></a>인덱스 스키마를 정의하기 위한 지침
인덱스를 디자인할 때 각 의사 결정을 통해 단계 toothink 계획 hello에 시간 걸릴. 각 필드 hello를 할당 해야 하는 대로 인덱스를 디자인할 때 염두에 검색 사용자 환경과 비즈니스 요구 유지 한다는 것 [적절 한 특성](https://docs.microsoft.com/rest/api/searchservice/Create-Index)합니다. 배포 후에 인덱스를 변경 다시 작성 하 고 hello 데이터를 다시 로드 해야 합니다.

데이터 저장소 요구 사항이 시간이 지남에 따라 변하는 경우 파티션을 추가하거나 제거하여 용량을 늘리거나 줄일 수 있습니다. 자세한 내용은 [Azure에서 검색 서비스 관리](search-manage.md) 또는 [서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.

