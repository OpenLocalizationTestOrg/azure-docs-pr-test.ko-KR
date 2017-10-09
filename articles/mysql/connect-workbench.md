---
title: "MySQL 워크 벤치에서 MySQL에 대 한 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 MySQL 용 hello 단계 toouse MySQL 워크 벤치 Azure 데이터베이스에서 tooconnect 및 쿼리 데이터를 제공합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>MySQL에 대 한 azure 데이터베이스: 사용 하 여 MySQL 워크 벤치 tooconnect 및 쿼리 데이터
이 빠른 시작에서는 방법을 사용 하 여 MySQL에 대 한 Azure 데이터베이스 tooconnect tooan hello MySQL 워크 벤치 응용 프로그램입니다. 

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>MySQL Workbench 설치
다운로드 하 여 MySQL 워크 벤치에서 컴퓨터에 설치 [hello MySQL 웹 사이트](https://dev.mysql.com/downloads/workbench/)합니다.

## <a name="get-connection-information"></a>연결 정보 가져오기
MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.

2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **myserver4demo**합니다.

3. Hello 서버 이름을 클릭 합니다.

4. 선택 hello 서버 **속성** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.

 ![MySQL용 Azure Database 서버 이름](./media/connect-workbench/1-server-properties-name-login.png)
 
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="connect-toohello-server-using-mysql-workbench"></a>MySQL 워크 벤치를 사용 하 여 toohello 서버 연결 
MySQL 워크 벤치 hello GUI 도구를 사용 하 여 tooconnect tooAzure MySQL 서버:

1.  Hello 컴퓨터에서 MySQL 워크 벤치 응용 프로그램을 시작 합니다. 

2.  **새 연결을 설정** 대화 상자를 hello hello에 다음 정보를 입력 **매개 변수** 탭:

    ![새 연결 설정](./media/connect-workbench/2-setup-new-connection.png)

    | **설정** | **제안 값** | **필드 설명** |
    |---|---|---|
    |   연결 이름 | 데모 연결 | 이 연결에 대한 레이블을 지정합니다. |
    | 연결 방법 | 표준(TCP/IP) | 표준(TCP/IP)이면 충분합니다. |
    | 호스트 이름 | *서버 이름* | 이전 MySQL 용 hello Azure 데이터베이스를 만들 때 사용 된 hello 서버 이름 값을 지정 합니다. 표시된 예제 서버는 myserver4demo.mysql.database.azure.com입니다. Hello 정규화 된 도메인 이름 사용 (\*. mysql.database.azure.com) hello 예제에 나와 있는 것 처럼 합니다. 서버 이름을 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다.  |
    | 포트 | 3306 | 항상 3306 MySQL 용 tooAzure 데이터베이스를 연결할 때 포트를 사용 합니다. |
    | 사용자 이름 |  *서버 관리자 로그인 이름* | Hello 서버 관리자 로그인 사용자 이름 앞 MySQL 용 hello Azure 데이터베이스를 만들 때 제공 된 입력 합니다. 이 예제에서는 사용자 이름이 myadmin@myserver4demo입니다. Hello username 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다. hello 형식은  *username@servername* 합니다.
    | 암호 | 사용자 암호 | 클릭 **자격 증명 모음에 저장 중...**  단추 toosave hello 암호입니다. |

3.   클릭 **연결 테스트** tootest 모든 매개 변수가 올바르게 구성 되어 있습니다. 

4.   클릭 **확인** toosave hello 연결 합니다. 

5.   hello 목록에서 **MySQL이 연결 되어**hello 연결 toobe 설정 될 때까지 기다리는 hello 타일 해당 tooyour 서버를 클릭 합니다.

6.   새 SQL 탭이 쿼리를 입력할 수 있는 빈 편집기로 열립니다.

    > [!NOTE]
    > 기본적으로 SSL 연결 보안이 필요하며 MySQL 서버용 Azure Database에서 적용됩니다. 일반적으로 SSL 인증서를 추가 구성 없이 MySQL 워크 벤치 tooconnect tooyour 서버에 필요 합니다. SSL에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](./howto-configure-ssl.md)합니다.  SSL toodisable 해야 할 경우 hello Azure 포털을 방문 하 고 hello 연결 보안 페이지 toodisable hello 적용 SSL 연결 설정/해제 단추를 클릭 합니다.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>테이블 만들기, 데이터 삽입, 데이터 읽기, 데이터 업데이트, 데이터 삭제
1. 데이터 복사 및 붙여넣기 hello 샘플 SQL 코드 빈 SQL 탭 tooillustrate에 몇 가지 예제입니다.

    이 코드는 quickstartdb라는 빈 데이터베이스를 만든 후 inventory라는 샘플 테이블을 만듭니다. 몇 개의 행을 삽입 하는 다음 hello 행을 읽습니다. Update 문과 함께 hello 데이터를 변경 하 고 읽기 안녕 행 키를 누릅니다. 마지막으로 한 행을 삭제 하 고 hello 행을 다시 읽습니다.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    hello 스크린 샷 실행 된 후 SQL Workbench 및 hello 출력의 hello SQL 코드의 예를 보여 줍니다.
    
    ![MySQL 워크 벤치 SQL 탭 toorun 샘플 SQL 코드](media/connect-workbench/3-workbench-sql-tab.png)

2. toorun hello 샘플 SQL 코드의 hello hello 도구 모음에서 모양 아이콘 밝게 hello 클릭 **SQL 파일** 탭 합니다.
3. Hello에 3 개의 탭된 결과 hello 확인 **결과 표** hello 가운데에 hello 페이지의 섹션입니다. 
4. 공지 hello **출력** hello hello 페이지 맨 아래에 목록입니다. 그러면 각 명령의 hello 상태가 표시 됩니다. 

이제 데이터베이스 tooAzure MySQL 워크 벤치를 사용 하 여 MySQL에 대 한 연결 하 고 hello SQL 언어를 사용 하 여 데이터를 쿼리 합니다.

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./concepts-migrate-import-export.md)
