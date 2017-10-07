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
# <a name="log-analytics-log-search-rest-api"></a>Log Analytics 로그 검색 REST API
이 가이드에서는 hello 로그 분석 검색 REST API를 사용 하는 방법의 예제를 비롯 한 기본 자습서를 제공 합니다. 로그 분석은 hello Operations Management Suite (OMS)의 일부입니다.

> [!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md),이 문서에 설명 된 대로 toouse hello 레거시 쿼리 언어 hello 로그 검색 API 계속 해야 합니다.  새로운 API 업그레이드 된 작업 영역에서 릴리스되며 hello 설명서 당시에 업데이트 됩니다. 

> [!NOTE]
> 로그 분석이 이전에 hello 리소스 공급자에서 사용 되는 hello 이름을이 Operational Insights는 호출 합니다.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Hello 로그 검색 REST API 개요
hello 로그 분석 검색 REST API는 RESTful 이며 Azure 리소스 관리자 API hello를 통해 액세스할 수 있습니다. 이 문서에서는 hello API를 통해 액세스의 예로 제공 [ARMClient](https://github.com/projectkudu/ARMClient), 호출을 간소화 하는 오픈 소스 명령줄 도구인 hello Azure 리소스 관리자 API입니다. hello 사용 하 여 ARMClient 많은 옵션 tooaccess hello 로그 분석 검색 API 중 하나입니다. 또 다른 옵션은 검색에 액세스 하기 위한 cmdlet이 포함 되어 있는 OperationalInsights에 대 한 toouse hello Azure PowerShell 모듈입니다. 이러한 도구를 통해 hello Azure 리소스 관리자 API toomake 호출 tooOMS 작업 영역을 사용 하 고 그 안에서 검색 명령을 수행할 수 있습니다. hello API 있도록 toouse hello 검색 결과 다양 한 방법으로 프로그래밍 방식으로 JSON 형식으로 된 검색 결과 출력 합니다.

hello Azure 리소스 관리자 통해 사용할 수 있습니다는 [Library for.net](https://msdn.microsoft.com/library/azure/dn910477.aspx) 및 hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx)합니다. 더 toolearn hello 연결 된 웹 페이지를 검토 합니다.

> [!NOTE]
> 명령을 사용 하 여는 집계와 같은 `|measure count()` 또는 `distinct`, 각 호출 toosearch 최대 500, 000 레코드를 반환할 수 있습니다. 집계 명령을 포함하지 않는 검색의 경우 최대 5,000개의 레코드를 반환합니다.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>기본 Log Analytics 검색 REST API 자습서
### <a name="toouse-armclient"></a>ARMClient toouse
1. Windows용 오픈 소스 패키지 관리자인 [Chocolatey](https://chocolatey.org/)를 설치합니다. 관리자 권한으로 명령 프롬프트 창을 열고 hello 다음 명령을 실행 합니다.

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Hello 다음 명령을 실행 하 여 ARMClient를 설치 합니다.

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>ARMClient를 사용 하 여 검색 한 tooperform
1. Microsoft 계정이나 회사 또는 학교 계정을 사용하여 로그인합니다.

    ```
    armclient login
    ```

    성공적으로 로그인 계정을 지정 하는 모든 연결 된 구독 toohello를 나열 합니다.

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Hello Operations Management Suite 작업 영역을 가져옵니다.

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Get 호출이 성공 하면 모든 작업 영역 연결 toohello 구독 출력 됩니다.

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
3. 검색 변수를 만듭니다.

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. 새 검색 변수를 사용하여 검색 합니다.

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Log Analytics 검색 REST API 참조 예제
다음 예제는 hello hello 검색 API를 사용 하는 방법을 보여 줍니다.

### <a name="search---actionread"></a>검색-동작/읽기
**샘플 Url:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**요청:**

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
다음 표에서 hello에 사용할 수 있는 hello 속성에 설명 합니다.

| **속성** | **설명** |
| --- | --- |
| top |결과 tooreturn hello 최대 수입니다. |
| highlight |일치하는 필드를 강조 표시하는 데 사용된 pre 및 post 매개 변수를 포함합니다 |
| pre |Hello 문자열 tooyour 일치 필드 지정 된 접두사를 추가 합니다. |
| post |문자열 일치 tooyour 필드를 지정 하는 hello를 추가 합니다. |
| 쿼리 |hello 검색 쿼리 toocollect를 사용 하 고 결과 반환 합니다. |
| start |hello 시작 부분에서 찾은 결과 toobe 원하는 hello 시간 창입니다. |
| end |hello 끝에서 발견 되는 결과 toobe 원하는 hello 시간 창입니다. |

**응답:**

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

### <a name="searchid---actionread"></a>검색/{ID}-동작/읽기
**저장 된 검색의 hello 내용을 요청:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Hello 검색 '보류중' 상태를 반환 하는 경우이 API를 통해 폴링 hello 업데이트 결과 수행할 수 있습니다. 6 분 후 hello 검색 결과를 hello hello 캐시에서 삭제 되 고 HTTP Gone이 반환 됩니다. Hello 초기 검색 요청이 '성공' 상태를 즉시 반환 hello 결과 쿼리 하는 경우 HTTP Gone이 API tooreturn toohello 캐시를 추가 되지 않습니다. HTTP 200 결과의 hello 내용은 업데이트 된 값이 포함 된 hello 초기 검색 요청과 동일한 형식 hello에 됩니다.
>
>

### <a name="saved-searches"></a>저장된 검색
**저장된 검색의 목록 요청입니다.**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

지원되는 메서드: GET PUT DELETE

지원되는 컬렉션 메서드: GET

다음 표에서 hello에 사용할 수 있는 hello 속성에 설명 합니다.

| 속성 | 설명 |
| --- | --- |
| Id |hello 고유 식별자입니다. |
| ETag |**패치에 필요합니다**. 각 쓰기에 대해 서버에서 업데이트되었습니다. 값 같음 toohello 현재 저장 된 값 이어야 합니다. 또는 ' *' tooupdate 합니다. 오래되거나 잘못된 값에 대해 409가 반환되었습니다. |
| properties.query |**필수입니다**. hello 검색 쿼리입니다. |
| properties.displayName |**필수입니다**. hello 쿼리의 hello 사용자 지정 표시 이름입니다. |
| properties.category |**필수입니다**. hello 쿼리의 hello 사용자 정의 범주입니다. |

> [!NOTE]
> 로그 분석 검색 API hello 현재 반환 사용자가 만든 저장 된 작업 영역에서 저장 된 검색에 대 한 폴링 될 때 검색 합니다. hello API 솔루션에서 제공 하는 저장 된 검색을 반환 하지 않습니다.
>
>

### <a name="create-saved-searches"></a>저장된 검색 만들기
**요청:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> 저장 된 모든 검색, 일정 및 hello 로그 분석 API를 사용 하 여 만든 작업에 대 한 hello 이름은 소문자 여야 합니다.

### <a name="delete-saved-searches"></a>저장된 검색 삭제
**요청:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>저장된 검색 업데이트
 **요청:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>메타데이터-JSON만
작업 영역에 수집 된 hello 데이터에 대 한 모든 로그 형식에 대 한 방식으로 toosee hello 필드는 다음과 같습니다. 예를 들어 hello 이벤트 유형에 컴퓨터 라는 필드가 있는지 알고을 하려는 경우이 쿼리는 한 가지 방법은 toocheck 합니다.

**필드에 대한 요청:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**응답:**

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

다음 표에서 hello에 사용할 수 있는 hello 속성에 설명 합니다.

| **속성** | **설명** |
| --- | --- |
| name |필드 이름. |
| displayName |hello는 hello 필드의 이름을 표시 합니다. |
| type |hello hello 필드 값의 형식입니다. |
| facetable |현재 'indexed', 'store' 및 'facet' 속성의 조합입니다. |
| display |현재 'display' 속성입니다. 필드를 검색에서 볼 수 있는 경우 true입니다. |
| ownerType |Tooonboarded IP 속하는 감소 tooonly 형식입니다. |

## <a name="optional-parameters"></a>선택적 매개 변수
다음 정보는 hello 사용할 수 있는 선택적 매개 변수를 설명 합니다.

### <a name="highlighting"></a>강조 표시
hello "Highlight" 매개 변수는 toorequest hello 검색 하위 시스템을 사용할 수는 선택적 매개 변수는 해당 응답의 표식 집합을 포함 합니다.

이러한 표식은 hello 시작 및 종료 나타냅니다 검색 쿼리에 제공 된 hello 용어와 일치 하는 강조 표시 된 텍스트입니다.
지정 hello 시작 및 끝 표식을 검색어 toowrap hello 강조 표시에 사용 되는 수 있습니다.

**예제 검색 쿼리**

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

**샘플 결과:**

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

위의 결과 hello는 접두사가 있고 추가 된 오류 메시지가 들어 있습니다.

## <a name="computer-groups"></a>컴퓨터 그룹
컴퓨터 그룹은 컴퓨터 집합을 반환하는 특수한 저장된 검색입니다.  Hello 그룹의 다른 쿼리 toolimit hello 결과 toohello 컴퓨터에서 컴퓨터 그룹을 사용할 수 있습니다.  컴퓨터 그룹은 값이 Computer인 Group 태그가 있는 저장된 검색으로 구현됩니다.

다음은 컴퓨터 그룹에 대한 샘플 응답입니다.

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

### <a name="retrieving-computer-groups"></a>컴퓨터 그룹 검색
tooretrieve 컴퓨터 그룹을 사용 하 여 hello hello 그룹과 Get 메서드가 id입니다.

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>컴퓨터 그룹 만들기 또는 업데이트
컴퓨터 그룹 toocreate hello Put 메서드를 사용 하 여 저장 된 검색 고유 id 기존 컴퓨터 그룹 ID를 사용하는 경우 해당 ID가 수정됩니다. Hello 로그 분석 포털에서 컴퓨터 그룹을 만들 때 hello ID가 hello 그룹 및 이름에서 만들어집니다.

hello 쿼리 hello 그룹 정의에 사용 되는 그룹 toofunction hello에 대 한 컴퓨터 집합을 제대로 반환 해야 합니다.  와 함께 쿼리를 종료 하는 것이 좋습니다. `| Distinct Computer` tooensure hello 올바른 데이터가 반환 됩니다.

hello 저장 된 검색의 hello 정의 hello 검색 toobe 컴퓨터 그룹으로 분류에 대 한 그룹 컴퓨터의 값이 지정 하는 태그를 포함 해야 합니다.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>컴퓨터 그룹 삭제
toodelete 컴퓨터 그룹을 사용 하 여 hello hello 그룹과 Delete 메서드 id입니다.

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) toobuild 쿼리 조건에 대 한 사용자 지정 필드를 사용 합니다.
