---
title: "스트림 분석 및 기계 학습 통합 aaaAzure | Microsoft Docs"
description: "어떻게 toouse 사용자 정의 함수 및 스트림 분석 작업에 대 한 기계 학습"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Azure Stream Analytics 및 Azure Machine Learning을 사용한 감정 분석 수행
이 문서에서는 tooquickly Azure 기계 학습을 통합 하는 간단한 Azure 스트림 분석 작업을 설정 하는 방법에 대해 설명 합니다. Hello Cortana Intelligence 갤러리 tooanalyze 스트리밍 텍스트 데이터에서에서 기계 학습 감성 분석 모델을 사용 하 고이 정보를 실시간으로 hello 감성 점수를 결정 합니다. Hello Cortana Intelligence Suite를 사용 하 여 hello 복잡 한 감성 분석 모델을 작성 하는 방법에 대 한 걱정 없이이 작업을 수행할 수 있습니다.

이 문서 tooscenarios 이러한에서 배운 적용할 수 있습니다.

* 스트리밍 Twitter 데이터에 대한 실시간 감정 분석
* 지원 담당자와 고객 채팅 레코드 분석
* 포럼, 블로그 및 동영상에 대한 의견 평가 
* 기타 실시간 예측 점수 매기기 시나리오

실제 시나리오에서는 Twitter 데이터 스트림에서 직접 hello 데이터 얻게 됩니다. toosimplify hello 자습서 작성 했습니다 것 수 있도록 hello 스트리밍 분석 작업을 트 윗 Azure Blob 저장소에서 CSV 파일에서 합니다. 사용자 고유의 CSV 파일을 만들 수 있습니다 또는 hello 다음 이미지에에서 표시 된 대로 샘플 CSV 파일을 사용할 수 있습니다.

