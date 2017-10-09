---
title: "aaa \"Azure CLI 스크립트 단위 Azure PostgreSQL 데이터베이스 | \"Microsoft Docs"
description: "Azure CLI 스크립트 샘플-hello 메트릭을 쿼리 한 후 PostgreSQL 서버 tooa 다양 한 성능 수준에 대 한 Azure 데이터베이스 크기 조정 합니다."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Azure CLI를 사용하여 단일 PostgreSQL 서버 모니터링 및 확장
이 샘플 CLI 스크립트 hello 메트릭을 쿼리 한 후 PostgreSQL 서버 tooa 다양 한 성능 수준에 대 한 단일 Azure 데이터베이스를 확장 합니다. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="sample-script"></a>샘플 스크립트
이 샘플 스크립트를 강조 표시 하는 hello 줄 toocustomize hello 관리자 사용자 이름 및 암호를 변경 합니다. 사용자 고유의 구독 id로 hello az 모니터 명령에 사용 된 hello 구독 id를 대체 합니다.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>배포 정리
Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>스크립트 설명
이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| **명령** | **참고 사항** |
|---|---|
| [az group create](/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az postgres server create](/cli/azure/postgres/server#create) | PostgreSQL hello 데이터베이스를 호스팅하는 서버를 만듭니다. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | Hello 리소스에 대 한 hello 메트릭 값을 나열 합니다. |
| [az group delete](/cli/azure/group#delete) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계
- Azure CLI hello에 대 한 자세한 정보를 확인할: [Azure CLI 설명서](/cli/azure/overview)
- 추가 스크립트 시도: [PostgreSQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)
- 크기 조정에 대한 자세한 내용은 [서비스 계층](../concepts-service-tiers.md) 및 [계산 단위 및 저장 단위](../concepts-compute-unit-and-storage.md)를 참조하세요.
