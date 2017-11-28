---
title: "Node.js에서 MySQL에 대 한 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 MySQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 여러 Node.js 코드 샘플을 제공 합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="99974-103">MySQL에 대 한 azure 데이터베이스: 사용 하 여 Node.js tooconnect 및 쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="99974-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="99974-104">이 빠른 시작에서는 tooconnect tooan Azure를 사용 하 여 MySQL에 대 한 데이터베이스 방법을 [Node.js](https://nodejs.org/) 창, Ubuntu Linux 및 Mac 플랫폼에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="99974-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99974-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="99974-106">hello이 문서의 단계 Node.js를 사용 하 여 개발 된 익숙한 고 가정 MySQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99974-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="99974-107">Prerequisites</span></span>
<span data-ttu-id="99974-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="99974-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="99974-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="99974-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="99974-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="99974-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-111">You also need to:</span></span>
- <span data-ttu-id="99974-112">Hello 설치 [Node.js](https://nodejs.org) 런타임.</span><span class="sxs-lookup"><span data-stu-id="99974-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="99974-113">설치 [mysql2](https://www.npmjs.com/package/mysql2) hello Node.js 응용 프로그램에서에서 tooconnect tooMySQL 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="99974-114">Node.js를 설치 하 고 MySQL 커넥터 hello</span><span class="sxs-lookup"><span data-stu-id="99974-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="99974-115">플랫폼에 따라 적절 한 지침이 tooinstall hello Node.js를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="99974-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="99974-116">Npm tooinstall hello mysql2 패키지 및 해당 종속성을 사용 하 여 프로젝트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99974-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="99974-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="99974-117">**Windows**</span></span>
1. <span data-ttu-id="99974-118">Hello 방문 [Node.js 다운로드 페이지](https://nodejs.org/en/download/) 에 원하는 Windows installer 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="99974-119">로컬 프로젝트 폴더를 만듭니다(예: `nodejsmysql`).</span><span class="sxs-lookup"><span data-stu-id="99974-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="99974-120">명령 프롬프트 hello 및 cd hello 프로젝트 폴더에 같은 시작`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="99974-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="99974-121">Hello 프로젝트 폴더에 hello NPM 도구 tooinstall hello mysql2 라이브러리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="99974-122">Hello를 확인 하 여 hello 설치 확인 `npm list` 에 대 한 텍스트 출력 `mysql2@1.3.5`합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="99974-123">**Linux(Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="99974-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="99974-124">실행된 hello 다음 명령을 tooinstall **Node.js** 및 **npm** Node.js 용 hello 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="99974-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="99974-125">프로젝트 폴더 hello 명령을 toomake 다음 실행 `mysqlnodejs` hello mysql2 패키지를 해당 폴더에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="99974-126">Npm 목록 출력 텍스트를 확인 하 여 hello 설치 확인 `mysql2@1.3.5`합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="99974-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="99974-127">**Mac OS**</span></span>
1. <span data-ttu-id="99974-128">다음 명령을 tooinstall hello 입력 **끓여**, Mac OS X에 대 한 사용 하기 쉬운 패키지 관리자 및 **Node.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="99974-129">프로젝트 폴더 hello 명령을 toomake 다음 실행 `mysqlnodejs` hello mysql2 패키지를 해당 폴더에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="99974-130">Hello를 확인 하 여 hello 설치 확인 `npm list` 에 대 한 텍스트 출력 `mysql2@1.3.6`합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="99974-131">hello 버전 번호가 다를 수 있습니다 새로운 패치 출시 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="99974-132">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="99974-132">Get connection information</span></span>
<span data-ttu-id="99974-133">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="99974-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="99974-134">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="99974-135">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="99974-136">Hello 왼쪽된 창에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 (예를 들어 **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="99974-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="99974-137">Hello 서버 이름을 클릭 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="99974-138">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="99974-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="99974-139">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="99974-140">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="99974-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="99974-141">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="99974-142">Node.js에 hello JavaScript 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="99974-143">텍스트 파일에 hello JavaScript 코드를 붙여 넣고 파일 확장명은.js, 예: C:\nodejsmysql\createtable.js 또는 /home/username/nodejsmysql/createtable.js와 프로젝트 폴더에 저장</span><span class="sxs-lookup"><span data-stu-id="99974-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="99974-144">Hello 명령 프롬프트를 시작 하거나 bash 셸은 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="99974-145">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd nodejsmysql`).</span><span class="sxs-lookup"><span data-stu-id="99974-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="99974-146">toorun hello 응용 프로그램 뒤 hello 파일 이름이 같은 hello 노드 명령을 입력 `node createtable.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="99974-147">Windows hello 노드 응용 프로그램 환경 변수 경로에 없는 경우 할 수도 있습니다 toouse hello 전체 경로 toolaunch hello 노드 응용 프로그램을와 같은`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="99974-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="99974-148">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="99974-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="99974-149">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 **CREATE TABLE** 및 **INSERT INTO** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="99974-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="99974-151">hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 함수는 사용 되는 tooestablish hello 연결 toohello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="99974-152">hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 함수는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="99974-153">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="99974-154">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="99974-154">Read data</span></span>
<span data-ttu-id="99974-155">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="99974-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="99974-157">hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 tooestablish hello 연결 toohello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="99974-158">hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="99974-159">hello 결과 배열이 hello 쿼리의 사용 되는 toohold hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="99974-160">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="99974-161">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="99974-161">Update data</span></span>
<span data-ttu-id="99974-162">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="99974-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="99974-164">hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 tooestablish hello 연결 toohello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="99974-165">hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="99974-166">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="99974-167">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="99974-167">Delete data</span></span>
<span data-ttu-id="99974-168">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="99974-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="99974-170">hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 tooestablish hello 연결 toohello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="99974-171">hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="99974-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="99974-172">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="99974-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="99974-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99974-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="99974-174">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="99974-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
