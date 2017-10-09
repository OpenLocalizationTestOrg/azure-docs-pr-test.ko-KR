---
title: "Azure 활동 로그 aaaArchive hello | Microsoft Docs"
description: "Tooarchive Azure 활동 로그 하는 방법은 저장소 계정에 대 한 장기 보존을 위해에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Hello Azure 활동 로그를 보관 합니다.
이 문서에서는 hello Azure 포털, PowerShell Cmdlet 또는 플랫폼 간 CLI tooarchive를 사용 하는 방법을 보여줍니다 프로그램 [ **Azure 활동 로그** ](monitoring-overview-activity-logs.md) 저장소 계정에 있습니다. 이 옵션에 대 한 hello 보존 정책에 대해 모든 권한) (있음 90 일 이상 활동 로그 분석 정적 분석 또는 백업 tooretain 원하는 경우에 유용 합니다. Tooretain만 필요한 경우 작업 로그 이벤트를 보존할 hello Azure 플랫폼에서에서 90 일 동안 보관을 사용 하지 않고 이후 90 일 동안 개 이하인 이벤트 tooset tooa 보관 저장소 계정이 필요 하지 않습니다.

## <a name="prerequisites"></a>필수 조건
시작 하기 전에 해야 너무[저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich 활동 로그를 보관할 수 있습니다. Toomonitoring 데이터 액세스를 더 잘 제어할 수 있도록에 저장 된 다른, 비 모니터링 데이터가 있는 기존 저장소 계정을 사용 하지 않는 것이 좋습니다. 그러나 또한 보관 하는 경우 진단 로그 및 메트릭 tooa 저장소 계정, 사항이 감지 toouse 해당 저장소 계정 로그에 대 한 활동도 tookeep 모든 모니터링 데이터를 중앙 위치에. hello 사용 하는 저장소 계정에는 일반적인 용도의 스토리지 계정, blob 저장소 계정 이어야 합니다. 저장소 계정 hello이 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 구독과 동일한 구독 합니다.

## <a name="log-profile"></a>로그 프로필
hello 설정 tooarchive hello 아래 hello 방법 중 하나를 사용 하 여 활동 로그, **로그 프로필** 구독에 대 한 합니다. hello 로그 프로필 hello 형식의 저장 되는지 아니면 스트리밍되는지를 하는 이벤트를 정의 하 고 출력 hello-저장소 계정 및/또는 이벤트 허브입니다. 또한 저장소 계정에 저장 된 이벤트에 대 한 hello 보존 정책 (tooretain 일 수)을 정의 합니다. Hello 보존 정책이 toozero 설정 되 면 이벤트 무기한 저장 됩니다. 그렇지 않은 경우이 수 값을 설정할 수 tooany 1과 2147483647 사이입니다. 보존 정책이 적용 된 매일 많으면 hello 때 종료 시간 (UTC)는 이제 hello 보존 정책을 불가능 hello 날짜 로부터 기록 되므로 삭제 됩니다. 예를 들어 1 일의 보존 정책의 설치한 경우 hello 하루의 오늘 hello 시작 부분에 hello hello 이틀 전에서에서 로그 삭제 됩니다. [여기에서 로그 프로필에 대한 자세한 내용을 확인할 수 있습니다](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>보관 hello hello 포털을 사용 하 여 활동 로그
1. Hello 포털에서을 클릭 hello **활동 로그** hello 왼쪽 탐색 모음에 링크 합니다. 활동 로그 hello에 대 한 링크 보이지 않으면 클릭 hello **더 서비스** 먼저 연결 합니다.
   
    ![TooActivity 로그 블레이드를 탐색 합니다.](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Hello 블레이드의 hello 위쪽 클릭 **내보내기**합니다.
   
    ![Hello 내보내기 단추를 클릭 합니다.](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. 표시 되는 hello 블레이드에서 확인란 hello에 대 한 **tooa 저장소 계정을 내보내기** 하 고 저장소 계정을 선택 합니다.
   
    ![저장소 계정 설정](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Hello 슬라이더 또는 텍스트 상자를 사용 하 여, 정의할을 저장소 계정에 이벤트 활동 로그를 보관할 일 수 있습니다. 데이터 무기한 hello 저장소 계정에 유지 toohave 선호 하는 경우이 숫자 toozero를 설정 합니다.
5. **Save**를 클릭합니다.

## <a name="archive-hello-activity-log-via-powershell"></a>Hello PowerShell 통해 활동 로그를 보관 합니다.
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| StorageAccountId |아니요 |저장소 계정 toowhich hello 활동 로그의 리소스 ID는 저장 해야 합니다. |
| 위치 |예 |쉼표로 구분 된 목록 하려는 toocollect 활동 로그 이벤트는 영역입니다. 지역 모두의 목록을 볼 수 있습니다 [이 페이지를 방문 하 여](https://azure.microsoft.com/en-us/regions) 또는 사용 하 여 [Azure 관리 REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx)합니다. |
| RetentionInDays |예 |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. Hello 로그를 무기한으로 저장 값이 0 (무제한). |
| 범주 |예 |수집할 쉼표로 구분된 이벤트 범주 목록입니다. 가능한 값은 쓰기, 삭제 및 작업입니다. |

## <a name="archive-hello-activity-log-via-cli"></a>Hello CLI 통해 활동 로그를 보관 합니다.
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| name |예 |로그 프로필의 이름입니다. |
| storageId |아니요 |저장소 계정 toowhich hello 활동 로그의 리소스 ID는 저장 해야 합니다. |
| 위치 |예 |쉼표로 구분 된 목록 하려는 toocollect 활동 로그 이벤트는 영역입니다. 지역 모두의 목록을 볼 수 있습니다 [이 페이지를 방문 하 여](https://azure.microsoft.com/en-us/regions) 또는 사용 하 여 [Azure 관리 REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx)합니다. |
| RetentionInDays |예 |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. 값이 0 hello 로그를 무기한으로 저장 됩니다 (계속). |
| 범주 |예 |수집할 쉼표로 구분된 이벤트 범주 목록입니다. 가능한 값은 쓰기, 삭제 및 작업입니다. |

## <a name="storage-schema-of-hello-activity-log"></a>저장소 스키마의 hello 활동 로그
설정한 후 보관, 작업 로그 이벤트가 발생 하는 즉시 저장소 컨테이너 hello 저장소 계정에 생성 됩니다. hello 컨테이너 내 blob hello hello hello 활동 로그 및 진단 로그에서 동일한 형식에 따라 합니다. 이러한 blob의 hello 구조는.

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
> 
> 

예를 들어 Blob 이름은 다음과 같습니다.

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

각 PT1H.json blob hello blob URL에 지정 된 hello 시간 이내에 발생 한 이벤트의 JSON blob에 포함 (예: h = 12). 현재 시간 hello 하는 동안 이벤트는 나타나는 순서 대로 추가 toohello PT1H.json 파일입니다. 분 값 hello (m 00 =)는 항상 00, 이후 활동 로그 이벤트 1 시간 마다 각 blob으로 나뉩니다.

Hello PT1H.json 파일 내에서 각 이벤트는이 형식에 따라 레코드"hello" 배열에 저장 됩니다.

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| 요소 이름 | 설명 |
| --- | --- |
| 실시간 |Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다. |
| resourceId |Hello의 리소스 ID 리소스를 저하 됩니다. |
| operationName |Hello 작업의 이름입니다. |
| 카테고리 |범주 hello 동작의 예입니다. (예: 쓰기, 읽기, 작업) |
| resultType |hello 결과의 형식 예: hello 합니다. (예: 성공, 실패, 시작) |
| resultSignature |Hello 리소스 종류에 따라 다릅니다. |
| durationMS |밀리초에서 hello 작업 기간 |
| callerIpAddress |Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 IP 주소입니다. |
| CorrelationId |일반적으로 hello 문자열 형식의 GUID입니다. CorrelationId를 공유 하는 이벤트가 속하는지 toohello 같은 uber 작업 합니다. |
| ID |Hello 권한 부여 및 클레임 설명 하는 JSON blob입니다. |
| 권한 부여 |Hello 이벤트의 RBAC 속성의 blob입니다. 일반적으로 hello "action", "role" 및 "범위" 속성이 포함 됩니다. |
| level |Hello 이벤트의 수준입니다. Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose" |
| location |오류가 발생 했습니다. (또는 전역) hello 위치의 영역입니다. |
| properties |설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (예: 사전). |

> [!NOTE]
> hello 속성 및 해당 속성의 사용 현황 hello 리소스에 따라 달라질 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [분석을 위한 Blob 다운로드](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Hello 활동 로그 tooEvent 허브 스트림](monitoring-stream-activity-logs-event-hubs.md)
* [활동 로그 hello에 대 한 자세한 내용](monitoring-overview-activity-logs.md)

