---
title: "Node.js를 사용하여 Azure Cosmos DB에 MongoDB 앱 연결 | Microsoft Docs"
description: "Azure Cosmos DB에 기존 Node.js MongoDB 앱을 연결하는 자세한 방법"
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
ms.openlocfilehash: a26477d692cc98ed16c195233ade5434cc536a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="ddca8-103">Azure Cosmos DB: 기존 Node.js MongoDB 웹앱 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="ddca8-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="ddca8-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ddca8-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ddca8-106">이 빠른 시작은 Node.js로 작성된 기존의 [MongoDB](mongodb-introduction.md) 앱을 사용하는 방법을 보여주고 MongoDB 클라이언트 연결을 지원하는 Azure Cosmos DB 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-106">This quickstart demonstrates how to use an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="ddca8-107">즉, Node.js 응용 프로그램은 MongoDB API를 사용하여 데이터베이스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-107">In other words, your Node.js application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="ddca8-108">Azure Cosmos DB에 데이터가 저장되는 응용 프로그램에 대해 투명합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="ddca8-109">완료하고 나면 MEAN 응용 프로그램(MongoDB, Express, AngularJS 및 Node.js)이 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Azure App Service에서 실행 중인 MEAN.js 응용 프로그램](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ddca8-111">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-111">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ddca8-112">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="ddca8-113">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddca8-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ddca8-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ddca8-114">Prerequisites</span></span> 
<span data-ttu-id="ddca8-115">Azure CLI 외에도 `npm` 및 `git` 명령을 실행하려면 [Node.js](https://nodejs.org/) 및 [Git](http://www.git-scm.com/downloads)가 로컬로 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-115">In addition to Azure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally to run `npm` and `git` commands.</span></span>

<span data-ttu-id="ddca8-116">Node.js에 대한 실무 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="ddca8-117">이 빠른 시작은 일반적으로 Node.js 응용 프로그램을 개발하는 데 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-117">This quickstart is not intended to help you with developing Node.js applications in general.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="ddca8-118">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="ddca8-118">Clone the sample application</span></span>

<span data-ttu-id="ddca8-119">git bash와 같은 git 터미널 창을 열고 `cd`를 수행하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

<span data-ttu-id="ddca8-120">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-120">Run the following commands to clone the sample repository.</span></span> <span data-ttu-id="ddca8-121">이 샘플 리포지토리에는 기본 [MEAN.js](http://meanjs.org/) 응용 프로그램이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-121">This sample repository contains the default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-the-application"></a><span data-ttu-id="ddca8-122">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="ddca8-122">Run the application</span></span>

<span data-ttu-id="ddca8-123">필요한 패키지를 설치하고 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-123">Install the required packages and start the application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-to-azure"></a><span data-ttu-id="ddca8-124">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="ddca8-124">Log in to Azure</span></span>

<span data-ttu-id="ddca8-125">설치된 Azure CLI를 사용하는 경우 [az login](/cli/azure/#login) 명령을 사용하여 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-125">If you are using an installed Azure CLI, log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="ddca8-126">Azure Cloud Shell을 사용하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-126">You can skip this step if you're using the Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-the-azure-cosmos-db-module"></a><span data-ttu-id="ddca8-127">Azure Cosmos DB 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="ddca8-127">Add the Azure Cosmos DB module</span></span>

<span data-ttu-id="ddca8-128">설치된 Azure CLI를 사용하는 경우 `az` 명령을 실행하여 `cosmosdb` 구성 요소가 이미 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-128">If you are using an installed Azure CLI, check to see if the `cosmosdb` component is already installed by running the `az` command.</span></span> <span data-ttu-id="ddca8-129">기본 명령 목록에 `cosmosdb`가 있으면 다음 명령으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-129">If `cosmosdb` is in the list of base commands, proceed to the next command.</span></span> <span data-ttu-id="ddca8-130">Azure Cloud Shell을 사용하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-130">You can skip this step if you're using the Azure Cloud Shell.</span></span>

<span data-ttu-id="ddca8-131">`cosmosdb`가 기본 명령 목록에 없으면 [Azure CLI 2.0]( /cli/azure/install-azure-cli)을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-131">If `cosmosdb` is not in the list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ddca8-132">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ddca8-132">Create a resource group</span></span>

<span data-ttu-id="ddca8-133">[az group create](/cli/azure/group#create)를 사용하여 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ddca8-134">Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정이 관리되었는지 등 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="ddca8-135">다음 예제에서는 유럽 서부 지역의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-135">The following example creates a resource group in the West Europe region.</span></span> <span data-ttu-id="ddca8-136">리소스 그룹에 고유한 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-136">Choose a unique name for the resource group.</span></span>

<span data-ttu-id="ddca8-137">Azure Cloud Shell을 사용하는 경우 **시도**를 클릭하고, 화면의 지시에 따라 로그인한 다음, 명령 프롬프트에 명령을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-137">If you are using Azure Cloud Shell, click **Try It**, follow the onscreen prompts to login, then copy the command into the command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="ddca8-138">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ddca8-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="ddca8-139">[az cosmosdb create](/cli/azure/cosmosdb#create) 명령을 사용하여 Azure Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-139">Create an Azure Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="ddca8-140">다음 명령에서 `<cosmosdb-name>` 자리 표시자를 표시하는 고유한 Azure Cosmos DB 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-140">In the following command, please substitute your own unique Azure Cosmos DB account name where you see the `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="ddca8-141">이 고유한 이름은 Azure Cosmos DB 끝점의 일부(`https://<cosmosdb-name>.documents.azure.com/`)로 사용되므로, Azure의 모든 Azure Cosmos DB 계정에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so the name needs to be unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="ddca8-142">`--kind MongoDB` 매개 변수는 MongoDB 클라이언트 연결을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-142">The `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="ddca8-143">Azure Cosmos DB 계정을 만든 경우 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-143">When the Azure Cosmos DB account is created, the Azure CLI shows information similar to the following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="ddca8-144">이 예서는 Azure CLI 출력 형식으로 JSON을 사용합니다(기본값).</span><span class="sxs-lookup"><span data-stu-id="ddca8-144">This example uses JSON as the Azure CLI output format, which is the default.</span></span> <span data-ttu-id="ddca8-145">다른 출력 형식을 사용하려면 [Azure CLI 2.0 명령에 대한 출력 형식](https://docs.microsoft.com/cli/azure/format-output-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddca8-145">To use another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

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

## <a name="connect-your-nodejs-application-to-the-database"></a><span data-ttu-id="ddca8-146">데이터베이스에 Node.js 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="ddca8-146">Connect your Node.js application to the database</span></span>

<span data-ttu-id="ddca8-147">이 단계에서는 MongoDB 연결 문자열을 사용하여 MEAN.js 샘플 응용 프로그램을 방금 만든 Azure Cosmos DB 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-147">In this step, you connect your MEAN.js sample application to an Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="ddca8-148">Node.js 응용 프로그램에 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="ddca8-148">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="ddca8-149">MEAN.js 리포지토리에서 `config/env/local-development.js`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="ddca8-150">이 파일 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-150">Replace the content of this file with the following code.</span></span> <span data-ttu-id="ddca8-151">또한 두 개의 `<cosmosdb-name>` 자리 표시자를 Azure Cosmos DB 계정 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-151">Be sure to also replace the two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-the-key"></a><span data-ttu-id="ddca8-152">키 검색</span><span class="sxs-lookup"><span data-stu-id="ddca8-152">Retrieve the key</span></span>

<span data-ttu-id="ddca8-153">Azure Cosmos DB 데이터베이스에 연결하기 위해 데이터베이스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-153">In order to connect to an Azure Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="ddca8-154">[az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) 명령을 사용하여 기본 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-154">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="ddca8-155">Azure CLI는 다음 예와 유사한 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-155">The Azure CLI outputs information similar to the following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="ddca8-156">`primaryMasterKey`의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-156">Copy the value of `primaryMasterKey`.</span></span> <span data-ttu-id="ddca8-157">`local-development.js`에 있는 `<primary_master_key>`에 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-157">Paste this over the  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="ddca8-158">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-158">Save your changes.</span></span>

### <a name="run-the-application-again"></a><span data-ttu-id="ddca8-159">응용 프로그램을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-159">Run the application again.</span></span>

<span data-ttu-id="ddca8-160">`npm start`을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="ddca8-161">이제 콘솔 메시지에서는 개발 환경이 실행된다고 알려 주어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-161">A console message should now tell you that the development environment is up and running.</span></span> 

<span data-ttu-id="ddca8-162">브라우저에서 `http://localhost:3000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-162">Navigate to `http://localhost:3000` in a browser.</span></span> <span data-ttu-id="ddca8-163">맨 위 메뉴에서 **등록**을 클릭하여 두 개의 더미 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-163">Click **Sign Up** in the top menu and try to create two dummy users.</span></span> 

<span data-ttu-id="ddca8-164">MEAN.js 샘플 응용 프로그램은 데이터베이스에 사용자 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-164">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="ddca8-165">성공해서 MEAN.js가 생성된 사용자로 자동 로그인하면 Azure Cosmos DB 연결이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-165">If you are successful and MEAN.js automatically signs into the created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js가 MongoDB 연결에 성공](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="ddca8-167">데이터 탐색기에서 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="ddca8-167">View data in Data Explorer</span></span>

<span data-ttu-id="ddca8-168">Azure Cosmos DB에서 저장된 데이터는 Azure Portal에서 비즈니스 논리 보기, 쿼리 및 실행에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-168">Data stored by an Azure Cosmos DB is available to view, query, and run business-logic on in the Azure portal.</span></span>

<span data-ttu-id="ddca8-169">이전 단계에서 만든 사용자 데이터를 보고 쿼리하고 사용하려면 웹 브라우저에서 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-169">To view, query, and work with the user data created in the previous step, login to the [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="ddca8-170">맨 위에 있는 Search 상자에서 Azure Cosmos DB를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-170">In the top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="ddca8-171">Cosmos DB 계정 블레이드가 열리면 Cosmos DB 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="ddca8-172">왼쪽 탐색에서 데이터 탐색기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-172">In the left navigation, click Data Explorer.</span></span> <span data-ttu-id="ddca8-173">컬렉션 창에서 컬렉션을 확장하면 컬렉션에서 문서를 보고, 데이터를 쿼리하고 저장된 프로시저, 트리거 및 UDF를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-173">Expand your collection in the Collections pane, and then you can view the documents in the collection, query the data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Azure Portal의 데이터 탐색기](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-the-nodejs-application-to-azure"></a><span data-ttu-id="ddca8-175">Azure에 Node.js 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="ddca8-175">Deploy the Node.js application to Azure</span></span>

<span data-ttu-id="ddca8-176">이 단계에서는 MongoDB에 연결된 Node.js 응용 프로그램을 Azure Cosmos DB에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-176">In this step, you deploy your MongoDB-connected Node.js application to Azure Cosmos DB.</span></span>

<span data-ttu-id="ddca8-177">개발 환경을 위해 이전에 변경한 구성 파일을 알 수 있습니다(`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="ddca8-177">You may have noticed that the configuration file that you changed earlier is for the development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="ddca8-178">응용 프로그램을 App Service에 배포하면 기본적으로 프로덕션 환경에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-178">When you deploy your application to App Service, it will run in the production environment by default.</span></span> <span data-ttu-id="ddca8-179">이제 해당 구성 파일을 동일하게 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-179">So now, you need to make the same change to the respective configuration file.</span></span>

<span data-ttu-id="ddca8-180">MEAN.js 리포지토리에서 `config/env/production.js`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="ddca8-181">`db` 개체에서 다음 예에 표시된 것과 같이 `uri` 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-181">In the `db` object, replace the value of `uri` as show in the following example.</span></span> <span data-ttu-id="ddca8-182">전과 같이 자리 표시자를 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-182">Be sure to replace the placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="ddca8-183">`ssl=true` 옵션은 [Azure Cosmos DB에서 SSL이 필요](connect-mongodb-account.md#connection-string-requirements)하기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-183">The `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="ddca8-184">터미널에서 Git에 모든 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-184">In the terminal, commit all your changes into Git.</span></span> <span data-ttu-id="ddca8-185">두 명령을 복사하여 함께 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-185">You can copy both commands to run them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="ddca8-186">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="ddca8-186">Clean up resources</span></span>

<span data-ttu-id="ddca8-187">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-187">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="ddca8-188">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-188">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="ddca8-189">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-189">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddca8-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddca8-190">Next steps</span></span>

<span data-ttu-id="ddca8-191">이 빠른 시작에서, Azure Cosmos DB 계정을 만들고, 데이터 탐색기를 사용하여 MongoDB 컬렉션을 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-191">In this quickstart, you've learned how to create an Azure Cosmos DB account and create a MongoDB collection using the Data Explorer.</span></span> <span data-ttu-id="ddca8-192">이제 Azure Cosmos DB에 MongoDB 데이터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddca8-192">You can now migrate your MongoDB data to Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="ddca8-193">Azure Cosmos DB로 MongoDB 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddca8-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
