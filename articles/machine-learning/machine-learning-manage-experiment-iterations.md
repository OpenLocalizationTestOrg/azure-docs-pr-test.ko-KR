---
title: "aaaManage 반복 기계 학습 스튜디오에서 실험 | Microsoft Docs"
description: "Toomanage 반복 Azure 기계 학습 스튜디오에서 실험 하는 방법"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오에서 반복 실험 관리
예측 분석 모델을 개발 하는 대화형 프로세스-hello를 수정할 때 결과 수렴 만족할 때까지 다양 한 기능과 실험의 매개 변수 학습 하 고 효과적인 모델을 해야 합니다. 키 toothis 프로세스는 추적 hello 실험 매개 변수 및 구성의 다양 한 반복 합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

이전 실행을 검토할 수 있습니다 순서 toochallenge에서 언제 든 지 실험, 다시 방문와 궁극적으로 확인 또는 이전 가정을 구체화 합니다. 실험을 실행 하면 기계 학습 스튜디오는 데이터 집합, 모듈 및 포트 연결 및 매개 변수를 포함 하 여 hello 실행 기록을 유지 합니다. 이 기록은 시작 및 종료 시간, 로그 메시지 및 실행 상태와 같은 결과, 런타임 정보도 파악합니다. 살펴볼 수에서 모든 시간 tooreview hello 연대순 실험 및 중간 결과에서 이러한 실행 중입니다. 프로그램 경로 toocreating 단순 복잡 하거나 짝수 앙상블 모델링 솔루션에 조회 및 검색의 새 단계로 실험 toolaunch의 이전 실행도 사용할 수 있습니다.

> [!NOTE]
> 실험을 실행 하는 이전를 볼 때 해당 버전의 hello 실험은 잠겨 있으며 편집할 수 없습니다. 그러나는 해당 복사본을 클릭 하 여에 저장할 수 있습니다 **SAVE AS** hello 복사본에 대 한 새 이름을 제공 하 고 있습니다. 기계 학습 스튜디오 다음 편집을 실행할 수 있는 hello 새 복사본을 엽니다. 실험의이 복사본은 hello 영어로 **실험** 다른 모든 실험 함께 목록입니다.
> 
> 

## <a name="viewing-hello-prior-run"></a>이전 실행 보기 hello
Hello hello 실험의 실행을 클릭 하 여 앞에 한 번 이상 실행 하는 실험 열려 있는 경우 볼 수 있습니다 **이전 실행** hello 속성 창에서.

예를 들어, 실험을 만들고 11:23, 11:42 및 11:55에 실험의 버전을 실행한다고 가정합니다. Hello hello 실험 (11:55)의 마지막 실행을 열고 클릭 **이전 실행**, 11시 42분을 실행 하는 hello 버전이 열립니다.

## <a name="viewing-hello-run-history"></a>보기 hello 실행 기록
클릭 하 여 실험의 모든 hello 이전 실행을 볼 수 있습니다 **실행 기록 보기** 열려 실험에서 합니다.

예를 들어 hello로 실험을 만들면 [선형 회귀] [ linear-regression] 모듈을 tooobserve hello 효과의 hello 값을 변경 하려면 **학습 속도** 에 실험 결과입니다. Hello 실험 여러 번 실행 하면이 매개 변수에 대해 서로 다른 값으로 다음과 같습니다.

| 학습 속도 값 | 실행 시작 시간 |
| --- | --- |
| 0.1 |2014년 9월 11일 오후 4:18:58 |
| 0.2 |2014년 9월 11일 오후 4:24:33 |
| 0.4 |2014년 9월 11일 오후 4:28:36 |
| 0.5 |2014년 9월 11일 오후 4:33:31 |

**실행 기록 보기**를 클릭하면 다음과 같은 실행 목록이 모두 표시됩니다.

![예제 실행 기록][runhistory]

이러한 실행 tooview 실행할 hello 시 hello에 대 한 스냅숏을 실험 중 하나를 클릭 합니다. hello 구성, 매개 변수 값, 설명 및 결과 모두 유지 된 toogive 실험의 실행이 해당 전체 레코드 수입니다.

> [!TIP]
> toodocument hello 실험의 반복을 제목을 수정할 수 있습니다 hello 실행 될 때마다, hello를 업데이트할 수 있습니다 **요약** hello의 hello 속성 창에서을 테스트를 추가 하거나 개별 모듈에 대 한 의견을 업데이트할 수 있습니다 toorecord 변경 내용을 합니다. hello 제목, 요약 및 모듈 주석 hello 실험을 실행할 때마다 저장 됩니다.
> 
> 

hello 목록이 hello에서 실험 **실험** 기계 학습 스튜디오에서 탭은 항상 실험의 hello 최신 버전을 표시 합니다. Hello 실험의 이전 실행을 열면 (사용 하 여 **이전 실행** 또는 **실행 기록 보기**)를 클릭 하 여 toohello 초안 버전을 반환할 수 있습니다 **실행 기록 보기** 선택 하 고 반복 된 hello는 **상태** 의 **편집 가능**합니다.

## <a name="iterating-on-a-previous-run"></a>이전 실행 반복
**이전 실행** 또는 **실행 기록 보기**를 클릭하고 이전 실행을 열면 읽기 전용 모드로 완료된 실험을 볼 수 있습니다.

Toobegin hello 방식으로 이전 실행에 대 한 구성으로 시작 하 여 실험의 반복 하려는 경우 이렇게 하려면 열어 hello를 실행 하 고 클릭 하 여 **SAVE AS**합니다. 이렇게 하면 새 제목, 빈 프로그램 실행된 기록을 모든 hello 및 구성 요소 실행 매개 변수 값의 이전 hello 새 실험을 만들어집니다. 이 새 실험 hello에 나열 된 **실험** 탭 hello 기계 학습 스튜디오 홈 페이지에서 수정할 수 있으며 도구를 실행 하 여 실험의이 반복에 대 한 기록을 실행 새 시작 합니다. 

예를 들어 실행 기록이 hello 이전 섹션에 표시 된 hello 실험을 있다고 가정 합니다. Hello를 설정 하면 어떤 일이 생기 tooobserve 원하는 **학습 속도** 매개 변수 too0.4 및 hello에 대 한 다른 값을 시도 **학습 epoch의 수** 매개 변수입니다.

1. 클릭 **실행 기록 보기** 오후 4시 28분: 36 (설정할 수 있는 hello 매개 변수 값 too0.4)에 실행 된 hello 실험의 hello 반복을 엽니다.
2. **다른 이름으로 저장**을 클릭합니다.
3. 새 제목을 입력 하 고 hello 클릭 **확인** 확인 표시 합니다. Hello 실험의 새 복사본이 생성 됩니다.
4. Hello 수정 **학습 epoch의 수** 매개 변수입니다.
5. **실행**을 클릭합니다.

이제 toomodify 계속 하 고 새 실행된 기록이 toorecord 작업 작성이 버전을 사용 하 여 실험을 실행할 수 있습니다.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
