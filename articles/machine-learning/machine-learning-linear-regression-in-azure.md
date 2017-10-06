---
title: "기계 학습에서 선형 회귀 aaaUsing | Microsoft Docs"
description: "Excel과 Azure 기계 학습 스튜디오의 선형 회귀 모델 비교"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Azure 기계 학습에서 선형 회귀 사용
> *Kate Baroni*와 *Ben Boatman*은 Microsoft Data Insights Center of Excellence의 엔터프라이즈 솔루션 설계자입니다. 이 문서에서는 기존 회귀 분석 suite tooa 클라우드 기반 솔루션 Azure 기계 학습을 사용 하 여 마이그레이션 자신의 환경을 설명 합니다. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>목표
다음 두 가지 목표를 염두에 두고 프로젝트를 시작했습니다. 

1. 조직의 월별 수익 예측의 예측 분석 tooimprove hello 정확도 사용 하 여 
2. Azure 기계 학습 tooconfirm를 사용 하 여, 최적화, 속도 높이 결과의 소수 자릿수입니다. 

많은 기업과 마찬가지로 우리 조직에서도 월별 수익 예측 프로세스를 수행합니다. 작은 비즈니스 분석가 팀 해야 Azure 기계 학습 toosupport hello 프로세스를 사용 하 고 예측된의 정확도 향상 합니다. hello 팀 소비한 몇 달 동안 여러 원본에서 데이터를 수집 하 고 관련 tooservices 판매 예측과 키 특성을 식별 하는 통계 분석을 통해 hello 데이터 특성을 실행 합니다. hello 다음 단계는 Excel의 hello 데이터에서 toobegin 프로토타입 통계 회귀 모델을 이었습니다. 몇 주 이내 hello 현재 필드 및 재무 예측 프로세스 보다 성능이 된 하는 Excel 회귀 모델을 했습니다. 이러한 방식을 hello 초기 예측 결과입니다. 

에서는 다음 인수할 hello 다음 단계 toomoving 예상 우리의 분석 tooAzure 기계 학습 toofind 기계 학습에서 예측 성능을 향상 시키는 방법을 아웃 합니다.

## <a name="achieving-predictive-performance-parity"></a>예측 성능 패리티 달성
이 첫 번째 우선 순위는 기계 학습 및 Excel 회귀 모델 간의 tooachieve 패리티 했습니다. 지정 된 동일한 데이터를 hello 및 학습 및 테스트 데이터에 대 한 분할 동일 hello, Excel 및 기계 학습 간의 tooachieve 예측 성능을 패리티 해야 할까요 합니다. 처음에는 실패했습니다. hello Excel 모델을 hello 기계 학습 모델을 실적이 우수 했습니다. 기계 학습에서 설정 하는 hello 기본 도구에 대 한 이해 tooa 부족 인해 hello 실패가 했습니다. Hello 기계 학습 제품 팀과 함께 동기화 이후 우리 hello 기본 설정 하는 데이터 집합에 필요한 더 잘 이해를 hello 두 모델 간의 수준에 도달 합니다. 

### <a name="create-regression-model-in-excel"></a>Excel에서 회귀 모델 만들기
이 Excel 회귀 hello 표준 선형 회귀 모델 hello Excel 분석 도구에 사용 됩니다. 

계산 *평균 절대 %Error* hello 모델에 대 한 hello 성능 측정으로 사용 합니다. Excel을 사용 하 여 작업 모델에 3 개월 tooarrive를 걸렸습니다. 에서는 상태가 hello 하 던 궁극적으로 요구 사항 이해 하는 데에서 유용 기계 학습 스튜디오 실험에 hello 학습의 많은 합니다.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Azure 기계 학습에서 비교 가능한 실험 만들기
이러한 단계 toocreate 기계 학습 스튜디오에서 실험 우리의 다음합니다. 

1. Csv 파일 tooMachine 학습 스튜디오 (매우 작은 파일)로 업로드 된 hello 데이터 집합
2. 새 실험 만들고 hello [데이터 집합의 열 선택] [ select-columns] 모듈 tooselect hello Excel에서 사용 되는 동일한 데이터 기능 
3. 사용 하는 hello [분할 데이터] [ split] 모듈 (으로 *상대 식을* 모드) toodivide hello 데이터를 Excel에서 되었던으로 동일한 학습 데이터 집합을 hello 
4. Hello로 실험 [선형 회귀] [ linear-regression] 모듈 (기본 옵션만)을 문서화 하 고 hello 결과 tooour Excel 회귀 모델 비교

### <a name="review-initial-results"></a>초기 결과 검토
처음에 hello Excel 모델을 hello 기계 학습 스튜디오 모델을 명확 하 게 실적이 우수 했습니다. 

