---
title: "Application Insights에서 aaaExport tooPower BI | Microsoft Docs"
description: "분석 쿼리를 Power BI에서 표시할 수 있습니다."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Application Insights에서 Power BI 공급
[Power BI](http://www.powerbi.com/)는 데이터를 분석하는 데 도움을 주고 통찰력을 공유하는 비즈니스 분석 도구 제품군입니다. 모든 장치에서 풍부한 대시보드를 사용할 수 있습니다. [Azure Application Insights](app-insights-overview.md)의 Analytics 쿼리를 포함하여 다양한 원본의 데이터를 포함할 수 있습니다.

Application Insights 데이터 tooPower BI 내보내기의 권장된 하는 세 가지 방법이 있습니다. 개별적으로 또는 함께 사용할 수 있습니다.

* [**Power BI 어댑터**](#power-pi-adapter) - 앱에서 원격 분석의 전체 대시보드를 설정 합니다. hello 일련의 차트 미리 정의 되어 있지만 다른 소스에서 직접 쿼리를 추가할 수 있습니다.
* [**분석 쿼리를 내보내기** ](#export-analytics-queries) -작성할 원하는 쿼리 분석을 사용 하 여 BI tooPower 내보냅니다. 이 쿼리를 다른 데이터와 함께 대시보드에 배치할 수 있습니다.
* [**연속 내보내기 및 스트림 분석** ](app-insights-export-stream-analytics.md) -를 더 많은 작업 tooset이 포함 됩니다. 오랜 시간 동안 tookeep 데이터 원하는 경우에 유용 합니다. 그렇지 않으면 hello 다른 메서드는 것이 좋습니다.

## <a name="power-bi-adapter"></a>Power BI 어댑터
이 방법은 원격 분석의 전체 대시보드를 만듭니다. hello 초기 데이터 집합을 미리 정의 되어 있지만 더 많은 데이터 tooit를 추가할 수 있습니다.

### <a name="get-hello-adapter"></a>Hello 어댑터를 가져옵니다
1. 역시 로그인[Power BI](https://app.powerbi.com/)합니다.
2. **데이터 가져오기**, **Services**, **Application Insights**를 엽니다.
   
    ![Application Insights 데이터 원본에서 가져오기](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Application Insights 리소스의 hello 세부 정보를 제공 합니다.
   
    ![Application Insights 데이터 원본에서 가져오기](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. 가져온 hello 데이터 toobe에 대 일 분 정도 기다립니다.
   
    ![Power BI 어댑터](./media/app-insights-export-power-bi/010.png)

다른 원본 및 분석 쿼리 hello Application Insights 차트를 결합 hello 대시보드를 편집할 수 있습니다. 추가 차트를 가져올 수 있는 시각화 갤러리가 있으며, 각 차트에는 설정할 수 있는 매개 변수가 있습니다.

Hello 초기 가져오기, hello 대시보드 및 보고서 hello 후 tooupdate를 매일 계속 합니다. Hello 데이터 집합에 대해 hello 새로 고침 일정을 제어할 수 있습니다.

## <a name="export-analytics-queries"></a>Analytics 쿼리 내보내기
이 경로 toowrite 수 있습니다. 모든 분석 원하는 쿼리 한 다음 해당 tooa Power BI 대시보드를 내보냅니다. (Hello 어댑터에서 만드는 toohello 대시보드에 추가할 수 있습니다.)

### <a name="one-time-install-power-bi-desktop"></a>한 번: Power BI Desktop을 설치합니다.
tooimport Application Insights 쿼리, Power BI의 데스크톱 버전 hello를 사용 합니다. 하지만 다음 게시할 수 있습니다 toohello 웹 또는 tooyour Power BI 클라우드 작업 영역입니다. 

[Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)을 설치합니다.

### <a name="export-an-analytics-query"></a>Analytics 쿼리 내보내기
1. [Analytics 열기 및 쿼리 작성](app-insights-analytics-tour.md).
2. 테스트 하 고 hello 쿼리를 구체화 하 여 hello 결과에 만족 하면 됩니다.

   **실행 올바르게 분석 하기 전에 내보낼 hello 쿼리 있는지 확인 합니다.**
3. Hello에 **내보내기** 메뉴 선택 **Power BI (M)**합니다. Hello 텍스트 파일을 저장 합니다.
   
    ![Power BI 쿼리 내보내기](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. Power BI Desktop select에서 **데이터 가져오기, 빈 쿼리** 다음 hello에서 쿼리 편집기에서 및 **보기** 선택 **고급 쿼리 편집기**합니다.

    붙여넣기 hello 내보낸 스크립트를 M 언어 hello 고급 쿼리 편집기.

    ![고급 쿼리 편집기](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Tooprovide 자격 증명 tooallow Power BI tooaccess Azure 할 수 있습니다. Microsoft 계정으로 '조직 계정' toosign를 사용 합니다.
   
    ![Application Insights 쿼리 tooenable Power BI toorun Azure 자격 증명 제공](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Tooverify hello 자격 증명이 필요한 경우 명령을 사용 하 여 hello 데이터 원본 설정 메뉴 hello 쿼리 편집기에서. 주의 toospecify hello Power BI에 대 한 사용자 자격 증명과 다를 수 있는 Azure에 사용할 자격 증명 합니다.)
2. 쿼리에 대 한 시각화를 선택 하 고 x 축, y 및 차원 분할에 대 한 hello 필드를 선택 합니다.
   
    ![시각화 선택](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. 보고서 tooyour Power BI 클라우드 작업 영역을 게시 합니다. 여기에서 다른 웹 페이지에 동기화된 버전을 포함할 수 있습니다.
   
    ![시각화 선택](./media/app-insights-export-power-bi/publish-power-bi.png)
4. 간격에 따라 hello 보고서를 수동으로 새로 고침 또는 hello 옵션 페이지에서 예약 된 새로 고침을 설정 합니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="401-or-403-unauthorized"></a>401 또는 403 권한 없음 
업데이트되지 않은 토큰을 새로 고치는 경우 발생할 수 있습니다. 에 이러한 단계 tooensure를 시도 하십시오. 액세스 권한이 refershing hello 자격 증명이 작동 하지 않는 경우 지원 티켓을 개시 하세요.

1. Hello Azure 포털에 로그인 하 고 hello 리소스에 액세스할 수 있는지 확인
2. 대시보드 hello에 대 한 toorefresh hello 자격 증명을 시도 하십시오

### <a name="502-bad-gateway"></a>502 잘못된 게이트웨이
일반적으로 너무 많은 데이터를 반환하는 분석 쿼리가 원인입니다. 더 작은 시간 범위를 사용 하는 것이 좋습니다 또는 hello를 사용 하 여 [전](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) 또는 [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) 함수만 해당 [프로젝트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello 필요한 필드입니다.

Hello 사용을 고려해 야 hello 분석 쿼리에서에서 들어오는 hello 데이터 집합을 줄여 요구 사항을 충족 하지 않는 경우 [API](https://dev.applicationinsights.io/documentation/overview) toopull 더 큰 데이터 집합입니다. 다음은 방법 tooconvert hello M 쿼리 내보내기 toouse hello API에 대 한 지침입니다.

1. [API 키](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID) 만들기
2. 업데이트 hello 대체 하 여 분석에서 내보낸 Power BI M 스크립트 hello ARM AI API URL (아래 예제 참조)
   * 대체 **https://management.azure.com/subscriptions/...**
   * **https://api.applicationinsights.io/beta/apps/...**
3. 마지막으로, 자격 증명 toobasic를 업데이트 하 고 API 키를 사용 하 여
  

**기존 스크립트**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**업데이트된 스크립트**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>샘플링 정보
응용 프로그램에서 많은 양의 데이터를 하는 경우 hello 적응 샘플링 기능 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다. hello 수동으로 설정 하면 샘플링 hello SDK 또는 수집 중에 마찬가지입니다. [샘플링에 대해 자세히 알아봅니다.](app-insights-sampling.md)


## <a name="next-steps"></a>다음 단계
* [Power BI - 알아보기](http://www.powerbi.com/learning/)
* [Analytics 자습서](app-insights-analytics-tour.md)

