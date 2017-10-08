---
title: "Python에서 PostgreSQL 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 있는 Python 코드 예제를 제공 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>Azure 데이터베이스에 대 한 PostgreSQL: Python 사용 tooconnect 및 쿼리 데이터
이 빠른 시작에서는 방법을 toouse [Python](https://python.org) tooconnect tooan PostgreSQL에 대 한 Azure 데이터베이스입니다. 또한 toouse SQL 문 tooquery를 삽입, 업데이트 및 macOS, Ubuntu Linux 및 Windows 플랫폼에서 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. 이 문서의 단계 hello Python을 사용 하 여 개발에 익숙한 하 고 새 tooworking PostgreSQL에 대 한 Azure 데이터베이스는 가정 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [DB 만들기 - 포털](quickstart-create-server-database-portal.md)
- [DB 만들기 - CLI](quickstart-create-server-database-azure-cli.md)

다음 항목도 필요합니다.
- [python](https://www.python.org/downloads/) 설치
- [pip](https://pip.pypa.io/en/stable/installing/) 패키지 설치([python.org](https://python.org)에서 다운로드한 Python 2 >=2.7.9 또는 Python 3 >=3.4 이진 파일을 사용하는 경우 pip가 이미 설치됨)

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>PostgreSQL에 대 한 hello Python 연결 라이브러리를 설치 합니다.
Hello 설치 [psycopg2](http://initd.org/psycopg/docs/install.html) tooconnect 및 쿼리 hello 데이터베이스를 사용할 수 있는 패키지입니다. psycopg2은 [PyPI에서 사용할 수 있는](https://pypi.python.org/pypi/psycopg2/) hello 형태로 [휠](http://pythonwheels.com/) hello 가장 일반적인 플랫폼 (OSX, Linux, Windows)에 대 한 패키지입니다. 사용 하 여 pip 모든 hello 종속성을 포함 하 여 hello 모듈의 tooget hello 이진 버전을 설치 합니다.

1. 자신의 컴퓨터에서 명령줄 인터페이스를 시작합니다.
    - Linux에서 hello Bash 셸의 시작 합니다.
    - MacOS 등 hello 터미널을 시작 합니다.
    - Windows hello 시작 메뉴에서에서 hello 명령 프롬프트를 시작 합니다.
2. 와 같은 명령을 실행 하 여 hello pip의 최신 버전을 사용 하 고 있는지 확인 합니다.
    ```cmd
    pip install -U pip
    ```

3. 다음 명령은 tooinstall hello psycopg2 패키지 hello를 실행 합니다.
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>연결 정보 가져오기
PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 검색 한 **mypgserver 20170401** (방금 만든 hello 서버).
3. Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.
4. 선택 hello 서버 **개요** 페이지를 선택한 다음 hello를 적어 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-python/1-connection-string.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="how-toorun-python-code"></a>어떻게 toorun Python 코드
이 항목에는 각각 특정 기능을 수행하는 총 4가지 샘플 코드가 포함되어 있습니다. hello 다음 지침을 나타내고 방법을 toocreate 텍스트 파일을 코드 블록을 삽입 다음 나중에 실행할 수 있도록 hello 파일을 저장 합니다. 있는지 toocreate 네 개의 별도 파일을 하나씩 각 코드 블록에 대 한 수입니다.

- 원하는 텍스트 편집기를 사용하여 새 파일을 만듭니다.
- 복사한 hello 코드 예제 중 하나를 hello hello 텍스트 파일에 다음 섹션에에서 붙여 넣습니다. Hello 대체 **호스트**, **dbname**, **사용자**, 및 **암호** hello 값이 hello를 만들 때 지정 된 매개 변수 서버 및 데이터베이스입니다.
- Hello 파일 hello.py 확장명 (예: postgres.py)으로 프로젝트 폴더에 저장 합니다. Hello Windows 운영 체제를 실행 하는 경우 수 있는지 tooselect utf-8 인코딩을 hello 파일을 저장할 때입니다. 
- Hello 명령 프롬프트 또는 Bash 셸을 시작 하 고 예를 들어 hello 디렉터리 tooyour 프로젝트 폴더를 변경 합니다 `cd postgres`합니다.
-  toorun hello 코드 형식 hello hello 파일 이름 예를 들어 다음 Python 명령 `Python postgres.py`합니다.

> [!NOTE]
> Python 버전 3 년부터 hello 오류가 표시 될 수 있습니다 `SyntaxError: Missing parentheses in call too'print'` hello 다음 코드 블록을 실행 하는 경우. 이렇게 되 면 각 호출 toohello 명령 대신 `print "string"` 같은 괄호를 사용 하 여 함수 호출으로 `print("string")`합니다.

## <a name="connect-create-table-and-insert-data"></a>테이블 연결, 생성 및 데이터 삽입
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) 작동 **삽입** SQL 문입니다. hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 함수는 PostgreSQL 데이터베이스에 대해 사용 되는 tooexecute hello SQL 쿼리 합니다. Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

Hello 코드를 실행 한 다음, 다음과 같이 hello 출력 됩니다.

![명령줄 출력](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 코드를 사용 하 여 삽입 한 tooread hello 데이터 [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 작동 **선택** SQL 문입니다. 이 함수는 쿼리를 허용 하 고 hello 사용 하 여 반환 된 결과 집합을 반복 [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall)합니다. Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 코드를 사용 하 여 앞서 삽입 한 tooupdate hello 인벤토리 행 [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 작동 **업데이트** SQL 문입니다. Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 코드를 사용 하 여 이전에 삽입 된 인벤토리 항목 toodelete [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 작동 **삭제** SQL 문입니다. Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값이 있는 hello 호스트, dbname, 사용자 및 암호 매개 변수를 대체 합니다.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
