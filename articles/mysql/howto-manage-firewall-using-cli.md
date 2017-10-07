---
title: "aaaCreate 및 Azure CLI를 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 및 Azure CLI 명령줄을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스를 관리 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Azure CLI를 사용한 MySQL용 Azure Database 방화벽 규칙 만들기 및 관리
특정 IP 주소 또는 IP 주소 범위에서 MySQL Server에 대 한 관리자 toomanage 액세스 tooan Azure 데이터베이스를 사용 하는 서버 수준 방화벽 규칙입니다. 편리 하 게 Azure CLI 명령을 사용 하 여, 수를 만들고 업데이트, 삭제, 목록, 서버 방화벽 규칙 toomanage를 표시 합니다. MySQL용 Azure Database 방화벽에 대한 개요는 [MySQL용 Azure Database 서버 방화벽 규칙](./concepts-firewall-rules.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
* [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)
* PostgreSQL 및 MySQL용 Azure Python SDK 서비스 설치
* PostgreSQL 및 MySQL 서비스에 대 한 hello Azure CLI 구성 요소 설치
* Azure Database for MySQL 서버 만들기

## <a name="firewall-rule-commands"></a>방화벽 규칙 명령:
hello **az mysql 서버 방화벽 규칙** Azure CLI toocreate에서 명령을 사용 하는, 삭제, 나열, 표시 및 방화벽 규칙을 업데이트 합니다.

명령:
- **create**: Azure MySQL 서버 방화벽 규칙을 만듭니다.
- **delete**: Azure MySQL 서버 방화벽 규칙을 삭제합니다.
- **목록** : hello Azure MySQL 서버 방화벽 규칙을 나열 합니다.
- **표시** : 방화벽 규칙의 Azure의 MySQL server hello 세부 정보를 표시 합니다.
- **update**: Azure MySQL 서버 방화벽 규칙을 업데이트합니다.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>로그인 tooAzure 및 MySQL Server에 대 한 Azure 데이터베이스 목록
Azure 계정으로 Azure CLI를 안전하게 연결합니다. 사용 하 여 hello **az 로그인** toodo이 명령입니다.

1. Hello hello 명령줄에서 다음 명령을 실행 합니다.
```azurecli
az login
```
이 명령은 hello 다음 단계에서 코드 toouse를 출력 합니다.

2. 웹 브라우저 tooopen hello 페이지를 사용 하 여 [https://aka.ms/devicelogin](https://aka.ms/devicelogin) hello 코드를 입력 합니다.

3. Hello 프롬프트에서 Azure 자격 증명을 사용 하 여 로그인 합니다.

4. 사용자의 로그인에 게 권한이 부여 되 면 hello 콘솔에서 구독 목록이 표시 됩니다. 원하는 hello 구독 tooset hello 현재 구독 toobe 사용 일경의 hello id를 복사 합니다.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Hello 이름의 확실 하지 않은 경우에 구독 및 리소스 그룹에 대 한 MySQL server에 대 한 hello Azure 데이터베이스를 나열 합니다.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Hello 사용된 toospecify 됩니다 목록은 hello에 name 특성에는 MySQL server toowork를 note 합니다. 필요한 경우 해당 서버 toousing hello 이름 특성 tooconfirm 이름 형식이 hello 세부 정보를 확인 합니다.

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버에서 방화벽 규칙 나열 
Hello 서버 이름 및 hello 리소스 그룹 이름 목록 hello 기존 서버 방화벽 규칙 hello 서버에서 사용 하 여 합니다. Hello에 해당 hello 서버 이름 특성에 지정 됩니다 **-서버** 전환한 하지 hello **-이름** 전환 합니다.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
hello 출력은 JSON에서 기본적으로 모든 형식 hello 규칙을 나열 합니다. Hello 스위치를 사용할 수 있습니다 **-출력 테이블** hello 출력으로 더 읽기 쉬운 테이블 형식에 대 한 합니다.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버에서 방화벽 규칙 만들기
Hello Azure MySQL 서버 이름 및 hello 리소스 그룹 이름을 사용 하 여, hello 서버에 새 방화벽 규칙을 만들 합니다. Hello 규칙 toocover 범위의 IP 주소 tooallow 액세스에 대 한 hello 규칙, hello 시작 IP 및 끝 IP에 대 한 이름을 제공 합니다.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
단일 IP 주소에 대 대 한 액세스가 허용 toobe, 제공 IP 시작 및 끝 IP 다음이 예제와 같이 hello 처럼 동일한 주소 hello 합니다.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
요청이 성공 하면 hello 명령 출력은 JSON 형식에서 기본적으로 만든 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다. 오류가 있으면 hello 출력 대신 오류 메시지 텍스트로 표시 됩니다.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버에서 방화벽 규칙 업데이트 
서버 이름 및 hello 리소스 그룹 이름은 hello 서버에서 기존 방화벽 규칙을 업데이트 hello Azure MySQL을 사용 하 여 합니다. 입력 및 시작 IP 및 끝 IP 특성 tooupdate hello로 hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
요청이 성공 하면 hello 명령 출력을 업데이트 한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다. 오류가 있으면 hello 출력 대신 오류 메시지 텍스트로 표시 됩니다.

> [!NOTE]
> Hello 방화벽 규칙이 존재 하지 않습니다 hello 업데이트 명령으로 만들어집니다.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버에서 방화벽 규칙 세부 정보 표시
Hello Azure MySQL 서버 이름 및 hello 리소스 그룹 이름을 사용 하 여, hello 기존 방화벽 규칙 세부 정보 hello 서버에서 표시할 합니다. Hello 이름 hello 기존 방화벽 규칙의 입력으로 제공 합니다.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
요청이 성공 하면 hello 명령 출력은 사용자가 지정한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다. 오류가 있으면 hello 출력 대신 오류 메시지 텍스트로 표시 됩니다.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버에서 방화벽 규칙 삭제
Hello Azure MySQL을 사용 하 여 서버 이름 및 hello 리소스 그룹 이름은 기존 방화벽 규칙에서에서 제거 hello 서버 합니다. Hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
성공하면 출력은 없습니다. 실패 시 hello 오류 메시지 텍스트를 반환 됩니다.

## <a name="next-steps"></a>다음 단계
- [MySQL용 Azure Database 서버 방화벽 규칙](./concepts-firewall-rules.md) 자세히 알아보기
- [만들기 및 hello Azure 포털을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리](./howto-manage-firewall-using-portal.md)
