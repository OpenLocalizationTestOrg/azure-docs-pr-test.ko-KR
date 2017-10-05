---
title: "Node.js에서 MySQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 MySQL용 Azure Database에서 데이터를 연결하고 쿼리하는 데 사용할 수 있는 몇 가지 Node.js 코드 샘플을 제공합니다."
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
ms.openlocfilehash: 0c0bd4b707c114d2991e5f0473a4bfbe9e463e3c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="b169b-103">MySQL용 Azure Database: Node.js를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="b169b-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="b169b-104">이 빠른 시작에서는 Windows, Ubuntu Linux 및 Mac 플랫폼에서 [Node.js](https://nodejs.org/)를 사용하여 MySQL용 Azure Database에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="b169b-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b169b-106">이 문서의 단계에서는 Node.js를 사용하여 개발하는 데 익숙하고 MySQL용 Azure Database를 처음 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b169b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b169b-107">Prerequisites</span></span>
<span data-ttu-id="b169b-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b169b-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b169b-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="b169b-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b169b-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="b169b-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-111">You also need to:</span></span>
- <span data-ttu-id="b169b-112">[Node.js](https://nodejs.org) 런타임을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="b169b-113">Node.js 응용 프로그램에서 MySQL에 연결하려면 [mysql2](https://www.npmjs.com/package/mysql2) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="b169b-114">Node.js 및 MySQL 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="b169b-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="b169b-115">플랫폼에 따라 적절한 지침을 수행하여 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-115">Depending on your platform, follow the appropriate instructions to install Node.js.</span></span> <span data-ttu-id="b169b-116">npm을 사용하여 프로젝트 폴더에 mysql2 패키지와 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="b169b-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b169b-117">**Windows**</span></span>
1. <span data-ttu-id="b169b-118">[Node.js 다운로드 페이지](https://nodejs.org/en/download/)를 방문하여 원하는 Windows 설치 관리자 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="b169b-119">로컬 프로젝트 폴더를 만듭니다(예: `nodejsmysql`).</span><span class="sxs-lookup"><span data-stu-id="b169b-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="b169b-120">명령 프롬프트를 시작하고 디렉터리를 프로젝트 폴더로 변경합니다(예: `cd c:\nodejsmysql\`).</span><span class="sxs-lookup"><span data-stu-id="b169b-120">Launch the command prompt and cd into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="b169b-121">NPM 도구를 실행하여 mysql2 라이브러리를 프로젝트 폴더에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="b169b-122">`mysql2@1.3.5`에 대한 `npm list` 출력 텍스트를 확인하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b169b-123">**Linux(Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="b169b-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="b169b-124">다음 명령을 실행하여 **Node.js** 및 **npm**(Node.js용 패키지 관리자)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="b169b-125">다음 명령을 실행하여 `mysqlnodejs` 프로젝트 폴더를 만들고 이 폴더에 mysql2 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-125">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="b169b-126">`mysql2@1.3.5`에 대한 npm list 출력 텍스트를 확인하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="b169b-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="b169b-127">**Mac OS**</span></span>
1. <span data-ttu-id="b169b-128">**Node.js** 및 사용하기 쉬운 Mac OS X용 패키지 관리자인 **brew**를 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="b169b-129">다음 명령을 실행하여 `mysqlnodejs` 프로젝트 폴더를 만들고 이 폴더에 mysql2 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-129">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="b169b-130">`mysql2@1.3.6`에 대한 `npm list` 출력 텍스트를 확인하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="b169b-131">버전 번호는 새 패치가 출시될 때마다 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b169b-132">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="b169b-132">Get connection information</span></span>
<span data-ttu-id="b169b-133">MySQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="b169b-134">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b169b-135">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b169b-136">왼쪽 창에서 **모든 리소스**를 클릭하고 만든 서버를 검색합니다(예: **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="b169b-136">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="b169b-137">**myserver4demo** 서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-137">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="b169b-138">서버의 **속성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="b169b-139">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b169b-140">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b169b-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b169b-141">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="b169b-142">Node.js에서 JavaScript 코드 실행</span><span class="sxs-lookup"><span data-stu-id="b169b-142">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="b169b-143">JavaScript 코드를 텍스트 파일에 붙여넣고 C:\nodejsmysql\createtable.js 또는 /home/username/nodejsmysql/createtable.js와 같이 .js 파일 확장명이 포함된 프로젝트 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-143">Paste the JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="b169b-144">명령 프롬프트 또는 Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-144">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="b169b-145">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd nodejsmysql`).</span><span class="sxs-lookup"><span data-stu-id="b169b-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="b169b-146">응용 프로그램을 실행하려면 node 명령 다음에 파일 이름을 입력합니다(예: `node createtable.js`).</span><span class="sxs-lookup"><span data-stu-id="b169b-146">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="b169b-147">Windows에서 노드 응용 프로그램이 환경 변수 경로에 없는 경우 전체 경로를 사용하여 노드 응용 프로그램을 시작해야 할 수도 있습니다(예: `"C:\Program Files\nodejs\node.exe" createtable.js`).</span><span class="sxs-lookup"><span data-stu-id="b169b-147">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b169b-148">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="b169b-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="b169b-149">**CREATE TABLE** 및 **INSERT INTO** SQL 문을 사용하여 데이터를 연결하고 로드하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b169b-149">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="b169b-150">[mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 MySQL 서버와 상호 작용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-150">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="b169b-151">[connect()](https://github.com/mysqljs/mysql#establishing-connections) 함수는 서버에 대한 연결을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-151">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="b169b-152">[query()](https://github.com/mysqljs/mysql#performing-queries) 함수는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-152">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="b169b-153">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-153">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="b169b-154">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="b169b-154">Read data</span></span>
<span data-ttu-id="b169b-155">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b169b-155">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="b169b-156">[mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 MySQL 서버와 상호 작용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-156">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="b169b-157">[connect()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 서버에 대한 연결을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-157">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="b169b-158">[query()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-158">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="b169b-159">결과 배열은 쿼리 결과를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-159">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="b169b-160">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-160">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="b169b-161">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="b169b-161">Update data</span></span>
<span data-ttu-id="b169b-162">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b169b-162">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="b169b-163">[mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 MySQL 서버와 상호 작용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-163">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="b169b-164">[connect()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 서버에 대한 연결을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-164">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="b169b-165">[query()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-165">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="b169b-166">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="b169b-167">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="b169b-167">Delete data</span></span>
<span data-ttu-id="b169b-168">**DELETE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b169b-168">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="b169b-169">[mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 MySQL 서버와 상호 작용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-169">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="b169b-170">[connect()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 서버에 대한 연결을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-170">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="b169b-171">[query()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-171">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="b169b-172">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b169b-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b169b-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b169b-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b169b-174">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b169b-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
