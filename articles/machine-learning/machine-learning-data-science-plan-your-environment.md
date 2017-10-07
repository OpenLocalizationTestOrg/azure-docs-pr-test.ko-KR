---
title: "aaaIdentify 시나리오 및 계획 분석 프로세스-Azure | Microsoft Docs"
description: "일련의 주요 질문을 고려한 고급 분석 계획"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Tooidentify 시나리오 및 계획에 대 한 고급 분석 데이터 처리 방법
리소스 하면 경우에 계획 해야 tooinclude 환경 toodo 설정 고급 분석 데이터 집합에 대 한 처리? 이 문서는 일련의 질문 tooask hello 작업 및 관련 리소스를 식별 하는 데 도움이 되는 시나리오를 제안 합니다. predictive analytics에 대해 상위 수준 단계 순서 hello로 둘러싸여 [hello 팀 데이터 과학 프로세스 (TDSP) 이란?](data-science-process-overview.md)합니다. 이러한 각 단계 hello 작업 관련 tooyour 특정 시나리오에 대 한 특정 리소스를 걸립니다. 주요 질문 tooidentify 사용자 시나리오 별로 중요 데이터 물류, 특성, hello 데이터 집합 및 hello 도구와 toodo hello 분석을 원하는 언어의 hello 품질 hello 합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>로지스틱 질문: 데이터 위치 및 이동
hello 로지스틱 질문 관련 hello의 hello 위치 **데이터 소스**, hello **목표 대상** Azure 및 hello 데이터 이동에 대 한 요구 사항에서 비롯 한 hello 일정, amount 및 리소스 에 관련 되었습니다. hello 데이터 toobe hello 분석 프로세스 중 여러 번 이동 해야 합니다. 일반적인 시나리오는 Azure에 있는 저장소의 일종으로 변환한 다음 다시 기계 학습 스튜디오로 toomove 로컬 데이터입니다.

1. **데이터 원본은 무엇인가요?** 로컬 또는 클라우드 hello 입니까? 예:
   
   * hello 데이터는 HTTP 주소에서 공개적으로 사용할 수 있습니다.
   * hello 데이터 로컬/네트워크 파일 위치에 저장 됩니다.
   * hello 데이터는 SQL Server 데이터베이스입니다.
   * hello 데이터는 Azure 저장소 컨테이너에 저장
2. **Hello Azure 대상 이란?** 처리 또는 모델링을 위해 여기서 toobe 해야 합니까? 예:
   
   * 데이터 이동
   * SQL Azure 데이터베이스
   * Azure VM에서 SQL Server
   * HDInsight(Azure의 Hadoop) 또는 하이브 테이블
   * Azure 기계 학습
   * 탑재식 Azure 가상 하드 디스크
3. **Toomove hello 데이터 어떻게 예정 입니까?**  hello 절차와 리소스 사용 가능한 tooingest 또는 로드 데이터를 다양 한 다른 저장소와 처리 환경 hello 다음 항목에에서 설명 되어 있습니다.
   
   * [분석용 저장소 환경에 데이터 로드](machine-learning-data-science-ingest-data.md)
   * [다양한 데이터 원본에서 Azure Machine Learning Studio로 학습 데이터를 가져옵니다](machine-learning-data-science-import-data.md).
4. **Hello 데이터 toobe 정기적으로 이동 하거나 마이그레이션하는 동안 수정에 필요 합니까?** 하이브리드 시나리오 온-프레미스에 액세스 하 고 클라우드 리소스와 관련 되어 또는 hello 데이터의 트랜잭션 처리 또는 toobe 수정 해야 하거나 비즈니스 논리가 있는 경우에 특히 패키지가 마이그레이션되면 데이터 요구 toobe 지속적으로 Azure 데이터 팩터리 ADF ()를 사용 하는 것이 좋습니다. 마이그레이션 중인 hello 과정에서 tooit를 추가 합니다. 자세한 내용은 참조 하세요. [온-프레미스 SQL server tooSQL Azure 데이터 팩터리를 사용 하 여 Azure에서에서 데이터 이동](machine-learning-data-science-move-sql-azure-adf.md)
5. **Hello 데이터의 양을 이동 toobe tooAzure?** 매우 큰 데이터 집합의 특정 환경 hello 저장소 용량을 초과할 수 있습니다. 예를 들어 hello 다음 섹션에는 기계 학습 스튜디오에 대 한 크기 제한에 대 한 hello 설명은 참조 하세요. 이러한 경우 hello 데이터의 샘플 hello 분석 중 사용할 수 있습니다. 어떻게 toodown 샘플 데이터 집합의 다양 한 Azure 환경에서 세부 정보를 참조 하십시오. [hello 팀 데이터 과학 프로세스에에서 대 한 데이터 샘플](machine-learning-data-science-sample-data.md)합니다.

