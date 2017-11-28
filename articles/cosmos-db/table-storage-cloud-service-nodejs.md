---
title: "테이블 저장소를 사용하는 웹앱(Node.js) | Microsoft Docs"
description: "Azure 저장소 서비스 및 Azure 모듈을 추가해 Express를 사용하여 웹 앱 빌드 자습서를 기반으로 응용 프로그램을 빌드하는 자습서입니다."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b802f880c1131abb7eb9ba00dd8f2e65017bc802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="7f6e2-103">저장소를 사용하는 Node.js 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="7f6e2-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="7f6e2-104">개요</span><span class="sxs-lookup"><span data-stu-id="7f6e2-104">Overview</span></span>
<span data-ttu-id="7f6e2-105">이 자습서에서는 데이터 관리 서비스를 작업하도록 Node.js용 Microsoft Azure Client Libraries를 사용하여 [Express를 사용하는 Node.js 웹 응용 프로그램] 자습서에서 만든 응용 프로그램을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-105">In this tutorial, the application you created in the [Node.js Web Application using Express] tutorial is extended using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="7f6e2-106">Azure에 배포할 수 있는 웹 기반 작업 목록 응용 프로그램을 만들도록 응용 프로그램을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-106">You extend your application by creating a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="7f6e2-107">작업 목록을 통해 사용자는 작업을 가져오고 새 작업을 추가하고 작업을 완료로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="7f6e2-108">작업 항목은 Azure 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="7f6e2-109">Azure 저장소는 내결함성과 고가용성이 있는 구조화되지 않은 데이터 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="7f6e2-110">Azure Storage에는 데이터를 저장 및 액세스할 수 있는 몇 가지 데이터 구조가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="7f6e2-111">Node.js용 Azure SDK에 포함된 API 또는 REST API를 통해 저장소 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-111">You can use the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="7f6e2-112">자세한 내용은 [Azure에 데이터 저장 및 액세스]를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="7f6e2-113">이 자습서는 [Node.js 웹 응용 프로그램] 및 [Express를 사용하는 Node.js][Express를 사용하는 Node.js 웹 응용 프로그램] 자습서를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-113">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="7f6e2-114">여기에는 다음 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-114">It contains the following information:</span></span>

* <span data-ttu-id="7f6e2-115">Jade 템플릿 엔진으로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f6e2-115">How to work with the Jade template engine</span></span>
* <span data-ttu-id="7f6e2-116">Azure 데이터 관리 서비스로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f6e2-116">How to work with Azure Data Management services</span></span>

<span data-ttu-id="7f6e2-117">다음 스크린샷에 완성된 응용 프로그램이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-117">The following screenshot shows the completed application:</span></span>

