---
title: "테이블 저장소 (Node.js) aaaWeb 앱 | Microsoft Docs"
description: "Azure 저장소 서비스와 hello Azure 모듈을 추가 하 여 Express 자습서와 함께 hello 웹 앱에 구축 하는 자습서입니다."
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
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="bcfab-103">저장소를 사용하는 Node.js 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bcfab-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="bcfab-104">개요</span><span class="sxs-lookup"><span data-stu-id="bcfab-104">Overview</span></span>
<span data-ttu-id="bcfab-105">이 자습서에서 만든 응용 프로그램을 hello는 [Express를 사용 하 여 Node.js 웹 응용 프로그램] 자습서 hello Microsoft Azure 클라이언트 라이브러리를 사용 하 여 데이터 관리 서비스와 Node.js toowork에 대 한 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="bcfab-106">TooAzure를 배포할 수 있음을 작업 목록-웹 기반 응용 프로그램을 만들어 응용 프로그램을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="bcfab-107">hello 작업 목록에는 작업을 검색, 새 작업 추가 및 작업을 완료로 표시 하려면 사용자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="bcfab-108">hello 작업 항목은 Azure 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="bcfab-109">Azure 저장소는 내결함성과 고가용성이 있는 구조화되지 않은 데이터 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="bcfab-110">Azure Storage에는 데이터를 저장 및 액세스할 수 있는 몇 가지 데이터 구조가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="bcfab-111">Hello 저장소 서비스 REST Api를 통해 또는 Node.js 용 Azure SDK hello에 포함 된 Api hello에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="bcfab-112">자세한 내용은 [Azure에 데이터 저장 및 액세스]를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcfab-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="bcfab-113">이 자습서에서는 hello 완료 한 것으로 가정 [Node.js 웹 응용 프로그램] 및 [빠른 Node.js][Express를 사용 하 여 Node.js 웹 응용 프로그램] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="bcfab-114">다음 정보는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-114">It contains hello following information:</span></span>

* <span data-ttu-id="bcfab-115">방법으로 toowork hello Jade 템플릿 엔진</span><span class="sxs-lookup"><span data-stu-id="bcfab-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="bcfab-116">어떻게 toowork Azure 데이터 관리 서비스</span><span class="sxs-lookup"><span data-stu-id="bcfab-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="bcfab-117">다음 스크린 샷 hello 완료 hello 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-117">hello following screenshot shows hello completed application:</span></span>

