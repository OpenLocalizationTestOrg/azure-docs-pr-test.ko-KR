---
title: "hello Azure 테이블 서비스를 사용 하 여 aaaNode.js 웹 앱"
description: "이 자습서는 toouse hello Azure 테이블 Azure 앱 서비스 웹 앱에서 호스팅되는 Node.js 응용 프로그램에서 toostore 데이터를 서비스 하는 방법을 배웁니다."
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
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Hello Azure 테이블 서비스를 사용 하 여 Node.js 웹 응용 프로그램
## <a name="overview"></a>개요
이 자습서에서는 테이블 서비스 toouse toostore 및 액세스 데이터를 Azure 데이터 관리에서 제공 하는 방법을 [노드] 응용 프로그램에서 호스트 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 웹 앱입니다. 이 자습서에서는 이전에 node 및 [Git]를 사용한 경험이 있다고 가정합니다.

다음 내용을 배웁니다.

* Toouse npm (노드 패키지 관리자) tooinstall 노드 모듈 hello 하는 방법
* 방법으로 toowork hello Azure 테이블 서비스
* 어떻게 toouse 웹 앱 Azure CLI toocreate를 hello 합니다.

이 자습서를 따라 작업을 만들고, 검색하고, 완료할 수 있는 간단한 웹 기반 "할 일 모음" 응용프로그램을 구축합니다. hello 작업 hello 테이블 서비스에에서 저장 됩니다.

다음은 완료 하는 hello 응용 프로그램이입니다.

![빈 tasklist가 표시된 웹 페이지][node-table-finished]

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서의 지침 hello를 수행 하기 전에 hello 다음이 설치 되어 있는지 확인 합니다.

