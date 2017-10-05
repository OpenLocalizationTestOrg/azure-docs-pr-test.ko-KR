---
title: "Azure 서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시 | Microsoft Docs"
description: "조직의 구성원을 위한 Azure 관리되는 응용 프로그램을 만드는 방법이 나와 있습니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 39b74984ec2f89ed39753963de7fe3ff79577c9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="87855-103">내부 사용을 위한 관리되는 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="87855-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="87855-104">조직의 구성원을 위한 Azure [관리되는 응용 프로그램](managed-application-overview.md)을 만들고 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="87855-105">예를 들어 조직 표준을 준수하도록 하는 IT 부서에서 관리되는 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="87855-106">이러한 관리되는 응용 프로그램은 Azure Marketplace가 아닌 서비스 카탈로그를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-106">These managed applications are available through the service catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="87855-107">서비스 카탈로그에 대한 관리되는 응용 프로그램을 게시하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="87855-108">세 가지 필수 템플릿 파일을 포함하는 .zip 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87855-108">Create a .zip package that contains the three required template files.</span></span>
* <span data-ttu-id="87855-109">사용자의 구독에 속한 리소스 그룹에 액세스해야 하는 사용자, 그룹 또는 응용 프로그램을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-109">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="87855-110">.zip 패키지를 나타내고 ID에 대한 액세스를 요청하는 관리되는 응용 프로그램 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87855-110">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="87855-111">관리되는 응용 프로그램 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="87855-111">Create a managed application package</span></span>

<span data-ttu-id="87855-112">첫 번째 단계는 세 가지 필수 템플릿 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-112">The first step is to create the three required template files.</span></span> <span data-ttu-id="87855-113">세 파일을 모두 하나의 .zip 파일로 패키지하고, 저장소 계정과 같이 액세스할 수 있는 위치에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-113">Package all three files into a .zip file, and upload it to an accessible location, such as a storage account.</span></span> <span data-ttu-id="87855-114">관리되는 응용 프로그램 정의를 만들 때 이 .zip 파일에 대한 링크를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-114">You pass a link to this .zip file when creating the managed application definition.</span></span>

