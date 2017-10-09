---
title: "Azure 기계 학습 웹 서비스에서 가져오기/내보내기 데이터 aaaUsing | Microsoft Docs"
description: "Toouse 데이터 가져오기 및 내보내기 데이터 모듈 toosend hello 하 고 웹 서비스에서 데이터를 수신 하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>데이터 가져오기 및 데이터 내보내기 모듈을 사용하는 Azure ML 웹 서비스 배포

예측 실험을 만들 때 일반적으로 웹 서비스 입력 및 출력을 추가합니다. Hello 실험을 배포 하면 소비자가 보내고 hello 입 / 출력을 통해 hello 웹 서비스에서 데이터를 받을 수 있습니다. 일부 응용 프로그램에서는 소비자 데이터를 데이터 피드에서 사용할 수 있거나 해당 데이터가 Azure Blob 저장소와 같은 외부 데이터 원본에 이미 있을 수 있습니다. 이러한 경우 웹 서비스 입력 및 출력을 사용하여 데이터를 읽고 쓸 필요가 없습니다. 수, 대신 hello 일괄 처리 실행 서비스 (BES) tooread 데이터 데이터 가져오기 모듈을 사용 하 여 hello 데이터 소스에서 사용 하 고 결과 데이터 내보내기 모듈을 사용 하 여 tooa 다른 데이터 위치 점수 매기기 hello.

hello 데이터 가져오기 및 내보내기 데이터 모듈에서 읽고 쓸 수는 온-프레미스 SQL 데이터베이스 또는 toovarious 데이터는 HTTP, Hive 쿼리, Azure SQL 데이터베이스, Azure 테이블 저장소, Azure Blob 저장소, 데이터 피드를 통해 웹 URL 등의 위치를 제공 합니다.

이 항목에서는 hello "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합" 샘플링 하 고 hello 데이터 집합 censusdata 라는 Azure SQL 테이블에 이미 로드 된 것으로 가정 합니다.

## <a name="create-hello-training-experiment"></a>Hello 학습 실험 만들기
Hello를 열 때 "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합" 사용 하 여 hello 샘플 성인 인구 조사 소득 이진 분류 데이터 집합을 샘플링 합니다. 및 hello 캔버스의 hello 실험 비슷한 toohello 다음 이미지에 표시 됩니다.

