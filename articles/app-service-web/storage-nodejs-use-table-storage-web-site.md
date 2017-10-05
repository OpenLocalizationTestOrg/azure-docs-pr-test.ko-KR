---
title: "Azure 테이블 서비스를 사용하는 Node.js 웹앱"
description: "이 자습서는 Azure 테이블 서비스를 사용하여 Azure 앱 서비스 웹앱에서 호스트되는 Node.js 응용프로그램의 데이터를 저장하는 방법을 설명합니다."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="f335e-103">Azure 테이블 서비스를 사용하는 Node.js 웹앱</span><span class="sxs-lookup"><span data-stu-id="f335e-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="f335e-104">개요</span><span class="sxs-lookup"><span data-stu-id="f335e-104">Overview</span></span>
<span data-ttu-id="f335e-105">이 자습서에서는 Azure Data Management에서 제공하는 Table service를 사용하여 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 웹앱에서 호스트되는 [node] 응용 프로그램에서 데이터를 저장하고 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="f335e-106">이 자습서에서는 이전에 node 및 [Git]를 사용한 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="f335e-107">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-107">You will learn:</span></span>

* <span data-ttu-id="f335e-108">npm(node 패키지 관리자)을 사용하여 node 모듈을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="f335e-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="f335e-109">Azure 테이블 서비스에 대한 작업 방법</span><span class="sxs-lookup"><span data-stu-id="f335e-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="f335e-110">Azure CLI를 사용하여 웹앱을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f335e-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="f335e-111">이 자습서를 따라 작업을 만들고, 검색하고, 완료할 수 있는 간단한 웹 기반 "할 일 모음" 응용프로그램을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="f335e-112">작업은 테이블 서비스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="f335e-113">다음은 완성된 응용프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-113">Here is the completed application:</span></span>

![빈 tasklist가 표시된 웹 페이지][node-table-finished]

