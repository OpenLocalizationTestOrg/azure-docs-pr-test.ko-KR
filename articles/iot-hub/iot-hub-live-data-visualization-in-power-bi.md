---
title: "Azure IoT Hub-Power BI에서에서 센서 데이터의 타임 aaaReal 데이터 시각화 | Microsoft Docs"
description: "Power BI toovisualize 온도 및 습도 데이터를 사용 hello 센서에서 수집 되 고 tooyour Azure IoT 허브를 전송 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "실시간 데이터 시각화, 라이브 데이터 시각화, 센서 데이터 시각화"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Power BI를 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>학습 내용

배웁니다 어떻게 Power BI에서 Azure IoT hub 받는 toovisualize 센서 실시간 데이터입니다. Tootry hello 데이터를 시각화 하려면 웹 앱과 IoT 허브에서를 참조 하세요 [Azure IoT 허브에서 사용 하 여 Azure 웹 앱 toovisualize 실시간 센서 데이터](iot-hub-live-data-visualization-in-web-apps.md)합니다.

## <a name="what-you-do"></a>수행할 작업

- 소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비
- 만들고 구성 하 고 IoT 허브 tooyour Power BI 계정에서에서 데이터 전송에 대 한 스트림 분석 작업을 실행 합니다.
- 만들고 Power BI 보고서 toovisualize hello 데이터를 게시 합니다.

## <a name="what-you-need"></a>필요한 항목

- 자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.
  - 활성 Azure 구독.
  - 구독 중인 Azure IoT Hub
  - 메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.
