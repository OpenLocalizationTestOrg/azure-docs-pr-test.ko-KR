---
title: "빠른 시작: Azure Database for MySQL 서버 만들기 - Azure Portal | Microsoft Docs"
description: "Azure 포털 tooquickly hello를 사용 하 여 단계별로이 문서의 단계는 약 5 분 후에 MySQL server에 대 한 샘플 Azure 데이터베이스를 만듭니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Azure Portal을 사용한 Azure Database for MySQL 서버 만들기
Azure에 대 한 MySQL 데이터베이스가 toorun 수 있는 관리 되는 서비스, 관리 하 고 hello 클라우드에서 MySQL 데이터베이스를 항상 사용 가능한 크기를 조정 합니다. 이 퀵 스타트의 toocreate Azure 데이터베이스 방법 hello Azure 포털을 사용 하 여 약 5 분 후에는 MySQL server에 대 한 보여 줍니다. 

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인
웹 브라우저를 열고 toohello [Microsoft Azure 포털](https://portal.azure.com/)합니다. 자격 증명 toosign toohello 포털에 입력 합니다. hello 기본 보기는 서비스 대시보드에.

## <a name="create-azure-database-for-mysql-server"></a>Azure Database for MySQL 서버 만들기
Azure Database for MySQL 서버는 정의된 [계산 및 저장소 리소스](./concepts-compute-unit-and-storage.md) 집합을 사용하여 만들어집니다. hello 서버 내에서 만든는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다.

이러한 단계 toocreate MySQL server에 대 한 Azure 데이터베이스를 수행 합니다.

1. Hello 클릭 **새로** 단추 (+) hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2. 선택 **데이터베이스** hello에서 **새로** 선택한 페이지 **MySQL에 대 한 Azure 데이터베이스** hello에서 **데이터베이스** 페이지. 입력할 수도 있습니다 **MySQL** hello 새 페이지 검색 상자 toofind hello 서비스에에서 있습니다.
![Azure Portal - 새로 만들기 - 데이터베이스 - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Hello 이미지 앞에 표시 된 대로 hello 새 서버 세부 정보 양식을 사용 hello 다음 정보를 입력 합니다.

    **설정** | **제안 값** | **필드 설명** 
    ---|---|---
    서버 이름 | myserver4demo | Azure Database for MySQL 서버를 식별하는 고유한 이름을 선택합니다. hello 도메인 이름 *mysql.database.azure.com* 를 tooconnect 응용 프로그램에 대해 제공한 추가 toohello 서버 이름입니다. hello 서버 이름에는 소문자, 숫자 및 hello 하이픈 (-) 문자를 포함 될 수 있습니다 및 3에서 63 자 사이 포함 해야 합니다.
    구독 | 사용자의 구독 | hello 서버에 대 한 toouse 되도록 Azure 구독. 여러 구독이 있는 경우는 hello 리소스에 대 한 요금이 청구 됩니다 hello 적절 한 구독을 선택 합니다.
    리소스 그룹 | myresourcegroup | 새 리소스 그룹 이름을 만들거나, 구독에서 기존 이름을 사용할 수 있습니다.
    서버 관리자 로그인 | myadmin | Toohello 서버에 연결 하는 경우 직접 로그인 계정 toouse를 확인 합니다. 'azure_superuser', '관리', '관리자', '루트', 'guest' 또는 'public' hello 관리자 로그인 이름 수 없습니다.
    암호 | *사용자 선택* | 서버 관리자 계정은 hello에 대 한 새 암호를 만듭니다. 8 too128 문자를 포함 해야 합니다. 암호는 hello 다음 범주 중 세 범주의 문자를 포함 해야-영어 대문자 문자, 영어 소문자, 숫자 (0-9) 및 영숫자가 아닌 문자 (!, $, #, % 등.).
    암호 확인 | *사용자 선택*| Hello 관리자 계정 암호를 확인 합니다.
    위치 | *hello 지역 가장 가까운 tooyour 사용자*| Hello 위치를 가장 가까운 tooyour 사용자 또는 다른 Azure 응용 프로그램을 선택 합니다.
    버전 | *Hello 최신 버전을 선택*| 특정 요구 사항이 있는 경우가 아니면 hello 최신 버전을 선택 합니다.
    가격 책정 계층 | **기본**, **50 Compute 단위** **50 GB** | 클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 데이터베이스에 대 한 합니다. 선택 **기본 계층** hello 탭 hello 위쪽에 있습니다. Hello의 왼쪽된 끝 hello 클릭 **단위 계산** 슬라이더 tooadjust hello 값 toohello 이상 금액 사용할 수 있는이 빠른 시작에 대 한 합니다. 클릭 **확인** toosave hello 가격 계층 선택 합니다. 다음 스크린 샷 hello를 참조 하십시오.
    Pin toodashboard | 확인 | Hello 확인 **Pin toodashboard** 옵션 tooallow 간편한 추적 서버의 Azure 포털의 hello 프런트 대시보드 페이지에 있습니다.

    > [!IMPORTANT]
    > hello 서버 관리자 로그인과 암호를 여기에서 지정한은 toohello 서버에서 필요한 toolog 및이 빠른 시작의 뒷부분에 나오는 해당 데이터베이스입니다. 나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.
    > 

    ![Azure 포털-MySQL 필요한 hello 양식 입력을 제공 하 여 만들기](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  클릭 **만들기** tooprovision hello 서버입니다. 최대 too20 분을 몇 분이 걸립니다 프로 비전.
   
5.  Hello 도구 모음에서 **알림** (종 모양 아이콘) toomonitor hello 배포 프로세스입니다.

## <a name="configure-a-server-level-firewall-rule"></a>서버 수준 방화벽 규칙 구성

MySQL 서비스에 대 한 Azure 데이터베이스 hello hello 서버 수준 방화벽을 만듭니다. 이 방화벽 방화벽 규칙은 특정 IP 주소에 대 한 tooopen hello 방화벽을 만들지 않은 toohello 서버 및 모든 데이터베이스 hello 서버에 연결 하지 못하도록 외부 응용 프로그램 및 도구 방지 합니다. 

1.  Hello 배포가 완료 된 후 서버를 찾습니다. 필요한 경우 검색할 수 있습니다. 예를 들어 클릭 **모든 리소스** hello 왼쪽 메뉴 및 hello 서버 이름에는 형식에서 (hello 예제와 같은 *myserver4demo*) toosearch 새로 만든된 서버에 대 한 합니다. Hello 검색 결과에 나열 된 서버 이름을 클릭 합니다. hello **개요** 페이지 서버 열리고 더 이상의 구성에 대 한 옵션을 제공 합니다.

2. Hello 서버 페이지에서 선택 **연결 보안**합니다.

3.  Hello에서 **방화벽 규칙** hello hello 빈 텍스트 상자에 머리글을 클릭 하 여 **규칙 이름** hello 방화벽 규칙을 만드는 열 toobegin 합니다. 

    이 빠른 시작 보겠습니다 hello 서버에 다음 값에는 hello로 각 열에 hello 텍스트 상자에 입력 하 여 모든 IP 주소를 허용 합니다.

    규칙 이름 | 시작 IP | 종료 IP 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Hello hello의 위쪽 도구 모음에서 **연결 보안** 페이지 **저장**합니다. 몇 분을 알리는 hello 알림을 계속 하기 전에 연결 보안 업데이트 성공적으로 완료가 표시를 기다립니다.

    > [!NOTE]
    > MySQL에 대 한 데이터베이스 연결 tooAzure 3306 포트를 통해 통신 합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 3306 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우 됩니다 수 tooconnect tooyour 서버 않으면 IT 부서 3306 포트를 엽니다.
    > 

## <a name="get-hello-connection-information"></a>Hello 연결 정보를 가져옵니다
tooconnect tooyour 데이터베이스 서버 tooremember hello 전체 서버 이름 및 관리자 로그인 자격 증명이 필요 합니다. Hello 퀵 스타트 문서의 앞부분에 나오는 값 기록한 수 있습니다. 설치 하지 않은 경우 쉽게 찾을 수 hello 서버 hello 서버에서 이름 및 로그인 정보 **개요** 페이지나 hello **속성** hello Azure 포털에서에서 페이지입니다.

1. 서버의 **개요** 페이지를 엽니다. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다. 
    각 필드 위에 커서를 올려서 및 hello 복사 아이콘 toohello 오른쪽 hello 텍스트에 나타납니다. 필요한 toocopy hello 값으로 hello 복사 아이콘을 클릭 합니다.

    이 예제에서는 hello 서버 이름은 *myserver4demo.mysql.database.azure.com*, hello 서버 관리자 로그인이 고  *myadmin@myserver4demo* 합니다.

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Mysql 명령줄 도구를 사용 하 여 tooMySQL 연결
여러 가지 응용 프로그램의 MySQL server에 대 한 tooconnect tooyour Azure 데이터베이스를 사용할 수 있습니다. Hello를 먼저 사용해 보겠습니다 [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) 명령줄 tooillustrate 어떻게 도구 tooconnect toohello 서버입니다.  웹 브라우저를 사용할 수 있습니다 및 hello hello 없이 여기에 설명 된 대로 Azure 클라우드 셸 tooinstall를 모든 추가 소프트웨어가 필요 합니다. 사용자의 컴퓨터에 로컬로 설치 하는 hello mysql 유틸리티를 사용 하도록 설정한 경우 여기 에서도 연결할 수 있습니다.

1. Hello 터미널 아이콘을 통해 Azure 클라우드 셸 hello 시작 (> _) hello에 hello Azure 포털의 웹 페이지의 오른쪽 위에 있습니다.

2. Azure 클라우드 셸 hello tootype bash 셸 명령을 사용 하면 브라우저에서 열립니다.

    ![명령 프롬프트 - mysql 명령줄 예](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. Hello 클라우드 셸 프롬프트에서 녹색 hello 프롬프트 hello mysql 명령줄을 입력 하 여 MySQL server에 대 한 tooyour Azure 데이터베이스를 연결 합니다.

    형식에 따라 hello은 MySQL 서버 hello mysql 유틸리티에 대 한 사용 되는 tooconnect tooan Azure 데이터베이스입니다.
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    예를 들어 다음 명령을 hello tooour 예제 서버를 연결 합니다.
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    mysql 매개 변수 |제안 값|설명
    ---|---|---
    --host | *서버 이름* | 이전 MySQL 용 hello Azure 데이터베이스를 만들 때 사용 된 hello 서버 이름 값을 지정 합니다. 표시된 예제 서버는 myserver4demo.mysql.database.azure.com입니다. Hello 정규화 된 도메인 이름 사용 (\*. mysql.database.azure.com) hello 예제에 나와 있는 것 처럼 합니다. 서버 이름을 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다. 
    --user | *서버 관리자 로그인 이름* |Hello 서버 관리자 로그인 사용자 이름 앞 MySQL 용 hello Azure 데이터베이스를 만들 때 제공 된 입력 합니다. Hello username 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다.  hello 형식은  *username@servername* 합니다.
    --password | *메시지가 표시될 때까지 대기* | 메시지가 표시 됩니다 너무 "후" 암호 입력 입력 hello 명령입니다. 메시지가 나타나면 입력 hello에 동일한 hello 서버를 만들 때 제공한 암호입니다.  참고 hello 문자에 표시 되지 않는 hello bash 프롬프트에 입력할 때 암호를 입력 합니다. 연결 하 고 모든 hello 문자 tooauthenticate를 입력 한 후 enter 키를 누릅니다.

   연결 되 면 hello mysql 유틸리티 표시는 `mysql>` 있습니다 tootype 명령을 확인 합니다. 

    mysql 출력의 예:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Hello 방화벽을 해제 하는 경우 구성의 hello Azure 클라우드 셸 tooallow hello IP 주소 hello 다음 오류가 발생 합니다.
    >
    > 오류 2003 (28000): 123.456.789.0 IP 주소를 사용 하 여 클라이언트 tooaccess hello 서버를 허용 되지 않습니다.
    >
    > tooresolve hello 오류를 확인 하는지 hello 서버 구성 일치 hello hello에서 단계 *서버 수준 방화벽 규칙 구성* hello 문서의 섹션.

4. 보기 서버 상태 tooensure hello 연결 기능이 작동 합니다. 형식 `status` hello mysql에서 >은 연결 되 면 메시지를 표시 합니다.
    ```sql
    status
    ```

   > [!TIP]
   > 다른 명령은 [MySQL 5.7 참조 설명서 - 4.5.1장](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)을 참조하세요.

5.  Hello mysql에서 새 데이터베이스 만들기 > hello 다음 명령을 입력 하 여 프롬프트:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    hello 명령에는 몇 분 정도의 toocomplete를 걸릴 수 있습니다. 

    Azure Database for MySQL 서버 내에서 하나 이상의 데이터베이스를 만들 수 있습니다. 모든 hello 리소스 toocreate 서버 tooutilize 당 단일 데이터베이스를 선택 하거나 여러 데이터베이스 tooshare hello 리소스를 만들 수 있습니다. 만들 수 있는 데이터베이스 수 없는 제한 toohello 이지만 hello를 공유 하는 여러 데이터베이스가 동일한 서버 리소스입니다. 

6. Hello hello mysql 데이터베이스 목록 > hello 다음 명령을 입력 하 여 프롬프트:

    ```sql
    SHOW DATABASES;
    ```

7.  형식 `\q` tooquit hello mysql 도구 ENTER를 누릅니다. 완료 한 후 Azure 클라우드 셸 hello를 닫을 수 있습니다.

이제 MySQL 용 toohello Azure 데이터베이스를 연결 하 고 빈 사용자 데이터베이스를 만들었습니다. 보았습니다. Toohello 다음 섹션 toorepeat 비슷한 연습 tooconnect toohello 계속 또 다른 일반적인 도구 MySQL 워크 벤치를 사용 하 여 동일한 서버입니다.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Toohello 서버 hello MySQL 워크 벤치 GUI 도구를 사용 하 여 연결
MySQL 워크 벤치 hello GUI 도구를 사용 하 여 tooconnect tooAzure MySQL 서버:

1.  Hello 클라이언트 컴퓨터에서 MySQL 워크 벤치 응용 프로그램을 시작 합니다. MySQL Workbench는 [여기](https://dev.mysql.com/downloads/workbench/)에서 다운로드할 수 있습니다.

2.  **새 연결을 설정** 대화 상자에 입력 다음 정보는 hello **매개 변수** 탭:

    ![새 연결 설정](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **설정** | **제안 값** | **필드 설명** |
    |---|---|---|
    |   연결 이름 | 데모 연결 | 이 연결에 대한 레이블을 지정합니다. |
    | 연결 방법 | 표준(TCP/IP) | 표준(TCP/IP)이면 충분합니다. |
    | 호스트 이름 | *서버 이름* | 이전 MySQL 용 hello Azure 데이터베이스를 만들 때 사용 된 hello 서버 이름 값을 지정 합니다. 표시된 예제 서버는 myserver4demo.mysql.database.azure.com입니다. Hello 정규화 된 도메인 이름 사용 (\*. mysql.database.azure.com) hello 예제에 나와 있는 것 처럼 합니다. 서버 이름을 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다.  |
    | 포트 | 3306 | 항상 3306 MySQL 용 tooAzure 데이터베이스를 연결할 때 포트를 사용 합니다. |
    | 사용자 이름 |  *서버 관리자 로그인 이름* | Hello 서버 관리자 로그인 사용자 이름 앞 MySQL 용 hello Azure 데이터베이스를 만들 때 제공 된 입력 합니다. 이 예제에서는 사용자 이름이 myadmin@myserver4demo입니다. Hello username 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다. hello 형식은  *username@servername* 합니다.
    | 암호 | 사용자 암호 | 클릭 하 여 자격 증명 모음에... 단추 toosave hello 암호 저장 합니다. |

    클릭 **연결 테스트** tootest 모든 매개 변수가 올바르게 구성 되어 있습니다. 확인 toosave hello 연결을 클릭 합니다. 

    > [!NOTE]
    > SSL 서버에 기본적으로 적용 됩니다 및 성공적으로 순서 tooconnect에 추가적인 구성이 필요 합니다. 참조 [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](./howto-configure-ssl.md)합니다.  이 빠른 시작에 대 한 SSL toodisable 원하는 hello Azure 포털을 방문 하 고 hello 연결 보안 페이지 toodisable hello 적용 SSL 연결 설정/해제 단추를 클릭 합니다.

## <a name="clean-up-resources"></a>리소스 정리
Hello 빠른 시작에서 만든 hello 리소스를 정리 하거나 삭제 하 여 hello [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md), 모든 hello 리소스 hello 리소스 그룹에 포함 된 또는 tookeep hello를 원하는 경우 hello 한 서버 리소스를 삭제 합니다. 기타 리소스 그대로 유지 합니다.

> [!TIP]
> 이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 구성됩니다. Toocontinue toowork 후속 사용 하려는 경우 퀵 스타트를 정리 하지 않습니다는이 빠른 시작에서 만든 리소스 hello 합니다. Toocontinue 않으려는 경우 모든 리소스를 만들 단계 toodelete hello Azure 포털에서에서이 빠른 시작에서 다음 hello를 사용 합니다.
>

새로 만든 hello 서버 뿐 아니라 toodelete hello 전체 리소스 그룹:
1.  Hello Azure 포털에서에서 리소스 그룹을 찾습니다. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 다음 예에서 같은 리소스 그룹의 hello 이름을 클릭 하 고 **myresourcegroup**합니다.
2.  리소스 그룹 페이지에서 **삭제**를 클릭합니다. 예제와 같은 리소스 그룹의 다음 유형 hello 이름을 **myresourcegroup**를 hello 텍스트 상자 tooconfirm 삭제 한 다음 클릭 **삭제**합니다.

또는 대신 toodelete hello 서버를 새로 만듭니다.
1.  하지 않은 경우 열었기 hello Azure 포털에서에서 서버를 찾습니다. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 합니다.
2.  Hello에 **개요** 페이지에서 hello **삭제** hello 위쪽 창에서 단추입니다.
![Azure Database for MySQL - 서버 삭제](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  영향을 받는 것에서 hello 데이터베이스 쿼리와 toodelete, 원하는 hello 서버 이름을 확인 합니다. 이 예제와 같은 hello 텍스트 상자에 서버 이름을 입력 **myserver4demo**, 클릭 하 고 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [첫 번째 Azure Database for MySQL 데이터베이스 디자인](./tutorial-design-database-using-portal.md)