## <a name="data-characteristics-questions-type-format-and-size"></a>데이터 특성 질문: 유형, 형식, 크기
이러한 질문은 키 tooplanning 저장소 및 데이터 형식과 몇 가지 제한 사항이 적절 한 toovarious 사용 되는 환경의 처리 합니다.

1. **Hello 데이터 유형은 무엇 인가요?** 예:
   
   * 숫자
   * 범주
   * 문자열
   * 이진
2. **데이터 형식이 어떻습니까?** 예:
   
   * 쉼표로 구분되거나(CSV) 탭으로 구분된(TSV) 플랫 파일
   * 압축되거나 압축되지 않은
   * Azure Blob
   * Hadoop 하이브 테이블
   * SQL Server 테이블
3. **데이터가 얼마나 큽니까?**
   
   * 작음: 2GB 미만
   * 보통: 2GB보다 크고 10GB보다 작음
   * 큼: 10GB 초과

Hello Azure 기계 학습 스튜디오 환경을 예로 들어 보겠습니다.

* Hello 데이터 형식 및 Azure 기계 학습 스튜디오에서 지원 되는 형식 목록에 대 한 참조 [데이터 형식과 지원 되는 데이터 형식](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) 섹션.
* Azure 기계 학습 스튜디오의 데이터 제한에 대 한 자세한 내용은 참조 hello **향 될 수 있습니다 hello 데이터 집합 내 모듈에 대 한?** 의 섹션 [가져오기 및 기계 학습에 대 한 데이터 내보내기](machine-learning-faq.md#machine-learning-studio-questions)

Hello 분석 프로세스에서 사용 되는 다른 Azure 서비스의 hello 제한 사항에 대 한 자세한 내용은 참조 하십시오. [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)합니다.

## <a name="data-quality-questions-exploration-and-pre-processing"></a>데이터 품질 질문: 탐색 및 전처리
1. **데이터에 대해 무엇을 알고 있나요?** 기본적인 특성도 toogain는 이해 해야 하는 경우 데이터를 탐색 합니다. 표시되는 패턴 또는 추세, 포함된 이상값 또는 값의 개수가 필요합니다. 이 단계는 필요한 hello 가장 적절 한 기능을 제안 하거나 분석의 입력 수 있는 가설을 작성 하는 작업에 대 한 추가 데이터 수집에 대 한 계획을 세울 전처리 hello 범위를 결정 하기 위한 중요 합니다. 기술 통계 계산 및 시각화 표현은 데이터 검사에 유용한 기법입니다. 어떻게 tooexplore 다양 한 Azure 환경에서 데이터 집합 참조에 대 한 자세한 내용은 [hello 팀 데이터 과학 프로세스에서에서 데이터를 탐색](machine-learning-data-science-explore-data.md)합니다.
2. **전처리 또는 정리 hello 데이터 필요 합니까?**
   데이터 전처리 및 정리는 일반적으로 기계 학습에 데이터 집합을 효과적으로 사용할 수 있기 전에 수행해야 하는 중요한 작업입니다. 원시 데이터는 노이즈가 많고, 불안정하고, 값이 누락된 경우가 종종 있습니다. 이러한 데이터를 모델링에 사용하면 결과가 잘못될 수 있습니다. 에 대 한 참조 [작업에 대 한 향상 된 기계 학습 tooprepare 데이터](machine-learning-data-science-prepare-data.md)합니다.

## <a name="tools-and-languages-questions"></a>도구 및 언어 질문
필요하거나 사용하기에 가장 편리한 언어 및 개발 환경 또는 도구에 따라서 많은 옵션이 있습니다.

1. **언어 하 신 분석용 toouse 선호?**  
   
   * R
   * Python
   * SQL
2. **데이터 분석에 사용해야 하는 도구는 무엇인가요?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -스크립트 언어 tooadminister Azure 리소스 언어에서 사용 되는 스크립트입니다.
   * [Azure 기계 학습 스튜디오](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools for Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Jupyter 노트북](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>고급 분석 시나리오 파악
Hello 이전 단원의 hello 질문에 답변 하는 한 시나리오를 모범 여 상황에 맞는 준비 toodetermine 됩니다. hello 샘플 시나리오에 설명 된 [Azure 기계 학습에서 고급 분석에 대 한 시나리오](machine-learning-data-science-plan-sample-scenarios.md)합니다.

