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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="957a8-103">Azure의 Linux VM에서 MEAN(MongoDB, Express, AngularJS 및 Node.js) 스택 만들기</span><span class="sxs-lookup"><span data-stu-id="957a8-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="957a8-104">이 자습서에서는 Azure에서 Linux VM의 스택 tooimplement는 MongoDB, Express, AngularJS 및 Node.js (평균).</span><span class="sxs-lookup"><span data-stu-id="957a8-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="957a8-105">만들면 hello 평균 스택 추가, 삭제 및 나열 하는 데이터베이스에 있는 책 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="957a8-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="957a8-107">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="957a8-107">Create a Linux VM</span></span>
> * <span data-ttu-id="957a8-108">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="957a8-108">Install Node.js</span></span>
> * <span data-ttu-id="957a8-109">MongoDB를 설치 하 고 hello 서버 설정</span><span class="sxs-lookup"><span data-stu-id="957a8-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="957a8-110">Express를 설치 하 고 경로 toohello 서버 설정</span><span class="sxs-lookup"><span data-stu-id="957a8-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="957a8-111">AngularJS와 액세스 hello 경로</span><span class="sxs-lookup"><span data-stu-id="957a8-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="957a8-112">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="957a8-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="957a8-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="957a8-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="957a8-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="957a8-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="957a8-116">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="957a8-116">Create a Linux VM</span></span>

