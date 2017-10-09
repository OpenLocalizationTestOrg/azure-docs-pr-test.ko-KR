---
title: "Azure 검색 서비스 REST API 버전 2016-09-01 aaaUpgrading toohello | Microsoft Docs"
description: "Azure 검색 서비스 REST API 버전 2016-09-01 toohello 업그레이드"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Azure 검색 서비스 REST API 버전 2016-09-01 toohello 업그레이드
2015-02-28 버전 또는 2015-02-28-미리 보기의 hello 사용 하는 경우 [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), 2016-09-01 프로그램 응용 프로그램 toouse hello 다음 일반적으로 사용할 수 있는 API 버전을 업그레이드 하면이 문서가 도움이 됩니다.

Hello REST API의 버전 2016-09-01 이전 버전의 일부 변경 내용이 포함 되어 있습니다. 이는 대부분 이전 버전과 호환되기 때문에 이전에 사용하던 버전에 따라 간단히 코드를 변경할 수 있습니다. 참조 [단계 tooupgrade](#UpgradeSteps) 방법에 대 한 지침은 toochange 코드 toouse hello 새 API 버전입니다.

> [!NOTE]
> Azure 검색 서비스 인스턴스를 최신 hello를 비롯 한 몇 가지 REST API 버전을 지원 합니다. 이것은 더 이상 최신 하나 hello 코드 toouse hello 최신 버전으로 마이그레이션하는 것을 권장 하는 경우 toouse 버전을 계속할 수 없습니다.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>2016-09-01 버전의 새로운 기능
버전 2016-09-01는 hello Azure 검색 서비스 REST API의 두 번째 일반 공급 릴리스 hello입니다. 이 API 버전의 새로운 기능은 다음과 같습니다.

* [사용자 지정 분석기](https://aka.ms/customanalyzers), 인덱싱 및 검색 가능한 토큰 텍스트 변환 hello 프로세스 tootake를 제어할 수 있는 합니다.
* [Azure Blob 저장소](search-howto-indexing-azure-blob-storage.md) 및 [Azure 테이블 저장소](search-howto-indexing-azure-tables.md) 인덱서 tooeasily 수 있게 해 주는 데이터 가져오기에 Azure 저장소에서 Azure 검색 일정 또는 요청 시에 있습니다.
* [필드 매핑](search-indexer-field-mappings.md), toocustomize 수 있는 인덱서를 Azure 검색에 데이터를 가져오려면 어떻게 합니다.
* Etag는 동시성 으로부터 안전한 방식에서 tooupdate hello 정의의 인덱스, 인덱서 및 데이터 소스를 허용 합니다. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>단계 tooupgrade
2015-02-28 버전에서 업그레이드 하는 경우 아마도 않아도 toomake toochange hello 버전 번호 이외의 모든 변경 내용을 tooyour 코드 됩니다. hello만 상황 toochange 코드를 할 수 있는 경우입니다.

* 인식할 수 없는 속성이 API 응답에 반환되는 경우 코드가 실패합니다. 기본적으로 응용 프로그램은 이해하지 못하는 속성을 무시합니다.
* 코드 API 요청을 지속 하 고 tooresend 시도 toohello 새로운 API 버전입니다. 예를 들어 hello 검색 API에서에서 반환 된 연속 토큰을 계속 되 면 응용 프로그램을이 발생할 수 있습니다 (자세한 내용은 찾아보십시오 `@search.nextPageParameters` hello에 [검색 API 참조](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Tooyou을 적용 하는 경우 이러한 할 수 있습니다 toochange 코드 적절 하 게 합니다. 그렇지 않으면 변경 내용이 없습니다 필요가 toostart hello를 사용 하 여 사용 하려는 경우가 아니면 [새로운 기능](#WhatsNew) 2016-09-01 버전입니다.

버전 2015-02-28-미리 보기에서 업그레이드 하는 경우에 위의 hello도 적용 됩니다 하지만 일부 미리 보기 기능은 2016-09-01 버전에서 사용할 수 없는 알고 있어야 합니다.

* Azure Blob Storage 인덱서는 CSV 파일과 JSON 배열을 포함하는 Blob을 지원합니다.
* 동의어
* "이보다 더 나은" 쿼리

이러한 기능을 사용 하는 코드, 수 tooupgrade too2016-09-01의 사용량을 제거 하지 않고 되지 않습니다.

> [!IMPORTANT]
> 미리 보기 API는 테스트 및 평가 용도로 제공되며 프로덕션 환경에는 사용되지 않는다는 점을 유념하세요.
> 
> 

## <a name="conclusion"></a>결론
Hello Azure 검색 서비스 REST API를 사용 하 여 대 한 자세한 내용이 필요한 경우 참조 최근에 업데이트 hello [API 참조](https://msdn.microsoft.com/library/azure/dn798935.aspx) msdn 합니다.

Azure Search에 대한 귀하의 피드백을 환영합니다. 문제가 발생 하면 느껴집니다 무료 tooask us hello에 대 한 도움말 [Azure 검색 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) 또는 [StackOverflow](http://stackoverflow.com/)합니다. Azure에 대 한 질문을 요청 하는 경우 검색 StackOverflow, 있는지 tootag 확인에 사용 하 여 `azure-search`합니다.

Azure 검색을 이용해 주셔서 감사합니다!

