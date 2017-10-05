---
title: "Azure의 Linux VM에서 MEAN 스택 만들기 | Microsoft Docs"
description: "Azure의 Linux VM에서 MEAN(MongoDB, Express, AngularJS 및 Node.js) 스택을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 892d3481b4ec70fb8434cb25013c5cfd8ab85051
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="d213a-103">Azure의 Linux VM에서 MEAN(MongoDB, Express, AngularJS 및 Node.js) 스택 만들기</span><span class="sxs-lookup"><span data-stu-id="d213a-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="d213a-104">이 자습서에서는 Azure의 Linux VM에서 MEAN(MongoDB, Express, AngularJS 및 Node.js) 스택을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-104">This tutorial shows you how to implement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="d213a-105">만드는 MEAN 스택을 사용하여 데이터베이스에서 책을 추가, 삭제 및 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-105">The MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="d213a-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d213a-107">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d213a-107">Create a Linux VM</span></span>
> * <span data-ttu-id="d213a-108">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="d213a-108">Install Node.js</span></span>
> * <span data-ttu-id="d213a-109">MongoDB 설치 및 서버 설정</span><span class="sxs-lookup"><span data-stu-id="d213a-109">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="d213a-110">Express 설치 및 서버에 대한 경로 설정</span><span class="sxs-lookup"><span data-stu-id="d213a-110">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="d213a-111">AngularJS를 사용하여 경로에 액세스</span><span class="sxs-lookup"><span data-stu-id="d213a-111">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="d213a-112">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d213a-112">Run the application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d213a-113">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d213a-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="d213a-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d213a-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="d213a-116">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d213a-116">Create a Linux VM</span></span>