![hello는 internet explorer에서 웹 페이지를 완료합니다.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="bcfab-119">Web.Config에서 저장소 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="bcfab-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="bcfab-120">저장소 자격 증명 tooaccess Azure 저장소에에서 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="bcfab-121">이 hello web.config 응용 프로그램 설정을 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="bcfab-122">hello Azure SDK에서 다음에 읽기 환경 변수 tooNode 변수로 hello web.config 설정은 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="bcfab-123">저장소 자격 증명 hello 응용 프로그램이 배포 된 tooAzure 때에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="bcfab-124">Hello 에뮬레이터에서 실행할 경우 hello 응용 프로그램 hello 저장소 에뮬레이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="bcfab-125">Hello 단계 tooretrieve hello 저장소 계정 자격 증명에 다음을 수행 하 고 toohello web.config 설정 추가:</span><span class="sxs-lookup"><span data-stu-id="bcfab-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="bcfab-126">열려 있지 않으면 hello에서 hello Azure PowerShell을 시작 **시작** 메뉴를 확장 하 여 **모든 프로그램, Azure**를 마우스 오른쪽 단추로 클릭 **Azure PowerShell**를 선택한 후  **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="bcfab-127">응용 프로그램을 포함 하는 디렉터리 toohello 폴더를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="bcfab-128">예를 들어 C:\\node\\tasklist\\WebRole1로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="bcfab-129">Hello Azure Powershell 창에서 다음 cmdlet tooretrieve hello 저장소 계정 정보 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="bcfab-130">hello 위의 cmdlet hello의 목록을 검색 저장소 계정 및 호스팅된 서비스와 연결 된 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bcfab-131">Hello Azure SDK는 한 서비스를 배포할 때 저장소 계정을 만듭니다, 이후 hello 이전 가이드에서 응용 프로그램 배포에서 저장소 계정은 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="bcfab-132">열기 hello **ServiceDefinition.csdef** hello 응용 프로그램은 배포 된 tooAzure 때 사용 되는 hello 환경 설정이 포함 된 파일:</span><span class="sxs-lookup"><span data-stu-id="bcfab-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="bcfab-133">삽입 hello 다음에서 차단 **환경** 요소를 대체 {저장소 계정} 및 {저장소 액세스 키} hello 계정 이름 및 배포에 대 한 toouse 원하는 hello 저장소 계정에 대 한 기본 키 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="bcfab-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![hello web.cloud.config 파일 내용](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="bcfab-135">Hello 파일을 저장 하 고 메모장을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="bcfab-136">추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="bcfab-136">Install additional modules</span></span>
1. <span data-ttu-id="bcfab-137">사용 하 여 hello 다음 명령 tooinstall hello [azure], [노드-uuid] [nconf] 및 [비동기] 모듈 로컬로 뿐 toosave 항목을 toohello **package.json** 파일:</span><span class="sxs-lookup"><span data-stu-id="bcfab-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="bcfab-138">이 명령의 출력 hello 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-138">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="bcfab-139">Node 응용 프로그램의 hello 테이블 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="bcfab-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="bcfab-140">이 섹션에서는 hello hello에서 만든 기본 응용 프로그램 **express** 명령을 추가 하 여 확장 되는 **task.js** 작업에 대 한 hello 모델이 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="bcfab-141">Hello 기존 수정 **app.js** 파일을 새 **tasklist.js** hello 모델을 사용 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="bcfab-142">Hello 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="bcfab-142">Create hello model</span></span>
1. <span data-ttu-id="bcfab-143">Hello에 **WebRole1** 디렉터리 라는 새 디렉터리를 만들고 **모델**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="bcfab-144">Hello에 **모델** 디렉터리 라는 새 파일을 만들어 **task.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="bcfab-145">이 파일에는 응용 프로그램에서 만든 hello 작업에 대 한 hello 모델이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="bcfab-146">Hello hello 시작 시 **task.js** 파일에서 다음 코드는 데 필요한 tooreference 라이브러리 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="bcfab-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="bcfab-147">다음으로 코드 toodefine 추가 hello (Task) 개체를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="bcfab-148">hello (Task) 개체는 toohello 테이블을 연결 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-148">hello Task object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="bcfab-149">다음에 추가 코드 toodefine 추가 방법에 나오는 hello 작업 개체에 hello hello 테이블에 저장 된 데이터와의 상호 작용 허용:</span><span class="sxs-lookup"><span data-stu-id="bcfab-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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
        // use entityGenerator tooset types
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

6. <span data-ttu-id="bcfab-150">저장 후 닫기 hello **task.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="bcfab-151">Hello 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="bcfab-151">Create hello controller</span></span>
1. <span data-ttu-id="bcfab-152">Hello에 **WebRole1/경로** 디렉터리 라는 새 파일을 만들어 **tasklist.js** 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="bcfab-153">추가 코드를 너무 다음 hello**tasklist.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="bcfab-154">이 코드를 azure hello 및에서 사용 되는 비동기 모듈 로드 **tasklist.js** hello 정의 **TaskList \ / s** hello의 인스턴스를 전달 되는 함수 **작업** म 개체 앞에서 정의한:</span><span class="sxs-lookup"><span data-stu-id="bcfab-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="bcfab-155">계속 해 서 추가 toohello **tasklist.js** 너무 hello 메서드를 추가 하 여 파일**showTasks**, **addTask**, 및 **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="bcfab-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="bcfab-156">Hello 저장 **tasklist.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="bcfab-157">app.js 수정</span><span class="sxs-lookup"><span data-stu-id="bcfab-157">Modify app.js</span></span>
1. <span data-ttu-id="bcfab-158">Hello에 **WebRole1** 디렉터리, 열기 hello **app.js** 파일 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="bcfab-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="bcfab-159">Hello 파일 시작 부분의 hello, hello 다음 tooload hello azure 모듈을 추가 하 고 hello 테이블 이름과 파티션 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="bcfab-160">표시 toowhere 아래로 스크롤하여 hello app.js 파일에 다음 줄 hello:</span><span class="sxs-lookup"><span data-stu-id="bcfab-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="bcfab-161">Hello 줄 앞에 오는 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="bcfab-162">이 코드의 인스턴스를 초기화 합니다. <strong>작업</strong> 연결 tooyour 스토리지 계정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="bcfab-163">hello <strong>작업</strong> toohello 전달 <strong>TaskList \ / s</strong>를 사용 하는 것 toocommunicate hello 테이블 서비스:</span><span class="sxs-lookup"><span data-stu-id="bcfab-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="bcfab-164">Hello 저장 **app.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="bcfab-165">Hello 인덱스 뷰를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-165">Modify hello index view</span></span>
1. <span data-ttu-id="bcfab-166">디렉터리 toohello 변경 **뷰** 디렉터리 및 오픈 hello **index.jade** 파일 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="bcfab-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="bcfab-167">Hello hello 내용 바꾸기 **index.jade** 코드 다음 hello로는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="bcfab-168">이 코드는 기존 작업을 표시 하기 위한 hello 뷰를 정의 하 고 새 작업 추가 및 기존 세션을 완료 된 것으로 표시 하기 위한 양식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="bcfab-169">**index.jade** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="bcfab-170">Hello 글로벌 레이아웃 수정</span><span class="sxs-lookup"><span data-stu-id="bcfab-170">Modify hello global layout</span></span>
<span data-ttu-id="bcfab-171">hello **layout.jade** hello에 대 한 파일 **뷰** 디렉터리는 기본 서식 파일의 다른 사용 **.jade** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="bcfab-172">이 단계에서 수정 hello **layout.jade** toouse 파일 [Twitter 부트스트랩](https://github.com/twbs/bootstrap), 변수인 쉽게 toodesign 좋은 찾고 웹 사이트를 사용 하면 하는 도구 키트입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="bcfab-173">다운로드 하 고 hello 파일에 대 한 추출 [Twitter 부트스트랩](http://getbootstrap.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="bcfab-174">복사 hello **bootstrap.min.css** hello에서 파일 **부트스트랩\\dist\\css** 폴더 toohello **공용\\스타일 시트** tasklist \ / s 응용 프로그램의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="bcfab-175">Hello에서 **뷰** 폴더, 열기 hello **layout.jade** 텍스트 편집기에서 파일을 hello 내용을 hello 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="bcfab-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="bcfab-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="bcfab-177">Hello 저장 **layout.jade** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="bcfab-178">Hello 에뮬레이터의에서 hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="bcfab-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="bcfab-179">Hello 명령 toostart hello 응용 프로그램 hello 에뮬레이터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="bcfab-180">hello 브라우저가 열리고 hello 페이지 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-180">hello browser opens and displays hello following page:</span></span>

![웹 페이지 제목 내 작업 목록에 tooadd 작업 및 필드를 포함 하는 테이블에 새 작업 있습니다.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="bcfab-182">Hello 양식 tooadd 항목을 사용 하거나 완료 된 것으로 표시 하 여 기존 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="bcfab-183">게시 hello 응용 프로그램 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bcfab-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="bcfab-184">Hello Windows PowerShell 창에서 다음 cmdlet tooredeploy hello 호스팅된 서비스 tooAzure 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="bcfab-185">**myuniquename**을 이 응용 프로그램의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="bcfab-186">대체 **datacentername** Azure 데이터 센터의 hello 이름으로 같은 **West US**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="bcfab-187">Hello 배포가 완료 된 후 응답 비슷한 toohello 다음을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="bcfab-188">Hello를 지정 하 여 **-시작** hello 이전 cmdlet에서 hello 브라우저 옵션 열리고 게시가 완료 되 면 Azure에서 실행 중인 응용 프로그램을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Hello 내 작업 목록 페이지를 표시 하는 브라우저 창입니다.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="bcfab-191">응용 프로그램 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="bcfab-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="bcfab-192">응용 프로그램을 배포한 후 toodisable 비용이 발생 하지 않도록 또는 빌드 및 hello 내의 다른 응용 프로그램을 배포할 수 있도록 무료로 평가판 기간을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="bcfab-193">Azure는 사용된 서버 시간의 시간당 웹 역할 인스턴스 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="bcfab-194">서버 시간 인스턴스를 실행 하지 않는 중지 하는 hello 상태에 놓인 경우에 응용 프로그램을 배포한 후에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="bcfab-195">hello 다음 단계 방법을 보여 줍니다 toostop 및 응용 프로그램을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="bcfab-196">Hello Windows PowerShell 창에서 cmdlet 뒤 hello를 사용 하 여 hello 이전 섹션에서 만든 hello 서비스 배포를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="bcfab-197">Hello 서비스를 중지 하면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="bcfab-198">Hello 서비스가 중지 되 면이 중지 되었음을 나타내는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="bcfab-199">cmdlet을 다음 호출 hello toodelete hello 서비스:</span><span class="sxs-lookup"><span data-stu-id="bcfab-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="bcfab-200">메시지가 표시 되 면 입력 **Y** toodelete hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="bcfab-201">Hello 서비스를 삭제 하면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="bcfab-202">Hello 서비스가 삭제 된 후 hello 서비스가 삭제 되었거나 메시지가 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcfab-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[Express를 사용 하 여 Node.js 웹 응용 프로그램]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Azure에 데이터 저장 및 액세스]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js 웹 응용 프로그램]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


