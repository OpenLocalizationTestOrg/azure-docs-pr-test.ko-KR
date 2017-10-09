---
title: "aaa \"Azure CLI 스크립팅-PostgreSQL에 대 한 Azure 데이터베이스 만들기 | \"Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - PostgreSQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>PostgreSQL 서버에 대 한 Azure 데이터베이스를 만들고 hello Azure CLI를 사용 하는 방화벽 규칙 구성
이 샘플 CLI 스크립트는 PostgreSQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다. Hello 스크립트 성공적으로 실행 되 면 hello PostgreSQL 서버는 모든 Azure 서비스에서 액세스할 수 있으며 hello IP 주소를 구성 합니다.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="sample-script"></a>샘플 스크립트
이 샘플 스크립트를 강조 표시 하는 hello 줄 toocustomize hello 관리자 사용자 이름 및 암호를 편집 합니다.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>배포 정리
Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>스크립트 설명
이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| **명령** | **참고 사항** |
|---|---|
| [az group create](/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az postgres server create](/cli/azure/postgres/server#create) | PostgreSQL hello 데이터베이스를 호스팅하는 서버를 만듭니다. |
| [az postgres server firewall create](/cli/azure/postgres/server/firewall-rule#create) | Hello 입력 한 IP 주소 범위의 방화벽 규칙 tooallow 액세스 toohello 서버 및 데이터베이스를 만듭니다. |
| [az group delete](/cli/azure/group#delete) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계
- Azure CLI hello에 대 한 자세한 정보를 확인할: [Azure CLI 설명서](/cli/azure/overview)
- 추가 스크립트 시도: [PostgreSQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)
