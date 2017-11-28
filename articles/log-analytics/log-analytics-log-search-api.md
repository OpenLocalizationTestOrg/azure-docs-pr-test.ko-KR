---
title: "aaaLog 분석 로그 검색 REST API | Microsoft Docs"
description: "이 가이드에서는 hello를 사용 하는 방법을 설명 하는 기본 자습서를 로그 분석 REST API hello Operations Management Suite (OMS)에서 검색 하 고 방법을 보여 주는 예제를 제공 제공 toouse hello 명령입니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="15b25-103">Log Analytics 로그 검색 REST API</span><span class="sxs-lookup"><span data-stu-id="15b25-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="15b25-104">이 가이드에서는 hello 로그 분석 검색 REST API를 사용 하는 방법의 예제를 비롯 한 기본 자습서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="15b25-105">로그 분석은 hello Operations Management Suite (OMS)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="15b25-106">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md),이 문서에 설명 된 대로 toouse hello 레거시 쿼리 언어 hello 로그 검색 API 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="15b25-107">새로운 API 업그레이드 된 작업 영역에서 릴리스되며 hello 설명서 당시에 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="15b25-108">로그 분석이 이전에 hello 리소스 공급자에서 사용 되는 hello 이름을이 Operational Insights는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="15b25-109">Hello 로그 검색 REST API 개요</span><span class="sxs-lookup"><span data-stu-id="15b25-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="15b25-110">hello 로그 분석 검색 REST API는 RESTful 이며 Azure 리소스 관리자 API hello를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="15b25-111">이 문서에서는 hello API를 통해 액세스의 예로 제공 [ARMClient](https://github.com/projectkudu/ARMClient), 호출을 간소화 하는 오픈 소스 명령줄 도구인 hello Azure 리소스 관리자 API입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="15b25-112">hello 사용 하 여 ARMClient 많은 옵션 tooaccess hello 로그 분석 검색 API 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="15b25-113">또 다른 옵션은 검색에 액세스 하기 위한 cmdlet이 포함 되어 있는 OperationalInsights에 대 한 toouse hello Azure PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="15b25-114">이러한 도구를 통해 hello Azure 리소스 관리자 API toomake 호출 tooOMS 작업 영역을 사용 하 고 그 안에서 검색 명령을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="15b25-115">hello API 있도록 toouse hello 검색 결과 다양 한 방법으로 프로그래밍 방식으로 JSON 형식으로 된 검색 결과 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="15b25-116">hello Azure 리소스 관리자 통해 사용할 수 있습니다는 [Library for.net](https://msdn.microsoft.com/library/azure/dn910477.aspx) 및 hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="15b25-117">더 toolearn hello 연결 된 웹 페이지를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="15b25-118">명령을 사용 하 여는 집계와 같은 `|measure count()` 또는 `distinct`, 각 호출 toosearch 최대 500, 000 레코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="15b25-119">집계 명령을 포함하지 않는 검색의 경우 최대 5,000개의 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="15b25-120">기본 Log Analytics 검색 REST API 자습서</span><span class="sxs-lookup"><span data-stu-id="15b25-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="15b25-121">ARMClient toouse</span><span class="sxs-lookup"><span data-stu-id="15b25-121">toouse ARMClient</span></span>
1. <span data-ttu-id="15b25-122">Windows용 오픈 소스 패키지 관리자인 [Chocolatey](https://chocolatey.org/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="15b25-123">관리자 권한으로 명령 프롬프트 창을 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="15b25-124">Hello 다음 명령을 실행 하 여 ARMClient를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="15b25-125">ARMClient를 사용 하 여 검색 한 tooperform</span><span class="sxs-lookup"><span data-stu-id="15b25-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="15b25-126">Microsoft 계정이나 회사 또는 학교 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="15b25-127">성공적으로 로그인 계정을 지정 하는 모든 연결 된 구독 toohello를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="15b25-128">Hello Operations Management Suite 작업 영역을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="15b25-129">Get 호출이 성공 하면 모든 작업 영역 연결 toohello 구독 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. <span data-ttu-id="15b25-130">검색 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="15b25-131">새 검색 변수를 사용하여 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="15b25-132">Log Analytics 검색 REST API 참조 예제</span><span class="sxs-lookup"><span data-stu-id="15b25-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="15b25-133">다음 예제는 hello hello 검색 API를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="15b25-134">검색-동작/읽기</span><span class="sxs-lookup"><span data-stu-id="15b25-134">Search - Action/Read</span></span>
<span data-ttu-id="15b25-135">**샘플 Url:**</span><span class="sxs-lookup"><span data-stu-id="15b25-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="15b25-136">**요청:**</span><span class="sxs-lookup"><span data-stu-id="15b25-136">**Request:**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
<span data-ttu-id="15b25-137">다음 표에서 hello에 사용할 수 있는 hello 속성에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="15b25-138">**속성**</span><span class="sxs-lookup"><span data-stu-id="15b25-138">**Property**</span></span> | <span data-ttu-id="15b25-139">**설명**</span><span class="sxs-lookup"><span data-stu-id="15b25-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="15b25-140">top</span><span class="sxs-lookup"><span data-stu-id="15b25-140">top</span></span> |<span data-ttu-id="15b25-141">결과 tooreturn hello 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="15b25-142">highlight</span><span class="sxs-lookup"><span data-stu-id="15b25-142">highlight</span></span> |<span data-ttu-id="15b25-143">일치하는 필드를 강조 표시하는 데 사용된 pre 및 post 매개 변수를 포함합니다</span><span class="sxs-lookup"><span data-stu-id="15b25-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="15b25-144">pre</span><span class="sxs-lookup"><span data-stu-id="15b25-144">pre</span></span> |<span data-ttu-id="15b25-145">Hello 문자열 tooyour 일치 필드 지정 된 접두사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="15b25-146">post</span><span class="sxs-lookup"><span data-stu-id="15b25-146">post</span></span> |<span data-ttu-id="15b25-147">문자열 일치 tooyour 필드를 지정 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="15b25-148">쿼리</span><span class="sxs-lookup"><span data-stu-id="15b25-148">query</span></span> |<span data-ttu-id="15b25-149">hello 검색 쿼리 toocollect를 사용 하 고 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="15b25-150">start</span><span class="sxs-lookup"><span data-stu-id="15b25-150">start</span></span> |<span data-ttu-id="15b25-151">hello 시작 부분에서 찾은 결과 toobe 원하는 hello 시간 창입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="15b25-152">end</span><span class="sxs-lookup"><span data-stu-id="15b25-152">end</span></span> |<span data-ttu-id="15b25-153">hello 끝에서 발견 되는 결과 toobe 원하는 hello 시간 창입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="15b25-154">**응답:**</span><span class="sxs-lookup"><span data-stu-id="15b25-154">**Response:**</span></span>

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a><span data-ttu-id="15b25-155">검색/{ID}-동작/읽기</span><span class="sxs-lookup"><span data-stu-id="15b25-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="15b25-156">**저장 된 검색의 hello 내용을 요청:**</span><span class="sxs-lookup"><span data-stu-id="15b25-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="15b25-157">Hello 검색 '보류중' 상태를 반환 하는 경우이 API를 통해 폴링 hello 업데이트 결과 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="15b25-158">6 분 후 hello 검색 결과를 hello hello 캐시에서 삭제 되 고 HTTP Gone이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="15b25-159">Hello 초기 검색 요청이 '성공' 상태를 즉시 반환 hello 결과 쿼리 하는 경우 HTTP Gone이 API tooreturn toohello 캐시를 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="15b25-160">HTTP 200 결과의 hello 내용은 업데이트 된 값이 포함 된 hello 초기 검색 요청과 동일한 형식 hello에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="15b25-161">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="15b25-161">Saved searches</span></span>
<span data-ttu-id="15b25-162">**저장된 검색의 목록 요청입니다.**</span><span class="sxs-lookup"><span data-stu-id="15b25-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="15b25-163">지원되는 메서드: GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="15b25-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="15b25-164">지원되는 컬렉션 메서드: GET</span><span class="sxs-lookup"><span data-stu-id="15b25-164">Supported collection methods: GET</span></span>

<span data-ttu-id="15b25-165">다음 표에서 hello에 사용할 수 있는 hello 속성에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="15b25-166">속성</span><span class="sxs-lookup"><span data-stu-id="15b25-166">Property</span></span> | <span data-ttu-id="15b25-167">설명</span><span class="sxs-lookup"><span data-stu-id="15b25-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15b25-168">Id</span><span class="sxs-lookup"><span data-stu-id="15b25-168">Id</span></span> |<span data-ttu-id="15b25-169">hello 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-169">hello unique identifier.</span></span> |
| <span data-ttu-id="15b25-170">ETag</span><span class="sxs-lookup"><span data-stu-id="15b25-170">Etag</span></span> |<span data-ttu-id="15b25-171">**패치에 필요합니다**.</span><span class="sxs-lookup"><span data-stu-id="15b25-171">**Required for Patch**.</span></span> <span data-ttu-id="15b25-172">각 쓰기에 대해 서버에서 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-172">Updated by server on each write.</span></span> <span data-ttu-id="15b25-173">값 같음 toohello 현재 저장 된 값 이어야 합니다. 또는 ' *' tooupdate 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="15b25-174">오래되거나 잘못된 값에 대해 409가 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="15b25-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="15b25-175">properties.query</span></span> |<span data-ttu-id="15b25-176">**필수입니다**.</span><span class="sxs-lookup"><span data-stu-id="15b25-176">**Required**.</span></span> <span data-ttu-id="15b25-177">hello 검색 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-177">hello search query.</span></span> |
| <span data-ttu-id="15b25-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="15b25-178">properties.displayName</span></span> |<span data-ttu-id="15b25-179">**필수입니다**.</span><span class="sxs-lookup"><span data-stu-id="15b25-179">**Required**.</span></span> <span data-ttu-id="15b25-180">hello 쿼리의 hello 사용자 지정 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="15b25-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="15b25-181">properties.category</span></span> |<span data-ttu-id="15b25-182">**필수입니다**.</span><span class="sxs-lookup"><span data-stu-id="15b25-182">**Required**.</span></span> <span data-ttu-id="15b25-183">hello 쿼리의 hello 사용자 정의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="15b25-184">로그 분석 검색 API hello 현재 반환 사용자가 만든 저장 된 작업 영역에서 저장 된 검색에 대 한 폴링 될 때 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="15b25-185">hello API 솔루션에서 제공 하는 저장 된 검색을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="15b25-186">저장된 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="15b25-186">Create saved searches</span></span>
<span data-ttu-id="15b25-187">**요청:**</span><span class="sxs-lookup"><span data-stu-id="15b25-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="15b25-188">저장 된 모든 검색, 일정 및 hello 로그 분석 API를 사용 하 여 만든 작업에 대 한 hello 이름은 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="15b25-189">저장된 검색 삭제</span><span class="sxs-lookup"><span data-stu-id="15b25-189">Delete saved searches</span></span>
<span data-ttu-id="15b25-190">**요청:**</span><span class="sxs-lookup"><span data-stu-id="15b25-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="15b25-191">저장된 검색 업데이트</span><span class="sxs-lookup"><span data-stu-id="15b25-191">Update saved searches</span></span>
 <span data-ttu-id="15b25-192">**요청:**</span><span class="sxs-lookup"><span data-stu-id="15b25-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="15b25-193">메타데이터-JSON만</span><span class="sxs-lookup"><span data-stu-id="15b25-193">Metadata - JSON only</span></span>
<span data-ttu-id="15b25-194">작업 영역에 수집 된 hello 데이터에 대 한 모든 로그 형식에 대 한 방식으로 toosee hello 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="15b25-195">예를 들어 hello 이벤트 유형에 컴퓨터 라는 필드가 있는지 알고을 하려는 경우이 쿼리는 한 가지 방법은 toocheck 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="15b25-196">**필드에 대한 요청:**</span><span class="sxs-lookup"><span data-stu-id="15b25-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="15b25-197">**응답:**</span><span class="sxs-lookup"><span data-stu-id="15b25-197">**Response:**</span></span>

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

<span data-ttu-id="15b25-198">다음 표에서 hello에 사용할 수 있는 hello 속성에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="15b25-199">**속성**</span><span class="sxs-lookup"><span data-stu-id="15b25-199">**Property**</span></span> | <span data-ttu-id="15b25-200">**설명**</span><span class="sxs-lookup"><span data-stu-id="15b25-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="15b25-201">name</span><span class="sxs-lookup"><span data-stu-id="15b25-201">name</span></span> |<span data-ttu-id="15b25-202">필드 이름.</span><span class="sxs-lookup"><span data-stu-id="15b25-202">Field name.</span></span> |
| <span data-ttu-id="15b25-203">displayName</span><span class="sxs-lookup"><span data-stu-id="15b25-203">displayName</span></span> |<span data-ttu-id="15b25-204">hello는 hello 필드의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="15b25-205">type</span><span class="sxs-lookup"><span data-stu-id="15b25-205">type</span></span> |<span data-ttu-id="15b25-206">hello hello 필드 값의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="15b25-207">facetable</span><span class="sxs-lookup"><span data-stu-id="15b25-207">facetable</span></span> |<span data-ttu-id="15b25-208">현재 'indexed', 'store' 및 'facet' 속성의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="15b25-209">display</span><span class="sxs-lookup"><span data-stu-id="15b25-209">display</span></span> |<span data-ttu-id="15b25-210">현재 'display' 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-210">Current ‘display’ property.</span></span> <span data-ttu-id="15b25-211">필드를 검색에서 볼 수 있는 경우 true입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="15b25-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="15b25-212">ownerType</span></span> |<span data-ttu-id="15b25-213">Tooonboarded IP 속하는 감소 tooonly 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="15b25-214">선택적 매개 변수</span><span class="sxs-lookup"><span data-stu-id="15b25-214">Optional parameters</span></span>
<span data-ttu-id="15b25-215">다음 정보는 hello 사용할 수 있는 선택적 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="15b25-216">강조 표시</span><span class="sxs-lookup"><span data-stu-id="15b25-216">Highlighting</span></span>
<span data-ttu-id="15b25-217">hello "Highlight" 매개 변수는 toorequest hello 검색 하위 시스템을 사용할 수는 선택적 매개 변수는 해당 응답의 표식 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="15b25-218">이러한 표식은 hello 시작 및 종료 나타냅니다 검색 쿼리에 제공 된 hello 용어와 일치 하는 강조 표시 된 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="15b25-219">지정 hello 시작 및 끝 표식을 검색어 toowrap hello 강조 표시에 사용 되는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="15b25-220">**예제 검색 쿼리**</span><span class="sxs-lookup"><span data-stu-id="15b25-220">**Example search query**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

<span data-ttu-id="15b25-221">**샘플 결과:**</span><span class="sxs-lookup"><span data-stu-id="15b25-221">**Sample result:**</span></span>

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

<span data-ttu-id="15b25-222">위의 결과 hello는 접두사가 있고 추가 된 오류 메시지가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="15b25-223">컴퓨터 그룹</span><span class="sxs-lookup"><span data-stu-id="15b25-223">Computer groups</span></span>
<span data-ttu-id="15b25-224">컴퓨터 그룹은 컴퓨터 집합을 반환하는 특수한 저장된 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="15b25-225">Hello 그룹의 다른 쿼리 toolimit hello 결과 toohello 컴퓨터에서 컴퓨터 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="15b25-226">컴퓨터 그룹은 값이 Computer인 Group 태그가 있는 저장된 검색으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="15b25-227">다음은 컴퓨터 그룹에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-227">Following is a sample response for a computer group.</span></span>

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a><span data-ttu-id="15b25-228">컴퓨터 그룹 검색</span><span class="sxs-lookup"><span data-stu-id="15b25-228">Retrieving computer groups</span></span>
<span data-ttu-id="15b25-229">tooretrieve 컴퓨터 그룹을 사용 하 여 hello hello 그룹과 Get 메서드가 id입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="15b25-230">컴퓨터 그룹 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="15b25-230">Creating or updating a computer group</span></span>
<span data-ttu-id="15b25-231">컴퓨터 그룹 toocreate hello Put 메서드를 사용 하 여 저장 된 검색 고유 id</span><span class="sxs-lookup"><span data-stu-id="15b25-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="15b25-232">기존 컴퓨터 그룹 ID를 사용하는 경우 해당 ID가 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="15b25-233">Hello 로그 분석 포털에서 컴퓨터 그룹을 만들 때 hello ID가 hello 그룹 및 이름에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="15b25-234">hello 쿼리 hello 그룹 정의에 사용 되는 그룹 toofunction hello에 대 한 컴퓨터 집합을 제대로 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="15b25-235">와 함께 쿼리를 종료 하는 것이 좋습니다. `| Distinct Computer` tooensure hello 올바른 데이터가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="15b25-236">hello 저장 된 검색의 hello 정의 hello 검색 toobe 컴퓨터 그룹으로 분류에 대 한 그룹 컴퓨터의 값이 지정 하는 태그를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="15b25-237">컴퓨터 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="15b25-237">Deleting computer groups</span></span>
<span data-ttu-id="15b25-238">toodelete 컴퓨터 그룹을 사용 하 여 hello hello 그룹과 Delete 메서드 id입니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="15b25-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15b25-239">Next steps</span></span>
* <span data-ttu-id="15b25-240">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) toobuild 쿼리 조건에 대 한 사용자 지정 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b25-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
