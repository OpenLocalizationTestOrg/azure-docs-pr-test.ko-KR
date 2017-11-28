---
title: "Azure의 Node.js 및 MongoDB 웹 앱 aaaBuild | Microsoft Docs"
description: "자세한 내용은 방법 tooget Azure에서 작업 하는 Node.js 응용 프로그램 연결 tooa와 Cosmos DB 데이터베이스 MongoDB 연결 문자열을 사용 합니다."
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
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="3cb63-103">Azure에서 Node.js 및 MongoDB 웹앱 작성</span><span class="sxs-lookup"><span data-stu-id="3cb63-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="3cb63-104">Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="3cb63-105">이 자습서에서는 toocreate는 Node.js Azure에서 응용 프로그램을 구성 하 고 tooa MongoDB 데이터베이스 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="3cb63-106">완료되면 MEAN 응용 프로그램(MongoDB, Express, AngularJS 및 Node.js)이 [Azure App Service](app-service-web-overview.md)에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="3cb63-107">간단한 설명을 위해 hello 예제 응용 프로그램 사용 hello [MEAN.js 웹 프레임 워크](http://meanjs.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Azure App Service에서 실행 중인 MEAN.js 응용 프로그램](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="3cb63-109">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="3cb63-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3cb63-110">Azure에서 MongoDB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="3cb63-111">Node.js 앱 tooMongoDB 연결</span><span class="sxs-lookup"><span data-stu-id="3cb63-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="3cb63-112">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="3cb63-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="3cb63-113">Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="3cb63-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="3cb63-114">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="3cb63-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="3cb63-115">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="3cb63-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cb63-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3cb63-116">Prerequisites</span></span>

<span data-ttu-id="3cb63-117">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="3cb63-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="3cb63-118">Git 설치</span><span class="sxs-lookup"><span data-stu-id="3cb63-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="3cb63-119">Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="3cb63-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="3cb63-120">[Gulp.js 설치](http://gulpjs.com/)([MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started)에 필요)</span><span class="sxs-lookup"><span data-stu-id="3cb63-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="3cb63-121">MongoDB Community Edition 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="3cb63-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3cb63-122">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3cb63-123">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3cb63-124">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="3cb63-125">로컬 MongoDB 테스트</span><span class="sxs-lookup"><span data-stu-id="3cb63-125">Test local MongoDB</span></span>

