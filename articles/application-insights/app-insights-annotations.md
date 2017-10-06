---
title: "Application Insights에 대 한 주석을 aaaRelease | Microsoft Docs"
description: "배포 추가 하거나 표식 Application Insights에서 tooyour 메트릭 탐색기 차트를 작성 합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Application Insights의 메트릭 차트에 대한 주석
[메트릭 탐색기](app-insights-metrics-explorer.md) 차트의 주석은 새 빌드를 배포한 위치 또는 다른 중요한 이벤트를 표시합니다. 이러한 사용 하면 쉽게 toosee 변경 내용을 응용 프로그램의 성능에 영향을 줄에 있는지 여부를 있습니다. Hello에서 자동으로 생성 [시스템을 작성 하는 Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs)합니다. 만들 수도 있습니다 주석 tooflag 하 여 원하는 모든 이벤트 [PowerShell에서 만드는](#create-annotations-from-powershell)합니다.

![서버 응답 시간과 상관 관계가 표시된 주석 예제](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>VSTS 빌드를 사용한 릴리스 주석

릴리스 주석은 hello 클라우드 기반 빌드의 기능 및 Visual Studio Team Services의 서비스를 해제 합니다. 

### <a name="install-hello-annotations-extension-one-time"></a>Hello 주석 확장 (한 번) 설치
toobe 수 toocreate 릴리스 주석 tooinstall 하나 필요 합니다 hello의 많은 팀 서비스 확장에서 사용할 수 있는 Visual Studio 마켓플레이스를 hello 합니다.

1. Tooyour 로그인 [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) 프로젝트.
2. Visual Studio 마켓플레이스에서 [hello 릴리스 주석 확장을 가져오려면](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), tooyour Team Services 계정을 추가 합니다.

![Team Services 웹 페이지의 오른쪽 위에서 마켓플레이스를 엽니다. Visual Team Services를 선택하고 빌드 및 릴리스에서 자세히 보기를 선택합니다.](./media/app-insights-annotations/10.png)

하기만 하면 toodo 한 번이 Visual Studio Team Services 계정에 대 한 합니다. 이제 계정의 모든 프로젝트에 대해 릴리스 주석을 구성할 수 있습니다. 

### <a name="configure-release-annotations"></a>릴리스 주석 구성

각 VSTS 릴리스 템플릿에 대해 tooget 별도 API 키가 필요 합니다.

1. Toohello 로그인 [Microsoft Azure 포털](https://portal.azure.com) 응용 프로그램을 모니터링 하는 hello Application Insights 리소스를 엽니다. (또는 아직 만들지 않은 경우 [지금 만듭니다](app-insights-overview.md).)
2. **API 액세스**, **Application Insights ID**를 차례로 엽니다.
   
    ![portal.azure.com에서 Application Insights 리소스를 열고 설정을 선택합니다. API 액세스를 엽니다. Hello 응용 프로그램 ID를 복사 합니다.](./media/app-insights-annotations/20.png)

4. 별도 브라우저 창에서 열기 (또는 만들기) Visual Studio Team Services에서 배포를 관리 하는 hello 릴리스 템플릿을 합니다. 
   
    태스크를 추가 하 고 hello 메뉴에서 hello 응용 프로그램 통찰력 릴리스 주석 작업을 선택 합니다.
   
    붙여넣기 hello **응용 프로그램 Id** hello API 액세스 블레이드에서에서 복사 합니다.
   
    ![Visual Studio Team Services에서 릴리스를 열고 릴리스 정의를 선택하고 편집을 선택합니다. 작업 추가를 클릭하고 Application Insights 릴리스 주석을 선택합니다. 붙여넣기 hello 응용 프로그램 통찰력 id입니다.](./media/app-insights-annotations/30.png)
4. 집합 hello **APIKey** 필드 tooa 변수 `$(ApiKey)`합니다.

5. Hello Azure 창으로 돌아가서 새 API 키를 만들고는 해당 복사본을 사용 합니다.
   
    ![Hello Azure 창에에서 대 한 API 액세스 블레이드 hello에서 API 키 만들기를 클릭 합니다. 설명을 입력하고 주석 쓰기를 선택하고 키 생성을 클릭합니다. Hello 새 키를 복사 합니다.](./media/app-insights-annotations/40.png)

6. Hello 릴리스 템플릿의 hello 구성 탭을 엽니다.
   
    `ApiKey`에 대한 변수 정의를 만듭니다.
   
    API 키 toohello를 ApiKey 변수 정의 붙여 넣습니다.
   
    ![Hello Team Services 창의 hello 구성 탭을 선택 하 고 변수 추가 클릭 합니다. Hello 이름 tooApiKey 설정 값 hello에 방금 생성 된 hello 키를 붙여 넣고 hello 자물쇠 아이콘을 클릭 합니다.](./media/app-insights-annotations/50.png)
7. 마지막으로, **저장** hello 릴리스 정의 합니다.


## <a name="view-annotations"></a>주석 보기
이제 hello 릴리스 템플릿 toodeploy 새 릴리스를 사용할 때마다 주석을 받게 될 tooApplication Insights 합니다. hello 주석 메트릭 탐색기에서 차트에 표시 됩니다.

요청자, 소스 제어 분기, 릴리스 정의 환경 등을 포함 하는 hello 릴리스에 대 한 모든 주석 표식 tooopen 정보를 클릭 합니다.

![릴리스 주석 마커를 클릭합니다.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>PowerShell에서 사용자 지정 주석 만들기
VS Team 시스템을 사용하지 않고 원하는 모든 프로세스에서 주석을 만들 수도 있습니다. 


1. Hello의 로컬 복사본을 만들 [GitHub에서 Powershell 스크립트](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)합니다.

2. Hello 응용 프로그램 ID를 가져오고 hello API 액세스 블레이드에서에서 API 키를 만듭니다.

3. 이러한 hello 스크립트를 호출 합니다.

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

지난 hello에 대 한 예를 들어 toocreate 주석을 쉽게 toomodify hello 스크립트는

## <a name="next-steps"></a>다음 단계

* [작업 항목 만들기](app-insights-diagnostic-search.md#create-work-item)
* [PowerShell을 사용한 자동화](app-insights-powershell.md)
