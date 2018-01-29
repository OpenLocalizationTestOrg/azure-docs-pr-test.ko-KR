---
title: "Azure CLI를 사용하여 Azure Database for MySQL에서 서버 로그에 액세스 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 명령줄 유틸리티를 사용하여 Azure Database for MySQL에서 서버 로그에 액세스하는 방법을 설명합니다."
services: mysql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 11/28/2017
ms.openlocfilehash: 908f28d8bd3d0dcbd03636e69cd47b5c47f3cfde
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Azure CLI를 사용하여 서버 로그 구성 및 액세스
Azure 명령줄 유틸리티인 Azure CLI를 사용하여 Azure Database for MySQL 서버 로그를 다운로드할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.
- [Azure Database for MySQL 서버](quickstart-create-mysql-server-database-using-azure-cli.md)
- [Azure CLI 2.0](/cli/azure/install-azure-cli) 또는 브라우저의 Azure Cloud Shell 사용

## <a name="configure-logging-for-azure-database-for-mysql"></a>Azure Database for MySQL에 대한 로깅 구성
MySQL 느린 쿼리 로그에 액세스하도록 서버를 구성할 수 있습니다.
1. **slow\_query\_log** 매개 변수를 켜기로 설정하여 로깅을 사용합니다.
2. **long\_query\_time** 및 **log\_slow\_admin\_statements**와 같은 다른 매개 변수를 조정합니다.

Azure CLI를 통해 이러한 매개 변수 값을 설정하는 방법을 알아보려면 [서버 매개 변수를 구성하는 방법](howto-configure-server-parameters-using-cli.md)을 참조하세요.

예를 들어 다음 CLI 명령은 느린 쿼리 로그를 켜기로 설정하고, 긴 쿼리 시간을 10초로 설정하고, 느린 관리자 문의 로깅을 해제합니다. 마지막으로 검토할 구성 옵션을 나열합니다.
```azurecli-interactive
az mysql server configuration set --name slow_query_log --resource-group myresourcegroup --server myserver4demo --value ON
az mysql server configuration set --name long_query_time --resource-group myresourcegroup --server myserver4demo --value 10
az mysql server configuration set --name log_slow_admin_statements --resource-group myresourcegroup --server myserver4demo --value OFF
az mysql server configuration list --resource-group myresourcegroup --server myserver4demo
```

## <a name="list-logs-for-azure-database-for-mysql-server"></a>Azure Database for MySQL 서버에 대한 로그 나열
서버에 대한 사용 가능한 로그 파일을 나열하려면 [az mysql server-logs list](/cli/azure/mysql/server-logs#az_mysql_server_logs_list) 명령을 실행합니다.

리소스 그룹 **myresourcegroup**에 있는 **myserver4demo.mysql.database.azure.com** 서버에 대한 로그 파일을 나열하고 **log\_files\_list.txt**라는 텍스트 파일로 보낼 수 있습니다.
```azurecli-interactive
az mysql server-logs list --resource-group myresourcegroup --server myserver4demo > log_files_list.txt
```
## <a name="download-logs-from-the-server"></a>서버에서 로그 다운로드
[az mysql server-logs download](/cli/azure/mysql/server-logs#az_mysql_server_logs_download) 명령을 사용하여 서버에 대한 개별 로그 파일을 다운로드할 수 있습니다. 

이 예제에서는 리소스 그룹 **myresourcegroup**에 있는 **myserver4demo.mysql.database.azure.com** 서버에 대한 특정 로그 파일을 로컬 환경으로 다운로드합니다.
```azurecli-interactive
az mysql server-logs download --name 20170414-myserver4demo-mysql.log --resource-group myresourcegroup --server myserver4demo
```

## <a name="next-steps"></a>다음 단계
- [Azure Database for MySQL의 서버 로그](concepts-server-logs.md)에 대한 자세한 내용
