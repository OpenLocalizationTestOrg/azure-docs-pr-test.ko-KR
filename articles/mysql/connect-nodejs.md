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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>MySQL에 대 한 azure 데이터베이스: 사용 하 여 Node.js tooconnect 및 쿼리 데이터
이 빠른 시작에서는 tooconnect tooan Azure를 사용 하 여 MySQL에 대 한 데이터베이스 방법을 [Node.js](https://nodejs.org/) 창, Ubuntu Linux 및 Mac 플랫폼에서 합니다. Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. hello이 문서의 단계 Node.js를 사용 하 여 개발 된 익숙한 고 가정 MySQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기](./quickstart-create-mysql-server-database-using-azure-cli.md)

다음과 같은 작업도 필요합니다.
- Hello 설치 [Node.js](https://nodejs.org) 런타임.
- 설치 [mysql2](https://www.npmjs.com/package/mysql2) hello Node.js 응용 프로그램에서에서 tooconnect tooMySQL 패키지 합니다. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Node.js를 설치 하 고 MySQL 커넥터 hello
플랫폼에 따라 적절 한 지침이 tooinstall hello Node.js를 따릅니다. Npm tooinstall hello mysql2 패키지 및 해당 종속성을 사용 하 여 프로젝트 폴더에 있습니다.

### <a name="windows"></a>**Windows**
1. Hello 방문 [Node.js 다운로드 페이지](https://nodejs.org/en/download/) 에 원하는 Windows installer 옵션을 선택 합니다.
2. 로컬 프로젝트 폴더를 만듭니다(예: `nodejsmysql`). 
3. 명령 프롬프트 hello 및 cd hello 프로젝트 폴더에 같은 시작`cd c:\nodejsmysql\`
4. Hello 프로젝트 폴더에 hello NPM 도구 tooinstall hello mysql2 라이브러리를 실행 합니다.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Hello를 확인 하 여 hello 설치 확인 `npm list` 에 대 한 텍스트 출력 `mysql2@1.3.5`합니다.

### <a name="linux-ubuntu"></a>**Linux(Ubuntu)**
1. 실행된 hello 다음 명령을 tooinstall **Node.js** 및 **npm** Node.js 용 hello 패키지 관리자.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. 프로젝트 폴더 hello 명령을 toomake 다음 실행 `mysqlnodejs` hello mysql2 패키지를 해당 폴더에 설치 합니다.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Npm 목록 출력 텍스트를 확인 하 여 hello 설치 확인 `mysql2@1.3.5`합니다.

### <a name="mac-os"></a>**Mac OS**
1. 다음 명령을 tooinstall hello 입력 **끓여**, Mac OS X에 대 한 사용 하기 쉬운 패키지 관리자 및 **Node.js**합니다.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. 프로젝트 폴더 hello 명령을 toomake 다음 실행 `mysqlnodejs` hello mysql2 패키지를 해당 폴더에 설치 합니다.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Hello를 확인 하 여 hello 설치 확인 `npm list` 에 대 한 텍스트 출력 `mysql2@1.3.6`합니다. hello 버전 번호가 다를 수 있습니다 새로운 패치 출시 되 합니다.

## <a name="get-connection-information"></a>연결 정보 가져오기
MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 왼쪽된 창에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 (예를 들어 **myserver4demo**).
3. Hello 서버 이름을 클릭 **myserver4demo**합니다.
4. 선택 hello 서버 **속성** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-nodejs/1_server-properties-name-login.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="running-hello-javascript-code-in-nodejs"></a>Node.js에 hello JavaScript 코드를 실행합니다.
1. 텍스트 파일에 hello JavaScript 코드를 붙여 넣고 파일 확장명은.js, 예: C:\nodejsmysql\createtable.js 또는 /home/username/nodejsmysql/createtable.js와 프로젝트 폴더에 저장
2. Hello 명령 프롬프트를 시작 하거나 bash 셸은 합니다. 디렉터리를 프로젝트 폴더로 변경합니다(예: `cd nodejsmysql`).
3. toorun hello 응용 프로그램 뒤 hello 파일 이름이 같은 hello 노드 명령을 입력 `node createtable.js`합니다.
4. Windows hello 노드 응용 프로그램 환경 변수 경로에 없는 경우 할 수도 있습니다 toouse hello 전체 경로 toolaunch hello 노드 응용 프로그램을와 같은`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>테이블 연결, 생성 및 데이터 삽입
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 **CREATE TABLE** 및 **INSERT INTO** SQL 문입니다.

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다. hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 함수는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 함수는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.

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

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다. 

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다. hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. hello 결과 배열이 hello 쿼리의 사용 되는 toohold hello 결과입니다.

Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.

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

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **업데이트** SQL 문입니다. 

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다. hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.

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

## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다. 

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 toointerface hello MySQL 서버와 합니다. hello [connect ()](https://github.com/mysqljs/mysql#establishing-connections) 메서드는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [query ()](https://github.com/mysqljs/mysql#performing-queries) 메서드는 MySQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.

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

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./concepts-migrate-import-export.md)
