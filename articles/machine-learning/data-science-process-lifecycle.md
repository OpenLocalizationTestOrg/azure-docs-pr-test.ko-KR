---
title: "팀 데이터 과학 프로세스 수명 주기 aaaAzure | Microsoft Docs"
description: "단계는 데이터 과학 프로젝트 tooexecute를 필요합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>팀 데이터 과학 프로세스 수명 주기

권장 되는 주기를 제공 하는 hello 팀 데이터 과학 프로세스 (TDSP) 사용할 수 있는 toostructure 데이터 과학 프로젝트. hello 수명 주기에서 다음에 나오는 프로젝트 일반적으로 실행 될 때 시작 toofinish hello 단계를 간략하게 설명 합니다. 다른 데이터 과학 수명 주기를와 같은 사용 중인 경우 [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) 회사의 사용자 지정 프로세스를 계속 사용할 수 있습니다 또는 작업 기반 TDSP 이러한 개발 주기 hello 합니다. 

이 주기는 지능형 응용 프로그램의 일부로 의도 한 tooship 되는 데이터 과학 프로젝트에 대 한 설계 되었습니다. 이러한 응용 프로그램은 예측 분석을 위해 기계 학습 또는 인공 지능 모델을 배포합니다. 예비 데이터 과학 프로젝트 및 임시 분석 프로젝트에서 이 프로세스를 사용하여 활용할 수도 있습니다. 하지만 이러한 경우 설명된 몇 가지 단계가 필요하지 않습니다.    

여기 hello의 시각적 표현인 **팀 데이터 과학 프로세스 수명 주기**합니다. 

![TDSP 수명 주기](./media/data-science-process-overview/tdsp-lifecycle.png) 

hello TDSP 수명 주기는 반복적으로 실행 되는 5 개의 주요 단계로 구성 됩니다. 내용은 다음과 같습니다.

* **비즈니스 이해**
* **데이터 취득 및 이해**
* **모델링**
* **배포웹사이트를**
* **고객 승인**

각 단계에 대해 다음 정보는 hello 제공:

* **목표**: hello 구체적 목표입니다.
* **어떻게 toodo 것**: hello 설명 된 특정 작업 및 지침을 완료 하에 제공 합니다.
* **아티팩트**: hello 결과물 및 hello를 제작 하는 것에 대 한 지원.


## <a name="1-business-understanding"></a>1. 비즈니스 이해

### <a name="goals"></a>목표
* hello **변수 키** hello로 tooserve 않은 지정 된 **대상 모델** 관련된 된 메트릭을 사용 되 고 hello 프로젝트에 대 한 hello 성공을 확인할 합니다.
* 관련 hello **데이터 원본** hello 비즈니스에 대 한 액세스 tooor 요구 tooobtain 있는지 식별 됩니다.

### <a name="how-toodo-it"></a>어떻게 toodo 것
이 단계에서 설명하는 두 가지 기본 작업은 다음과 같습니다. 

* **목표 정의**: 고객 및 기타 관련자 toounderstand 작업할 hello 비즈니스 문제를 식별 합니다. Hello 비즈니스 목표와 데이터 과학 기술 대상으로 지정할 수 있는지를 정의 하는 질문을 작성 합니다.
* **데이터 원본 식별**: hello hello 프로젝트 목표를 정의 하는 hello 질문에 대답 하는 데 유용한 찾기 hello 관련 데이터입니다.

#### <a name="11-define-objectives"></a>1.1 목표 정의

1. 이 단계는 중앙 목표는 tooidentify hello 키 **비즈니스 변수** hello 분석 toopredict 필요 함을 합니다. 이러한 변수는 참조 된 tooas hello **대상 모델** hello 연관 메트릭은 hello 프로젝트의 사용 되는 toodetermine hello 성공 하 고 있습니다. 해당 대상의 두 가지 예제는 사기성 되 고 주문 판매 예측 또는 hello 확률입니다.

