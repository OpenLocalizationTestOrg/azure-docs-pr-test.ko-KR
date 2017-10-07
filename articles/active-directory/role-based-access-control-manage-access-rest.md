---
title: "rest-Azure AD 액세스 제어 aaaRole 기반 | Microsoft Docs"
description: "Hello REST API로 역할 기반 액세스 제어 관리"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Hello REST API로 역할 기반 액세스 제어 관리
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

역할 기반 액세스 제어 (RBAC) hello Azure 포털에서에서 Azure 리소스 관리자 API 하면 쉽게 액세스 tooyour 구독 및 세분화 된 수준에서 리소스를 관리할 수 있습니다. 이 기능을 특정 범위에서 일부 역할 toothem 할당 하 여 Active Directory 사용자, 그룹 또는 서비스 사용자에 대 한 액세스를 부여할 수 있습니다.

## <a name="list-all-role-assignments"></a>모든 역할 할당 나열
지정 된 hello에서 모든 hello 역할 할당 범위 및 subscopes 합니다.

toolist 역할 할당을 액세스할 수 있어야 너무`Microsoft.Authorization/roleAssignments/read` hello 범위에서 작업 합니다. 모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위를 원하는 toolist hello 역할 할당 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. *{api-version}* 을 2015-07-01로 바꿉니다.
3. 대체 *{filter}* tooapply toofilter hello 역할 할당 목록을 원하는 hello 조건:

   * 만 hello에 대 한 역할 할당 목록을 subscopes에서 hello 역할 할당을 포함 하지 않는 범위를 지정 합니다.`atScope()`    
   * 특정 사용자, 그룹 또는 응용 프로그램에 대해서만 역할 할당 나열: `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * 그룹에서 상속된 역할 할당을 포함하여 특정 사용자에 대한 역할 할당 나열 | `assignedTo('{objectId of user}')`

### <a name="response"></a>응답
상태 코드: 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>역할 할당에 대한 정보 가져오기
Hello 역할 할당 id에서 지정한 단일 역할 할당에 대 한 정보를 가져옵니다.

역할 할당에 대 한 tooget 정보를 액세스할 수 있어야 너무`Microsoft.Authorization/roleAssignments/read` 작업 합니다. 모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위를 원하는 toolist hello 역할 할당 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 할당 id}* hello 역할 할당의 hello GUID 식별자를 사용 합니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

### <a name="response"></a>응답
상태 코드: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>역할 할당 만들기
역할 만들기 hello 지정한 보안 주체 권한을 부여 hello 지정 된 역할에 대 한 할당 hello에 범위를 지정 합니다.

역할 할당 toocreate 권한이 너무`Microsoft.Authorization/roleAssignments/write` 작업 합니다. Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **배치** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위를 원하는 toocreate hello 역할 할당 합니다. 모든 자식 범위 상속 hello 부모 범위에서 역할 할당을 만들 때 동일한 역할 할당 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1   
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 할당 id}* hello 새 역할 할당의 GUID 식별자 hello 새 GUID를 가진 됩니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

Hello 요청 본문에 대 한 형식에 따라 hello에 hello 값을 제공 합니다.

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| 요소 이름 | 필수 | 형식 | 설명 |
| --- | --- | --- | --- |
| roleDefinitionId |예 |문자열 |hello 역할의 hello 식별자입니다. hello hello 식별자의 형식은 다음과 같습니다.`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |예 |문자열 |hello Azure AD 보안 주체 (사용자, 그룹 또는 서비스 사용자)의 objectId toowhich hello 역할 할당 됩니다. |

### <a name="response"></a>응답
상태 코드: 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>역할 할당 삭제
Delete hello에서 역할 할당 범위를 지정 합니다.

역할 할당 toodelete 있어야 액세스 toohello `Microsoft.Authorization/roleAssignments/delete` 작업 합니다. Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **삭제** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위를 원하는 toocreate hello 역할 할당 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 할당 id}* hello 역할 할당 id GUID 사용 합니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

### <a name="response"></a>응답
상태 코드: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>모든 역할 나열
지정 된 hello에 대 한 할당에 사용할 수 있는 모든 hello 역할이 나열 범위입니다.

toolist 역할 권한이 너무`Microsoft.Authorization/roleDefinitions/read` hello 범위에서 작업 합니다. 모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위를 원하는 toolist hello 역할입니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. *{api-version}* 을 2015-07-01로 바꿉니다.
3. 대체 *{filter}* 역할 목록이 toofilter hello tooapply 한다고 hello 조건:

   * 할당 hello에 사용할 수 있는 목록 역할 범위 및 해당 하위 범위 중 하나를 지정:`atScopeAndBelow()`
   * 정확한 표시 이름을 사용하여 역할 검색: `roleName%20eq%20'{role-display-name}'` Hello 역할의 정확한 표시 이름으로 hello hello URL 인코딩 형식을 사용 합니다. 예를 들어, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>응답
