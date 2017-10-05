---
title: "Application Insights를 사용하여 SharePoint 사이트 모니터링"
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
ms.openlocfilehash: a3b37674469a131016f46af590e1eee3ba4cdc73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="d7a1f-103">Application Insights를 사용하여 SharePoint 사이트 모니터링</span><span class="sxs-lookup"><span data-stu-id="d7a1f-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="d7a1f-104">Azure Application Insights는 응용 프로그램의 가용성, 성능 및 사용량을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="d7a1f-105">여기에서는 SharePoint 사이트에 맞게 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="d7a1f-106">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="d7a1f-106">Create an Application Insights resource</span></span>
<span data-ttu-id="d7a1f-107">[Azure 포털](https://portal.azure.com)에서 새 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="d7a1f-108">응용 프로그램 유형으로 ASP.NET을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-108">Choose ASP.NET as the application type.</span></span>

![속성 클릭, 키 선택 및 ctrl+C 누르기](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="d7a1f-110">열리는 블레이드에서 앱의 성능 및 사용 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="d7a1f-111">다음에 Azure에 로그인할 때 다시 이 블레이드로 돌아가려면 시작 화면에서 해당 타일을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="d7a1f-112">또는 찾아보기를 클릭하여 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="d7a1f-113">웹 페이지에 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="d7a1f-113">Add our script to your web pages</span></span>
<span data-ttu-id="d7a1f-114">빠른 시작에서 웹 페이지용 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-114">In Quick Start, get the script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="d7a1f-115">추적하려는 모든 페이지의 &lt;/head&gt; 태그 바로 앞에 스크립트를 삽입합니다. 웹 사이트에 마스터 페이지가 있는 경우 이 페이지에 스크립트를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="d7a1f-116">예를 들어 ASP.NET MVC 프로젝트에서는 View\Shared\_Layout.cshtml에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="d7a1f-117">스크립트에는 Application Insights 리소스에 원격 분석을 전달하는 계측 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="d7a1f-118">사이트 페이지에 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="d7a1f-119">마스터 페이지에서</span><span class="sxs-lookup"><span data-stu-id="d7a1f-119">On the master page</span></span>
<span data-ttu-id="d7a1f-120">사이트의 마스터 페이지를 편집할 수 있는 경우 사이트의 모든 페이지에 대한 모니터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="d7a1f-121">마스터 페이지를 체크 아웃하고 SharePoint Designer 또는 다른 편집기를 사용하여 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="d7a1f-122"></head> 태그 바로 앞에 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-122">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="d7a1f-123">또는 개별 페이지에서</span><span class="sxs-lookup"><span data-stu-id="d7a1f-123">Or on individual pages</span></span>
<span data-ttu-id="d7a1f-124">제한된 페이지 집합을 모니터링하려면 각 페이지에 개별적으로 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="d7a1f-125">웹 파트를 삽입하고 코드 조각을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-125">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="d7a1f-126">앱에 대한 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="d7a1f-126">View data about your app</span></span>
<span data-ttu-id="d7a1f-127">응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-127">Redeploy your app.</span></span>

<span data-ttu-id="d7a1f-128">[Azure 포털](https://portal.azure.com)에서 사용자 응용 프로그램 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d7a1f-129">첫 번째 이벤트가 검색에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-129">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="d7a1f-130">더 많은 데이터를 기대하는 경우 몇 초 후에 새로고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="d7a1f-131">개요 블레이드에서 **사용 현황 분석** 을 클릭하여 사용자, 세션 및 페이지 보기에 대한 차트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="d7a1f-132">자세한 정보를 보려면 차트를 클릭합니다. 예: 페이지 보기:</span><span class="sxs-lookup"><span data-stu-id="d7a1f-132">Click any chart to see more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="d7a1f-133">또는 사용자:</span><span class="sxs-lookup"><span data-stu-id="d7a1f-133">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="d7a1f-134">사용자 ID 캡처</span><span class="sxs-lookup"><span data-stu-id="d7a1f-134">Capturing User Id</span></span>
<span data-ttu-id="d7a1f-135">표준 웹 페이지 코드 조각은 SharePoint에서 사용자 ID를 캡처하지 않지만 약간 수정하여 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="d7a1f-136">Application Insights의 Essentials 드롭 다운에서 앱의 계측 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="d7a1f-137">다음 코드 조각에서 'XXXX'에 대한 계측 키를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="d7a1f-138">포털에서 가져온 코드 조각 대신 SharePoint 앱에 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d7a1f-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="d7a1f-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7a1f-139">Next Steps</span></span>
* <span data-ttu-id="d7a1f-140">[웹 테스트](app-insights-monitor-web-app-availability.md) </span><span class="sxs-lookup"><span data-stu-id="d7a1f-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="d7a1f-141">[Application Insights](app-insights-overview.md) </span><span class="sxs-lookup"><span data-stu-id="d7a1f-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


