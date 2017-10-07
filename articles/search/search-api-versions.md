---
title: "Azure 검색의 aaaAPI 버전 | Microsoft Docs"
description: "Azure 검색 REST Api 및 hello 클라이언트 라이브러리를.NET SDK hello에 대 한 정책 버전입니다."
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Azure 검색의 API 버전
Azure Search는 정기적으로 기능 업데이트를 공개합니다. 항상 그렇지는 않지만 따라서는 이러한 업데이트 해야 우리 toopublish 우리의 API toopreserve 이전 버전과 호환성의 새 버전. 새 버전을 게시 하면 toocontrol와 코드에서 검색 서비스 업데이트를 통합 하는 방법.

일반적으로 시도 toopublish 새 버전이 필요한 경우에 일부 노력 tooupgrade 포함할 수 있으므로 코드 toouse 새로운 API 버전입니다. 이전 버전과 호환성을 중단 하는 방식으로 hello API의 일부 측면 toochange 해야 하는 경우 새 버전만 발표 합니다. 이 수정 tooexisting 기능 때문에 또는 기존 API 노출 영역을 변경 하는 새로운 기능으로 인해 발생할 수 있습니다.

Hello 동일한 SDK 업데이트에 대 한 규칙을 따릅니다. Azure 검색 SDK hello 뒤 hello [의미 체계 버전 관리](http://semver.org/) 는 해당 버전에서 세 부분으로 구성 함을 의미 하는 규칙을: 주, 부, 및 빌드 번호 (예를 들어 1.1.0). 우리는 이전 버전과 호환성을 중단 하는 변경 된 경우만 hello SDK의 새로운 주 버전이 해제 합니다. 사소한 기능 업데이트에 대 한 hello 부 버전을 증분할 및 버그 수정에 대 한 것만 증가 hello 빌드 버전.

> [!NOTE]
> Azure 검색 서비스 인스턴스를 최신 hello를 비롯 한 몇 가지 REST API 버전을 지원 합니다. 이것은 더 이상 최신 하나 hello 코드 toouse hello 최신 버전으로 마이그레이션하는 것을 권장 하는 경우 toouse 버전을 계속할 수 없습니다. Hello REST API를 사용할 경우 hello api 버전 매개 변수를 통해 모든 요청에서 hello API 버전을 지정 해야 합니다. Hello.NET SDK를 사용할 때는 hello 버전의 SDK 사용 하는 hello hello hello REST API의 해당 버전을 결정 합니다. 이전 SDK를 사용 하는 경우 계속할 수 있습니다 toorun 변경 하지 않고 해당 코드 경우에 hello 서비스 업그레이드 toosupport 최신 API 버전.

## <a name="snapshot-of-current-versions"></a>현재 버전의 스냅숏
다음 hello에 대 한 스냅숏을 모든 프로그래밍 인터페이스 tooAzure 검색의 현재 버전은입니다.

| 인터페이스 | 가장 최근의 주 버전 | 가동 상태 |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |3.0 |일반 공급, 2016년 11월 릴리스됨 |
| [.NET SDK 미리 보기](https://aka.ms/search-sdk-preview) |2.0-preview |미리 보기, 2016년 8월 릴리스 |
| [서비스 REST API](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |일반 공급 |
| [서비스 REST API 미리 보기](search-api-2015-02-28-preview.md) |2015-02-28-Preview |미리 보기 |
| [.NET 관리 SDK](https://aka.ms/search-mgmt-sdk) |2015-08-19 |일반 공급 |
| [관리 REST API](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |일반 공급 |

Hello hello를 포함 하 여 REST Api에 대 한 `api-version` 각 호출에서이 필요 합니다. 이 통해 쉽게 tootarget 미리 보기 API와 같은 특정 버전. hello 다음 예제에서는 어떻게 hello `api-version` 매개 변수를 지정 합니다.

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> 각 요청에 있지만 `api-version`, hello를 사용 하는 것이 좋습니다 모든 API 요청에 대 한 동일한 버전입니다. 새 API 버전이 이전 버전에서 인식 하지 못하는 특성 또는 작업을 도입하는 경우 특히 유용합니다. 혼합 API 버전에는 의도하지 않은 결과가 있을 수 있기 때문에 사용하지 말아야 합니다.
>
> hello 서비스 REST API 및 관리 REST API 버전 서로 독립적으로 관리 됩니다. 버전 번호 체계는 동일합니다.

일반적으로 사용 가능한 (또는 GA) Api 프로덕션 환경에서 사용할 수 있습니다 및 서비스 수준 계약 주체 tooAzure 됩니다. 미리 보기 버전에 없는 경우가 있는 마이그레이션된 tooa GA 버전 실험적인 기능이 있습니다. **프로덕션 응용 프로그램에서 미리 보기 API를 사용하지 않는 것이 좋습니다.**

## <a name="about-preview-and-generally-available-versions"></a>미리 보기 및 일반 공급 버전 정보
Azure 검색 항상 미리 해제 hello REST API를 통해 실험적 기능을 먼저 다음 시험판 버전의.NET SDK hello 통해 합니다.

미리 보기 기능 toobe 보장 되지 tooa GA 릴리스 마이그레이션됩니다. 테스트와 실험에 피드백을 수집 하의 hello 목표와에 사용할 수 있는 미리 보기 기능 GA 버전의 기능에는 작은 이전 버전과 호환 수정과 향상 된 기능 hello 제외 하 고 안정적인 toochange 간주 되므로, 반면 기능 디자인과 구현 합니다.

그러나 미리 보기 기능 주체 toochange 이기 때문에 미리 보기 버전을 사용 하는 프로덕션 코드 작성 좋습니다. 이전 미리 보기 버전을 사용 하는 경우 마이그레이션하는 것이 좋습니다 toohello 일반적으로 사용 가능한 (GA) 버전입니다.

Hello.NET SDK에 대 한:에서 코드 마이그레이션에 대 한 지침을 찾을 수 있습니다 [업그레이드 hello.NET SDK](search-dotnet-sdk-migration.md)합니다.

일반 공급 이제 Azure 검색 hello 서비스 수준 계약 (SLA)에서 적용 임을 의미 합니다. hello SLA에서 찾을 수 있습니다 [Azure 검색 서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/search/v1_0/)합니다.
