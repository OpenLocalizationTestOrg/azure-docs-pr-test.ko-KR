---
title: aaaMicrosoft Dynamics CRM, Azure Application Insights | Microsoft Docs
description: "Application Insights를 사용하여 Microsoft Dynamics CRM Online에서 원격 분석 가져오기 설정, 데이터 가져오기, 시각화 및 내보내기의 연습입니다."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>연습: Application Insights를 사용하여 Microsoft Dynamics CRM Online 작업에 대한 원격 분석 설정
이 문서에서는 어떻게 tooget 원격 분석 데이터를 [Microsoft Dynamics CRM Online](https://www.dynamics.com/) 를 사용 하 여 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)합니다. Application Insights 스크립트 tooyour 응용 프로그램을 추가, 데이터 및 데이터 시각화 캡처 hello 전체 과정을 단계별로 살펴보겠습니다.

> [!NOTE]
> [Hello 샘플 솔루션을 찾아보기](https://dynamicsandappinsights.codeplex.com/)합니다.
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Application Insights toonew 또는 기존 CRM Online 인스턴스에 추가 합니다.
toomonitor 응용 프로그램에 Application Insights SDK tooyour 응용 프로그램을 추가 합니다. hello SDK 원격 분석 toohello 보냅니다 [Application Insights 포털](https://portal.azure.com), 여기서 강력한 분석 및 진단 도구를 사용 하거나 내보낼 수 있습니다 hello 데이터 toostorage 합니다.

### <a name="create-an-application-insights-resource-in-azure"></a>Azure에서 Application Insights 리소스 만들기
1. [Microsoft Azure에서 계정](http://azure.com/pricing)을 만듭니다. 
2. Hello에 로그인 [Azure 포털](https://portal.azure.com) 새 Application Insights 리소스를 추가 합니다. 데이터가 처리되어 표시될 위치입니다.
   
    ![+, 개발자 서비스, Application Insights를 클릭합니다.](./media/app-insights-sample-mscrm/01.png)
   
    ASP.NET hello 응용 프로그램 유형으로 선택 합니다.
3. Hello 시작 페이지를 열고 열기 "모니터 및 클라이언트 쪽 진단"입니다.
   
    ![웹 페이지에서 삽입에 대한 코드 조각](./media/app-insights-sample-mscrm/03.png)

**Hello 코드 페이지를 열어** 다른 브라우저 창에서 다음 단계를 hello 수행 하는 동안 합니다. 곧 hello 코드가 필요 합니다. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Microsoft Dynamics CRM의 JavaScript 웹 리소스 만들기
1. CRM Online 인스턴스를 열고 관리자 권한으로 로그인합니다.
2. Microsoft Dynamics CRM 설정, 사용자 지정, 사용자 지정 hello 시스템을 열려면
   
    ![Microsoft Dynamics CRM 설정](./media/app-insights-sample-mscrm/04.png)
   
    ![설정 > 사용자 지정](./media/app-insights-sample-mscrm/05.png)

    ![Hello 시스템 옵션을 사용자 지정](./media/app-insights-sample-mscrm/06.png)

1. JavaScript 리소스를 만듭니다.
   
    ![새 웹 리소스 대화 상자](./media/app-insights-sample-mscrm/07.png)
   
    이름을 선택 **스크립트 (JScript)** 및 열기 hello 텍스트 편집기입니다.
   
    ![열기 hello 텍스트 편집기](./media/app-insights-sample-mscrm/08.png)
2. Application Insights에서 hello 코드를 복사 합니다. 복사 하는 동안 있는지 tooignore 스크립트 태그를 확인 합니다. 아래 스크린샷을 참조하세요.
   
    ![계측 키 설정](./media/app-insights-sample-mscrm/09.png)
   
    hello 코드 포함 Application insights 리소스를 식별 하는 hello 계측 키가 됩니다.
3. 저장하고 게시합니다.
   
    ![저장 및 게시](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>계측 양식
1. Microsoft CRM Online에서 hello 계정 양식을 엽니다
   
    ![계정 양식](./media/app-insights-sample-mscrm/11.png)
2. Hello 폼 속성 열기
   
    ![양식 속성](./media/app-insights-sample-mscrm/12.png)
3. Hello 만든 JavaScript 웹 리소스를 추가 합니다.
   
    ![추가 메뉴](./media/app-insights-sample-mscrm/13.png)
   
    ![Hello 웹 리소스 추가](./media/app-insights-sample-mscrm/14.png)
4. 양식 사용자 지정 항목을 저장하고 게시합니다.

## <a name="metrics-captured"></a>캡처된 메트릭
이제 hello 폼에 대 한 원격 분석 캡처를 설정 했습니다. 사용할 때마다 tooyour Application Insights 리소스로 데이터가 전송 됩니다.

다음은 표시 하는 hello 데이터의 샘플입니다.

#### <a name="application-health"></a>응용 프로그램 상태
![예제 페이지 로드 시간](./media/app-insights-sample-mscrm/15.png)

![예제 페이지 보기 차트](./media/app-insights-sample-mscrm/16.png)

브라우저 예외:

![브라우저 예외 차트](./media/app-insights-sample-mscrm/17.png)

Hello 차트 tooget 자세히를 클릭 합니다.

![예외 목록](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>사용
![사용자, 세션 및 페이지 보기](./media/app-insights-sample-mscrm/19.png)

![세션 차트](./media/app-insights-sample-mscrm/20.png)

![브라우저 버전](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>브라우저
![페이지 로드 시간 분석](./media/app-insights-sample-mscrm/22.png)

![브라우저 버전별 세션 수](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>지리적 위치
![국가별 세션 수](./media/app-insights-sample-mscrm/24.png)

![국가별 세션 및 사용자](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>내부 페이지 보기 요청
![페이지 보기 요약](./media/app-insights-sample-mscrm/26.png)

![페이지 보기 이벤트 검색](./media/app-insights-sample-mscrm/27.png)

![비슷한 페이지 보기](./media/app-insights-sample-mscrm/28.png)

![페이지 보기 속성](./media/app-insights-sample-mscrm/29.png)

![세션별 페이지](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>샘플 코드
[Hello 샘플 코드를 찾아보려면](https://dynamicsandappinsights.codeplex.com/)합니다.

## <a name="power-bi"></a>Power BI
경우에 자세히 분석을 수행할 수 있습니다 있습니다 [hello 데이터 tooMicrosoft Power BI 내보내기](app-insights-export-power-bi.md)합니다.

## <a name="sample-microsoft-dynamics-crm-solution"></a>샘플 Microsoft Dynamics CRM 솔루션
[다음은 Microsoft Dynamics CRM에서 구현 된 hello 샘플 솔루션](https://dynamicsandappinsights.codeplex.com/)합니다.

## <a name="learn-more"></a>자세한 정보
* [Application Insights란?](app-insights-overview.md)
* [웹 페이지용 Application Insights](app-insights-javascript.md)
* [추가 샘플 및 연습](app-insights-code-samples.md)
