---
title: "aaaHow toodocument 데이터 소스 | Microsoft Docs"
description: "방법 tooarticle 강조 표시 방법을 toodocument 데이터 자산 Azure Data Catalog에 있습니다."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a>데이터 원본 문서화
## <a name="introduction"></a>소개
**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 즉, **Azure Data Catalog** 을 검색할 수 있도록 모두는 *이해*, 데이터 원본을 사용 하 고 기존 데이터에서 값 추가 조직 tooget 수 있도록 지원 합니다.

데이터 원본으로 등록 될 때 **Azure Data Catalog**hello 스토리 끝나지 있습니다 하지만 해당 메타 데이터를 복사 하 여 hello 서비스에 의해 인덱싱된, 합니다. **Azure Data Catalog** hello 사용량과 hello 데이터 원본에 대 한 일반적인 시나리오를 설명 하는 전체 설명서가 자신의 사용자 tooprovide를 수도 있습니다.

[어떻게 tooannotate 데이터 원본](data-catalog-how-to-annotate.md)는 hello 데이터 소스를 알고 있는 전문가 주석을 달 수 것 태그 및 설명을 사용 하 여는 방법을 배웁니다. hello **Azure Data Catalog** 포털 사용자는 데이터 자산 및 컨테이너에 완벽 하 게 문서화할 수 있도록 서식 있는 텍스트 편집기에 포함 되어 있습니다. hello 편집기 같은 단락 서식을 머리글의 텍스트 서식을 글머리 기호 목록, 번호 매기기 목록 및 테이블을 포함 합니다.

태그와 설명은 간단한 주석에 유용합니다. 그러나 toohelp 데이터 소비자는 데이터 원본의 hello 사용을 더 잘 이해 하 고 전문가 데이터 원본에 대 한 비즈니스 시나리오에서 완전 하 고 자세한 설명서를 제공할 수 있습니다. 되기 쉬운 toodocument 데이터 원본입니다. 데이터 자산 또는 컨테이너를 선택하고 **설명서**를 선택합니다.

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a>데이터 자산 문서화
이점은 hello **Azure Data Catalog** 설명서 있습니다 toouse 데이터 자산의 전체 narrative 콘텐츠 리포지토리 toocreate로 데이터 카탈로그입니다. 컨테이너 및 테이블을 설명하는 자세한 내용을 둘러볼 수 있습니다. SharePoint 또는 파일 공유와 같은 다른 콘텐츠 저장소의 콘텐츠를 이미 있는 경우이 기존 콘텐츠 toohello 자산 설명서 링크 tooreference를 추가할 수 있습니다. 이 기능을 사용해 기존 문서를 더 쉽게 검색할 수 있습니다.

> [!NOTE]
> 설명서는 검색 인덱스에 포함되지 않습니다.
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

hello 설명서의 수준에서 까지입니다 hello 특성 및 값의 데이터를 설명 하는 자산 컨테이너 tooa 세부 설명 컨테이너 내에서 테이블 스키마입니다. 제공 된 설명서 hello 수준의 비즈니스 요구 사항에 따라 결정 해야 합니다. 하지만 데이터 자산을 문서화하는 일반적인 몇 가지 장단점은 다음과 같습니다.

* 단지 문서화: 모든 hello 콘텐츠를 한 곳에는 하지만 수 부족 필요한 세부 정보를 사용자 toomake 합리적인된 결정 합니다.
* 방금 hello 테이블 문서: 콘텐츠 특정 toothat 개체가 아니라 사용자 문서에 대 한 여러 위치에 있어야 합니다.
* 컨테이너와 테이블을 문서화: 가장 포괄적인 접근 방식 있지만 hello 문서 관리가 더 수행할 수도 있습니다.

## <a name="summary"></a>요약
**Azure Data Catalog** 로 데이터 원본을 문서화하는 작업은 필요한 만큼의 세부 정보로 데이터 자산에 대한 설명을 만들 수 있습니다.  링크를 사용 하 여 통합 하는 기존 문서 및 데이터 자산에서 기존 콘텐츠 저장소에 저장 된 toocontent을 연결할 수 있습니다. 사용자가 적절한 데이터 자산을 검색하면 일련의 전체 설명서를 가져올 수 있습니다.
