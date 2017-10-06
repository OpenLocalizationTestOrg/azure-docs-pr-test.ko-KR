---
title: "MySQL 데이터베이스-Azure 포털에 대 한 첫 번째 Azure 데이터베이스 aaaDesign | Microsoft Docs"
description: "이 자습서에 설명 어떻게 toocreate MySQL server에 대 한 Azure 데이터베이스 관리 및 Azure 포털을 사용 하 여 데이터베이스입니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>첫 번째 Azure Database for MySQL 데이터베이스 디자인
Azure에 대 한 MySQL 데이터베이스가 toorun 수 있는 관리 되는 서비스, 관리 하 고 hello 클라우드에서 MySQL 데이터베이스를 항상 사용 가능한 크기를 조정 합니다. Hello Azure 포털을 사용 하 여 쉽게 서버를 관리 하 고 수 데이터베이스 디자인 합니다.

이 자습서를 사용 하 여 Azure 포털 toolearn hello 어떻게에:

> [!div class="checklist"]
> * Azure Database for MySQL 만들기
> * Hello 서버 방화벽을 구성
> * Mysql 명령줄 도구 toocreate 데이터베이스를 사용 하 여
> * 샘플 데이터 로드
> * 쿼리 데이터
> * 데이터 업데이트
> * 데이터 복원

## <a name="sign-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인
즐겨 찾는 웹 브라우저를 열고 hello 방문 [Microsoft Azure 포털](https://portal.azure.com/)합니다. 자격 증명 toosign toohello 포털에 입력 합니다. hello 기본 보기는 서비스 대시보드에.

## <a name="create-an-azure-database-for-mysql-server"></a>Azure Database for MySQL 서버 만들기
Azure Database for MySQL 서버는 정의된 [계산 및 저장소 리소스](./concepts-compute-unit-and-storage.md) 집합을 사용하여 만들어집니다. hello 서버 내에서 만든는 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)합니다.

