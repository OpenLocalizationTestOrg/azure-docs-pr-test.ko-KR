---
title: "기계 학습 스튜디오로 aaaImport 데이터 | Microsoft Docs"
description: "어떻게 tooimport 다양 한 데이터 원본에서 Azure 기계 학습 스튜디오에 데이터입니다. 지원되는 데이터 형식에 대해 알아봅니다."
keywords: "데이터 가져오기, 데이터 형식, 데이터 유형, 데이터 원본, 학습 데이터"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>다양한 데이터 원본에서 Azure 기계 학습 스튜디오로 학습 데이터를 가져오기
toouse 기계 학습 스튜디오 toodevelop 및 학습 예측 분석 솔루션에서 사용자 고유의 데이터를 할 수 있습니다. 

* 데이터 업로드는 **로컬 파일** 보다 빠른 시간 하드 드라이브 toocreate에서 작업 영역에서 데이터 집합 모듈
* 여러 가지 방법 중 하나에서 데이터에 액세스 **온라인 데이터 원본** 실험 hello를 사용 하 여 실행 되는 동안 [데이터 가져오기] [ import-data] 모듈 
* **데이터 집합**으로 저장된 또 다른 Azure 기계 학습 실험에서 나온 데이터를 사용합니다.
* 온-프레미스 **SQL Server 데이터베이스**에서 데이터 사용합니다.

이러한 각 옵션은 hello 메뉴 아래에서 hello 항목 중 하나에 설명 되어 있습니다. 이 항목 tooimport 데이터를 이러한 다양 한 데이터에서에서 기계 학습 스튜디오에서 toouse 원본 하는 방법을 보여 줍니다. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> 기계 학습 스튜디오에는 학습 데이터로 사용할 수 있는 샘플 데이터 집합이 많이 있습니다. 이러한 이벤트 정보를 참조 하십시오. [hello 샘플 데이터 집합을 사용 하 여 Azure 기계 학습 스튜디오에서](machine-learning-use-sample-datasets.md)).
> 
> 

이 소개 항목은도 tooget 데이터 준비에 대 한 기계 학습 스튜디오에서 사용 하는 방법을 설명 하 고 있는 데이터 형식 및 데이터 형식을 지원 설명 합니다. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오에서 사용할 준비가 완료된 데이터 가져오기
기계 학습 스튜디오는 디자인 된 toowork 구분 또는 경우에 일부 환경에서 사각형이 아닌 데이터를 사용할 수 있습니다는 데이터베이스에서 데이터를 구조화 된 텍스트 데이터와 같은 사각형 또는 테이블 형식 데이터를 사용 합니다.

데이터가 비교적 정리되어 있는 것이 좋습니다. 즉, 실험에 hello 데이터를 업로드 하기 전에 따옴표가 없는 문자열 등의 문제 care of tootake를 좋습니다.

그러나 기계 학습 스튜디오에는 실험에서 데이터를 조작할 수 있는 모듈도 있습니다. 따라 hello 기계 학습 알고리즘을 사용 하 게을 할 수 있습니다 toodecide 어떻게 스파스 데이터 누락 값 등의 데이터 구조적 문제를 처리 되며 하에 도움이 될 수 있는 모듈입니다. 찾는 위치 hello **데이터 변환** 이러한 기능을 수행 하는 모듈에 대 한 hello 모듈 색상표의 섹션입니다.

어느 시점 실험에서 보거나 수 hello 출력 포트를 클릭 하 여 모듈에 의해 생성 되는 hello 데이터를 다운로드 합니다. Hello 모듈에 따라 서로 다른 다운로드 옵션을 사용할 수 있거나 기계 학습 스튜디오에서 웹 브라우저에서 수 toovisualize hello 데이터를 수 있습니다.

## <a name="data-formats-and-data-types-supported"></a>지원되는 데이터 형식 및 데이터 유형
실험으로 데이터 형식의 수를 가져올 수 있습니다, tooimport 데이터와에서 가져온 사용 방식에 따라:

* 일반 텍스트(.txt)
* 헤더가 있거나(.csv) 없는(.nh.csv) 쉼표로 구분된 값(CSV)
* 헤더가 있거나(.tsv) 없는(.nh.tsv) 탭으로 구분된 값(TSV)
* Excel 파일
* Azure 테이블
* Hive 테이블
* SQL 데이터베이스 테이블
* OData 값
* SVMLight 데이터 (.svmlight) (hello 참조 [SVMLight 정의](http://svmlight.joachims.org/) 형식 정보에 대 한)
* 특성 관계 파일 형식 (ARFF) 데이터 (.arff) (hello 참조 [ARFF 정의](http://weka.wikispaces.com/ARFF) 형식 정보에 대 한)
* Zip 파일(.zip)
* R 개체 또는 작업 영역 파일(. RData)

ARFF 메타 데이터를 포함 하는 같은 형식으로 데이터를에서 가져오는 경우 기계 학습 스튜디오가 메타 데이터 toodefine hello 제목 및 각 열의 데이터 형식을 사용 합니다.

등이 메타 데이터가 포함 되지 않은 TSV 또는 CSV 형식의 데이터를 가져오는 경우 기계 학습 스튜디오에서는 hello 데이터를 샘플링 하 여 hello 각 열의 데이터 형식을 유추 합니다. Hello 데이터도 없는 경우 열 머리글, 기계 학습 스튜디오에 기본 이름을 제공 합니다.

명시적으로 지정 하거나 hello를 사용 하 여 열에 대 한 hello 머리글 및 데이터 형식을 변경할 수 있습니다 [메타 데이터 편집][edit-metadata]합니다.

hello 다음 **데이터 형식** 기계 학습 스튜디오에 의해 인식 됩니다.

* 문자열
* Integer
* double
* Boolean
* DateTime
* TimeSpan

기계 학습 스튜디오에 호출 하는 내부 데이터 형식을 사용 하 여 ***데이터 테이블*** 모듈 간에 toopass 데이터입니다. Hello를 사용 하 여 데이터 테이블 형식으로 데이터를 명시적으로 변환할 수 있습니다 [tooDataset 변환] [ convert-to-dataset] 모듈입니다.

데이터 테이블 이외의 다른 형식을 허용 하는 모든 모듈은 toohello 다음 모듈로 전달 하기 전에 hello 데이터 tooData 테이블 작업을 자동으로 변환 됩니다.

필요한 경우 다른 변환 모듈을 사용하여 데이터 테이블 형식을 다시 CSV, TSV, ARFF 또는 SVMLight 형식으로 변환할 수 있습니다.
찾는 위치 hello **데이터 형식 변환** 이러한 기능을 수행 하는 모듈에 대 한 hello 모듈 색상표의 섹션입니다.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
