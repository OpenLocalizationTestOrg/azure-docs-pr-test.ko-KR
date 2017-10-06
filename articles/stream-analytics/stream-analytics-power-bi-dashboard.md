---
title: "Azure 스트림 분석에서 aaaPower BI 대시보드 | Microsoft Docs"
description: "실시간 스트리밍 Power BI 대시보드 toogather 비즈니스 인텔리전스를 사용 하 고 스트림 분석 작업에서 대용량 데이터를 분석 합니다."
keywords: "분석 대시보드, 실시간 대시보드"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics 및 Power BI: 스트리밍 데이터에 대한 실시간 분석 대시보드
Azure 스트림 분석 하면 비즈니스 인텔리전스 도구를 선행 hello 중 하나의 tootake 이점은 [Microsoft Power BI](https://powerbi.com/)합니다. 이 문서에서는 Azure Stream Analytics 작업에 대한 출력으로 Power BI를 사용하여 비즈니스 인텔리전스 도구를 만드는 방법에 대해 알아봅니다. 또한 학습 방법을 toocreate 실시간 대시보드를 사용 합니다.

이 문서는 hello 스트림 분석에서에서 계속 [실시간 사기 감지](stream-analytics-real-time-fraud-detection.md) 자습서입니다. 해당 자습서에서 만든 hello 워크플로 작성 하 고 출력 스트리밍 분석 작업에서 검색 되는 사기성 전화 통화를 시각화할 수 있도록 Power BI에 추가 합니다. 

이 시나리오를 보여주는 [비디오](https://www.youtube.com/watch?v=SGUpT-a99MA)를 시청할 수 있습니다.


## <a name="prerequisites"></a>필수 조건

시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.

* Azure 계정.
* Power BI에 대한 계정. 회사 계정 또는 학교 계정을 사용할 수 있습니다.
* 완성 된 버전의 hello [실시간 사기 감지](stream-analytics-real-time-fraud-detection.md) 자습서입니다. hello 자습서는 가상의 전화 통화 메타 데이터를 생성 하는 응용 프로그램을 포함 합니다. Hello 자습서에서는 이벤트 허브는 만들고 hello 전화 통화 데이터 toohello 이벤트 허브를 스트리밍 보냅니다. 사기성 호출 (호출 hello hello에 같은 수의 시간이 서로 다른 위치에)를 검색 하는 쿼리를 작성 합니다. 


## <a name="add-power-bi-output"></a>Power BI 출력 추가
Hello 실시간 사기 감지 자습서 hello 출력 tooAzure Blob 저장소를 전송 됩니다. 이 섹션의 정보 tooPower BI 전송 하는 출력을 추가 합니다.

1. Hello Azure 포털에서에서 앞에서 만든 hello 스트리밍 분석 작업을 엽니다. Hello 작업의 이름은 hello 제안 된 이름을 사용 하는 경우 `sa_frauddetection_job_demo`합니다.

2. 선택 hello **출력** 상자 hello 작업 대시보드의 hello 중간에 선택한 후 **+ 추가**합니다.

3. **출력 별칭**에 `CallStream-PowerBI`를 입력합니다. 다른 이름을 사용할 수 있습니다. 이렇게 하면 hello 이름을 나중에 필요 하기 때문에, 메모를 확인 합니다. 

4. **싱크** 아래에서 **Power BI**를 선택합니다.

   ![Power BI에 대한 출력 만들기](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. **권한 부여**를 클릭합니다.

    회사 또는 학교 계정에 대한 Azure 자격 증명을 제공할 수 있는 창이 열립니다. 

    ![액세스 tooPower BI에 대 한 자격 증명을 입력 합니다.](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. 자격 증명을 입력합니다. 업그레이드할 경우 자격 증명을 입력 하면 하는 또한 부여 권한을 toohello 스트리밍 분석 작업 tooaccess 사용자 Power BI의 지역 합니다.

7. Toohello을 반환 하는 때 **새 출력** 블레이드에서 hello 다음 정보를 입력 합니다.

    * **그룹 작업 영역**: toocreate hello 데이터 집합을 원하는 Power BI 테 넌 트의 작업 영역을 선택 합니다.
    * **데이터 집합 이름**: `sa-dataset`을 입력합니다. 다른 이름을 사용할 수 있습니다. 이 경우 나중을 위해 기록해 둡니다.
    * **테이블 이름**: `fraudulent-calls`를 입력합니다. 현재, Stream Analytics 작업의 Power BI 출력에는 하나의 데이터 집합에 하나의 테이블만 있을 수 있습니다.

    ![PBI 작업 영역](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Power BI 데이터 집합에 없는 테이블 hello hello와 이름이 같은 hello Stream Analytics 작업에서 지정 하는 경우는 스토리를 기존 hello가 덮어씁니다.
    > 이 데이터 집합 및 테이블을 Power BI 계정에 명시적으로 만들지 않는 것이 좋습니다. 스트림 분석 작업 시작 hello 작업 Power BI에 대리 펌핑 출력을 시작 하는 경우 자동으로 생성 됩니다. 작업 쿼리 어떤 결과도 반환 하지 않는 경우 hello 데이터 집합 및 테이블 만들어지지 않습니다.
    >

8. **만들기**를 클릭합니다.

hello dataset hello 다음 설정으로 만들어집니다.

* **defaultRetentionPolicy: BasicFIFO**:데이터는 FIFO이고, 최대 200,000개의 행이 있습니다.
* **defaultMode: pushStreaming**: hello dataset 스트리밍 타일 및 기존 보고서를 기반으로 시각적 개체를 모두 지원 (규칙 하위 푸시)를 모두 지원합니다.

지금은 다른 플래그로 데이터 집합을 만들 수 없습니다.

Power BI 데이터 집합에 대 한 자세한 내용은 참조 hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) 참조 합니다.


## <a name="write-hello-query"></a>Hello 쿼리 작성

1. 닫기 hello **출력** 블레이드에 대 한 반환 toohello 작업 블레이드입니다.

2. Hello 클릭 **쿼리** 상자입니다. 

3. 다음 쿼리에서 hello를 입력 합니다. 이 쿼리는 비슷한 toohello 자체 조인 쿼리 hello 사기 감지 자습서에서 만든 합니다. hello 차이점은이 쿼리 보내는 사용자가 만든 새 결과 toohello 출력 (`CallStream-PowerBI`). 

    >[!NOTE]
    >Hello 입력 이름을 하지 않은 경우 `CallStream` hello 사기 감지 자습서에서에 대 한 이름을 대체 `CallStream` hello에 **FROM** 및 **조인** hello 쿼리에서 절.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. **Save**를 클릭합니다.


## <a name="test-hello-query"></a>Hello 쿼리 테스트
이 섹션은 선택 사항이지만 권장됩니다. 

1. Hello TelcoStreaming 앱 현재 실행 되지 않는 경우 다음이 단계를 수행 하 여 시작 합니다.

    * 명령 창을 엽니다.
    * Hello telcogenerator.exe와 수정 된 telcodatagen.exe.config 파일이 있는 toohello 폴더를 이동 합니다.
    * Hello 다음 명령을 실행 합니다.

            telcodatagen.exe 1000 .2 2

2. Hello에 **쿼리** 블레이드에서 hello 점 다음 toohello 클릭 `CallStream` 입력 한 다음 선택 **데이터 입력에서 샘플**합니다.

3. 3분 분량의 데이터를 원하는 것으로 지정하고 **확인**을 클릭합니다. Hello 데이터는 샘플링 된 알림을 받으면 때까지 기다립니다.

4. **테스트**를 클릭하고 결과를 가져오는지 확인합니다.


## <a name="run-hello-job"></a>Hello 작업 실행

1. Hello TelcoStreaming 앱 실행 되 고 있는지 확인 합니다.

2. 닫기 hello **쿼리** 블레이드입니다.

3. Hello 작업 블레이드에서 클릭 **시작**합니다.

    ![Hello 스트림 분석 작업 시작](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

스트리밍 분석 작업 hello 들어오는 스트림에 사기성 호출에 대 한 검색 하기 시작 합니다. hello 작업 hello 데이터 집합 및 테이블 Power BI에서 만들어지고 사기성 호출 toothem hello에 대 한 데이터를 보내기 시작 됩니다.


## <a name="create-hello-dashboard-in-power-bi"></a>Power BI에서 hello 대시보드 만들기

1. 너무 이동[Powerbi.com](https://powerbi.com) 회사 또는 학교 계정으로 로그인 합니다. Hello 스트림 분석 작업 쿼리 결과 출력 하는 경우 데이터 집합은 이미 생성 되어 있음을 확인할 수 있습니다.

    ![Power BI에서 스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. 작업 영역에서 **+&nbsp;만들기**를 클릭합니다.

    ![Power BI 작업 영역에서 hello 만들기 단추](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. 새 대시보드를 만들고 이름을 `Fraudulent Calls`로 지정합니다.

    ![대시보드를 만들고 Power BI 작업 영역에서 이름 지정](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Hello 창의 hello 위쪽을 클릭 **타일 추가**선택, **스트리밍 데이터 사용자 지정**, 클릭 하 고 **다음**합니다.

    ![사용자 지정 스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. **데이터 집합** 아래에서 데이터 집합을 선택하고 **다음**을 클릭합니다.

    ![스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. **시각화 유형을**선택, **카드**, 한 다음 hello **필드** 목록에서 **fraudulentcalls**합니다.

    ![새 타일에 대한 시각화 세부 정보](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. **다음**을 누릅니다.

8. 제목 및 부제목 같은 타일 세부 정보를 입력합니다.

    ![새 타일에 대한 제목 및 부제목](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. **Apply**를 클릭합니다.

    이제 사기 카운터가 나타납니다.

    ![사기 카운터](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. 다음 hello 단계를 다시 tooadd 타일 (4 단계부터 시작)입니다. 이 이번에는 다음 hello지 않습니다.

    * 받을 경우에 너무**시각화 유형을**선택, **꺾은선형 차트**합니다. 
    * 축을 추가하고 **windowend**를 선택합니다. 
    * 값을 추가하고 **fraudulentcalls**를 선택합니다.
    * 에 대 한 **시간 창 toodisplay**선택, hello 지난 10 분입니다.

    ![꺾은선형 차트에 대한 타일 만들기](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. **다음**을 클릭하고 제목 및 부제목을 추가하고 **적용**을 클릭합니다.

    Power BI 대시보드 hello 이제 제공 사기성 호출에 대 한 두 개의 데이터 보기 hello 스트리밍 데이터에서에서 검색 합니다.

    ![사기성 호출에 대한 두 가지 타일을 보여 주는 완료된 Power BI 대시보드](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Power BI에 대해 자세히 알아보기

이 자습서에서는 설명 방법을 toocreate 몇 가지 유형의 데이터 집합에 대 한 시각화입니다. Power BI는 조직에 대한 다른 고객 비즈니스 인텔리전스 도구를 만드는 데 도움이 됩니다. 자세한 내용은 다음 리소스는 hello 참조:

* Power BI 대시보드의 또 다른 예로, 감시 hello [Power BI 시작 하기](https://youtu.be/L-Z_6P56aas?t=1m58s) 비디오.
* 스트리밍 분석을 구성 하는 방법에 대 한 자세한 내용은 작업 출력 tooPower BI 및 hello 검토 Power BI 그룹을 사용 하 여 [Power BI](stream-analytics-define-outputs.md#power-bi) hello 섹션 [스트림 분석 출력](stream-analytics-define-outputs.md) 문서. 
* 일반적으로 Power BI를 사용 하는 방법은 [Power BI의 대시보드](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)를 참조하세요.


## <a name="learn-about-limitations-and-best-practices"></a>제한 사항 및 모범 사례에 대해 알아보기
현재는 대략 1초당 한 번 Power BI를 호출할 수 있습니다. 스트리밍 시각적 개체는 15KB의 패킷을 지원합니다. 이 외 스트리밍 시각적 개체가 실패 (하지만 푸시 계속 toowork) 합니다. 이러한 제한 때문에 Power BI는 경우가 많으므로 가장 자연스럽 게 toocases Azure 스트림 분석에서 중요 한 데이터 로드를 줄이기 하 게 합니다. 연속 창 또는 도약 창 tooensure 데이터 푸시 최대 초 당 하나의 푸시 있으며 하는지 hello 처리량 요구 사항 내에서 처음 삽입 쿼리를 사용 하는 것이 좋습니다.

다음 수식은 toocompute hello 값 toogive hello 창 (초)에서 사용할 수 있습니다.

![수식 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

예:

* 1,000대의 장치가 1초 간격으로 데이터를 보내고 있습니다.
* Power BI Pro SKU에 시간당 1000000 행 지원 hello를 사용 하는 합니다.
* 장치 tooPower BI 당 평균 데이터의 toopublish hello 양을 사용 하는 것이 좋습니다.

결과적으로, hello 수식을 다음과 같이 됩니다.

![수식 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

구성이 이와 hello 원래 쿼리 toohello 다음을 변경할 수 있습니다.

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>권한 부여 갱신
Hello 암호 작업을 만들거나 마지막으로 인증 된 이후 변경 된 경우 Power BI 계정이 tooreauthenticate 필요 합니다. Azure Multi-factor Authentication은 Azure Active Directory (Azure AD) 테 넌 트에 구성 된 경우에 toorenew Power BI 권한 부여 2 주마다 필요 합니다. 갱신 하지 않는 경우 작업 출력의 부족과 같이 증상을 볼 수 있습니다 또는 `Authenticate user error` hello 작업 로그에 있습니다.

마찬가지로, 작업에는 hello 토큰이 만료 된 후 시작 되 면 오류가 발생 하 고 hello 작업이 실패 합니다. tooresolve이이 문제를 hello 실행 중인 작업을 중지 하 고 Power BI 출력 tooyour 이동. tooavoid 데이터 손실, 선택 hello **권한 부여를 갱신** 링크를 선택한 다음 hello에서 작업을 다시 시작 **마지막으로 중지 된 시간**합니다.

Power BI와 hello 권한 부여가 새로 고쳐지지, 녹색 경고에에서 표시 hello 권한 부여 영역 tooreflect hello 문제가 해결 되었습니다.

## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure 스트림 분석 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