<span data-ttu-id="d213a-117">[az group create](https://docs.microsoft.com/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만들고 [az vm create](https://docs.microsoft.com/cli/azure/vm#create) 명령을 사용하여 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-117">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="d213a-118">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d213a-119">다음 예제에서는 Azure CLI를 사용하여 *eastus* 위치에 *myResourceGroupMEAN*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-119">The following example uses the Azure CLI to create a resource group named *myResourceGroupMEAN* in the *eastus* location.</span></span> <span data-ttu-id="d213a-120">또한 기본 키 위치에 SSH 키가 없는 경우 SSH 키가 있는 *myVM*이라는 VM이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="d213a-121">특정 키 집합을 사용하려면 --ssh-key-value 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-121">To use a specific set of keys, use the --ssh-key-value option.</span></span>

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

<span data-ttu-id="d213a-122">VM을 만든 경우 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-122">When the VM has been created, the Azure CLI shows information similar to the following example:</span></span> 

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
<span data-ttu-id="d213a-123">`publicIpAddress`을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-123">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="d213a-124">이 주소는 VM에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-124">This address is used to access the VM.</span></span>

<span data-ttu-id="d213a-125">다음 명령을 사용하여 VM으로 SSH 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-125">Use the following command to create an SSH session with the VM.</span></span> <span data-ttu-id="d213a-126">유효한 공용 IP 주소를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-126">Make sure to use the correct public IP address.</span></span> <span data-ttu-id="d213a-127">위 예제에서 IP 주소는 13.72.77.9입니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="d213a-128">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="d213a-128">Install Node.js</span></span>

<span data-ttu-id="d213a-129">[Node.js](https://nodejs.org/en/)는 Chrome의 V8 JavaScript 엔진을 기준으로 하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="d213a-130">Node.js는 Express 경로 및 AngularJS 컨트롤러를 설정하기 위해 이 자습서에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-130">Node.js is used in this tutorial to set up the Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="d213a-131">VM에서 연 bash 셸을 SSH와 함께 사용하여 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-131">On the VM, using the bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-the-server"></a><span data-ttu-id="d213a-132">MongoDB 설치 및 서버 설정</span><span class="sxs-lookup"><span data-stu-id="d213a-132">Install MongoDB and set up the server</span></span>
<span data-ttu-id="d213a-133">[MongoDB](http://www.mongodb.com)는 유연한 JSON 유사 문서에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="d213a-134">데이터베이스의 필드는 문서마다 다를 수 있으며 데이터 구조는 시간이 지남에 따라 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-134">Fields in a database can vary from document to document and data structure can be changed over time.</span></span> <span data-ttu-id="d213a-135">예제 응용 프로그램에서는 책 이름, isbn 번호, 저자 및 페이지 수를 포함하는 책 레코드를 MongoDB에 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-135">For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="d213a-136">VM에서 연 bash 셸을 SSH와 함께 사용하여 MongoDB를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-136">On the VM, using the bash shell that you opened with SSH, set the MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="d213a-137">패키지 관리자를 키로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-137">Update the package manager with the key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="d213a-138">MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="d213a-139">서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-139">Start the server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="d213a-140">또한 서버 요청에 전달된 JSON을 처리하는 데 도움이 되는 [body-parser](https://www.npmjs.com/package/body-parser-json) 패키지도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-140">We also need to install the [body-parser](https://www.npmjs.com/package/body-parser-json) package to help us process the JSON passed in requests to the server.</span></span>

    <span data-ttu-id="d213a-141">npm 패키지 관리자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-141">Install the npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="d213a-142">본문 파서 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-142">Install the body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="d213a-143">*books*라는 폴더를 만들고 웹 서버에 대한 구성을 포함하는 *server.js*라는 파일을 이 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-143">Create a folder named *Books* and add a file to it named *server.js* that contains the configuration for the web server.</span></span>

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

## <a name="install-express-and-set-up-routes-to-the-server"></a><span data-ttu-id="d213a-144">Express 설치 및 서버에 대한 경로 설정</span><span class="sxs-lookup"><span data-stu-id="d213a-144">Install Express and set up routes to the server</span></span>

<span data-ttu-id="d213a-145">[Express](https://expressjs.com)는 웹 및 모바일 응용 프로그램용 기능을 제공하는 유연한 최소 규모의 Node.js 웹 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="d213a-146">이 자습서에서는 MongoDB 데이터베이스와 책 정보를 빠르게 주고 받기 위해 Express를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-146">Express is used in this tutorial to pass book information to and from our MongoDB database.</span></span> <span data-ttu-id="d213a-147">[Mongoose](http://mongoosejs.com)는 응용 프로그램 데이터를 모델링하기 위한 간편한 스키마 기반 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution to model your application data.</span></span> <span data-ttu-id="d213a-148">Mongoose는 데이터베이스에 책 스키마를 제공하기 위해 이 자습서에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-148">Mongoose is used in this tutorial to provide a book schema for the database.</span></span>

1. <span data-ttu-id="d213a-149">Express 및 Mongoose를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="d213a-150">*Books* 폴더에서 *apps*라는 폴더를 만들고 Express 경로가 정의된 *routes.js*라는 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-150">In the *Books* folder, create a folder named *apps* and add a file named *routes.js* with the express routes defined.</span></span>

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
            message: "Successfully deleted the book",
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

3. <span data-ttu-id="d213a-151">*apps* 폴더에서 *models*라는 폴더를 만들고 책 모델 구성이 정의된 *book.js*라는 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-151">In the *apps* folder, create a folder named *models* and add a file named *book.js* with the book model configuration defined.</span></span>  

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

## <a name="access-the-routes-with-angularjs"></a><span data-ttu-id="d213a-152">AngularJS를 사용하여 경로에 액세스</span><span class="sxs-lookup"><span data-stu-id="d213a-152">Access the routes with AngularJS</span></span>

<span data-ttu-id="d213a-153">[AngularJS](https://angularjs.org)는 웹 응용 프로그램에서 동적 뷰를 만들기 위한 웹 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="d213a-154">이 자습서에서는 AngularJS를 사용하여 웹 페이지를 Express에 연결하고 책 데이터베이스에 대해 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-154">In this tutorial, we use AngularJS to connect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="d213a-155">디렉터리를 *Books*로 다시 변경하고(`cd ../..`) *public*이라는 폴더를 만들고 컨트롤러 구성이 정의된 *script.js*라는 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-155">Change the directory back up to *Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with the controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="d213a-156">*public* 폴더에 웹 페이지가 정의된 *index.html*이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-156">In the *public* folder, create a file named *index.html* with the web page defined.</span></span>

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

##  <a name="run-the-application"></a><span data-ttu-id="d213a-157">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d213a-157">Run the application</span></span>

1. <span data-ttu-id="d213a-158">디렉터리를 *Books*로 다시 변경하고(`cd ..`) 다음 명령을 실행하여 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-158">Change the directory back up to *Books* (`cd ..`) and start the server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="d213a-159">VM에 대해 기록된 주소로 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-159">Open a web browser to the address that you recorded for the VM.</span></span> <span data-ttu-id="d213a-160">예: *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="d213a-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="d213a-161">다음 페이지와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-161">You should see something like the following page:</span></span>

    ![책 레코드](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="d213a-163">데이터를 텍스트 상자에 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-163">Enter data into the textboxes and click **Add**.</span></span> <span data-ttu-id="d213a-164">예:</span><span class="sxs-lookup"><span data-stu-id="d213a-164">For example:</span></span>

    ![책 레코드 추가](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="d213a-166">페이지를 새로 고치면 다음 페이지와 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-166">After refreshing the page, you should see something like this page:</span></span>

    ![책 레코드 나열](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="d213a-168">**삭제**를 클릭하고 데이터베이스에서 책 레코드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-168">You could click **Delete** and remove the book record from the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d213a-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d213a-169">Next steps</span></span>

<span data-ttu-id="d213a-170">이 자습서에서는 Linux VM에 대해 MEAN 스택을 사용하여 책 레코드를 추적하는 웹 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="d213a-171">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d213a-172">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d213a-172">Create a Linux VM</span></span>
> * <span data-ttu-id="d213a-173">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="d213a-173">Install Node.js</span></span>
> * <span data-ttu-id="d213a-174">MongoDB 설치 및 서버 설정</span><span class="sxs-lookup"><span data-stu-id="d213a-174">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="d213a-175">Express 설치 및 서버에 대한 경로 설정</span><span class="sxs-lookup"><span data-stu-id="d213a-175">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="d213a-176">AngularJS를 사용하여 경로에 액세스</span><span class="sxs-lookup"><span data-stu-id="d213a-176">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="d213a-177">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d213a-177">Run the application</span></span>

<span data-ttu-id="d213a-178">SSL 인증서로 웹 서버를 보호하는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d213a-178">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d213a-179">SSL로 웹 서버 보안</span><span class="sxs-lookup"><span data-stu-id="d213a-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
