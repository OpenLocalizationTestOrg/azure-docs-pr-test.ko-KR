---
title: "테이블 저장소 (Node.js) aaaWeb 앱 | Microsoft Docs"
description: "Azure 저장소 서비스와 hello Azure 모듈을 추가 하 여 Express 자습서와 함께 hello 웹 앱에 구축 하는 자습서입니다."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a>저장소를 사용하는 Node.js 웹 응용 프로그램
## <a name="overview"></a>개요
이 자습서에서 만든 hello 응용 프로그램을 확장 합니다는 [Express를 사용 하 여 Node.js 웹 응용 프로그램] Node.js toowork 데이터 관리 서비스에 대 한 hello Microsoft Azure 클라이언트 라이브러리를 사용 하 여 자습서입니다. 응용 프로그램 toocreate tooAzure를 배포할 수는 작업 목록-웹 기반 응용 프로그램을 확장 합니다. hello 작업 목록에는 작업을 검색, 새 작업 추가 및 작업을 완료로 표시 하려면 사용자 수 있습니다.

hello 작업 항목은 Azure 저장소에 저장 됩니다. Azure 저장소는 내결함성과 고가용성이 있는 구조화되지 않은 데이터 저장소를 제공합니다. Azure 저장소에 저장할 수 있습니다 하 고 데이터에 액세스 하 고 hello 저장소 서비스 REST Api를 통해 또는 Node.js 용 Azure SDK hello에 포함 된 Api hello에서 활용할 수 있는 몇 가지 데이터 구조에 포함 됩니다. 자세한 내용은 [Azure에 데이터 저장 및 액세스]를 참조하십시오.

이 자습서에서는 hello 완료 한 것으로 가정 [Node.js 웹 응용 프로그램] 및 [빠른 Node.js][Express를 사용 하 여 Node.js 웹 응용 프로그램] 자습서입니다.

다음 내용을 배웁니다.

* 방법으로 toowork hello Jade 템플릿 엔진
* 어떻게 toowork Azure 데이터 관리 서비스

완료 하는 hello 응용 프로그램의 스크린샷을 다음과 같습니다.

