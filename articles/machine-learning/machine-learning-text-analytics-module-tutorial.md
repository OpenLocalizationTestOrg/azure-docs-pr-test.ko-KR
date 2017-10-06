---
title: "Azure 기계 학습 스튜디오에서 aaaCreate 텍스트 분석 모델 | Microsoft Docs"
description: "텍스트 전처리, N 그램 또는 기능 해시 모듈을 사용 하 여 Azure 기계 학습 스튜디오에서 toocreate 텍스트 분석을 모델링 하는 방법"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오에서 텍스트 분석 모델 만들기
Azure 기계 학습 toobuild를 사용할 수 있으며 텍스트 분석 모델을 운용 있습니다. 예를 들어 이러한 모델은 문서 분류 또는 정서 분석 문제를 해결하는 데 유용할 수 있습니다.

텍스트 분석 실험에서는 일반적으로 다음을 수행합니다.

1. 텍스트 데이터 집합 정리 및 전처리
2. 전처리된 텍스트에서 숫자 특성 벡터 추출
3. 분류 또는 회귀 모델 학습
4. 점수와 hello 모델 유효성 검사
5. Hello 모델 tooproduction 배포

이 자습서에서는 Amazon 도서 리뷰 데이터 집합을 사용하여 정서 분석을 진행하면서 이러한 단계를 배우게 됩니다(연구 논문 “Biographies, Bollywood, Boom-boxes and Blenders: Domain Adaptation for Sentiment Classification”(저자: John Blitzer, Mark Dredze 및 Fernando Pereira), Association of Computational Linguistics(ACL), 2007) 참조). 이 데이터 집합은 리뷰 점수(1-2 또는 4-5) 및 자유 형식 텍스트로 구성됩니다. hello ´ ֲ toopredict hello 검토 점수: 낮은 (1-2) 또는 high (4-5).

Cortana Intelligence Gallery에서 이 자습서에 나오는 실험을 찾을 수 있습니다.

