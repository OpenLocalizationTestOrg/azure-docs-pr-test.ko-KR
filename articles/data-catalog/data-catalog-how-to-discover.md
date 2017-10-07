---
title: "Azure Data Catalog에서 aaaHow toodiscover 데이터 원본을 | Microsoft Docs"
description: "이 문서에서는 toodiscover Azure Data catalog를 검색 및 필터링을 포함 하 여 데이터 자산을 등록 하는 방법을 키를 누릅니다 hello를 사용 하 여 hello Azure Data Catalog 포털의 기능을 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Azure Data Catalog에서 toodiscover 데이터 원본 하는 방법
## <a name="introduction"></a>소개
Azure Data Catalog는 기업 데이터 원본의 등록 시스템 및 검색 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 다시 말해서 데이터 카탈로그는 사람들이 데이터 원본을 검색하고 이해하고 사용하도록 도우면서 조직의 기존 데이터로부터 더 많은 가치를 얻어내도록 돕는 역할을 합니다. 데이터 소스 Data Catalog에 등록 되 면 toodiscover hello 필요한 데이터를 쉽게 검색할 수 있도록 해당 메타 데이터는 hello 서비스에 의해 인덱싱됩니다.

## <a name="searching-and-filtering"></a>검색 및 필터링
데이터 카탈로그에서 검색은 검색 및 필터링이라는 두 가지 기본 메커니즘을 사용합니다.

검색은 설계 된 toobe 직관적이 고 강력 합니다. 기본적으로 검색 단어 hello 카탈로그에서 사용자가 제공한 주석 포함 한 모든 속성에 대해 일치 합니다.

필터링 기능은 toocomplement 검색 합니다. 전문가, 데이터 원본 유형, 개체 유형 및 태그 등의 특정 특성을 선택할 수 있습니다. 일치 하는 유일한 데이터 자산을 볼 수 있으며 검색 결과 toomatching 자산을 제한할 수 있습니다.

검색 및 필터링 조합의 사용 하 여 필요한 데이터 카탈로그 toodiscover hello 데이터 원본에 등록 된 hello 데이터 소스를 신속 하 게 이동할 수 있습니다.

## <a name="search-syntax"></a>검색 구문
간단 하 고 직관적인 hello 기본 자유 텍스트 검색 되어도 hello 검색 결과 보다 효율적으로 제어 데이터 카탈로그 검색 구문을 사용할 수도 있습니다. 데이터 카탈로그 검색 지원 hello 기술을 다음:

| 기법 | 사용 | 예 |
| --- | --- | --- |
| 기본 검색 |기본 검색은 하나 이상의 검색 용어를 사용합니다. 결과 하나 이상의 지정 된 hello 용어와 모든 속성과 일치 하는 모든 자산입니다. |`sales data` |
| 속성 범위 |지정한 속성을 hello로 hello 검색 단어와 일치 하는 유일한 데이터 원본을 반환 합니다. |`name:finance` |
| 부울 연산자 |부울 연산을 사용하여 검색을 확대하거나 축소합니다. |`finance NOT corporate` |
| 괄호로 그룹화 |괄호 toogroup 부분의 hello 쿼리 tooachieve 논리, 특히에서 격리 부울 연산자와 함께 사용 합니다. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| 비교 연산자 |숫자 및 날짜 데이터 유형이 있는 속성에 대한 일치가 아닌 비교를 사용합니다. |`modifiedTime > "11/05/2014"` |

카탈로그 데이터 검색에 대 한 자세한 내용은 참조 hello [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) 문서.

## <a name="hit-highlighting"></a>적중 항목 강조 표시
지정 하는 hello와 일치 하는 속성 표시 된 검색 결과 볼 때 검색 단어 (예: hello 데이터 자산 이름, 설명 및 태그)는 toomake 강조 표시 된 것 보다 쉽게 tooidentify 지정 된 데이터 자산 주어진된 검색에서 반환 된 이유입니다.

> [!NOTE]
> 강조 표시를 사용 하 여 hello 적중 오프 tooturn **강조 표시** hello Data Catalog 포털에서 전환 합니다.
>
>

검색 결과를 볼 때 적중 항목 강조 표시가 활성화되어 있더라도 데이터 자산이 포함된 이유가 항상 명확하지는 않을 수도 있습니다. 모든 속성은 기본적으로 검색되므로 열 수준 속성과 일치로 인해 데이터 자산이 반환될 수 있습니다. 및 여러 사용자가 자신의 태그 및 설명을 사용 하 여 등록 된 데이터 자산 주석을 달 수 때문에 일부 메타 데이터 검색 결과의 hello 목록에 표시 될 수 있습니다.

Hello 검색 결과에 표시 되는 각 타일에 포함 되어 hello 기본 타일 보기에는 **보기 검색 단어와 일치** 아이콘을 원하는 경우에 신속 하 게 일치 하는 항목 및 해당 위치와 toojump toothem hello 수를 볼 수 있도록 합니다.

 ![방문 횟수 강조 하 고 hello Azure Data Catalog 포털에서 검색 일치](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>요약
구조적 및 설명이 포함 된 데이터 카탈로그를 복사 하 여 데이터 원본을 등록할 hello 데이터의 메타 데이터를 원본 toohello 카탈로그 서비스에 있으므로 hello 데이터 원본을 보다 쉽게 toodiscover 되며 이해 합니다. 데이터 소스를 등록 한 후에 필터링을 사용 하 여 검색 하 고 hello Data Catalog 포털 내에서 검색 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 방법에 대 한 단계별 정보에 대 한 toodiscover 데이터 원본 참조 [Azure Data Catalog 시작](data-catalog-get-started.md)합니다.
