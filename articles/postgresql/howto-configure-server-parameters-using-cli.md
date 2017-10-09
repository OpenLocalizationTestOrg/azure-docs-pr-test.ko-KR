---
title: "PostgreSQL에 대 한 Azure 데이터베이스에서 aaaConfigure hello 서비스 매개 변수 | Microsoft Docs"
description: "이 문서에서는 tooconfigure hello 서비스 매개 변수 Azure 데이터베이스에서 PostgreSQL 사용에 대 한 Azure CLI 명령줄 hello 하는 방법을 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정
목록, 표시 하 고 hello 명령줄 인터페이스 (Azure CLI)를 사용 하는 Azure PostgreSQL 서버에 대 한 구성 매개 변수를 업데이트할 수 있습니다. 그러나 엔진 구성의 하위 집합만 서버 수준에서 노출하고 수정할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건
이 방법 tooguide 통해 toostep를 해야합니다.
- 서버 및 데이터베이스 [PostgreSQL용 Azure Database 만들기](quickstart-create-server-database-azure-cli.md)
- 설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티 또는 사용 하 여 Azure 클라우드 셸에에서 hello hello 브라우저.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>PostgreSQL 서버용 Azure 데이터베이스에 대한 서버 구성 매개 변수 나열
서버 및 해당 값을 수정할 수 있는 모든 매개 변수가 실행 toolist hello [az postgres 서버 구성 목록](/cli/azure/postgres/server/configuration#list) 명령입니다.

서버 hello에 대 한 hello 서버 구성 매개 변수를 나열할 수 있습니다 **mypgserver 20170401.postgres.database.azure.com** 리소스 그룹 아래의 **myresourcegroup**합니다.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>서버 구성 매개 변수 세부 정보 표시
hello를 실행 하는 서버에 대 한 특정 구성 매개 변수에 대 한 세부 정보 tooshow [az postgres 서버 구성 표시](/cli/azure/postgres/server/configuration#show) 명령입니다.

Hello에 대 한 세부 정보를 보여 주는이 예제 **로그\_min\_메시지** 서버에 대 한 서버 구성 매개 변수 **mypgserver 20170401.postgres.database.azure.com** 아래 리소스 그룹 **myresourcegroup 합니다.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>서버 구성 매개 변수 값 수정
Hello는 특정 서버 구성 매개 변수 값을 수정할 수 있습니다 및 이렇게 hello hello PostgreSQL 서버 엔진에 대 한 기본 구성 값을 업데이트 합니다. tooupdate hello 구성 사용 하 여 hello [az postgres 서버 구성 집합](/cli/azure/postgres/server/configuration#set) 명령입니다. 

tooupdate hello **로그\_min\_메시지** 서버의 서버 구성 매개 변수 **mypgserver 20170401.postgres.database.azure.com** 리소스그룹**myresourcegroup 합니다.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
선택적 hello 아웃 tooleave tooreset hello 구성 매개 변수 값을 사용 하도록 하려는 경우 선택 하면 `--value` 매개 변수 및 hello 서비스는 hello 기본값 적용 됩니다. 위의 예제에서는 다음과 같이 표시됩니다.
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
이렇게 하면 hello 다시 설정 **로그\_min\_메시지** 구성 toohello 기본값 **경고**합니다. 서버 구성 및 허용되는 값에 자세한 내용은 [서버 구성](https://www.postgresql.org/docs/9.6/static/runtime-config.html)의 PostgreSQL 설명서를 참조하세요.

## <a name="next-steps"></a>다음 단계
- tooconfigure 및 액세스 서버 로그를 참조 [PostgreSQL에 대 한 Azure 데이터베이스에서 서버 로그](concepts-server-logs.md)
