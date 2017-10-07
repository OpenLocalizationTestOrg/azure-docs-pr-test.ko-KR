---
title: "평균 aaaCreate Azure에서 Linux VM에 대 한 스택 | Microsoft Docs"
description: "Azure에서 Linux VM의 스택 toocreate는 MongoDB, Express, AngularJS 및 Node.js (평균)에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Azure의 Linux VM에서 MEAN(MongoDB, Express, AngularJS 및 Node.js) 스택 만들기

이 자습서에서는 Azure에서 Linux VM의 스택 tooimplement는 MongoDB, Express, AngularJS 및 Node.js (평균). 만들면 hello 평균 스택 추가, 삭제 및 나열 하는 데이터베이스에 있는 책 수 있습니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Linux VM 만들기
> * Node.js 설치
> * MongoDB를 설치 하 고 hello 서버 설정
> * Express를 설치 하 고 경로 toohello 서버 설정
> * AngularJS와 액세스 hello 경로
> * Hello 응용 프로그램 실행

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.


## <a name="create-a-linux-vm"></a>Linux VM 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) hello로 Linux VM을 만들고 명령을 [az vm 만들기](https://docs.microsoft.com/cli/azure/vm#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.

hello 다음 예제에서는 리소스 그룹 이름이 hello Azure CLI toocreate *myResourceGroupMEAN* hello에 *eastus* 위치 합니다. 또한 기본 키 위치에 SSH 키가 없는 경우 SSH 키가 있는 *myVM*이라는 VM이 만들어집니다. toouse 특정 키를 사용 하 여 hello-ssh 키-값 옵션의 집합입니다.

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

Hello VM을 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다. 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
Hello를 메모해 `publicIpAddress`합니다. 이 주소는 사용 되는 tooaccess hello VM입니다.

사용 하 여 hello 다음 명령은 VM hello로 SSH 세션 toocreate 합니다. Toouse hello 올바른 공용 IP 주소가 있는지 확인 합니다. 위 예제에서 IP 주소는 13.72.77.9입니다.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Node.js 설치

[Node.js](https://nodejs.org/en/)는 Chrome의 V8 JavaScript 엔진을 기준으로 하는 JavaScript 런타임입니다. Node.js는 Express 경로 hello 및 AngularJS 컨트롤러를이 자습서 tooset에 사용 됩니다.

Hello, SSH를 사용 하 여 열린 hello bash 셸의 사용 하 여 VM에서 Node.js를 설치 합니다.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>MongoDB를 설치 하 고 hello 서버 설정
[MongoDB](http://www.mongodb.com)는 유연한 JSON 유사 문서에 데이터를 저장합니다. 문서 toodocument에서 다양 한 데이터베이스의 필드 및 데이터 구조는 시간이 지남에 따라 변경 될 수 있습니다. 이 예제에서는 응용 프로그램에 대 한 책 이름, isbn 번호, 작성자 및 페이지 수를 포함 하는 책 레코드 tooMongoDB 추가 됩니다. 

1. Hello, SSH를 사용 하 여 열린 hello bash 셸의 사용 하 여 VM에서 hello MongoDB 키로 설정 합니다.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Hello 키로 hello 패키지 관리자를 업데이트 합니다.
  
    ```bash
    sudo apt-get update
    ```

3. MongoDB를 설치합니다.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Hello 서버를 시작 합니다.

    ```bash
    sudo service mongodb start
    ```

5. 또한 tooinstall hello 필요 [본문 파서](https://www.npmjs.com/package/body-parser-json) 패키지 toohelp us 처리 hello JSON 요청 toohello 서버에 전달 합니다.

    Hello npm 패키지 관리자를 설치 합니다.

    ```bash
    sudo apt-get install npm
    ```

    Hello 본문 파서 패키지를 설치 합니다.
    
    ```bash
    sudo npm install body-parser
    ```

6. 라는 폴더를 만듭니다 *설명서* 라는 파일 tooit 추가 *server.js* hello 웹 서버에 대 한 hello 구성을 포함 하 합니다.

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a>Express를 설치 하 고 경로 toohello 서버 설정

[Express](https://expressjs.com)는 웹 및 모바일 응용 프로그램용 기능을 제공하는 유연한 최소 규모의 Node.js 웹 응용 프로그램 프레임워크입니다. MongoDB 데이터베이스에서이 자습서 toopass 책 정보 tooand에 빠른 사용 됩니다. [Mongoose](http://mongoosejs.com) 직접적인 스키마 기반 솔루션 toomodel 응용 프로그램 데이터를 제공 합니다. 이 자습서 tooprovide mongoose는 hello 데이터베이스에 대 한 책 스키마입니다.

1. Express 및 Mongoose를 설치합니다.

    ```bash
    sudo npm install express mongoose
    ```

2. Hello에 *설명서* 폴더를 라는 폴더를 만듭니다 *앱* 라는 파일 *routes.js* hello로 express 경로 정의 합니다.

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. Hello에 *앱* 폴더 라는 폴더를 만듭니다 *모델* 라는 파일 *book.js* hello 책 모델 구성을 정의 합니다.  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a>AngularJS와 액세스 hello 경로

[AngularJS](https://angularjs.org)는 웹 응용 프로그램에서 동적 뷰를 만들기 위한 웹 프레임워크를 제공합니다. 이 자습서에서는 빠른 AngularJS tooconnect 품질 웹 페이지를 사용 하 고 책 데이터베이스에서 작업을 수행 합니다.

1. Hello 디렉터리를 백업에 변경*설명서* (`cd ../..`), 다음 라는 폴더를 만듭니다 *공용* 라는 파일 *script.js* hello 컨트롤러와 정의 된 구성입니다.

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. Hello에 *공용* 폴더를 라는 파일을 만들어 *index.html* 된 hello 웹 페이지를 정의 합니다.

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a>Hello 응용 프로그램 실행

1. Hello 디렉터리를 백업에 변경*설명서* (`cd ..`)이이 명령을 실행 하 여 hello 서버를 시작 합니다.

    ```bash
    nodejs server.js
    ```

2. 웹 브라우저 toohello 주소를 hello VM에 대해 기록를 엽니다. 예: *http://13.72.77.9:3300*. 다음 페이지는 hello와 같은 나타나야 합니다.

    ![책 레코드](media/tutorial-mean/meanstack-init.png)

3. Hello 텍스트 상자에 데이터를 입력 하 고 클릭 **추가**합니다. 예:

    ![책 레코드 추가](media/tutorial-mean/meanstack-add.png)

4. Hello 페이지를 새로 고친 후 다음과 같이이 페이지를 표시 됩니다.

    ![책 레코드 나열](media/tutorial-mean/meanstack-list.png)

5. 누르면 **삭제** hello 데이터베이스에서 hello 책 레코드를 제거 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Linux VM에 대해 MEAN 스택을 사용하여 책 레코드를 추적하는 웹 응용 프로그램을 만들었습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Linux VM 만들기
> * Node.js 설치
> * MongoDB를 설치 하 고 hello 서버 설정
> * Express를 설치 하 고 경로 toohello 서버 설정
> * AngularJS와 액세스 hello 경로
> * Hello 응용 프로그램 실행

다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.

> [!div class="nextstepaction"]
> [SSL로 웹 서버 보안](tutorial-secure-web-server.md)
