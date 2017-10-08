---
title: "MySQL 데이터베이스-Azure CLI에 대 한 첫 번째 Azure 데이터베이스 aaaDesign | Microsoft Docs"
description: "이 자습서에 설명 어떻게 toocreate hello 명령줄에서 Azure CLI 2.0을 사용 하 여 데이터베이스 및 MySQL 서버에 대 한 Azure 데이터베이스를 관리 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>첫 번째 Azure Database for MySQL 데이터베이스 디자인

MySQL에 대 한 azure 데이터베이스는 MySQL Community Edition 데이터베이스 엔진을 기반으로 하는 Microsoft 클라우드 hello에 관계형 데이터베이스 서비스입니다. 이 자습서를 사용 하 여 Azure CLI (명령줄 인터페이스) 및 기타 유틸리티 toolearn 어떻게에:

> [!div class="checklist"]
> * Azure Database for MySQL 만들기
> * Hello 서버 방화벽을 구성
> * 사용 하 여 [mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate 데이터베이스
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
[az group create](https://docs.microsoft.com/cli/azure/group#create) 명령을 사용하여 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)을 만듭니다. 리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.

hello 다음 예제에서는 명명 된 리소스 그룹 `mycliresource` hello에 `westus` 위치 합니다.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Azure Database for MySQL 서버 만들기
Hello az mysql server와 MySQL server 만들기 명령에 대 한 Azure 데이터베이스를 만듭니다. 서버는 여러 데이터베이스를 관리할 수 있습니다. 일반적으로 각 프로젝트 또는 각 사용자에 대해 별도의 데이터베이스가 사용됩니다.

hello 다음 예제에서는 Azure 데이터베이스에 있는 MySQL 서버에 대 한 `westus` hello 리소스 그룹에 `mycliresource` 이름의 `mycliserver`합니다. hello 서버에 관리자 로그에 명명 된 `myadmin` 및 암호 `Password01!`합니다. hello 생성 되 **기본** 성능 계층 및 **50** hello 서버에서 모든 hello 데이터베이스 간에 공유 되는 단위를 계산 합니다. 확장할 수 있습니다 계산 및 저장소 위나 아래로 hello 응용 프로그램 요구에 따라.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>방화벽 규칙 구성
Hello az mysql 서버 방화벽 규칙으로 MySQL 서버 수준 방화벽 규칙 만들기 명령에 대 한 Azure 데이터베이스를 만듭니다. 와 같은 외부 응용 프로그램 서버 수준 방화벽 규칙을 허용 **mysql** 명령줄 도구 또는 MySQL 워크 벤치 tooconnect tooyour 서버 hello Azure MySQL 서비스 방화벽을 통해. 

hello 다음 예제에서는 미리 정의 된 주소 범위에 대 한 방화벽 규칙 이 예제는 hello 전체 가능한 IP 주소 범위를 보여줍니다.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Hello 연결 정보를 가져옵니다

tooconnect tooyour 서버 tooprovide 호스트 정보 및 액세스 자격 증명이 필요 합니다.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

hello 결과 JSON 형식에서입니다. Hello 메모 **fullyQualifiedDomainName** 및 **administratorLogin**합니다.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a>Mysql을 사용 하 여 toohello 서버 연결
사용 하 여 [mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish MySQL server에 대 한 연결 tooyour Azure 데이터베이스입니다. 이 예제에서는 hello 명령을 사용합니다.
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>빈 데이터베이스 만들기
을 사용 하는 연결 된 toohello 서버 후 빈 데이터베이스를 만듭니다.
```sql
mysql> CREATE DATABASE mysampledb;
```

Hello 프롬프트 hello 명령 tooswitch hello 연결 toothis 새로 만든 데이터베이스를 다음을 실행 합니다.
```sql
mysql> USE mysampledb;
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
실수로 이 테이블을 삭제했다고 가정해 보겠습니다. 이런 경우는 쉽게 복구할 수 없는 경우입니다. MySQL에 대 한 azure 데이터베이스 toogo 백 tooany 지점 hello의 지정 시간으로 마지막 too35 일을 있으며이 지점 시간 tooa 새 서버에 복원 합니다. 이 새 서버 toorecover 삭제 된 데이터를 사용할 수 있습니다. hello 표를 추가 하기 전에 단계 복원 hello 샘플 서버 tooa 지점 뒤 번호입니다.

Hello 복원에 대 한 다음 정보는 hello가 필요 합니다.

- 복원 지점을:에-시간 hello 서버 변경 되기 전에 발생 하는 선택 합니다. 보다 커야 하거나 toohello 원본 데이터베이스의 가장 오래 된 백업 값과 일치 해야 합니다.
- 대상 서버: toorestore에 사용할 새 서버 이름을 제공 합니다.
- 원본 서버: toorestore에서 원하는 hello 서버 hello 이름을 제공 합니다.
- 기본적으로 hello 원본 서버와 동일한은, 위치: hello 영역을 선택할 수 없습니다.

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

toorestore hello 서버 및 [tooa 시점에 복원](./howto-restore-server-portal.md) 전에 hello 테이블을 삭제 합니다. 서버 tooa 다른 지정 시간으로 복원 중복 새 서버를 만듭니다 hello, 원래 서버 hello 지정 시간을 지정 하면, hello 보존 기간 내에 않은 경우 프로그램 [서비스 계층](./concepts-service-tiers.md)합니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음에 대해 알아보았습니다.
> [!div class="checklist"]
> * Azure Database for MySQL 만들기
> * Hello 서버 방화벽을 구성
> * 사용 하 여 [mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate 데이터베이스
> * 샘플 데이터 로드
> * 쿼리 데이터
> * 데이터 업데이트
> * 데이터 복원

> [!div class="nextstepaction"]
> [Azure Database for MySQL - Azure CLI 샘플](./sample-scripts-azure-cli.md)
