---
title: "데이터 카탈로그 aaaIntroduction tooAzure | Microsoft Docs"
description: "이 문서에서는 언어의 기능 및 hello 문제 해결을 포함 하 여 Microsoft Azure Data Catalog에 대 한 개요를 제공 합니다. 데이터 카탈로그를 사용할 수 있는 사용자 tooregister 있게, 검색, 이해 하 고, 데이터 소스를 사용 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: cc733907-17ec-4153-9f0c-5b3754b2db19
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 82144c440b5692d3608af08208f36ee8e6dfdc93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-data-catalog"></a>Azure 데이터 카탈로그란?
Azure Data Catalog는 완전히 관리 되는 클라우드 서비스 사용자가 속한 필요 하며을 찾게 hello 데이터 원본을 이해 hello 데이터 소스를 검색할 수 있습니다. Hello에서 동일한 시간, 데이터 카탈로그 사용 하면 조직 get 기존 투자에서 값 추가 합니다. 

데이터 카탈로그를 통해 모든 사용자(분석가, 데이터 과학자 또는 개발자)는 데이터 원본을 검색, 파악 및 사용할 수 있습니다. 데이터 카탈로그에는 메타데이터 및 주석의 크라우드소싱 모델이 포함됩니다. 한 대의 중앙 위치에는 조직의 사용자가 toocontribute의 모든 지식을 사용 되며 커뮤니티 및 데이터의 culture를 생성 합니다.

## <a name="discovery-challenges-for-data-consumers"></a>데이터 소비자에 대한 검색 과제
일반적으로 엔터프라이즈 데이터 원본을 검색하는 일은 기초 지식에 기반한 유기적인 프로세스였습니다. 이 방법은 회사의 정보 자산 중에서 가장 많은 가치 tooget hello 원하는 대 한 다양 한 문제를 제공 합니다.

* 사용자는 다른 프로세스의 일부로 데이터 원본에 연결되지 않는 한 데이터 원본이 존재한다는 사실을 모를 수도 있습니다. 데이터 원본이 등록되는 중앙 위치가 없습니다.
* 사용자가 데이터 원본의 hello 위치를 알고, toohello 데이터 클라이언트 응용 프로그램을 사용 하 여 연결할 수 없습니다. 데이터 사용 환경을 사용자 tooknow hello 연결 문자열 또는 경로가 필요합니다.
* 사용자가 데이터 원본 설명서의 hello 위치를 알 수, 하지 않는 한 사실을 알고 hello 데이터의 의도 한 hello를 사용 합니다. 데이터 원본과 설명서는 다양한 위치에 있으며 다양한 환경을 통해 사용될 수 있습니다.
* 사용자가 정보 자산에 대 한 질문을 하는 경우 해야 hello 전문가 또는 팀은 hello 데이터에 대 한를 찾을 오프 라인으로 끌어야 합니다. 이 때 용도에 대한 전문가의 관점을 가진 데이터와 데이터 간의 명시적 연결은 없습니다.
* 사용자가 액세스 toohello 데이터 소스를 요청 하기 위한 hello 프로세스를 이해 하지 않는 한 hello 데이터 원본 및 해당 설명서를 검색 합니다. 도움이 되지 않거나 hello 데이터에 액세스 하 합니다.

## <a name="discovery-challenges-for-data-producers"></a>데이터 생산자에 대한 검색 과제
데이터 소비자 얼굴 hello 과제에서 설명한 하지만 사용자가 생성 하 고 정보 자산을 유지 관리 하는 일을 담당 하는 문제에 직면 자체의:

* 데이터 원본에 설명이 포함된 메타데이터로 주석을 추가하는 것은 종종 시간 낭비입니다. 클라이언트 응용 프로그램에는 일반적으로 hello 데이터 원본에 저장 되는 설명 무시 합니다.
* 데이터 원본에 대한 설명서를 만드는 것은 종종 시간 낭비입니다. 설명서를 데이터 원본과 동기화시키는 것은 지속적인 책임이며, 설명서는 대개 오래된 것으로 간주되기 때문에 사용자가 이를 신뢰하지 않습니다.
* 데이터 원본에 대한 설명서 생성 및 유지 관리는 복잡하고 시간 소모적입니다. Hello 데이터 소스를 사용 하는 tooeveryone 해당 설명서를 즉시 사용할 수 있습니다 더욱 그렇습니다.
* Toodata 소스 액세스를 제한 하 고 데이터 소비자 toorequest 액세스가 지속적인 챌린지 방법을 알고 있는지 확인 합니다.