* <span data-ttu-id="87855-115">**applianceMainTemplate.json**: 이 파일은 관리되는 응용 프로그램의 일부로 프로비전되는 Azure 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-115">**applianceMainTemplate.json**: This file defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="87855-116">템플릿은 일반 Resource Manager 템플릿과 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-116">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="87855-117">예를 들어 관리되는 응용 프로그램을 통해 저장소 계정을 만들기 위해 applianceMainTemplate.json에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="87855-117">For example, to create a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="87855-118">**mainTemplate.json**: 사용자가 관리되는 응용 프로그램을 만들 때 이 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-118">**mainTemplate.json**: Users deploy this template when creating the managed application.</span></span> <span data-ttu-id="87855-119">Microsoft.Solutions/appliances 리소스 형식인 관리되는 응용 프로그램 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-119">It defines the managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="87855-120">이 파일에는 applianceMainTemplate.json의 리소스에 필요한 모든 매개 변수도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="87855-120">This file contains all the parameters you need for the resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="87855-121">이 템플릿에서 두 가지 중요한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-121">You set two important properties in this template.</span></span> <span data-ttu-id="87855-122">우선 **applianceDefinitionId** 속성은 관리되는 응용 프로그램 정의의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-122">First, the **applianceDefinitionId** property is the ID of the managed application definition.</span></span> <span data-ttu-id="87855-123">이 토픽의 뒷부분에서 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87855-123">You create the definition later in this topic.</span></span> <span data-ttu-id="87855-124">이 값을 설정할 때 관리되는 응용 프로그램 정의를 저장하는 데 사용하는 구독 및 리소스 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-124">When setting this value, you must decide which subscription and resource group to use for storing the managed application definitions.</span></span> <span data-ttu-id="87855-125">또한 정의에 대한 이름을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-125">And, you must decide on a name for the definition.</span></span> <span data-ttu-id="87855-126">ID의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-126">The ID is in the format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="87855-127">**managedResourceGroupId** 속성은 Azure 리소스가 생성되는 리소스 그룹의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-127">Second, the **managedResourceGroupId** property is the ID of the resource group where the Azure resources are created.</span></span> <span data-ttu-id="87855-128">이 리소스 그룹 이름에 대한 값을 할당하거나 사용자가 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-128">You can assign a value for this resource group name or let the user provide a name.</span></span> <span data-ttu-id="87855-129">ID의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-129">The format of the ID is:</span></span>

  <span data-ttu-id="87855-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`</span><span class="sxs-lookup"><span data-stu-id="87855-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="87855-131">다음 예제에서는 mainTemplate.json 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87855-131">The following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="87855-132">배포된 리소스에 대한 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-132">It specifies a resource group for the deployed resources.</span></span> <span data-ttu-id="87855-133">정의 ID가 **managedApplicationGroup**이라는 리소스 그룹의 **storageApp**이라는 정의를 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-133">The definition ID is set to use a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="87855-134">이러한 값을 변경하여 서로 다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-134">You can change these values to use different names.</span></span> <span data-ttu-id="87855-135">정의 ID에 사용자의 구독 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-135">Provide your own subscription ID in the definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="87855-136">**applianceCreateUiDefinition.json**: Azure Portal에서 이 파일을 사용하여 관리되는 응용 프로그램을 만드는 사용자를 위한 사용자 인터페이스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-136">**applianceCreateUiDefinition.json**: The Azure portal uses this file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="87855-137">사용자가 각 매개 변수에 대한 입력을 제공하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="87855-138">드롭다운 목록, 텍스트 상자, 암호 상자 및 기타 입력 도구와 같은 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="87855-139">관리되는 응용 프로그램에 대한 UI 정의 파일을 만드는 방법은 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-139">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="87855-140">다음 예제에서는 사용자가 텍스트 상자를 통해 저장소 계정 이름 접두사를 지정할 수 있도록 applianceCreateUiDefinition.json 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87855-140">The following example shows an applianceCreateUiDefinition.json file that enables users to specify the storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for the prefix of your storage account. Limit to 11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="87855-141">필요한 모든 파일이 준비되면 .zip 파일로 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-141">After all the needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="87855-142">세 개의 파일이 .zip 파일의 루트 수준에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-142">The three files must be at the root level of the .zip file.</span></span> <span data-ttu-id="87855-143">폴더에 배치하는 경우 관리되는 응용 프로그램 정의를 만들 때 필요한 파일이 없음을 나타내는 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="87855-143">If you put them in a folder, you receive an error when creating the managed application definition that states the required files are not present.</span></span> <span data-ttu-id="87855-144">패키지를 사용할 수 있는 액세스 가능한 위치에 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-144">Upload the package to an accessible location from where it can be consumed.</span></span> <span data-ttu-id="87855-145">이 문서의 나머지 부분에서는 .zip 파일을 공개적으로 액세스할 수 있는 저장소 blob 컨테이너에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-145">The remainder of this article assumes the .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="87855-146">Azure Active Directory 사용자 그룹 또는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="87855-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="87855-147">두 번째 단계는 고객을 대신하여 리소스를 관리하기 위해 사용자 그룹 또는 응용 프로그램을 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-147">The second step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="87855-148">이 사용자 그룹 또는 응용 프로그램에는 할당된 역할에 따라 관리되는 리소스 그룹에 대한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-148">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="87855-149">역할은 소유자 또는 참가자와 같은 기본 제공 RBAC(역할 기반 액세스 제어) 역할일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-149">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="87855-150">개별 사용자에게도 리소스를 관리할 수 있는 권한을 부여할 수 있지만, 일반적으로 사용자 그룹에 이 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-150">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="87855-151">새 Active Directory 사용자 그룹을 만들려면 [그룹을 만들고 Azure Active Directory에 구성원 추가](../active-directory/active-directory-groups-create-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-151">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="87855-152">리소스 관리에 사용할 사용자 그룹의 개체 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-152">You need the object ID of the user group to use for managing the resources.</span></span> <span data-ttu-id="87855-153">다음 예제에서는 그룹의 표시 이름에서 개체 ID를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87855-153">The following example shows how to get the object ID from the group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="87855-154">예제 명령은 다음 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-154">The example command returns the following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="87855-155">개체 ID만 검색하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-155">To retrieve just the object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-the-role-definition-id"></a><span data-ttu-id="87855-156">역할 정의 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="87855-156">Get the role definition ID</span></span>