1. 너무 이동**데이터베이스** > **MySQL에 대 한 Azure 데이터베이스**합니다. MySQL 서버를 찾을 수 없는 경우 **데이터베이스** 범주를 클릭 하 여 **스크롤하게** tooshow 사용 가능한 모든 데이터베이스 서비스입니다. 입력할 수도 있습니다 **MySQL에 대 한 Azure 데이터베이스** hello 검색 상자 tooquickly에서 hello 서비스를 찾습니다.
![2-1 탐색 tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. **MySQL용 Azure Database** 타일을 클릭한 다음 **만들기**를 클릭합니다.

예제에서는 다음 정보는 hello로 MySQL 폼에 대 한 hello Azure 데이터베이스를 입력 합니다.

| **설정** | **제안 값** | **필드 설명** |
|---|---|---|
| *서버 이름* | myserver4demo  | 서버 이름에 toobe 전역적으로 고유 합니다. |
| *구독* | mysubscription | Hello 드롭다운 목록에서 구독을 선택 합니다. |
| *리소스 그룹* | myresourcegroup | 리소스 그룹을 만들거나 기존 그룹을 사용합니다. |
| *서버 관리자 로그인* | myadmin | 관리자 계정 이름을 설정합니다. |
| *암호* |  | 강력한 관리자 계정 암호를 설정합니다. |
| *암호 확인* |  | Hello 관리자 계정 암호를 확인 합니다. |
| *위치* |  | 사용 가능한 지역을 선택합니다. |
| *버전* | 5.7 | Hello 최신 버전을 선택 합니다. |
| *성능 구성* | 기본, 50 계산 단위, 50GB  | **가격 책정 계층**, **계산 단위**, **저장소(GB)**를 선택한 다음 **확인**을 클릭합니다. |
| *Pin tooDashboard* | 확인 | 나중에 쉽게 hello 서버를 찾을 수 있도록이 상자 toocheck 권장 |
그런 다음에 **만들기**를 클릭합니다. 2 분 정도로에서 MySQL server에 대 한 새 Azure 데이터베이스 hello 클라우드에서 제거할 수 없습니다. 클릭할 수 있는 **알림** hello 도구 모음 toomonitor hello 배포 프로세스에는 단추입니다.

## <a name="configure-firewall"></a>방화벽 구성
Azure Databases for MySQL은 방화벽으로 보호됩니다. 기본적으로 모든 연결 toohello 서버와 hello 데이터베이스 hello 서버 내부에서 거부 됩니다. 데이터베이스 tooAzure MySQL hello에 대 한 처음으로 연결 하기 전에 hello 방화벽 tooadd hello 클라이언트 컴퓨터의 공용 네트워크 IP 주소 (또는 IP 주소 범위)를 구성 합니다.

1. 새로 만든 서버를 클릭한 다음 **연결 보안**을 클릭합니다.
   ![3-1 연결 보안](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. **내 IP를 추가**하거나 여기서 방화벽 규칙을 구성할 수 있습니다. Tooclick 기억 **저장** hello 규칙을 만든 후 합니다.
Mysql 명령줄 도구 또는 MySQL 워크 벤치 GUI 도구를 사용 하 여 toohello 서버를 연결할 수 있습니다.

> [!TIP]
> Azure Databases for MySQL 서버는 3306 포트를 통해 통신합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 3306 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우에 IT 부서 3306 포트를 엽니다. 하지 않는 한 tooAzure MySQL 서버를 연결할 수 없습니다.

## <a name="get-connection-information"></a>연결 정보 가져오기
정규화 된 get hello **서버 이름** 및 **서버 관리자 로그인 이름** hello Azure 포털에서에서 MySQL 서버에 대 한 Azure 데이터베이스에 대 한 합니다. Mysql 명령줄 도구를 사용 하 여 hello 정규화 된 서버 이름 tooconnect tooyour 서버를 사용 합니다. 

1. [Azure 포털](https://portal.azure.com/), 클릭 **모든 리소스** hello 왼쪽 메뉴, 형식 hello 이름 및 MySQL 서버에 대 한 Azure 데이터베이스에 대 한 검색 합니다. Hello 서버 이름 tooview hello 세부 정보를 선택 합니다.

2. Hello 설정에서 머리글을 클릭 하 여 **속성**합니다. **서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다. Hello 단추 다음 tooeach 필드 toocopy toohello 클립보드로 복사를 클릭할 수 있습니다.
   ![4-2 서버 속성](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

이 예제에서는 hello 서버 이름은 *myserver4demo.mysql.database.azure.com*, hello 서버 관리자 로그인이 고  *myadmin@myserver4demo* 합니다.

## <a name="connect-toohello-server-using-mysql"></a>Mysql을 사용 하 여 toohello 서버 연결
사용 하 여 [mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish MySQL server에 대 한 연결 tooyour Azure 데이터베이스입니다. Hello 브라우저에서 Azure 클라우드 셸 hello 또는 로컬로 설치 된 mysql 도구를 사용 하 여 사용자의 컴퓨터에서 hello mysql 명령줄 도구를 실행할 수 있습니다. toolaunch hello Azure 클라우드 셸 클릭 hello `Try It` 이 문서에 있는 코드 블록에 단추 또는 hello Azure 포털을 방문 하 고 hello 클릭 `>_` hello 맨 위의 오른쪽 도구 모음에서 아이콘입니다. 

Hello 명령 tooconnect를 입력 합니다.
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>빈 데이터베이스 만들기
을 사용 하는 연결 된 toohello 서버와 새 데이터베이스 toowork 만들.
```sql
CREATE DATABASE mysampledb;
```

Hello 프롬프트 hello 명령 tooswitch 연결 toothis 새로 만든 데이터베이스를 다음을 실행 합니다.
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Hello 데이터베이스에서 테이블 만들기
배웠으므로 어떻게 tooconnect toohello MySQL 데이터베이스에 대 한 Azure 데이터베이스, 해 볼 수 있습니다 방법을 보다 toocomplete 몇 가지 기본적인 작업 합니다.

먼저 테이블을 만들고 일부 데이터와 함께 로드할 수 있습니다. 인벤토리 정보를 저장하는 테이블을 만들어 보겠습니다.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Hello 테이블로 데이터를 로드 합니다.
이제 테이블을 만들었으므로 이 테이블에 일부 데이터를 삽입할 수 있습니다. Hello open 명령 프롬프트 창에서 데이터의 일부 행 hello 쿼리 tooinsert 다음 실행 합니다.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

이제 두 개의 행 앞에서 만든 hello 테이블에 샘플 데이터의 해야 합니다.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Hello 테이블의 hello 데이터 쿼리 및 업데이트
Hello 쿼리 tooretrieve 정보 hello 데이터베이스 테이블에서 다음을 실행 합니다.
```sql
SELECT * FROM inventory;
```

Hello 테이블의 hello 데이터를 업데이트할 수 있습니다.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

hello 행이 데이터를 검색 하는 경우 그에 따라 업데이트를 가져옵니다.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>데이터베이스 tooa 이전 시점으로 복원
실수로 중요 한 데이터베이스 테이블을 삭제 하 고 hello 데이터를 쉽게 복구할 수 없습니다 가정해 보세요. Azure 데이터베이스 MySQL에 대 한를 통해 toorestore hello 서버 tooa 지점 시간 내에 새 서버에 hello 데이터베이스의 복사본을 만들어야 합니다. 이 새 서버 toorecover 삭제 된 데이터를 사용할 수 있습니다. hello 표를 추가 하기 전에 단계 복원 hello 샘플 서버 tooa 지점 뒤 번호입니다.

1. Hello Azure 포털에서에서 MySQL에 대 한 Azure 데이터베이스를 찾습니다. Hello에 **개요** 페이지 **복원** hello 도구 모음입니다. hello 복원 페이지가 열립니다.

   ![10-1 데이터베이스 복원](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Hello 채울 **복원** hello 필요한 정보가 포함 된 폼입니다.
   
   ![10-2 복원 양식](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **복원 지점**:에-시간, 나열 된 hello 정해진 toorestore 한다는 것을 선택 합니다. 현지 표준 시간대 tooUTC tooconvert 있는지를 확인 합니다.
   - **Toonew 서버 복원**: toorestore을 원하는 새 서버 이름을 제공 합니다.
   - **위치**: hello 영역이 hello 원본 서버와 동일한 되 고 변경할 수 없습니다.
   - **가격 책정 계층**: 가격 책정 계층 hello는 hello 원본 서버를 hello와 동일 하며 변경할 수 없습니다.
   
3. 클릭 **확인** toorestore hello 서버 너무[복원 tooa 지정 시간으로](./howto-restore-server-portal.md) 전에 hello 테이블을 삭제 합니다. 서버 복원의 hello 서버 hello 시간 기준으로 지정한 새 복사본을 만듭니다. 

## <a name="next-steps"></a>다음 단계
이 자습서를 사용 하 여 Azure 포털 toolearned hello 어떻게에:

> [!div class="checklist"]
> * Azure Database for MySQL 만들기
> * Hello 서버 방화벽을 구성
> * Mysql 명령줄 도구 toocreate 데이터베이스를 사용 하 여
> * 샘플 데이터 로드
> * 쿼리 데이터
> * 데이터 업데이트
> * 데이터 복원

> [!div class="nextstepaction"]
> [MySQL에 대 한 응용 프로그램 tooAzure tooconnect 데이터베이스 하는 방법](./howto-connection-string.md)
