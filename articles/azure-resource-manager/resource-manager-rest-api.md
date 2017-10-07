---
title: "관리자 REST Api aaaResource | Microsoft Docs"
description: "리소스 관리자 REST Api 인증 hello 및 사용 예제 개요"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>리소스 관리자 REST API
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [포털](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

뒤에 배포 된 모든 서식 파일에 부속 모든 호출 tooAzure 리소스 관리자 뒤에 있는 모든 구성 된 저장소 계정이 있는 경우 하나 이상의 호출 toohello Azure 리소스 관리자의 RESTful API 이 항목은 전용된 toothose Api 및 모든 SDK를 전혀 사용 하지 않고 해당를 호출 하는 방법을 합니다. 이 방법은 기본 설정된 언어에 대 한 SDK hello을 사용할 수 없거나 필요한 hello 작업을 지원 하지 하는 경우 또는 요청 tooAzure의 완전히 제어 하려는 경우에 유용 합니다.

이 문서는 Azure에서 노출 하지만 대신 일부 작업을 사용 하 여 toothem를 연결 하는 방법의 예로 모든 API 통과 하지 않으므로 합니다. Hello를 읽을 수 hello 기본 사항을 이해 하면 [Azure 리소스 관리자 REST API 참조](https://docs.microsoft.com/rest/api/resources/) toofind 대 한 상세 정보가 어떻게 toouse hello 나머지 hello Api입니다.

## <a name="authentication"></a>인증
Resource Manager에 대한 인증은 Azure AD(Active Directory)에 의해 처리됩니다. tooconnect tooany API, 먼저 Azure AD tooreceive tooevery 요청에 전달할 수 있는 인증 토큰으로 tooauthenticate 합니다. REST Api toohello 있다고 가정 하는 직접 순수 호출을 기술 하는 것 처럼 사용자 이름 및 암호를 묻는 메시지가 여 tooauthenticate를 바람직하지 않습니다. 또한 두 가지 요소 인증 메커니즘을 사용하지 않는다고 가정합니다. 따라서 Azure AD 응용 프로그램 및 서비스 보안 주체에 사용 되는 toolog 있는 섞어 만듭니다. 여러 인증 절차와 모든 Azure AD를 지원 하는지 설명 하지만 사용 되는 tooretrieve 후속 API 요청에 대 한 해당 인증 토큰 수 있습니다.
단계별 지침은 [Azure AD 응용 프로그램 및 서비스 주체 만들기](resource-group-create-service-principal-portal.md)를 따릅니다.

### <a name="generating-an-access-token"></a>액세스 토큰 생성하기
Azure AD에 대 한 인증 login.microsoftonline.com에 위치한 tooAzure 광고를를 호출 하 여 수행 됩니다. tooauthenticate, 다음 정보는 toohave hello가 필요 합니다.

* Azure AD 테 넌 트 ID (hello toolog에서 사용 하는 Azure AD의 이름, 회사와 동일 하지만 반드시 종종 hello)
* 응용 프로그램 ID (hello Azure AD 응용 프로그램 작성 단계 중에 수행)
* 암호 (즉 hello Azure AD 응용 프로그램을 만드는 동안 선택한)

HTTP 요청을 수행 하는 hello, 있는지 tooreplace "Azure AD 테 넌 트 ID", "응용 프로그램 ID" 및 "Password" hello 올바른 값을 확인 합니다.

**일반 HTTP 요청:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... (인증 성공) 하는 경우에 다음 응답 응답 비슷한 toohello 발생:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(앞에 응답 하는 hello에 hello access_token 된 약식된 tooincrease 가독성)

**Bash를 사용하여 액세스 토큰 생성하기:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Powershell을 사용하여 액세스 토큰 생성:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

hello 응답에는 액세스 토큰, 기간 해당 토큰은 유효 하는 방법에 대 한 정보 및 어떤 리소스에 대 한 해당 토큰을 사용할 수 있습니다에 대 한 정보를 포함 합니다.
hello 이전 HTTP 호출에 받은 hello 액세스 토큰에 대 한 모든 요청 toohello 리소스 관리자 API에 전달 되어야 합니다. "인증" hello 값 "전달자 YOUR_ACCESS_TOKEN" 라는 헤더 값으로 전달 합니다. Hello 간격 "Bearer" 및 액세스 토큰을 확인 합니다.

HTTP 결과 위에서 hello 알 수 있듯이는 캐시 및 동일한 토큰을 다시 사용 해야 하는 시간을 특정 기간에 대 한 hello 토큰은 유효 합니다. 각 API 호출에 대 한 Azure AD에 대해 가능한 tooauthenticate 인 경우에 수 없기 매우 효율적입니다.

## <a name="calling-resource-manager-rest-apis"></a>Resource Manager REST API 호출
이 항목에는 몇 가지 Api tooexplain hello의 기본 사용법 hello REST 작업 사용합니다. 모든 hello 작업에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자 REST Api](https://docs.microsoft.com/rest/api/resources/)합니다.

### <a name="list-all-subscriptions"></a>모든 구독 나열
할 수 있는 hello 가장 간단한 작업 중 하나에 액세스할 수 있는 toolist hello 사용 가능한 구독입니다. 요청을 수행 하는 hello, 어떻게 hello 액세스 토큰으로 전달 되어 헤더 표시 됩니다.

(실제 액세스 토큰으로 YOUR_ACCESS_TOKEN을 대체합니다.)

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... 결과적으로, 수 있게 구독 목록을이 서비스 사용자 tooaccess 허용 됨

(구독 ID는 가독성을 위해 줄였습니다)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>특정 구독의 모든 리소스 그룹 나열
리소스 관리자 Api hello로 사용할 수 있는 모든 리소스는 리소스 그룹 내부에 중첩 되어 있습니다. HTTP GET 요청을 수행 하는 hello를 사용 하 여 구독에 기존 리소스 그룹에 대 한 리소스 관리자를 쿼리할 수 있습니다. Hello 구독 ID 전달 방법에서 hello URL의 일부로이 시간을 확인 합니다.

(실제 액세스 토큰 및 구독 ID를 YOUR_ACCESS_TOKEN 및 SUBSCRIPTION_ID로 대체합니다)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

hello 얻게 응답에 따라 달라 집니다 리소스 그룹이 정의 되어 있는지 여부 그리고 있다면 개수입니다.

(구독 ID는 가독성을 위해 줄였습니다)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기
지금까지 म 했습니다만 된 쿼리 정보에 대 한 리소스 관리자 Api hello 합니다. 일부 리소스를 만든 하 hello 모두, 리소스 그룹의 가장 간단한부터 살펴보겠습니다 차례입니다. hello 다음 HTTP 요청 리소스 그룹의 선택한 지역/위치에 만들고 추가 태그 tooit 합니다.

(바꿉니다 YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME 실제 액세스 토큰, 구독 ID로, hello toocreate 리소스 그룹의 이름)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

성공 하면 응답에 따라 유사한 toohello 하는 응답을 가져오려면

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Azure에서 리소스 그룹을 성공적으로 만들었습니다. 축하합니다.

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>리소스 관리자 템플릿을 사용 하 여 리소스 tooa 리소스 그룹 배포
Resource Manager를 사용하면 템플릿을 사용하여 리소스를 배포할 수 있습니다. 템플릿은 여러 리소스 및 해당 종속성을 정의합니다. 이 섹션에 대 한 리소스 관리자 템플릿을 잘 알고 있다면 하만 표시할 toomake hello API toostart 배포를 호출 하는 방법을 가정 합니다. 템플릿을 만드는 더 자세한 내용은 [Azure Resource Manager 템플릿 작성하기](resource-group-authoring-templates.md)를 참조하세요.

서식 파일의 배포는 다른 Api를 호출 하는 많은 toohow를 다 하지 않습니다. 중요한 점은 템플릿을 배포하는 데 상당한 시간이 걸린다는 것입니다. hello API 호출만 반환 하 고이 프로토콜은 tooyou 위쪽으로 아웃 hello 배포 toofind의 상태에 대 한 개발자 tooquery hello 배포 수행 되는 경우. 자세한 내용은 [Azure 비동기 작업 추적](resource-manager-async-operations.md)을 참조하세요.

이 예제에서는 [GitHub](https://github.com/Azure/azure-quickstart-templates)에서 사용할 수 있는 공개적으로 노출된 템플릿을 사용합니다. hello 템플릿을 사용 하 여 Linux VM toohello 미국 서 부 지역을 배포 합니다. 이 예에서는 템플릿을 사용할 수 있는 GitHub와 같은 공용 저장소에서를 사용 하는 경우에 hello 요청의 일부로 hello 전체 서식 파일을 대신 전달할 수 있습니다. Hello 내에서 사용 되는 매개 변수 값 hello 요청에서 제공 하는 참고 서식 파일을 배포 합니다.

(요청에 대 한 적절 한 SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD 및 DNS_NAME_FOR_PUBLIC_IP toovalues replace)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

이 요청에 대 한 hello 긴 JSON 응답은이 설명서의 생략 된 tooimprove 가독성 되었습니다. hello 응답 만든 hello 템플릿 배포에 대 한 정보를 포함 합니다.

## <a name="next-steps"></a>다음 단계

- 비동기 REST 작업을 처리 하는 방법에 대 한 toolearn 참조 [Azure 비동기 작업을 추적](resource-manager-async-operations.md)합니다.