<span data-ttu-id="3cb63-126">터미널 윈도우를 열고 hello 및 `cd` toohello `bin` MongoDB 설치의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="3cb63-127">이 자습서에서는이 터미널 윈도우 toorun 모든 hello 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="3cb63-128">실행 `mongo` hello 터미널 tooconnect tooyour 로컬 MongoDB 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="3cb63-129">연결이 성공한다면 MongoDB 데이터베이스가 이미 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="3cb63-130">그렇지 않은 경우 로컬 MongoDB 데이터베이스 hello 단계를 수행 하 여 시작 되었는지 확인 [MongoDB Community Edition 설치](https://docs.mongodb.com/manual/administration/install-community/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="3cb63-131">MongoDB가 설치 되어 아니지만, 종종 toostart 여전히 필요 하면 실행 하 여 `mongod`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="3cb63-132">완료 하면 입력 MongoDB 데이터베이스 테스트 `Ctrl+C` hello 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="3cb63-133">로컬 Node.js 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-133">Create local Node.js app</span></span>

<span data-ttu-id="3cb63-134">이 단계에서는 hello 로컬 Node.js 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="3cb63-135">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="3cb63-135">Clone hello sample application</span></span>

<span data-ttu-id="3cb63-136">Hello 터미널 창에서 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="3cb63-137">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="3cb63-138">이 샘플 리포지토리 hello의 복사본이 포함 [MEAN.js 리포지토리](https://github.com/meanjs/mean)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="3cb63-139">앱 서비스에서 수정 된 toorun는 (자세한 내용은 참조 hello MEAN.js 리포지토리 [추가 정보 파일](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="3cb63-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="3cb63-140">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3cb63-140">Run hello application</span></span>

<span data-ttu-id="3cb63-141">Hello 다음 명령을 tooinstall hello 필요한 패키지를 실행 하 고 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="3cb63-142">Hello 앱은 완전히 로드, 메시지의 뒤에, 다음과 유사한 toohello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="3cb63-143">브라우저에서 toohttp://localhost:3000을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="3cb63-144">클릭 **등록** 에 최상위 메뉴 hello 및 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="3cb63-145">hello MEAN.js 샘플 응용 프로그램 hello 데이터베이스에 사용자 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="3cb63-146">사용자를 만들고 로그인에 성공 하면 앱은 데이터 toohello 로컬 MongoDB 데이터베이스를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js tooMongoDB 성공적으로 연결](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="3cb63-148">선택 **관리 > 관리 문서** tooadd 일부 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="3cb63-149">키를 눌러 언제 든 지 Node.js toostop `Ctrl+C` hello 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="3cb63-150">프로덕션 MongoDB 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-150">Create production MongoDB</span></span>

<span data-ttu-id="3cb63-151">이 단계에서는 Azure에 MongoDB 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="3cb63-152">앱 배포 tooAzure 이면이 클라우드 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="3cb63-153">MongoDB의 경우 이 자습서에서는 [Azure Cosmos DB](/azure/documentdb/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="3cb63-154">Cosmos DB는 MongoDB 클라이언트 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="3cb63-155">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="3cb63-155">Log in tooAzure</span></span>

<span data-ttu-id="3cb63-156">Azure에서 응용 프로그램 hello Azure CLI 2.0 toocreate hello 필요한 리소스 toohost를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="3cb63-157">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="3cb63-158">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-158">Create a resource group</span></span>

<span data-ttu-id="3cb63-159">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="3cb63-160">hello 다음 예제에서는 리소스 그룹 hello 서 부 유럽 지역에서</span><span class="sxs-lookup"><span data-stu-id="3cb63-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="3cb63-161">사용 하 여 hello [위치 나열 az appservice](/cli/azure/appservice#list-locations) Azure CLI 명령을 toolist 사용 가능한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="3cb63-162">Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="3cb63-163">Hello Cosmos DB 계정을 만들고 [az cosmosdb 만들](/cli/azure/cosmosdb#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="3cb63-164">Hello hello에 대 한 고유한 Cosmos DB 이름을 대체한 다음 명령을,  *\<cosmosdb_name >* 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="3cb63-165">이 이름은 hello Cosmos DB 끝점의 hello 일부로 사용 됩니다 `https://<cosmosdb_name>.documents.azure.com/`hello 이름 해야 toobe 고유 Azure의 모든 Cosmos DB 계정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="3cb63-166">hello 이름은 소문자, 숫자 및 hello 하이픈 (-) 문자를 포함 해야 하며 3 자에서 50 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="3cb63-167">hello *-kind MongoDB* MongoDB 클라이언트 연결 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="3cb63-168">Hello Cosmos DB 계정이 만들어질 때 hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="3cb63-169">응용 프로그램 tooproduction MongoDB 연결</span><span class="sxs-lookup"><span data-stu-id="3cb63-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="3cb63-170">이 단계에서는 방금 만든 MongoDB 연결 문자열을 사용 하 여 MEAN.js 샘플 응용 프로그램 toohello Cosmos DB 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="3cb63-171">Hello 데이터베이스 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-171">Retrieve hello database key</span></span>

<span data-ttu-id="3cb63-172">tooconnect toohello Cosmos DB 데이터베이스 hello 데이터베이스 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="3cb63-173">사용 하 여 hello [키 나열 az cosmosdb](/cli/azure/cosmosdb#list-keys) 명령 tooretrieve hello에 대 한 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="3cb63-174">hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

hello 값을 복사 `primaryMasterKey`합니다. <span data-ttu-id="3cb63-176">Hello 다음 단계에서이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="3cb63-177">Node.js 응용 프로그램에서 hello 연결 문자열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="3cb63-178">MEAN.js 리포지토리에서 _config/env/production.js_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="3cb63-179">Hello에 `db` 개체 값을 업데이트 hello `uri`:</span><span class="sxs-lookup"><span data-stu-id="3cb63-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="3cb63-180">Hello 두 대체  *\<cosmosdb_name >* Cosmos DB 데이터베이스 이름의 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="3cb63-181">Hello 대체  *\<primary_master_key >* hello 이전 단계에서 복사한 hello 키가 있는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="3cb63-182">hello 다음 코드를 보여 줍니다 hello `db` 개체:</span><span class="sxs-lookup"><span data-stu-id="3cb63-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="3cb63-183">hello `ssl=true` 옵션을 지정 해야 하기 때문에 [Cosmos DB에 SSL이 필요한](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="3cb63-184">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="3cb63-185">프로덕션 모드에서 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="3cb63-185">Test hello application in production mode</span></span> 

<span data-ttu-id="3cb63-186">Hello 다음 hello 프로덕션 환경에 대 한 명령 toominify 및 번들 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="3cb63-187">이 프로세스는 hello 프로덕션 환경에서 필요한 hello 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="3cb63-188">다음 명령은 toouse hello 연결 문자열에 구성 된 실행된 hello _config/env/production.js_합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="3cb63-189">`NODE_ENV=production`hello 프로덕션 환경에서 Node.js toorun에 알리는 hello 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="3cb63-190">`node server.js`시작 Node.js 서버 hello `server.js` 리포지토리 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="3cb63-191">이 방법으로 Node.js 응용 프로그램을 Azure에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="3cb63-192">Hello 응용 프로그램이 로드 되 면 toomake hello 프로덕션 환경에서 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="3cb63-193">브라우저에서 toohttp://localhost:8443을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="3cb63-194">클릭 **등록** 에 최상위 메뉴 hello 및 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="3cb63-195">성공적으로 사용자를 만들고 로그인 인 경우 응용 프로그램 Azure에서 데이터 toohello Cosmos DB 데이터베이스를 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="3cb63-196">Hello 터미널에서 입력 하 여 Node.js 중지 `Ctrl+C`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="3cb63-197">응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="3cb63-197">Deploy app tooAzure</span></span>

<span data-ttu-id="3cb63-198">이 단계에서는 Node.js MongoDB에 연결 된 응용 프로그램 tooAzure 앱 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="3cb63-199">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-199">Create an App Service plan</span></span>

<span data-ttu-id="3cb63-200">Hello로 앱 서비스 계획 만들기 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="3cb63-201">hello 다음 예제에서는 명명 된 앱 서비스 계획 _myAppServicePlan_ hello를 사용 하 여 **무료** 가격 책정 계층:</span><span class="sxs-lookup"><span data-stu-id="3cb63-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="3cb63-202">Hello 앱 서비스 계획을 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="3cb63-203">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-203">Create a web app</span></span>

<span data-ttu-id="3cb63-204">Hello에 웹 앱 만들기 `myAppServicePlan` hello로 앱 서비스 계획 [az webapp 만들](/cli/azure/webapp#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="3cb63-205">응용 프로그램을 배포 하는 hello 웹 응용 프로그램을 제공 된 호스팅 toodeploy 코드 공간 tooview hello 있습니다에 대 한 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="3cb63-206">Toocreate hello 웹 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="3cb63-207">Hello hello 바꿉니다 다음 명령을,  *\<app_name >* 고유한 응용 프로그램 이름 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="3cb63-208">이 이름은 hello 이름 해야 toobe 고유 Azure 앱 서비스의 모든 앱 간에 hello 웹 앱에 대 한 hello 기본 URL의 hello 일부로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="3cb63-209">Hello 웹 응용 프로그램을 만들면 Azure CLI hello 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="3cb63-210">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="3cb63-210">Configure an environment variable</span></span>

<span data-ttu-id="3cb63-211">Hello 자습서, 있습니다 하드 코드 된 hello 데이터베이스에서 연결 문자열의 앞부분에 나오는 _config/env/production.js_합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="3cb63-212">보안 모범 사례에 따라 원하는 tookeep 중요 한 데이터 Git 리포지토리를 벗어났습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="3cb63-213">Azure에서 실행되는 응용 프로그램의 경우는 대신 환경 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="3cb63-214">앱 서비스 환경 변수를 설정 _앱 설정_ hello를 사용 하 여 [az webapp config appsettings 업데이트](/cli/azure/webapp/config/appsettings#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="3cb63-215">hello 다음 예제에서는 구성 된 `MONGODB_URI` Azure 웹 앱의 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="3cb63-216">Hello 대체  *\<app_name >*,  *\<cosmosdb_name >*, 및  *\<primary_master_key >* 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="3cb63-217">Node.js 코드에서는 다른 환경 변수에 액세스할 때와 마찬가지로 `process.env.MONGODB_URI`를 사용하여 이 응용 프로그램 설정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="3cb63-218">이제, 다음 명령을 hello로 변경 내용을 too_config/env/production.js_을 실행 취소:</span><span class="sxs-lookup"><span data-stu-id="3cb63-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="3cb63-219">_config/env/production.js_를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="3cb63-220">Hello 기본 MEAN.js 이러한 앱은 이미 구성 된 toouse hello `MONGODB_URI` 만든 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="3cb63-221">로컬 Git 배포 구성</span><span class="sxs-lookup"><span data-stu-id="3cb63-221">Configure local git deployment</span></span> 

<span data-ttu-id="3cb63-222">사용 하 여 hello [az webapp 배포 사용자 집합](/cli/azure/webapp/deployment/user#set) toocreate 자격 증명 배포에 대 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="3cb63-223">다양 한 방법으로 FTP, 로컬 Git, GitHub, Visual Studio Team Services 및 BitBucket을 포함 하 여 응용 프로그램 tooAzure 앱 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="3cb63-224">FTP 및 로컬 Git에 대 한 필요는 toohave 배포 사용자 배포의 hello 서버 tooauthenticate에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="3cb63-225">이 배포 사용자는 계정 수준이며 Azure 구독 계정과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="3cb63-226">하기만 하면 tooconfigure 배포 사용자가 한 번 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="3cb63-227">Hello에서 다음 명령을, 대체  *\<사용자 이름 >* 및  *\<암호 >* 새 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="3cb63-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="3cb63-228">hello 사용자 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-228">hello user name must be unique.</span></span> <span data-ttu-id="3cb63-229">hello 암호 최소 8 자 이어야, hello 세 요소 다음의 두 개의: 문자, 숫자, 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="3cb63-230">발생 하는 경우는 ` 'Conflict'. Details: 409` 오류, hello 사용자 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="3cb63-231">` 'Bad Request'. Details: 400` 오류가 발생하면 더 강력한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="3cb63-232">레코드 hello 사용자 이름 및 hello 앱을 배포할 때에 이후 단계에서 사용 하기 위해 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="3cb63-233">사용 하 여 hello [az webapp 배포 소스-config-로컬-git](/cli/azure/webapp/deployment/source#config-local-git) 명령 tooconfigure 로컬 Git access toohello Azure 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="3cb63-234">Hello 배포 사용자가 구성 된 경우 hello Azure CLI 형식에 따라 hello에 Azure 웹 앱에 대 한 hello 배포 URL을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="3cb63-235">Hello 다음 단계에서 사용 되므로 hello hello 터미널에서 출력을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="3cb63-236">Git에서 tooAzure 푸시</span><span class="sxs-lookup"><span data-stu-id="3cb63-236">Push tooAzure from Git</span></span>

<span data-ttu-id="3cb63-237">Azure 원격 tooyour 로컬 Git 리포지토리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="3cb63-238">Azure 원격 toodeploy toohello Node.js 응용 프로그램을 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="3cb63-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="3cb63-239">이전 hello 배포 사용자의 hello 만들기의 일부로 제공한 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="3cb63-240">배포하는 동안 Azure App Service는 진행 상황을 Git에 전합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="3cb63-241">Hello 배포 프로세스에서 실행 되도록 하는 것을 알 수 있습니다 [Gulp](http://gulpjs.com/) 후 `npm install`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="3cb63-242">앱 서비스 배포 중 Gulp / Grunt 작업을 실행 하지 않습니다, 그리고 되므로이 샘플 리포지토리는 두 개의 추가 파일의 루트 디렉터리 tooenable에서:</span><span class="sxs-lookup"><span data-stu-id="3cb63-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="3cb63-243">_.deployment_ -이 파일을 통해 앱 서비스 toorun 알 `bash deploy.sh` hello 사용자 지정 배포 스크립트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="3cb63-244">_deploy.sh_ -사용자 지정 배포 스크립트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="3cb63-245">Hello 파일을 검토 하는 경우 실행 되는지 표시 됩니다 `gulp prod` 후 `npm install` 및 `bower install`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="3cb63-246">이 접근 방식을 tooadd 모든 단계 tooyour Git 기반 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="3cb63-247">언제든지 Azure Web App을 다시 시작하면 App Service에서 이 자동화 작업을 다시 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="3cb63-248">Toohello Azure 웹 앱을 찾아보기</span><span class="sxs-lookup"><span data-stu-id="3cb63-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="3cb63-249">찾아보기 toohello 웹 브라우저를 사용 하 여 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="3cb63-250">클릭 **등록** 에 최상위 메뉴 hello 및 더미 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="3cb63-251">성공 하 고 hello 앱 자동으로 로그인 하는 경우 Azure에서 만들어진 사용자를 다음 MEAN.js 앱 toohello 연결 toohello MongoDB (Cosmos DB) 데이터베이스를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Azure App Service에서 실행 중인 MEAN.js 응용 프로그램](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="3cb63-253">선택 **관리 > 관리 문서** tooadd 일부 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="3cb63-254">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="3cb63-254">**Congratulations!**</span></span> <span data-ttu-id="3cb63-255">Azure App Service에서 데이터 기반 Node.js 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="3cb63-256">데이터 모델 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="3cb63-256">Update data model and redeploy</span></span>

<span data-ttu-id="3cb63-257">이 단계에서는 hello 변경한 `article` 데이터 모델 및 변경 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="3cb63-258">Hello 데이터 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="3cb63-258">Update hello data model</span></span>

<span data-ttu-id="3cb63-259">_modules/articles/server/models/article.server.model.js_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="3cb63-260">`ArticleSchema`에서 `comment`라는 `String` 형식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="3cb63-261">완료된 후의 스키마 코드는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="3cb63-262">Hello 문서 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="3cb63-262">Update hello articles code</span></span>

<span data-ttu-id="3cb63-263">Hello 나머지 업데이트 프로그램 `articles` toouse 코드 `comment`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="3cb63-264">5 개의 파일이 toomodify 필요한: hello 서버 컨트롤러 및 4 hello 클라이언트 뷰.</span><span class="sxs-lookup"><span data-stu-id="3cb63-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="3cb63-265">_modules/articles/server/controllers/articles.server.controller.js_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="3cb63-266">Hello에 `update` 함수를 날짜에 대 한 추가 `article.comment`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="3cb63-267">hello 다음 보여 주는 코드를 완료 하는 hello `update` 함수:</span><span class="sxs-lookup"><span data-stu-id="3cb63-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="3cb63-268">_modules/articles/client/views/view-article.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="3cb63-269">Hello 닫는 바로 위에 `</section>` 태그에 다음 줄 toodisplay hello 추가 `comment` hello 나머지 hello 문서 데이터와 함께:</span><span class="sxs-lookup"><span data-stu-id="3cb63-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="3cb63-270">_modules/articles/client/views/list-articles.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="3cb63-271">Hello 닫는 바로 위에 `</a>` 태그에 다음 줄 toodisplay hello 추가 `comment` hello 나머지 hello 문서 데이터와 함께:</span><span class="sxs-lookup"><span data-stu-id="3cb63-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="3cb63-272">_modules/articles/client/views/admin/list-articles.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="3cb63-273">내부 hello `<div class="list-group">` 요소 및 hello 닫는 바로 위에 `</a>` 태그에 다음 줄 toodisplay hello 추가 `comment` hello 나머지 hello 문서 데이터와 함께:</span><span class="sxs-lookup"><span data-stu-id="3cb63-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="3cb63-274">_modules/articles/client/views/admin/form-article.client.view.html_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="3cb63-275">Hello `<div class="form-group">` hello 전송 단추, 다음과 같은 포함 된 요소:</span><span class="sxs-lookup"><span data-stu-id="3cb63-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="3cb63-276">이 태그 바로 위에 다른 항목 추가 `<div class="form-group">` hello를 편집 하는 사람들 요소 `comment` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="3cb63-277">새 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="3cb63-278">변경 내용을 로컬에서 테스트</span><span class="sxs-lookup"><span data-stu-id="3cb63-278">Test your changes locally</span></span>

<span data-ttu-id="3cb63-279">변경 내용을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-279">Save all your changes.</span></span>

<span data-ttu-id="3cb63-280">프로덕션 모드에서 변경 내용을 다시 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="3cb63-281">프로그램 _config/env/production.js_ 되돌려 졌습니다 및 hello `MONGODB_URI` 환경 변수는 로컬 컴퓨터에 없는 Azure 웹 앱에만 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="3cb63-282">해당 hello 찾을 hello 구성 파일을 보면: production 구성 기본값 toouse 로컬 MongoDB 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="3cb63-283">이렇게 하면 로컬에서 코드 변경 내용을 테스트할 때 프로덕션 데이터를 건드리지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="3cb63-284">너무 이동`http://localhost:8443` 브라우저에서 로그인 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="3cb63-285">선택 **관리 > 관리 문서**, 다음 hello를 선택 하 여 아티클을 추가  **+**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="3cb63-286">Hello 새 참조 `Comment` 이제 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-286">You see hello new `Comment` textbox now.</span></span>

![추가 된 주석 필드 tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="3cb63-288">Hello 터미널에서 입력 하 여 Node.js 중지 `Ctrl+C`합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="3cb63-289">변경 내용을 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="3cb63-289">Publish changes tooAzure</span></span>

<span data-ttu-id="3cb63-290">Git에서 변경 내용을 적용 한 다음 hello 코드 변경 내용을 tooAzure 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="3cb63-291">한 번 hello `git push` 완료 tooyour Azure 웹 앱을 탐색 하 고 hello 새 기능을 시험해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![모델 및 데이터베이스 변경 내용이 게시 tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="3cb63-293">이전에 문서를 추가했으면 그 문서를 지금도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="3cb63-294">Cosmos DB의 기존 데이터는 손실되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="3cb63-295">또한 업데이트 toohello 데이터 스키마 기존 데이터를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="3cb63-296">진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="3cb63-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="3cb63-297">Azure 앱 서비스에서 Node.js 응용 프로그램이 실행 되는 동안 hello 콘솔 로그 파이프 된 tooyour 터미널 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="3cb63-298">이런 방식으로 가져올 수 있습니다 hello 같은 진단 메시지 toohelp 응용 프로그램 오류를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="3cb63-299">스트리밍을 사용 하 여 hello toostart 로그 [az webapp 비상 로그](/cli/azure/webapp/log#tail) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="3cb63-300">스트리밍 로그 시작 된 후 일부 웹 트래픽을 hello 브라우저 tooget에서 Azure 웹 앱을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="3cb63-301">콘솔 로그 파이프 tooyour 터미널 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="3cb63-302">언제든지 `Ctrl+C`를 입력하여 로그 스트리밍을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="3cb63-303">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="3cb63-303">Manage your Azure web app</span></span>

<span data-ttu-id="3cb63-304">Toohello 이동 [Azure 포털](https://portal.azure.com) 만든 toosee hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="3cb63-305">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="3cb63-307">기본적으로 hello 포털은 웹 앱의 표시 **개요** 페이지.</span><span class="sxs-lookup"><span data-stu-id="3cb63-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="3cb63-308">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="3cb63-309">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="3cb63-310">hello hello 페이지의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="3cb63-312">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cb63-312">Next steps</span></span>

<span data-ttu-id="3cb63-313">학습한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3cb63-314">Azure에서 MongoDB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3cb63-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="3cb63-315">Node.js 앱 tooMongoDB 연결</span><span class="sxs-lookup"><span data-stu-id="3cb63-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="3cb63-316">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="3cb63-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="3cb63-317">Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="3cb63-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="3cb63-318">Azure tooyour 터미널에서 스트림 로그</span><span class="sxs-lookup"><span data-stu-id="3cb63-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="3cb63-319">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="3cb63-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="3cb63-320">다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap tooyour 웹 앱의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb63-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="3cb63-321">지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3cb63-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