![hello는 internet explorer에서 웹 페이지를 완료합니다.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Web.Config에서 저장소 자격 증명 설정
Azure 저장소 tooaccess toopass 저장소 자격 증명에 필요합니다. toodo이 web.config 응용 프로그램 설정을 사용 합니다.
이러한 설정은 다음 hello Azure SDK가 읽는 환경 변수 tooNode로 전달 됩니다.

> [!NOTE]
> 저장소 자격 증명 hello 응용 프로그램이 배포 된 tooAzure 때에 사용 됩니다. Hello 에뮬레이터에서 실행할 때는 hello 응용 hello 저장소 에뮬레이터를 사용 합니다.
>
>

Hello 단계 tooretrieve hello 저장소 계정 자격 증명에 다음을 수행 하 고 toohello web.config 설정 추가:

1. 열려 있지 않으면 hello에서 hello Azure PowerShell을 시작 **시작** 메뉴를 확장 하 여 **모든 프로그램, Azure**를 마우스 오른쪽 단추로 클릭 **Azure PowerShell**를 선택한 후  **관리자 권한으로 실행**합니다.
2. 응용 프로그램을 포함 하는 디렉터리 toohello 폴더를 변경 합니다. 예를 들어 C:\\node\\tasklist\\WebRole1로 변경합니다.
3. Hello Azure Powershell 창에서 다음 cmdlet tooretrieve hello 저장소 계정 정보 hello를 입력 합니다.

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   이 저장소 계정 및 계정 키 호스팅된 서비스와 연결 된 hello 목록을 검색 합니다.

   > [!NOTE]
   > Hello Azure SDK는 한 서비스를 배포할 때 저장소 계정을 만듭니다, 이후 hello 이전 가이드에서 응용 프로그램 배포에서 저장소 계정은 이미 있어야 합니다.
   >
   >
4. 열기 hello **ServiceDefinition.csdef** hello 응용 프로그램은 배포 된 tooAzure 때 사용 되는 hello 환경 설정이 포함 된 파일:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. 삽입 hello 다음에서 차단 **환경** 요소를 대체 {저장소 계정} 및 {저장소 액세스 키} hello 계정 이름 및 배포에 대 한 toouse 원하는 hello 저장소 계정에 대 한 기본 키 hello 사용:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![hello web.cloud.config 파일 내용](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. Hello 파일을 저장 하 고 메모장을 닫습니다.

### <a name="install-additional-modules"></a>추가 모듈 설치
1. 사용 하 여 hello 다음 명령 tooinstall hello [azure], [노드-uuid] [nconf] 및 [비동기] 모듈 로컬로 뿐 toosave 항목을 toohello **package.json** 파일:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  이 명령의 출력 hello 비슷한 toohello 다음과 같아야 합니다.

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

## <a name="using-hello-table-service-in-a-node-application"></a>Node 응용 프로그램의 hello 테이블 서비스 사용
이 섹션의 hello에서 만든 hello 기본 응용 프로그램을 확장 합니다 **express** 명령을 추가 하 여 한 **task.js** hello 모델 작업에 대해 포함 된 파일입니다. Hello 기존 수정 합니다 **app.js** 을 새로 만듭니다 **tasklist.js** hello 모델을 사용 하는 파일입니다.

### <a name="create-hello-model"></a>Hello 모델 만들기
1. Hello에 **WebRole1** 디렉터리 라는 새 디렉터리를 만들고 **모델**합니다.
2. Hello에 **모델** 디렉터리 라는 새 파일을 만들어 **task.js**합니다. 이 파일은 응용 프로그램에서 만든 hello 작업에 대 한 hello 모델을 포함 합니다.
3. Hello hello 시작 시 **task.js** 파일에서 다음 코드는 데 필요한 tooreference 라이브러리 hello 추가:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. 다음으로 코드 toodefine를 추가 하 고 hello (Task) 개체를 내보냅니다. 이 개체는 toohello 테이블을 연결 하는 일을 담당 합니다.

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

5. 다음에 추가 코드 toodefine 추가 방법에 나오는 hello 작업 개체에 hello hello 테이블에 저장 된 데이터와의 상호 작용 허용:

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

6. 저장 후 닫기 hello **task.js** 파일입니다.

### <a name="create-hello-controller"></a>Hello 컨트롤러 만들기
1. Hello에 **WebRole1/경로** 디렉터리 라는 새 파일을 만들어 **tasklist.js** 텍스트 편집기에서 엽니다.
2. 추가 코드를 너무 다음 hello**tasklist.js**합니다. 사용 되는 hello azure와 비동기 모듈 로드 **tasklist.js**합니다. Hello 정의 **TaskList \ / s** hello의 인스턴스를 전달 되는 함수 **작업** 앞에서 정의한 개체:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. 계속 해 서 추가 toohello **tasklist.js** 너무 hello 메서드를 추가 하 여 파일**showTasks**, **addTask**, 및 **completeTasks**:

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

4. Hello 저장 **tasklist.js** 파일입니다.

### <a name="modify-appjs"></a>app.js 수정
1. Hello에 **WebRole1** 디렉터리, 열기 hello **app.js** 파일 텍스트 편집기에서.
2. Hello 파일 시작 부분의 hello, hello 다음 tooload hello azure 모듈을 추가 하 고 hello 테이블 이름과 파티션 키를 설정 합니다.

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. 표시 toowhere 아래로 스크롤하여 hello app.js 파일에 다음 줄 hello:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    아래 표시 된 hello 코드 줄 위에 hello를 바꿉니다. 인스턴스를 초기화 합니다이 <strong>작업</strong> 연결 tooyour 스토리지 계정으로 합니다. 이 toohello 전달 되어 <strong>TaskList \ / s</strong>를 사용 하 여 toocommunicate 테이블 서비스 hello로:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Hello 저장 **app.js** 파일입니다.

### <a name="modify-hello-index-view"></a>Hello 인덱스 뷰를 수정 합니다.
1. 디렉터리 toohello 변경 **뷰** 디렉터리 및 오픈 hello **index.jade** 파일 텍스트 편집기에서.
2. Hello hello 내용 바꾸기 **index.jade** 아래 hello 코드가 포함 된 파일입니다. 새 작업을 추가 하 고 완료 된 것으로 기존 관계를 표시 하는 양식 뿐만 아니라 기존 작업을 표시 하기 위한 hello 뷰를 정의 합니다.

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

3. **index.jade** 파일을 저장하고 닫습니다.

### <a name="modify-hello-global-layout"></a>Hello 글로벌 레이아웃 수정
hello **layout.jade** hello에 대 한 파일 **뷰** 디렉터리는 기본 서식 파일의 다른 사용 **.jade** 파일입니다. 이 단계에서 수정 toouse [Twitter 부트스트랩](https://github.com/twbs/bootstrap)는 쉽게 toodesign 좋은 찾고 웹 사이트를 사용 하면 하는 도구 키트입니다.

1. 다운로드 하 고 hello 파일에 대 한 추출 [Twitter 부트스트랩](http://getbootstrap.com/)합니다. 복사 hello **bootstrap.min.css** hello에서 파일 **부트스트랩\\dist\\css** 폴더 toohello **공용\\스타일 시트** tasklist \ / s 응용 프로그램의 디렉터리입니다.
2. Hello에서 **뷰** 폴더, 열기 hello **layout.jade** hello 다음과 같이 프로그램 텍스트 편집기 및 바꾸기 hello 내용에서:

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. Hello 저장 **layout.jade** 파일입니다.

### <a name="running-hello-application-in-hello-emulator"></a>Hello 에뮬레이터의에서 hello 응용 프로그램 실행
Hello 명령 toostart hello 응용 프로그램 hello 에뮬레이터에서 다음을 사용 합니다.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

hello 브라우저 열리고 hello 페이지 뒤에 표시 됩니다.

![웹 페이지 제목 내 작업 목록에 tooadd 작업 및 필드를 포함 하는 테이블에 새 작업 있습니다.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

Hello 양식 tooadd 항목을 사용 하거나 완료 된 것으로 표시 하 여 기존 항목을 제거 합니다.

## <a name="publishing-hello-application-tooazure"></a>게시 hello 응용 프로그램 tooAzure
Hello Windows PowerShell 창에서 다음 cmdlet tooredeploy hello 호스팅된 서비스 tooAzure 호출 합니다.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

**myuniquename**을 이 응용 프로그램의 고유한 이름으로 바꿉니다. 대체 **datacentername** Azure 데이터 센터의 hello 이름으로 같은 **West US**합니다.

Hello 배포가 완료 된 후 응답 비슷한 toohello 다음을 표시 되어야 합니다.

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

이전 처럼 hello 지정 했기 때문에 **-시작** 옵션을 hello 브라우저가 열리고 게시가 완료 되 면 Azure에서 실행 중인 응용 프로그램을 표시 합니다.

![Hello 내 작업 목록 페이지를 표시 하는 브라우저 창입니다. hello URL hello 페이지 이제 Azure에서 호스팅됨을 나타냅니다.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>응용 프로그램 중지 및 삭제
응용 프로그램을 배포한 후 toodisable 비용이 발생 하지 않도록 또는 빌드 및 hello 내의 다른 응용 프로그램을 배포할 수 있도록 무료로 평가판 기간을 할 수 있습니다.

Azure는 사용된 서버 시간의 시간당 웹 역할 인스턴스 요금을 청구합니다.
서버 시간 인스턴스를 실행 하지 않는 중지 하는 hello 상태에 놓인 경우에 응용 프로그램을 배포한 후에 사용 됩니다.

hello 다음 단계 방법을 보여 줍니다 toostop 및 응용 프로그램을 삭제 합니다.

1. Hello Windows PowerShell 창에서 cmdlet 뒤 hello를 사용 하 여 hello 이전 섹션에서 만든 hello 서비스 배포를 중지 합니다.

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Hello 서비스를 중지 하면 몇 분 정도 걸릴 수 있습니다. Hello 서비스가 중지 되 면이 중지 되었음을 나타내는 메시지가 나타납니다.

2. cmdlet을 다음 호출 hello toodelete hello 서비스:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   메시지가 표시 되 면 입력 **Y** toodelete hello 서비스입니다.

   Hello 서비스를 삭제 하면 몇 분 정도 걸릴 수 있습니다. Hello 서비스를 삭제 한 후에 hello 서비스가 삭제 되었거나를 나타내는 메시지가 표시 됩니다.

[Express를 사용 하 여 Node.js 웹 응용 프로그램]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Azure에 데이터 저장 및 액세스]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js 웹 응용 프로그램]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


