---
title: "aaaSet를 사용 하 여 컴퓨터 학습 권장 사항을 API hello | Microsoft Docs"
description: "Azure 기계 학습을 사용하여 빌드한 Microsoft 권장 사항 API FAQ"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>기계 학습 권장 사항 API 설정 및 사용에 대한 FAQ
**권장 사항이란 무엇입니까?**

> [!NOTE]
> 이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다. hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다. 일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.
> 에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)
> 
> 

조직 및 권장 사항 toocross 판매 상향 판매 제품 및 서비스 tootheir 고객 필요로 하는 비즈니스에 대 한 Azure 기계 학습의 권장 사항을 셀프 서비스 권장 사항을 엔진을 제공 합니다. 이는 행렬 인수분해를 핵심 알고리즘으로 사용한 공동 작업 필터링 구현입니다. 응용 프로그램 개발자는 REST API를 사용하여 RECOMMENDATIONS에 액세스할 수 있습니다. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**권장 사항으로 무엇을 수행할 수 있습니까?**

권장 사항은 항목 또는 항목 집합을 입력으로 이용하고 관련 권장 사항 목록을 반환합니다. 예를 들어 한 온라인 소매점의 고객이 제품을 클릭합니다. hello 온라인 상점 tooRECOMMENDATIONS 입력된으로 해당 제품을 보냅니다, 그리고 제품, 가져오고 toohello 고객을 표시 중 이러한 제품을 결정 합니다. 원하는 toouse 권장 사항을 toooptimize 서 온라인 상점 수도 tooinform 프로그램 내부에도 판매 부서 또는 call center 합니다.

**사용 제한이 있습니까?**

권장 사항에는 다음과 같은 제한을 사용 하는 hello에 있습니다.

* 구독당 최대 모델 수: 10
* 카탈로그에 포함할 수 있는 최대 항목 수: 100,000
* hello 사용 포인트 유지 되는 최대 수에는 ~ 5,000,000는 합니다. 새로 업로드 되거나 보고 되는 경우 가장 오래 된 hello 삭제 됩니다.
* 메일로 전송할 수 있는 최대 데이터 크기(예: 카탈로그 데이터 가져오기, 사용 현황 데이터 가져오기)는 200MB입니다.
* 활성화되지 않은 권장 사항 모델 빌드에 대한 TPS(초당 트랜잭션 수)는 최대 2TPS입니다. 활성화 된 권장 사항을 모델 빌드 too20 TPS를 보유할 수 있습니다.

## <a name="purchase-and-billing"></a>구매 및 요금 청구
**비용은 얼마 입니까 권장 사항을 hello 실행 기간 동안?**

권장 사항은 구독 기반 서비스입니다. 요금 청구는 월별 트랜잭션 볼륨 기준입니다. Hello를 확인할 수 있습니다 [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations) 가격 정보에 대 한 Microsoft Azure Marketplace에서 합니다.

**권장 사항 추적 및 저장 사용자 활동을 포함하는 것과 관련된 비용이 있습니까?**

에 hello 시점입니다.

**권장 사항에 무료 평가판이 있습니까?**

제한 된 too10, 000 월별 트랜잭션 수 있는 무료 내역이 있습니다.

**권장 사항에 대한 요금은 언제 청구됩니까?**

유료 구독은 월별 요금이 있는 구독입니다. 유료 구독을 구매 하는 경우 즉시 요금이 청구 되므로 hello에 대 한 처음 월의 사용 합니다. Hello 제공 서비스로 hello 구독 페이지 (및 해당 세금)에 연결 되어 있는 hello 금액을 청구 됩니다. 이 월별 요금은 hello 구독을 취소할 때까지 원래 구매한 날짜 달력 동일 hello에 각 달 이루어집니다. 

**Tooa 더 높은 계층 서비스를 업그레이드 하려면 어떻게 해야 합니까?**

구입 하거나 hello에서 구독을 업데이트할 수 있습니다 [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations) Microsoft Azure 마켓플레이스에서 페이지입니다.

구독을 업그레이드할 경우:

* 이전 구독에는 남은 트랜잭션은 새 구독 tooyour 추가 되지 않습니다. 
* 있더라도 hello 새 구독에 대 한 전체 가격을 지불 이전 구독에 사용 하지 않은 트랜잭션이 있습니다.

프로세스 tooupgrade 구독:

* Nevigate toohello [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations)합니다.
* 로그인 하지 않은 경우 toohello Marketplace에에서 로그인 합니다.
* Hello 사용 가능한 모든 계획은 hello 오른쪽 창에 나열 됩니다. tooupgrade hello 계획에 대 한 hello 라디오 단추를 클릭 합니다.
* Tooupgrade 클릭 **확인**합니다. Tooupgrade 하지 않으려면 클릭 **취소**합니다.

**중요 한** 대금 청구 및 사용에 영향을 줄 있기 때문에 업그레이드 하기 전에 신중 하 게 읽기 hello 대화 상자.

**내 구독 tooRecommendations 끝납니다 하는 경우**