![CSV 파일에서 샘플 트윗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

hello blob 저장소에서 hello 샘플 텍스트 데이터에 대해 사용자 정의 함수 (UDF)으로 hello 감성 분석 모델을 적용 하는 만드는 hello 스트리밍 분석 작업 합니다. hello 출력 (hello 감성 분석 결과 hello)은 toohello를 기록 하는 다른 CSV 파일에서 동일한 blob 저장소입니다. 

hello 다음 그림에서는이 구성을 언급한 대로 좀 더 현실적인 시나리오에서는 Blob Storage를 Azure Event Hubs 입력의 스트리밍 Twitter 데이터로 바꿀 수 있습니다. 또한 작성할 수 있습니다는 [Microsoft Power BI](https://powerbi.microsoft.com/) hello 집계 감성의 실시간으로 시각화 합니다.    

![Stream Analytics Machine Learning 통합 개요](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>필수 조건
시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.

* 활성 Azure 구독.
* 데이터가 포함된 CSV 파일. 앞에서 살펴본 hello 파일을 다운로드할 수 있습니다 [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), 하거나 사용자 고유의 파일을 만들 수 있습니다. 이 문서에 대 한 GitHub에서 hello 파일을 사용 하는 가정 합니다.

상위 수준에서이 문서에서는 표시 되는 toocomplete hello 작업 하면 수행 hello 다음:

1. Azure 저장소 계정 및 blob 저장소 컨테이너를 만들고 CSV 형식의 입력된 파일이 toohello 컨테이너를 업로드 합니다.
3. Hello Cortana Intelligence 갤러리 tooyour Azure 기계 학습 작업 영역에서 감성 분석 모델을 추가 하 고 hello 기계 학습 작업 영역에서 웹 서비스로이 모델을 배포 합니다.
5. Hello 텍스트 입력에 대 한 순서 toodetermine 감성에서 함수로이 웹 서비스를 호출 하는 스트림 분석 작업을 만듭니다.
6. Hello 스트림 분석 작업을 시작 하 고 hello 출력을 확인 합니다.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>저장소 컨테이너를 만들고 hello CSV 입력된 파일을 업로드
이 단계에 대 한 hello GitHub에서 사용할 수 있는 등의 모든 CSV 파일을 사용할 수 있습니다.

1. Hello Azure 포털에서에서 클릭 **새로** &gt; **저장소** &gt; **저장소 계정**합니다.

   ![새 저장소 계정 만들기](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. 이름을 제공 (`samldemo` hello 예제에서). hello 이름은 소문자 및 숫자를 사용할 수 및 Azure 전체에서 고유 해야 합니다. 

3. 기존 리소스 그룹을 지정하고 위치를 지정합니다. 위치에 대 한 모든 hello 리소스 사용이 자습서에서 만든 동일한을 hello 권장 위치입니다.

    ![저장소 계정 세부 정보 입력](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. Hello Azure 포털에서에서 hello 저장소 계정을 선택 합니다. 저장소 계정 블레이드에서 hello 클릭 **컨테이너** 클릭 하 고  **+ &nbsp;컨테이너** toocreate blob 저장소입니다.

    ![Blob 컨테이너 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Hello 컨테이너에 대 한 이름을 제공 (`azuresamldemoblob` hello 예제에서) 되어 있는지 확인 하 고 **액세스 형식** 너무 설정**Blob**합니다. 완료되면 **확인**을 클릭합니다.

    ![Blob 컨테이너 정보 지정](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. Hello에 **컨테이너** 블레이드, 선택 hello 새 컨테이너는 해당 컨테이너에 대 한 hello 블레이드가 열립니다.

7. **업로드**를 클릭합니다.

    ![컨테이너의 '업로드' 단추](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. Hello에 **업로드 blob** 블레이드에서이 자습서에 대 한 toouse 되도록 hello CSV 파일을 지정 합니다. 에 대 한 **Blob 유형**선택, **블록 blob** 및 집합 hello 블록 too4 MB 하기이 자습서에 충분 한 크기 조정 합니다.

    ![Blob 파일 업로드](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Hello 클릭 **업로드** hello hello 블레이드 맨 아래에 단추입니다.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Hello Cortana 인텔리전스 갤러리에서에서 hello 감성 분석 모델을 추가 합니다.

이제 hello 샘플 데이터는 blob에 Cortana 인텔리전스 갤러리에서 hello 감성 분석 모델을 사용할 수 있습니다.

1. Toohello 이동 [예측 감성 분석 모델](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) hello Cortana 인텔리전스 갤러리의에서 페이지입니다.  

2. **Studio에서 열기**를 클릭합니다.  
   
   ![Stream Analytics Machine Learning, Machine Learning 스튜디오 열기](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Toogo toohello 작업 영역에 로그인 합니다. 위치를 선택합니다.

4. 클릭 **실행** hello hello 페이지 맨 아래에 있습니다. 약 1 분이 걸립니다 hello 프로세스가 실행 됩니다.

   ![Machine Learning Studio에서 실험 실행](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Hello 프로세스가 성공적으로 실행 된 후에 선택 **웹 서비스 배포** hello hello 페이지 맨 아래에 있습니다.

   ![Machine Learning Studio에서 실험을 웹 서비스로 배포](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. 감성 분석 모델은 준비 toouse hello toovalidate 클릭 hello **테스트** 단추입니다. "I love Microsoft"와 같은 텍스트를 입력합니다. 

   ![Machine Learning Studio에서 실험 테스트](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Hello 테스트가 작동 하는 경우 다음 예제 결과 유사한 toohello를 표시 됩니다.

   ![Machine Learning Studio의 결과 테스트](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. Hello에 **앱** 열 hello 클릭 **이전 통합 문서 또는 Excel 2010** 링크 toodownload Excel 통합 문서. hello API 키 및 이후 tooset hello 스트림 분석 작업을 사용 해야 하는 hello URL hello 통합 문서에 포함 되어 있습니다.

    ![Stream Analytics Machine Learning, 간략 상태](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Hello 기계 학습 모델을 사용 하는 스트림 분석 작업 만들기

이제 hello 샘플 트 윗을 blob 저장소에 hello CSV 파일에서 읽을 수 있는 스트림 분석 작업을 만들 수 있습니다. 

### <a name="create-hello-job"></a>Hello 작업 만들기

1. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.  

2. **새로 만들기** > **사물 인터넷** > **Stream Analytics 작업**을 클릭합니다. 

   ![Azure 포털 경로 tooa 새 스트림 분석 작업을 가져오기 위한](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. 이름 hello 작업 `azure-sa-ml-demo`, 구독을 지정, 기존 리소스 그룹을 지정 하거나 새 대시보드를 만든를 hello 작업에 대 한 hello 위치를 선택 합니다.

   ![새 Stream Analytics 작업의 설정 지정](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Hello 작업 입력 구성
hello 작업 이전 tooblob 저장소를 업로드 하는 hello CSV 파일에서 입력을 가져옵니다.

1. Hello 작업이 만들어진 후에, 아래에서 **작업 토폴로지** hello 작업 블레이드에서 hello 클릭 **입력** 상자입니다.  
   
   ![Stream Analytics 작업 블레이드의 '입력' 상자](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. Hello에 **입력** 블레이드에서 클릭 **+ 추가**합니다.

   ![' Add' 입력된 toohello 스트림 분석 작업을 추가 하기 위한 단추](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Hello 채울 **새 입력** 블레이드의 값이 있습니다.

    * **입력된 별칭**: hello 이름 사용 `datainput`합니다.
    * **원본 형식**: **데이터 스트림**을 선택합니다.
    * **원본**: **Blob Storage**를 선택합니다.
    * **가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다. 
    * **저장소 계정**. 이전에 만든 hello 저장소 계정을 선택 합니다.
    * **컨테이너**. 이전에 만든 선택 hello 컨테이너 (`azuresamldemoblob`).
    * **이벤트 직렬화 형식** **CSV**를 선택합니다.

    ![새 작업 입력의 설정](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. **만들기**를 클릭합니다.

### <a name="configure-hello-job-output"></a>Hello 작업 출력을 구성 합니다.
hello 작업 보냅니다 결과 toohello 동일한 blob 저장소 입력 가져옵니다입니다. 

1. 아래 **작업 토폴로지** hello 작업 블레이드에서 hello 클릭 **출력** 상자입니다.  
  
   ![Streaming Analytics 작업에 대한 새 출력 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. Hello에 **출력** 블레이드에서 클릭 **+ 추가**, 다음 hello 별칭으로 출력을 추가 하 고 `datamloutput`합니다. 

3. **싱크**에서 **Blob Storage**를 선택합니다. Hello hello 나머지를 입력 한 다음 설정을 사용 하 여 hello 입력에 대 한 hello blob 저장소에 사용 되는 동일한 값을 출력 합니다.

    * **저장소 계정**. 이전에 만든 hello 저장소 계정을 선택 합니다.
    * **컨테이너**. 이전에 만든 선택 hello 컨테이너 (`azuresamldemoblob`).
    * **이벤트 직렬화 형식** **CSV**를 선택합니다.

   ![새 작업 출력의 설정](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. **만들기**를 클릭합니다.   


### <a name="add-hello-machine-learning-function"></a>Hello 기계 학습 함수 추가 
이전 기계 학습 모델 tooa 웹 서비스를 게시 합니다. 이 시나리오에서 hello 스트림 분석 작업이 실행 될 때 보냅니다 각 샘플 윗 감성 분석에 대 한 hello 입력된 toohello 웹 서비스에서. hello 기계 학습 웹 서비스는 감성 반환 (`positive`, `neutral`, 또는 `negative`) 및 양의 되 고 hello 윗의 확률입니다. 

Hello 자습서의이 섹션에서는 hello 스트림 분석 작업의 함수를 정의합니다. hello 함수 윗 toohello 웹 서비스 호출 된 toosend 일를 돌아갈 hello 응답 합니다. 

1. Hello 웹 서비스 URL 및 API 키가 이전 hello Excel 통합 문서에서에서 다운로드 한 있는지 확인 합니다.

2. Toohello 작업 개요 블레이드를 반환 합니다.

3. **설정** 아래에서 **함수**를 선택하고 **+ 추가**를 클릭합니다.

   ![함수 toohello 스트림 분석 작업 추가](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. 입력 `sentiment` hello로 별칭를 작동 하 고 이러한 값을 사용 하 여 hello 블레이드 hello 나머지 채울:

    * **함수 유형**: **Azure ML**을 선택합니다.
    * **가져오기 옵션**: **다른 구독에서 가져오기**를 선택합니다. 이렇게 하면 기회 tooenter hello URL과 키입니다.
    * **URL**: hello 웹 서비스 URL에 붙여 넣습니다.
    * **키**: hello API 키에 붙여 넣습니다.
  
    ![기계 학습 함수 toohello 스트림 분석 작업을 추가 하는 것에 대 한 설정](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. **만들기**를 클릭합니다.

### <a name="create-a-query-tootransform-hello-data"></a>쿼리 tootransform hello 데이터 만들기

Stream Analytics는 선언적 이며 SQL 기반 쿼리 tooexamine hello 입력을 사용 하 고 처리 합니다. 이 섹션에서는 입력 으로부터 각 윗을 읽고 다음 hello 기계 학습 함수 tooperform 감성 분석을 호출 하는 쿼리를 만듭니다. hello 쿼리는 다음 hello 결과 toohello (blob storage)를 정의 하는 출력을 보냅니다.

1. Toohello 작업 개요 블레이드를 반환 합니다.

2.  아래 **작업 토폴로지**, hello 클릭 **쿼리** 상자입니다.

    ![Streaming Analytics 작업에 쿼리 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. 다음 쿼리에서 hello를 입력 합니다.

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    이전에 만든 hello 함수를 호출 하는 hello 쿼리 (`sentiment`) hello 입력의 각 트 윗에 순서 tooperform 감성 분석에서 합니다. 

4. 클릭 **저장** toosave hello 쿼리 합니다.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Hello 스트림 분석 작업을 시작 하 고 hello 출력 확인

이제 hello 스트림 분석 작업을 시작할 수 있습니다.

### <a name="start-hello-job"></a>Hello 작업 시작
1. Toohello 작업 개요 블레이드를 반환 합니다.

2. 클릭 **시작** hello hello 블레이드 위쪽에 있습니다.

    ![Streaming Analytics 작업에 쿼리 만들기](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. Hello에 **시작 작업**선택, **사용자 지정**를 선택한 후 1 일 이전 toowhen hello CSV 파일 tooblob 저장소를 업로드 합니다. 완료되면 **시작**을 클릭합니다.  


### <a name="check-hello-output"></a>Hello 출력 확인
1. Let hello 작업 hello에서 작업을 볼 때까지 몇 분 동안 실행 **모니터링** 상자입니다. 

2. 일반적으로 blob 저장소의 tooexamine hello 콘텐츠를 사용 하는 도구를 사용 하도록 설정한 경우 해당 도구 tooexamine hello를 사용 하 여 `azuresamldemoblob` 컨테이너입니다. 또는 않습니다 hello hello Azure 포털의에서 단계를 실행 합니다.

    1. Hello 포털에서 찾을 hello `samldemo` 저장소 계정을 찾을 hello hello 계정 내에서 한 `azuresamldemoblob` 컨테이너입니다. Hello 컨테이너에 두 파일이 표시: hello hello 샘플 트 윗을 포함 하는 파일 및 hello 스트림 분석 작업에 의해 생성 된 CSV 파일입니다.
    2. Hello 생성 된 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **다운로드**합니다. 

   ![Blob Storage에서 CSV 작업 출력 다운로드](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. 열기 hello CSV 파일을 생성 합니다. 다음 예제는 hello 같은 결과가 표시:  
   
   ![Stream Analytics Machine Learning, CSV 보기](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>메트릭 보기
또한 Azure Machine Learning 함수 관련 메트릭도 확인할 수 있습니다. 다음 함수 관련 메트릭 hello hello에 표시 되는 **모니터링** hello 작업 블레이드에서 상자:

* **요청 함수** hello 수가 전송 된 요청 tooa 기계 학습 웹 서비스를 나타냅니다.  
* **이벤트 함수** hello hello 요청에 있는 이벤트 수를 나타냅니다. 기본적으로 각 요청 tooa 기계 학습 웹 서비스 too1, 000 이벤트를 포함합니다.  


## <a name="next-steps"></a>다음 단계

* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API 및 Machine Learning 통합](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)



