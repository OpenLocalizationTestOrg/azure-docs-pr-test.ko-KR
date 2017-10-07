---
title: "Azure Data Catalog에 관리 분류 용 hello 비즈니스 용어집을 aaaSet | Microsoft Docs"
description: "방법 tooarticle 강조 hello 비즈니스 용어집을 정의 하 고 일반적인 비즈니스 어휘 tootag를 사용 하 여 Azure Data Catalog에 등록 된 데이터 자산입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>태그 지정을 제어에 대 한 hello 비즈니스 용어집를 활용 설정
## <a name="introduction"></a>소개
Azure Data Catalog 쉽게 검색 하 고 이해 hello 데이터 소스 tooperform 분석 필요 하 고 결정을 내릴 수 있도록 데이터 원본 검색을 수 있습니다. 이러한 기능을 찾아 hello 광범위 한 사용 가능한 데이터 소스를 이해 하는 경우 hello 가장 큰 영향을 확인 합니다.

자산 데이터에 대한 이해를 크게 증진하는 데이터 카탈로그의 한 가지 기능이 태그 지정합니다. 태그를 사용 하 여 키워드 자산 또는 차례로 하므로 검색 또는 탐색을 통해 보다 쉽게 toodiscover hello 자산은 열과 연결할 수 있습니다. 또한 태그를 지정 하면 hello 컨텍스트와 hello asset의 의도 쉽게 이해할 수 있습니다.

하지만 태그 지정이 자체적으로 문제를 유발하는 경우도 있습니다. 태그 지정을 통해 발생할 수 있는 문제의 예:

* hello 일부 자산에 대 한 약어 및 다른 사용자에 확장 된 텍스트를 활용 합니다. 이러한 불일치는에 방해가 됩니다 한 자산 hello 검색 되었지만 hello 의도 hello 사용 하 여 tootag hello 자산 같은 태그입니다.
* 의미의 잠재적 변형은 컨텍스트에 따라 다릅니다. 예를 들어 태그 라는 *수익* 고객 데이터 집합 고객이 수익 의미 의미 하는 hello 분기별 판매 데이터 집합에 동일한 태그 수 hello 회사에 대 한 분기별 수익입니다.  

toohelp 이러한 오류 코드 및 다른 유사한 문제 해결, 데이터 카탈로그 포함 비즈니스 용어집를 활용 합니다.

Hello 데이터 카탈로그 비즈니스 용어집을 사용 하 여 조직 주요 비즈니스 용어 및 해당 정의 toocreate 공통적인 비즈니스 용어 모음을 문서화할 수 있습니다. 이 거 버 넌이 스 hello 조직에서 사용 현황 데이터의에서 일관성을 사용합니다. 지정 하는 단어 hello 비즈니스 용어집를 활용에 정의 된 후 tooa 데이터 자산 hello 카탈로그에 할당할 수 있습니다. 이 방법은 *태그 지정을 제어*는 hello와 동일한 방식으로 태그를 지정 합니다.

## <a name="glossary-availability-and-privileges"></a>용어집 가용성 및 권한
hello 비즈니스 용어집를 활용 hello 표준 버전의 Azure Data Catalog만 제공 됩니다. hello 데이터 카탈로그의 무료 버전이 용어집을 보려면 없으며 관리 태그에 대 한 기능을 제공 하지는 않습니다.

Hello 비즈니스 용어집를 활용 hello 통해 액세스할 수 있습니다 **용어집** hello Data Catalog 포털 탐색 메뉴에서 옵션입니다.  

