---
title: "Power BI 포함 Azure에서 데이터 집합에서 새 보고서 aaaCreate | Microsoft Docs"
description: "Power BI Embedded 보고서는 이제 자체 응용 프로그램의 데이터 집합에서 만들 수 있습니다."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Power BI Embedded의 데이터 집합에서 새 보고서 만들기

Power BI Embedded 보고서는 이제 자체 응용 프로그램의 데이터 집합에서 만들 수 있습니다. 

hello 인증 메서드는 보고서의 toothat 포함 합니다. 액세스 토큰을 특정 tooa 데이터 집합은 기반으로 합니다. PowerBI.com에 사용되는 토큰은AAD(Azure Active Directory)에서 발급되고 Power BI Embedded 토큰은 사용자의 자체 서비스에서 발급됩니다.

Hello createing 포함 된 보고서를 특정 데이터 집합에 대해 발급 한 토큰 됩니다. 토큰을 연결 해야 할지 hello로 URL을 포함 hello에 동일한 요소 tooensure 각각에 고유한 토큰이 있습니다. 순서로 toocreate 포함 된 보고서, *Dataset.Read 및 Workspace.Report.Create* hello 액세스 토큰의 범위를 제공 해야 합니다.

## <a name="create-access-token-needed-toocreate-new-report"></a>액세스 토큰 필요한 toocreate 새 보고서 만들기

Power BI Embedded는 HMAC 서명 JSON Web Token에 해당하는 Embed 토큰을 사용합니다. hello 토큰은 Azure Power BI 포함 작업 영역 컬렉션에서 hello 액세스 키로 서명 됩니다. 기본적으로 토큰을 포함, 됩니다 하 읽기 사용된 tooprovide 응용 프로그램으로 tooa 보고서 tooembed만 액세스 합니다. Embed 토큰은 특정 보고서에 대해 발급되며 Embed URL에 연결되어야 합니다.

액세스 토큰 hello 액세스 키가 사용 되는 toosign/암호화 hello 토큰으로 hello 서버에 만들어야 합니다. 방법에 대 한 내용은 toocreate, 액세스 토큰이 참조 [인증 하 고 Power BI embedded 허가](power-bi-embedded-app-token-flow.md)합니다. 또한 hello을 검토할 수 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드. 이 모양을 hello.NET SDK를 사용 하 여 Power BI에 대 한 예를 들면 다음과 같습니다.

이 예제에는 toocreat hello에 대 한 새 보고서에 원하는 데이터 집합 id 우리의 개가 있습니다. 또한 tooadd hello 범위에 대 한 필요 *Dataset.Read 및 Workspace.Report.Create*합니다.

hello *PowerBIToken 클래스* hello를 설치 해야 [Power BI 핵심 NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)합니다.

**NuGet 패키지 설치**

```
Install-Package Microsoft.PowerBI.Core
```

**C# 코드**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>비어 있는 새 보고서 만들기

Hello 순서 toocreate 새 보고서에서에서 만들 구성을 제공 해야 합니다. Toocreate hello 보고서를 원하는 hello 액세스 토큰, hello embedURL 및 hello datasetID 포함 해야 합니다. Hello nuget을 설치 하는이 위해서는 [Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)합니다. hello embedUrl https://embedded.powerbi.com/appTokenReportEmbed 됩니다.

> [!NOTE]
> Hello를 사용할 수 있습니다 [JavaScript 보고서 포함 예제](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest 기능입니다. 또한 hello 사용할 수 있는 다른 작업에 대 한 코드 예제를 제공 합니다.

**NuGet 패키지 설치**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript 코드**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

호출 *powerbi.createReport()* 편집 모드에 빈 캔버스 hello 내에 표시 하면 *div* 요소입니다.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>새 보고서 저장

hello 보고서 생성 되지 것입니다 실제로 hello를 호출할 때까지 **다른 이름으로 저장** 작업 합니다. 파일 메뉴에서 또는 JavaScript에서 이 작업을 수행할 수 있습니다.

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
> **다른 이름으로 저장**을 호출해야만 새 보고서가 만들어집니다. 을 저장 한 후 hello 캔버스 편집 모드 및 하지 hello 보고서에 hello 데이터 집합을 계속 표시 합니다. 다른 보고서의 경우 처럼 tooreload hello에 대 한 새 보고서를 할 수 있습니다.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Hello 새 보고서를 로드 합니다.

Hello 새 보고서와 함께 순서 toointeract tooembed hello 새 보고서에 맞게 hello 응용 프로그램을 일반 보고서, 의미, 새 토큰을 포함 하는 동일한 방식으로 발급 해야 하는 hello 및 호출 hello에이 메서드를 포함 해야 합니다.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>저장 자동화 및 이벤트를 "저장" hello를 사용 하 여 새 보고서 로드

"다른 이름으로 저장" 순서 tooautomate hello 프로세스에서의 이벤트를 "저장" hello 사용 하 여 다음 수 있게 하는 hello 새 보고서를 로드 합니다. Hello 저장 작업이 완료 되 고 새 reportId hello, 보고서 이름, hello 이전 reportId (있는 경우)를 포함 하는 Json 개체가 반환 하 고 hello 작업에 다른 이름으로 저장 하면 또는 저장이 이벤트가 발생 합니다.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

hello 새 reportId 걸리고 hello 새 토큰을 만들 것으로 구성 된 hello 새 보고서를 포함 하는 tooAutomate hello 프로세스 "저장" hello 이벤트에서 수신할 수 있습니다.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a>참고 항목

[샘플 시작](power-bi-embedded-get-started-sample.md)  
[보고서 저장](power-bi-embedded-save-reports.md)  
[보고서 포함](power-bi-embedded-embed-report.md)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI Core NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)
