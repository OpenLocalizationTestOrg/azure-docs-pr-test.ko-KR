---
title: "aaaHow tooannotate 데이터 소스 | Microsoft Docs"
description: "방법 tooarticle 강조 표시 방법을 tooannotate 데이터 자산 친숙 한 이름, 태그, 설명, 전문가 등 Azure 데이터 카탈로그에 있습니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>어떻게 tooannotate 데이터 원본
## <a name="introduction"></a>소개
**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 즉, 데이터 카탈로그는 모두에 대 한 검색, 이해 하 고, 데이터 원본을 사용할 수 있도록 하 고 기존 데이터에서 조직 tooget 더 많은 값을 지원 합니다. 데이터 카탈로그와 데이터 소스를 등록 하는 경우 해당 메타 데이터를 복사 하 여 hello 서비스에 의해 인덱싱된 있지만 hello 스토리 다 하지 않습니다. 데이터 카탈로그 허용 사용자 tooprovide 자체 설명 메타 데이터-예: 설명 및 태그 – toosupplement hello 메타 데이터 hello 데이터 원본에서 추출 하 고 toomake hello 데이터 소스 더 많은 이해할 수 있는 toomore 사용자 키를 누릅니다.

## <a name="annotation-and-crowdsourcing"></a>주석 및 크라우드소싱
모든 사람은 의견이 있습니다. 이는 좋은 일입니다.
데이터 카탈로그는 다양한 사용자는 엔터프라이즈 데이터 원본에 대해 다양한 관점이 있으며 각 관점은 가치가 있다는 것을 인식하고 있습니다. Hello를 시나리오를 따르는 것이 좋습니다.

* 시스템 관리자에 게 해당 호스트 hello 데이터 원본을 hello hello 서버 또는 서비스에 대 한 서비스 수준 계약을 알고 있습니다.
* 데이터베이스 관리자에 게 hello 백업 각 데이터베이스에 대 한 일정 및 허용 된 ETL 처리 windows hello를 알고 있습니다.
* hello 시스템 소유자 사용자 toorequest access toohello 데이터 원본에 대 한 hello 프로세스를 알고 있습니다.
* 데이터 관리자가 hello hello 데이터 원본에는 특성과 hello 자산 toohello enterprise 데이터 모델 매핑하는 방법을 알고 있습니다.
* hello 분석가 hello 데이터가 원하는 그 hello 비즈니스 프로세스의 hello 컨텍스트에서 사용 되는 방법을 알고 있습니다.

이러한 큐브 뷰를 각각 유용 하 고 데이터 카탈로그 각 하나의 toobe 캡처하고 tooprovide 등록 된 데이터 원본에 대 한 전체적인 그림을 사용을 허용 하는 crowdsourcing 접근 방식을 toometadata를 사용 합니다. Hello Data Catalog 포털을 사용 하는 각 사용자 추가 및 편집할 수 자신의 주석 수 tooview 주석에서 다른 사용자에 게 제공 되는 동안 합니다.

## <a name="different-types-of-annotations"></a>다양한 유형의 주석
데이터 카탈로그 지원 hello 주석 유형만:

