---
title: "aaaClean Azure 기계 학습에 대 한 데이터를 준비 하 고 | Microsoft Docs"
description: "데이터를 전처리 하 고 깨끗 tooprepare 기계 학습에 대 한 것입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>향상 된 기계 학습에 대 한 작업 tooprepare 데이터
데이터 전처리 및 정리는 일반적으로 기계 학습에 데이터 집합을 효과적으로 사용할 수 있기 전에 수행해야 하는 중요한 작업입니다. 원시 데이터는 노이즈가 많고, 불안정하고, 값이 누락된 경우가 종종 있습니다. 이러한 데이터를 모델링에 사용하면 결과가 잘못될 수 있습니다. 이러한 작업 hello 팀 데이터 과학 프로세스 (TDSP)의 일부 이며 일반적으로 사용 된 데이터 집합 toodiscover 및 필요한 계획 hello 사전 처리는 초기 탐색을 수행 합니다. Hello TDSP 프로세스에 대 한 지침 보다 자세한 참조 hello에 설명 된 hello 단계 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.

전처리 및 정리 태스크를 같은 hello 데이터 탐색 작업을 수행할 수 있는 다양 한 환경에서는 SQL 또는 하이브 또는 Azure 기계 학습 스튜디오에서는 같은 및 다양 한 도구와 데이터가 따라 Python 또는 R 등의 언어에 저장 하 고 형식 지정 방법을 키를 누릅니다. TDSP 특성상 반복적이 이므로 이러한 작업 hello 워크플로의 hello 프로세스의 다양 한 단계에서 수행할 수 있습니다.

이 문서에서는 Azure 기계 학습에 데이터를 수집하기 전 또는 후에 수행할 수 있는 다양한 데이터 처리 개념 및 작업을 소개합니다.

데이터 탐색 및 Azure 기계 학습 스튜디오에서 수행 하는 전처리 작업의 예를 들어 참조 hello [Azure 기계 학습 스튜디오에서 데이터를 전처리](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) 비디오.

## <a name="why-pre-process-and-clean-data"></a>데이터 전처리 및 정리가 필요한 이유
다양 한 소스에서 실제 데이터를 수집 하 고 프로세스 이므로 불규칙 하거나 hello 데이터 집합의 hello 품질을 손상 시 키 지 손상 된 데이터가 포함 될 수 있습니다. hello 일반적인 데이터 품질 발생 하는 사항은 다음과 같습니다.

* **불완전**: 데이터에 특성이 없거나 값이 누락되었습니다.
* **노이즈가 많은**: 데이터에 잘못된 레코드 또는 이상값이 있습니다.
* **불일치**: 데이터에 충돌하는 레코드 또는 일치하지 않는 값이 있습니다.

우수한 예측 모델을 구축하려면 우수한 데이터가 필요합니다. 가비지 아웃 tooavoid "가비지" 및 데이터 품질을 향상 하 고 따라서 성능 모델, 명령적 tooconduct 데이터 상태 화면 toospot 데이터 문제를 조기에 단계 정리 및 데이터 처리에 해당 하는 hello을 결정 하는 합니다.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>가장 일반적으로 사용되는 데이터 상태 검사 방법으로 어떤 것이 있습니까?
Hello 일반 데이터 품질을 확인 하 여 확인할 수 있습니다.

* 수가 hello **레코드**합니다.
* 수가 hello **특성** (또는 **기능**).
* hello 특성 **데이터 형식** (명목, 서 수, 또는 연속)입니다.
* 수가 hello **누락 값**합니다.
* **제대로** hello 데이터입니다.
  * Hello 데이터 CSV 또는 TSV 인 경우에 개별 하 여 hello 열 구분 기호 및 선 구분 기호가 항상 올바르게 막대와 꺾은선이를 확인 합니다.
  * Hello 데이터는 HTML 또는 XML 형식에 있는지 여부를 hello 데이터가 잘 작성 기반의 해당 표준에를 확인 합니다.
  * 구문 분석 구조화 또는 반 구조화 된 데이터에서 주문 tooextract 구조화 된 정보에 필요한 수도 있습니다.
