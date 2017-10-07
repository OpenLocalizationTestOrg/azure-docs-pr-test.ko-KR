---
title: "Power BI 포함 Azure에서 aaaSave 보고서 | Microsoft Docs"
description: "Power BI에서 보고서를 toosave 포함 하는 방법에 대해 알아봅니다. 이 성공적으로 순서 toowork에 적절 한 사용 권한이 필요합니다."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>Power BI Embedded에서 보고서 저장

Power BI에서 보고서를 toosave 포함 하는 방법에 대해 알아봅니다. 이 성공적으로 순서 toowork에 적절 한 사용 권한이 필요합니다.

Power BI Embedded 내에서 기존 보고서를 편집하고 저장할 수 있습니다. 새 보고서를 만들 하 고 하나는 새 보고서 toocreate로 저장할 수도 있습니다.

순서 toosave 보고서의에서 첫 번째 hello hello 오른쪽 범위와 특정 보고서에 대 한 toocreate 토큰을 필요.

* Report.ReadWrite 범위 저장 tooenable가 필요
* 저장으로 tooenable Report.Read 및 Workspace.Report.Copy 범위 증명이 있습니다.
* tooenable 저장 하 고 저장 다른 이름으로 Report.ReadWrite와 Workspace.Report.Copy requierd

각각 순서 tooenable hello 저장/저장 오른쪽에서 파일 메뉴에서 단추가 필요 tooprovide hello 마우스 오른쪽 단추로 hello Embed 구성에 대 한 사용 권한을 포함 하면 보고서를 hello 때:

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> 액세스 토큰 hello 적절 한 범위를도 필요합니다. 자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.

## <a name="embed-report-in-edit-mode"></a>편집 모드에서 보고서 포함

보겠습니다 예: 앱 내 tooEmbed 편집 모드에서 보고서를 원하는 toodo 되었으므로 Embed 구성에서 hello 오른쪽 속성을 전달 powerbi.embed() 호출 합니다. 편집 모드에 있을 때 단추로 toosupply 사용 권한 및 순서 toosee hello에 저장 하 고 저장에서 viewMode 필요 합니다. 자세한 내용은 [Embed 구성 정보](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)를 참조하세요.

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
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
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

이제 보고서가 편집 모드에서 앱에 포함됩니다.

## <a name="save-report"></a>보고서 저장

Embbeding hello 보고서 편집 모드 오른쪽 토큰 hello 및 사용 권한으로 후 hello 파일 메뉴에서 또는 javascript에서 hello 보고서를 저장할 수 있습니다.

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>다른 이름으로 저장

```
// Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> *다른 이름으로 저장* 이후에만 새 보고서가 만들어집니다. Hello 저장 hello 캔버스 편집 모드와 하지 hello 새 보고서에 hello 오래 된 보고서를 계속 표시 됩니다. Tooembed hello 새 보고서를 생성 해야 합니다. 이렇게 하려면 보고서가 만들어질 때마다 새 액세스 토큰이 필요합니다.

그런 다음 이후의 tooload hello 새 보고서를 해야 합니다는 *다른 이름으로 저장*합니다. 이 비슷한 tooembedding 모든 보고서입니다.

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a>참고 항목

[샘플 시작](power-bi-embedded-get-started-sample.md)  
[보고서 포함](power-bi-embedded-embed-report.md)  
[데이터 집합에서 새 보고서 만들기](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)