2. Hello 정의 **프로젝트 목표** 있으며 "날카로운"의 질문을 관련 및 구체적이 고 명확한를 재정의 하 여 합니다. 데이터 과학의 이름을 사용 하 여 hello 진행 되며 이러한 사항을 tooanswer 번호입니다. 날카로운 질문에 대 한 자세한 내용은 참조 하십시오. [어떻게 toodo 데이터 과학](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) 블로그. 데이터 과학 / 기계 학습은 일반적으로 사용 되는 tooanswer 질문의 5 가지 유형:
 
   * 양 또는 개수는 얼마인가요? (회귀)
   * 어떤 범주? (분류)
   * 어떤 그룹? (클러스터링)
   * 이것은 이상한가요? (이상 감지)
   * 수행해야 할 옵션은? (권장)

    이러한 질문 중 어떤 질문을 하고 비즈니스 목표 달성을 위해 질문에 어떻게 대답할지를 결정합니다.

3. Hello 정의 **프로젝트 팀** hello 역할 및 해당 멤버의 책임을 지정 하 여 합니다. 더 많은 정보를 찾아내면 반복하는 높은 수준의 획기적인 계획을 개발합니다.  

4. **성공 메트릭 정의**를 수행합니다. 예를 들어: म 프로 모션 tooreduce 변동률을 제공할 수 있도록 X % 고객 변동을 예측 정확도의 hello 끝날 때이 3 개월 프로젝트를 달성 합니다. hello 메트릭 있어야 **스마트**: 
   * **S**pecific(특정) 
   * **M**easurable(측정 가능)
   * **A**chievable(달성 가능) 
   * **R**elevant(관련성) 
   * **T**ime-bound(시간 제한) 

#### <a name="12-identify-data-sources"></a>1.2 데이터 원본 식별
대답 tooyour 날카로운 질문의 알려진된 예가 포함 된 데이터 원본을 확인 합니다. 같은 데이터가 hello를 찾습니다.

* 데이터는 **관련성** toohello 질문 합니다. Hello 대상 및 기능 관련된 toohello 대상에 대 한 측정 가요?
* 데이터는는 **정확 하 게 계산할** 이 기능의 모델 대상과 hello 중요 합니다.

일반적을 예를 들어 기존 시스템 toocollect 필요한 및 다른 종류의 데이터 tooaddress 기록할 toofind 문제 hello hello 프로젝트 목표를 달성 합니다. 이 경우 toolook 외부 데이터 원본에 대 한 원하는 또는 시스템 toocollect 새 데이터를 업데이트할 수 있습니다.

### <a name="artifacts"></a>아티팩트
다음은이 단계에서는 hello 결과물이입니다.

* [**기본 문서 문서**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): 표준 템플릿을 hello TDSP 프로젝트 구조 정의에 제공 됩니다. 이것이 되 새로운 발견 하 고 비즈니스 요구 사항을 변경 하는 대로 hello 프로젝트 전반에 걸쳐 업데이트 되는 실무 문서입니다. hello 키는 tooiterate 진행률 hello 검색 프로세스를 통해 좀 더 자세하게 추가이 문서에 있습니다. 유지 hello 고객 및 기타 관련자와 hello 변경 관련 변경 내용 toothem hello에 대 한 hello 이유를 명확 하 게 전달 합니다.  
* [**데이터 원본**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources):이 hello **원시 데이터 소스** hello 섹션 **데이터 정의** hello TDSP 프로젝트에 있는 보고서 **데이터 보고서**  폴더입니다. 원래 hello 및 hello 원시 데이터에 대 한 대상 위치를 지정 합니다. 이후 단계에서 스크립트 toomove hello 데이터 tooyour 분석 환경와 같은 추가 세부 정보에 채웁니다.  
* [**데이터 사전**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries):이 문서에서는 hello 클라이언트에서 제공 하는 hello 데이터 설명 합니다. 이러한 설명은 hello 스키마 (데이터 형식, 있는 경우 유효성 검사 규칙에 대 한 정보)에 대 한 정보를 포함 하 고 사용 가능한 경우 엔터티-관계 다이어그램을 hello 합니다.


## <a name="2-data-acquisition-and-understanding"></a>2. 데이터 취득 및 이해

### <a name="goals"></a>목표
* 잘 정리 되 고 고품질 데이터 집합 인 관계 toohello 대상 변수를 이해 하는 hello 분석 적절 한 환경 준비 toomodel에에서 있는.
* 데이터 파이프라인 toorefresh hello 및 점수 솔루션 아키텍처 데이터 정기적으로 개발 되었습니다.

