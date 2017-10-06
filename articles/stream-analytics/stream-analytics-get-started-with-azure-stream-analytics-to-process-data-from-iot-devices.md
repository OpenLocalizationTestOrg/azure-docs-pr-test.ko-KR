---
title: "aaaIoT 실시간 데이터 스트림 및 Azure 스트림 분석 | Microsoft Docs"
description: "스트림 분석 및 실시간 데이터 처리와 IoT 센서 태그 및 데이터 스트림"
keywords: "IoT 솔루션, IoT 시작"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>IoT 장치에서 Azure 스트림 분석 tooprocess 데이터 시작
이 자습서에서는 살펴보겠습니다 어떻게 toocreate 스트림 처리 논리 toogather 장치에서에서 데이터를 인터넷 IoT (사물). 사용 하 여 실제, 인터넷 IoT (사물) 사용 하 여 사례 toodemonstrate 어떻게 toobuild 솔루션 신속 하 고 경제적으로 합니다.

## <a name="prerequisites"></a>필수 조건
* [Azure 구독](https://azure.microsoft.com/pricing/free-trial/)
* 샘플 쿼리 및 데이터 파일은 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>시나리오
Hello 산업 자동화 공간에서 회사는 Contoso의 제조 프로세스 완전히 자동화 했습니다. 이 공장의 hello 기계 스트림을 실시간으로 데이터를 내보낼 수 있는 센서에 있습니다. 이 시나리오는 프로덕션 floor 관리자 hello 센서 데이터 toolook에서 실시간 정보 toohave 서빙 직원을 위한 패턴 및에 작업을 수행 합니다. 데이터의 hello 들어오는 스트림에서 hello 센서 데이터 toofind 주목할 만한 패턴을 통해 스트림 분석 쿼리 언어 (SAQL) hello를 사용 합니다.

여기서 데이터는 Texas Instrument 센서 태그 장치에서 생성됩니다.

![Texas Instruments 센서 태그](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

hello 데이터 페이로드를 hello JSON 형식 이므로 hello 다음과 같습니다.

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

실제 시나리오에서는 이러한 센서가 수백 개 있으며 이벤트를 스트림으로 생성할 수 있습니다. 이상적으로 게이트웨이 장치는 실행 코드 toopush 이러한 이벤트 너무[Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 또는 [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/)합니다. 스트림 분석 작업 이벤트 허브에서 이러한 이벤트를 수집 하 고 hello 스트림에 대해 실시간 분석 쿼리를 실행할 게 됩니다. Hello의 hello 결과 tooone를 보낼 수 있으며 그런 다음 [출력 지원](stream-analytics-define-outputs.md)합니다.

사용 편의성을 위해 이 시작 가이드는 실제 센서 태그 장치에서 캡처된 샘플 데이터 파일을 제공합니다. Hello 예제 데이터에서 쿼리를 실행 하 고 결과 확인할 수 있습니다. 이후 자습서에 설명 합니다 방법을 tooconnect 프로그램 tooinputs / 출력 작업 및 toohello Azure 서비스를 배포 합니다.

## <a name="create-a-stream-analytics-job"></a>Stream Analytics 작업 만들기
1. Hello에 [Azure 포털](http://portal.azure.com)hello 더하기 기호를 클릭 한 다음 입력, **스트림 분석** hello 텍스트 창 toohello 오른쪽에 있습니다. 그런 다음 선택 **스트림 분석 작업** hello 결과 목록에 있습니다.
   
    ![새 스트림 분석 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. 고유한 작업 이름을 입력 하 고 hello 구독 작업에 적절 한 hello는 확인 합니다. 그런 다음 새 리소스 그룹을 만들거나 구독에 속한 기존 리소스 그룹을 선택합니다.
3. 작업의 위치를 선택합니다. 처리 속도 hello를 선택 하는 데이터 전송에서 비용을 절감 하는 역할에 대 한 hello 리소스 그룹 및 의도 한 저장소 계정이 동일한 위치 하는 것이 좋습니다.
   
    ![새 Stream Analytics 작업 만들기 세부 정보](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > 이 저장소 계정은 지역당 한 번만 만들어야 합니다. 이 저장소는 해당 지역에 생성되는 모든 Stream Analytics 작업에서 공유됩니다.
   > 
   > 
4. Hello 상자 tooplace 대시보드 작업을 확인 하 고 클릭 **만들기**합니다.
   
    ![진행 중인 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. '배포 시작...'를 참조 해야 브라우저 창의 오른쪽 위 hello에에서 표시 합니다. 곧 아래와 같이 완료 tooa 창이 변경 됩니다.
   
    ![진행 중인 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Azure Stream Analytics 쿼리 만들기
후 작업을 만든 시간 tooopen 쿼리 작성 합니다. 에 대 한 hello 타일을 클릭 하 여 작업을 쉽게 액세스할 수 있습니다.

![작업 타일](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

Hello에 **작업 토폴로지** 창의 hello 클릭 **쿼리** toogo toohello 쿼리 편집기 상자입니다. hello **쿼리** hello 들어오는 이벤트 데이터에 대해 hello 변환을 수행 하는 T-SQL tooenter 쿼리 편집기를 사용 합니다.

![쿼리 상자](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>쿼리: 원시 데이터 보관
쿼리 hello 가장 간단한 형태는 출력을 지정 하는 모든 입력된 데이터 tooits 보관 하는 통과 쿼리입니다. Hello 예제 데이터 파일의 다운로드 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) 컴퓨터에서 tooa 위치입니다. 

1. Hello PassThrough.txt 파일에서 hello 쿼리를 붙여 넣습니다. 
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Hello 3 점 다음 tooyour 입력을 클릭 하 고 선택 **파일에서 샘플 데이터 업로드** 상자입니다.
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. 결과 오른쪽으로 hello에는 창이 열립니다에 select hello HelloWorldASA InputStream.json 데이터 파일을 다운로드 한 위치에서 클릭 **확인** hello hello 창 맨 아래에 있습니다.
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Hello 클릭 **테스트** hello 창의 왼쪽 hello 위에에서 기어를 hello 샘플 데이터 집합에 대해 테스트 쿼리를 처리 합니다. Hello 처리가 완료 될 때 쿼리 아래 결과 창이 열립니다.
   
    ![테스트 결과](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>조건에 따라 hello 데이터를 필터링 하는 쿼리:
조건에 따라 toofilter hello 결과 보겠습니다. "SensorA"에서 제공 하는 이벤트에 대 한 tooshow 결과 같은 hello 쿼리 hello Filtering.txt 파일에는입니다.

![데이터 스트림 필터링](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Hello 대/소문자 구분 쿼리 하는 문자열 값을 비교 합니다. Hello 클릭 **테스트** 기어 다시 tooexecute hello 쿼리 합니다. hello 쿼리 389 행 1860 이벤트 밖으로 반환 해야 합니다.

![쿼리 테스트의 두 번째 출력 결과](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>쿼리: 경고 tootrigger 비즈니스 워크플로
쿼리를 더 자세히 만들겠습니다. 모든 유형의 센서에 대 한 30 초 창당 toomonitor 평균 온도 원하는 म 고 hello 평균 온도 100 이상인 경우에 결과 표시 합니다. Hello 다음 쿼리하고 클릭 작성 하 **테스트** toosee hello 결과입니다. hello 쿼리 hello ThresholdAlerting.txt 파일에는입니다.

![30초 필터 쿼리](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

이제 표시 되어야만 245 행과 센서의 이름을 포함 하는 결과 온도 hello 평균이 100 보다 큰 합니다. 이 쿼리로 이벤트의 hello 스트림을 그룹화 **dspl**는 hello 센서 이름을 초과 하는 한 **텀블 링 창** 30 초입니다. 임시 쿼리 시간 tooprogress 원하는 라고 명시 해야 합니다. Hello를 사용 하 여 **TIMESTAMP BY** 절 hello 앞서 지정한 **OUTPUTTIME** 열 tooassociate 시간이 모든 임시 계산 합니다. 에 대 한 자세한 정보에 대 한 hello MSDN 문서를 읽을 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [창 작업 기능](https://msdn.microsoft.com/library/azure/dn835019.aspx)합니다.

### <a name="query-detect-absence-of-events"></a>쿼리: 이벤트 부재 감지
에서는 작성 방법을 쿼리 toofind 입력된 이벤트의 부족? 센서 데이터를 전송 하 고 다음 다음 분 hello에 대 한 이벤트를 보내지 않은 hello 마지막으로 알아보겠습니다. hello 쿼리 hello AbsenseOfEvent.txt 파일에는입니다.

![이벤트의 부재 감지](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

사용 하 여 여기는 **LEFT OUTER** toohello 조인 동일한 데이터 스트림 (자체 조인). **내부** 조인의 경우 결과는 일치 항목이 있는 경우에만 반환됩니다.  에 대 한는 **LEFT OUTER** 조인을 경우 hello hello 조인의 왼쪽의 이벤트를 일치 하지 않으면 모든 hello hello 오른쪽의 열에 대 한 NULL이 있는 행 반환 됩니다. 이 방법은 매우 유용한 toofind 이벤트의 부재입니다. [조인](https://msdn.microsoft.com/library/azure/dn835026.aspx)에 대한 자세한 내용은 MSDN 설명서를 참조하세요.

## <a name="conclusion"></a>결론
hello이이 자습서의 목적은 toodemonstrate toowrite 다른 스트림 분석 쿼리 언어 쿼리 및 참조 hello 브라우저에서 발생 하는 방법입니다. 그러나 이 과정은 시작일 뿐입니다. Stream Analytics으로 많은 작업을 수행할 수 있습니다. 스트림 분석은 다양 한 입력 및 출력을 지원 및 수에 사용 하 여 함수가 Azure 기계 학습 toomake 것 데이터 스트림 분석 하기 위한 강력한 도구입니다. 사용 하 여 스트림 분석에 대 한 자세한 tooexplore를 시작할 수 있습니다이 [학습 맵](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/)합니다. 방법에 대 한 자세한 내용은 대 한 hello 문서를 참조 하는 쿼리를 toowrite [일반 쿼리 패턴](stream-analytics-stream-analytics-query-patterns.md)합니다.