이러한 문제를 결합 tooencourage 및 승격 hello 사용 및 엔터프라이즈 데이터를 이해 하는 회사에 대 한 중요 한 장벽을 제공 합니다.

## <a name="azure-data-catalog-can-help"></a>Azure Data Catalog는 다음 과제에 도움이 될 수 있습니다.
데이터 카탈로그는 이러한 문제와 toohelp 기업 get hello 기존의 정보 자산 중에서 가장 값 디자인 된 tooaddress입니다. 데이터 카탈로그 사용 하면 데이터 원본 쉽게 검색 가능 하 고 이해할 수 있도록 hello 데이터를 관리 하는 hello 사용자가 있습니다.

데이터 카탈로그는 데이터 원본을 등록할 수 있는 클라우드 기반 서비스를 제공합니다. 해당 메타 데이터의 복사본이 있지만 기존 위치에 hello 데이터는 유지 참조 toohello 데이터 소스 위치와 함께 tooData 카탈로그에 추가 됩니다. 메타 데이터를 hello 인덱싱된 toomake 각 데이터 소스 이기도 검색 하 고 이해 하기 쉽게 toohello 사용자 검색을 통해 쉽게 검색할 수 있습니다.

데이터 원본을 등록 하 고 나면 해당 메타 데이터 수 다음 성능을 강화를 등록 하 고 있는 사용자는 hello 또는 hello 엔터프라이즈의 다른 사용자가 있습니다. 모든 사용자는 설명, 태그 또는 설명서와 데이터 원본 액세스 요청과 같은 기타 메타데이터를 제공하여 데이터 원본에 주석을 달 수 있습니다. 이 설명이 포함 된 메타 데이터 hello 구조적 메타 데이터 (예: 열 이름 및 데이터 형식) hello 데이터 원본의 등록을 보완 합니다.

검색 데이터 원본 및 용도 이해 하 고 hello 주로 hello 소스를 등록 하는 중입니다. 기업 사용자는 비즈니스 인텔리전스, 응용 프로그램 개발, 데이터 과학 또는 hello 적절 한 데이터를 필요한 경우 다른 작업에 대 한 데이터가 필요할 수 있습니다. 경험 tooquickly 데이터 찾기, 요구에 맞게 일치 하는 hello 데이터 tooevaluate의 목적에의 적합성 hello 이해 하 고 선택한 해당 도구에서 hello 데이터 소스를 열어 hello 데이터를 소비 hello 데이터 카탈로그 검색을 사용할 수 있습니다. 

At hello 동일 시간, 사용자가 태그 지정, 문서화 및 이미 등록 되어 있는 데이터 원본에 주석 지정으로 toohello 카탈로그를 느려지게 할 수 있습니다. 다음 검색, 이해 하 고 수 있는 카탈로그 사용자의 hello 커뮤니티에서 사용할 새 데이터 소스를 등록할 수도 있습니다.

![데이터 카탈로그 기능](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a>데이터 카탈로그에 대한 자세한 정보
데이터 카탈로그의 hello 기능에 대해 자세히 toolearn 참조:

* [어떻게 tooregister 데이터 원본](data-catalog-how-to-register.md)
* [어떻게 toodiscover 데이터 원본](data-catalog-how-to-discover.md)
* [어떻게 tooannotate 데이터 원본](data-catalog-how-to-annotate.md)
* [어떻게 toodocument 데이터 원본](data-catalog-how-to-documentation.md)
* [어떻게 tooconnect toodata 원본](data-catalog-how-to-connect.md)
* [어떻게 빅 데이터 관련 toowork](data-catalog-how-to-big-data.md)
* [어떻게 toomanage 데이터 자산](data-catalog-how-to-manage.md)
* [tooset 비즈니스 용어집를 활용 hello 하는 방법](data-catalog-how-to-business-glossary.md)
* [질문과 대답](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a>다음 단계
데이터 카탈로그 시작 tooget 이동:
* [Microsoft Azure Data Catalog](https://www.azuredatacatalog.com)
* [Azure 데이터 카탈로그 시작](data-catalog-get-started.md)
