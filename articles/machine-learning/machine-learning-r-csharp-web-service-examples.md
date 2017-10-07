---
title: "aaa(deprecated) 컴퓨터 학습 웹 서비스 예제 R-Azure 사용 하 여 빌드한 | Microsoft Docs"
description: "(사용 되지 않음) 웹 서비스 예제에서는 유용한 R 코드 및 기계 학습을 사용 하 여 만든 및 toohello Azure 마켓플레이스에서 게시 찾습니다."
keywords: "csharp, r 코드, 웹 서비스 예제"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a>(사용 되지 않음) 웹 서비스는 Azure 기계 학습 및 게시 된 tooMicrosoft Azure Marketplace에서 R 코드를 사용 하는 예제

> [!NOTE]
> Microsoft DataMarket hello 사용 중지 됩니다 하 고 이러한 Api가 사용 되지 않습니다. 
> 
> Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다. Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

이 문서에는 예제 웹 서비스는 Azure 기계 학습을 사용 하 여 만든 및 toohello Azure 마켓플레이스에서 게시 합니다. 각 웹 서비스 예제에는 전체 문서는 연결을 위해 hello 서비스를 테스트 하 고 어떻게 hello 사용자 직접 만들 수 있습니다 유사한 서비스를 설명 하는 샘플 데이터 집합을 포함 합니다. 

Azure 기계 학습 스튜디오에서 사용자가 R 코드를 작성 하 고 몇 번의 클릭으로 hello 전 세계 tooconsume 응용 프로그램 및 장치에 대 한 웹 서비스로 게시할 수입니다. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

사용자 지정 텍스트 마이닝 감성 분석 예측자 toocreating 통계 기능을 제공 하는 간단한 계산기를 생성, 신규 및 경력 전화 R 사용자는 사용자가 Azure 기계 학습의 R을 운용 수 있습니다. hello 용이성에서 얻을 수합니다 있습니다. 코드입니다. 모바일 앱 또는 웹 사이트를 통해 잠재적으로 사용자가 해당 웹 서비스를 소비 될 수 하는 동안 예제는 기계 학습 수 운영 화 방법을 tooshow 이러한 웹 서비스의 hello 용도 R 분석 용도로 사용에 대 한 스크립트에 포함할 및 toocreate 사용 되는 웹 서비스 R 코드의 맨 위로 이동 합니다.

각 예제에는 웹 서비스 소비를 위한 C# 예제가 포함되어 있습니다.

![Azure 기계 학습의 R 코드의 다이어그램: R 솔루션을 게시 된 toohello Azure 마켓플레이스 또는 독점적인 사용 합니다.][1]

다음 시나리오는 hello를 것이 좋습니다.

## <a name="scenario-1-generic-model"></a>시나리오 1: 일반 모델
사용자 기본 예측 시계열 데이터 또는 고급 분석을 사용 하 여 사용자가 작성 한 R 메서드 등과 같은 tooa 적용 된 새 사용자의 데이터 일 수 있는 일반 모델을 사용 합니다. 이 사용자가 hello 게시 tooconsume 하면서 자신의 데이터를 다른 사용자에 대 한 웹 서비스로 모델링 합니다.

* [이진 분류자](machine-learning-r-csharp-binary-classifier.md)
* [클러스터 모델](machine-learning-r-csharp-cluster-model.md)
* [다변량 선형 회귀](machine-learning-r-csharp-multivariate-linear-regression.md)
* [예측 - 지수 평활법](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [EETS + STL 예측](machine-learning-r-csharp-retail-demand-forecasting.md)
* [예측 - ARIMA(자동 회귀 통합 이동 평균)](machine-learning-r-csharp-arima.md)
* [생존 분석](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>시나리오 2: 학습된 모델 – 특정 데이터
사용자의 개성 질문의 큰 샘플 k 알고리즘 toopredict hello 사용자의 개성 형식을 통해 클러스터링 또는 설문 조사 toopredict 사용된 될 수 있는 데이터는 개인의 상태와 같은 R 코드를 통해 유용한 예측을 제공 하는 데이터가 있는 생존 분석 R 패키지와 함께 lung 유방암에 대 한 위험 합니다. hello 사용자가 새 사용자의 결과 예측 하는 웹 서비스를 통해 hello 데이터를 게시 합니다.

## <a name="scenario-3-trained-model--generic-data"></a>시나리오 3: 학습된 모델 – 일반 데이터
사용자는 웹 서비스 toobe 빌드되고 다양 한 유형의 사용 사례 및 시나리오에 일반적인 방식으로 적용할 수 있는 일반 데이터 (예: 텍스트 모음)에 있습니다.

* [어휘집 기반 감정 분석](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>시나리오 4: 고급 계산기
사용자는 고급 계산 또는 모든 학습 된 모델 또는 모델 toohello 사용자 데이터의 맞춤 요구 하지 않는 시뮬레이션을 제공 합니다.

* [비율 차이 테스트](machine-learning-r-csharp-difference-in-two-proportions.md)
* [정규 분포 제품군](machine-learning-r-csharp-normal-distribution.md)
* [이항 분포 패키지](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>FAQ
Hello 웹 서비스 또는 게시 toohello Marketplace의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



