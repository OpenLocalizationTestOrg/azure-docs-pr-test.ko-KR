---
title: "Power BI 포함 Azure에서 보고서에 대 한 보기와 편집 모드 간에 aaaToggle | Microsoft Docs"
description: "자세한 방법을 Power BI 포함 내 보고서에 대 한 보기와 편집 모드 간에 tootoggle 합니다."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>Power BI Embedded에서 보고서에 대해 보기 및 편집 모드 간 전환

자세한 방법을 Power BI 포함 내 보고서에 대 한 보기와 편집 모드 간에 tootoggle 합니다.

## <a name="creating-an-access-token"></a>액세스 토큰 만들기

Toocreate hello 기능 tooboth 보기 및 보고서를 편집 하면 액세스 토큰이 필요 합니다. tooedit 보고서를 저장 해야 hello 및 **Report.ReadWrite** 권한 토큰입니다. 자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.

> [!NOTE]
> Tooedit를 허용 되 고 변경 내용을 tooan 기존 보고서를 저장 합니다. Hello 함수를 지원할도 원하면 **다른 이름으로 저장**, toosupply 추가 권한이 필요 합니다. 자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>Embed 구성

Toosupply 사용 권한 및 save 편집 모드에 있을 때 단추 순서 toosee hello에 viewMode 필요 합니다. 자세한 내용은 [Embed 구성 정보](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)를 참조하세요.

예를 들어 JavaScript에서 다음을 수행합니다.

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

이 기반으로 하는 보기 모드에서 tooembed hello 보고서 나타냅니다 **viewMode** 너무 설정**모델. ViewMode.View**합니다.

## <a name="view-mode"></a>보기 모드

편집 모드에 있는 경우 JavaScript tooswitch 보기 모드에 따라 hello를 사용할 수 있습니다.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>편집 모드

모드는 보이는 경우 hello JavaScript tooswitch 편집 모드에 따라 사용할 수 있습니다.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>참고 항목

[샘플 시작](power-bi-embedded-get-started-sample.md)  
[보고서 포함](power-bi-embedded-embed-report.md)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[PowerBI-CSharp Git 리포지토리](https://github.com/Microsoft/PowerBI-CSharp)  
[PowerBI-Node Git 리포지토리](https://github.com/Microsoft/PowerBI-Node)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)