|  | Excel | 스튜디오 |
| --- |:---:|:---:|
| 성능 | | |
| <ul style="list-style-type: none;"><li>조정된 R 제곱</li></ul> |0.96 |해당 없음 |
| <ul style="list-style-type: none;"><li>결정 <br />계수</li></ul> |해당 없음 |0.78<br />(낮은 정확도) |
| 평균 절대 오류 |$9.5M |$19.4M |
| 평균 절대 오차율(%) |6.03% |12.2% |

프로세스 및 결과 hello 개발자 및 데이터 과학자에서 수행한 hello 기계 학습 팀, 몇 가지 유용한 팁 신속 하 게 제공 합니다. 

* Hello를 사용 하는 경우 [선형 회귀] [ linear-regression] 기계 학습 스튜디오의 모듈을 두 가지 방법이 제공 됩니다.
  * 온라인 기울기 하강: 보다 큰 규모의 문제에 적합할 수 있습니다.
  * 최소 자승법: 선형 회귀를 듣고 때 대부분의 사람들이 생각 hello 방법입니다. 데이터 집합이 작은 경우 최소 자승법이 보다 적합할 수 있습니다.
* 작업은 hello L2 정규화 가중치 매개 변수 tooimprove 성능 조정 하는 것이 좋습니다. 기본적으로 too0.001 설정 이지만 작은 데이터 집합에 대 한 म 설정할 too0.005 tooimprove 성능. 

### <a name="mystery-solved"></a>문제 해결!
달성 hello 권장 사항, 적용 하는 경우 Excel과 마찬가지로 기계 학습 스튜디오에서 동일한 기준 성능 hello: 

|  | Excel | Studio(초기) | Studio w/ 최소 자승 |
| --- |:---:|:---:|:---:|
| 레이블이 지정된 값 |실제 값(숫자) |동일 |동일 |
| 학습자 |Excel -> 데이터 분석 ->회귀 |선형 회귀 |Linear Regression |
| 학습자 옵션 |해당 없음 |기본값 |최소 자승법<br />L2 = 0.005 |
| 데이터 집합 |26개 행, 3가지 기능, 1개 레이블 모든 숫자 |동일 |동일 |
| 분할: 학습 |Excel은 hello에 먼저 18 개의 행을 학습, 마지막 8 개 행 hello에서 테스트 합니다. |동일 |동일 |
| 분할: 테스트 |적용 되는 회귀 수식이 excel toohello 마지막 8 개 행 |동일 |동일 |
| **성능** | | | |
| 조정된 R 제곱 |0.96 |해당 없음 | |
| 결정 계수 |해당 없음 |0.78 |0.952049 |
| 평균 절대 오류 |$9.5M |$19.4M |$9.5M |
| 평균 절대 오차율(%) |<span style="background-color: 00FF00;"> 6.03%</span> |12.2% |<span style="background-color: 00FF00;"> 6.03%</span> |

또한 hello Excel 계수와 비교도 toohello 기능 가중치를 hello Azure 학습 된 모델에서.

|  | Excel 계수 | Azure 기능 가중치 |
| --- |:---:|:---:|
| 가로채기/바이어스 |19470209.88 |19328500 |
| 기능 A |0.832653063 |0.834156 |
| 기능 B |11071967.08 |11007300 |
| 기능 C |25383318.09 |25140800 |

## <a name="next-steps"></a>다음 단계
싶었기 Excel 내에서 tooconsume hello 기계 학습 웹 서비스. 필요한 방식으로 toocall hello 기계 학습 웹 서비스와 Excel 데이터의 행 및 반환 하도록 비즈니스 분석가 Excel 않으며이 함수에 의존 hello tooExcel 값을 예측 합니다. 

했습니다 toooptimize 예제의 모델에서는 hello 옵션 및 기계 학습 스튜디오에서 사용할 수 있는 알고리즘을 사용 하 여 합니다.

### <a name="integration-with-excel"></a>Excel과 통합
솔루션 toooperationalize hello 학습 된 모델에서 웹 서비스를 만들어 우리의 기계 학습 회귀 모델을 했습니다. 몇 분 안에 hello 웹 서비스를 만들었습니다 및 수 이름을 tooreturn Excel에서 직접 예측된 수익 값입니다. 

hello *웹 서비스 대시보드* 섹션에는 다운로드 가능한 Excel 통합 문서에 포함 되어 있습니다. hello 통합 문서 제공 hello 웹 서비스 API 및 스키마 정보가 포함 된 미리 서식이 지정 됩니다. 클릭할 때 *Excel 통합 문서 다운로드*, hello 통합 문서가 열리고 tooyour 로컬 컴퓨터를 저장할 수 있습니다. 

![][1]