상태 코드: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>역할에 대한 정보 가져오기
Hello 역할 정의 id에서 지정한 단일 역할에 대 한 정보를 가져옵니다. 표시 이름을 사용 하 여 단일 역할에 대 한 tooget 정보 참조 [모든 역할을 나열](role-based-access-control-manage-access-rest.md#list-all-roles)합니다.

역할에 대 한 tooget 정보를 액세스할 수 있어야 너무`Microsoft.Authorization/roleDefinitions/read` 작업 합니다. 모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위를 원하는 toolist hello 역할 할당 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 정의 id}* hello 역할 정의의 hello GUID 식별자를 사용 합니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

### <a name="response"></a>응답
상태 코드: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>사용자 지정 역할 만들기
사용자 지정 역할을 만듭니다.

사용자 지정 역할 toocreate 권한이 너무`Microsoft.Authorization/roleDefinitions/write` 모든 hello에 대 한 작업이 `AssignableScopes`합니다. Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **배치** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello로 첫 번째 *AssignableScope* hello 사용자 지정 역할을 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 정의 id}* hello GUID 식별자 hello 새 사용자 지정 역할의 새 GUID를 가진 됩니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

Hello 요청 본문에 대 한 형식에 따라 hello에 hello 값을 제공 합니다.

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| 요소 이름 | 필수 | 형식 | 설명 |
| --- | --- | --- | --- |
| name |예 |문자열 |사용자 지정 역할 hello의 GUID 식별자입니다. |
| properties.roleName |예 |문자열 |Hello 사용자 지정 역할의 표시 이름입니다. 최대 128자입니다. |
| properties.description |아니요 |문자열 |Hello 사용자 지정 역할의 설명입니다. 최대 1024자입니다. |
| properties.type |예 |문자열 |도 "CustomRole." |
| properties.permissions.actions |예 |문자열[] |동작의 배열을 지정 하 여 hello 작업 hello 사용자 지정 역할에 의해 부여 된 문자열입니다. |
| properties.permissions.notActions |아니요 |문자열[] |Hello 작업 tooexclude hello 사용자 지정 역할에 의해 부여 된 hello 작업에서 지정 하는 동작 문자열의 배열입니다. |
| properties.assignableScopes |예 |문자열[] |배열 범위는 hello 사용자 지정 역할을 사용할 수입니다. |

### <a name="response"></a>응답
상태 코드: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>사용자 지정 역할 업데이트
사용자 지정 역할을 수정합니다.

사용자 지정 역할 toomodify 권한이 너무`Microsoft.Authorization/roleDefinitions/write` 모든 hello에 대 한 작업이 `AssignableScopes`합니다. Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **배치** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello로 첫 번째 *AssignableScope* hello 사용자 지정 역할을 합니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 정의 id}* hello 사용자 지정 역할의 hello GUID 식별자를 사용 합니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

Hello 요청 본문에 대 한 형식에 따라 hello에 hello 값을 제공 합니다.

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| 요소 이름 | 필수 | 형식 | 설명 |
| --- | --- | --- | --- |
| name |예 |문자열 |사용자 지정 역할 hello의 GUID 식별자입니다. |
| properties.roleName |예 |문자열 |사용자 지정 역할을 업데이트 하는 hello의 표시 이름입니다. |
| properties.description |아니요 |문자열 |Hello 설명 사용자 지정 역할을 업데이트 합니다. |
| properties.type |예 |문자열 |도 "CustomRole." |
| properties.permissions.actions |예 |문자열[] |Hello 작업 toowhich hello를 지정 하는 동작 문자열의 배열 액세스를 부여 하는 사용자 지정 역할을 업데이트 합니다. |
| properties.permissions.notActions |아니요 |문자열[] |동작의 배열을 지정 하 여 hello 작업 tooexclude는 hello 부여 사용자 지정 역할을 업데이트 하는 hello 작업에서 문자열입니다. |
| properties.assignableScopes |예 |문자열[] |배열 범위는 hello 업데이트 된 사용자 지정 역할을 사용할 수입니다. |

### <a name="response"></a>응답
상태 코드: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>사용자 지정 역할 삭제
사용자 지정 역할을 삭제합니다.

사용자 지정 역할 toodelete 권한이 너무`Microsoft.Authorization/roleDefinitions/delete` 모든 hello에 대 한 작업이 `AssignableScopes`합니다. Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다. Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.

### <a name="request"></a>요청
사용 하 여 hello **삭제** URI 뒤 hello로 메서드:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:

1. 대체 *{scope}* hello 범위 원하는 toodelete hello 역할 정의입니다. 다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.

   * 구독: /subscriptions/{subscription-id}  
   * 리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 대체 *{역할 정의 id}* hello hello 사용자 지정 역할의 역할 정의 id GUID 사용 합니다.
3. *{api-version}* 을 2015-07-01로 바꿉니다.

### <a name="response"></a>응답
상태 코드: 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>다음 단계

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