구독은 고객이 구독을 취소할 때 종료됩니다. Toocancel 원하는 경우 구독 hello 다음 지침을 참조 하세요.

**권장 사항 구독을 취소하려면 어떻게 해야 합니까?**

구독을 사용 하 여 hello 다음 단계를 toocancel 합니다. 유료 구독이 현재 구독을 사용 하는 경우 구독 청구 기간 현재 hello hello 끝날 때까지 적용 계속 합니다. 효과적인 취소 toobe를 즉시 hello 필요에 게 문의 하세요. [Microsoft 지원](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)합니다.

**참고** 요금은 환불 되지 않습니다 청구 기간에 청구 기간 또는 사용 하지 않는 트랜잭션에 대 한 hello 종료 전에 취소 합니다.

* Toohello 이동 [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations)합니다.
* 로그인 하지 않은 경우 toohello Marketplace에에서 로그인 합니다.
* 클릭 **취소** toohello hello 데이터 집합 이름 및 상태 오른쪽에 있습니다. 현재 청구 기간 되거나 트랜잭션 제한 hello hello 끝 (중 먼저 발생)에 도달할 때까지이 구독을 사용할 수 있습니다.

파일에서 티켓을 새 구독을 구입할 수 있으므로 즉시 구독 toocancel 원하는 경우 [Microsoft 지원](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)합니다.

## <a name="getting-started-with-recommendations"></a>권장 사항 시작하기
**권장 사항이 고객에게 적합합니까?** 

기계 학습의 권장 사항을 조직 및 권장 사항 toocross 판매 및 상향 판매 제품 또는 서비스 tootheir 고객에 의존 하는 회사입니다. 고객을 응대하는 웹 사이트, 영업 인력, 내부 판매 인력 또는 콜 센터가 있고 수십 개의 제품이나 서비스가 포함된 카탈로그를 제공하는 경우 권장 사항을 활용하여 수익을 높일 수 있습니다. 

권장 사항을 작업할 수 있도록 설계 된 toobe 매우 단순한입니다. hello 현재 API 기반 버전의 기본 프로그래밍 기술을 사용 해야 합니다. 도움이 필요 하면 웹 사이트를 개발 하는 hello 공급 업체에 문의 합니다. 내부 IT 부서 또는 사내 개발자가 있으면 사용자에 대 한 권장 사항 toowork 수 tooget 수 있어야 합니다. 

**권장 사항을를 설정 하기 위한 필수 구성 요소 hello 이란?**

권장 사항 tooyour 카탈로그와 관련 사용자 선택 항목의 로그에 있어야 합니다. 해당 로그가 없고 고객 응대 웹 사이트를 운영하는 경우 권장 사항에서 대신 사용자 활동을 수집할 수 있습니다. 

권장 사항에는 제품 또는 서비스에 대한 카탈로그도 필요합니다. Hello 카탈로그를 설정 하지 않은 경우 권장 사항을 hello 실제 고객 사용 현황 데이터를 사용할 수 있으며 추출 카탈로그. "묵시적" 카탈로그에는 사용자 트랜잭션의 일부로 "보고"되지 않은 항목이 포함되지 않습니다.

**어떻게 설정 하나요 권장 사항을 hello에 대 한 처음으로?**

후 [구독](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, hello에 hello API 설명서를 사용 해야 [Azure 시스템 학습 권장 사항-빠른 시작 가이드](machine-learning-recommendation-api-quick-start-guide.md) tooset hello 서비스를 구성 합니다.

**API 설명서는 어디서 찾을 수 있습니까?** 

hello API 설명서는 [Azure 시스템 학습 권장 사항-빠른 시작 가이드](machine-learning-recommendation-api-quick-start-guide.md)합니다.

**옵션의 대신할 tooupload 카탈로그 및 사용 현황 데이터 tooRecommendations 있습니까?**

카탈로그 및 사용 현황 데이터를 업로드 하기 위한 두 가지 옵션이 있습니다: 하 여 CRM 시스템 이나 다른 로그에서 hello 데이터를 내보낼 tooRecommendations를 업로드 하거나 사용자 활동을 추적 하는 태그 tooyour 웹 사이트를 추가할 수 있습니다. Hello 두 번째 방법을 사용 하는 경우 Azure의 hello 데이터 저장 됩니다.

## <a name="maintenance-and-support"></a>유지 관리 및 지원
**내 데이터 집합은 얼마나 확장할 수 있습니까?**

각 데이터 집합 사용 현황 데이터의 too2048 MB를 too100, 000 카탈로그 항목을 포함할 수 있습니다.
또한 구독 too10 데이터 집합 (모델)을 포함할 수 있습니다.

**권장 사항에 대한 기술 지원은 어디서 받을 수 있습니까?**

기술 지원은 hello에서 사용할 수 있는 [Microsoft Azure 지원](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) 사이트입니다.

**사용 약관 hello 어디에 있습니까?**

[Microsoft Azure 기계 학습 권장 사항 API 서비스 약관](https://datamarket.azure.com/dataset/amla/recommendations#terms)에서 찾을 수 있습니다.