* [노드] 버전 0.10.24 이상
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>저장소 계정 만들기
Azure 저장소 계정 만들기 hello 앱이 계정 toostore hello 할 일 항목을 사용 합니다.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 클릭 **새로** hello 포털의 왼쪽 hello 아래쪽에 아이콘을 클릭 한 다음 **데이터 + 저장소** > **저장소**합니다. Hello 저장소 계정에 고유한 이름을 지정 하 고 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) 것에 대 한 합니다.
   
      ![새 단추](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Hello 저장소 계정이 생성 되 면 hello **알림** 단추가 녹색 깜박입니다 **성공** 블레이드 hello 저장소 계정을 열릴 및 tooshow 속하는지 toohello 새 리소스 그룹 만들어집니다.
3. Hello 저장소 계정의 블레이드에서 클릭 **설정** > **키**합니다. Hello 기본 액세스 키 toohello 클립보드에 복사 합니다.
   
    ![액세스 키][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>모듈 설치 및 스캐폴딩 생성
이 섹션에서는 새 노드 응용 프로그램을 만들고 npm tooadd 모듈 패키지를 사용 합니다. 이 응용 프로그램에 대 한 hello 사용할 [Express] 및 [Azure] 모듈입니다. 노드에 대 한 모델 뷰 컨트롤러 프레임 워크를 제공 하는 hello Express 모듈, Azure 모듈 hello 하는 동안 연결 toohello 테이블 서비스를 제공 합니다.

### <a name="install-express-and-generate-scaffolding"></a>express 설치 및 스캐폴딩 생성
1. Hello 명령줄에서 라는 새 디렉터리를 만들고 **tasklist \ / s** 및 스위치 toothat 디렉터리입니다.  
2. 다음 명령은 tooinstall hello Express 모듈 hello를 입력 합니다.
   
        npm install express-generator@4.2.0 -g
   
    Hello 운영 체제에 따라 tooput 'sudo' hello 명령 전에 할 수 있습니다.
   
        sudo npm install express-generator@4.2.0 -g
   
    hello 출력이 다음 예제와 비슷한 toohello 나타납니다.
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > hello '-g' 매개 변수 hello 모듈을 전역으로 설치 합니다. 사용할 수 이런 방식으로 **express** 추가 경로 정보에 tootype 필요 없이 toogenerate 웹 응용 프로그램 스 캐 폴딩 합니다.
   > 
   > 
3. toocreate hello 스 캐 폴딩 hello 응용 프로그램에 대 한 입력 hello **express** 명령:
   
        express
   
    hello이이 명령의 출력에는 다음 예제와 비슷한 toohello 나타납니다.
   
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
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    이제 몇 가지 새 디렉터리 및 파일 hello에 있는 **tasklist \ / s** 디렉터리입니다.

### <a name="install-additional-modules"></a>추가 모듈 설치
Hello 중 파일을 **express** 만듭니다는 **package.json**합니다. 이 파일에는 모듈 종속성 목록이 포함됩니다. 나중 hello 응용 프로그램 tooApp 서비스 웹 앱을 배포할 때이 파일 모듈 toobe Azure에 설치 해야 확인 합니다.

Hello 명령줄에서 다음 명령 tooinstall hello 모듈 hello에 설명 된 hello 입력 **package.json** 파일입니다. Toouse 'sudo' 할 수 있습니다.

    npm install

hello이이 명령의 출력에는 다음 예제와 비슷한 toohello 나타납니다.

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


다음으로, 다음 명령은 tooinstall hello hello 입력 [azure], [노드 uuid], [nconf] 및 [비동기] 모듈:

    npm install azure-storage node-uuid async nconf --save

hello **-저장** 이러한 모듈 toohello에 대 한 항목을 추가 하는 플래그 **package.json** 파일입니다.

hello이이 명령의 출력에는 다음 예제와 비슷한 toohello 나타납니다.

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기
이제 여러분 준비 toobuild hello 응용 프로그램입니다.

### <a name="create-a-model"></a>모델 만들기
A *모델* 는 hello 응용 프로그램에서 데이터를 나타내는 개체입니다. Hello 응용 프로그램 hello만 모델을 hello 할 일 목록에서 항목을 나타내는 작업 개체입니다. 작업에는 필드 다음 hello를 적용 됩니다.

* PartitionKey
* RowKey
* 이름(문자열)
* 범주(문자열)
* 완료됨(부울)

**PartitionKey** 및 **RowKey** hello 테이블 서비스에 의해 테이블 키로 사용 됩니다. 자세한 내용은 참조 [이해 hello 테이블 서비스 데이터 모델](https://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.

1. Hello에 **tasklist \ / s** 디렉터리 라는 새 디렉터리를 만들고 **모델**합니다.
2. Hello에 **모델** 디렉터리 라는 새 파일을 만들어 **task.js**합니다. 이 파일은 응용 프로그램에서 만든 hello 작업에 대 한 hello 모델을 포함 합니다.
3. Hello hello 시작 시 **task.js** 파일에서 다음 코드는 데 필요한 tooreference 라이브러리 hello 추가:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Hello 다음 toodefine 코드 내보내고 hello (Task) 개체를 추가 합니다. 이 개체는 toohello 테이블을 연결 하는 일을 담당 합니다.
   
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
5. Hello 테이블에 저장 된 데이터와의 상호 작용을 수 있는 hello에 나오는 코드 toodefine 추가 방법에 따라 hello Task 개체를 추가 합니다.
   
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
6. 저장 후 닫기 hello **task.js** 파일입니다.

### <a name="create-a-controller"></a>컨트롤러 만들기
A *컨트롤러* HTTP 요청을 처리 하 고 hello HTML 응답을 렌더링 합니다.

1. Hello에 **tasklist \ / s/경로** 디렉터리 라는 새 파일을 만들어 **tasklist.js** 텍스트 편집기에서 엽니다.
2. 추가 코드를 너무 다음 hello**tasklist.js**합니다. 사용 되는 hello azure와 비동기 모듈 로드 **tasklist.js**합니다. Hello 정의 **TaskList \ / s** hello의 인스턴스를 전달 되는 함수 **작업** 앞에서 정의한 개체:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. **TaskList** 개체를 정의합니다.
   
        function TaskList(task) {
          this.task = task;
        }
4. Hello 너무 메서드를 다음 추가**TaskList \ / s**:
   
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

### <a name="modify-appjs"></a>app.js 수정
1. Hello에서 **tasklist \ / s** 디렉터리, 열기 hello **app.js** 파일입니다. 이 파일 hello를 실행 하 여 앞서 만든 **express** 명령입니다.
2. Hello 파일 시작 부분의 hello, hello tooload hello azure 모듈, 집합 hello 테이블 이름, 파티션 키 및 집합 hello 저장소 자격 증명이이 예제에서 사용 하는 다음을 추가 합니다.
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf hello 구성 값을 로드 하는 환경 변수 또는 hello에서 **config.json** 파일을 나중에 만들어집니다.
   > 
   > 
3. 표시 toowhere 아래로 스크롤하여 hello app.js 파일에 다음 줄 hello:
   
        app.use('/', routes);
        app.use('/users', users);
   
    아래 표시 된 hello 코드 줄 위에 hello를 바꿉니다. 인스턴스를 초기화 합니다이 <strong>작업</strong> 연결 tooyour 스토리지 계정으로 합니다. 이 toohello 전달 되어 <strong>TaskList \ / s</strong>를 사용 하 여 toocommunicate 테이블 서비스 hello로:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Hello 저장 **app.js** 파일입니다.

### <a name="modify-hello-index-view"></a>Hello 인덱스 뷰를 수정 합니다.
1. 열기 hello **tasklist/views/index.jade** 파일 텍스트 편집기에서.
2. Hello 파일의 전체 내용을 hello 코드 다음 hello로 대체 합니다. 이렇게 하면 기존 작업을 표시하는 보기와 새 작업을 추가하고 기존 작업을 완료로 표시하는 양식이 정의됩니다.
   
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
3. **index.jade** 파일을 저장하고 닫습니다.

### <a name="modify-hello-global-layout"></a>Hello 글로벌 레이아웃 수정
hello **layout.jade** hello에 대 한 파일 **뷰** 디렉터리는 다른 전역 서식 **.jade** 파일입니다. 이 단계에서 수정 toouse [Twitter 부트스트랩](https://github.com/twbs/bootstrap), 하는 쉽게 toodesign 좋은 찾고 웹 응용 프로그램에 있도록 하는 도구 키트입니다.

다운로드 하 고 hello 파일에 대 한 추출 [Twitter 부트스트랩](http://getbootstrap.com/)합니다. 복사 hello **bootstrap.min.css** hello 부트스트랩에서에서 파일 **css** hello 폴더 **공개/스타일 시트** 응용 프로그램의 디렉터리입니다.

Hello에서 **뷰** 폴더를 엽니다 **layout.jade** hello 전체 내용을 hello 다음과 같이 바꿉니다.

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

### <a name="create-a-config-file"></a>구성 파일 만들기
toorun hello 로컬로 앱을 Azure 저장소 자격 증명 구성 파일에 포함 합니다. 라는 파일을 만들어 **config.json* * 다음 JSON hello로:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

대체 **저장소 계정 이름** hello 저장소의 hello 이름의 계정이 이전에 만든 및 바꾸기 **저장소 액세스 키** 저장소 계정에 대 한 hello 기본 액세스 키를 가진 합니다. 예:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

이 파일을 저장 *한 디렉터리 수준 높은* hello 보다 **tasklist \ / s** 다음과 같이 디렉터리:

    parent/
      |-- config.json
      |-- tasklist/

hello이 원인은 tooavoid 소스 제어에 hello 구성 파일을 확인 하는 중입니다. 여기서 공개 될 수 있습니다. Hello 앱 tooAzure를 배포에서는 구성 파일 대신 환경 변수 사용 합니다.

## <a name="run-hello-application-locally"></a>Hello 응용 프로그램을 로컬로 실행
로컬 컴퓨터의 tootest hello 응용 hello 다음 단계를 수행 합니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **tasklist \ / s** 디렉터리입니다.
2. 다음 명령은 toolaunch hello 응용 프로그램을 로컬 hello를 사용 합니다.
   
        npm start
3. 웹 브라우저를 열고 toohttp://127.0.0.1:3000 이동 합니다.
   
    다음 예에서는 웹 페이지와 유사한 toohello가 나타납니다.
   
    ![빈 tasklist가 표시된 웹 페이지][node-table-finished]
4. toocreate 할 일 항목을 새 이름 및 범주를 입력 하 고 클릭 **항목 추가**합니다. 
5. toomark 완료 검사 방법으로 작업 **완료** 클릭 **작업 업데이트**합니다.
   
    ![작업의 hello 목록에서 한 hello 새 항목의 이미지][node-table-list-items]

Hello 응용 프로그램을 로컬에서 실행 하는 경우에 것에서 데이터를 저장 hello hello Azure 테이블 서비스에에서 있습니다.

## <a name="deploy-your-application-tooazure"></a>응용 프로그램 tooAzure 배포
이 섹션의 단계 hello hello Azure 명령줄 도구 toocreate 새 웹 앱을 사용 하 여 앱 서비스에서 한 다음 사용할 Git toodeploy 응용 프로그램. tooperform 이러한 단계는 Azure 구독이 있어야 합니다.

> [!NOTE]
> Hello를 사용 하 여 다음이 단계를 수행할 수도 있습니다 [Azure 포털](https://portal.azure.com/)합니다. [Azure 앱 서비스에서 Node.js 웹앱 빌드 및 배포]를 참조하세요.
> 
> 만든 hello 첫 번째 웹 앱의 경우이 응용 프로그램 hello Azure 포털 toodeploy 사용 해야 합니다.
> 
> 

시작 tooget 설치 hello [Azure CLI] hello hello 명령줄에서 다음 명령을 입력 하 여:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>게시 설정 가져오기
이 단계에서는 구독에 대한 정보를 포함하는 파일을 다운로드합니다.

1. Hello 다음 명령을 입력 합니다.
   
        azure login
   
    이 명령은 브라우저를 시작 하 고 toohello 다운로드 페이지를 탐색 합니다. 메시지가 표시 되 면 Azure 구독에 연결 된 hello 계정으로 로그인 합니다.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    hello 파일 다운로드가 자동으로 시작 그렇지 않으면 hello 파일 시작 부분의 hello 페이지 toomanually 다운로드 hello hello 링크를 클릭 합니다. Hello 파일 및 참고 hello 파일 경로 저장 합니다.
2. Hello 명령 tooimport hello 설정을 다음을 입력 합니다.
   
        azure account import <path-to-file>
   
    Hello 이전 단계에서 다운로드 한 설정 파일을 게시 하는 hello hello 경로 파일 이름을 지정 합니다.
3. Hello 설정의 가져온 후 삭제 hello 게시 설정 파일입니다. 이 파일은 더 이상 필요하지 않으며 Azure 구독과 관련된 중요한 정보가 포함됩니다.

### <a name="create-an-app-service-web-app"></a>앱 서비스 웹앱 만들기
1. Hello 명령줄에서 디렉터리 toohello 변경 **tasklist \ / s** 디렉터리입니다.
2. Hello 명령 toocreate 새 웹 앱에 다음을 사용 합니다.
   
        azure site create --git
   
    Hello 웹 응용 프로그램 이름 및 위치를 묻는 메시지가 나타납니다. 고유 이름 및 선택 hello Azure 저장소 계정과 동일한 지리적 위치를 제공 합니다.
   
    hello `--git` 매개 변수 Azure에서이 웹 앱에 대 한 Git 리포지토리를 만듭니다. None 있고에 추가 하는 hello 현재 디렉터리의 Git 리포지토리 초기화는 [Git 원격] 'azure' 명명 된, 즉 사용 되는 toopublish hello 응용 프로그램 tooAzure 합니다. 마지막으로 만듭니다는 **web.config** toohost Azure 노드에 응용 프로그램에서 사용 하는 설정을 포함 하는 파일입니다. Hello를 생략 하면 `--git` 매개 변수는 있지만 hello 디렉터리에 Git 리포지토리, hello 명령은 여전히 'azure' hello 원격을 만듭니다.
   
    이 명령이 완료 되 면 유사한 toohello 다음 출력이 표시 됩니다. 참고로 시작 하는 hello 줄 **웹 사이트에서 만든** hello 웹 앱에 대 한 hello URL을 포함 합니다.
   
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
   > 구독에 대 한 hello 첫 번째 앱 서비스 웹 앱 이면 지시 toouse hello Azure 포털 toocreate hello 웹 앱 됩니다. 자세한 내용은 [Azure 앱 서비스에서 Node.js 웹앱 빌드 및 배포]를 참조하세요.
   > 
   > 

### <a name="set-environment-variables"></a>환경 변수 설정
이 단계에서는 Azure에서 환경 변수 tooyour 웹 응용 프로그램 구성을 추가 합니다.
Hello 명령줄에서 hello 다음을 입력 합니다.

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


대체  **<storage account name>**  hello 저장소의 hello 이름의 계정이 이전에 만든 및 바꾸기  **<storage access key>**  저장소 계정에 대 한 hello 기본 액세스 키를 가진 합니다. (이전에 만든 hello config.json 파일로 hello 값을 사용 합니다.)

또는 hello에서 환경 변수를 설정할 수 [Azure 포털](https://portal.azure.com/):

1. 클릭 하 여 hello 웹 앱 블레이드를 열고 **찾아보기** > **웹 앱** > 웹 응용 프로그램 이름입니다.
2. 웹앱 블레이드에서 **모든 설정** > **응용 프로그램 설정**을 클릭합니다.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Toohello 아래로 스크롤하여 **앱 설정** 섹션 및 hello 키/값 쌍을 추가 합니다.
   
     ![앱 설정](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. **저장**을 클릭합니다.

### <a name="publish-hello-application"></a>Hello 응용 프로그램 게시
toopublish hello 앱 hello 코드 파일 tooGit 커밋하고 tooazure/마스터를 푸시합니다.

1. 배포 자격 증명을 설정합니다.
   
        azure site deployment user set <name> <password>
2. 응용프로그램 파일을 추가 및 커밋합니다.
   
        git add .
        git commit -m "adding files"
3. 밀어넣기 hello 커밋 toohello 앱 서비스 웹 앱:
   
        git push azure master
   
    사용 하 여 **마스터** hello 대상 분기도 합니다. Hello 배포의 hello 끝 다음 예제에서는 문을 비슷한 toohello를 확인할 수 있습니다.
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Hello 푸시 작업이 완료 되 면 hello 이전에 반환한 toohello 웹 앱 URL을 찾아보기 `azure create site` tooview 응용 프로그램 명령입니다.

## <a name="next-steps"></a>다음 단계
이 문서의 단계 hello hello 테이블 서비스 toostore 정보를 사용 하 여 데이터를 설명 하지만 사용할 수도 있습니다 [MongoDB](https://mlab.com/azure/)합니다. 

## <a name="additional-resources"></a>추가 리소스
[Azure CLI]

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[Azure 앱 서비스에서 Node.js 웹앱 빌드 및 배포]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[노드]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git 원격]: http://git-scm.com/docs/git-remote

[Azure CLI]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[노드 uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[비동기]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
