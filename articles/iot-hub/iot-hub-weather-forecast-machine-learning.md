---
title: "Azure 기계 학습을 사용 하 여 IoT 허브에서 데이터와 예측 aaaWeather | Microsoft Docs"
description: "Azure 기계 학습 hello 온도 및 습도에 따라 비 toopredict hello 가능성이 IoT 허브는 센서에서 수집 된 데이터를 사용 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "일기 예보 기계 학습"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>IoT 허브에서 hello 센서 데이터를 사용 하 여 Azure 기계 학습에서 일기 예보

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

기계 학습에는 컴퓨터에서 기존 데이터 tooforecast 이후 동작, 결과 및 추세를 배울 도움이 되는 데이터 과학자의 기술입니다. Azure 기계 학습은 클라우드 예측 분석 서비스를 이용 하 가능한 tooquickly 생성 하 고 분석 솔루션으로 예측 모델을 배포 합니다.

## <a name="what-you-learn"></a>학습 내용

어떻게 Azure IoT 허브에서 데이터를 온도 및 습도 hello toouse Azure 기계 학습 toodo 일기 예보 (비 가능성)를 사용 하 여 방법을 배웁니다. 비 hello 가능성은 준비 날씨 예측 모델의 hello 출력. hello 모델 온도 및 습도에 따라 비 tooforecast 가능성이 기록 데이터를 기반으로 합니다.

## <a name="what-you-do"></a>수행할 작업

- 웹 서비스로 hello 날씨 예측 모델을 배포 합니다.
- 소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비
- 스트림 분석 작업을 만들고 hello 작업을 구성 합니다.
  - IoT Hub에서 온도 및 습도 데이터를 읽습니다.
  - Hello 웹 서비스 tooget hello 비 기회를 호출 합니다.
  - Hello 결과 tooan Azure blob 저장소를 저장 합니다.
- Microsoft Azure 저장소 탐색기 tooview hello 일기 예보를 사용 합니다.

## <a name="what-you-need"></a>필요한 항목

- 자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.
  - 활성 Azure 구독.
  - 구독 중인 Azure IoT Hub
  - 메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.