![Internet Explorer의 완료된 웹 페이지](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="7f6e2-119">Web.Config에서 저장소 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="7f6e2-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="7f6e2-120">Azure Storage에 액세스하려면 저장소 자격 증명을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-120">You must pass in storage credentials to access Azure Storage.</span></span> <span data-ttu-id="7f6e2-121">이를 위해 web.config 응용 프로그램 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-121">This is done by utilizing the web.config application settings.</span></span>
<span data-ttu-id="7f6e2-122">web.config 설정은 환경 변수로서 노드에 전달된 다음 Azure SDK에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-122">The web.config settings are passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="7f6e2-123">저장소 자격 증명은 응용 프로그램이 Azure에 배포될 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-123">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="7f6e2-124">에뮬레이터에서 실행 중이면 응용 프로그램은 저장소 에뮬레이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-124">When running in the emulator, the application uses the storage emulator.</span></span>
>
>

<span data-ttu-id="7f6e2-125">다음 단계에 따라 저장소 계정 자격 증명을 가져와 web.config 설정에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-125">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="7f6e2-126">설정이 열려 있지 않은 경우 **모든 프로그램, Azure**를 확장하고 **Azure PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 선택하여 **시작** 메뉴에서 Azure PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-126">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="7f6e2-127">응용 프로그램이 포함된 폴더로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-127">Change directories to the folder containing your application.</span></span> <span data-ttu-id="7f6e2-128">예를 들어 C:\\node\\tasklist\\WebRole1로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="7f6e2-129">Azure Powershell 창에서 다음 cmdlet을 입력하여 저장소 계정 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-129">From the Azure Powershell window, enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="7f6e2-130">앞에 나오는 cmdlet은 호스티드 서비스와 연결된 저장소 계정 및 계정 키 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-130">The preceding cmdlet retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f6e2-131">서비스를 배포할 때 Azure SDK가 저장소 계정을 만들기 때문에 저장소 계정은 이전 가이드에서 응용 프로그램을 배포해서 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-131">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="7f6e2-132">응용 프로그램이 Azure에 배포될 때 사용하는 환경 설정이 포함된 **ServiceDefinition.csdef** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-132">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="7f6e2-133">**Environment** 요소 아래에 다음 블록을 삽입하고 {STORAGE ACCOUNT} 및 {STORAGE ACCESS KEY}를 배포에 사용할 저장소 계정의 계정 이름 및 기본 키로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-133">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![web.cloud.config 파일 콘텐츠](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="7f6e2-135">파일을 저장하고 메모장을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-135">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="7f6e2-136">추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="7f6e2-136">Install additional modules</span></span>
1. <span data-ttu-id="7f6e2-137">다음 명령을 사용하여 [azure], [node-uuid], [nconf] 및 [async] 모듈을 로컬에 설치하고 해당 모듈의 항목을 **package.json** 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-137">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="7f6e2-138">이 명령의 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-138">The output of this command should appear similar to the following:</span></span>

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="7f6e2-139">node 응용 프로그램에서 테이블 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="7f6e2-139">Using the Table service in a node application</span></span>
<span data-ttu-id="7f6e2-140">이 섹션에서는 작업에 대한 모델을 포함하는 **task.js** 파일을 추가하여 **express** 명령으로 만들어진 기본 응용 프로그램을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-140">In this section, the basic application created by the **express** command is extended by adding a **task.js** file containing the model for your tasks.</span></span> <span data-ttu-id="7f6e2-141">기존 **app.js** 파일을 수정하고 모델을 사용하는 새 **tasklist.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-141">Modify the existing **app.js** file and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="7f6e2-142">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="7f6e2-142">Create the model</span></span>
1. <span data-ttu-id="7f6e2-143">**WebRole1** 디렉터리에서 **models**라는 새로운 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-143">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="7f6e2-144">**models** 디렉터리에서 **task.js**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-144">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="7f6e2-145">이 파일에는 응용 프로그램에서 만든 작업 모델이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-145">This file contains the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="7f6e2-146">**task.js** 파일의 시작 부분에 필수 라이브러리를 참조하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-146">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="7f6e2-147">그런 다음, Task 개체를 정의하고 내보내는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-147">Next, add code to define and export the Task object.</span></span> <span data-ttu-id="7f6e2-148">Task 개체가 테이블에 연결하는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-148">The Task object is responsible for connecting to the table.</span></span>

    ```nodejs
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
    ```

5. <span data-ttu-id="7f6e2-149">이제 다음 코드를 추가하여 Task 개체에서 추가 메서드를 정의합니다. 이 메서드가 테이블에 저장된 데이터에 대한 조작을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-149">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. <span data-ttu-id="7f6e2-150">**task.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-150">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="7f6e2-151">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="7f6e2-151">Create the controller</span></span>
1. <span data-ttu-id="7f6e2-152">**WebRole1/routes** 디렉터리에서 **tasklist.js**라는 새 파일을 만들고 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-152">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="7f6e2-153">아래 코드를 **tasklist.js**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-153">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="7f6e2-154">이 코드는 **tasklist.js**에서 사용되는 Azure 및 비동기 모듈을 로드하고 이전에 정의한 **Task** 개체의 인스턴스에 전달되는 **TaskList** 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-154">This code loads the azure and async modules, which are used by **tasklist.js** and defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="7f6e2-155">**showTasks**, **addTask** 및 **completeTasks**에 사용된 메서드를 추가하여 **tasklist.js** 파일에 계속 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. <span data-ttu-id="7f6e2-156">**tasklist.js** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="7f6e2-157">app.js 수정</span><span class="sxs-lookup"><span data-stu-id="7f6e2-157">Modify app.js</span></span>
1. <span data-ttu-id="7f6e2-158">**WebRole1** 디렉터리에 있는 **app.js** 파일을 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="7f6e2-159">파일 시작 부분에 다음을 추가하여 azure 모듈을 로드하고 테이블 이름과 파티션 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="7f6e2-160">app.js 파일에서 다음 줄이 보일 때까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="7f6e2-161">앞에 나온 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-161">Replace the preceding lines with the following code.</span></span> <span data-ttu-id="7f6e2-162">이 코드는 저장소 계정에 대한 연결을 사용하여 <strong>Task</strong>의 인스턴스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-162">This code initializes an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="7f6e2-163"><strong>Task</strong>는 <strong>TaskList</strong>로 전달되어 Table Service와의 통신에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-163">The <strong>Task</strong> is passed to the <strong>TaskList</strong>, which uses it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="7f6e2-164">**app.js** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="7f6e2-165">인덱스 보기 수정</span><span class="sxs-lookup"><span data-stu-id="7f6e2-165">Modify the index view</span></span>
1. <span data-ttu-id="7f6e2-166">디렉터리를 **views** 디렉터리로 변경하고 **index.jade** 파일을 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="7f6e2-167">**index.jade** 파일 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-167">Replace the contents of the **index.jade** file with the following code.</span></span> <span data-ttu-id="7f6e2-168">이 코드는 기존 작업을 표시하는 데 사용되는 보기와 새 작업을 추가하고 기존 작업을 완료로 표시하는 데 사용되는 양식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-168">This code defines the view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

    ```
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
          if tasks != []
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
    ```

3. <span data-ttu-id="7f6e2-169">**index.jade** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="7f6e2-170">전역 레이아웃 수정</span><span class="sxs-lookup"><span data-stu-id="7f6e2-170">Modify the global layout</span></span>
<span data-ttu-id="7f6e2-171">**views** 디렉터리의 **layout.jade** 파일은 다른 **.jade** 파일에 대한 전역 템플릿으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="7f6e2-172">이 단계에서는 멋진 모습의 웹 사이트를 쉽게 디자인할 수 있게 해주는 도구 키트인 [Twitter Bootstrap](https://github.com/twbs/bootstrap)을 사용하도록 **layout.jade** 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-172">In this step, modify the **layout.jade** file to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="7f6e2-173">[Twitter Bootstrap](http://getbootstrap.com/)용 파일을 다운로드하여 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="7f6e2-174">**bootstrap\\dist\\css** 폴더의 **bootstrap.min.css** 파일을 tasklist 응용 프로그램의 **public\\stylesheets** 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="7f6e2-175">**views** 폴더에 있는 **layout.jade** 파일을 텍스트 편집기에서 열어 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-175">From the **views** folder, open the **layout.jade** file in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="7f6e2-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="7f6e2-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="7f6e2-177">**layout.jade** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="7f6e2-178">에뮬레이터에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7f6e2-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="7f6e2-179">에뮬레이터에서 응용 프로그램을 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="7f6e2-180">브라우저가 열리며 다음 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-180">The browser opens and displays the following page:</span></span>

![작업 및 새 작업을 추가할 필드를 포함하는 테이블이 있는 내 작업 목록 웹 페이지](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="7f6e2-182">양식을 사용하여 항목을 추가하거나 기존 항목을 완료됨으로 표시하여 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="7f6e2-183">Azure에 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="7f6e2-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="7f6e2-184">Windows PowerShell 창에서 다음 cmdlet을 호출하여 호스티드 서비스를 Azure에 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="7f6e2-185">**myuniquename**을 이 응용 프로그램의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="7f6e2-186">**datacentername**을 **West US**와 같은 Azure 데이터 센터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="7f6e2-187">배포가 완료된 후 다음과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="7f6e2-188">이전 cmdlet에서 **-launch** 옵션을 지정했으므로 브라우저가 열리며 게시가 완료될 때 Azure에서 실행 중인 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-188">By specifying the **-launch** option in the previous cmdlet, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![내 작업 목록 페이지를 표시하는 브라우저 창.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="7f6e2-191">응용 프로그램 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="7f6e2-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="7f6e2-192">추가 비용을 방지하거나 다른 응용 프로그램을 빌드 및 배포할 수 있도록 이전에 배포한 응용 프로그램을 무료 평가판 기간 동안 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="7f6e2-193">Azure는 사용된 서버 시간의 시간당 웹 역할 인스턴스 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="7f6e2-194">서버 시간은 응용 프로그램이 배포된 다음에 사용되며 인스턴스가 실행되지 않고 중지된 상태인 경우에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="7f6e2-195">다음 단계에 따라 응용 프로그램을 중지 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="7f6e2-196">Windows PowerShell 창에서, 이전 섹션에서 만든 서비스 배포를 다음 cmdlet을 사용하여 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="7f6e2-197">서비스를 중지하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="7f6e2-198">서비스가 중지되면 서비스가 중지되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="7f6e2-199">서비스를 삭제하려면 다음 cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="7f6e2-200">메시지가 표시되면 **Y** 를 입력하여 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="7f6e2-201">서비스를 삭제하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="7f6e2-202">서비스가 삭제되면 서비스가 삭제되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-202">After the service is deleted, you will receive a message indicating that the service was deleted.</span></span>

[Express를 사용하는 Node.js 웹 응용 프로그램]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Azure에 데이터 저장 및 액세스]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js 웹 응용 프로그램]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