[도서 리뷰 예측](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[도서 리뷰 예측 - 예측 실험](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>1단계: 텍스트 데이터 집합 정리 및 전처리
2 클래스 분류로의 범주는 낮은 임계값과 높은 버킷 tooformulate hello 문제가 hello 검토 점수를 분할 하 여 hello 실험을 시작 합니다. [메타데이터 편집](https://msdn.microsoft.com/library/azure/dn905986.aspx) 및 [범주 값 그룹화](https://msdn.microsoft.com/library/azure/dn906014.aspx) 모듈을 사용합니다.

![레이블 만들기](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

그런 다음 사용 하 여 hello 텍스트 정리 우리 [전처리 텍스트](https://msdn.microsoft.com/library/azure/mt762915.aspx) 모듈입니다. 정리 하는 hello hello 데이터 집합의 hello 노이즈, 개선 하 고 hello 가장 중요 한 기능을 찾는 데 도움이 hello hello 최종 모델의 정확도 합니다. 중지 단어("the" 또는 "a"와 같은 일반 단어)와 숫자, 특수 문자, 중복된 문자, 전자 메일 주소 및 URL을 제거합니다. 또한 hello 텍스트 toolowercase 변환, hello 단어 lemmatize 하 고 다음으로 표시 된 문장 경계 검색 "| | |" 전처리 된 텍스트의 기호입니다.

![텍스트 전처리](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

경우에 어떻게 toouse 중지 단어의 사용자 지정 목록 시겠습니까? 선택적 입력으로 전달할 수 있습니다. 또한 사용자 지정 C# 구문 정규식 tooreplace 부분 문자열을 사용 하 고 음성 부분에서 단어를 제거할 수 있습니다: 명사, 동사 나 형용사.

완료 되 면 hello 전처리 hello 데이터 기차를 분할 및 테스트 집합 했습니다.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>2단계: 전처리된 텍스트에서 숫자 특성 벡터 추출
텍스트 데이터에 대 한 모델 toobuild 일반적으로 필요를 숫자 기능 벡터로 tooconvert 자유 형식 텍스트입니다. 이 예에서는 사용 [추출 N 그램 텍스트 기능](https://msdn.microsoft.com/library/azure/mt762916.aspx) 모듈 tootransform hello 텍스트 데이터 toosuch 형식입니다. 이 모듈은 공백으로 구분된 단어 열을 가져온 후 데이터 집합에 나타나는 단어 사전 또는 단어 N-Gram을 계산합니다. 그런 다음 각 단어 또는 N-Gram이 이러한 레코드에 나오는 횟수를 계산하고 그 개수에서 특성 벡터를 만듭니다. 이 자습서에서는 우리의 기능 벡터는 단일 단어 및 두 개의 후속 단어 조합을 하므로 N 그램 크기 too2를 설정 합니다.

![N-Gram 추출](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

TF 적용할 * tooN 그램 가중치 IDF (용어 빈도 역 문서 빈도)를 계산 합니다. 이 방법을 사용 하는 단일 레코드에 자주 나타나지만 있지만 hello 전체 데이터 집합에서 드물게의 가중치를 추가 합니다. 다른 옵션으로는 이진, TF 및 그래프 가중이 포함됩니다.

이러한 텍스트 특성은 종종 차원이 매우 높습니다. 예를 들어 모음에 100,000개의 고유 단어가 있는 경우 특성 공간은 100,000개 차원을 가지고, N-Gram이 사용되는 경우 더 큰 공간을 갖습니다. hello N 그램 기능 추출 모듈 옵션 tooreduce hello 차원 집합을 제공합니다. Tooexclude 단어는 짧은 또는 또는 일반적이 지 않은 너무 길거나 너무 자주 toohave 중요 한 예측 값을 선택할 수 있습니다. 이 자습서에서는 5개보다 적은 레코드 또는 레코드의 80% 이상에서 나타나는 N-Gram을 제외합니다.

또한 예측 대상을 사용 하 여 기능 선택 tooselect 가장 hello 있는 기능만 상관 관계를 사용할 수 있습니다. 카이 제곱 기능 선택 tooselect 1000 기능 사용합니다. 추출 N 그램 모듈의 hello 오른쪽 출력을 클릭 하 여 선택한 단어 또는 N 그램의 hello 어휘를 볼 수 있습니다.

N 그램 기능 추출에 다른 접근 방식은 toousing으로 기능 해시 모듈을 사용할 수 있습니다. 그러나 [특성 해시](https://msdn.microsoft.com/library/azure/dn906018.aspx) 는 기본 제공 특성 선택 기능이나 TF* IDF 가중 기능이 없습니다.

## <a name="step-3-train-classification-or-regression-model"></a>3단계: 분류 또는 회귀 모델 학습
이제 hello 텍스트 변형 된 toonumeric 기능 열 되었습니다. 데이터 집합 tooexclude에서 열 선택를 사용 하도록 여전히 이전 단계에서 문자열 열이 포함 hello 데이터 집합에 있습니다.

사용 하 여이 [2 클래스 로지스틱 회귀](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict 목표: 높거나 낮은 검토 점수입니다. 이 시점에서 hello 텍스트 분석 문제 일반 분류 문제의 경우에 변환 된 합니다. Azure 기계 학습 tooimprove hello 모델에서 사용할 수 있는 hello 도구를 사용할 수 있습니다. 예를 들어 다른 분류자 toofind에 게 제공 하거나 hyperparameter 튜닝 tooimprove hello 정확도 사용 하 여 이러한 정확도 결과 테스트할 수 있습니다.

![학습 및 점수 매기기](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>4 단계: 점수와 hello 모델 유효성 검사
Hello 학습 된 모델 유효성을 검사 하는 방법을? Hello 테스트 데이터 집합에 대해 점수 하 고 hello 정확도 평가 합니다. 그러나 hello 모델 N 그램 및 hello 학습 데이터 집합에서 해당 가중치의 hello 어휘를 배웠습니다. 따라서 새로 toocreating hello 어휘 해도 상관 없다면 테스트 데이터에서 기능으로 추출 하는 경우 해당 용어와 이러한 가중치 사용 해야 했습니다. 따라서에서는 추가 N 그램 기능 추출 모듈 toohello hello 실험 분기 점수 매기기, 교육 분기에서 hello 출력 어휘를 연결 및 tooread 전용 hello 어휘 모드를 설정 합니다. 또한 hello N 그램의 진동수에 의해 hello 최소 too1 인스턴스 설정 및 필터링 최대 too100 %를 사용 하지 않도록 설정 하 고 hello 기능 선택이 해제 합니다.

Hello 된 데이터는 테스트에서 텍스트 열 변환 된 후 toonumeric 기능 열을 hello 문자열 학습 분기에서와 같이 이전 단계에서 열을 제외 합니다. 그런 다음 모델 점수 매기기 모듈 toomake 예측 및 평가 모델 모듈 tooevaluate hello 정확도 사용합니다.

## <a name="step-5-deploy-hello-model-tooproduction"></a>5 단계: hello 모델 tooproduction 배포
hello 모델은 배포 된 것 같군요 toobe tooproduction입니다. 모델을 웹 서비스로 배포하면 자유 형식 텍스트 문자열을 입력으로 받은 후 예측 "높음" 또는 "낮음"을 반환합니다. 배운 hello N 그램 어휘 tootransform hello 텍스트 toofeatures을 사용 하 고 로지스틱 회귀 모델 toomake 해당 기능에서 예측을 학습 합니다. 

hello 예측 실험을 tooset를 먼저 저장 hello N 그램 어휘, 데이터 집합으로 및 hello hello 실험 hello 교육 분기에서 로지스틱 회귀 모델을 학습 합니다. 그런 다음 "다른 이름으로 저장" toocreate를 사용 하 여 hello 실험 예측 실험에 대 한 실험 그래프를 저장 합니다. Hello 실험에서 hello 분할 데이터 모듈과 hello 교육 분기 제거합니다. 다음 연결 hello 이전에 저장 된 N 그램 어휘 및 모델 tooExtract N 그램 기능 및 모델 점수 매기기 모듈 각각. 또한 hello 모델 평가 모듈을 제거 합니다.

전처리 텍스트 모듈 tooremove hello 레이블 열을 하기 전에 데이터 집합 모듈에서 열 선택 삽입 하 고 점수 모듈에서 "추가 점수 열 toodataset" 옵션 선택을 취소 합니다. 이런 방식으로 hello 웹 서비스는 hello 레이블 toopredict를 시도 하 고 hello 입력된 기능에 대 한 응답에서을 표시 하지 않습니다를 요청 하지 않습니다.

![예측 실험](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

이제 웹 서비스로 게시되고, 요청-응답 또는 일괄 처리 실행 API를 사용하여 호출할 수 있는 실험이 생성되었습니다.

## <a name="next-steps"></a>다음 단계
[MSDN 설명서](https://msdn.microsoft.com/library/azure/dn905886.aspx)에서 텍스트 분석 모듈에 대해 자세히 알아봅니다.

