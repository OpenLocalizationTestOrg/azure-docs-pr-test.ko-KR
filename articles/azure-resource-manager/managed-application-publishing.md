---
title: "aaaCreate Azure 서비스 관리 되는 카탈로그 응용 프로그램을 게시 하 고 | Microsoft Docs"
description: "Azure toocreate 조직의 구성원을 위한 것은 응용 프로그램을 관리 하는 방법을 보여 줍니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="17c7f-103">내부 사용을 위한 관리되는 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="17c7f-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="17c7f-104">조직의 구성원을 위한 Azure [관리되는 응용 프로그램](managed-application-overview.md)을 만들고 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="17c7f-105">예를 들어 조직 표준을 준수하도록 하는 IT 부서에서 관리되는 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="17c7f-106">이러한 관리 되는 응용 프로그램은 hello 서비스 카탈로그 하지 hello Azure 마켓플레이스를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="17c7f-107">toopublish hello 서비스 카탈로그에 대 한 관리 되는 응용 프로그램을 다음과 같이합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="17c7f-108">Hello 세 필요한 템플릿 파일이 포함 된.zip 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="17c7f-109">결정 하는 사용자, 그룹 또는 응용 프로그램 hello 사용자의 구독에서 toohello 리소스 그룹에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="17c7f-110">Toohello.zip 패키지 가리키고 hello id에 대 한 액세스를 요청 하는 hello 관리 되는 응용 프로그램 정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="17c7f-111">관리되는 응용 프로그램 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="17c7f-111">Create a managed application package</span></span>