| 주석 | 참고 사항 |
| --- | --- |
| 친숙한 이름 |친숙 한 이름은 toomake hello 데이터 자산에서 더 쉽게 이해 hello 데이터 자산 수준에서 제공 될 수 있습니다. 친숙 한 이름을 hello 기본 개체 이름이 toousers 암호화, 약식 또는 그렇지 않은 경우 의미가 없을 때 가장 유용 합니다. |
| 설명 |Hello 데이터 자산 및 특성에 대 한 설명을 제공할 수 있습니다 / 열 수준입니다. 설명은은 hello 데이터 자산에 대해 hello 사용자의 관점 또는 용도 설명 하는 자유 형식 짧은 텍스트 주석이 됩니다. |
| 태그(사용자 태그) |태그 데이터 자산으로 hello 및 특성에 제공 될 수 있습니다 / 열 수준입니다. 사용자 태그는 사용자 지정 레이블을 사용 하는 toocategorize 데이터 자산 또는 특성 일 수 있는입니다. |
| 태그(용어집 태그) |태그 데이터 자산으로 hello 및 특성에 제공 될 수 있습니다 / 열 수준입니다. 용어집 태그는 사용 되는 toocategorize 데이터 자산 또는 일반적인 비즈니스 분류를 사용 하 여 특성 수 있는 용어를 중앙에서 정의 된 설명입니다. 자세한 내용은 참조 [를 tooset 비즈니스 용어집를 활용 태그 지정 제어에 대 한 hello 하는 방법](data-catalog-how-to-business-glossary.md) |
| 전문가 |전문가는 hello 데이터 자산 수준에서 제공 될 수 있습니다. 전문가 hello 데이터에 대 한 전문 큐브 뷰를 사용자 또는 그룹을 식별 하 고 hello를 검색 하는 사용자에 대 한 연결 지점 데이터 원본 등록 및 hello 기존 주석에서 답하지 않은 질문이 있는 사용할 수 있습니다. |
| 액세스 요청 |Hello 데이터 자산 수준에서 요청 정보에 액세스를 제공할 수 있습니다. 이 정보는 사용자에 게는 아직 없는 사용 권한을 tooaccess 데이터 소스를 검색 합니다. 사용자가 액세스 권한을 부여, URL hello 프로세스의 hello 또는 액세스 하는 필요성 toogain, 도구 또는 텍스트로 hello 프로세스 자체를 입력할 수 있는 hello 사용자 또는 그룹의 hello 전자 메일 주소를 입력할 수 있습니다. |
| 설명서 |설명서는 hello 데이터 자산 수준에서 제공 될 수 있습니다. 자산 설명서는 링크와 이미지를 포함할 수 있으며 설명과 태그를 통해 전달되지 않은 어떠한 정보든 제공할 수 있는 서식 있는 텍스트 정보입니다. |

## <a name="annotating-multiple-assets"></a>여러 자산 주석 지정
여러 데이터 자산 hello Data Catalog 포털에서을 선택 하면 사용자가 한 번에 모든 선택 된 자산 주석을 달 수 있습니다. 주석은 tooall 선택한 자산을 쉽게 tooselect 만들기를 적용 하 고 관련된 데이터 자산에 대 한 일관 된 설명 및 태그 및 전문가 집합이 제공 됩니다.

> [!NOTE]
> 태그와 전문가 hello 데이터 카탈로그 데이터를 사용 하 여 등록 데이터 자산 등록 도구 소스도 제공 수 있습니다.
>
>

때 여러 테이블이 나 뷰, 열만 데이터 자산 서로 공통 되는 모든 선택을 선택 하면 표시 됩니다 hello Data Catalog 포털. 이 선택 된 모든 자산에 대 한 사용자가 tooprovide 태그와 hello 이름과 같은 이름을 가진 모든 열에 대 한 설명이 있습니다.

## <a name="annotations-and-discovery"></a>주석 및 검색
등록 하는 동안 hello 데이터 원본에서 추출 된 메타 데이터는 toohello 데이터 카탈로그 검색 인덱스를 추가 하는 데 hello와 마찬가지로 사용자가 제공한 메타 데이터도 인덱싱됩니다. 즉, 뿐만 아니라 않습니다 주석을 쉽게 발견할 사용자 toounderstand hello 데이터에 대 한 주석을 쉽게 사용자 toodiscover hello 주석이 지정 된 데이터 자산에 대 한 의미 toothem 하는 hello 용어를 사용 하 여 검색 합니다.

## <a name="summary"></a>요약
Data catalog 데이터 원본 등록 쉽게 hello 카탈로그 서비스에 hello 데이터 원본의 구조 및 설명이 포함 된 메타 데이터를 복사 하 여 데이터를 검색할 수 있습니다. 데이터 원본 등록 되 면 사용자가 주석을 toomake 쉽게 toodiscover을 제공 hello Data Catalog 포털 내에서 이해 해야 합니다.

## <a name="see-also"></a>참고 항목
* [Azure Data Catalog 시작](data-catalog-get-started.md) 방법에 대 한 단계별 정보에 대 한 자습서 tooannotate 데이터 원본입니다.