* **일관되지 않은 데이터 레코드**. 허용 되는 값의 hello 범위를 확인 합니다. 예를 들어 hello 데이터 학생 GPA, 범위를 지정 하는 hello에 hello GPA는 되었는지 확인 하 고 포함 된 경우 예를 들어 0 ~ 4입니다.

데이터와 함께 문제를 발견할 경우 **처리 단계** 필요한 누락 된 값, 데이터 정규화, 분할, 텍스트 처리 tooremove 정리 포함 되기도 및/또는 영향을 줄 수 있는 포함 된 문자를 대체 합니다. 데이터 맞춤, 혼합된 데이터 형식은 공통 필드 및 다른 합니다.

**Azure 기계 학습에서는 올바르게 구성된 테이블 형식 데이터를 사용합니다**.  Hello 데이터 테이블 형식에 이미 있으면 Azure 기계 학습 hello 기계 학습 스튜디오에서에서 사용 하 여 직접 데이터 전처리를 수행할 수 있습니다.  데이터 테이블 형식에 없는 경우 XML을 구문 분석에 의견을 언급 해서도 주문 tooconvert hello 데이터 tootabular 양식에서 필요할 수 있습니다.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>몇 가지 주요 작업 데이터 사전 처리 hello?
* **데이터 정리**: 누락된 값을 채우거나 노이즈가 많은 데이터와 이상값을 감지하여 제거합니다.
* **데이터 변환**: 데이터 tooreduce 차원 및 노이즈를 정규화 합니다.
* **데이터 감소**: 데이터를 쉽게 처리할 수 있도록 데이터 레코드 또는 특성을 샘플링합니다.
* **데이터 분할**: Convert 연속 특성 특정 기계 학습 방법의을 사용 하기 쉽도록 toocategorical 특성입니다.
* **텍스트 정리**: 탭으로 구분된 데이터 파일에 포함된 탭, 레코드 줄 맞춤 문제를 일으킬 수 있는 포함된 새 줄 등 데이터 정렬 문제를 일으킬 수 있는 포함된 문자를 제거합니다.

아래의 섹션 들 hello에서는 이러한 데이터 처리 단계 중 일부를 자세히 설명합니다.

## <a name="how-toodeal-with-missing-values"></a>어떻게 toodeal 누락 된 값?
값이 누락 된 toodeal, 것이 가장 좋습니다 toofirst hello 누락 값의 toobetter 핸들 hello 문제에 대 한 hello 하는 이유를 식별 합니다. 일반적인 누락 값 처리 방법은 다음과 같습니다.

* **삭제**: 값이 누락된 레코드를 제거합니다.
* **더미 대체**: 누락된 값을 더미로 대체합니다. 예를 들어 범주 값은 *알 수 없음*, 숫자 값은 0으로 대체합니다.
* **대체 의미**: hello 누락 된 데이터가 숫자 이면 hello 평균 hello 누락 값 대체 합니다.
* **자주 사용 하는 대체**: hello 누락 된 데이터 범주 이면 hello 가장 자주 나타나는 항목으로 hello 누락 값 대체
* **회귀 대체**:는 회귀 메서드 tooreplace 누락 값의 이전 상태로 되돌아간된 값으로 사용 합니다.  

## <a name="how-toonormalize-data"></a>어떻게 toonormalize 데이터?
데이터 정규화 다시 조정 숫자 값 tooa 범위를 지정 합니다. 일반적인 데이터 정규화 방법은 다음과 같습니다.

