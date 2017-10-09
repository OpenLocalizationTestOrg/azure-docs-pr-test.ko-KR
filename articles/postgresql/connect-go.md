---
title: "aaaConnect tooAzure Go 언어를 사용 하 여 PostgreSQL 데이터베이스 | Microsoft Docs"
description: "이 퀵 스타트의 Go 프로그래밍 언어에서는 예제를 제공 tooconnect 사용 및 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 있습니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>Azure 데이터베이스에 대 한 PostgreSQL: 언어 tooconnect 및 쿼리 데이터 사용 하 여 이동
이 빠른 시작에서는 PostgreSQL 사용에 대 한 tooconnect tooan Azure 데이터베이스에서 작성 된 hello 코드가 방식 [이동](https://golang.org/) 언어 (golang). Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. 이 문서에서는 하지만 새 tooworking PostgreSQL에 대 한 Azure 데이터베이스는 Go를 사용 하 여 개발에 잘 알고 있다면 가정 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [DB 만들기 - 포털](quickstart-create-server-database-portal.md)
- [DB 만들기 - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Go 및 pq 커넥터 설치
설치 [이동](https://golang.org/doc/install) 및 hello [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) 사용자의 컴퓨터에 있습니다. 플랫폼에 따라 hello 단계를 수행 합니다.

### <a name="windows"></a>Windows
1. [다운로드](https://golang.org/dl/) Go toohello에 따라 Microsoft Windows 용 설치 [설치 지침](https://golang.org/doc/install)합니다.
2. Hello 시작 메뉴에서 hello 명령 프롬프트를 시작 합니다.
3. 다음과 같이 프로젝트 폴더를 만듭니다. `mkdir  %USERPROFILE%\go\src\postgresqlgo`
4. 와 같은 hello 프로젝트 폴더로 디렉터리를 변경 `cd %USERPROFILE%\go\src\postgresqlgo`합니다.
5. GOPATH toopoint toohello 소스 코드 디렉터리에 대 한 hello 환경 변수를 설정 합니다. `set GOPATH=%USERPROFILE%\go`
6. Hello 설치 [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) hello를 실행 하 여 `go get github.com/lib/pq` 명령입니다.

   요약 하자면, Go 설치 후 hello 명령 프롬프트에서 다음이 명령을 실행 합니다.
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux(Ubuntu)
1. Hello Bash 셸의 시작 합니다. 
2. `sudo apt-get install golang-go`를 실행하여 Go를 설치합니다.
3. 홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/postgresqlgo/`).
4. 와 같은 hello 폴더로 디렉터리를 변경 `cd ~/go/src/postgresqlgo/`합니다.
5. 집합 hello GOPATH 환경 변수 toopoint tooa 유효한 소스와 같은 디렉터리에 현재 홈 디렉터리의 폴더를 이동 합니다. Hello bash 셸의 실행 `export GOPATH=~/go` tooadd hello GOPATH hello 현재 셸 세션에 대 한 hello으로 디렉터리를 이동 합니다.
6. Hello 설치 [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) hello를 실행 하 여 `go get github.com/lib/pq` 명령입니다.

   요약하자면, 다음과 같은 Bash 명령을 실행합니다.
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>Apple macOS
1. 다운로드 및 설치 toohello를 따라 이동 [설치 지침](https://golang.org/doc/install) 플랫폼에 일치 합니다. 
2. Hello Bash 셸의 시작 합니다. 
3. 홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/postgresqlgo/`).
4. 와 같은 hello 폴더로 디렉터리를 변경 `cd ~/go/src/postgresqlgo/`합니다.
5. 집합 hello GOPATH 환경 변수 toopoint tooa 유효한 소스와 같은 디렉터리에 현재 홈 디렉터리의 폴더를 이동 합니다. Hello bash 셸의 실행 `export GOPATH=~/go` tooadd hello GOPATH hello 현재 셸 세션에 대 한 hello으로 디렉터리를 이동 합니다.
6. Hello 설치 [순수 이동 Postgres 드라이버 (pq)](https://github.com/lib/pq) hello를 실행 하 여 `go get github.com/lib/pq` 명령입니다.

   요약하자면, Go 설치 후 다음 bash 명령을 실행합니다.
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>연결 정보 가져오기
PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **mypgserver 20170401**합니다.
3. Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.
4. 선택 hello 서버 **개요** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-go/1-connection-string.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** 페이지 및 보기 hello 서버 관리자 로그인 이름입니다. 필요한 경우 hello 암호를 재설정 합니다.

## <a name="build-and-run-go-code"></a>Go 코드 작성 및 실행 
1. toowrite Golang 코드, Microsoft Windows의 메모장과 같은 간단한 텍스트 편집기를 사용할 수 있습니다 [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) 또는 [Nano](https://www.nano-editor.org/) Ubuntu, 또는 macOS에서 TextEdit 합니다. 보다 풍부한 IDE(대화형 개발 환경)를 선호하는 경우 Jetbrains의 [Gogland](https://www.jetbrains.com/go/), Microsoft의 [Visual Studio Code](https://code.visualstudio.com/) 또는 [Atom](https://atom.io/)을 사용해 보세요.
2. 텍스트 파일로 hello 섹션 아래에서 hello Golang 코드를 붙여 넣고 파일 확장명으로 프로젝트 폴더에 저장할 \*Windows 경로 같은.go `%USERPROFILE%\go\src\postgresqlgo\createtable.go` 또는 Linux 경로 `~/go/src/postgresqlgo/createtable.go`합니다.
3. Hello 찾습니다 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` hello 코드 및 고유한 값으로 바꾸기 hello 예제 값에는 상수입니다.  
4. Hello 명령 프롬프트를 시작 하거나 bash 셸은 합니다. 디렉터리를 프로젝트 폴더로 변경합니다. 예를 들어 Windows에서는 `cd %USERPROFILE%\go\src\postgresqlgo\`이고, Linux에서는 `cd ~/go/src/postgresqlgo/`입니다. 일부 hello IDE 환경 셸 명령이 필요 없이 디버그 및 런타임 기능을 제공 합니다.
5. Hello 명령을 입력 하 여 hello 코드 실행 `go run createtable.go` toocompile hello 응용 프로그램을 실행 합니다. 
6. 네이티브 응용 프로그램에 hello 코드 또는 toobuild `go build createtable.go`, 다음 실행 `createtable.exe` toorun hello 응용 프로그램입니다.

## <a name="connect-and-create-a-table"></a>테이블 연결 및 생성
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 테이블을 만들 **CREATE TABLE** SQL 문 다음에 **INSERT INTO** hello 테이블에 SQL 문 tooadd 행입니다.

hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.

메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다. A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다. hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드가 여러 번 toorun 몇 가지 SQL 명령을 합니다. 각 오류가 발생 한 경우 사용자 지정 checkError() 메서드 toocheck 시간 및 tooexit 오류가 발생 하면 당황 합니다.

Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다. 

hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.

메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다. A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다. 메서드를 호출 하 여 hello select 쿼리를 실행할 [db입니다. Query ()](https://golang.org/pkg/database/sql/#DB.Query), 형식의 변수에 유지 되는 결과 행 hello 및 [행](https://golang.org/pkg/database/sql/#Rows)합니다. hello 코드 메서드를 사용 하 여 hello 현재 행의 hello 열 데이터 값을 읽고 [행. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) 및 hello 반복기를 사용 하 여 hello 행에 대해 루프 [행. Next ()](https://golang.org/pkg/database/sql/#Rows.Next) 행이 더 이상 존재 될 때까지 합니다. 각 행의 열 값은 아웃 인쇄 toohello 콘솔입니다. 각 오류가 발생 한 경우 사용자 지정 checkError() 메서드 toocheck 시간 및 tooexit 오류가 발생 하면 당황 합니다.

Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.

hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.

메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다. A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다. hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드 toorun hello hello 테이블을 업데이트 하는 SQL 문입니다. 사용자 지정 checkError() 메서드 toocheck에서 오류가 발생 했으며 오류가 tooexit 당황 경우 발생 합니다.

Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다. 

hello 코드는 세 가지 패키지를 가져옵니다: hello [sql 패키지](https://golang.org/pkg/database/sql/), hello [pq 패키지](http://godoc.org/github.com/lib/pq) hello Postgres 서버 hello와 드라이버 toocommunicate로 [fmt 패키지](https://golang.org/pkg/fmt/) 인쇄에 대 한 입력 및 hello 명령줄에 출력 합니다.

메서드를 호출 하는 hello 코드 [sql 합니다. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL, 및 메서드를 사용 하 여 검사 hello 연결에 대 한 데이터베이스 [db입니다. Ping()](https://golang.org/pkg/database/sql/#DB.Ping)합니다. A [데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB) hello 데이터베이스 서버에 대 한 hello 연결 풀을 보유, 전체에서 사용 됩니다. hello 코드 호출 hello [exec ()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드 toorun hello hello 테이블을 업데이트 하는 SQL 문입니다. 사용자 지정 checkError() 메서드 toocheck에서 오류가 발생 했으며 오류가 tooexit 당황 경우 발생 합니다.

Hello 대체 `HOST`, `DATABASE`, `USER`, 및 `PASSWORD` 를 원하는 값으로 매개 변수입니다. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
