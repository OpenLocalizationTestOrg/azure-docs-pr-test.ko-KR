---
title: "Azure에서 Node.js 및 MongoDB 웹앱 작성 | Microsoft Docs"
description: "Azure에서 작동하며 MongoDB 연결 문자열로 Cosmos 데이터베이스에 연결되는 Node.js 응용 프로그램을 만드는 방법을 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="00bbc-103">Azure에서 Node.js 및 MongoDB 웹앱 작성</span><span class="sxs-lookup"><span data-stu-id="00bbc-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="00bbc-104">Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="00bbc-105">이 자습서에서는 Azure에서 Node.js 웹앱을 만들고 MongoDB 데이터베이스에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="00bbc-106">완료되면 MEAN 응용 프로그램(MongoDB, Express, AngularJS 및 Node.js)이 [Azure App Service](app-service-web-overview.md)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="00bbc-107">간편하게 하기 위해 샘플 응용 프로그램은 [MEAN.js 웹 프레임워크](http://meanjs.org/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![Azure App Service에서 실행 중인 MEAN.js 응용 프로그램](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="00bbc-109">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="00bbc-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00bbc-110">Azure에서 MongoDB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="00bbc-111">Node.js 앱을 MongoDB에 연결</span><span class="sxs-lookup"><span data-stu-id="00bbc-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="00bbc-112">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="00bbc-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="00bbc-113">데이터 모델 업데이트 및 앱 다시 배포</span><span class="sxs-lookup"><span data-stu-id="00bbc-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="00bbc-114">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="00bbc-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="00bbc-115">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="00bbc-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00bbc-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00bbc-116">Prerequisites</span></span>

<span data-ttu-id="00bbc-117">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="00bbc-118">Git 설치</span><span class="sxs-lookup"><span data-stu-id="00bbc-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="00bbc-119">Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="00bbc-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="00bbc-120">[Gulp.js 설치](http://gulpjs.com/)([MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started)에 필요)</span><span class="sxs-lookup"><span data-stu-id="00bbc-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="00bbc-121">MongoDB Community Edition 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="00bbc-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="00bbc-122">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="00bbc-123">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="00bbc-124">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00bbc-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="00bbc-125">로컬 MongoDB 테스트</span><span class="sxs-lookup"><span data-stu-id="00bbc-125">Test local MongoDB</span></span>

<span data-ttu-id="00bbc-126">터미널 창을 열고 `cd`를 사용하여 MongoDB 설치 위치의 `bin` 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="00bbc-127">이 터미널 창을 사용하여 이 자습서의 모든 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="00bbc-128">터미널에서 `mongo`를 실행하여 로컬 MongoDB 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="00bbc-129">연결이 성공한다면 MongoDB 데이터베이스가 이미 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="00bbc-130">그렇지 않으면 [MongoDB Community Edition 설치](https://docs.mongodb.com/manual/administration/install-community/)의 단계에 따라 로컬 MongoDB 데이터베이스가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="00bbc-131">MongoDB가 주로 설치되어 있지만 `mongod`를 실행하여 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="00bbc-132">MongoDB 데이터베이스를 테스트했으면 터미널에서 `Ctrl+C`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="00bbc-133">로컬 Node.js 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-133">Create local Node.js app</span></span>

<span data-ttu-id="00bbc-134">이 단계에서는 로컬 Node.js 프로젝트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="00bbc-135">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="00bbc-135">Clone the sample application</span></span>

<span data-ttu-id="00bbc-136">터미널 창에서 `cd`를 사용하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="00bbc-137">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="00bbc-138">이 샘플 리포지토리에는 [MEAN.js 리포지토리](https://github.com/meanjs/mean) 복사본이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="00bbc-139">App Service에서 실행하도록 수정되었습니다(자세한 내용은 MEAN.js 리포지토리의 [README(추가 정보) 파일](https://github.com/Azure-Samples/meanjs/blob/master/README.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="00bbc-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="00bbc-140">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="00bbc-140">Run the application</span></span>

<span data-ttu-id="00bbc-141">다음 명령을 실행하여 필요한 패키지를 설치하고 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="00bbc-142">앱이 완전히 로드되면 다음과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-142">When the app is fully loaded, you see something similar to the following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="00bbc-143">브라우저에서 http://localhost:3000 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="00bbc-144">위쪽 메뉴에서 **등록**을 클릭하고 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="00bbc-145">MEAN.js 샘플 응용 프로그램은 데이터베이스에 사용자 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="00bbc-146">사용자 만들기와 로그인에 성공하면 앱에서 로컬 MongoDB 데이터베이스에 데이터를 쓰고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js가 MongoDB 연결에 성공](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="00bbc-148">**관리자 > 문서 관리**를 선택하여 문서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="00bbc-149">언제든지 Node.js를 중지하려면 터미널에서 `Ctrl+C`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="00bbc-150">프로덕션 MongoDB 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-150">Create production MongoDB</span></span>

<span data-ttu-id="00bbc-151">이 단계에서는 Azure에 MongoDB 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="00bbc-152">Azure에 앱을 배포하면 이 클라우드 데이터베이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="00bbc-153">MongoDB의 경우 이 자습서에서는 [Azure Cosmos DB](/azure/documentdb/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="00bbc-154">Cosmos DB는 MongoDB 클라이언트 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="00bbc-155">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="00bbc-155">Log in to Azure</span></span>

<span data-ttu-id="00bbc-156">Azure CLI 2.0을 사용하여 Azure에서 앱을 호스팅하는 데 필요한 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="00bbc-157">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="00bbc-158">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-158">Create a resource group</span></span>

<span data-ttu-id="00bbc-159">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="00bbc-160">다음 예제에서는 유럽 서부 지역의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="00bbc-161">[az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI 명령을 사용하여 사용할 수 있는 위치를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="00bbc-162">Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="00bbc-163">[az cosmosdb create](/cli/azure/cosmosdb#create) 명령을 사용하여 Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="00bbc-164">다음 명령에서 *\<cosmosdb_name>* 자리 표시자를 대신하여 고유한 Cosmos DB 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="00bbc-165">이 이름은 Cosmos DB 끝점(`https://<cosmosdb_name>.documents.azure.com/`)의 일부로 사용되므로 Azure의 모든 Cosmos DB 계정에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="00bbc-166">이름은 소문자, 숫자 및 하이픈(-) 문자만 포함할 수 있으며, 3-50자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="00bbc-167">*--kind MongoDB* 매개 변수는 MongoDB 클라이언트 연결을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="00bbc-168">Cosmos DB 계정을 만든 경우 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="00bbc-169">프로덕션 MongoDB에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="00bbc-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="00bbc-170">이 단계에서는 MongoDB 연결 문자열을 사용하여 MEAN.js 샘플 응용 프로그램을 방금 만든 Cosmos DB 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="00bbc-171">데이터베이스 키 검색</span><span class="sxs-lookup"><span data-stu-id="00bbc-171">Retrieve the database key</span></span>

<span data-ttu-id="00bbc-172">Cosmos DB 데이터베이스에 연결하려면 데이터베이스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="00bbc-173">[az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) 명령을 사용하여 기본 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="00bbc-174">Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

`primaryMasterKey`의 값을 복사합니다. <span data-ttu-id="00bbc-176">이 정보는 다음 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="00bbc-177">Node.js 응용 프로그램에 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="00bbc-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="00bbc-178">MEAN.js 리포지토리에서 _config/env/production.js_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="00bbc-179">`db` 개체에서 `uri`의 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="00bbc-180">두 개의 *\<cosmosdb_name>* 자리 표시자를 Cosmos DB 데이터베이스 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="00bbc-181">*\<primary_master_key>* 자리 표시자를 이전 단계에서 복사한 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="00bbc-182">다음은 `db` 개체를 보여 주는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="00bbc-183">[Cosmos DB에서 SSL을 요구](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)하므로 `ssl=true` 옵션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="00bbc-184">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="00bbc-185">프로덕션 모드에서 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="00bbc-185">Test the application in production mode</span></span> 

<span data-ttu-id="00bbc-186">다음 명령을 실행하여 프로덕션 환경에 대한 스크립트를 축소하고 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="00bbc-187">이 프로세스는 프로덕션 환경에 필요한 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="00bbc-188">다음 명령을 실행하여 _config/env/production.js_에서 구성한 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="00bbc-189">`NODE_ENV=production`은 프로덕션 환경에서 실행되도록 Node.js에 지시하는 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="00bbc-190">`node server.js`는 리포지토리 루트의 `server.js`로 Node.js 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="00bbc-191">이 방법으로 Node.js 응용 프로그램을 Azure에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="00bbc-192">앱이 로드되면 프로덕션 환경에서 실행 중인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="00bbc-193">브라우저에서 http://localhost:8443 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="00bbc-194">위쪽 메뉴에서 **등록**을 클릭하고 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="00bbc-195">사용자 만들기와 로그인에 성공하면 앱에서 Azure의 Cosmos DB 데이터베이스에 데이터를 쓰고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="00bbc-196">터미널에서 `Ctrl+C`를 입력하여 Node.js를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="00bbc-197">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="00bbc-197">Deploy app to Azure</span></span>

<span data-ttu-id="00bbc-198">이 단계에서는 MongoDB에 연결된 Node.js 응용 프로그램을 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="00bbc-199">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-199">Create an App Service plan</span></span>

<span data-ttu-id="00bbc-200">[az appservice plan create](/cli/azure/appservice/plan#create) 명령으로 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="00bbc-201">다음 예제에서는 **무료** 가격 책정 계층을 사용하여 _myAppServicePlan_이라는 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="00bbc-202">App Service 계획을 만들면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="00bbc-203">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-203">Create a web app</span></span>

<span data-ttu-id="00bbc-204">[az webapp create](/cli/azure/webapp#create) 명령을 사용하여 `myAppServicePlan` App Service 계획에 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="00bbc-205">웹앱은 코드를 배포할 호스팅 공간을 제공하고, 배포된 응용 프로그램을 확인할 수 있도록 URL도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="00bbc-206">웹앱을 만드는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-206">Use  to create the web app.</span></span> 

<span data-ttu-id="00bbc-207">다음 명령에서 *\<app_name>* 자리 표시자를 고유한 앱 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="00bbc-208">이 이름은 웹앱에 대한 URL의 일부로 사용되므로 Azure App Service의 모든 앱에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="00bbc-209">웹앱을 만들었으면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="00bbc-210">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="00bbc-210">Configure an environment variable</span></span>

<span data-ttu-id="00bbc-211">자습서의 앞부분에서는 _config/env/production.js_에 데이터베이스 연결 문자열을 하드코딩했습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="00bbc-212">최상의 보안을 유지하려면 이 중요한 데이터를 Git 리포지토리 외부에 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="00bbc-213">Azure에서 실행되는 응용 프로그램의 경우는 대신 환경 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="00bbc-214">App Service에서 [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) 명령을 사용하여 환경 변수를 _앱 설정_으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="00bbc-215">다음 예제에서는 Azure 웹앱에 `MONGODB_URI` 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="00bbc-216">*\<app_name>*, *\<cosmosdb_name>* 및 *\<primary_master_key>* 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="00bbc-217">Node.js 코드에서는 다른 환경 변수에 액세스할 때와 마찬가지로 `process.env.MONGODB_URI`를 사용하여 이 응용 프로그램 설정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="00bbc-218">이제 다음 명령을 사용하여 _config/env/production.js_의 변경 내용을 실행 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="00bbc-219">_config/env/production.js_를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="00bbc-220">기본 MEAN.js 앱은 만든 `MONGODB_URI` 환경 변수를 사용하도록 이미 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="00bbc-221">로컬 Git 배포 구성</span><span class="sxs-lookup"><span data-stu-id="00bbc-221">Configure local git deployment</span></span> 

<span data-ttu-id="00bbc-222">[az webapp deployment user set](/cli/azure/webapp/deployment/user#set) 명령을 사용하여 배포에 대한 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="00bbc-223">FTP, 로컬 Git, GitHub, Visual Studio Team Services 및 BitBucket과 같은 다양한 방법으로 응용 프로그램을 Azure App Service에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="00bbc-224">FTP 및 로컬 Git의 경우 배포에 인증하기 위해 배포 사용자를 서버에 구성할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="00bbc-225">이 배포 사용자는 계정 수준이며 Azure 구독 계정과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="00bbc-226">이 배포 사용자는 한 번만 구성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="00bbc-227">다음 명령에서 *\<사용자 이름>* 및 *\<암호>*를 새 사용자 이름 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="00bbc-228">사용자 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-228">The user name must be unique.</span></span> <span data-ttu-id="00bbc-229">암호는 글자, 숫자, 기호와 같은 세 가지 요소 중 두 가지를 포함하여 8자 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="00bbc-230">` 'Conflict'. Details: 409` 오류가 발생하면 사용자 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="00bbc-231">` 'Bad Request'. Details: 400` 오류가 발생하면 더 강력한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="00bbc-232">앱을 배포할 때 이후 단계에서 사용할 사용자 이름과 암호를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="00bbc-233">[az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) 명령을 사용하여 Azure 웹앱에 대한 로컬 Git 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="00bbc-234">배포 사용자가 구성되면 Azure CLI에 다음과 같은 형식으로 Azure 웹앱의 배포 URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="00bbc-235">다음 단계에서 사용되므로 터미널의 출력을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="00bbc-236">Git에서 Azure에 푸시</span><span class="sxs-lookup"><span data-stu-id="00bbc-236">Push to Azure from Git</span></span>

<span data-ttu-id="00bbc-237">로컬 Git 리포지토리에 Azure 원격을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="00bbc-238">Azure에 원격으로 푸시하여 Node.js 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="00bbc-239">배포 사용자를 만드는 작업의 일부로 이전에 입력한 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="00bbc-240">배포하는 동안 Azure App Service는 진행 상황을 Git에 전합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="00bbc-241">배포 프로세스에서 `npm install` 후에 [Gulp](http://gulpjs.com/)를 실행하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="00bbc-242">App Service는 배포 중에 Gulp 또는 Grunt 작업을 실행하지 않으므로 이 샘플 리포지토리는 사용 설정에 사용되는 추가 파일 두 개가 루트 디렉터리에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="00bbc-243">_.deployment_ - 이 파일은 App Service에서 `bash deploy.sh`를 사용자 지정 배포 스크립트로 실행하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="00bbc-244">_deploy.sh_ - 사용자 지정 배포 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="00bbc-245">파일을 검토 하는 경우 실행 되도록 표시 됩니다 `gulp prod` 후 `npm install` 및 `bower install`합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="00bbc-246">이 방식으로 Git 기반 배포에 어떤 단계든 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="00bbc-247">언제든지 Azure Web App을 다시 시작하면 App Service에서 이 자동화 작업을 다시 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="00bbc-248">Azure 웹앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="00bbc-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="00bbc-249">웹 브라우저를 사용하여 배포된 웹앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="00bbc-250">위쪽 메뉴에서 **등록**을 클릭하고 더미 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="00bbc-251">앱에서 성공적으로 만든 사용자로 자동 로그인하면 Azure의 MEAN.js 앱이 MongoDB(Cosmos DB) 데이터베이스에 연결된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![Azure App Service에서 실행 중인 MEAN.js 응용 프로그램](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="00bbc-253">**관리자 > 문서 관리**를 선택하여 문서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="00bbc-254">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="00bbc-254">**Congratulations!**</span></span> <span data-ttu-id="00bbc-255">Azure App Service에서 데이터 기반 Node.js 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="00bbc-256">데이터 모델 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="00bbc-256">Update data model and redeploy</span></span>

<span data-ttu-id="00bbc-257">이 단계에서는 `article` 데이터 모델을 변경하고 변경 내용을 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="00bbc-258">데이터 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="00bbc-258">Update the data model</span></span>

<span data-ttu-id="00bbc-259">_modules/articles/server/models/article.server.model.js_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="00bbc-260">`ArticleSchema`에서 `comment`라는 `String` 형식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="00bbc-261">완료된 후의 스키마 코드는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-the-articles-code"></a><span data-ttu-id="00bbc-262">문서 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="00bbc-262">Update the articles code</span></span>

<span data-ttu-id="00bbc-263">`comment`를 사용하도록 `articles` 코드의 나머지 부분을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="00bbc-264">수정해야 하는 5개의 파일, 즉 서버 컨트롤러 하나와 클라이언트 보기 네 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="00bbc-265">_modules/articles/server/controllers/articles.server.controller.js_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="00bbc-266">`update` 함수에 `article.comment`의 할당을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="00bbc-267">다음 코드에서는 완성된 `update` 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="00bbc-268">_modules/articles/client/views/view-article.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="00bbc-269">닫는 `</section>` 태그 바로 위에 다음 줄을 추가하여 `comment`를 나머지 문서 데이터와 함께 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="00bbc-270">_modules/articles/client/views/list-articles.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="00bbc-271">닫는 `</a>` 태그 바로 위에 다음 줄을 추가하여 `comment`를 나머지 문서 데이터와 함께 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="00bbc-272">_modules/articles/client/views/admin/list-articles.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="00bbc-273">`<div class="list-group">` 요소 안과 닫는 `</a>` 태그 바로 위에 다음 줄을 추가하여 나머지 문서 데이터와 함께 `comment`를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="00bbc-274">_modules/articles/client/views/admin/form-article.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="00bbc-275">다음과 같이 제출 단추가 포함된 `<div class="form-group">` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="00bbc-276">이 태그 바로 위에 사람들이 `comment` 필드를 편집할 수 있게 하는 또 다른 `<div class="form-group">` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="00bbc-277">새 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="00bbc-278">변경 내용을 로컬에서 테스트</span><span class="sxs-lookup"><span data-stu-id="00bbc-278">Test your changes locally</span></span>

<span data-ttu-id="00bbc-279">변경 내용을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-279">Save all your changes.</span></span>

<span data-ttu-id="00bbc-280">프로덕션 모드에서 변경 내용을 다시 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="00bbc-281">_config/env/production.js_이 원래대로 돌아갔으며 `MONGODB_URI` 환경 변수는 로컬 컴퓨터가 아닌 Azure 웹앱에만 설정되어 있다는 점에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="00bbc-282">구성 파일을 살펴보면 프로덕션 구성에서 기본적으로 로컬 MongoDB 데이터베이스를 사용하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="00bbc-283">이렇게 하면 로컬에서 코드 변경 내용을 테스트할 때 프로덕션 데이터를 건드리지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="00bbc-284">브라우저에서 `http://localhost:8443`으로 이동하여 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="00bbc-285">**관리자 > 문서 관리**를 선택한 다음 **+** 단추를 선택하여 문서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="00bbc-286">이제 새로운 `Comment` 텍스트 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-286">You see the new `Comment` textbox now.</span></span>

![문서에 추가된 주석 필드](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="00bbc-288">터미널에서 `Ctrl+C`를 입력하여 Node.js를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="00bbc-289">변경 내용을 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="00bbc-289">Publish changes to Azure</span></span>

<span data-ttu-id="00bbc-290">Git에서 변경 내용을 커밋한 다음 Azure에 코드 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="00bbc-291">`git push`가 완료되면 Azure 웹앱으로 이동하여 새 기능을 테스트해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Azure에 게시된 모델 및 데이터베이스 변경 내용](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="00bbc-293">이전에 문서를 추가했으면 그 문서를 지금도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="00bbc-294">Cosmos DB의 기존 데이터는 손실되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="00bbc-295">또한 데이터 스키마가 업데이트되고 기존 데이터는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="00bbc-296">진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="00bbc-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="00bbc-297">Node.js 응용 프로그램이 Azure App Service에서 실행되는 동안 콘솔 로그를 터미널에 파이프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="00bbc-298">이 방법으로 응용 프로그램 오류를 디버깅하는 데 도움이 되는 진단 메시지를 동일하게 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="00bbc-299">로그 스트리밍을 시작하려면 [az webapp log tail](/cli/azure/webapp/log#tail) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="00bbc-300">로그 스트리밍이 시작되고 나면 브라우저에서 Azure 웹앱을 새로 고쳐 웹 트래픽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="00bbc-301">이제 터미널에 파이프된 콘솔 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="00bbc-302">언제든지 `Ctrl+C`를 입력하여 로그 스트리밍을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="00bbc-303">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="00bbc-303">Manage your Azure web app</span></span>

<span data-ttu-id="00bbc-304">[Azure Portal](https://portal.azure.com)로 이동하여 만든 웹앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="00bbc-305">왼쪽 메뉴에서 **App Services**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="00bbc-307">기본적으로 포털에는 웹앱의 **개요** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="00bbc-308">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="00bbc-309">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="00bbc-310">페이지의 왼쪽에 있는 탭에서는 열 수 있는 여러 구성 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="00bbc-312">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00bbc-312">Next steps</span></span>

<span data-ttu-id="00bbc-313">학습한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00bbc-314">Azure에서 MongoDB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00bbc-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="00bbc-315">Node.js 앱을 MongoDB에 연결</span><span class="sxs-lookup"><span data-stu-id="00bbc-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="00bbc-316">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="00bbc-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="00bbc-317">데이터 모델 업데이트 및 앱 다시 배포</span><span class="sxs-lookup"><span data-stu-id="00bbc-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="00bbc-318">Azure에서 터미널로 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="00bbc-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="00bbc-319">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="00bbc-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="00bbc-320">다음 자습서로 이동하여 사용자 지정 DNS 이름을 웹앱에 매핑하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00bbc-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="00bbc-321">Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="00bbc-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