### <a name="how-toodo-it"></a>어떻게 toodo 것
이 단계에서 설명하는 세 가지 기본 작업은 다음과 같습니다.

* **Hello 데이터 수집** hello 대상 분석 환경으로 합니다.
* **Hello 데이터 탐색** toodetermine hello 데이터 품질은 적절 한 tooanswer hello 질문 하는 경우. 
* **데이터 파이프라인 설정** tooscore new 또는 정기적으로 데이터가 새로 고쳐집니다.

#### <a name="21-ingest-hello-data"></a>2.1 hello 데이터 수집
교육 등의 분석 작업 고 예측은 실행 toobe toohello 대상 위치 소스 위치에서 hello toomove hello 데이터 처리를 설정 합니다. 기술 세부 정보 및 toodo이 다양 한 Azure 데이터 서비스를 확인 하려면 어떻게 해야의 옵션에 대 한 [데이터 분석을 위해 저장 환경에 로드](machine-learning-data-science-ingest-data.md)합니다. 

#### <a name="22-explore-hello-data"></a>2.2 hello 데이터를 탐색 합니다.
모델을 학습 하기 전에 toodevelop hello 데이터의 사운드 이해 해야 합니다. 실제 데이터 집합은 종종 난해하거나 가치가 없거나 상당히 일치하지 않습니다. 데이터 요약 및 시각화 데이터의 사용된 tooaudit hello 품질 수 있으며 필요한 tooprocess hello 데이터 모델링을 위한 준비가 될 때까지 hello 정보를 제공 됩니다. 이 프로세스는 종종 반복적입니다.