> [!NOTE]
> <span data-ttu-id="f335e-115">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f335e-116">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f335e-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f335e-117">Prerequisites</span></span>
<span data-ttu-id="f335e-118">이 문서의 지침을 따르기 전에 다음이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="f335e-119">[node] 버전 0.10.24 이상</span><span class="sxs-lookup"><span data-stu-id="f335e-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="f335e-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="f335e-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="f335e-121">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f335e-121">Create a storage account</span></span>
<span data-ttu-id="f335e-122">Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-122">Create an Azure storage account.</span></span> <span data-ttu-id="f335e-123">앱에서는 할 일 항목을 저장하기 위해 이 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="f335e-124">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f335e-125">포털의 왼쪽 아래에서 **새로 만들기** 아이콘을 클릭한 다음 **데이터 + 저장소** > **저장소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="f335e-126">저장소 계정에 고유한 이름을 지정하고 이를 위한 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![새 단추](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="f335e-128">저장소 계정이 만들어지면 **알림** 단추가 녹색 **성공**으로 깜박이고 저장소 계정의 블레이드가 열려 새로 만든 리소스 그룹에 속한 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="f335e-129">저장소 계정의 블레이드에서 **설정** > **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="f335e-130">기본 액세스 키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-130">Copy the primary access key to the clipboard.</span></span>
   
    ![액세스 키][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="f335e-132">모듈 설치 및 스캐폴딩 생성</span><span class="sxs-lookup"><span data-stu-id="f335e-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="f335e-133">이 섹션에서는 새로운 Node 응용 프로그램을 만들고 npm을 사용하여 모듈 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="f335e-134">이 응용 프로그램의 경우 [Express] 및 [Azure] 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="f335e-135">Express 모듈은 node에 모델 보기 컨트롤러 프레임워크를 제공하지만 Azure 모듈은 테이블 서비스에 대한 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="f335e-136">express 설치 및 스캐폴딩 생성</span><span class="sxs-lookup"><span data-stu-id="f335e-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="f335e-137">명령줄에서 **tasklist** 라는 새 디렉터리를 만들고 해당 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="f335e-138">다음 명령을 입력하여 Express 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="f335e-139">운영 체제에 따라 명령 앞에 'sudo'를 배치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="f335e-140">출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="f335e-141">'-g' 매개 변수는 모듈을 전역적으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="f335e-142">이와 같이 **express** 를 사용하여 추가 경로 정보를 입력하지 않고도 웹앱 스캐폴딩을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="f335e-143">응용프로그램에 대한 스캐폴딩을 만들려면 **express** 명령을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="f335e-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="f335e-144">이 명령의 출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-144">The output of this command appears similar to the following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="f335e-145">이제 **tasklist** 디렉터리에 몇 개의 새 디렉터리 및 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="f335e-146">추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="f335e-146">Install additional modules</span></span>
<span data-ttu-id="f335e-147">**express**로 만든 파일 중 하나는 **package.json**입니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="f335e-148">이 파일에는 모듈 종속성 목록이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="f335e-149">나중에 이 응용프로그램을 앱 서비스 웹앱에 배포하는 경우 이 파일을 사용하여 Azure에 설치해야 할 모듈을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="f335e-150">명령줄에서 다음 명령을 입력하여 **package.json** 파일에 설명된 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="f335e-151">'sudo'를 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="f335e-152">이 명령의 출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="f335e-153">이제 다음 명령을 입력하여 [azure], [node-uuid], [nconf] 및 [async] 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="f335e-154">**--save** 플래그는 이러한 모듈에 대한 항목을 **package.json** 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="f335e-155">이 명령의 출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="f335e-156">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f335e-156">Create the application</span></span>
<span data-ttu-id="f335e-157">이제 응용프로그램을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="f335e-158">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="f335e-158">Create a model</span></span>
<span data-ttu-id="f335e-159">*모델* 은 응용프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="f335e-160">응용프로그램의 경우 모델만 할 일 목록에서 항목을 나타내는 작업 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="f335e-161">작업에는 다음 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="f335e-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="f335e-162">PartitionKey</span></span>
* <span data-ttu-id="f335e-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="f335e-163">RowKey</span></span>
* <span data-ttu-id="f335e-164">이름(문자열)</span><span class="sxs-lookup"><span data-stu-id="f335e-164">name (string)</span></span>
* <span data-ttu-id="f335e-165">범주(문자열)</span><span class="sxs-lookup"><span data-stu-id="f335e-165">category (string)</span></span>
* <span data-ttu-id="f335e-166">완료됨(부울)</span><span class="sxs-lookup"><span data-stu-id="f335e-166">completed (Boolean)</span></span>

<span data-ttu-id="f335e-167">**PartitionKey** 및 **RowKey**는 테이블 키로 Table Service에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="f335e-168">자세한 내용은 [테이블 서비스 데이터 모델 이해](https://msdn.microsoft.com/library/azure/dd179338.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f335e-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="f335e-169">**tasklist** 디렉터리에서 **models**라는 새로운 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="f335e-170">**models** 디렉터리에서 **task.js**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="f335e-171">이 파일에는 응용 프로그램에서 만든 작업 모델이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="f335e-172">**task.js** 파일의 시작 부분에 필수 라이브러리를 참조하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="f335e-173">Task 개체를 정의하고 내보내는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="f335e-174">이 개체가 테이블에 연결하는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-174">This object is responsible for connecting to the table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="f335e-175">다음 코드를 추가하여 Task 개체에서 추가 메서드를 정의합니다. 이 메서드가 테이블에 저장된 데이터에 대한 조작을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator to set types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="f335e-176">**task.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="f335e-177">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="f335e-177">Create a controller</span></span>
<span data-ttu-id="f335e-178">*컨트롤러* 는 HTTP 요청을 처리하고 HTML 응답을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="f335e-179">**tasklist/routes** 디렉터리에서 **tasklist.js**라는 새 파일을 만들고 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="f335e-180">아래 코드를 **tasklist.js**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="f335e-181">이 코드는 **tasklist.js**에 사용되는 azure 및 async 모듈을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="f335e-182">또한 **TaskList** 함수를 정의합니다. 이 함수에 앞서 정의한 **Task** 개체의 인스턴스가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="f335e-183">**TaskList** 개체를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="f335e-184">다음 메소드를 **TaskList**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-184">Add the following methods to **TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="f335e-185">app.js 수정</span><span class="sxs-lookup"><span data-stu-id="f335e-185">Modify app.js</span></span>
1. <span data-ttu-id="f335e-186">**tasklist** 디렉터리에서 **app.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="f335e-187">이 파일은 앞에서 **express** 명령을 실행하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="f335e-188">파일의 앞부분에 다음을 추가하여 azure 모듈을 로드하고 테이블 이름인 파티션 키를 설정하고 이 예제에서 사용한 저장소 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="f335e-189">nconf는 환경 변수 또는 나중에 만들 **config.json** 파일에서 구성 값을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="f335e-190">app.js 파일에서 다음 줄이 보일 때까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="f335e-191">위의 줄을 아래의 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="f335e-192">이 코드는 저장소 계정에 대한 연결을 사용하여 <strong>Task</strong>의 인스턴스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="f335e-193">이 인스턴스는 <strong>TaskList</strong>로 전달되어 테이블 서비스와의 통신에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="f335e-194">**app.js** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="f335e-195">인덱스 보기 수정</span><span class="sxs-lookup"><span data-stu-id="f335e-195">Modify the index view</span></span>
1. <span data-ttu-id="f335e-196">**tasklist/views/index.jade** 파일을 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="f335e-197">파일의 전체 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="f335e-198">이렇게 하면 기존 작업을 표시하는 보기와 새 작업을 추가하고 기존 작업을 완료로 표시하는 양식이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="f335e-199">**index.jade** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="f335e-200">전역 레이아웃 수정</span><span class="sxs-lookup"><span data-stu-id="f335e-200">Modify the global layout</span></span>
<span data-ttu-id="f335e-201">**views** 디렉터리의 **layout.jade** 파일은 다른 **.jade** 파일에 대한 전역 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="f335e-202">이 단계에서는 멋진 모습의 웹앱을 쉽게 디자인할 수 있게 해주는 도구 키트인 [Twitter Bootstrap](https://github.com/twbs/bootstrap)을 사용하도록 이 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="f335e-203">[Twitter Bootstrap](http://getbootstrap.com/)용 파일을 다운로드하여 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="f335e-204">Bootstrap **css** 폴더의 **bootstrap.min.css** 파일을 응용 프로그램의 **public/stylesheets** 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="f335e-205">**views** 폴더에서 **layout.jade**를 열고 전체 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="f335e-206">구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="f335e-206">Create a config file</span></span>
<span data-ttu-id="f335e-207">앱을 로컬로 실행하기 위해 Azure 저장소 자격 증명을 구성 파일에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="f335e-208">다음 JSON으로 **config.json* *이라는 이름의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="f335e-209">**저장소 계정 이름**을 앞서 만든 저장소 계정 이름으로 바꾸고 **저장소 액세스 키**를 저장소 계정의 기본 선택키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="f335e-210">예:</span><span class="sxs-lookup"><span data-stu-id="f335e-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="f335e-211">다음과 같이 이 파일을 *tasklist* 디렉터리보다 **한 디렉터리 높은 단계** 에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="f335e-212">공용이 될 수 있는 원본 제어기에 구성 파일을 확인하지 않도록 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="f335e-213">Azure에 앱을 배포할 때 구성 파일 대신 환경 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="f335e-214">로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f335e-214">Run the application locally</span></span>
<span data-ttu-id="f335e-215">로컬 컴퓨터에서 응용 프로그램을 테스트하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="f335e-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="f335e-216">명령줄에서 **tasklist** 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="f335e-217">다음 명령을 사용하여 응용 프로그램을 로컬에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="f335e-218">웹 브라우저를 열고 http://127.0.0.1:3000 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="f335e-219">다음 예제와 유사한 웹 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-219">A web page similar to the following example appears.</span></span>
   
    ![빈 tasklist가 표시된 웹 페이지][node-table-finished]
4. <span data-ttu-id="f335e-221">새 할 일 항목을 만들려면 이름 및 범주를 입력하고 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="f335e-222">작업을 완료로 표시하려면 **완료**에 표시하고 **작업 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![작업 목록의 새 항목 이미지][node-table-list-items]

<span data-ttu-id="f335e-224">응용프로그램이 로컬로 실행함에도 불구하고 Azure 테이블 서비스에 해당 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="f335e-225">Azure에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f335e-225">Deploy your application to Azure</span></span>
<span data-ttu-id="f335e-226">이 섹션의 단계는 Azure 명령줄 도구를 사용하여 앱 서비스에서 새 웹앱을 만든 다음 Git을 사용하여 응용프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="f335e-227">이러한 단계를 수행하려면 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f335e-228">이러한 단계는 [Azure 포털](https://portal.azure.com/)을 사용하여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f335e-229">[Azure 앱 서비스에서 Node.js 웹앱 빌드 및 배포]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f335e-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="f335e-230">처음으로 만든 웹앱인 경우 Azure 포털을 사용하여 이 응용프로그램을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="f335e-231">시작하려면 명령줄에서 다음 명령을 입력하여 [Azure CLI] 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="f335e-232">게시 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="f335e-232">Import publishing settings</span></span>
<span data-ttu-id="f335e-233">이 단계에서는 구독에 대한 정보를 포함하는 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="f335e-234">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="f335e-235">이 명령은 브라우저를 시작하고 다운로드 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="f335e-236">메시지가 나타나면 Azure 구독과 관련된 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="f335e-237">파일 다운로드가 자동으로 시작됩니다. 그렇지 않은 경우 페이지 처음 부분에서 링크를 클릭하여 수동으로 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="f335e-238">파일을 저장하고 파일 경로를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="f335e-239">다음 명령을 입력하여 설정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="f335e-240">이전 단계에서 다운로드한 게시 설정 파일의 경로와 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="f335e-241">설정을 가져온 후에는 게시 설정 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="f335e-242">이 파일은 더 이상 필요하지 않으며 Azure 구독과 관련된 중요한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="f335e-243">앱 서비스 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f335e-243">Create an App Service web app</span></span>
1. <span data-ttu-id="f335e-244">명령줄에서 **tasklist** 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="f335e-245">다음 명령을 사용하여 새 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="f335e-246">웹앱 이름 및 위치를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="f335e-247">고유한 이름을 제공하고 Azure 저장소 계정과 동일한 지리적 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="f335e-248">`--git` 매개 변수는 Azure에 이 웹앱에 대한 Git 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="f335e-249">현재 디렉터리에 존재하는 항목이 없는 경우 Git 리포지토리를 초기화하고 'azure'라는 [Git 원격] 을 추가하여 Azure에 응용프로그램을 게시하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="f335e-250">마지막으로 Azure에서 노드 응용프로그램을 호스트하는 데 사용하는 설정이 포함된 **web.config** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="f335e-251">`--git` 매개 변수를 생략하지만 해당 디렉터리가 Git 리포지토리를 포함하는 경우에도 이 명령은 여전히 'azure' 원격을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="f335e-252">이 명령이 완료되면 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="f335e-253">**Website created at** 으로 시작하는 줄에 웹앱의 URL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="f335e-254">구독에 대한 앱 서비스 웹앱을 처음 만드는 경우 Azure 포털을 사용하여 웹앱을 만들라고 안내됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="f335e-255">자세한 내용은 [Azure 앱 서비스에서 Node.js 웹앱 빌드 및 배포]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f335e-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="f335e-256">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="f335e-256">Set environment variables</span></span>
<span data-ttu-id="f335e-257">이 단계에서는 Azure에서 웹앱 구성에 환경 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="f335e-258">명령줄에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="f335e-259">**<storage account name>**을 앞서 만든 저장소 계정 이름으로 바꾸고 **<storage access key>**를 저장소 계정의 기본 선택키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="f335e-260">(이전에 만든 config.json 파일과 동일한 값을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="f335e-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="f335e-261">또는 [Azure 포털](https://portal.azure.com/)에서 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="f335e-262">**찾아보기** > **Web Apps** > 사용자의 웹앱 이름을 클릭하여 웹앱 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="f335e-263">웹앱 블레이드에서 **모든 설정** > **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="f335e-264">**앱 설정** 섹션으로 스크롤하여 키/값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![앱 설정](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="f335e-266">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="f335e-267">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="f335e-267">Publish the application</span></span>
<span data-ttu-id="f335e-268">앱을 게시하려면 코드 파일을 Git으로 커밋한 다음 azure/master로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="f335e-269">배포 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="f335e-270">응용프로그램 파일을 추가 및 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="f335e-271">앱 서비스 웹앱으로 커밋을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="f335e-272">대상 분기로 **master** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-272">Use **master** as the target branch.</span></span> <span data-ttu-id="f335e-273">배포가 끝나면 다음 예제와 유사한 문이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="f335e-274">푸시 작업이 완료되면 `azure create site` 명령에서 이전에 반환한 웹앱 URL로 이동하여 응용프로그램을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f335e-275">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f335e-275">Next steps</span></span>
<span data-ttu-id="f335e-276">이 문서의 단계에서는 Table Service를 사용하여 정보를 저장하는 방법에 대해 설명하지만 [MongoDB](https://mlab.com/azure/)도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f335e-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f335e-277">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f335e-277">Additional resources</span></span>
<span data-ttu-id="f335e-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="f335e-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f335e-279">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="f335e-279">What's changed</span></span>
* <span data-ttu-id="f335e-280">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f335e-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="f335e-281">[Azure 앱 서비스에서 Node.js 웹앱 빌드 및 배포]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="f335e-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="f335e-282">[node]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="f335e-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="f335e-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="f335e-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="f335e-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="f335e-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="f335e-285">[Git 원격]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="f335e-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="f335e-286">[Azure CLI]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="f335e-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="f335e-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="f335e-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="f335e-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="f335e-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="f335e-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="f335e-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="f335e-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="f335e-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