<span data-ttu-id="17c7f-112">hello 첫 번째 단계는 toocreate hello 세 필요한 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="17c7f-113">모든 세 파일이.zip 파일로 패키지 하 고 저장소 계정과 같은 tooan 액세스할 수 있는 위치를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="17c7f-114">만드는 hello 관리 응용 프로그램 정의 하는 경우 링크 toothis.zip 파일을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="17c7f-115">**applianceMainTemplate.json**:이 파일은 Azure hello 정의 hello의 일부로 프로 비전 되는 리소스 관리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="17c7f-116">hello 서식 파일은 일반 리소스 관리자 템플릿을 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="17c7f-117">예를 들어 관리 되는 응용 프로그램을 통해 저장소 계정 toocreate applianceMainTemplate.json 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="17c7f-118">**mainTemplate.json**: 사용자가 응용 프로그램 관리 hello를 만들 때이 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="17c7f-119">리소스 형식이 Microsoft.Solutions/appliances hello 관리 되는 응용 프로그램 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="17c7f-120">이 파일 applianceMainTemplate.json의 hello 리소스에 필요한 모든 hello 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="17c7f-121">이 템플릿에서 두 가지 중요한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-121">You set two important properties in this template.</span></span> <span data-ttu-id="17c7f-122">첫째, hello **applianceDefinitionId** 속성은 hello ID hello 관리 되는 응용 프로그램 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="17c7f-123">이 항목의 뒷부분에 나오는 hello 정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="17c7f-124">이 값을 설정할 때에 구독 및 리소스 그룹 toouse 저장 하기 위한 관리 되는 응용 프로그램 정의 hello 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="17c7f-125">및 hello 정의 이름을 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="17c7f-126">hello ID는 hello 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="17c7f-127">둘째, hello **managedResourceGroupId** 속성 hello Azure 리소스 만들어지는 hello hello 리소스 그룹 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="17c7f-128">이 리소스 그룹 이름에 대 한 값을 할당 하거나 hello 사용자 이름을 제공 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="17c7f-129">hello hello ID의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="17c7f-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`</span><span class="sxs-lookup"><span data-stu-id="17c7f-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="17c7f-131">다음 예제는 hello mainTemplate.json 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="17c7f-132">배포 된 hello 리소스에 대 한 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="17c7f-133">hello 정의 ID가 정의 명명 된 집합 toouse **storageApp** 리소스 그룹 이름은 **managedApplicationGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="17c7f-134">이러한 값 toouse 서로 다른 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-134">You can change these values toouse different names.</span></span> <span data-ttu-id="17c7f-135">Hello 정의 ID에 해당 하는 구독 ID를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-135">Provide your own subscription ID in hello definition ID.</span></span>

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

* <span data-ttu-id="17c7f-136">**applianceCreateUiDefinition.json**: hello Azure 포털 사용 하 여이 파일 toogenerate hello 사용자 인터페이스를 만드는 사용자가 관리 되는 응용 프로그램 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="17c7f-137">사용자가 각 매개 변수에 대한 입력을 제공하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="17c7f-138">드롭다운 목록, 텍스트 상자, 암호 상자 및 기타 입력 도구와 같은 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="17c7f-139">toocreate는 관리 되는 응용 프로그램에 대 한 UI 정의 파일을 확인 하려면 어떻게 해야 toolearn [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="17c7f-140">hello 다음 예제에서는 사용자가 toospecify hello 저장소 계정 이름 접두사를 맞추면 textbox 통해 사용 하도록 설정 하는 applianceCreateUiDefinition.json 파일</span><span class="sxs-lookup"><span data-stu-id="17c7f-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

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
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
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

<span data-ttu-id="17c7f-141">모든 필요한 hello 파일 준비 되 면.zip 파일로 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="17c7f-142">hello 3 개의 파일 hello.zip 파일의 hello 루트 수준에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="17c7f-143">폴더에 배치 하면 응용 프로그램 정의 파일이 없는 hello 필요한 상태를 관리 하는 hello를 만들 때 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="17c7f-144">Hello 패키지 tooan 사용 될 수에서 액세스할 수 있는 위치를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="17c7f-145">이 문서의 나머지 부분에서는 hello hello.zip 파일을 공개적으로 액세스할 수 있는 저장소 blob 컨테이너에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="17c7f-146">Azure Active Directory 사용자 그룹 또는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="17c7f-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="17c7f-147">hello 두 번째 단계는 tooselect 사용자 그룹 또는 응용 프로그램 hello 고객을 대신 하 여 hello 리소스를 관리 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="17c7f-148">이 사용자 그룹 또는 응용 프로그램 hello 관리 되는 리소스 그룹에 따라 toohello 역할에 할당 된 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="17c7f-149">hello 역할 소유자 또는 참가자와 같은 모든 기본 제공 역할 기반 액세스 제어 (RBAC) 역할 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="17c7f-150">또한 제공할 수 있습니다는 개별 사용자 권한 toomanage hello 리소스 있지만 일반적으로이 권한이 tooa 사용자 그룹에 할당할.</span><span class="sxs-lookup"><span data-stu-id="17c7f-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="17c7f-151">새 Active Directory 사용자 그룹 toocreate 참조 [그룹을 만들고 Azure Active Directory에 멤버를 추가](../active-directory/active-directory-groups-create-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="17c7f-152">Hello 리소스를 관리 하기 위한 사용자 그룹 toouse hello의 hello 개체 ID를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="17c7f-153">다음 예제는 hello tooget hello 그룹의 표시 이름에서 개체 ID를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="17c7f-154">hello 예제 명령은 hello 다음 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="17c7f-155">tooretrieve 정당한 hello 개체 ID를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="17c7f-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="17c7f-156">Hello 역할 정의 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="17c7f-156">Get hello role definition ID</span></span>

<span data-ttu-id="17c7f-157">다음으로, hello RBAC 기본 제공 역할 toogrant 액세스 toohello 사용자, 사용자 그룹 또는 응용 프로그램의 역할 정의 ID hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="17c7f-158">일반적으로 hello 소유자 또는 참가자 또는 판독기 역할 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="17c7f-159">다음 명령을 hello tooget hello 소유자 역할에 대 한 역할 정의 ID를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="17c7f-160">해당 명령은 hello 다음 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
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

<span data-ttu-id="17c7f-161">Hello hello 예에서는 앞에서 hello "name" 속성 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="17c7f-162">다음을 통해 해당 속성만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="17c7f-163">관리 되는 hello 응용 프로그램 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="17c7f-163">Create hello managed application definition</span></span>

<span data-ttu-id="17c7f-164">관리되는 응용 프로그램 정의를 저장하기 위한 리소스 그룹이 아직 없는 경우 지금 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="17c7f-165">이제 hello 관리 되는 응용 프로그램 정의 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-165">Now, create hello managed application definition resource.</span></span>

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

<span data-ttu-id="17c7f-166">hello 매개 변수 앞 예제는 hello에 사용 되는.</span><span class="sxs-lookup"><span data-stu-id="17c7f-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="17c7f-167">**리소스 그룹**: hello 관리 응용 프로그램 정의 hello 리소스 그룹의 hello 이름이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="17c7f-168">**잠금 수준을**: hello 유형의 잠금이 hello 관리 되는 리소스 그룹에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="17c7f-169">Hello 고객을이 리소스 그룹에 바람직하지 않은 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="17c7f-170">현재 읽기 전용은 hello 잠금 수준 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="17c7f-171">ReadOnly를 지정 하는 경우 hello 고객은 hello 리소스 hello 관리 되는 리소스 그룹에만 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="17c7f-172">**권한 부여**: 사용 되는 toogrant 권한 toohello 관리 되는 리소스 그룹은 보안 주체 ID hello 및 hello 역할 정의 ID에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="17c7f-173">hello 형식에 지정 된 `<principalId>:<roleDefinitionId>`합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="17c7f-174">이 속성에는 여러 값을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="17c7f-175">여러 값이 필요 하지만 지정 hello 형태로 `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="17c7f-176">여러 값은 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="17c7f-177">**패키지 파일 uri**: hello Azure 저장소 blob 수 있는 hello 템플릿 파일을 포함 하는 hello 관리 되는 응용 프로그램 패키지의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17c7f-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17c7f-178">Next steps</span></span>

* <span data-ttu-id="17c7f-179">소개 toomanaged 응용 프로그램에 대 한 참조 [관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="17c7f-180">Hello 파일의 예 참조 [관리 응용 프로그램 샘플](https://github.com/Azure/azure-managedapp-samples/tree/master/samples)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="17c7f-181">서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17c7f-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="17c7f-182">게시는 관리 되는 응용 프로그램 toohello Azure Marketplace에 대 한 정보를 참조 하십시오. [Azure 마켓플레이스 hello에 대 한 응용 프로그램 관리](managed-application-author-marketplace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="17c7f-183">Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="17c7f-184">toocreate는 관리 되는 응용 프로그램에 대 한 UI 정의 파일을 확인 하려면 어떻게 해야 toolearn [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17c7f-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
