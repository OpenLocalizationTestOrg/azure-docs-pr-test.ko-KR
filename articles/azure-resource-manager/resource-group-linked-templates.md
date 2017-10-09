---
title: "Azure 배포에 대 한 템플릿을 aaaLink | Microsoft Docs"
description: "Toouse 연결 하는 방법을 서식 파일에는 Azure 리소스 관리자 템플릿 toocreate 모듈식 서식 파일 솔루션에 설명 합니다. Toopass 매개 변수 값을 매개 변수 파일을 지정 하 고 동적으로 Url을 생성 하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="8a5a1-104">Azure 리소스를 배포할 때 연결된 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="8a5a1-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="8a5a1-105">하나의 Azure 리소스 관리자 템플릿 내에서 연결할 수 있습니다 toodecompose 사용할 수 있는 tooanother 서식 파일을 대상으로 하는 목적에 따른 템플릿 집합에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="8a5a1-106">응용 프로그램을 여러 코드 클래스로 분해하는 경우처럼 이러한 분해는 테스트, 다시 사용 및 가독성 측면에서 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="8a5a1-107">주 템플릿 tooa 연결 된 템플릿의 매개 변수를 전달할 수 및 이러한 매개 변수는 tooparameters 또는 서식 파일을 호출 하는 hello에 의해 노출 되는 변수에 직접 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="8a5a1-108">hello 연결 된 템플릿 템플릿 간의 양방향 데이터 교환을 활성화는 출력 변수 백 toohello 원본 템플릿을 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="8a5a1-109">Tooa 템플릿 연결</span><span class="sxs-lookup"><span data-stu-id="8a5a1-109">Linking tooa template</span></span>
<span data-ttu-id="8a5a1-110">해당 지점 toohello 연결 된 템플릿 hello 주 템플릿 내에서 배포 리소스를 추가 하 여 두 개의 템플릿 간의 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="8a5a1-111">Hello 설정 **templateLink** 속성 toohello hello 연결 된 템플릿의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="8a5a1-112">서식 파일에서 직접 또는 매개 변수 파일에 연결 된 템플릿 hello에 대 한 매개 변수 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="8a5a1-113">hello 다음 예제에서는 hello **매개 변수** 속성 toospecify 매개 변수 값을 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="8a5a1-114">다른 리소스 유형과 마찬가지로 hello 연결 된 템플릿 및 기타 리소스 간의 종속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="8a5a1-115">따라서 hello 연결 된 템플릿에서 출력 값을 요구 하는 다른 리소스를 때 앞 hello 연결 된 템플릿 배포 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="8a5a1-116">또는 hello 연결 된 템플릿을 다른 리소스를 사용 하는 경우 다른 리소스가 연결 된 템플릿 hello 하기 전에 배포 않는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="8a5a1-117">구문 다음 hello로 연결 된 서식 파일에서 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="8a5a1-118">리소스 관리자 서비스 hello 수 tooaccess hello 연결 된 템플릿 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="8a5a1-119">로컬 파일 또는 연결 된 템플릿 hello에 대 한 로컬 네트워크에 사용할 수 있는 파일을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="8a5a1-120">**http** 또는 **https** 중 하나를 포함하는 URI 값만 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="8a5a1-121">한 가지 옵션은 저장소 계정을 사용 하 여 연결 된 서식 파일에 같은 hello 다음 예제에에서 표시 된 해당 항목에 대 한 URI를 hello tooplace:</span><span class="sxs-lookup"><span data-stu-id="8a5a1-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="8a5a1-122">연결 된 템플릿 hello 여야 하지만 외부에서 사용 가능, toobe toohello 일반적으로 사용할 수 있는 public이 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="8a5a1-123">사용자 템플릿 tooa 개인 저장소 계정에 액세스할 수 있는 tooonly hello 저장소 계정 소유자가 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="8a5a1-124">그런 다음 배포 하는 동안 공유 액세스 서명 (SAS) 토큰 tooenable 액세스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="8a5a1-125">해당 SAS 토큰 toohello URI hello 연결 된 서식 파일에 대 한 추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="8a5a1-126">저장소 계정에서 템플릿을 설정하고 SAS 토큰을 생성하는 절차는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy.md) 또는 [Resource Manager 템플릿과 Azure CLI로 리소스 배포](resource-group-template-deploy-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="8a5a1-127">다음 예제는 hello 부모 템플릿의 해당 링크 tooanother 서식 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="8a5a1-128">hello 연결 된 템플릿 매개 변수로 전달 되는 SAS 토큰으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="8a5a1-129">Hello 토큰은 보안 문자열로 전달 되는 경우에 hello hello SAS 토큰을 포함 하 여 hello 연결 된 템플릿에의 URI가 로그인 hello 배포 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="8a5a1-130">toolimit 노출 hello 토큰에 대 한 만료 날짜를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="8a5a1-131">Resource Manager는 연결된 각 템플릿을 별도 배포로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="8a5a1-132">Hello 리소스 그룹에 대 한 배포 기록을 hello hello 부모 및 중첩 된 템플릿에 대 한 별도 배포를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![배포 기록](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="8a5a1-134">연결 tooa 매개 변수 파일</span><span class="sxs-lookup"><span data-stu-id="8a5a1-134">Linking tooa parameter file</span></span>
<span data-ttu-id="8a5a1-135">다음 예제에서는 hello hello를 사용 하 여 **parametersLink** 속성 toolink tooa 매개 변수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="8a5a1-136">hello URI의 값 hello 연결 된 매개 변수 파일을 로컬 파일로 일 수 없습니다 및 하나만 포함 해야 **http** 또는 **https**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="8a5a1-137">hello 매개 변수 파일에는 SAS 토큰을 통해 제한 된 tooaccess 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="8a5a1-138">변수 toolink 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8a5a1-138">Using variables toolink templates</span></span>
<span data-ttu-id="8a5a1-139">hello 앞의 예제에서는 hello 템플릿 링크에 대 한 직접 URL 값에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="8a5a1-140">이 방법은 간단한 템플릿에는 적용될 수 있지만 대규모 모듈식 템플릿 집합으로 작업하는 경우에는 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="8a5a1-141">대신 주 템플릿 hello에 대 한 기본 URL을 저장 하는 정적 변수를 만들고 기본 URL 연결 하는 hello 서식 파일에 대 한 Url를 동적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="8a5a1-142">이 방법의 hello 이점은는 쉽게 이동 또는 fork 셰이프로부터 hello 템플릿 toochange hello 정적 변수 hello 기본 서식 파일에만 필요 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="8a5a1-143">hello 주 템플릿 hello 올바른 서식 파일을 분해 하는 hello 전체 Uri를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="8a5a1-144">hello 다음 예제에서는 두 개의 Url에 대 한 연결 하는 기본 URL toocreate toouse 방법을 템플릿 (**sharedTemplateUrl** 및 **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="8a5a1-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="8a5a1-145">사용할 수도 있습니다 [배포 선정 ()](resource-group-template-functions-deployment.md#deployment) tooget hello 현재 서식 파일에 대 한 기본 URL hello 및 다른 템플릿에 hello에 대 한 해당 tooget hello URL을 사용 하 여 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="8a5a1-146">이 방법은 템플릿 위치를 변경 하는 경우에 유용 (미정 due tooversioning) 또는 원하는 tooavoid 하드 코딩 hello 템플릿 파일의 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="8a5a1-147">전체 예제</span><span class="sxs-lookup"><span data-stu-id="8a5a1-147">Complete example</span></span>
<span data-ttu-id="8a5a1-148">예제 서식 파일을 다음 hello 표시 단순화 하는 연결 된 템플릿 tooillustrate 배열을 hello 개념 중 몇 가지이 문서의.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="8a5a1-149">가정 hello 템플릿이 toohello 해제 되어 동일한 컨테이너를 공용 액세스로 저장소 계정에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="8a5a1-150">hello 연결 된 템플릿 hello의 가치 백 toohello 기본 서식 파일을 전달 **출력** 섹션.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="8a5a1-151">hello **parent.json** 파일 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-151">hello **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="8a5a1-152">hello **helloworld.json** 파일 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-152">hello **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="8a5a1-153">PowerShell에서 hello 컨테이너에 대 한 토큰 가져오고 사용 하 여 hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="8a5a1-154">Azure CLI 2.0에서 hello 컨테이너에 대 한 토큰 가져오고 코드 다음 hello로 hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="8a5a1-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a5a1-155">Next steps</span></span>
* <span data-ttu-id="8a5a1-156">리소스에 대 한 hello 배포 순서를 정의 하는 hello에 대 한 toolearn 참조 [Azure 리소스 관리자 템플릿을에서 종속성을 정의 합니다.](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="8a5a1-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="8a5a1-157">toolearn toodefine 하나의 리소스 하지만, 여러 인스턴스를 만들 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="8a5a1-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