Hello 통합 문서와 열려 아래와 같이 미리 정의 된 매개 변수를 파란색 hello 매개 변수 섹션으로 복사 합니다. Hello 매개 변수를 입력 Excel toohello 기계 학습 웹 서비스를 호출 하 고 hello 예측된 점수가 매겨진된 레이블 표시 됩니다 hello 녹색 예측 값 섹션. hello 통합 문서에는 매개 변수에서 입력 한 모든 행 항목에 대 한 학습 된 모델에 따라 매개 변수에 대 한 예측 toocreate 계속 됩니다. Toouse이 기능의 방식에 대 한 자세한 내용은 참조 하십시오. [Excel에서는 Azure 기계 학습 웹 서비스를 사용해](machine-learning-consuming-from-excel.md)합니다. 

![][2]

### <a name="optimization-and-further-experiments"></a>최적화 및 추가 실험
초기 Excel 이익을와 했습니다 했으므로 미리 toooptimize 우리의 기계 학습 선형 회귀 모델 이동 합니다. Hello 모듈을 사용 했습니다 [필터 기반 기능 선택] [ filter-based-feature-selection] 우리의 초기 데이터 요소와 그 선택에 tooimprove 데 도움을 준 4.6%의 성능이 향상 절대 오차 것을 의미 합니다. 향후 프로젝트에이 기능을 절약 주 특성 toofind hello 오른쪽의 데이터 집합 모델링 기능 toouse 반복에 사용 합니다. 

와 같은 추가 알고리즘 tooinclude 계획 다음 [Bayesian] [ bayesian-linear-regression] 또는 [승격 된 의사 결정 트리] [ boosted-decision-tree-regression] 우리의 실험 toocompare에서 성능을 제공 합니다. 

좋은 데이터 집합 tootry 회귀와 tooexperiment 원하는 경우 hello 에너지 효율성 회귀 샘플 데이터 집합, 숫자 특성이 여러 개인입니다. hello 데이터 집합은 기계 학습 스튜디오에서 hello 샘플 데이터 집합의 일부로 제공 됩니다. 다양 한 모듈 toopredict 학습에 사용할 수 있습니다가 열 부하 또는 냉각 로드 합니다. 아래 hello 차트는 hello 에너지 효율성 dataset 예측 hello 대상 냉각 가변 부하에 대해 서로 다른 회귀 성능 비교를 알아냅니다. 

| 모델 | 평균 절대 오류 | 제곱 평균 오차 | 상대 절대 오차 | 상대 제곱 오차 | 결정 계수 |
| --- | --- | --- | --- | --- | --- |
| 향상된 의사 결정 트리 |0.930113 |1.4239 |0.106647 |0.021662 |0.978338 |
| 선형 회귀(기울기 하강) |2.035693 |2.98006 |0.233414 |0.094881 |0.905119 |
| 신경망 회귀 |1.548195 |2.114617 |0.177517 |0.047774 |0.952226 |
| 선형 회귀(최소 자승법) |1.428273 |1.984461 |0.163767 |0.042074 |0.957926 |

## <a name="key-takeaways"></a>핵심 내용
Excel 회귀와 Azure 기계 학습 실험을 함께 실행하여 많은 것을 배울 수 있었습니다. Excel 및 기계 학습을 사용 하 여 toomodels 비교에서 만드는 hello 기준 모델 [선형 회귀] [ linear-regression] 주세요. Azure 기계 학습 알아보고 기회 tooimprove 데이터를 발견 했습니다 도움을 준 선택 영역 및 모델 성능입니다. 

또한 권장 toouse 인지 찾았습니다 [필터 기반 기능 선택] [ filter-based-feature-selection] tooaccelerate 미래 예측 프로젝트. 기능 선택 tooyour 데이터를 적용 하면 보다 나은 전반적인 성능 기계 학습에서 향상 된 모델을 만들 수 있습니다. 

hello 기능 tootransfer hello systemically tooExcel 기계 학습에서에서 예측 분석 하면 크게 증가의 hello 기능 toosuccessfully 예측 결과 tooa 광범위 한 비즈니스 사용자 그룹을 제공 합니다. 

## <a name="resources"></a>리소스
회귀 작업에 유용한 일부 리소스는 다음과 같습니다. 

* Excel의 회귀 Excel에서 회귀를 사용해 본 적이 없는 경우 [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html) 자습서를 통해 쉽게 사용할 수 있습니다.
* 회귀와 예측 Tyler 갖추어 toodo 시간 선형 회귀에 대 한 좋은 초보자 설명을 포함 하는 Excel에서 시계열 예측 하는 방법을 설명 하는 블로그 게시물을 작성 했습니다. [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* 최소 자승법 선형 회귀: 결함, 문제점 및 단점 회귀에 대한 개요 및 설명은 [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)를 참조하세요.

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

