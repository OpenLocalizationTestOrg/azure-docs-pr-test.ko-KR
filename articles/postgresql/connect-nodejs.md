---
title: "Node.js에서 PostgreSQL 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 있는 Node.js 코드 샘플을 제공 합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Azure 데이터베이스에 대 한 PostgreSQL: 사용 하 여 Node.js tooconnect 및 쿼리 데이터
이 빠른 시작에서는 tooconnect tooan Azure PostgreSQL 사용에 대 한 데이터베이스 방법을 [Node.js](https://nodejs.org/)합니다. Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. hello이 문서의 단계 Node.js를 사용 하 여 개발 된 익숙한 고 가정 PostgreSQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [DB 만들기 - 포털](quickstart-create-server-database-portal.md)
- [DB 만들기 - CLI](quickstart-create-server-database-azure-cli.md)

다음과 같은 작업도 필요합니다.
- [Node.js](https://nodejs.org)

## <a name="install-pg-client"></a>Pg 클라이언트 설치
Node.js용 PostgreSQL 클라이언트인 [pg](https://www.npmjs.com/package/pg)를 설치합니다.

따라서 toodo 명령줄 tooinstall hello pg 클라이언트에서 hello 노드 패키지 관리자 (npm) javascript 실행 합니다.
```bash
npm install pg
```

설치 된 hello 패키지를 나열 하 여 hello 설치를 확인 합니다.
```bash
npm list
```

## <a name="get-connection-information"></a>연결 정보 가져오기
PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 방금 만든 hello 서버에 대 한 검색 합니다.
3. Hello 서버 이름을 클릭 합니다.
4. 선택 hello 서버 **개요** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-nodejs/1-connection-string.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="running-hello-javascript-code-in-nodejs"></a>Node.js에 hello JavaScript 코드를 실행합니다.
입력 하 여 hello bash 셸 또는 windows 명령 프롬프트에서 Node.js를 시작할 수 있습니다 `node`, 다음 복사 하 여 hello 예제 JavaScript 코드를 대화형으로 실행 및 hello 프롬프트에 붙여 넣는 것입니다. 또는 hello JavaScript 코드 실행 및 텍스트 파일에 저장할 수 있습니다 있습니다 `node filename.js` hello 파일 이름으로 매개 변수 toorun 것입니다.

## <a name="connect-create-table-and-insert-data"></a>테이블 연결, 생성 및 데이터 삽입
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 **CREATE TABLE** 및 **INSERT INTO** SQL 문입니다.
hello [pg 합니다. 클라이언트](https://github.com/brianc/node-postgres/wiki/Client) 개체는 사용 되는 toointerface hello PostgreSQL 서버와 합니다. hello [pg 합니다. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 함수는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [pg 합니다. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 함수는 PostgreSQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다.

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다. hello [pg 합니다. 클라이언트](https://github.com/brianc/node-postgres/wiki/Client) 개체는 사용 되는 toointerface hello PostgreSQL 서버와 합니다. hello [pg 합니다. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 함수는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [pg 합니다. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 함수는 PostgreSQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **업데이트** SQL 문입니다. hello [pg 합니다. 클라이언트](https://github.com/brianc/node-postgres/wiki/Client) 개체는 사용 되는 toointerface hello PostgreSQL 서버와 합니다. hello [pg 합니다. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 함수는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [pg 합니다. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 함수는 PostgreSQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다. hello [pg 합니다. 클라이언트](https://github.com/brianc/node-postgres/wiki/Client) 개체는 사용 되는 toointerface hello PostgreSQL 서버와 합니다. hello [pg 합니다. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 함수는 사용 되는 tooestablish hello 연결 toohello 서버입니다. hello [pg 합니다. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 함수는 PostgreSQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. 

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
