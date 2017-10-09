---
title: "Azure Application Insights에서 스트림 분석을 사용 하 여 aaaExport | Microsoft Docs"
description: "스트림 분석 지속적으로 변형할 수, Application Insights에서 내보내는 hello 데이터 필터 및 경로입니다."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Application Insights에서 내보내는 데이터를 사용 하 여 스트림 분석 tooprocess
[Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 는 데이터 처리를 위한 이상적인 도구 hello [Application Insights에서 내보낸](app-insights-export-telemetry.md)합니다. Stream Analytics는 다양한 원본의 데이터를 가져와서 변환 하 고 hello 데이터를 필터링 하 고 tooa 다양 한 싱크 라우팅할 수 것입니다.

이 예제에서는 이름 바꾸기, Application Insights에서 데이터를 가져와서 hello 필드 중 일부를 처리 하 고 Power BI로 파이프 하는 어댑터를 만들어 보겠습니다.

> [!WARNING]
> 더 나은 훨씬 손쉽고 없는 [권장 방법으로 Power BI에서 toodisplay Application Insights 데이터](app-insights-export-power-bi.md)합니다. hello 여기에서 설명 하는 경로는 예제 tooillustrate 방금 tooprocess 데이터를 내보내는 방법입니다.
> 
> 

![SA tooPBI 통해 내보내기에 대 한 블록 다이어그램](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Azure에서 저장소 만들기
연속 내보내기를 먼저 toocreate hello 저장소가 필요 하므로 항상 데이터 tooan Azure 저장소 계정을 출력 합니다.

1. Hello에 구독에서 "클래식" 저장소 계정을 만드는 [Azure 포털](https://portal.azure.com)합니다.
   
   ![Azure 포털에서 새로 만들기, 데이터, 저장소 선택](./media/app-insights-export-stream-analytics/030.png)
2. 컨테이너 만들기
   
    ![Hello 새 저장소를 선택 하세요.를 hello 컨테이너 타일 및 추가 클릭 합니다.](./media/app-insights-export-stream-analytics/040.png)
3. Hello 저장소 액세스 키를 복사 합니다.
   
    해야 곧 tooset hello 입력된 toohello 스트림 분석 서비스를 구성 합니다.
   
    ![Hello 저장소에서 설정, 키를 열고 hello 기본 액세스 키의 복사본](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>연속 내보내기를 tooAzure 저장소 시작
[연속 내보내기](app-insights-export-telemetry.md) 는 Application Insights에서 Azure 저장소로 데이터를 이동합니다.

1. Hello Azure 포털에서에서 응용 프로그램에 대해 만든 toohello Application Insights 리소스를 찾습니다.
   
    ![찾아보기, Application Insights, 응용 프로그램 선택](./media/app-insights-export-stream-analytics/050.png)
2. 연속 내보내기를 만듭니다.
   
    ![설정, 연속 내보내기, 추가를 차례로 선택](./media/app-insights-export-stream-analytics/060.png)

    이전에 만든 hello 저장소 계정을 선택 합니다.

    ![Hello 내보내기 대상을 설정합니다](./media/app-insights-export-stream-analytics/070.png)

    Toosee 원하는 hello 이벤트 유형을 설정 합니다.

    ![이벤트 유형 선택](./media/app-insights-export-stream-analytics/080.png)

1. 일부 데이터가 누적되도록 합니다. 한동안 사용자가 응용 프로그램을 사용하도록 놓아둡니다. 원격 분석이 제공되어 [메트릭 탐색기](app-insights-metrics-explorer.md)에서 통계 차트가, [진단 검색](app-insights-diagnostic-search.md)에서 개별 이벤트가 표시됩니다. 
   
    및 또한 hello 데이터는 tooyour 저장소를 내보냅니다. 
2. Hello 내보낸 데이터를 검사 합니다. Visual Studio에서 **보기/클라우드 탐색기**를 선택하고 Azure/저장소를 엽니다. (Tooinstall hello Azure SDK이 메뉴 옵션에 없을 경우 해야: hello 새 프로젝트 대화 상자를 열고 엽니다 Visual C# / 클라우드 / Microsoft Azure SDK for.NET 가져오기.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Hello 응용 프로그램 이름 및 계측 키에서 파생 된 hello 경로 이름의 hello 공통 부분을 기록해 둡니다. 

hello 이벤트는 JSON 형식의 tooblob 파일 기록 됩니다. 각 파일에는 하나 이상의 이벤트가 있을 수 있습니다. 따라서 싶습니다 tooread hello 이벤트 데이터와 원하는 hello 필드를 필터링 합니다. 모든 종류의 hello 데이터로 수행 하는 항목이 없지만 현재 계획으로 오늘 toouse 스트림 분석 toopipe hello 데이터 tooPower BI는 있습니다.

## <a name="create-an-azure-stream-analytics-instance"></a>Azure 스트림 분석 인스턴스 만들기
Hello에서 [클래식 Azure 포털](https://manage.windowsazure.com/)hello Azure 스트림 분석 서비스를 선택 하 고 새 스트림 분석 작업 만들기:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Hello 새 작업을 만든 경우 해당 세부 정보를 확장 합니다.

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Blob 위치 설정
연속 내보내기 blob의 tootake 입력으로 설정 합니다.

![](./media/app-insights-export-stream-analytics/120.png)

이제 기본 액세스 키 hello 앞에서 기록해 둔 저장소 계정에서 필요 합니다. 저장소 계정 키 hello로 설정 합니다.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>경로 접두사 패턴 설정
![](./media/app-insights-export-stream-analytics/140.png)

**있는지 tooset hello 날짜 형식 tooYYYY-월-일 (포함 대시) 수입니다.**

hello 경로 접두사 패턴 스트림 분석 hello 저장소의 hello 입력된 파일을 찾는 하는 위치를 지정 합니다. Tooset 필요한 것 연속 내보내기가 toocorrespond toohow hello 데이터를 저장 합니다. 다음과 같이 설정합니다.

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

이 예제에서:

* `webapplication27`hello Application Insights 리소스의 hello 이름인 **모두 소문자로**합니다.
* `1234...`hello Application Insights 리소스의 계측 키 hello **대시 생략**합니다. 
* `PageViews`hello 형식인 원하는 tooanalyze 데이터입니다. 연속 내보내기에서 설정한 hello 필터에 대 한 hello 사용 가능한 형식에 따라 달라 집니다. 사용 가능한 다른 유형 hello 내보낸된 데이터 toosee hello를 검사 하 고 hello 참조 [데이터 모델을 내보낼](app-insights-export-data-model.md)합니다.
* `/{date}/{time}` 은 문자로 기록된 패턴입니다.

> [!NOTE]
> 그러면 오른쪽 hello 경로 가져올 hello 저장소 toomake를 검사 합니다.
> 
> 

### <a name="finish-initial-setup"></a>초기 설치 완료
Hello 직렬화 형식을 확인 합니다.

![마법사 확인 후 닫기](./media/app-insights-export-stream-analytics/150.png)

Hello 마법사를 닫고 설치 프로그램 toocomplete hello에 대 한 대기 합니다.

> [!TIP]
> Hello 샘플 명령은 toodownload 일부 데이터를 사용 합니다. 지속적으로 테스트 샘플 toodebug 쿼리입니다.
> 
> 

## <a name="set-hello-output"></a>집합 hello 출력
이제 작업을 선택 하 고 hello 출력을 설정 합니다.

![Hello 새 채널을 선택, 출력, 추가, Power BI를 클릭 합니다.](./media/app-insights-export-stream-analytics/160.png)

제공 프로그램 **회사 또는 학교 계정** tooauthorize 스트림 분석 tooaccess 사용자 Power BI 리소스입니다. 그런 다음 만들 hello 출력 하 고 hello 대상 Power BI 데이터 집합 및 테이블에 대 한 이름입니다.

![이름 3개를 생성합니다.](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>집합 hello 쿼리
hello 쿼리 입력된 toooutput에서 hello 번역을 제어합니다.

![Hello 작업을 선택 하 고 쿼리를 클릭 합니다. Hello 샘플을 아래에 붙여 넣습니다.](./media/app-insights-export-stream-analytics/180.png)

Hello 테스트 함수 toocheck hello 오른쪽 출력을 가져올 수를 사용 합니다. Hello 입력 페이지에서 수행한 hello 예제 데이터를 지정 합니다. 

### <a name="query-toodisplay-counts-of-events"></a>쿼리 이벤트 toodisplay 수
이 쿼리 붙여넣기:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* 내보내기 입력은 hello 별칭 toohello 스트림 입력 적용 했습니다.
* pbi 출력은 정의한 hello 출력 별칭
* 사용 하 여 [외부 적용 GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) hello 이벤트 이름은 중첩 된 JSON arrray 이므로 합니다. 그런 다음 hello 선택 선택 hello hello hello 기간에에서 같은 이름의 인스턴스 수의 개수와 함께 이벤트 이름입니다. hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) 절 기간을 1 분으로 hello 요소를 그룹화 합니다.

### <a name="query-toodisplay-metric-values"></a>쿼리 toodisplay 메트릭 값
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* 이 쿼리는 hello 메트릭 원격 분석 tooget hello 이벤트 시간 및 hello 메트릭 값으로 드릴 합니다. 외부 적용 GetElements 패턴 tooextract hello 행 hello를 사용 하도록 배열, 내부 hello 메트릭 값은입니다. 이 경우 "myMetric"는 hello 이름 hello 메트릭입니다. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>차원 속성의 tooinclude 값 쿼리
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* 이 쿼리 hello 차원 배열에서 고정된 된 인덱스에 특정 차원에 따라 없이 hello 차원 속성의 값을 포함 합니다.

## <a name="run-hello-job"></a>Hello 작업 실행
Hello toostart hello 작업에서 이전에 날짜를 선택할 수 있습니다. 

![Hello 작업을 선택 하 고 쿼리를 클릭 합니다. Hello 샘플을 아래에 붙여 넣습니다.](./media/app-insights-export-stream-analytics/190.png)

Hello 작업이 실행 될 때까지 기다립니다.

## <a name="see-results-in-power-bi"></a>Power BI에 결과를 참조하세요.
> [!WARNING]
> 더 나은 훨씬 손쉽고 없는 [권장 방법으로 Power BI에서 toodisplay Application Insights 데이터](app-insights-export-power-bi.md)합니다. hello 여기에서 설명 하는 경로는 예제 tooillustrate 방금 tooprocess 데이터를 내보내는 방법입니다.
> 
> 

작업 또는 학교 계정 및 선택 hello 데이터 집합 및 hello 스트림 분석 작업의 hello 출력으로 정의 되어 테이블을 사용 하 여 Power BI를 엽니다.

![Power BI에서 데이터 집합과 필드를 선택합니다.](./media/app-insights-export-stream-analytics/200.png)

이제 [Power BI](https://powerbi.microsoft.com)의 보고서 및 대시보드에서 이 데이터 집합을 사용할 수 있습니다.

![Power BI에서 데이터 집합과 필드를 선택합니다.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>데이터가 없나요?
* 확인을 [hello 날짜 형식 설정](#set-path-prefix-pattern) 올바르게 tooYYYY-월-일 (대시) 사용 합니다.

## <a name="video"></a>비디오
Noam Ben Zeev tooprocess Stream Analytics을 사용 하 여 데이터를 내보내는 방법을 보여 줍니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>다음 단계
* [연속 내보내기](app-insights-export-telemetry.md)
* [세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

