---
title: "'빅 데이터' 데이터 원본과 aaaHow toowork | Microsoft Docs"
description: "Azure Data Catalog를 사용 하 여 Azure Blob 저장소, Azure 데이터 레이크 Hadoop HDFS 등 '빅 데이터' 데이터 원본에 대 한 패턴을 강조 표시 하는 방법 tooarticle 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>빅 데이터 관련 toowork 원본 Azure Data Catalog에 어떻게
## <a name="introduction"></a>소개
**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 핵심은 검색 이해 하 고 데이터 원본을 사용할 수 있도록 하 고 빅 데이터를 포함 하 여 자신의 기존 데이터 원본에서 조직의 tooget 더 많은 가치를 지원 합니다.

**Azure Data Catalog** 지원 hello Azure 블로그 저장소의 blob 및 디렉터리와 Hadoop HDFS 파일 및 디렉터리를 등록 합니다. hello 반 구조화 된 특성의 이러한 데이터 원본 뛰어난 유연성을 제공합니다. 그러나 tooget hello를 사용 하 여 등록에서 가장 많은 가치 **Azure Data Catalog**, 사용자가 hello 데이터 소스 구성 방법을 고려해 야 합니다.

## <a name="directories-as-logical-data-sets"></a>논리적 데이터 집합으로 디렉터리 처리
빅 데이터 원본 구성을 위한 일반적인 방법은 논리 데이터 집합으로 tootreat 디렉터리 것입니다. 최상위 디렉터리 하위 폴더에 파티션 정의 및 포함 된 hello 파일 자체 hello 데이터를 저장 하는 동안 사용 되는 toodefine 데이터 집합에는.

이 패턴의 예는 다음과 같습니다.

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

이 예에서는 vehicle_maintenance_events 및 location_tracking_events가 논리 데이터 집합을 나타냅니다. 이러한 폴더 각각에는 년 및 월 단위로 하위 폴더에 정리된 데이터 파일이 있습니다. 이러한 폴더 각각에는 수백 또는 수천 개의 파일이 있을 수 있습니다.

이 패턴에서 개별 파일을 **Azure 데이터 카탈로그**에 등록해도 이를 사용할 수 없습니다. 의미 있는 toohello users hello 데이터로 작업 하는 hello 데이터 집합을 나타내는 hello 디렉터리를 등록 합니다.

## <a name="reference-data-files"></a>참조 데이터 파일
상호 보완적인 패턴에는 개별 파일로 toostore 참조 데이터 집합은입니다. 이러한 데이터 집합 빅 데이터의 hello '작은' 쪽으로 생각할 수 및 분석 데이터 모델에서 비슷한 toodimensions 경우가 많습니다. 참조 데이터 파일에는 레코드 hello 빅 데이터 저장소의 다른 위치에 저장 하는 hello 데이터 파일의 hello 대부분을 사용 하는 tooprovide 컨텍스트를 포함 합니다.

이 패턴의 예는 다음과 같습니다.

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

참조 파일에 데이터는 hello 사용된 tooprovide 된 엔터티를 더 큰 데이터 hello에에서 이름 또는 ID로 tooonly 참조에 대 한 자세한 정보 수 분석가 나 데이터 과학자는 hello 큰 디렉터리 구조에 포함 된 hello 데이터를 사용할 때 설정 합니다.

이 패턴에서는 의미가 있는 tooregister hello 개별 참조 데이터 파일 **Azure Data Catalog**합니다. 각 파일은 데이터 집합을 나타내며, 각각에 대해 개별적으로 주석을 추가하고 검색할 수 있습니다.

## <a name="alternate-patterns"></a>대체 패턴
hello hello 앞 섹션에서에서 설명 하는 패턴 방금 두 가지 가능한 큰 데이터 저장소를 구성할 수 있습니다 있지만 각 구현은 다릅니다. 데이터 소스 구성 방법, 빅 데이터 원본으로 등록 하는 경우에 관계 없이 **Azure Data Catalog**, hello 파일 및 디렉터리 내에서 값 tooothers의 않는 hello 데이터 집합을 나타내는 등록에 집중 프로그램 조직입니다. 모든 파일 및 디렉터리 등록 hello 카탈로그, 관리가 어려울 toofind 사용자에 대 한가 필요한 복잡 수 있습니다.

## <a name="summary"></a>요약
포함 된 데이터 원본 등록 **Azure Data Catalog** 쉽게 toodiscover 되도록 하 고 이해 합니다. 등록 하 고 hello 빅 데이터 파일 및 디렉터리를 나타내는 논리 데이터 집합에 주석 지정를 찾아서 필요한 hello 빅 데이터 원본을 사용 하는 사용자가 도울 수 있습니다.