![Hello 실험의 초기 구성입니다.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

tooread hello Azure SQL 테이블에서 데이터를 hello:

1. Hello dataset 모듈을 삭제 합니다.
2. Hello 구성 요소 검색 상자에 가져오기 '를 입력 합니다.
3. Hello 결과 목록에서 추가 된 *데이터 가져오기* 모듈 toohello 실험 캔버스입니다.
4. Hello 출력에 연결 *데이터 가져오기* hello의 모듈 hello 입력 *누락 데이터 정리* 모듈입니다.
5. 속성 창에서 선택 **Azure SQL 데이터베이스** hello에 **데이터 원본** 드롭다운입니다.
6. Hello에 **데이터베이스 서버 이름**, **데이터베이스 이름**, **사용자 이름**, 및 **암호** 필드 hello에 대 한 적절 한 정보 입력 데이터베이스입니다.
7. 다음 쿼리에서 hello hello 데이터베이스 쿼리 필드에 입력 합니다.
   
     select [age],
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     from dbo.censusdata;
8. Hello 실험 캔버스의 hello 아래쪽 클릭 **실행**합니다.

## <a name="create-hello-predictive-experiment"></a>Hello 예측 실험 만들기
그런 다음 웹 서비스를 배포 하는 hello 예측 실험을 설정할 수도 있습니다.

1. Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **예측 웹 서비스 [권장]**합니다.
2. Hello 제거 *웹 서비스 입력* 및 *웹 서비스 출력 모듈* hello 예측 실험에서 합니다. 
3. Hello 구성 요소 검색 상자에 내보내기를 입력 합니다.
4. Hello 결과 목록에서 추가 된 *데이터 내보내기* 모듈 toohello 실험 캔버스입니다.
5. Hello 출력에 연결 *모델 점수 매기기* hello의 모듈 hello 입력 *데이터 내보내기* 모듈입니다. 
6. 속성 창에서 선택 **Azure SQL 데이터베이스** hello 데이터 대상 드롭다운에서 합니다.
7. Hello에 **데이터베이스 서버 이름**, **데이터베이스 이름**, **서버 사용자 계정 이름**, 및 **서버 사용자 계정 암호** 필드 입력 hello 데이터베이스에 대 한 적절 한 정보입니다.
8. Hello에 **쉼표로 구분한 목록입니다. 저장 하는 열 toobe** 필드 점수가 매겨진 레이블을 입력 합니다.
9. Hello에 **데이터 테이블 이름 필드**, dbo를 입력 합니다. ScoredLabels 합니다. Hello 테이블이 존재 하지 않는 경우 실행 되는 hello 실험 또는 hello 웹 서비스를 호출할 때 생성 됩니다.
10. Hello에 **쉼표로 구분 된 데이터 테이블 열 목록** 필드 ScoredLabels를 입력 합니다.

Hello 최종 웹 서비스를 호출 하는 응용 프로그램을 작성, 할 수 있습니다 toospecify 다른 입력된 쿼리 또는 대상 테이블에서 런타임에 합니다. tooconfigure 이러한 입력 및 출력을 사용 하 여 hello 웹 서비스 매개 변수 기능 tooset hello *데이터 가져오기* 모듈 *데이터 소스* 속성과 hello *데이터 내보내기* 모드 데이터 대상 속성입니다.  웹 서비스 매개 변수에 대 한 자세한 내용은 참조 hello [AzureML 웹 서비스 매개 변수 항목](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) hello Cortana 인텔리전스 및 기계 학습 블로그.

tooconfigure hello hello 가져오기 쿼리 및 hello 대상 테이블에 대 한 웹 서비스 매개 변수:

1. Hello에 대 한 hello 속성 창에서 *데이터 가져오기* 모듈을 hello에 hello 아이콘을 클릭 hello의 오른쪽 위에 **데이터베이스 쿼리** 필드 및 선택 **웹 서비스 매개 변수로 설정할**합니다.
2. Hello에 대 한 hello 속성 창에서 *데이터 내보내기* 모듈을 hello에 hello 아이콘을 클릭 hello의 오른쪽 위에 **데이터 테이블 이름** 필드 및 선택 **웹 서비스 매개 변수로 설정할**합니다.
3. Hello hello 맨 아래에 *데이터 내보내기* 모듈 속성 창의 hello **웹 서비스 매개 변수가** 섹션 데이터베이스 쿼리를 클릭 하 고 쿼리 이름을 바꿉니다.
4. **데이터 테이블 이름**을 클릭하고 이름을 **테이블**로 바꿉니다.

완료 되 면 다음 이미지와 비슷한 toohello 실험 같아야 합니다.

![실험의 최종 모습입니다.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

이제 hello 실험을 웹 서비스로 배포할 수 있습니다.

## <a name="deploy-hello-web-service"></a>Hello 웹 서비스를 배포 합니다.
Tooeither 클래식 또는 새 웹 서비스를 배포할 수 있습니다.

### <a name="deploy-a-classic-web-service"></a>기존 웹 서비스 배포
클래식 웹 서비스로 toodeploy 응용 프로그램 tooconsume를 만들고 해당:

1. Hello 실험 캔버스의 hello 맨 아래에 실행을 클릭 합니다.
2. Hello 실행이 완료 되 면 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]**합니다.
3. Hello 웹 서비스 대시보드에서 API 키를 찾습니다. 복사한 toouse 나중 저장 합니다.
4. Hello에 **기본 끝점** 테이블에서 hello **일괄 처리 실행** 링크 tooopen hello API 도움말 페이지입니다.
5. Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.
6. Hello API 도움말 페이지를 찾을 hello **샘플 코드** hello hello 페이지 맨 아래에 섹션입니다.
7. 복사 하 여 Program.cs 파일에 hello C# 예제 코드를 붙여 넣고 모든 toohello blob 저장소 참조를 제거 합니다.
8. Hello에 hello 값을 업데이트 *apiKey* 이전에 저장 하는 hello API 키가 있는 변수입니다.
9. Toohello 전달 되는 웹 서비스 매개 변수 hello 요청 선언과 업데이트 hello 값을 찾을 *데이터 가져오기* 및 *데이터 내보내기* 모듈입니다. 이 경우 hello 원래 쿼리를 사용 하지만 새 테이블 이름을 정의 합니다.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Hello 응용 프로그램을 실행 합니다. 

Hello 실행 완료 되 면 새 테이블 hello 평가 결과 포함 하는 toohello 데이터베이스를 추가 됩니다.

### <a name="deploy-a-new-web-service"></a>새 웹 서비스 배포

> [!NOTE] 
> toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다. 자세한 내용은 참조 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

새 웹 서비스로 toodeploy 응용 프로그램 tooconsume를 만들고 해당:

1. Hello 실험 캔버스의 hello 아래쪽 클릭 **실행**합니다.
2. Hello 실행이 완료 되 면 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [New]**합니다.
3. Hello 실험 배포 페이지에서 웹 서비스에 대 한 이름을 입력 하 고 가격 계획을 선택한 다음 클릭 **배포**합니다.
4. Hello에 **퀵 스타트** 페이지 **사용**합니다.
5. Hello에 **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.
6. Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.
7. 복사 하 여 Program.cs 파일에 hello C# 예제 코드를 붙여 넣습니다.
8. Hello에 hello 값을 업데이트 *apiKey* hello로 변수 **기본 키** hello에 **기본 소비 정보** 섹션.
9. Hello 찾을 *scoreRequest* toohello 전달 되는 웹 서비스 매개 변수 선언 및 업데이트 hello 값 *데이터 가져오기* 및 *데이터 내보내기* 모듈입니다. 이 경우 hello 원래 쿼리를 사용 하지만 새 테이블 이름을 정의 합니다.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Hello 응용 프로그램을 실행 합니다. 

