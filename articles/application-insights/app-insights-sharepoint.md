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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="93c50-103">Application Insights를 사용하여 SharePoint 사이트 모니터링</span><span class="sxs-lookup"><span data-stu-id="93c50-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="93c50-104">Application Insights azure hello 가용성, 성능 및 사용 중인 응용 프로그램의 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="93c50-105">여기에 대해 배워 봅니다 어떻게 tooset SharePoint 사이트에 대해 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="93c50-106">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="93c50-106">Create an Application Insights resource</span></span>
<span data-ttu-id="93c50-107">Hello에 [Azure 포털](https://portal.azure.com), 새 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="93c50-108">ASP.NET hello 응용 프로그램 유형으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-108">Choose ASP.NET as hello application type.</span></span>

![속성을 클릭 hello 키를 선택 하 고 ctrl + C를 누릅니다.](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="93c50-110">열리는 hello 블레이드는 hello 위치 응용 프로그램에 대 한 성능 및 사용 현황 데이터를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="93c50-111">tooget 백 tooit 다음에 로그인 tooAzure를 찾아야 타일에 대 한 hello 시작 화면에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="93c50-112">또는 찾아보기 toofind 클릭 하 여 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="93c50-113">스크립트 tooyour 웹 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="93c50-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="93c50-114">빠른 시작에서 웹 페이지에 대 한 hello 스크립트를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="93c50-115">Hello 하기 바로 전에 hello 스크립트 삽입 &lt;/h&gt; 태그 tootrack 모든 페이지의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="93c50-116">웹 사이트에서 마스터 페이지, 경우에 hello 스크립트 있습니다 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="93c50-117">예를 들어 ASP.NET MVC 프로젝트에서는 View\Shared\_Layout.cshtml에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="93c50-118">hello 스크립트 hello 원격 분석 tooyour Application Insights 리소스를 알려 주는 hello 계측 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="93c50-119">Hello 코드 tooyour 사이트 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="93c50-120">Hello 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="93c50-120">On hello master page</span></span>
<span data-ttu-id="93c50-121">Hello 사이트의 마스터 페이지를 편집할 수 있는 hello 사이트의 모든 페이지에 대 한 모니터링을 제공 합니다입니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="93c50-122">Hello 마스터 페이지를 확인 하 고 SharePoint Designer 또는 다른 편집기를 사용 하 여 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="93c50-123">Hello 하기 바로 전에 hello 코드를 추가 </head> 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="93c50-124">또는 개별 페이지에서</span><span class="sxs-lookup"><span data-stu-id="93c50-124">Or on individual pages</span></span>
<span data-ttu-id="93c50-125">페이지의 제한 된 집합 toomonitor hello 스크립트를 별도로 추가 tooeach 페이지.</span><span class="sxs-lookup"><span data-stu-id="93c50-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="93c50-126">웹 파트를 삽입 하 고 hello 코드 조각에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="93c50-127">앱에 대한 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="93c50-127">View data about your app</span></span>
<span data-ttu-id="93c50-128">응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-128">Redeploy your app.</span></span>

<span data-ttu-id="93c50-129">Hello에 응용 프로그램 블레이드 반환 tooyour [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="93c50-130">hello 첫 번째 이벤트는 검색에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="93c50-131">더 많은 데이터를 기대하는 경우 몇 초 후에 새로고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="93c50-132">Hello 개요 블레이드에서 클릭 **사용 현황 분석** 사용자, 세션 및 페이지 보기의 toosee toocharts:</span><span class="sxs-lookup"><span data-stu-id="93c50-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="93c50-133">모든 차트 toosee 자세한 세부 정보-예를 들어 페이지 뷰를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="93c50-134">또는 사용자:</span><span class="sxs-lookup"><span data-stu-id="93c50-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="93c50-135">사용자 ID 캡처</span><span class="sxs-lookup"><span data-stu-id="93c50-135">Capturing User Id</span></span>
<span data-ttu-id="93c50-136">hello 표준 웹 페이지 코드 조각에는 SharePoint에서 사용자 id hello 캡처하지 않습니다 하지만 작은 수정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="93c50-137">Hello Essentials 드롭 다운 Application Insights에서에서 응용 프로그램의 계측 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="93c50-138">'XXXX' hello 계측 키 아래 hello 조각을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="93c50-139">Hello 조각 hello 포털에서 받아야 하는 대신 SharePoint 응용 프로그램에 hello 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="93c50-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93c50-140">Next Steps</span></span>
* <span data-ttu-id="93c50-141">[웹 테스트](app-insights-monitor-web-app-availability.md) toomonitor hello 가용성의 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="93c50-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="93c50-142">[Application Insights](app-insights-overview.md) </span><span class="sxs-lookup"><span data-stu-id="93c50-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


