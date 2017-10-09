---
title: "SQL 데이터 웨어하우스에 Azure 기계 학습 aaaUse | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용
Azure 기계 학습 SQL 데이터 웨어하우스의 데이터에 대해 toocreate 예측 모델을 사용할 수 있으며 다음 준비를 사용 하는 웹 서비스로 게시 하는 완전히 관리 되는 예측 분석 서비스입니다. 예측 분석의 hello 기본 사항 학습 하 고 기계 학습을 읽어 [소개 tooMachine Azure에서 학습][Introduction tooMachine Learning on Azure]합니다.  방법 toocreate, 학습, 점수 및 hello를 사용 하 여 기계 학습 모델을 테스트 한 다음 알아보십시오 [만들기 실험 자습서][Create experiment tutorial]합니다.

이 문서에서는 살펴보겠습니다 어떻게 hello를 사용 하 여 다음 toodo hello [Azure 기계 학습 스튜디오][Azure Machine Learning Studio]:

* 데이터베이스 toocreate에서 데이터 읽기, 학습 및 예측 모델 점수를 매깁니다.
* 데이터 tooyour 데이터베이스 쓰기

## <a name="read-data-from-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 데이터 읽기
우리는 hello AdventureWorksDW 데이터베이스의 Product 테이블에서 데이터를 읽습니다.

### <a name="step-1"></a>1단계
클릭 하 여 새 실험 시작 + hello hello 기계 학습 스튜디오 창 맨 아래에 새 실험을 선택한 다음 빈 실험을 선택 합니다. 선택 hello 기본 hello hello 캔버스 맨 위에 있는 이름 실험을 toosomething 의미 있는 예를 들어 자전거 가격 예측 합니다.

### <a name="step-2"></a>2단계
데이터 집합의 hello 팔레트에 hello 판독기 모듈 및 모듈 hello 실험 캔버스의 왼쪽 hello 찾습니다. Hello 모듈 toohello 실험 캔버스를 끕니다.
![][drag_reader]

### <a name="step-3"></a>3단계
Hello 판독기 모듈을 선택 하 고 hello 속성 창 입력 합니다.

1. Hello 데이터 원본으로 Azure SQL 데이터베이스를 선택 합니다.
2. 데이터베이스 서버 이름: 종류 hello 서버 이름입니다. Hello를 사용할 수 있습니다 [Azure 포털] [ Azure portal] toofind이 있습니다.

![][server_name]

1. 데이터베이스 이름: 방금 지정한 hello 서버에 있는 데이터베이스의 형식 hello 이름입니다.
2. 서버 사용자 계정 이름: hello hello 데이터베이스에 대 한 액세스 권한이 있는 계정의 사용자 이름을 입력 합니다.
3. 서버 사용자 계정 암호: 제공 hello에 대 한 hello 암호가 사용자 계정을 지정 합니다.
4. 모든 서버 인증서 수락: tooskip 데이터를 읽기 전에 먼저 hello 사이트 인증서를 검토 하려는 경우이 옵션 (보안 수준 낮음)을 사용 합니다.
5. 쿼리 만들기: tooread 원하는 hello 데이터를 설명 하는 SQL 문을 입력 합니다. 이 경우 다음 쿼리는 hello를 사용 하 여 Product 테이블에서 데이터를 읽이 됩니다.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>4단계
1. Hello 실험 캔버스에서 실행을 클릭 하 여 hello 실험을 실행 합니다.
2. Hello 실험 완료 되 면 hello 판독기 모듈 성공적으로 완료 된 녹색 확인 표시가 tooindicate를 갖습니다. 또한 hello 오른쪽 위 모서리에서 실행 중 상태로 마침 hello를 확인 합니다.

![][run]

1. toosee 가져온된 데이터 hello hello 아래쪽 hello 자동차 데이터 집합의 출력 포트 hello 누르고 시각화를 선택 합니다.

## <a name="create-train-and-score-a-model"></a>모델 만들기, 훈련 및 점수 매기기
이제 이 데이터 집합을 사용하여 다음을 수행할 수 있습니다.

* 모델 만들기: 데이터 처리 및 기능 정의
* Hello 모델 학습: 선택 하 고 학습 알고리즘을 적용
* 점수 및 테스트 hello 모델: 새 자전거 가격 예측

![][model]

toolearn 방법 toocreate, 학습, 점수 및 기계 학습 모델 사용 하 여 hello를 테스트 하는 방법에 대 한 자세한 [만들기 실험 자습서][Create experiment tutorial]합니다.

## <a name="write-data-tooazure-sql-data-warehouse"></a>데이터 tooAzure SQL 데이터 웨어하우스 쓰기
Hello 결과 집합 tooProductPriceForecast 테이블 hello AdventureWorksDW 데이터베이스에 작성 하 합니다.

### <a name="step-1"></a>1단계
데이터 집합의 hello 팔레트에 hello 기록기 모듈 및 모듈 hello 실험 캔버스의 왼쪽 hello 찾습니다. Hello 모듈 toohello 실험 캔버스를 끕니다.

![][drag_writer]

### <a name="step-2"></a>2단계
Hello 기록기 모듈을 선택 하 고 hello 속성 창 입력 합니다.

1. Hello 데이터 대상으로 Azure SQL 데이터베이스를 선택 합니다.
2. 데이터베이스 서버 이름: 종류 hello 서버 이름입니다. Hello를 사용할 수 있습니다 [Azure 포털] [ Azure portal] toofind이 있습니다.
3. 데이터베이스 이름: 방금 지정한 hello 서버에 있는 데이터베이스의 형식 hello 이름입니다.
4. 서버 사용자 계정 이름: hello hello 데이터베이스에 대 한 쓰기 권한이 있는 계정의 사용자 이름을 입력 합니다.
5. 서버 사용자 계정 암호: 제공 hello에 대 한 hello 암호가 사용자 계정을 지정 합니다.
6. (안전 하지 않음) 모든 서버 인증서 수락: tooview hello 인증서를 표시 하지 않으려는 경우이 옵션을 선택 합니다.
7. 쉼표로 구분 된 목록이 저장 열 toobe: toooutput 원하는 hello 데이터 집합 또는 결과 열 목록을 제공 합니다.
8. 데이터 테이블 이름: hello 데이터 테이블의 hello 이름을 지정 합니다.
9. Datatable 열의 쉼표로 구분 된 목록: hello 새 테이블에 열 이름을 toouse hello를 지정 합니다. hello 열 이름은 다를 수 있습니다 hello 원본 데이터 집합에 hello 것 이지만 나열 해야 hello 출력 테이블에 대 한 정의 하는 동일한 수의 열을 여기 hello 합니다.
10. SQL Azure 작업당 작성 된 행 수: hello tooa SQL 데이터베이스를 한 번에 작성 된 행 수를 구성할 수 있습니다.

![][writer_properties]

### <a name="step-3"></a>3단계
1. Hello 실험 캔버스에서 실행을 클릭 하 여 hello 실험을 실행 합니다.
2. Hello 실험 완료 되 면 모든 모듈은 성공적으로 완료 된 녹색 확인 표시가 tooindicate를 갖습니다.

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
