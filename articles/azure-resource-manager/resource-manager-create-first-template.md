---
title: "첫 번째 Azure 리소스 관리자 템플릿 aaaCreate | Microsoft Docs"
description: "단계별 가이드 toocreating 첫 번째 Azure 리소스 관리자 서식 파일에 있습니다. Toouse 저장소 계정 toocreate hello 템플릿에 대 한 템플릿 참조 hello 하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="fee6b-104">첫 번째 Azure Resource Manager 템플릿을 만들고 배포</span><span class="sxs-lookup"><span data-stu-id="fee6b-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="fee6b-105">이 항목의 첫 번째 여 Azure 리소스 관리자 템플릿을 만드는 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="fee6b-106">리소스 관리자 템플릿은 toodeploy 솔루션에 필요한 hello 리소스 정의 하는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="fee6b-107">배포 하 고 Azure 솔루션 관리와 관련 된 toounderstand hello 개념 참조 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="fee6b-108">기존 리소스가 있는 해당 리소스에 대해 tooget 서식 파일을 원하는 경우 참조 [기존 리소스에서 Azure 리소스 관리자 템플릿 내보내기](resource-manager-export-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="fee6b-109">toocreate 및 개정 템플릿에서 JSON 편집기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="fee6b-110">[Visual Studio Code](https://code.visualstudio.com/)는 간단한 오픈 소스 크로스 플랫폼 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="fee6b-111">Visual Studio Code를 사용하여 Resource Manager 템플릿을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="fee6b-112">이 항목에서는 VS 코드를 사용한다고 가정하지만 다른 JSON 편집기(예: Visual Studio)가 있는 경우 해당 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fee6b-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fee6b-113">Prerequisites</span></span>

* <span data-ttu-id="fee6b-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fee6b-114">Visual Studio Code.</span></span> <span data-ttu-id="fee6b-115">필요한 경우 [https://code.visualstudio.com/](https://code.visualstudio.com/)에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="fee6b-116">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="fee6b-116">An Azure subscription.</span></span> <span data-ttu-id="fee6b-117">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="fee6b-118">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="fee6b-118">Create template</span></span>

<span data-ttu-id="fee6b-119">저장소 계정 tooyour 구독을 배포 하는 간단한 템플릿을 사용 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="fee6b-120">**파일** > **새 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-120">Select **File** > **New File**.</span></span> 

   ![새 파일](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="fee6b-122">복사한 파일에 JSON 구문 다음 hello를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-122">Copy and paste hello following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="fee6b-123">저장소 계정 이름에 어려운 tooset 게 사용할 수 있는 몇 가지 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="fee6b-124">hello 이름 길이 사용 하 여만 숫자 및 소문자, 3 자에서 24 자 사이 여야 하 고 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="fee6b-125">hello 이전 템플릿을 사용 하 여 hello [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate 해시 값을 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="fee6b-126">hello 접두사를 추가, 즉 자세히 toogive이이 해시 값 *저장소*합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="fee6b-127">이 파일을 저장 **azuredeploy.json** tooa 로컬 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![템플릿 저장](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="fee6b-129">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="fee6b-129">Deploy template</span></span>

<span data-ttu-id="fee6b-130">사용자는 준비 toodeploy이 서식이 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="fee6b-131">PowerShell 또는 Azure CLI toocreate 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="fee6b-132">그런 다음, 저장소 계정 toothat 리소스 그룹을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="fee6b-133">PowerShell을 hello 명령을 hello 서식 파일을 포함 하는 hello 폴더에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="fee6b-134">Azure CLI의 로컬 설치의 경우 hello 명령을 hello 서식 파일을 포함 하는 hello 폴더에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="fee6b-135">배포 완료 되 면 hello 리소스 그룹에 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="fee6b-136">Cloud Shell에서 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="fee6b-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="fee6b-137">사용할 수 있습니다 [클라우드 셸](../cloud-shell/overview.md) toorun hello Azure CLI 서식 파일을 배포 하기 위한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="fee6b-138">그러나 먼저 로드 해야 서식 파일을 hello 파일 공유에 클라우드 셸에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="fee6b-139">Cloud Shell을 사용해 본 적이 없다면 [Azure Cloud Shell 개요](../cloud-shell/overview.md)에서 Cloud Shell 설정 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fee6b-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="fee6b-140">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="fee6b-141">Cloud Shell 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="fee6b-142">hello 이름 패턴은 `cloud-shell-storage-<region>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![리소스 그룹 선택](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="fee6b-144">클라우드 셸에 대 한 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-144">Select hello storage account for your Cloud Shell.</span></span>

   ![저장소 계정 선택](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="fee6b-146">**파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-146">Select **Files**.</span></span>

   ![파일 선택](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="fee6b-148">클라우드 셸용 hello 파일 공유를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="fee6b-149">hello 이름 패턴은 `cs-<user>-<domain>-com-<uniqueGuid>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![파일 공유 선택](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="fee6b-151">**디렉터리 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-151">Select **Add directory**.</span></span>

   ![디렉터리 추가](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="fee6b-153">이름을 **templates**로 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-153">Name it **templates**, and select **Okay**.</span></span>

   ![디렉터리 이름 지정](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="fee6b-155">새 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-155">Select your new directory.</span></span>

   ![디렉터리 선택](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="fee6b-157">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-157">Select **Upload**.</span></span>

   ![업로드 선택](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="fee6b-159">템플릿을 찾아서 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-159">Find and upload your template.</span></span>

   ![파일 업로드](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="fee6b-161">열기 hello 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-161">Open hello prompt.</span></span>

   ![Cloud Shell 열기](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="fee6b-163">Hello 명령을 hello 클라우드 셸에서에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="fee6b-164">배포 완료 되 면 hello 리소스 그룹에 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="fee6b-165">Hello 템플릿을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="fee6b-165">Customize hello template</span></span>

<span data-ttu-id="fee6b-166">hello 템플릿 정상적으로 작동 하지만 유연한있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="fee6b-167">항상 로컬 중복 저장소 tooSouth 중미 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="fee6b-168">hello 이름은 항상 *저장소* 다음 해시 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="fee6b-169">tooenable hello 템플릿을 사용 하 여 다양 한 시나리오에 대 한 매개 변수 toohello 서식 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="fee6b-170">hello 다음 예제에서는 두 개의 매개 변수를 사용 하 여 hello 매개 변수 섹션</span><span class="sxs-lookup"><span data-stu-id="fee6b-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="fee6b-171">첫 번째 매개 변수를 hello `storageSKU` toospecify hello 종류의 중복 항목 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="fee6b-172">Hello 값 저장소 계정에 대해 사용할 수 있는 toovalues에 전달할 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="fee6b-173">또한 기본값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-173">It also specifies a default value.</span></span> <span data-ttu-id="fee6b-174">두 번째 매개 변수를 hello `storageNamePrefix` 집합 tooallow 11 자 최대입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="fee6b-175">기본값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="fee6b-176">Hello 변수 섹션에서 명명 된 변수를 추가 `storageName`합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="fee6b-177">Hello 매개 변수에서 hello 접두사 값과 hello에서 해시 값을 결합 하 여 [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="fee6b-178">Hello를 사용 하 여 [toLower](resource-group-template-functions-string.md#tolower) tooconvert 모든 문자 toolowercase 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="fee6b-179">toouse hello 리소스 정의 변경 하는 저장소 계정에 이러한 새 값:</span><span class="sxs-lookup"><span data-stu-id="fee6b-179">toouse these new values for your storage account, change hello resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="fee6b-180">해당 hello 확인 hello 저장소 계정의 이름을 이제 사용자가 추가한 toohello 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="fee6b-181">hello SKU 이름 toohello hello 매개 변수 값을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="fee6b-182">hello 위치가 설정 hello 같은 hello 리소스 그룹 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="fee6b-183">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-183">Save your file.</span></span> 

<span data-ttu-id="fee6b-184">이 문서의 hello 단계를 완료 한 후 해당 템플릿을 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-184">After completing hello steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="fee6b-185">템플릿 다시 배포</span><span class="sxs-lookup"><span data-stu-id="fee6b-185">Redeploy template</span></span>

<span data-ttu-id="fee6b-186">값이 서로 다른 hello 템플릿을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="fee6b-187">PowerShell의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="fee6b-188">Azure CLI의 경우 </span><span class="sxs-lookup"><span data-stu-id="fee6b-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="fee6b-189">클라우드 셸 hello에 대 한 변경 된 템플릿을 toohello 파일 공유에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="fee6b-190">Hello 기존 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-190">Overwrite hello existing file.</span></span> <span data-ttu-id="fee6b-191">그런 다음 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="fee6b-192">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="fee6b-192">Clean up resources</span></span>

<span data-ttu-id="fee6b-193">더 이상 필요 hello 리소스 그룹을 삭제 하 여 배포 된 hello 리소스를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="fee6b-194">PowerShell의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="fee6b-195">Azure CLI의 경우 </span><span class="sxs-lookup"><span data-stu-id="fee6b-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="fee6b-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fee6b-196">Next steps</span></span>
* <span data-ttu-id="fee6b-197">참조는 템플릿의 hello 구조에 대해 자세히 toolearn [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fee6b-198">저장소 계정에 대 한 hello 속성에 대 한 toolearn 참조 [저장소 계정 템플릿 참조](/azure/templates/microsoft.storage/storageaccounts)합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="fee6b-199">다양 한 유형의 솔루션에 대 한 전체 템플릿을 tooview 참조 hello [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fee6b-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
