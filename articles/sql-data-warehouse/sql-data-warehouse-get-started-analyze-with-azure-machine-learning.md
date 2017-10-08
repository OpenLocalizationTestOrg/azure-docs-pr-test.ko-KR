---
title: "Azure 기계 학습을 사용 하 여 aaaAnalyze 데이터 | Microsoft Docs"
description: "Azure 기계 학습 toobuild 예측 기계 학습 Azure SQL 데이터 웨어하우스에 저장 된 데이터를 기반으로 모델을 사용 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Azure 기계 학습을 사용하여 데이터 분석
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure 기계 학습](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

이 자습서에서는 Azure 기계 학습 toobuild 예측 기계 학습 모델 Azure SQL 데이터 웨어하우스에 저장 된 데이터를 기반으로 사용 합니다. 특히,이 빌드 대상된 마케팅 캠페인 Adventure Works에서는 hello 자전거 매장에 대 한,으로 예측 하는 경우 고객은 가능성이 toobuy 자전거 여부.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>필수 조건
이 자습서를 통해 toostep를 해야합니다.

* AdventureWorksDW 샘플 데이터로 미리 로드된 SQL 데이터 웨어하우스. tooprovision이,이 참조 [SQL 데이터 웨어하우스를 만들] [ Create a SQL Data Warehouse] tooload hello 샘플 데이터를 선택 합니다. 데이터 웨어하우스는 있지만 샘플 데이터가 없는 경우 [샘플 데이터를 수동으로 로드][load sample data manually]할 수 있습니다.

## <a name="1-get-hello-data"></a>1. Hello 데이터 가져오기
hello 데이터는 hello AdventureWorksDW 데이터베이스에서 hello dbo.vTargetMail 보기입니다. tooread이이 데이터:

1. [Azure Machine Learning 스튜디오][Azure Machine Learning studio]에 로그인하고 내 실험을 클릭합니다.
2. **+새로 만들기**를 클릭하고 **빈 실험**을 선택합니다.
3. 실험: 대상 마케팅에 대한 이름을 입력합니다.
4. 끌어서 hello **판독기** hello canvas에 hello 모듈 창에서 모듈입니다.
5. Hello 속성 창에서 SQL 데이터 웨어하우스 데이터베이스의 hello 세부 정보를 지정 합니다.
6. Hello 데이터베이스 지정 **쿼리** 대상 tooread hello 데이터입니다.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

클릭 하 여 hello 실험을 실행 **실행** hello 실험 캔버스에서 합니다.
![Hello 실험을 실행 합니다.][1]

Hello 실험 성공적으로 완료 되 면 hello 판독기 모듈 hello 맨 아래에 hello 출력 포트를 클릭 하 고 선택 **시각화** toosee hello 가져온 데이터입니다.
![가져온 데이터 확인][3]

## <a name="2-clean-hello-data"></a>2. 클린 hello 데이터
tooclean hello 데이터 hello 모델에 대 한 관계 없는 일부 열을 삭제 합니다. toodo이:

1. 끌어서 hello **열 프로젝션** hello 캔버스에는 모듈입니다.
2. 클릭 **열 선택기 시작** hello 속성 창 toospecify toodrop 원하는 열에에서 있습니다.
   ![프로젝트 열][4]
3. 다음 두 열을 제외합니다.
   ![불필요한 열 제거][5]

## <a name="3-build-hello-model"></a>3. Hello 모델 작성
Hello 데이터 80-20 분할 합니다: 80 %tootrain 기계 학습 모델 및 20% tootest hello 모델입니다. 해 드립니다이 이진 분류 문제에 대 한 hello "2 클래스" 알고리즘을 활용 합니다.

1. 끌어서 hello **분할** hello 캔버스에는 모듈입니다.
2. Hello 첫 번째 hello 속성 창에서 출력 데이터 집합의 행 비율을 0.8를 입력 합니다.
   ![훈련 및 테스트 집합으로 데이터 분할][6]
3. 끌어서 hello **2 클래스 승격 된 의사 결정 트리** hello 캔버스에는 모듈입니다.
4. 끌어서 hello **모델 학습** 모듈 hello로 캔버스 및 hello 입력을 지정 합니다. 클릭 **열 선택기 시작** hello 속성 창에서.
   * 첫 번째 입력: ML 알고리즘입니다.
   * 두 번째 입력이:에서 tootrain hello 알고리즘은 데이터입니다.
     ![Hello 모델 학습 모듈에 연결][7]
5. 선택 hello **BikeBuyer** 열 toopredict hello 처럼 열입니다.
   ![열 toopredict 선택][8]

## <a name="4-score-hello-model"></a>4. Hello 모델 점수 매기기
이제 hello 모델 테스트 데이터에서 수행 하는 방법을 테스트 합니다. 에서는 더 잘 수행 하는 다른 알고리즘 toosee와 원하는 hello 알고리즘을 비교 합니다.

1. 끌기 **모델 점수 매기기** hello 캔버스에는 모듈입니다.
    첫 번째 입력이: 두 번째 입력이 모델을 학습: 테스트 데이터 ![hello 모델 점수 매기기][9]
2. 끌어서 hello **2 클래스 Bayes 지점 컴퓨터** hello 실험 캔버스에 있습니다. 이 알고리즘 비교 toohello 2 클래스 승격 된 의사 결정 트리에서에서 수행 하는 방법을 비교 합니다.
3. 복사 및 붙여넣기 hello 모델 학습 및 점수 모델의에서 모듈 hello 캔버스입니다.
4. 끌어서 hello **모델 평가** 모듈 hello 캔버스 toocompare hello 두 알고리즘으로 합니다.
5. **실행** 실험 hello 합니다.
   ![Hello 실험을 실행 합니다.][10]
6. Hello 모델 평가 모듈 hello 맨 아래에 hello 출력 포트를 클릭 하 고 시각화를 클릭 합니다.
   ![평가 결과 시각화][11]

제공 된 hello 메트릭을 hello ROC 곡선을 정밀도 회수 다이어그램 이며 곡선 리프트 합니다. 이러한 메트릭을 볼 hello 두 번째 식 보다 더 잘 수행 hello 첫 번째 모델을 볼 수 있습니다. toolook에 hello 예측 하는 첫 번째 모델링 hello 기능, hello 모델 점수 매기기의 출력 포트를 클릭 하 고 시각화를 클릭 합니다.
![점수 결과 시각화][12]

두 개 이상의 열 tooyour 테스트 데이터 집합을 추가 하는 것이 나타납니다.

* 점수가 매겨진된 확률: hello 가능성 고객이 자전거 구매자 인지 합니다.
* 점수가 매겨진된 레이블: hello 분류 hello 모델 – bike buyer (1)에 의해 수행 여부 (0)입니다. 레이블 지정에 대 한 확률 임계값이 too50% 설정 되어 있으며 조정할 수 있습니다.

Hello 열 hello 점수가 매겨진 레이블 (예측) BikeBuyer (실제)를 비교 hello 모델 수행한 얼마나 잘 확인할 수 있습니다. 다음 단계로이 모델 toomake 예측 신규 고객에 대 한 사용 및이 모델을 웹 서비스로 게시 하거나 결과 백 tooSQL 데이터 웨어하우스 쓰기 수 있습니다.

## <a name="next-steps"></a>다음 단계
toolearn 예측 기계 학습 모델을 작성에 대 한 참조를 너무[소개 tooMachine Azure에서 학습][Introduction tooMachine Learning on Azure]합니다.

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