- Azure Machine Learning Studio 계정 [Machine Learning Studio 체험해 보기](https://studio.azureml.net/)

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>웹 서비스로 hello 날씨 예측 모델을 배포 합니다.

1. Toohello 이동 [날씨 예측 모델 페이지](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1)합니다.
1. Microsoft Azure Machine Learning Studio에서 **Studio에서 열기**를 클릭합니다.
   ![Cortana Intelligence 갤러리에서 열기 hello 날씨 예측 모델 페이지](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. 클릭 **실행** toovalidate hello hello 모델의 단계입니다. 이 단계는 2 분 toocomplete를 걸릴 수 있습니다.
   ![Azure 기계 학습 스튜디오에서 열기 hello 날씨 예측 모델](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. **웹 서비스 설정** > **예측형 웹 서비스**를 클릭합니다.
   ![Azure 기계 학습 스튜디오에서 hello 날씨 예측 모델 배포](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Hello 다이어그램으로 끌어서 hello **웹 서비스 입력** hello 근처 어딘가에 모듈 **모델 점수 매기기** 모듈입니다.
1. Hello 연결 **웹 서비스 입력** 모듈 toohello **모델 점수 매기기** 모듈입니다.
   ![Azure Machine Learning Studio에서 두 모듈 연결](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. 클릭 **실행** toovalidate hello hello 모델의 단계입니다.
1. 클릭 **웹 서비스 배포** 웹 서비스로 toodeploy hello 모델입니다.
1. Hello 모델의 hello 대시보드에서 hello 다운로드 **이전 통합 문서 또는 Excel 2010** 에 대 한 **요청/응답**합니다.

   > [!Note]
   > Hello를 다운로드 하는 확인 **이전 통합 문서 또는 Excel 2010** 컴퓨터에 Excel의 이후 버전을 실행 하는 경우에 합니다.

   ![Hello 요청 응답 끝점에 대 한 Excel hello 다운로드](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Hello Excel 통합 문서를 열고, hello 메모 **웹 서비스 URL** 및 **선택 키**합니다.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Stream Analytics 작업 만들기, 구성 및 실행

### <a name="create-a-stream-analytics-job"></a>Stream Analytics 작업 만들기

1. Hello에 [Azure 포털](https://ms.portal.azure.com/), 클릭 **새로** > **사물 인터넷** > **스트림 분석 작업**합니다.
1. Hello 다음 hello 작업에 대 한 정보를 입력 합니다.

   **작업 이름**: hello 작업의 hello 이름입니다. hello 이름은 전역적으로 고유 해야 합니다.

   **리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.

   **위치**: 사용 하 여 hello 동일한 리소스 그룹 위치입니다.

   **Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.

   ![Azure에서 Stream Analytics 작업 만들기](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. **만들기**를 클릭합니다.

### <a name="add-an-input-toohello-stream-analytics-job"></a>입력된 toohello 스트림 분석 작업 추가

1. 열기 hello 스트림 분석 작업 합니다.
1. **작업 토폴로지**에서 **입력**을 클릭합니다.
1. Hello에 **입력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.

   **입력된 별칭**: hello hello 입력에 대 한 고유 별칭입니다.

   **원본**: **IoT Hub**를 선택합니다.

   **소비자 그룹**: 만든 선택 hello 소비자 그룹입니다.

   ![Azure에서 입력된 toohello 스트림 분석 작업 추가](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. **만들기**를 클릭합니다.

### <a name="add-an-output-toohello-stream-analytics-job"></a>출력 toohello 스트림 분석 작업 추가

1. **작업 토폴로지**에서 **출력**을 클릭합니다.
1. Hello에 **출력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.

   **출력 별칭**: hello hello 출력에 대 한 고유 별칭입니다.

   **싱크**: **Blob Storage**를 선택합니다.

   **저장소 계정**: hello blob 저장소에 대 한 저장소 계정입니다. 저장소 계정을 만들거나 기존 계정을 사용할 수 있습니다.

   **컨테이너**: hello 컨테이너 hello blob 저장 됩니다. 컨테이너를 만들거나 기존 컨테이너를 사용할 수 있습니다.

   **이벤트 직렬화 형식**: **CSV**를 선택합니다.

   ![Azure에서 출력 toohello 스트림 분석 작업 추가](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. **만들기**를 클릭합니다.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>함수 toohello 배포한 스트림 분석 작업 toocall hello 웹 서비스를 추가 합니다.

1. **작업 토폴로지**에서 **함수** > **추가**를 클릭합니다.
1. Hello 다음 정보를 입력 합니다.

   **별칭 함수**: `machinelearning`을(를) 입력합니다.

   **함수 유형**: **Azure ML**을 선택합니다.

   **가져오기 옵션**: **다른 구독에서 가져오기**를 선택합니다.

   **URL**: hello Excel 통합 문서에서 hello 아래로 기록한 웹 서비스 URL을 입력 합니다.

   **키**: hello Excel 통합 문서에서 hello에 아래 표시 된 선택 키를 입력 합니다.

   ![Azure에서 함수 toohello 스트림 분석 작업 추가](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. **만들기**를 클릭합니다.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Hello 스트림 분석 작업의 hello 쿼리 구성

1. **작업 토폴로지**에서 **쿼리**를 클릭합니다.
1. 코드 다음 hello hello 기존 코드를 바꿉니다.

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   대체 `[YourInputAlias]` hello 작업의 입력 hello 별칭으로 합니다.

   대체 `[YourOutputAlias]` hello 작업의 hello 출력 별칭 사용.

1. **Save**를 클릭합니다.

### <a name="run-hello-stream-analytics-job"></a>Hello 스트림 분석 작업을 실행 합니다.

Hello Stream Analytics 작업에서 클릭 **시작** > **이제** > **시작**합니다. Hello 작업 상태에서 변경 hello 작업이 성공적으로 시작 되 면 **Stopped** 너무**실행**합니다.

![Hello 스트림 분석 작업을 실행 합니다.](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Microsoft Azure 저장소 탐색기 tooview hello 일기 예보를 사용 하 여

온도 및 습도 데이터 tooyour IoT 허브를 보내고 hello 클라이언트 응용 프로그램 toostart 수집을 실행 합니다. IoT hub를 수신 하는 각 메시지에 대 한 hello 스트림 분석 작업 비 hello 일기 예보 웹 서비스 tooproduce hello 가능성이 호출 합니다. hello 결과 tooyour Azure blob 저장소를 저장 합니다. Azure 저장소 탐색기는 tooview hello 결과 사용할 수 있는 도구입니다.

1. [Microsoft Azure Storage 탐색기를 다운로드하고 설치합니다](http://storageexplorer.com/).
1. Azure Storage 탐색기를 엽니다.
1. Azure 계정 tooyour에 로그인 합니다.
1. 사용 중인 구독을 선택합니다.
1. 구독> **저장소 계정** > 저장소 계정> **Blob 컨테이너**> 컨테이너를 차례로 클릭합니다.
1. .Csv 파일 toosee hello 결과를 엽니다. 마지막 열 레코드 hello hello 비 가능성이 있습니다.

   ![Azure Machine Learning을 사용하여 일기 예보 결과 가져오기](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>요약

IoT hub 받는 hello 온도 및 습도 데이터를 기반으로 하는 비 Azure 기계 학습 tooproduce hello 가능성을 성공적으로 사용 했습니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]