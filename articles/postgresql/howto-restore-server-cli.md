---
title: "어떻게 tooback PostgreSQL에 대 한 Azure 데이터베이스의 서버를 복원 및 | Microsoft Docs"
description: "어떻게를 tooback 및 사용 하 여 복원 Azure 데이터베이스의 서버 PostgreSQL hello Azure CLI에 알아봅니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>tooback 및 사용 하 여 복원 Azure 데이터베이스의 서버 PostgreSQL hello Azure CLI 방법

PostgreSQL toorestore 서버 데이터베이스 tooan 7 too35 일에서에 걸쳐 있는 이전 날짜로 Azure 데이터베이스를 사용 합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete 해야이 방법 tooguide:
- [PostgreSQL용 Azure Database 서버 및 데이터베이스](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> 설치 하 고 hello Azure CLI를 로컬로 사용 하는 경우이 방법을 tooguide Azure CLI 버전 2.0 이상 사용 해야 합니다. tooconfirm hello 버전 hello Azure CLI 명령 프롬프트에서 입력 `az --version`합니다. tooinstall 또는 업그레이드를 참조 하세요. [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.

## <a name="back-up-happens-automatically"></a>자동으로 수행되는 백업
Azure 데이터베이스를 사용 하 여 PostgreSQL에 대 한 hello 데이터베이스 서비스가 자동으로 hello 서비스의 백업을 5 분 마다. 

기본 계층에 대 한 hello 사용할 수 있는 백업이 7 일 동안 합니다. 표준 계층에 대 한 hello 사용할 수 있는 백업이 35 일입니다. 자세한 내용은 [PostgreSQL용 Azure Database 가격 책정 계층](concepts-service-tiers.md)을 참조하세요.

이 자동 백업 기능을 hello 서버 및 해당 데이터베이스 tooan 이전 날짜를 복원 하거나 지정 시간 수 있습니다.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 데이터베이스 tooa 이전 시점으로 복원
PostgreSQL toorestore hello 서버 tooa 이전 지정 시간에 대 한 Azure 데이터베이스를 사용 합니다. 복원 hello 데이터 복사 tooa 새 서버 이며 서버 hello 기존 서버는 그대로 유지 됩니다. 예를 들어 실수로 정오에 오늘는 테이블을 삭제 하는 경우 정오 직전 toohello 시간으로 복원할 수 있습니다. 그런 다음 hello 누락 된 테이블 및 복원 하는 hello 사본 hello 서버에서에서 데이터를 검색할 수 있습니다. 

toorestore hello 서버를 사용 하 여 hello Azure CLI [az postgres 서버 복원을](/cli/azure/postgres/server#restore) 명령입니다.

### <a name="run-hello-restore-command"></a>Hello restore 명령 실행

hello Azure CLI 명령 프롬프트에서 toorestore hello 서버 hello 다음 명령을 입력 합니다.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

hello `az postgres server restore` 명령 hello 매개 변수 뒤에 필요 합니다.
| 설정 | 제안 값 | 설명  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  Hello 원본 서버가 있는 리소스 그룹입니다.  |
| name | mypgserver-restored | hello restore 명령에 의해 만들어진 hello 새 서버의 hello 이름입니다. |
| restore-point-in-time | 2017-04-13T13:59:00Z | 지정 시간 toorestore를 선택 합니다. 이 날짜 및 시간 hello 원본 서버의 보존 기간을 백업 내에 있어야 합니다. Hello ISO8601 날짜 및 시간 형식을 사용 합니다. 예를 들어 `2017-04-13T05:59:00-08:00`과 같이 현지 표준 시간대를 사용할 수 있습니다. 예를 들어 UTC Zulu 서식을 hello를 사용할 수도 있습니다 `2017-04-13T13:59:00Z`합니다. |
| source-server | mypgserver-20170401 | hello 이름 또는에서 원본 서버 toorestore hello의 ID입니다. |

서버 tooan를 복원 하는 경우 이전 시점으로에서, 새 서버 만들어집니다. hello 원래 서버와 hello에서 해당 데이터베이스 지정 시간에는 복사 toohello 새 서버를 지정 합니다.

hello 위치 및 가격 책정 계층 값 복원 hello 서버 유지 hello 동일 hello, 원래 서버. 

hello `az postgres server restore` 명령은 동기 메서드 됩니다. Hello 서버를 복원한 후 하면 다시 사용할 수 toorepeat hello 프로세스 다른 지점에 대 한 시간에서입니다. 

Hello 후 복원 프로세스가 완료 될 새 서버 hello 찾은 예상 대로 hello 데이터가 복원 되었는지 확인 합니다.

## <a name="next-steps"></a>다음 단계
[PostgreSQL용 Azure Database에 대한 연결 라이브러리](concepts-connection-libraries.md)
