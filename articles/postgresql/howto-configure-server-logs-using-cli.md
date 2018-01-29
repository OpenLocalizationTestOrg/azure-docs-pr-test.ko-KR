---
title: "Azure CLI를 사용하여 PostgreSQL용 서버 로그 구성 및 액세스 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 명령줄을 사용하여 PostgreSQL용 Azure 데이터베이스의 서버 로그를 구성 및 액세스하는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 11/27/2017
ms.openlocfilehash: d18ec44ecede44829b488ac9864bbfae2c62883a
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Azure CLI를 사용하여 서버 로그 구성 및 액세스
Azure CLI(명령줄 인터페이스)를 사용하여 PostgreSQL 서버 오류 로그를 다운로드할 수 있습니다. 그러나 트랜잭션 로그에 대한 액세스는 지원되지 않습니다. 

## <a name="prerequisites"></a>필수 조건
이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.
- [PostgreSQL용 Azure Database 서버](quickstart-create-server-database-azure-cli.md)
- [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티를 설치하거나, 브라우저에서 Azure Cloud Shell을 사용합니다.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>PostgreSQL용 Azure Database에 대한 로깅 구성
쿼리 로그 및 오류 로그에 액세스하도록 서버를 구성할 수 있습니다. 오류 로그에는 자동 진공, 연결 및 검사점 정보가 포함될 수 있습니다.
1. 로깅 켜기
2. log\_statement and log\_min\_duration\_statement를 업데이트하여 쿼리 로깅 사용
3. 보존 기간 업데이트

자세한 내용은 [서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>PostgreSQL용 Azure 데이터베이스 서버에 대한 로그 나열
서버에 대한 사용 가능한 로그 파일을 나열하려면 [az postgres server-logs list](/cli/azure/postgres/server-logs#az_postgres_server_logs_list) 명령을 실행합니다.

리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 로그 파일을 나열하고 **log\_files\_list.txt**라는 텍스트 파일로 보낼 수 있습니다.
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a>로그를 서버에서 로컬로 다운로드
[az postgres server-logs download](/cli/azure/postgres/server-logs#az_postgres_server_logs_download) 명령을 사용하여 서버에 대한 개별 로그 파일을 다운로드할 수 있습니다. 

이 예제에서는 리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 특정 로그 파일을 로컬 환경으로 다운로드합니다.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>다음 단계
- 서버 로그에 대한 자세한 내용은 [PostgreSQL용 Azure Database의 서버 로그](concepts-server-logs.md)를 참조하세요.
- 서버 매개 변수에 대한 자세한 내용은 [Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.
