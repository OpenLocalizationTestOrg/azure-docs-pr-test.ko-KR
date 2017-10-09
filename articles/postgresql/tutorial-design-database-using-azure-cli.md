---
title: "Azure CLI를 사용하여 첫 번째 Azure Database for PostgreSQL 디자인 | Microsoft Docs"
description: "이 자습서에서는 Azure CLI를 사용 하 여 tooDesign 첫 번째 Azure 데이터베이스에 대 한 PostgreSQL 보여 줍니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Azure CLI를 사용하여 Azure Database for PostgreSQL을 디자인합니다 
이 자습서를 사용 하 여 Azure CLI (명령줄 인터페이스) 및 기타 유틸리티 toolearn 어떻게에:
> [!div class="checklist"]
> * PostgreSQL용 Azure Database 만들기
> * Hello 서버 방화벽을 구성
> * 사용 하 여 [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티 toocreate 데이터베이스
> * 샘플 데이터 로드
> * 쿼리 데이터
> * 데이터 업데이트
> * 데이터 복원

Hello 브라우저에서 Azure 클라우드 셸 hello를 사용할 수 있습니다 또는 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli) 이 자습서에서 자신의 컴퓨터 toorun hello 코드 블록에 있습니다.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

여러 구독이 있는 경우 hello 리소스 존재 하거나에 대 한 청구 hello 적절 한 구독을 선택 합니다. [az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기
만들기는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello를 사용 하 여 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. 리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myresourcegroup` hello에 `westus` 위치 합니다.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>PostgreSQL용 Azure Database 서버 만들기
만들기는 [PostgreSQL 서버에 대 한 Azure 데이터베이스](overview.md) hello를 사용 하 여 [az postgres 서버 만들](/cli/azure/postgres/server#create) 명령입니다. 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다. 

hello 다음 예제에서는 라고 하는 서버 `mypgserver-20170401` 리소스 그룹에서 `myresourcegroup` 서버 관리자 로그인과 `mylogin`합니다. 서버 이름을 tooDNS 이름을 매핑하고 필요한 toobe Azure에서 전역적으로 고유 합니다. 대체 hello `<server_admin_password>` 고유한 값을 사용 합니다.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> 여기서 지정 하는 hello 서버 관리자 로그인 및 암호는 toohello 서버에서 필요한 toolog와이 빠른 시작의 뒷부분에 나오는 해당 데이터베이스. 나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.

기본적으로 **postgres** 데이터베이스가 서버 아래에 만들어집니다. hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 데이터베이스는 사용자, 유틸리티 및 타사 응용 프로그램에서 사용 하기 위해 의미 하는 기본 데이터베이스입니다. 


## <a name="configure-a-server-level-firewall-rule"></a>서버 수준 방화벽 규칙 구성

Hello로 Azure PostgreSQL 서버 수준 방화벽 규칙 만들기 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) 명령입니다. 와 같은 외부 응용 프로그램 서버 수준 방화벽 규칙을 허용 [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 또는 [PgAdmin](https://www.pgadmin.org/) hello PostgreSQL Azure 서비스 방화벽을 통해 tooconnect tooyour 서버입니다. 

IP 범위 toobe 수 tooconnect 네트워크에서에 대해 설명 하는 방화벽 규칙을 설정할 수 있습니다. hello 다음 예제에서는 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) toocreate 방화벽 규칙 `AllowAllIps` 는 ip 주소 범위입니다. tooopen 모든 IP 주소를 IP 주소와 255.255.255.255 끝 주소 hello로 시작 하는 hello로 0.0.0.0를 사용 합니다.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure PostgreSQL 서버는 5432 포트를 통해 통신합니다. 회사 네트워크 내에서 연결하려는 경우 5432 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다. IT 부서 포트 5432 tooconnect tooyour Azure SQL 데이터베이스 서버를 열고 있으며
>

## <a name="get-hello-connection-information"></a>Hello 연결 정보를 가져옵니다

tooconnect tooyour 서버 tooprovide 호스트 정보 및 액세스 자격 증명이 필요 합니다.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

hello 결과 JSON 형식에서입니다. Hello 메모 **administratorLogin** 및 **fullyQualifiedDomainName**합니다.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>TooAzure 데이터베이스 psql를 사용 하 여 PostgreSQL 데이터베이스에 대 한 연결
클라이언트 컴퓨터에 설치 된 PostgreSQL의 로컬 인스턴스를 사용할 수 있습니다 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), 또는 hello Azure 클라우드 콘솔 tooconnect tooan Azure PostgreSQL 서버입니다. PostgreSQL 서버에 대 한 hello psql 명령줄 유틸리티 tooconnect toohello Azure 데이터베이스를 지금 사용해 보겠습니다.

1. Hello psql 명령 tooconnect tooan Azure 데이터베이스 PostgreSQL 서버에 대 한 다음 실행
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  다음 명령을 hello 라는 toohello 기본 데이터베이스를 연결 하는 예를 들어 **postgres** PostgreSQL 서버의 **mypgserver 20170401.postgres.database.azure.com** 액세스 자격 증명을 사용 하 여 합니다. Hello 입력 `<server_admin_password>` 암호를 묻는 메시지가 나타나면 선택 합니다.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  연결 된 toohello 서버 되 면 hello 프롬프트에서 빈 데이터베이스를 만듭니다.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Hello 프롬프트에서 실행 명령을 tooswitch 연결 toohello 새로 만든 데이터베이스를 다음 hello **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Hello 데이터베이스에서 테이블 만들기
배웠으므로 어떻게 tooconnect toohello Azure PostgreSQL 데이터베이스 해 볼 수 있습니다 방법을 보다 toocomplete 몇 가지 기본적인 작업 합니다.

먼저 테이블을 만들고 일부 데이터와 함께 로드할 수 있습니다. 인벤토리 정보를 추적하는 테이블을 만들어 보겠습니다.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

새로 만든 테이블의 테이블 목록이 hello 지금 입력 하 여 hello를 확인할 수 있습니다.
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Hello 테이블로 데이터를 로드 합니다.
이제 테이블을 만들었으므로 이 테이블에 일부 데이터를 삽입할 수 있습니다. Hello open 명령 프롬프트 창에서 실행 hello 쿼리 tooinsert 다음 데이터의 일부 행
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

Hello 테이블의 hello 데이터를 업데이트할 수도 있습니다.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

hello 행이 데이터를 검색 하는 경우 그에 따라 업데이트를 가져옵니다.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>데이터베이스 tooa 이전 시점으로 복원
실수로 테이블을 삭제한 경우를 가정해 보겠습니다. 이런 경우는 쉽게 복구할 수 없는 경우입니다. PostgreSQL에 대 한 azure 데이터베이스 toogo 백 tooany-시점 (마지막 too7 일 (기본) 위쪽과 35 일 (표준) hello)에 있으며이 시점에서 tooa 새 서버를 복원 합니다. 이 새 서버 toorecover 삭제 된 데이터를 사용할 수 있습니다. hello 표를 추가 하기 전에 단계 복원 hello 샘플 서버 tooa 지점 뒤 번호입니다.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

hello `az postgres server restore` 명령 hello 매개 변수 뒤에 필요 합니다.
| 설정 | 제안 값 | 설명  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  원본 서버가 있는 hello에 있는 리소스 그룹입니다.  |
| --name | mypgserver-restored | hello restore 명령에 의해 만들어진 hello 새 서버의 hello 이름입니다. |
| restore-point-in-time | 2017-04-13T13:59:00Z | 지정 시간 toorestore를 선택 합니다. 이 날짜 및 시간 hello 원본 서버 백업 보존 기간 내에 있어야 합니다. ISO8601 날자 및 시간 형식을 사용합니다. 예를 들어 `2017-04-13T05:59:00-08:00`과 같은 고유한 현지 표준 시간대 또는 UTC Zulu 형식 `2017-04-13T13:59:00Z`를 사용할 수도 있습니다. |
| --source-server | mypgserver-20170401 | hello 이름 또는에서 원본 서버 toorestore hello의 ID입니다. |

복원 하는 서버 tooa-시점 hello 시점의 hello 원래 서버로 복사 하 여 지정한 시간에 새 서버를 만듭니다. hello 위치 및 복원 하는 hello 서버에 대 한 계층 값 가격 hello 원본 서버와 동일한 hello 됩니다.

hello 명령을 동기적 이므로 hello 서버 복원 된 후에 반환 합니다. Hello 복원이 완료 되 면 생성 된 hello 새 서버를 찾습니다. Hello 데이터가 예상 대로 복원 되었는지 확인 합니다.


## <a name="next-steps"></a>다음 단계
이 자습서에서는 방법에 대해 배웠습니다 toouse Azure CLI (명령줄 인터페이스) 및 기타 유틸리티를:
> [!div class="checklist"]
> * PostgreSQL용 Azure Database 만들기
> * Hello 서버 방화벽을 구성
> * 사용 하 여 [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티 toocreate 데이터베이스
> * 샘플 데이터 로드
> * 쿼리 데이터
> * 데이터 업데이트
> * 데이터 복원

그 다음, 자세한 방법을 toouse hello Azure 포털 toodo 유사한 작업을이 자습서를 검토: [PostgreSQL를 사용 하 여 Azure 포털을 hello에 대 한 첫 번째 Azure 데이터베이스 디자인](tutorial-design-database-using-azure-portal.md)
