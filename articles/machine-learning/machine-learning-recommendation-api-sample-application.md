---
title: "hello 컴퓨터 학습 권장 사항을 API에서에서 aaaCommon 작업 | Microsoft Docs"
description: "Azure ML 권장 사항 샘플 응용 프로그램"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
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
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>권장 사항 API 응용 프로그램 예제 연습
> [!NOTE]
> 이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다. hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다. 일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.
> 에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>목적
이 문서에서는 Azure 시스템 학습 권장 사항 API를 통해 hello의 hello 사용 표시는 [샘플 응용 프로그램](https://code.msdn.microsoft.com/Recommendations-144df403)합니다.

이 응용 프로그램은 의도 한 tooinclude 전체 기능을 하지도 모든 hello Api 사용. 기계 학습 권장 서비스가 hello로 tooplay 먼저 하려는 경우 몇 가지 일반적인 작업 tooperform를 보여 줍니다. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>소개 tooMachine 학습 권장 구성 서비스
Hello 기계 학습 권장 서비스를 통해 권장 사항 hello 다음 데이터를 기반으로 추천 모델을 빌드할 때 활성화 됩니다.

* 카탈로그 라고도 toorecommend hello 항목의 저장소
* 사용자 또는 세션 (이 얻을 수 hello 샘플 응용 프로그램의 일부가 아니라 데이터 취득 통해 시간이 지남에 따라) 당 항목 hello 사용을 나타내는 데이터

추천 모델을 작성 한 후 사용할 수 있습니다는 사용자에 관심을 가질 수 있는 toopredict 항목 따라 tooa 일련의 항목 (또는 단일 항목) hello 사용자가 선택 되어 있습니다.

tooenable hello 이전 시나리오에서 hello 다음 기계 학습 권장 서비스가 hello:

* 모델을 만듭니다:이 hello 데이터 (카탈로그 및 사용) 및 hello 예측 모델을 보관 하는 논리적 컨테이너입니다. 각 모델 컨테이너는 생성 시 할당되는 고유 ID를 통해 식별됩니다. 이 ID는 hello 모델 ID 라고 하 고 대부분의 hello Api에서 사용 됩니다. 
* Toocatalog 업로드: 모델 컨테이너를 만들면 tooit 카탈로그를 연결할 수 있습니다.

**참고**: 모델 만들기 및 업로드 tooa 카탈로그는 일반적으로 한 번 수행 hello 모델 수명 주기에 대 한 합니다.

* 사용 현황 업로드: 이렇게 하면 사용 현황 데이터 toohello 모델 컨테이너를 추가 합니다.
* 추천 모델을 빌드: 충분 한 데이터를 설정한 후에 hello 추천 모델을 구축할 수 있습니다. 이 작업 hello 상위 기계 학습 알고리즘 toocreate 추천 모델을 사용합니다. 각 빌드는 고유 ID와 연결됩니다. 일부 Api의 hello 기능에 필요한 있기 때문에이 ID에 대 한 기록을 tookeep을 해야 합니다.
* 빌드 프로세스 모니터 hello: 추천 모델 빌드는 비동기 작업을 하 고 hello 양의 데이터 (카탈로그 및 사용)에 따라 몇 분 tooseveral 시간에서 수행 하 고 hello 빌드 매개 변수 수입니다. 따라서 toomonitor hello 빌드를 해야합니다. 연결된 해당 빌드가 성공적으로 완료되는 경우에만 권장 사항 모델이 빌드됩니다.
* (선택 사항) 활성 권장 사항 모델 빌드 선택: 이 단계는 모델 컨테이너에서 권장 사항 모델이 두 개 이상 빌드된 경우에만 필요합니다. Hello 활성 추천 모델을 표시 하지 않고 요청 tooget 권장 사항을 hello 시스템 toohello 기본 현재 빌드에 의해 자동으로 리디렉션됩니다. 

**참고**: 활성 권장 사항 모델은 프로덕션 환경에서 바로 사용할 수 있으며 프로덕션 작업을 위해 빌드됩니다. 테스트와 비슷한 환경(스테이징 환경이라고도 함)에 머무르는 비활성 권장 사항 모델과는 다릅니다.

* 권장 사항 가져오기: 권장 사항 모델이 있으면 선택한 단일 항목 또는 항목 목록에 대한 권장 사항을 트리거할 수 있습니다. 

일반적으로 특정 기간에 대해 Get Recommendation을 호출합니다. 해당 시간 기간 동안 사용 현황 데이터 toohello이 데이터 toohello 지정된 모델 컨테이너를 추가 하는 기계 학습 추천 시스템을 리디렉션할 수 있습니다. 충분 한 사용 현황 데이터를 있으면 hello 추가 사용 현황 데이터를 통합 하는 새 추천 모델을 작성할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건
* Visual Studio 2013 이상
* 인터넷 액세스 
* 구독 toohello 권장 사항을 API (https://datamarket.azure.com/dataset/amla/recommendations)입니다.

## <a name="azure-machine-learning-sample-app-solution"></a>Azure 기계 학습 샘플 앱 솔루션
이 솔루션 hello 소스 코드, 사용법 예제, 카탈로그 파일 및 컴파일에 필요한 지시문 toodownload hello 패키지를 포함 합니다.

## <a name="hello-apis-used"></a>hello 사용 되는 Api
hello 응용 프로그램에서는 사용 가능한 Api의 하위 집합을 통해 기계 학습 권장 기능을 사용 합니다. 다음 Api hello 응용 프로그램에서 보여지는 hello:

* 모델을 만들: 논리적 컨테이너 toohold 데이터와 권장 사항 모델을 만듭니다. 모델은 한 이름으로 식별 되 고 hello로 하나 이상의 모델을 만들 수 없습니다 동일한 이름입니다.
* 카탈로그 파일을 업로드: tooupload 카탈로그 데이터를 사용 합니다.
* 사용 현황 파일 업로드: tooupload 사용 현황 데이터를 사용 합니다.
* 빌드를 트리거: toocreate 추천 모델을 사용 합니다.
* 빌드 실행을 모니터링할: toomonitor hello에서는 추천 모델 빌드 상태를 사용 합니다.
* 권장 사항이 작성 된 모델 선택: tooindicate는 추천 모델 toouse를 기본적으로 사용 특정 모델 컨테이너입니다. 이 단계는 추천 모델을 여러 개 있고 tooactivate 활성이 아닌 hello 활성 추천 모델을 빌드 하려는 경우에 필요 합니다.
* 권장 메시지가: tooretrieve 추천 tooa 지정 된 단일 항목 또는 항목 집합에 따라 항목을 사용 합니다. 

에 대 한 전체 설명은 hello Api, hello Microsoft Azure Marketplace 설명서를 참조 하십시오. 

**참고**: 시간이 지나면(동시는 아님) 모델 빌드가 여러 개 있을 수 있습니다. 각 빌드를 동일한 또는 업데이트 된 hello로 만든 카탈로그 및 추가 사용 현황 데이터.

## <a name="common-pitfalls"></a>공통 문제
* 사용자 이름 및 Microsoft Azure Marketplace 기본 계정 키 toorun hello 샘플 앱 tooprovide 해야합니다.
* 연속적으로 실행 중인 hello에 대 한 샘플 응용 프로그램 실패 합니다. hello 응용 프로그램 흐름 만들고 업로드 hello 모니터를 구축 하 고, 미리 정의 된 모델에서 권장 구성을 가져오는 포함 됩니다. 따라서 호출 사이의 hello 모델 이름을 변경 하지 않는 경우 연속 실행에 실패 합니다.
* 데이터 없이 권장 사항이 반환될 수 있습니다. hello 샘플 응용 프로그램에는 매우 작은 카탈로그 및 사용 현황 파일을 사용 합니다. 따라서 hello 카탈로그에서 일부 항목 권장된 항목이 포함 됩니다.

## <a name="disclaimer"></a>고지 사항
hello 샘플 응용 프로그램을 프로덕션 환경에서 실행 되는 의도 된 toobe 아닙니다. 매우 작은 hello 카탈로그에서 제공 하는 hello 데이터 이며 의미 있는 추천 모델을 제공 하지 않습니다. hello 데이터 데모로 제공 됩니다. 