- Power BI 계정 ([Power BI를 무료로 사용해 보기](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Stream Analytics 작업 만들기, 구성 및 실행

### <a name="create-a-stream-analytics-job"></a>Stream Analytics 작업 만들기

1. Hello Azure 포털에서 새로 만들기 > 사물 인터넷 > 스트림 분석 작업 합니다.
1. Hello 다음 hello 작업에 대 한 정보를 입력 합니다.

   **작업 이름**: hello 작업의 hello 이름입니다. hello 이름은 전역적으로 고유 해야 합니다.

   **리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.

   **위치**: 사용 하 여 hello 동일한 리소스 그룹 위치입니다.

   **Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.

   ![Azure에서 Stream Analytics 작업 만들기](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. **만들기**를 클릭합니다.

### <a name="add-an-input-toohello-stream-analytics-job"></a>입력된 toohello 스트림 분석 작업 추가

1. 열기 hello 스트림 분석 작업 합니다.
1. **작업 토폴로지**에서 **입력**을 클릭합니다.
1. Hello에 **입력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.

   **입력된 별칭**: hello hello 입력에 대 한 고유 별칭입니다.

   **원본**: **IoT Hub**를 선택합니다.

   **소비자 그룹**: 방금 만든 선택 hello 소비자 그룹입니다.
1. **만들기**를 클릭합니다.

   ![Azure에서 입력된 tooa 스트림 분석 작업 추가](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>출력 toohello 스트림 분석 작업 추가

1. **작업 토폴로지**에서 **출력**을 클릭합니다.
1. Hello에 **출력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.

   **출력 별칭**: hello hello 출력에 대 한 고유 별칭입니다.

   **싱크**: **Power BI**를 선택합니다.
1. **권한 부여**를 클릭한 다음 Power BI 계정에 로그인합니다.
1. 에 게 권한이 부여 되 면 hello 다음 정보를 입력 합니다.

   **그룹 작업 영역**: 대상 그룹 작업 영역을 선택합니다.

   **데이터 집합 이름**: 데이터 집합 이름을 입력합니다.

   **테이블 이름**: 테이블 이름을 입력합니다.
1. **만들기**를 클릭합니다.

   ![Azure에서 출력 tooa 스트림 분석 작업 추가](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Hello 스트림 분석 작업의 hello 쿼리 구성

1. **작업 토폴로지**에서 **쿼리**를 클릭합니다.
1. 대체 `[YourInputAlias]` hello 작업의 입력 hello 별칭으로 합니다.
1. 대체 `[YourOutputAlias]` hello 작업의 hello 출력 별칭 사용.
1. **Save**를 클릭합니다.

   ![Azure의 쿼리 tooa 스트림 분석 작업 추가](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Hello 스트림 분석 작업을 실행 합니다.

Hello Stream Analytics 작업에서 클릭 **시작** > **이제** > **시작**합니다. Hello 작업 상태에서 변경 hello 작업이 성공적으로 시작 되 면 **Stopped** 너무**실행**합니다.

![Azure에서 Stream Analytics 작업 실행](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>만들기 및 Power BI 보고서 toovisualize hello 데이터 게시

1. Hello 샘플 응용 프로그램 장치에서 실행 중인지 확인 합니다. 아래 toohello 자습서를 참조 하면 그렇지 [사용자 장치를 설정](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)합니다.
1. Tooyour 로그인 [Power BI](https://powerbi.microsoft.com/en-us/) 계정.
1. Hello 스트림 분석 작업에 대 한 hello 출력을 만들 때 설정한 toohello 그룹 작업 영역을 이동 합니다.
1. **스트리밍 데이터 집합**을 클릭합니다.

   Hello hello 스트림 분석 작업에 대 한 출력을 만들 때 지정한 hello 나열 된 데이터 집합을 표시 되어야 합니다.
1. 아래 **동작**, hello 첫 번째 아이콘 toocreate 보고서를 클릭 합니다.

   ![Microsoft Power BI 보고서 만들기](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. 시간이 지남에 따라 꺾은선형 차트 tooshow 실시간 온도를 만듭니다.
   1. Hello 보고서 만들기 페이지에는 꺾은선형 차트를 추가 합니다.
   1. Hello에 **필드** 창 hello 스트림 분석 작업에 대 한 hello 출력을 만들 때 지정한 hello 테이블을 확장 합니다.
   1. 끌기 **EventEnqueuedUtcTime** 너무**축** hello에 **시각화** 창.
   1. 끌기 **온도** 너무**값**합니다.

      이제 꺾은선형 차트가 만들어집니다. hello x 축 hello UTC 표준 시간대의 날짜 및 시간을 표시합니다. hello y 축 hello 센서의 온도 표시합니다.

      ![온도 tooa Microsoft Power BI 보고서는 꺾은선형 차트를 추가 합니다.](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. 시간에 따라 다른 꺾은선형 차트 tooshow 실시간 습도를 만듭니다. toodo이 위의 프로세스를 같은 hello을 따르고 **EventEnqueuedUtcTime** hello x 축에 및 **습도** hello y 축에 있습니다.

   ![습도 tooa Microsoft Power BI 보고서는 꺾은선형 차트를 추가 합니다.](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. 클릭 **저장** toosave hello 보고서입니다.
1. 클릭 **파일** > **tooweb 게시**합니다.
1. **Embed 태그 만들기**를 클릭한 다음 **게시**를 클릭합니다.

블로그 또는 웹 사이트에 보고서 액세스에 대 한 모든 사용자와 코드 조각 toointegrate hello 보고서와 공유할 수 있는 hello 보고서 링크를 제공 하는.

![Microsoft Power BI 보고서 게시](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft는 또한 hello 제공 [Power BI 모바일 앱](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) 보기 및 사용자 Power BI 대시보드 및 보고서 상호 작용에 대 한 모바일 장치에 있습니다.

## <a name="next-steps"></a>다음 단계

Azure IoT 허브에서 Power BI toovisualize 실시간 센서 데이터를 성공적으로 사용 했습니다.
다른 방법 toovisualize 데이터를 사용 하 여 Azure IoT Hub를 있습니다. 참조 [Azure IoT 허브에서 사용 하 여 Azure 웹 앱 toovisualize 실시간 센서 데이터](iot-hub-live-data-visualization-in-web-apps.md)합니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