<span data-ttu-id="87855-157">다음으로 사용자, 사용자 그룹 또는 응용 프로그램에 대한 액세스 권한을 부여하려는 RBAC 기본 제공 역할에 대한 역할 정의 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-157">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="87855-158">일반적으로 소유자 또는 참가자 또는 읽기 권한자 역할을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-158">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="87855-159">다음 명령은 소유자 역할에 대한 역할 정의 ID를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87855-159">The following command shows how to get the role definition ID for the Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="87855-160">해당 명령은 다음 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-160">That command returns the following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access to resources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="87855-161">위 예제에서 보여 주는 "name" 속성의 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-161">You need the value of the "name" property from the preceding example.</span></span> <span data-ttu-id="87855-162">다음을 통해 해당 속성만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="87855-163">관리되는 응용 프로그램 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="87855-163">Create the managed application definition</span></span>

<span data-ttu-id="87855-164">관리되는 응용 프로그램 정의를 저장하기 위한 리소스 그룹이 아직 없는 경우 지금 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87855-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="87855-165">이제 관리되는 응용 프로그램 정의 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87855-165">Now, create the managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="87855-166">앞의 예제에서 사용한 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-166">The parameters used in the preceding example are:</span></span>

* <span data-ttu-id="87855-167">**resource-group**: 관리되는 응용 프로그램 정의를 만든 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-167">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="87855-168">**lock-level**: 관리되는 리소스 그룹에 배치하는 잠금 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-168">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="87855-169">고객이 이 리소스 그룹에서 바람직하지 않은 작업을 수행할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-169">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="87855-170">현재 지원되는 유일한 잠금 수준은 ReadOnly입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-170">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="87855-171">ReadOnly를 지정하는 경우 고객은 관리되는 리소스 그룹에 있는 리소스만 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-171">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span>
* <span data-ttu-id="87855-172">**authorizations**: 관리되는 리소스 그룹에 권한을 부여하는 데 사용되는 보안 주체 ID 및 역할 정의 ID를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-172">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="87855-173">`<principalId>:<roleDefinitionId>` 형식으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="87855-173">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="87855-174">이 속성에는 여러 값을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87855-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="87855-175">여러 값이 필요하면 `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>` 형식으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87855-175">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="87855-176">여러 값은 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="87855-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="87855-177">**package-file-uri**: Azure Storage Blob일 수 있는 템플릿 파일이 포함된 관리되는 응용 프로그램 패키지의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="87855-177">**package-file-uri**: The location of the managed application package that contains the template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87855-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87855-178">Next steps</span></span>

* <span data-ttu-id="87855-179">관리되는 응용 프로그램에 대한 소개는 [관리되는 응용 프로그램 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-179">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="87855-180">파일의 예제는 [관리되는 응용 프로그램 샘플](https://github.com/Azure/azure-managedapp-samples/tree/master/samples)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-180">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="87855-181">서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="87855-182">Azure Marketplace에 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [Marketplace의 Azure 관리되는 응용 프로그램](managed-application-author-marketplace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-182">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="87855-183">Marketplace의 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [Marketplace의 Azure 관리되는 응용 프로그램 사용](managed-application-consume-marketplace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-183">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="87855-184">관리되는 응용 프로그램에 대한 UI 정의 파일을 만드는 방법은 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87855-184">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
