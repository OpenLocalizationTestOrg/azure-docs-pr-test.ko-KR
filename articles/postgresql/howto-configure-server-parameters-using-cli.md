---
title: "PostgreSQL용 Azure Database에서 서비스 매개 변수 구성 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 명령줄을 사용하여 PostgreSQL용 Azure 데이터베이스에서 서비스 매개 변수를 구성하는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 11/27/2017
ms.openlocfilehash: a2a3395fad35599591e093385305f28bbb161014
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정
Azure CLI(명령줄 인터페이스)를 사용하여 Azure PostgreSQL 서버의 구성 매개 변수를 나열하고, 표시하며, 업데이트할 수 있습니다. 엔진 구성의 하위 집합은 서버 수준에서 노출되고 수정할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건
이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.
- [Azure Database for PostgreSQL 만들기](quickstart-create-server-database-azure-cli.md)에 따라 Azure Database for PostgreSQL 서버 및 데이터베이스 만들기
- [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 인터페이스를 컴퓨터에 설치하거나 브라우저를 사용하여 Azure Portal의 [Azure Cloud Shell](../cloud-shell/overview.md)을 사용합니다.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>PostgreSQL 서버용 Azure 데이터베이스에 대한 서버 구성 매개 변수 나열
서버의 수정 가능한 모든 매개 변수와 해당 값을 나열하려면 [az postgres server configuration list](/cli/azure/postgres/server/configuration#az_postgres_server_configuration_list) 명령을 실행합니다.

리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 서버 구성 매개 변수를 나열할 수 있습니다.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>서버 구성 매개 변수 세부 정보 표시
서버에 대한 특정 구성 매개 변수의 세부 정보를 표시하려면 [az postgres server configuration show](/cli/azure/postgres/server/configuration#az_postgres_server_configuration_show) 명령을 실행합니다.

이 예에서는 리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 **log\_min\_messages** 서버 구성 매개 변수의 세부 정보를 보여 줍니다.
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>서버 구성 매개 변수 값 수정
특정 서버 구성 매개 변수의 값을 수정할 수 있습니다. 그러면 PostgreSQL 서버 엔진에 대한 기본 구성 값이 업데이트됩니다. 구성 값을 업데이트하려면 [az postgres server configuration set](/cli/azure/postgres/server/configuration#az_postgres_server_configuration_set) 명령을 사용합니다. 

리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버의 **log\_min\_messages** 서버 구성 매개 변수를 업데이트하려면 다음을 실행합니다.
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
구성 매개 변수 값을 다시 설정하려는 경우 선택 사항인 `--value` 매개 변수를 유지하도록 선택하기만 하면 서비스에서 기본 값을 적용합니다. 위의 예제에서는 다음과 같이 표시됩니다.
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
이 명령은 **log\_min\_messages** 구성을 기본값 **WARNING**으로 다시 설정합니다. 서버 구성 및 허용되는 값에 자세한 내용은 [서버 구성](https://www.postgresql.org/docs/9.6/static/runtime-config.html)의 PostgreSQL 설명서를 참조하세요.

## <a name="next-steps"></a>다음 단계
- 서버 로그를 구성하고 액세스하려면 [PostgreSQL용 Azure Database의 서버 로그](concepts-server-logs.md)를 참조하세요.