![Hello 비즈니스 용어집를 활용에 액세스](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Hello 용어집 만들 수 있는 관리자 역할의 구성원과 데이터 카탈로그 관리자 편집 및 hello 비즈니스 용어집를 활용에 용어집 용어를 삭제 합니다. 모든 데이터 카탈로그 사용자 hello 용어 정 및 용어집 용어를 사용 하 여 태그 자산 볼 수 있습니다.

![새 용어 추가](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>용어 만들기
데이터 카탈로그 관리자와 용어집 관리자 hello를 클릭 하 여 용어집 용어를 만들 수 **새 용어** 단추입니다. 각 용어집 용어 hello를 다음 필드가 포함 되어 있습니다.

* Hello 용어에 대 한 비즈니스 정의
* Hello 자산 또는 열에 대 한 의도 한 hello 또는 비즈니스 규칙을 캡처하는 설명
* Hello 용어에 대 한 가장 hello 아는 이해 관계자의 목록
* hello 용어는 구성 하는 hello 계층 구조를 정의 하는 hello 상위 용어

## <a name="glossary-term-hierarchies"></a>용어 계층 구조
Hello 데이터 카탈로그 비즈니스 용어집을 사용 하 여 조직 용어에 대 한 계층 구조와 해당 비즈니스 용어 모음을 설명할 수 및 해당 비즈니스 분류를 보다 잘 나타내는 용어의 분류를 만들 수 있습니다.

용어는 지정된 수준의 계층 구조에서 고유해야 합니다. 중복 이름은 허용되지 않습니다. 계층의 수준 수 없는 제한 toohello는 없지만 계층은 종종 보다 쉽게 이해할 수 있는 세 가지 수준 이하의 경우.

계층에서 hello 비즈니스 용어집를 활용 hello 사용은 선택 사항입니다. 종료 hello 상위 용어 필드 용어집 용어에 대 한 빈 hello 용어집에서 용어 단순 (비 계층적) 목록을 만듭니다.  

## <a name="tagging-assets-with-glossary-terms"></a>용어를 사용하여 자산에 태그 지정
Hello 카탈로그 내에서 용어집 용어를 정의한 후 hello 자산 태그 지정의 환경은 최적화 toosearch hello 용어집으로 태그를 입력 합니다. hello Data Catalog 포털에서 일치 하는 용어집 용어 toochoose 목록이 표시 됩니다. 용어집 용어 hello 목록에서 선택 하는 hello 사용자, hello 용어 toohello 자산 태그 (용어집 태그 라고도 함)으로 추가 됩니다. hello 사용자 선택할 수도 toocreate 새 태그 hello에 없는 단어를 입력 하 여 용어 설명 (사용자 정의 태그 라고도 함).

![사용자 태그 하나와 용어집 태그 두 개가 지정된 데이터 자산](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> 지원 되는 태그의 형식을 hello 데이터 카탈로그의 무료 버전에만 사용자 태그는 hello를 됩니다.
>
>

### <a name="hover-behavior-on-tags"></a>태그 가리키기 동작
Hello Data Catalog 포털 hello 두 가지 유형의 태그는 시각적으로 고유 하 고 있는 다른 가리키기 동작 합니다. 사용자 정의 태그를 마우스로 가리키면 hello 태그 텍스트 및 hello 사용자 또는 hello 태그 추가 사용자를 볼 수 있습니다. 용어집 태그를 마우스로 가리키면 hello 용어집 용어의 hello 정 및 링크 tooopen hello 비즈니스 용어집 tooview hello 전체 정의 hello 용어의 표시 됩니다.

### <a name="search-filters-for-tags"></a>태그에 대한 검색 필터
용어집 태그와 사용자 태그 모두 검색이 가능하며, 검색에 필터로 적용할 수 있습니다.

## <a name="summary"></a>요약
Azure Data Catalog 및 hello 적용 하면 태그 지정의 hello 비즈니스 용어집을 사용 하 여 식별, 관리 및 데이터 자산 일관 된 방식으로 검색할 수 있습니다. hello 비즈니스 용어집를 활용 학습 조직 구성원이 hello 비즈니스 용어 모음을 승격할 수 있습니다. hello 용어집 자산 검색 및 이해를 손쉽게 있는 의미 있는 메타 데이터를 캡처를 지원 합니다.

## <a name="next-steps"></a>다음 단계
* [비즈니스 용어집 작업에 대한 REST API 설명서](https://msdn.microsoft.com/library/mt708855.aspx)