호출 하는 자동화 된 유틸리티를 제공 하는 TDSP [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp hello 데이터를 시각화 하 고 데이터 요약 보고서를 준비 합니다. IDEAR 첫 번째 tooexplore hello 데이터 toohelp로 시작 하는 것이 좋습니다 코딩이를 대화형으로 이해 초기 데이터를 개발 하 고 다음 데이터 탐색 및 시각화에 대 한 사용자 지정 코드를 작성 합니다. Hello 데이터 정리에 대 한 지침을 참조 하십시오. [작업에 대 한 향상 된 기계 학습 tooprepare 데이터](machine-learning-data-science-prepare-data.md)합니다.  

Hello hello 정리 데이터 품질 만족 하는 hello 다음 단계는 toobetter 이해 하는 데 도움이 되는 hello 데이터에 고유한 hello 패턴 선택 하 고 대상에 대 한 적합 한 예측 모델을 개발 합니다. 충분 한 데이터 toomove 앞으로 hello 다음 모델링 단계를 통해이 있는지 여부와 얼마나 잘 연결 된 hello 데이터는 toohello 대상에 대 한 증명 정보를 찾습니다. 다시금 말하지만 이 프로세스는 종종 반복적입니다. 데이터 집합과 보다 정확 하 게 또는 관련성이 데이터 tooaugment hello hello 이전 단계에서 처음에 식별 된 toofind 새 데이터 소스를 할 수 있습니다.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 데이터 파이프라인 설정
또한 toohello 초기 수집 및 정리 hello 데이터를 일반적으로 tooset tooscore 새 데이터 처리 또는 새로 고침 hello 데이터를 정기적으로 지속적인 학습 프로세스의 일부로 합니다. 데이터 파이프라인 또는 워크플로를 설정하여 이 작업을 수행할 수 있습니다. 다음은 프로그램 [예제](machine-learning-data-science-move-sql-azure-adf.md) 방법의 tooset와 파이프라인 구성 [Azure 데이터 팩터리](https://azure.microsoft.com/services/data-factory/)합니다. 

Hello 데이터 파이프라인의 솔루션 아키텍처는이 단계에서 개발 됩니다. hello 파이프라인은 또한 hello 데이터 과학 프로젝트의 단계를 수행 하는 hello와 병렬로 개발 됩니다. 일괄 처리 기반 hello 파이프라인 수 있습니다 또는 스트리밍/실시간-일회용 또는 비즈니스에 따라 하이브리드 필요 하 고이 솔루션 통합 되는 기존 시스템의 제약 조건 hello 합니다. 

### <a name="artifacts"></a>아티팩트
hello 다음은이 단계에서는 hello 결과물입니다.

* [**데이터 품질 보고서**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md):이 보고서는 데이터 요약을 각 특성 및 대상, 변수 등 hello 순위 간 관계를 포함 [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) TDSP의 일부를 빠르게 생성할 수 있는 그대로 제공 하는 도구 CSV 파일 또는 관계형 테이블과 같은 테이블 형식 데이터 집합에이 보고서입니다. 
* **솔루션 아키텍처**: 모델을 작성 한 후 다이어그램 또는 데이터 사용 되는 파이프라인 toorun 점수 매기기 또는 새 데이터에 대 한 예측의 설명 될 수 있습니다이 있습니다. 또한 hello 파이프라인 tooretrain 새 데이터를 기반으로 모델에 포함 되어 있습니다. hello 문서는 hello에 저장 [프로젝트](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) hello TDSP 디렉터리 구조 서식 파일을 사용 하는 경우에 디렉터리입니다.
* **검사점 의사 결정**: hello 사용할 값이 중요 한 과정으로 충분 한 toocontinue 인지 hello 프로젝트 toodetermine 전체 기능 엔지니어링 및 모델 작성을 시작 하기 전에 재평가 수 있습니다. 있습니다 수, 예를 들어 더 많은 데이터를 준비 tooproceed, 필요 toocollect 수 또는 중단 한 hello 프로젝트 hello 데이터 tooanswer hello 질문 존재 하지 않습니다.


## <a name="3-modeling"></a>3. 모델링

### <a name="goals"></a>목표
* Hello 기계 학습 모델에 대 한 최적의 데이터 기능입니다.
* Hello 대상 가장 정확 하 게 예측 하는 정보 제공 용 기계 학습 모델입니다.
* 프로덕션에 적합한 ML 모델

### <a name="how-toodo-it"></a>어떻게 toodo 것
이 단계에서 설명하는 세 가지 기본 작업은 다음과 같습니다.

* **엔지니어링 기능**: hello 원시 데이터 toofacilitate 모델 학습에서 데이터 기능을 만듭니다.
* **모델 학습**: 모델을 찾을 hello 답변 hello 질문 가장 정확 하 게 해당 성공 메트릭을 비교 하 여 합니다.
* **프로덕션에 적합한** 모델인지 확인합니다.

#### <a name="31-feature-engineering"></a>3.1 기능 엔지니어링
포함, 집계 및 원시 변수 toocreate의 변환 기능 엔지니어링 포함 hello hello 분석에 사용 되는 기능입니다. 모델에 영향을 주는 요인을에 대 한 정보를 원할 경우 다음 기능이 필요 하면 toounderstand 기능은 다른 관련된 tooeach hello 기계 학습 알고리즘은 toouse 방법 등에 해당 합니다. 이 단계는 창조적인 조합의 도메인 기술력과 insights hello 데이터 탐색 단계에서 얻은 필요 합니다. 이렇게 하면 관련이 없는 변수를 상당히 많이 제거하면서 유용한 정보를 제공하는 변수를 찾아 포함시킬 수 있습니다. 정보 제공 용 변수 향상 우리의 결과가 됩니다. 관련 없는 변수는 hello 모델에 불필요 한 노이즈를 소개합니다. 또한이 기능이 필요 하면 toogenerate 이러한 점수 매기기 하는 동안 가져온 새 데이터에 대 한 합니다. 따라서 이러한 기능의 hello 생성 점수 매기기 hello 시 사용할 수 있는 데이터에만 달라질 수 있습니다. 다양 한 Azure 데이터 기술을 사용할 때 기능 엔지니어링에 기술 지침에 대 한 참조 [hello 데이터 과학 프로세스에서에서 엔지니어링 팀 기능](machine-learning-data-science-create-features.md)합니다. 

#### <a name="32-model-training"></a>3.2 모델 학습
대답하려는 질문 유형에 따라 다양한 모델링 알고리즘을 사용할 수 있습니다. Hello 알고리즘 선택에 대 한 지침을 참조 하십시오. [방법을 Microsoft Azure 기계 학습 알고리즘 toochoose](machine-learning-algorithm-choice.md)합니다. 이 문서는 Azure 기계 학습에 대 한 작성, 되었지만 hello 지침 제공 프로젝트를 학습 하는 모든 컴퓨터에 대 한 유용 합니다. 

모델 학습에 대 한 hello 프로세스 단계를 수행 하는 hello를 포함 되어 있습니다. 

* **입력 데이터를 분할 hello** 임의로 학습 데이터 집합과 테스트 데이터 집합에는 모델링에 대 한 합니다.
* **Hello 모델을 작성** hello 학습 데이터 집합을 사용 하 여 합니다.
* **평가** (학습 및 테스트 데이터 집합)의 경쟁 시스템 다양 한 관련된 조정 매개 변수 (매개 변수 비우기를 라고도 함)를 위한 대 hello로 관심 있는 hello 질문에 답변 하는 hello와 함께 알고리즘을 학습 시리즈 현재 데이터입니다.
* **Hello "최상의" 솔루션을 결정** 대체 방법 간의 hello 성공 메트릭을 비교 하 여 tooanswer hello 질문 합니다.

> [!NOTE]
> **누출을 방지**: toomake 비현실적으로 좋은 예측 모델 또는 기계 학습 알고리즘 수 있는 외부 hello 학습 데이터 집합의 데이터 유출 데이터의 hello 포함 하 여 발생할 수 있습니다. 유출은 데이터 과학자 받을 수 없는 이유 우려 것 보다 훨씬 좋은 toobe 예측 결과 true 도달 하는 일반적인 이유입니다. 이러한 종속성 하드 toodetect 수 있습니다. tooavoid 누출 분석 데이터 집합을 작성, 모델을 만들 및 hello 정확도 평가 사이의 반복과 필요 합니다. 
> 
> 

제공 된 [자동 모델링 및 보고 도구](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) TDSP 하는 여러 알고리즘을 통해 수 toorun 하 고 매개 변수는 초기 모델 tooproduce를 비우고 합니다. 또한 각 모델의 성능과 변수 중요도를 포함한 매개 변수 조합을 요약한 기본 모델링 보고서를 생성합니다. 이 프로세스는 추가 기능 엔지니어링을 진행할 수 있으므로 반복적입니다. 

### <a name="artifacts"></a>아티팩트
이 단계에서 생성 된 hello 아티팩트는 다음과 같습니다.

* [**기능 집합**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): hello hello 모델링 용으로 개발 된 hello 기능 설명 **기능 집합** hello 섹션 **데이터 정의** 보고서입니다. 포인터 toohello 코드 toogenerate hello 기능 및 hello 기능은 생성 된 방식에 대 한 설명을 포함 합니다.
* [**모델 보고서**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): 시도하는 각 모델에 대해 각 실험에 대한 세부 정보를 제공하는 템플릿 기반 표준 보고서가 생성됩니다.
* **검사점 의사 결정**: hello 모델 toodeploy 충분히 잘 수행 하는지 여부를 평가 하기 tooa 프로덕션 시스템입니다. 몇 가지 주요 질문 tooask이 됩니다.
  * 충분 한 신뢰도 hello 모델 응답 hello 질문 hello 테스트 데이터 제공 된? 
  * 다른 방법을 시도해야 합니다. 추가 데이터를 수집하고 더 많은 기능 엔지니어링을 수행하거나 다른 알고리즘으로 시험해 보겠습니까?


## <a name="4-deployment"></a>4. 배포

### <a name="goal"></a>목표
* 데이터 파이프라인을 사용 하 여 모델에는 배포 된 tooa 프로덕션 또는 최종 사용자 승인에 대 한 프로덕션 환경과 유사한 환경입니다. 

### <a name="how-toodo-it"></a>어떻게 toodo 것
이 단계에서 해결 hello 주 작업:

* **Hello 모델을 운용**: hello 모델과 파이프라인 tooa 프로덕션 또는 응용 프로그램에 사용 하기 위해 프로덕션 환경과 유사한 환경에 배포 합니다.

#### <a name="41-operationalize-a-model"></a>4.1 모델 운영
잘 수행 하는 모델 집합이 있으면 다른 응용 프로그램 tooconsume에 대 한 병원 수 있습니다. Hello 비즈니스 요구 사항에 따라 예측을 실시간으로 또는 일괄 처리 별로 만들어집니다. 병원 toobe, hello 모델 toobe 온라인 웹 사이트, 스프레드시트, 대시보드, 일련의 비즈니스 및 백 엔드 응용 프로그램 등 다양 한 응용 프로그램에서 쉽게 사용할 수 있는 개방형 API 인터페이스를 노출 하는. Azure Machine Learning 웹 서비스를 사용하는 모델 운영의 예는 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요. 또한 모범 사례 toobuild 원격 분석 되며 프로덕션 모델 hello에 모니터링 및 보고와 문제 해결 후속 시스템 상태와 함께 데이터 배포 파이프라인 toohelp hello.  

### <a name="artifacts"></a>아티팩트
* 시스템 상태 대시 보드 및 주요 메트릭 상태 대시보드
* 배포 세부 정보가 포함된 최종 모델링 보고서
* 최종 솔루션 아키텍처 문서

## <a name="5-customer-acceptance"></a>5. 고객 승인

### <a name="goal"></a>목표
* **Hello 프로젝트 결과물을 마무리**: hello 파이프라인과 hello 모델을 프로덕션 환경에서 배포 고객 목표를 만족 되는지 확인 합니다.

### <a name="how-toodo-it"></a>어떻게 toodo 것
이 단계에서 설명하는 두 가지 기본 작업은 다음과 같습니다.

* **시스템 유효성 검사**: 배포 된 hello 모델과 파이프라인 고객의 요구를 충족 하는지 확인 합니다.
* **프로젝트를 처리할**:는 프로덕션에서 toorun hello 시스템 toohello 엔터티입니다.

hello 고객의 비즈니스 요구를 충족 하는 hello 시스템 및 hello 대답의 클라이언트 응용 프로그램에서 사용 하기 위해 허용 가능한 정확도 toodeploy hello 시스템 tooproduction와 질문을 hello 확인 해야 합니다. 모든 hello 설명서를 종료 하 고 검토 합니다. 한 넘기기 hello 프로젝트 toohello 엔터티 작업에 대 한 책임의 완료 됩니다. 예를 들어 IT 또는 고객 데이터 과학 팀 또는 프로덕션 환경에서 hello 시스템을 실행 하는 일을 담당 하는 hello 고객의 에이전트가이 엔터티 수 있습니다. 

### <a name="artifacts"></a>아티팩트
이 마지막 단계에서 생성 하는 hello 주 아티팩트는 hello **고객에 대 한 프로젝트 보고서 종료**합니다. Hello에 대 한 유용한 해당 toolearn hello 프로젝트의 모든 세부 정보를 포함 하는 기술 보고서 이며 hello 시스템 운영 합니다. [종료 보고서](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) 템플릿은 TDSP에서 제공하며, 그대로 사용하거나 특정 클라이언트의 요구에 따라 사용자 지정할 수 있습니다. 

## <a name="summary"></a>요약
hello [팀 데이터 과학 프로세스 수명 주기](http://aka.ms/datascienceprocess) 일련의 hello 작업 지침을 제공 하는 단계를 반복된 toouse 예측 모델을 필요에 따라 모델링 됩니다. 이러한 모델을 프로덕션 환경 활용 toobe toobuild 지능형 응용 프로그램에 배포할 수 있습니다. 이 프로세스 수명 주기의 hello 목표 toocontinue toomove 데이터 과학 프로젝트 앞으로 지우기 engagement 끝 지점 방향으로입니다. 데이터 과학은 연구와 수 tooclearly 되 고 검색 작업 tooyour 팀이 개발자와 고객이 잘 정의 된 집합이 직원 표준화 된 서식 파일 수 있는 아티팩트를 사용 하 여 통신에 true 인 동안 오해 방지 고 복잡 한 데이터 과학 프로젝트의 성공적으로 완료 hello 가능성이 향상 됩니다.

## <a name="next-steps"></a>다음 단계
에 대 한 hello 프로세스의 모든 hello 단계를 보여 주는 종단 간 연습을 전체 **특정 시나리오에 맞춰** 도 제공 됩니다. 나타나고 hello에 대 한 축소판 설명과 함께 연결 [팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md) 항목입니다.

