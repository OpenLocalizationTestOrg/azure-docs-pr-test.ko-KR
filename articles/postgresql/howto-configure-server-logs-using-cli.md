---
title: "PostgreSQL Azure CLI를 사용 하 여 서버 로그 aaaConfigure 및 액세스 | Microsoft Docs"
description: "이 문서에서는 PostgreSQL Azure CLI 명령줄을 사용 하 여에 대 한 tooconfigure 및 액세스 hello 서버 Azure 데이터베이스에서 로그 하는 방법을 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Azure CLI를 사용하여 서버 로그 구성 및 액세스
명령줄 인터페이스 (Azure CLI) hello를 사용 하 여 hello PostgreSQL 서버 오류 로그를 다운로드할 수 있습니다. 그러나 액세스 tootransaction 로그는 지원 되지 않습니다. 

## <a name="prerequisites"></a>필수 조건
이 방법 tooguide 통해 toostep를 해야합니다.
- [PostgreSQL용 Azure Database 서버](quickstart-create-server-database-azure-cli.md)
- 설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티 또는 사용 하 여 Azure 클라우드 셸에에서 hello hello 브라우저.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>PostgreSQL용 Azure Database에 대한 로깅 구성
Hello 서버 tooaccess 쿼리 로그 및 오류 로그를 구성할 수 있습니다. 오류 로그에는 자동 진공, 연결 및 검사점 정보가 포함될 수 있습니다.
1. 로깅 켜기
2. 업데이트 로그\_문과 로그\_min\_기간\_문 tooenable 쿼리 로깅
3. 보존 기간 업데이트

자세한 내용은 [서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>PostgreSQL용 Azure 데이터베이스 서버에 대한 로그 나열
hello 실행 서버에 대해 toolist hello 사용 가능한 로그 파일 [az postgres 서버 로그 목록](/cli/azure/postgres/server-logs#list) 명령입니다.

서버에 대 한 hello 로그 파일을 나열할 수 있습니다 **mypgserver 20170401.postgres.database.azure.com** 리소스 그룹 아래의 **myresourcegroup**, 및 tooa 텍스트를 직접 라는 파일 **로그\_파일\_list.txt 합니다.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Hello 서버에서 로그를 로컬로 다운로드
hello [az postgres 서버 로그를 다운로드](/cli/azure/postgres/server-logs#download) 명령을 사용 하면 서버에 대 한 toodownload 개별 로그 파일입니다. 

이 예제에서는 다운로드 hello hello 서버에 대 한 특정 로그 파일 **mypgserver 20170401.postgres.database.azure.com** 리소스 그룹 아래의 **myresourcegroup** tooyour 로컬 환경입니다.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>다음 단계
- 서버 로그에 대해 자세히 toolearn 참조 [PostgreSQL에 대 한 Azure 데이터베이스에서 서버 로그](concepts-server-logs.md)
- 서버 매개 변수에 대한 자세한 내용은 [Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.
