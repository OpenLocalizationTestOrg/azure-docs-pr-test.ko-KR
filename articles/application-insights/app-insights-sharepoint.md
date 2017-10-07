---
title: "aaaMonitor Application Insights와 SharePoint 사이트"
description: "새 계측 키를 사용하여 새 응용 프로그램 모니터링 시작"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Application Insights를 사용하여 SharePoint 사이트 모니터링
Application Insights azure hello 가용성, 성능 및 사용 중인 응용 프로그램의 모니터링합니다. 여기에 대해 배워 봅니다 어떻게 tooset SharePoint 사이트에 대해 것입니다.

## <a name="create-an-application-insights-resource"></a>Application Insights 리소스 만들기
Hello에 [Azure 포털](https://portal.azure.com), 새 Application Insights 리소스를 만듭니다. ASP.NET hello 응용 프로그램 유형으로 선택 합니다.

![속성을 클릭 hello 키를 선택 하 고 ctrl + C를 누릅니다.](./media/app-insights-sharepoint/01-new.png)

열리는 hello 블레이드는 hello 위치 응용 프로그램에 대 한 성능 및 사용 현황 데이터를 표시 됩니다. tooget 백 tooit 다음에 로그인 tooAzure를 찾아야 타일에 대 한 hello 시작 화면에서 합니다. 또는 찾아보기 toofind 클릭 하 여 것입니다.

## <a name="add-our-script-tooyour-web-pages"></a>스크립트 tooyour 웹 페이지 추가
빠른 시작에서 웹 페이지에 대 한 hello 스크립트를 얻습니다.

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Hello 하기 바로 전에 hello 스크립트 삽입 &lt;/h&gt; 태그 tootrack 모든 페이지의 원하는 합니다. 웹 사이트에서 마스터 페이지, 경우에 hello 스크립트 있습니다 넣을 수 있습니다. 예를 들어 ASP.NET MVC 프로젝트에서는 View\Shared\_Layout.cshtml에 추가합니다.

hello 스크립트 hello 원격 분석 tooyour Application Insights 리소스를 알려 주는 hello 계측 키를 포함 합니다.

### <a name="add-hello-code-tooyour-site-pages"></a>Hello 코드 tooyour 사이트 페이지를 추가 합니다.
#### <a name="on-hello-master-page"></a>Hello 마스터 페이지
Hello 사이트의 마스터 페이지를 편집할 수 있는 hello 사이트의 모든 페이지에 대 한 모니터링을 제공 합니다입니다.

Hello 마스터 페이지를 확인 하 고 SharePoint Designer 또는 다른 편집기를 사용 하 여 편집 합니다.

![](./media/app-insights-sharepoint/03-master.png)

Hello 하기 바로 전에 hello 코드를 추가 </head> 태그입니다. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>또는 개별 페이지에서
페이지의 제한 된 집합 toomonitor hello 스크립트를 별도로 추가 tooeach 페이지. 

웹 파트를 삽입 하 고 hello 코드 조각에 포함 합니다.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>앱에 대한 데이터 보기
응용 프로그램을 다시 배포 합니다.

Hello에 응용 프로그램 블레이드 반환 tooyour [Azure 포털](https://portal.azure.com)합니다.

hello 첫 번째 이벤트는 검색에 표시 됩니다. 

![](./media/app-insights-sharepoint/09-search.png)

더 많은 데이터를 기대하는 경우 몇 초 후에 새로고침을 클릭합니다.

Hello 개요 블레이드에서 클릭 **사용 현황 분석** 사용자, 세션 및 페이지 보기의 toosee toocharts:

![](./media/app-insights-sharepoint/06-usage.png)

모든 차트 toosee 자세한 세부 정보-예를 들어 페이지 뷰를 클릭 합니다.

![](./media/app-insights-sharepoint/07-pages.png)

또는 사용자:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>사용자 ID 캡처
hello 표준 웹 페이지 코드 조각에는 SharePoint에서 사용자 id hello 캡처하지 않습니다 하지만 작은 수정을 할 수 있습니다.

1. Hello Essentials 드롭 다운 Application Insights에서에서 응용 프로그램의 계측 키를 복사 합니다. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. 'XXXX' hello 계측 키 아래 hello 조각을 대체 합니다. 
2. Hello 조각 hello 포털에서 받아야 하는 대신 SharePoint 응용 프로그램에 hello 스크립트를 포함 합니다.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>다음 단계
* [웹 테스트](app-insights-monitor-web-app-availability.md) toomonitor hello 가용성의 사이트입니다.
* [Application Insights](app-insights-overview.md) 

<!--Link references-->


