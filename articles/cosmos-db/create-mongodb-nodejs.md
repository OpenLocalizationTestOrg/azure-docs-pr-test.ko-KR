---
title: "Node.js를 사용 하 여 MongoDB 앱 tooAzure Cosmos DB aaaConnect | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect 기존 Node.js MongoDB 앱 tooAzure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="50634-103">Azure Cosmos DB: 기존 Node.js MongoDB 웹앱 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="50634-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="50634-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="50634-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="50634-106">이 빠른 시작에서는 방법을 기존 toouse [MongoDB](mongodb-introduction.md) Node.js로 작성 된 응용 MongoDB 클라이언트 연결을 지 원하는 tooyour Azure Cosmos DB 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="50634-107">즉, Node.js 응용 프로그램 연결 하는 MongoDB Api를 사용 하 여 tooa 데이터베이스만 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="50634-108">투명 데이터 hello toohello 응용 Azure Cosmos DB에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50634-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="50634-109">완료하고 나면 MEAN 응용 프로그램(MongoDB, Express, AngularJS 및 Node.js)이 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="50634-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Azure App Service에서 실행 중인 MEAN.js 응용 프로그램](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="50634-111">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="50634-112">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="50634-113">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="50634-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="50634-114">Prerequisites</span></span> 
<span data-ttu-id="50634-115">또한 CLI tooAzure 필요 [Node.js](https://nodejs.org/) 및 [Git](http://www.git-scm.com/downloads) toorun 로컬로 설치 `npm` 및 `git` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="50634-116">Node.js에 대한 실무 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="50634-117">이 퀵 스타트의 의도 한 toohelp 일반적 Node.js 응용 프로그램을 개발 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="50634-118">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="50634-118">Clone hello sample application</span></span>

<span data-ttu-id="50634-119">예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="50634-120">다음 명령을 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="50634-121">이 샘플 리포지토리 포함 hello 기본 [MEAN.js](http://meanjs.org/) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="50634-122">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="50634-122">Run hello application</span></span>

<span data-ttu-id="50634-123">Hello 필요한 패키지를 설치 하 고 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="50634-124">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="50634-124">Log in tooAzure</span></span>

<span data-ttu-id="50634-125">Tooyour hello로 Azure 구독에에서는 설치 된 Azure CLI를 사용 하는 경우 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="50634-126">Azure 클라우드 셸 hello를 사용 하 여이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="50634-127">Hello Azure Cosmos DB 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="50634-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="50634-128">설치 된 Azure CLI를 사용 하는 경우 확인 toosee 경우 hello `cosmosdb` hello를 실행 하 여 구성 요소가 이미 설치 되어 `az` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="50634-129">경우 `cosmosdb` 에 기본 명령 목록이 hello, toohello 다음 명령을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="50634-130">Azure 클라우드 셸 hello를 사용 하 여이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="50634-131">경우 `cosmosdb` 기본 명령 목록이 hello를 다시 설치에 없으면 [Azure CLI 2.0]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="50634-132">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="50634-132">Create a resource group</span></span>

<span data-ttu-id="50634-133">만들기는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello로 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="50634-134">Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정이 관리되었는지 등 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="50634-135">hello 다음 예제에서는 리소스 그룹 hello 서 부 유럽 지역에서</span><span class="sxs-lookup"><span data-stu-id="50634-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="50634-136">Hello 리소스 그룹에 대 한 고유한 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="50634-137">Azure 클라우드 셸을 사용 하는 경우 클릭 **시도**를 hello 화면에 나타나는 메시지 toologin에 따라 다음 hello 명령을 hello 명령 프롬프트에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="50634-138">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="50634-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="50634-139">Hello Azure Cosmos DB 계정을 만들고 [az cosmosdb 만들](/cli/azure/cosmosdb#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="50634-140">Hello에 다음 명령을, 하십시오 직접 고유한 Azure Cosmos DB 계정 이름을 대체 hello 나타나는 `<cosmosdb-name>` 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="50634-141">이 고유 이름이 Azure Cosmos DB 끝점의 일부로 사용될지 (`https://<cosmosdb-name>.documents.azure.com/`) hello 이름 해야 toobe 고유 Azure의 모든 Azure Cosmos DB 계정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="50634-142">hello `--kind MongoDB` MongoDB 클라이언트 연결 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="50634-143">Hello Azure Cosmos DB 계정이 만들어지면 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50634-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="50634-144">이 예제에서는 hello 기본 설정인 hello Azure CLI 출력 형식으로 JSON을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="50634-145">다른 출력 toouse, 참조 형식 [출력 Azure CLI 2.0 명령에 대 한 형식](https://docs.microsoft.com/cli/azure/format-output-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="50634-146">Node.js 응용 프로그램 toohello 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="50634-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="50634-147">이 단계에서는 방금 만든 MongoDB 연결 문자열을 사용 하 여 MEAN.js 샘플 응용 프로그램 tooan Azure Cosmos DB 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="50634-148">Node.js 응용 프로그램에서 hello 연결 문자열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="50634-149">MEAN.js 리포지토리에서 `config/env/local-development.js`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50634-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="50634-150">이 파일의 내용을 hello 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="50634-151">Tooalso hello 2를 대체 해야 `<cosmosdb-name>` Azure Cosmos DB 계정 이름의 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="50634-152">Hello 키 검색</span><span class="sxs-lookup"><span data-stu-id="50634-152">Retrieve hello key</span></span>

<span data-ttu-id="50634-153">주문 tooconnect tooan Azure Cosmos DB 데이터베이스 hello 데이터베이스 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="50634-154">사용 하 여 hello [키 나열 az cosmosdb](/cli/azure/cosmosdb#list-keys) 명령 tooretrieve hello에 대 한 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="50634-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="50634-155">hello Azure CLI 정보 비슷한 toohello 다음 예제를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="50634-156">hello 값을 복사 `primaryMasterKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="50634-157">Hello이 붙여 `<primary_master_key>` 에서 `local-development.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="50634-158">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="50634-159">Hello 응용 프로그램을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-159">Run hello application again.</span></span>

<span data-ttu-id="50634-160">`npm start`을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="50634-161">콘솔 메시지 이제 알려 주어 야 해당 hello 개발 환경에서 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="50634-162">너무 이동`http://localhost:3000` 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="50634-163">클릭 **등록** hello 최상위 메뉴와 시도 toocreate에 사용자가 더미 두 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="50634-164">hello MEAN.js 샘플 응용 프로그램 hello 데이터베이스에 사용자 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="50634-165">성공한 MEAN.js에 자동으로 로그인 할 hello 사용자를 만든 경우 Azure Cosmos DB 연결이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js tooMongoDB 성공적으로 연결](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="50634-167">데이터 탐색기에서 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="50634-167">View data in Data Explorer</span></span>

<span data-ttu-id="50634-168">Azure Cosmos DB에서 저장 된 데이터를 사용할 수 있는 tooview, 쿼리 및 비즈니스 논리 실행된에서 켜져 hello Azure 포털.</span><span class="sxs-lookup"><span data-stu-id="50634-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="50634-169">tooview, 쿼리 및 로그인 toohello hello 이전 단계에서 만든 hello 사용자 데이터로 작업 [Azure 포털](https://portal.azure.com) 웹 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="50634-170">Hello 최상위 검색 상자에 Azure Cosmos DB를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="50634-171">Cosmos DB 계정 블레이드가 열리면 Cosmos DB 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="50634-172">왼쪽 탐색 hello, 데이터 탐색기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="50634-173">Hello 모음 창에서 컬렉션을 확장 한 다음 수 hello 컬렉션, 쿼리 hello 데이터의에서 hello 문서를 표시 하 고도 만들고 저장된 프로시저, 트리거 및 Udf를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Hello Azure 포털에서에서 데이터 탐색기](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="50634-175">Hello Node.js 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="50634-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="50634-176">이 단계에서는 Node.js MongoDB에 연결 된 응용 프로그램 tooAzure Cosmos DB 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="50634-177">Hello 개발 환경에 대 한 이전 변경 된 hello 구성 파일은 단어로 (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="50634-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="50634-178">사용자 응용 프로그램 tooApp 서비스를 배포 하면 기본적으로 hello 프로덕션 환경에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50634-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="50634-179">이제 toomake hello 필요한 동일 toohello 각 구성 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="50634-180">MEAN.js 리포지토리에서 `config/env/production.js`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50634-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="50634-181">Hello에 `db` 개체, hello 값의 대체 `uri` 같이 다음 예에서는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="50634-182">있는지 tooreplace hello 자리 표시자로 전에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="50634-183">hello `ssl=true` 옵션은 중요 하기 때문에 [Azure Cosmos DB에 SSL이 필요한](connect-mongodb-account.md#connection-string-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="50634-184">Hello 터미널, Git에 모든 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="50634-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="50634-185">두 명령 toorun 복사할 수는 있지만 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="50634-186">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="50634-186">Clean up resources</span></span>

<span data-ttu-id="50634-187">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="50634-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="50634-188">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="50634-189">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="50634-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50634-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50634-190">Next steps</span></span>

<span data-ttu-id="50634-191">이 빠른 시작에서 배운 어떻게 toocreate Azure Cosmos DB 계정 및 hello 데이터 탐색기를 사용 하 여 MongoDB 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50634-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="50634-192">이제 MongoDB 데이터 tooAzure Cosmos DB를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50634-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="50634-193">Azure Cosmos DB로 MongoDB 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="50634-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
