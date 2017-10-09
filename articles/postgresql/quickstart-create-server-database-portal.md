---
title: "Azure Portal: PostgreSQL용 Azure Database 만들기 | Microsoft Docs"
description: "빠른 시작 가이드 toocreate 하 고 Azure 포털 사용자 인터페이스를 사용 하 여 PostgreSQL 서버에 대 한 Azure 데이터베이스를 관리 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: quickstart
ms.date: 08/10/2017
ms.openlocfilehash: 61753268147d6ea283d1aa5d6baf269d2756d25a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-in-hello-azure-portal"></a>Hello Azure 포털에서에서 PostgreSQL에 대 한 Azure 데이터베이스 만들기

Azure에 대 한 PostgreSQL 데이터베이스가 toorun 수 있는 관리 되는 서비스, 관리 하 고 hello 클라우드에서 항상 사용 가능한 PostgreSQL 데이터베이스의 크기를 조정 합니다. 이 퀵 스타트의 toocreate Azure 데이터베이스 방법 PostgreSQL 서버 hello Azure 포털을 사용 하 여 약 5 분 내에 표시 됩니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인
웹 브라우저를 열고 toohello [Microsoft Azure 포털](https://portal.azure.com/)합니다. 자격 증명 toosign toohello 포털에 입력 합니다. hello 기본 보기는 서비스 대시보드에.

## <a name="create-an-azure-database-for-postgresql"></a>PostgreSQL용 Azure Database 만들기

Azure Database for PostgreSQL 서버는 정의된 [계산 및 저장소 리소스](./concepts-compute-unit-and-storage.md) 집합으로 만들어집니다. hello 서버 내에서 만든는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다.

이러한 단계 toocreate PostgreSQL 서버에 대 한 Azure 데이터베이스를 수행 합니다.
1.  Hello 클릭 **새로** 단추 (+) hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.
2.  선택 **데이터베이스** hello에서 **새로** 선택한 페이지 **Azure PostgreSQL 데이터베이스** hello에서 **데이터베이스** 페이지.
 ![Azure 데이터베이스 PostgreSQL-에 대 한 hello 데이터베이스 만들기](./media/quickstart-create-database-portal/1-create-database.png)

3.  Hello 이미지 앞에 표시 된 대로 hello 새 서버 세부 정보 양식을 사용 hello 다음 정보를 입력 합니다.

    설정|제안 값|설명
    ---|---|---
    서버 이름 |*mypgserver-20170401*|Azure Database for PostgreSQL 서버를 식별하는 고유한 이름을 선택합니다. hello 도메인 이름 *postgres.database.azure.com* 를 tooconnect 응용 프로그램에 대해 제공한 추가 toohello 서버 이름입니다. hello 서버 이름에는 소문자, 숫자 및 hello 하이픈 (-) 문자를 포함 될 수 있습니다 및 3에서 63 자 사이 포함 해야 합니다.
    구독|*사용자의 구독*|hello 서버에 대 한 toouse 되도록 Azure 구독. 여러 구독이 있는 경우는 hello 리소스에 대 한 요금이 청구 됩니다 hello 적절 한 구독을 선택 합니다.
    리소스 그룹|*myresourcegroup*| 새 리소스 그룹 이름을 만들거나, 구독에서 기존 이름을 사용할 수 있습니다.
    서버 관리자 로그인 |*mylogin*| Toohello 서버에 연결 하는 경우 직접 로그인 계정 toouse를 확인 합니다. hello 관리자 로그인 이름 'azure_superuser', 'azure_pg_admin', '관리', '관리자', '루트', 'guest' 또는 'public' 일 수 없습니다 및 'pg_'로 시작할 수 없습니다.
    암호 |*사용자 선택* | 서버 관리자 계정은 hello에 대 한 새 암호를 만듭니다. 8 too128 문자를 포함 해야 합니다. 암호는 hello 다음 범주 중 세 범주의 문자를 포함 해야-영어 대문자 문자, 영어 소문자, 숫자 (0-9) 및 영숫자가 아닌 문자 (!, $, #, % 등.).
    위치|*hello 지역 가장 가까운 tooyour 사용자*| 가장 가까운 tooyour 사용자 hello 위치를 선택 합니다.
    PostgreSQL 버전|*Hello 최신 버전을 선택*| 특정 요구 사항이 있는 경우가 아니면 hello 최신 버전을 선택 합니다.
    가격 책정 계층 | **기본**, **50 Compute 단위** **50 GB** | 클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 데이터베이스에 대 한 합니다. Hello 위쪽 hello 탭에서 기본 계층을 선택 합니다. Hello 단위 계산 슬라이더 tooadjust hello 값 toohello의 왼쪽된 끝 hello 클릭이 빠른 시작에 사용할 수 있는 최소 크기입니다. 클릭 **확인** toosave hello 가격 계층 선택 합니다. 다음 스크린 샷 hello를 참조 하십시오.
    | Pin toodashboard | 확인 | Hello 확인 **Pin toodashboard** 옵션 tooallow 간편한 추적 서버의 Azure 포털의 hello 프런트 대시보드 페이지에 있습니다.

  > [!IMPORTANT]
  > 여기서 지정 하는 hello 서버 관리자 로그인 및 암호는 toohello 서버에서 필요한 toolog와이 빠른 시작의 뒷부분에 나오는 해당 데이터베이스. 나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.

    ![PostgreSQL-가격 책정 계층 선택 hello에 대 한 azure 데이터베이스](./media/quickstart-create-database-portal/2-service-tier.png)

4.  클릭 **만들기** tooprovision hello 서버입니다. 최대 too20 분을 몇 분이 걸립니다 프로 비전.

5.  Hello 도구 모음에서 **알림** toomonitor hello 배포 프로세스입니다.
 ![PostgreSQL용 Azure Database - 알림 확인](./media/quickstart-create-database-portal/3-notifications.png)
   
  기본적으로 **postgres** 데이터베이스가 서버 아래에 만들어집니다. hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 데이터베이스는 사용자, 유틸리티 및 타사 응용 프로그램에서 사용 하기 위해 의미 하는 기본 데이터베이스입니다. 

## <a name="configure-a-server-level-firewall-rule"></a>서버 수준 방화벽 규칙 구성

hello Azure 데이터베이스 PostgreSQL 서비스에 대 한 hello 서버 수준 방화벽을 만듭니다. 이 방화벽 방화벽 규칙은 특정 IP 주소에 대 한 tooopen hello 방화벽을 만들지 않은 toohello 서버 및 모든 데이터베이스 hello 서버에 연결 하지 못하도록 외부 응용 프로그램 및 도구 방지 합니다. 

1.  Hello 배포가 완료 된 후 서버를 찾습니다. 필요한 경우 검색할 수 있습니다. 예를 들어 클릭 **모든 리소스** hello 왼쪽 메뉴 및 hello 서버 이름에는 형식에서 (hello 예제와 같은 *mypgserver 20170401*) toosearch 새로 만든된 서버에 대 한 합니다. Hello 검색 결과에 나열 된 서버 이름을 클릭 합니다. hello **개요** 페이지 서버 열리고 더 이상의 구성에 대 한 옵션을 제공 합니다.
 
    ![Azure Database for PostgreSQL - 서버 이름 검색](./media/quickstart-create-database-portal/4-locate.png)

2.  Hello 서버 페이지에서 선택 **연결 보안**합니다. 
    ![Azure Database for PostgreSQL - 방화벽 규칙 만들기](./media/quickstart-create-database-portal/5-firewall-2.png)

3.  Hello에서 **방화벽 규칙** hello hello 빈 텍스트 상자에 머리글을 클릭 하 여 **규칙 이름** hello 방화벽 규칙을 만드는 열 toobegin 합니다. 

    이 빠른 시작 해 보겠습니다 hello 서버에 다음 값에는 hello로 각 열에 hello 텍스트 상자에 입력 하 여 모든 IP 주소를 허용 합니다.

    규칙 이름 | 시작 IP | 종료 IP 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Hello hello 연결 보안 페이지의 위쪽 도구 모음에서 클릭 **저장**합니다. 몇 분을 알리는 hello 알림을 계속 하기 전에 연결 보안 업데이트 성공적으로 완료가 표시를 기다립니다.

    > [!NOTE]
    > PostgreSQL 서버에 대 한 Azure 데이터베이스 연결 tooyour 5432 포트를 통해 통신 합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 5432 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우 됩니다 수 tooconnect tooyour 서버 않으면 IT 부서 5432 포트를 엽니다.
    >

## <a name="get-hello-connection-information"></a>Hello 연결 정보를 가져옵니다

Azure Database for PostgreSQL 서버를 만들 때 **postgres**라는 기본 데이터베이스도 만들어집니다. tooconnect tooyour 데이터베이스 서버 tooremember hello 전체 서버 이름 및 관리자 로그인 자격 증명이 필요 합니다. Hello 퀵 스타트 문서의 앞부분에 나오는 값 기록한 수 있습니다. 설치 하지 않은 경우 hello Azure 포털에서에서 hello 서버 개요 페이지에서 hello 서버 이름 및 로그인 정보를 쉽게 찾을 수 있습니다.

1. 서버의 **개요** 페이지를 엽니다. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
    각 필드 위에 커서를 올려서 및 hello 복사 아이콘 toohello 오른쪽 hello 텍스트에 나타납니다. 필요한 toocopy hello 값으로 hello 복사 아이콘을 클릭 합니다.

 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/quickstart-create-database-portal/6-server-name.png)

## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a>Psql를 사용 하 여 클라우드 셸에서 tooPostgreSQL 데이터베이스 연결

여러 가지 응용 프로그램의 PostgreSQL 서버에 대 한 tooconnect tooyour Azure 데이터베이스를 사용할 수 있습니다. 먼저 사용 hello psql 명령줄 유틸리티 tooillustrate 어떻게 tooconnect toohello 서버입니다.  웹 브라우저를 사용할 수 있습니다 및 hello hello 없이 여기에 설명 된 대로 Azure 클라우드 셸 tooinstall를 모든 추가 소프트웨어가 필요 합니다. 사용자의 컴퓨터에 로컬로 설치 하는 hello psql 유틸리티를 사용 하도록 설정한 경우 여기 에서도 연결할 수 있습니다.

1. Hello 위쪽 탐색 창에서 hello 터미널 아이콘을 통해 Azure 클라우드 셸 hello를 시작 합니다.

   ![PostgreSQL용 Azure Database - Azure Cloud Shell 터미널 아이콘](./media/quickstart-create-database-portal/7-cloud-console.png)

2. Azure 클라우드 셸 hello tootype bash 셸 명령을 사용 하면 브라우저에서 열립니다.

   ![PostgreSQL용 Azure Database - Azure Shell Bash 프롬프트](./media/quickstart-create-database-portal/8-bash.png)

3. Hello 클라우드 셸 프롬프트에서 녹색 hello 프롬프트 hello psql 명령줄을 입력 하 여 PostgreSQL 서버에 대 한 Azure 데이터베이스에 tooa 데이터베이스를 연결 합니다.

    hello 다음 형식이 사용 되는 tooconnect tooan Azure 데이터베이스 hello로 PostgreSQL 서버에 대 한 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티:
    ```bash
    psql --host=<yourserver> --port=<port> --username=<server admin login> --dbname=<database name>
    ```

    예를 들어 다음 명령을 hello tooan 예제 서버를 연결 합니다.

    ```bash
    psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
    ```

    psql parameter |제안 값|설명
    ---|---|---
    --host | *서버 이름* | 이전 PostgreSQL에 대 한 hello Azure 데이터베이스를 만들 때 사용 된 hello 서버 이름 값을 지정 합니다. 표시된 예제 서버는 mypgserver-20170401.postgres.database.azure.com입니다. Hello 정규화 된 도메인 이름 사용 (\*. postgres.database.azure.com) hello 예제에 나와 있는 것 처럼 합니다. 서버 이름을 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다. 
    --port | **5432** | 항상 5432 PostgreSQL에 대 한 tooAzure 데이터베이스를 연결할 때 포트를 사용 합니다. 
    --username | *서버 관리자 로그인 이름* |Hello 서버 관리자 로그인 사용자 이름 앞 PostgreSQL에 대 한 hello Azure 데이터베이스를 만들 때 제공 된 입력 합니다. Hello username 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다.  hello 형식은  *username@servername* 합니다.
    --dbname | **postgres** | 사용 하 여 hello 기본 생성 된 시스템 데이터베이스 이름은 *postgres* hello 첫 번째 연결에 대 한 합니다. 나중에 데이터베이스를 직접 만듭니다.

    Hello psql 명령을 실행 한 후 매개 변수 값을 사용 하 여 직접 됩니다 증명된 tootype hello 서버 관리자 암호. 이 암호는 hello 서버를 만들 때 제공한 동일한 hello 됩니다. 

    psql parameter |제안 값|설명
    ---|---|---
    암호 | *관리자 암호* | 입력 한 암호 문자에 표시 되지 않는 hello bash 프롬프트 hello 하십시오. 연결 하 고 모든 hello 문자 tooauthenticate를 입력 한 후 enter 키를 누릅니다.

    연결 되 면 hello psql 유틸리티는 sql 명령을 입력할 postgres 프롬프트를 표시 합니다. Hello 초기 연결 출력에 hello psql hello Azure 클라우드 Shell에서에서 서로 다른 버전인 PostgreSQL 서버 버전에 대 한 hello Azure 데이터베이스 일 수 있으므로 경고가 표시 될 수 있습니다. 
    
    psql 출력의 예:
    ```bash
    psql (9.5.7, server 9.6.2)
    WARNING: psql major version 9.5, server major version 9.6.
        Some psql features might not work.
    SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
    Type "help" for help.
   
    postgres=> 
    ```

    > [!TIP]
    > Hello 방화벽을 해제 하는 경우 구성의 hello Azure 클라우드 셸 tooallow hello IP 주소 hello 다음 오류가 발생 합니다.
    > 
    > "psql: FATAL:  no pg_hba.conf entry for host "138.91.195.82", user "mylogin", database "postgres", SSL on FATAL:  SSL connection is required. SSL 옵션을 지정하고 다시 시도하십시오.
    > 
    > tooresolve hello 오류를 확인 하는지 hello 서버 구성 일치 hello hello에서 단계 *서버 수준 방화벽 규칙 구성* hello 문서의 섹션.

4.  빈 데이터베이스를 만듭니다 hello에 프롬프트 hello 다음 명령을 입력 하 여:
    ```bash
    CREATE DATABASE mypgsqldb;
    ```
    hello 명령에는 몇 분 정도의 toocomplete를 걸릴 수 있습니다. 

5.  Hello 프롬프트에서 실행 명령을 tooswitch 연결 toohello 새로 만든 데이터베이스를 다음 hello **mypgsqldb**합니다.
    ```bash
    \c mypgsqldb
    ```

6.  \Q를 입력 하 고 tooquit psql ENTER 키를 누릅니다. 완료 한 후 Azure 클라우드 셸 hello를 닫을 수 있습니다.

이제 PostgreSQL 위해 toohello Azure 데이터베이스를 연결 하 고 빈 사용자 데이터베이스를 만들었습니다. 보았습니다. Toohello 다음 섹션 tooconnect pgAdmin 다른 일반적인 도구를 사용 하 여 계속 합니다.

## <a name="connect-toopostgresql-database-using-pgadmin"></a>PgAdmin를 사용 하 여 tooPostgreSQL 데이터베이스 연결

hello GUI 도구를 사용 하 여 tooconnect tooAzure PostgreSQL 서버 _pgAdmin_
1.  Hello 시작 _pgAdmin_ 클라이언트 컴퓨터에 응용 프로그램입니다. _pgAdmin_은 http://www.pgadmin.org/에서 설치할 수 있습니다.
2.  Hello 클릭 **새 서버 추가** hello에서 아이콘 **빠른 링크** hello 센터 hello 대시보드 페이지의 섹션입니다.
3.  Hello에 **서버 만들기-** 대화 상자 **일반** 탭에서 같은 hello 서버에 대 한 고유 이름을 입력 **Azure PostgreSQL 서버**합니다.
![pgAdmin 도구 - 만들기 - 서버](./media/quickstart-create-database-portal/9-pgadmin-create-server.png)
4.  Hello에 **서버 만들기-** 대화 상자, **연결** hello 설정을 사용 하 여 지정 된 대로 탭을 클릭 **저장**합니다.
   ![pgAdmin - 만들기 - 서버](./media/quickstart-create-database-portal/10-pgadmin-create-server.png)

    pgAdmin 매개 변수 |제안 값|설명
    ---|---|---
    호스트 이름/주소 | *서버 이름* | 이전 PostgreSQL에 대 한 hello Azure 데이터베이스를 만들 때 사용 된 hello 서버 이름 값을 지정 합니다. 표시된 예제 서버는 mypgserver-20170401.postgres.database.azure.com입니다. Hello 정규화 된 도메인 이름 사용 (\*. postgres.database.azure.com) hello 예제에 나와 있는 것 처럼 합니다. 서버 이름을 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다. 
    포트 | **5432** | 항상 5432 PostgreSQL에 대 한 tooAzure 데이터베이스를 연결할 때 포트를 사용 합니다.  
    데이터베이스 유지 관리 | **postgres** | 사용 하 여 hello 기본 생성 된 시스템 데이터베이스 이름은 *postgres*합니다.
    사용자 이름 | *서버 관리자 로그인 이름* | Hello 서버 관리자 로그인 사용자 이름 앞 PostgreSQL에 대 한 hello Azure 데이터베이스를 만들 때 제공 된 입력 합니다. Hello username 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다. hello 형식은  *username@servername* 합니다.
    암호 | *관리자 암호* |  hello 암호가 빠른이 시작의 앞부분에 나오는 hello 서버를 만들 때 선택한 있습니다.
    역할 | *비워 둠* | 더 필요 tooprovide 역할 이름을 시점에서 합니다. Hello 필드를 비워 둡니다.
    SSL 모드 | 필요 | 기본적으로 모든 Azure PostgreSQL 서버는 SSL을 실행한 상태에서 만들어집니다.  SSL 적용 해제 tooturn 세부 사항을 볼 [적용 SSL](./concepts-ssl-connection-security.md)합니다.
    
5.  **Save**를 클릭합니다.
6.  Hello 브라우저 왼쪽된 창에서 확장 hello **서버** 노드. 예를 들어 서버를 선택 **Azure PostgreSQL 서버** tooconnect tooit를 클릭 합니다.
7. Hello 서버 노드를 확장 한 다음 확장 **데이터베이스** 그 아래에서 합니다. hello 목록에 포함 되어야 기존 *postgres* 데이터베이스와 새로 만든된 모든 사용자 데이터베이스와 같은 *mypgsqldb*, hello 이전 섹션에서 만든 합니다. Azure Database for PostgreSQL에서는 서버당 여러 데이터베이스를 만들 수 있습니다.
8. 마우스 오른쪽 단추로 클릭 **데이터베이스**, hello 선택 **만들기** 메뉴를 **데이터베이스**합니다.
9.  Hello에 선택한 데이터베이스 이름을 입력 **데이터베이스** 필드와 같은 *mypgsqldb* hello 예제에 나와 있습니다. 
10. 선택 hello **소유자** hello 드롭다운 목록 상자에서 hello 데이터베이스에 대 한 합니다. 서버 관리자 로그인 이름(예: *mylogin*)을 선택합니다.
10. 클릭 **저장** toocreate 새 데이터베이스를 합니다.
11. Hello에 **브라우저** 창 hello에서 만든 데이터베이스를 데이터베이스 목록이 hello 서버 이름 아래를 참조 하십시오.
 ![pgAdmin - 만들기 - 데이터베이스](./media/quickstart-create-database-portal/11-pgadmin-database.png)


## <a name="clean-up-resources"></a>리소스 정리
Hello 빠른 시작에서 만든 hello 리소스를 정리 하거나 삭제 하 여 hello [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md), 모든 hello 리소스 hello 리소스 그룹에 포함 된 또는 tookeep hello를 원하는 경우 hello 한 서버 리소스를 삭제 합니다. 기타 리소스 그대로 유지 합니다.

> [!TIP]
> 이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 구성됩니다. Toocontinue toowork 후속 사용 하려는 경우 퀵 스타트를 정리 하지 않습니다는이 빠른 시작에서 만든 리소스 hello 합니다. Toocontinue 않으려는 경우 다음이 퀵 스타트의 hello Azure 포털에에서 의해 생성 된 단계 toodelete 리소스 hello를 사용 합니다.

새로 만든 hello 서버 뿐 아니라 toodelete hello 전체 리소스 그룹:
1.  Hello Azure 포털에서에서 리소스 그룹을 찾습니다. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 다음 예에서 같은 리소스 그룹의 hello 이름을 클릭 하 고 **myresourcegroup**합니다.
2.  리소스 그룹 페이지에서 **삭제**를 클릭합니다. 예제와 같은 리소스 그룹의 다음 유형 hello 이름을 **myresourcegroup**를 hello 텍스트 상자 tooconfirm 삭제 한 다음 클릭 **삭제**합니다.

또는 대신 toodelete hello 서버를 새로 만듭니다.
1.  하지 않은 경우 열었기 hello Azure 포털에서에서 서버를 찾습니다. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 합니다.
2.  Hello에 **개요** 페이지에서 hello **삭제** hello 위쪽 창에서 단추입니다.
![Azure Database for PostgreSQL - 서버 삭제](./media/quickstart-create-database-portal/12-delete.png)
3.  영향을 받는 것에서 hello 데이터베이스 쿼리와 toodelete, 원하는 hello 서버 이름을 확인 합니다. 이 예제와 같은 hello 텍스트 상자에 서버 이름을 입력 **mypgserver 20170401**, 클릭 하 고 **삭제**합니다.

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
