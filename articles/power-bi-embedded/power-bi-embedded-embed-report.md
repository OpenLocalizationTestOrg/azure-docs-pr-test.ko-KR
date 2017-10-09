---
title: "Power BI 포함 Azure에서 보고서 aaaEmbed | Microsoft Docs"
description: "자세한 내용은 방법 tooembed 응용 프로그램에 Power BI 포함에 있는 보고서입니다."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Power BI Embedded에서 보고서 포함

자세한 내용은 방법 tooembed 응용 프로그램에 Power BI 포함에 있는 보고서입니다.

Tooactually 응용 프로그램에 보고서를 포함 하는 방법을 살펴보겠습니다. 여기서는 작업 영역 컬렉션의 작업 영역 내에 보고서가 이미 있다고 가정합니다. 해당 단계를 아직 완료하지 않으면 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.

Hello.NET (C#) 또는 Node.js SDK JavaScript와 함께 사용할 수 있는데, tooeasily Power BI embedded 응용 프로그램을 작성 합니다. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Hello 액세스 키 toouse REST Api를 사용 하 여

순서 toocall hello REST API, hello 지정한 작업 영역 컬렉션에 대 한 Azure 포털에서에서 얻을 수 hello 액세스 키를 전달할 수 있습니다. 자세한 내용은 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.

## <a name="get-a-report-id"></a>보고서 ID 가져오기

모든 액세스 토큰은 보고서를 기준으로 합니다. Tooget hello tooembed hello 보고서에 대 한 보고서 id를 제공 해야 합니다. 이렇게 호출 toohello에 따라 [보고서 가져오기](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API입니다. 이 id와 hello url을 포함 하는 hello 보고서를 반환 됩니다. 이렇게 하려면 Power BI.NET SDK hello를 사용 하 여 또는 hello REST API를 직접 호출 합니다.

### <a name="using-hello-power-bi-net-sdk"></a>Power BI.NET SDK hello를 사용 하 여

Hello.NET SDK를 사용할 경우 toocreate hello Azure 포털에서에서 가져올 hello 선택 키를 기반으로 하는 토큰 자격 증명 해야 합니다. Hello를 설치 하는이 위해서는 [Power BI API NuGet 패키지](https://www.nuget.org/profiles/powerbi)합니다.

**NuGet 패키지 설치**

```
Install-Package Microsoft.PowerBI.Api
```

**C# 코드**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>REST API 호출 hello을 직접

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>액세스 토큰 만들기

Power BI Embedded는 HMAC 서명 JSON Web Token에 해당하는 Embed 토큰을 사용합니다. hello 토큰은 Azure Power BI 포함 작업 영역 컬렉션에서 hello 액세스 키로 서명 됩니다. 기본적으로 토큰을 포함, 됩니다 하 읽기 사용된 tooprovide 응용 프로그램으로 tooa 보고서 tooembed만 액세스 합니다. Embed 토큰은 특정 보고서에 대해 발급되며 Embed URL에 연결되어야 합니다.

액세스 토큰 hello 액세스 키가 사용 되는 toosign/암호화 hello 토큰으로 hello 서버에 만들어야 합니다. 방법에 대 한 내용은 toocreate, 액세스 토큰이 참조 [인증 하 고 Power BI embedded 허가](power-bi-embedded-app-token-flow.md)합니다. 또한 hello을 검토할 수 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드. 이 모양을 hello.NET SDK를 사용 하 여 Power BI에 대 한 예를 들면 다음과 같습니다.

앞서 검색 hello 보고서 id를 사용 합니다. Hello 포함 되 면 토큰이 만들어질, hello javascript 관점에서 사용할 수 있는 hello 액세스 키 toogenerate hello 토큰 사용 하 여 합니다. hello *PowerBIToken 클래스* hello를 설치 해야 [Power BI 핵심 NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)합니다.

**NuGet 패키지 설치**

```
Install-Package Microsoft.PowerBI.Core
```

**C# 코드**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>사용 권한 범위 tooembed 토큰 추가

Embed 토큰을 사용 하 여 hello 리소스에 대 한 액세스를 부여 toorestrict 사용을 할 수 있습니다. 이러한 이유로 범위가 지정된 사용 권한으로 토큰을 생성할 수 있습니다. 자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.

## <a name="embed-using-javascript"></a>JavaScript를 사용하여 포함

Hello 액세스 토큰 및 hello 보고서 id를 설정한 후 JavaScript를 사용 하 여 hello 보고서를 포함할 수 있습니다. Hello nuget을 설치 하는이 위해서는 [Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)합니다. hello embedUrl https://embedded.powerbi.com/appTokenReportEmbed 됩니다.

> [!NOTE]
> Hello를 사용할 수 있습니다 [JavaScript 보고서 포함 예제](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest 기능입니다. 또한 hello 사용할 수 있는 다른 작업에 대 한 코드 예제를 제공 합니다.

**NuGet 패키지 설치**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript 코드**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>포함 된 요소의 hello 크기 설정

hello 보고서 자동으로 포함 됩니다 해당 컨테이너의 hello 크기에 따라. hello의 toooverride hello 기본 크기를 포함 하기만 하면 너비 및 높이 대 한 CSS 클래스 특성 또는 인라인 스타일을 추가 합니다.

## <a name="see-also"></a>참고 항목

[샘플 시작](power-bi-embedded-get-started-sample.md)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Power BI API NuGet 패키지](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[PowerBI-CSharp Git 리포지토리](https://github.com/Microsoft/PowerBI-CSharp)  
[PowerBI-Node Git 리포지토리](https://github.com/Microsoft/PowerBI-Node)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)
