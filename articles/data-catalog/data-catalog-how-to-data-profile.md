---
title: "aaaHow tooData 프로 파일 데이터 원본"
description: "방법-tooarticle tooinclude 테이블 및 열 수준 데이터의 데이터 원본을 Azure Data Catalog에 등록 하는 경우 프로필 어떻게 및 어떻게 toouse 데이터 프로필 toounderstand 데이터 소스를 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>데이터 원본 데이터 프로파일링
## <a name="introduction"></a>소개
**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 즉, **Azure Data Catalog** 수 있도록 지 원하는 사용자에 대 한 모든 검색, 이해 하 고, 데이터 원본을 사용 하 고 기존 데이터에서 더 값 조직 tooget 수 있도록 지원 됩니다. 데이터 원본으로 등록 될 때 **Azure Data Catalog**hello 스토리 끝나지 있습니다 하지만 해당 메타 데이터를 복사 하 여 hello 서비스에 의해 인덱싱된, 합니다.

hello **데이터 프로 파일링** 의 기능 **Azure Data Catalog** 카탈로그에서 지원 되는 데이터 원본의 hello 데이터를 검사 하 고 통계와 해당 데이터에 대 한 정보를 수집 합니다. 되기 쉬운 tooinclude 데이터 자산에 대 한 프로필. 데이터 자산을 등록 하면 선택 **포함 데이터 프로필** hello 데이터 원본 등록 도구에서 합니다.

## <a name="what-is-data-profiling"></a>데이터 프로파일링의 정의
데이터 프로 파일링 hello hello 데이터 원본의 데이터에 등록 되를 검사 하 고 통계와 해당 데이터에 대 한 정보를 수집 합니다. 데이터 원본 검색 하는 동안 이러한 통계 확인할 수 있습니다 hello 데이터 toosolve의 hello 적합성 비즈니스 문제입니다.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

hello 다음 데이터 원본 지원 데이터 프로 파일링 합니다.

* SQL Server(Azure SQL DB 및 Azure SQL 데이터 웨어하우스 포함) 테이블 및 뷰
* Oracle 테이블 및 뷰
* Teradata 테이블 및 뷰
* Hive 테이블

데이터 자산을 등록할 때 데이터 프로필을 포함하면 사용자가 다음을 비롯한 데이터 원본에 대한 질문에 대답하도록 도움을 줍니다.

* 수 있는 비즈니스 문제 사용된 toosolve 수 있습니까?
* Tooparticular 표준 또는 패턴 hello 데이터 준수는?
* Hello 비정상 hello 데이터 원본 중 일부 무엇입니까?
* 내 응용 프로그램에 이 데이터를 통합할 경우 발생할 수 있는 문제는 무엇인가요?

> [!NOTE]
> 응용 프로그램으로 데이터를 통합 하는 방법을 설명서 tooan 자산 toodescribe를 추가할 수 있습니다. 참조 [어떻게 toodocument 데이터 원본](data-catalog-how-to-documentation.md)합니다.
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>데이터 원본을 등록할 때 tooinclude 데이터 프로 파일링 할 방법
되기 쉬운 tooinclude 데이터 원본에 대 한 프로필. Hello에 데이터 소스를 등록 하면 **등록 개체 toobe** hello 데이터 원본 등록의 패널 도구를 선택 **포함 데이터 프로필**합니다.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

tooregister 데이터 원본을 참조 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooregister 데이터 원본](data-catalog-how-to-register.md) 및 [Azure Data Catalog 시작](data-catalog-get-started.md)합니다.

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>데이터 프로필을 포함하는 데이터 자산에 대한 필터링
데이터 프로필을 포함 하는 toodiscover 데이터 자산을 포함 시킬 수 있습니다 `has:tableDataProfiles` 또는 `has:columnsDataProfiles` 검색 단어 중 하나로 합니다.

> [!NOTE]
> 선택 하면 **포함 데이터 프로필** 테이블 및 열 수준 프로필 정보를 모두에 hello 데이터 원본 등록 도구를 포함 합니다. 그러나 hello 데이터 카탈로그 API를 통해 데이터 자산 toobe 프로필 포함 되는 정보 집합을 하나만 등록 합니다.
>
>

## <a name="viewing-data-profile-information"></a>데이터 프로필 정보 보기
프로필에 적절 한 데이터 소스를 찾은 후 hello 데이터 프로필 세부 정보를 볼 수 있습니다. tooview hello 데이터 프로필을 선택 하는 데이터 자산 선택 **데이터 프로필** hello Data Catalog 포털 창에서.

![](media/data-catalog-data-profile/data-catalog-view.png)

**Azure Data Catalog** 의 데이터 프로필은 다음을 포함하여 테이블 및 열 프로필 정보를 보여줍니다.

### <a name="object-data-profile"></a>개체 데이터 프로필
* 행 수
* 테이블 크기
* Hello 개체가 마지막으로 업데이트

### <a name="column-data-profile"></a>열 데이터 프로필
* 열 데이터 형식
* 고유한 값 수
* NULL 값이 있는 행 수
* 열 값에 대한 최소, 최대, 평균 및 표준 편차

## <a name="summary"></a>요약
데이터 프로 파일링 통계를 제공 하 고 정보에 대 한 등록 데이터 자산 toohelp hello 데이터 toosolve 비즈니스 문제의 hello 한지를 결정 합니다. 주석 달기 및 데이터 원본을 문서화하는 작업과 함께 데이터 프로필은 사용자가 데이터를 잘 이해할 수 있도록 합니다.

## <a name="see-also"></a>참고 항목
* [어떻게 tooregister 데이터 원본](data-catalog-how-to-register.md)
* [Azure Azure Data Catalog 시작](data-catalog-get-started.md)