<span data-ttu-id="957a8-117">Hello로 리소스 그룹 만들기 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) hello로 Linux VM을 만들고 명령을 [az vm 만들기](https://docs.microsoft.com/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="957a8-118">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="957a8-119">hello 다음 예제에서는 리소스 그룹 이름이 hello Azure CLI toocreate *myResourceGroupMEAN* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="957a8-120">또한 기본 키 위치에 SSH 키가 없는 경우 SSH 키가 있는 *myVM*이라는 VM이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="957a8-121">toouse 특정 키를 사용 하 여 hello-ssh 키-값 옵션의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

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

<span data-ttu-id="957a8-122">Hello VM을 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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
<span data-ttu-id="957a8-123">Hello를 메모해 `publicIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="957a8-124">이 주소는 사용 되는 tooaccess hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="957a8-125">사용 하 여 hello 다음 명령은 VM hello로 SSH 세션 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="957a8-126">Toouse hello 올바른 공용 IP 주소가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="957a8-127">위 예제에서 IP 주소는 13.72.77.9입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="957a8-128">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="957a8-128">Install Node.js</span></span>

<span data-ttu-id="957a8-129">[Node.js](https://nodejs.org/en/)는 Chrome의 V8 JavaScript 엔진을 기준으로 하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="957a8-130">Node.js는 Express 경로 hello 및 AngularJS 컨트롤러를이 자습서 tooset에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="957a8-131">Hello, SSH를 사용 하 여 열린 hello bash 셸의 사용 하 여 VM에서 Node.js를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="957a8-132">MongoDB를 설치 하 고 hello 서버 설정</span><span class="sxs-lookup"><span data-stu-id="957a8-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="957a8-133">[MongoDB](http://www.mongodb.com)는 유연한 JSON 유사 문서에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="957a8-134">문서 toodocument에서 다양 한 데이터베이스의 필드 및 데이터 구조는 시간이 지남에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="957a8-135">이 예제에서는 응용 프로그램에 대 한 책 이름, isbn 번호, 작성자 및 페이지 수를 포함 하는 책 레코드 tooMongoDB 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="957a8-136">Hello, SSH를 사용 하 여 열린 hello bash 셸의 사용 하 여 VM에서 hello MongoDB 키로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="957a8-137">Hello 키로 hello 패키지 관리자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="957a8-138">MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="957a8-139">Hello 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="957a8-140">또한 tooinstall hello 필요 [본문 파서](https://www.npmjs.com/package/body-parser-json) 패키지 toohelp us 처리 hello JSON 요청 toohello 서버에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="957a8-141">Hello npm 패키지 관리자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="957a8-142">Hello 본문 파서 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="957a8-143">라는 폴더를 만듭니다 *설명서* 라는 파일 tooit 추가 *server.js* hello 웹 서버에 대 한 hello 구성을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

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

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="957a8-144">Express를 설치 하 고 경로 toohello 서버 설정</span><span class="sxs-lookup"><span data-stu-id="957a8-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="957a8-145">[Express](https://expressjs.com)는 웹 및 모바일 응용 프로그램용 기능을 제공하는 유연한 최소 규모의 Node.js 웹 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="957a8-146">MongoDB 데이터베이스에서이 자습서 toopass 책 정보 tooand에 빠른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="957a8-147">[Mongoose](http://mongoosejs.com) 직접적인 스키마 기반 솔루션 toomodel 응용 프로그램 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="957a8-148">이 자습서 tooprovide mongoose는 hello 데이터베이스에 대 한 책 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="957a8-149">Express 및 Mongoose를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="957a8-150">Hello에 *설명서* 폴더를 라는 폴더를 만듭니다 *앱* 라는 파일 *routes.js* hello로 express 경로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

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

3. <span data-ttu-id="957a8-151">Hello에 *앱* 폴더 라는 폴더를 만듭니다 *모델* 라는 파일 *book.js* hello 책 모델 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

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

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="957a8-152">AngularJS와 액세스 hello 경로</span><span class="sxs-lookup"><span data-stu-id="957a8-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="957a8-153">[AngularJS](https://angularjs.org)는 웹 응용 프로그램에서 동적 뷰를 만들기 위한 웹 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="957a8-154">이 자습서에서는 빠른 AngularJS tooconnect 품질 웹 페이지를 사용 하 고 책 데이터베이스에서 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="957a8-155">Hello 디렉터리를 백업에 변경*설명서* (`cd ../..`), 다음 라는 폴더를 만듭니다 *공용* 라는 파일 *script.js* hello 컨트롤러와 정의 된 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="957a8-156">Hello에 *공용* 폴더를 라는 파일을 만들어 *index.html* 된 hello 웹 페이지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

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

##  <a name="run-hello-application"></a><span data-ttu-id="957a8-157">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="957a8-157">Run hello application</span></span>

1. <span data-ttu-id="957a8-158">Hello 디렉터리를 백업에 변경*설명서* (`cd ..`)이이 명령을 실행 하 여 hello 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="957a8-159">웹 브라우저 toohello 주소를 hello VM에 대해 기록를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="957a8-160">예: *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="957a8-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="957a8-161">다음 페이지는 hello와 같은 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-161">You should see something like hello following page:</span></span>

    ![책 레코드](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="957a8-163">Hello 텍스트 상자에 데이터를 입력 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="957a8-164">예:</span><span class="sxs-lookup"><span data-stu-id="957a8-164">For example:</span></span>

    ![책 레코드 추가](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="957a8-166">Hello 페이지를 새로 고친 후 다음과 같이이 페이지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-166">After refreshing hello page, you should see something like this page:</span></span>

    ![책 레코드 나열](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="957a8-168">누르면 **삭제** hello 데이터베이스에서 hello 책 레코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="957a8-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="957a8-169">Next steps</span></span>

<span data-ttu-id="957a8-170">이 자습서에서는 Linux VM에 대해 MEAN 스택을 사용하여 책 레코드를 추적하는 웹 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="957a8-171">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="957a8-172">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="957a8-172">Create a Linux VM</span></span>
> * <span data-ttu-id="957a8-173">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="957a8-173">Install Node.js</span></span>
> * <span data-ttu-id="957a8-174">MongoDB를 설치 하 고 hello 서버 설정</span><span class="sxs-lookup"><span data-stu-id="957a8-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="957a8-175">Express를 설치 하 고 경로 toohello 서버 설정</span><span class="sxs-lookup"><span data-stu-id="957a8-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="957a8-176">AngularJS와 액세스 hello 경로</span><span class="sxs-lookup"><span data-stu-id="957a8-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="957a8-177">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="957a8-177">Run hello application</span></span>

<span data-ttu-id="957a8-178">다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="957a8-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="957a8-179">SSL로 웹 서버 보안</span><span class="sxs-lookup"><span data-stu-id="957a8-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
