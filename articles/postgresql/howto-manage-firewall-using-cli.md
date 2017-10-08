---
title: "aaaCreate 및 Azure CLI를 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 및 Azure CLI 명령줄을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스를 관리 합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Azure CLI를 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리
서버 수준 방화벽 규칙에서 특정 IP 주소 또는 IP 주소 범위 PostgreSQL 서버에 대 한 관리자 toomanage 액세스 tooan Azure 데이터베이스를 사용 합니다. 편리 하 게 Azure CLI 명령을 사용 하 여, 수를 만들고 업데이트, 삭제, 목록, 서버 방화벽 규칙 toomanage를 표시 합니다. PostgreSQL용 Azure Database 방화벽에 대한 개요는 [PostgreSQL용 Azure Database 서버 방화벽 규칙](concepts-firewall-rules.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
이 방법 tooguide 통해 toostep를 해야합니다.
- [PostgreSQL용 Azure Database 서버 및 데이터베이스](quickstart-create-server-database-azure-cli.md)
- 설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티 또는 사용 하 여 Azure 클라우드 셸에에서 hello hello 브라우저.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>PostgreSQL용 Azure Database에 대한 서버 방화벽 규칙 구성
hello [az postgres 서버 방화벽 규칙](/cli/azure/postgres/server/firewall-rule) 명령을 사용 하는 tooconfigure 방화벽 규칙 있습니다.

## <a name="list-firewall-rules"></a>방화벽 규칙 나열 
hello 실행 hello 서버에 서버 방화벽 규칙 toolist hello 기존 [az postgres 서버 방화벽 규칙 목록](/cli/azure/postgres/server/firewall-rule#list) 명령입니다.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
hello 출력 형식 JSON에서 기본적으로 모든 hello 규칙을 나열 합니다. Hello 스위치를 사용할 수 있습니다 `--output table` hello 출력으로 더 읽기 쉬운 테이블 형식에 대 한 합니다.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>방화벽 규칙 만들기
toocreate hello를 실행 하는 hello 서버에 새 방화벽 규칙 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) 명령입니다. 

이 예에서는 모든 IP 주소 tooaccess hello 서버 범위를 허용 **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
단일 IP 주소 tooaccess tooallow 제공 IP 시작 및 끝 IP 다음이 예제와 같이 hello 처럼 동일한 주소 hello 합니다.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
요청이 성공 하면 hello 명령 출력 JSON 형식에서 기본적으로 만든 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다. 오류가 있으면 hello 대신 showserror 메시지 텍스트를 출력 합니다.

## <a name="update-firewall-rule"></a>방화벽 규칙 업데이트 
사용 하 여 hello 서버에서 기존 방화벽 규칙 업데이트 [az postgres 서버 방화벽 규칙 업데이트](/cli/azure/postgres/server/firewall-rule#update) 명령입니다. 입력 및 시작 IP 및 끝 IP 특성 tooupdate hello로 hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
요청이 성공 하면 hello 명령 출력을 업데이트 한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다. 오류가 있으면 hello 대신 showserror 메시지 텍스트를 출력 합니다.
> [!NOTE]
> Hello 방화벽 규칙이 없으면 hello 업데이트 명령으로 생성 합니다.

## <a name="show-firewall-rule-details"></a>방화벽 규칙 세부 정보 표시
표시할 수도 있습니다 hello 기존 방화벽 규칙 세부 정보는 서버에 대 한 실행 하 여 [az postgres 서버 방화벽 규칙 표시](/cli/azure/postgres/server/firewall-rule#show) 명령입니다.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
요청이 성공 하면 hello 명령 출력을 지정한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다. 오류가 있으면 hello 대신 showserror 메시지 텍스트를 출력 합니다.

## <a name="delete-firewall-rule"></a>방화벽 규칙 삭제
hello를 실행 하 여 기존 방화벽 규칙을 삭제 하는 hello 서버에서 IP 범위에 대 한 액세스 toorevoke [az postgres 서버 방화벽 규칙 삭제](/cli/azure/postgres/server/firewall-rule#delete) 명령입니다. Hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
성공하면 출력은 없습니다. 실패 시 오류 메시지 텍스트 hello 반환 됩니다.

## <a name="next-steps"></a>다음 단계
- 웹 브라우저도 사용할 수는 마찬가지로, 소개[만들기 및 hello Azure 포털을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리](howto-manage-firewall-using-portal.md)
- [PostgreSQL용 Azure Database 서버 방화벽 규칙](concepts-firewall-rules.md) 자세히 알아보기
- PostgreSQL 서버에 대 한 tooan Azure 데이터베이스 연결에 대 한 도움말을 참조 하십시오. [PostgreSQL에 대 한 Azure 데이터베이스에 대 한 연결 라이브러리](concepts-connection-libraries.md)