* **최소-최대 정규화**: 예를 들어 0과 1 사이의 여기서 hello 최소 값은 크기 조정 된 too0 및 최대 값 too1를 선형으로 변환 하는 hello 데이터 tooa 범위입니다.
* **Z 점수 정규화**: 평균과 표준 편차를 기반으로 데이터의 크기를 조정: hello 데이터와 hello 평균 hello 차이 hello 표준 편차로 나눕니다.
* **10 진수 배율**: hello 특성 값의 hello 소수점을 이동 하 여 hello 데이터를 확장 합니다.  

## <a name="how-toodiscretize-data"></a>어떻게 toodiscretize 데이터?
연속 값 toonominal 특성 또는 간격으로 변환 하 여 데이터를 분할할 수 있습니다. 다음은 이 작업을 수행하는 방법 중 일부입니다.

* **동일한 너비 bin 설정을**: hello 동일 크기 및 hello bin 번호 bin에 속하는 hello 값 할당의 N 그룹 특성의 가능한 모든 값의 hello 범위를 나눕니다.
* **높이가 같도록 범주화**: hello 범위를 나눌 동일한 수의 인스턴스를 각각 포함 된 hello n 개 그룹에 특성의 가능한 모든 값의 다음 hello 값 할당에 속하는 hello로 bin에 숫자를 범주화 합니다.  

## <a name="how-tooreduce-data"></a>어떻게 tooreduce 데이터?
쉽게 데이터 처리에 대 한 다양 한 메서드 tooreduce 데이터 크기가 있습니다. 데이터 크기와 hello 도메인에 따라 hello 다음 메서드를 적용할 수 있습니다.

* **샘플링 기록**: hello 데이터 레코드를 샘플링 하 고만 hello 데이터에서 hello 해당 하위 집합을 선택 합니다.
* **샘플링 특성**: hello 데이터에서 hello 가장 중요 한 특성의 하위 집합만 선택 합니다.  
* **집계**: hello 데이터를 그룹으로 나누고 각 그룹에 대 한 hello 번호를 저장 합니다. 예를 들어 hello hello 지난 20 년을 통해 식당 체인의 숫자 수 일별 수익 집계 toomonthly 수익 tooreduce hello hello 데이터의 크기.  

## <a name="how-tooclean-text-data"></a>어떻게 tooclean 텍스트 데이터?
**테이블 형식 데이터의 텍스트 필드** 에 열 정렬 및/또는 레코드 경계에 영향을 미치는 문자가 포함될 수 있습니다. 예를 들어 탭으로 구분된 파일에 포함된 탭은 열 정렬 문제를 일으킬 수 있고, 포함된 새 줄 문자는 줄 맞춤 문제를 일으킬 수 있습니다. 부적절 한 텍스트 처리 텍스트를 읽는/쓰는 동안 인코딩 tooinformation 손실, 실수로 소개 읽을 수 없는 문자의 예를 들어, null, 및 수 또한 영향을 텍스트 구문 분석을 안내 합니다. 신중 하 게 구문 분석 하 고 편집을 적절 한 맞춤 및/또는 구조화 또는 반 구조화 된 텍스트 데이터에서 tooextract 구조화 된 데이터에 대 한 순서 tooclean 텍스트 필드에 필요할 수 있습니다.

**데이터 탐색** hello 데이터에는 초기 보기를 제공 합니다. 다양 한 데이터 문제가 수 대상이 단계를 수행 하 고 해당 메서드 수 적용된 tooaddress 이러한 문제가 발생할 수 있습니다.  것이 중요 한 tooask 질문 hello 문제의 hello 소스 란 무엇이 고 어떻게 hello 문제 수 도입 되었습니다. 또한 수 tooresolve 라인 해당 필요 toobe hello 데이터 처리 단계에서 결정 하는 데 해당 합니다. hello 유형의 insights hello 데이터에서 tooderive 노드가 하나에 사용 되는 tooprioritize hello 데이터 처리 활동 될 수도 있습니다.

## <a name="references"></a>참조
> *데이터 마이닝: 개념 및 기술*, Third Edition, Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber 및 Jian Pei
> 
> 

