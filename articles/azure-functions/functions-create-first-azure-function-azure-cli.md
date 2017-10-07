---
title: "첫 번째 함수에서 hello Azure CLI aaaCreate | Microsoft Docs"
description: "자세한 방법을 사용 하 여 서버 없이 실행에 대 한 첫 번째 Azure 작동 toocreate hello Azure CLI 합니다."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="08440-103">Hello Azure CLI를 사용 하 여 첫 번째 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="08440-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="08440-104">이 빠른 시작 자습서 방법 안내 toouse Azure 함수 toocreate 첫 번째 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="08440-105">Hello Azure CLI toocreate는 hello 함수를 호스팅하는 서버가 없는 인프라 함수 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="08440-106">hello 함수 코드 자체가 GitHub 샘플 리포지토리에서 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08440-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="08440-107">Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08440-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="08440-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="08440-108">Prerequisites</span></span> 

<span data-ttu-id="08440-109">이 샘플을 실행 하기 전에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="08440-110">활성 [GitHub](https://github.com) 계정</span><span class="sxs-lookup"><span data-stu-id="08440-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="08440-111">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="08440-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="08440-112">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="08440-113">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="08440-114">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="08440-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="08440-115">Create a resource group</span></span>

<span data-ttu-id="08440-116">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="08440-117">Azure 리소스 그룹은 함수 앱, 데이터베이스, 저장소 계정이 관리되었는지 등 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="08440-118">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="08440-119">Cloud Shell을 사용하지 않는 경우 먼저 `az login`을 사용하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="08440-120">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="08440-120">Create an Azure Storage account</span></span>

<span data-ttu-id="08440-121">함수는 Azure 저장소 계정 toomaintain 상태 및 함수에 대 한 기타 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="08440-122">Hello를 사용 하 여 만든 hello 리소스 그룹에서 저장소 계정을 만드는 [az 저장소 계정에 create](/cli/azure/storage/account#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="08440-123">Hello hello 나타나는 직접 전역적으로 고유한 저장소 계정 이름을 대체한 다음 명령을, `<storage_name>` 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="08440-124">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08440-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="08440-125">Hello 저장소 계정이 생성 된 후 Azure CLI hello 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08440-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a><span data-ttu-id="08440-126">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="08440-126">Create a function app</span></span>

<span data-ttu-id="08440-127">함수는 함수 앱 toohost hello 실행을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="08440-128">hello 함수 응용 프로그램 서버가 없는 함수 코드 실행에 대 한 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="08440-129">이를 통해 함수를 논리 단위로 그룹화하여 더욱 쉽게 리소스를 관리, 배포 및 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08440-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="08440-130">Hello를 사용 하 여 함수 앱 만들기 [az functionapp 만들](/cli/azure/functionapp#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="08440-131">Hello에 다음 명령을, 직접 고유한 함수 앱 이름을 대체 hello 나타나는 `<app_name>` 에 대 한 저장소 계정 이름 자리 표시자와 hello `<storage_name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="08440-132">hello `<app_name>` hello 함수 앱 등 hello 이름에 대 한 기본 DNS 도메인 hello 요구 사항에 맞춰 toobe 고유 Azure에서 모든 앱에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08440-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="08440-133">기본적으로 함수 앱 hello 소비 호스팅 계획에 리소스는 해당 함수가 필요에 따라 동적으로 추가 하 고 함수를 실행 하는 경우 요금만 지불 하기 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="08440-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="08440-134">자세한 내용은 참조 [선택 hello 올바른 호스팅 계획](functions-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="08440-135">Hello 함수 앱을 만든 후 Azure CLI hello 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08440-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="08440-136">함수 앱을가지고 hello GitHub 샘플 리포지토리에서 hello 실제 함수 코드를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08440-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="08440-137">함수 코드 배포</span><span class="sxs-lookup"><span data-stu-id="08440-137">Deploy your function code</span></span>  

<span data-ttu-id="08440-138">여러 가지 방법으로 toocreate 함수 코드에에서는 새 함수 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="08440-139">이 항목에는 GitHub의 tooa 샘플 리포지토리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="08440-140">이전 처럼 hello에서 코드 다음 대체 hello `<app_name>` 만든 hello 함수 앱의 hello 이름의 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="08440-141">Hello 배포 후 소스 설정, Azure CLI 정보 비슷한 toohello 다음 예제 (읽기 쉽도록 삭제 null 값)을 표시 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="08440-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a><span data-ttu-id="08440-142">테스트 hello 함수</span><span class="sxs-lookup"><span data-stu-id="08440-142">Test hello function</span></span>

<span data-ttu-id="08440-143">에서는 Mac 또는 Linux 컴퓨터 또는 Bash를 이용 하 여 Windows에서 cURL tootest 배포 된 hello 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="08440-144">다음 명령을 cURL hello hello 실행 `<app_name>` 함수 응용 프로그램의 hello 이름의 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="08440-145">쿼리 문자열 hello 추가 `&name=<yourname>` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![브라우저에 표시된 함수 응답.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="08440-147">CURL 명령줄에서 사용할 수 없으면 입력 hello 웹 브라우저의 주소 hello에서에서 같은 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="08440-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="08440-148">다시 hello 대체 `<app_name>` 함수 응용 프로그램의 hello 이름의 자리 표시자 hello 쿼리 문자열에 추가 하 고 `&name=<yourname>` toohello URL hello 요청을 실행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08440-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![브라우저에 표시된 함수 응답.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="08440-150">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="08440-150">Clean up resources</span></span>

<span data-ttu-id="08440-151">이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="08440-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="08440-152">후속 퀵 스타트 또는 hello 자습서 toowork toocontinue 하려는 경우이 빠른 시작에서 만든 hello 리소스를 정리할 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="08440-153">Toocontinue 않으려는 경우 다음 명령을 toodelete hello이 빠른이 시작에서 생성 된 모든 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="08440-154">메시지가 표시되면 `y`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="08440-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08440-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08440-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
