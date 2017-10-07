---
title: "새 Azure Application Insights 리소스 aaaCreate | Microsoft Docs"
description: "새 라이브 응용 프로그램에 대한 Application Insights 모니터링을 수동으로 설정합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Application Insights 리소스 만들기
Azure Application Insights는 Microsoft Azure *리소스*에 응용 프로그램에 대한 데이터를 표시합니다. 새 리소스 만들기의 일부가 되 [Application Insights toomonitor 새 응용 프로그램 설정][start]합니다. 대부분의 경우에서 리소스를 만들고 여 수행할 수 있습니다 자동으로 hello IDE. 하지만 경우에 따라 리소스를 만들 수동으로-toohave 개발 및 프로덕션에 대 한 별도 리소스 응용 프로그램의 예를 들어 만듭니다.

Hello 리소스를 만든 후 하면의 계측 키를 가져오고 hello 응용 프로그램에 해당 tooconfigure hello SDK를 사용 합니다. hello 리소스 키 링크 hello 원격 분석 toohello 리소스입니다.

## <a name="sign-up-toomicrosoft-azure"></a>TooMicrosoft Azure 등록
[Microsoft 계정이 없는 경우 계정을 만듭니다](http://live.com). Outlook.com, OneDrive, Windows Phone 또는 XBox Live 등의 서비스를 이용하는 경우 Microsoft 계정이 이미 있습니다.

또한 해야 구독 너무[Microsoft Azure](http://azure.com)합니다. 팀 또는 조직에 Azure 구독이 있으면 hello 소유자 추가할 수 있습니다 tooit, Windows Live ID를 사용 하 여 사용하는 구독에 대해서만 요금이 부과됩니다. hello 기본 기본 계획 일정량 무료로 실험용으로 사용할 수 있습니다.

액세스 tooa 구독을가지고 때 tooApplication Insights에 로그인 [http://portal.azure.com](https://portal.azure.com), Live ID toologin를 사용 합니다.

## <a name="create-an-application-insights-resource"></a>Application Insights 리소스 만들기
Hello에 [portal.azure.com](https://portal.azure.com), Application Insights 리소스를 추가 합니다.

![새로 만들기, Application Insights 클릭](./media/app-insights-create-new-resource/01-new.png)

* **응용 프로그램 종류** hello 개요 블레이드 및에서 사용할 수 있는 hello 속성에 표시 되는 내용에 영향을 줍니다 [메트릭 탐색기][metrics]합니다. 앱 유형이 표시되지 않으면 일반을 선택합니다.
* **구독** 은 Azure의 지불 계정입니다.
* **리소스 그룹** 은 액세스 제어와 같은 속성을 관리하기 위한 편의 기능입니다. 이미 다른 Azure 리소스를 만든 경우 선택할 수 있습니다 tooput이 새 리소스 hello에 동일한 그룹입니다.
* **위치** 는 데이터를 보관하는 곳입니다.
* **Pin toodashboard** 리소스에 대 한 빠른 액세스 타일 Azure 홈 페이지에 배치 합니다. 권장됩니다.

앱이 만들어지면 새 블레이드가 열립니다. 이 블레이드에서 앱의 성능 및 사용량 데이터를 볼 수 있습니다. 

tooget 백 tooit 다음 tooAzure에 로그인 할 때 응용 프로그램의 빠른 시작 타일 hello에 대 한 확인은 보드 (홈 화면)를 시작 합니다. 찾아보기 toofind 키를 누르거나 것입니다.

## <a name="copy-hello-instrumentation-key"></a>Hello 계측 키 복사
hello 계측 키 만든 hello 리소스를 식별 합니다. 해야 toogive toohello SDK.

![Essentials, hello 계측 키, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>응용 프로그램에서 hello SDK 설치
응용 프로그램에서 hello Application Insights SDK를 설치 합니다. 이 단계는 응용 프로그램의 hello 형식에 따라 크게 다릅니다. 

계측 키 tooconfigure hello를 사용 하 여 [SDK 응용 프로그램에서 설치 하는 hello][start]합니다.

hello SDK toowrite 코드 필요 없이 원격 분석을 전송 하는 표준 모듈을 포함 합니다. tootrack 사용자 작업 또는 문제를 보다 자세히 진단할 [hello API를 사용 하 여] [ api] toosend 직접 원격 분석 합니다.

## <a name="monitor"></a>원격 분석 데이터 보기
빠른 닫기 hello hello Azure 포털에서에서 블레이드 tooreturn tooyour 응용 프로그램 블레이드를 시작 합니다.

검색 타일 toosee hello 클릭 [진단 검색][diagnostic]hello 첫 번째 이벤트가 표시 되는 위치, 합니다. 

더 많은 데이터를 보려면 몇 초 후에 **새로 고침**을 클릭합니다.

## <a name="creating-a-resource-automatically"></a>자동으로 리소스 만들기
작성할 수 있습니다는 [PowerShell 스크립트](app-insights-powershell.md) toocreate 리소스 자동으로 합니다.

## <a name="next-steps"></a>다음 단계
* [대시보드 만들기](app-insights-dashboards.md)
* [진단 검색](app-insights-diagnostic-search.md)
* [메트릭 탐색](app-insights-metrics-explorer.md)
* [분석 쿼리 작성](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

