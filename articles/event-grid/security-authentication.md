---
title: "aaaAzure 이벤트 표 형태 보안 및 인증"
description: "Azure Event Grid 및 해당 개념을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Event Grid 보안 및 인증 

Azure Event Grid에는 세 가지 유형의 인증이 있습니다.

* 이벤트 구독
* 이벤트 게시
* WebHook 이벤트 전달

## <a name="webhook-event-delivery"></a>WebHook 이벤트 전달

Webhook이 Azure 이벤트 표 형태에서 실시간으로에서 여러 방법으로 tooreceive 이벤트 중 하나입니다.

새 이벤트 준비 toobe 배달가 있을 때마다 이벤트 표 형태 hello 본문에 tooyour WebHook hello 이벤트와 함께 사용 하는 HTTP 요청을 보냅니다.

이벤트 표 형태를 사용자 고유의 WebHook 끝점을 등록할 때는 보냅니다 있습니다 간단한 유효성 검사 코드 인 POST 요청은 순서 tooprove 끝점 소유권에. 앱 백 hello 유효성 검사 코드를 출력 하 여 toorespond가 필요 합니다. 이벤트 표 형태 이벤트 hello 유효성 검사에 통과 하지 못한 tooWebHook 끝점 배달 하지 않습니다.
 
### <a name="validation-details"></a>유효성 검사 세부 정보:

* 이벤트 구독 만들기/업데이트의 hello 시 이벤트 표 형태 "SubscriptionValidationEvent" 이벤트 toohello 대상 끝점을 게시합니다.
* hello 이벤트 "이벤트 형식:: 유효성 검사" 헤더 값을 포함합니다.
* hello 이벤트 본문 hello에 다른 이벤트 표 형태 이벤트와 동일한 스키마입니다.
* hello 이벤트 데이터 예: 임의로 생성 된 문자열에 "ValidationCode" 속성이 포함 된 “ValidationCode: acb13…”.

순서 tooprove 끝점 소유권 에코 백 hello 유효성 검사 코드 예: "ValidationResponse: acb13...".

마지막으로 Azure 이벤트 표 형태에만 HTTPS webhook 끝점 지원 되는 중요 한 toonote를입니다.
## <a name="event-subscription"></a>이벤트 구독

toosubscribe tooan 이벤트 있어야 hello **Microsoft.EventGrid/EventSubscriptions/Write** hello에 대 한 권한이 필요한 리소스입니다. Hello 리소스의 hello 범위에서 새 구독을 작성 하는 때문에이 권한이 있어야 합니다. hello 필요한 리소스 tooa 시스템 항목 또는 사용자 지정 항목은 구독 여부에 따라 다릅니다. 두 형식은 모두 이 섹션에 설명되어 있습니다.

### <a name="system-topics-azure-service-publishers"></a>시스템 항목(Azure 서비스 게시자)

시스템 항목에 대 한 사용 권한 toowrite hello 리소스 게시 hello 이벤트의 hello 범위에서 새 이벤트 구독 해야합니다. hello hello 리소스의 형식은 다음과 같습니다.`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

라는 저장소 계정에서 예를 들어 toosubscribe tooan 이벤트 **myacct**에 hello Microsoft.EventGrid/EventSubscriptions/Write 권한이 필요 합니다.`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>사용자 지정 항목

사용자 지정 항목에 대 한 사용 권한 toowrite hello 이벤트 표 형태 항목의 hello 범위에서 새 이벤트 구독 해야합니다. hello hello 리소스의 형식은 다음과 같습니다.`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

예를 들어 toosubscribe tooa 사용자 지정 항목 라는 **mytopic**에 hello Microsoft.EventGrid/EventSubscriptions/Write 권한이 필요 합니다.`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>항목 게시

항목은 SAS(공유 액세스 서명) 또는 키 인증을 사용합니다. SAS를 사용하는 것이 좋지만 키 인증에서는 간단한 프로그래밍을 제공하며 기존의 많은 Webhook 게시자와 호환 가능합니다. 

Hello HTTP 헤더에 hello 인증 값을 포함 합니다. SAS를 사용 하 여 **aeg sas 토큰** hello 헤더 값에 대 한 합니다. 키 인증을 사용 하 여 **aeg sas 키** hello 헤더 값에 대 한 합니다.

### <a name="key-authentication"></a>키 인증

키 인증은 인증의 hello 가장 간단한 형태입니다. Hello 형식을 사용 합니다.`aeg-sas-key: <your key>`

예를 들어 다음을 사용하여 키를 전달합니다. 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>SAS 토큰

이벤트 표 형태에 대 한 SAS 토큰에는 hello 리소스, 만료 시간 및 서명을 포함 됩니다. hello hello SAS 토큰 형식이: `r={resource}&e={expiration}&s={signature}`합니다.

hello 리소스 경로가 hello 항목 toowhich hello에 대 한 이벤트를 전송 됩니다. 예를 들어 올바른 리소스 경로는 다음과 같습니다. `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

키에서 hello 서명을 생성합니다.

예를 들어 유효한 **aeg-sas-token** 값은 다음과 같습니다.

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

다음 예제는 hello 이벤트 표 형태와 사용에 대 한 SAS 토큰을 만듭니다.

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>관리 액세스 제어

Azure의 이벤트 표 형태 있습니다 toocontrol hello 수준의 허용 지정 된 액세스 toodifferent 사용자 toodo 목록 이벤트 가입 등의 다양 한 관리 작업 하 고 새 데이터베이스를 만들고 키를 생성 합니다. Event Grid는 이에 대해 Azure의 RBAC(역할 기반 액세스 확인)를 활용합니다.

### <a name="operation-types"></a>작업 형식

Azure 이벤트 표 형태 hello 다음 작업을 지원 합니다.

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

안녕 마지막 세 작업 반환 잠재적으로 비밀 정보를 일반 읽기 작업에서 필터링을 가져옵니다. 하면 toorestrict 액세스 toothese 작업에 대 한 것이 좋습니다. 사용 하 여 사용자 지정 역할을 만들 수 [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure 명령줄 인터페이스 (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), 및 hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md)합니다.

### <a name="enforcing-role-based-access-check-rbac"></a>RBAC(역할 기반 액세스 확인) 적용

다른 사용자에 대해 단계 tooenforce RBAC를 수행 하는 hello를 사용 합니다.

#### <a name="create-a-custom-role-definition-file-json"></a>사용자 지정 역할 정의 파일(.json) 만들기

hello 다음은 사용자가 다른 일련의 동작 tooperform 수 있는 샘플 이벤트 표 형태 역할 정의입니다.

**EventGridReadOnlyRole.json**: 읽기 전용 작업만을 허용합니다.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: 제한된 게시 작업을 허용하지만 삭제 동작을 허용하지 않습니다.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: 모든 Event Grid 작업을 허용합니다.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>설치 및 로그인 tooAzure CLI

* Azure CLI 버전 0.8.8 이상을 사용하세요. Azure 구독으로 참조 tooinstall hello에 대 한 최신 정보 및 연결 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다.
* Azure CLI에서 Azure Resource Manager입니다. 너무 이동[hello 리소스 관리자를 사용 하 여 hello Azure CLI](../xplat-cli-azure-resource-manager.md) 내용을 확인 합니다.

#### <a name="create-a-custom-role"></a>사용자 지정 역할 만들기

사용자 지정 역할 toocreate 사용 합니다.

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Hello 역할 tooa 사용자 할당


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>다음 단계

* 소개 tooEvent 표를 참조 하세요. [이벤트 표 형태에 대 한](overview.md)
