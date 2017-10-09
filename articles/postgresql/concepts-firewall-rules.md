---
title: "PostgreSQL용 Azure 데이터베이스 서버 방화벽 규칙 | Microsoft Docs"
description: "PostgreSQL용 Azure 데이터베이스 서버의 방화벽 규칙에 대해 설명합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>PostgreSQL용 Azure 데이터베이스 서버 방화벽 규칙
방화벽은 권한이 있는 컴퓨터를 지정할 때까지 모든 액세스 tooyour 데이터베이스 서버를 차단 합니다. hello 방화벽 액세스 toohello 서버 hello 시작 IP 주소를 각 요청에 따라 권한을 부여 합니다.
tooconfigure 허용 IP 주소 범위를 지정 하는 방화벽 규칙을 만들 방화벽입니다. Hello 서버 수준 방화벽 규칙을 만들 수 있습니다.

**방화벽 규칙:** 내의 모든 hello 데이터베이스의 동일한 논리 서버 hello, 즉, 이러한 규칙을 통해 클라이언트 tooaccess 전체 Azure 데이터베이스에 PostgreSQL 서버에 대 한 합니다. Hello Azure 포털을 사용 하거나 Azure CLI 명령을 사용 하 여 서버 수준 방화벽 규칙을 구성할 수 있습니다. toocreate 서버 수준 방화벽 규칙 hello 구독 소유자 또는 구독 참가자 여야 합니다.

## <a name="firewall-overview"></a>방화벽 개요
모든 데이터베이스 액세스 tooyour Azure 데이터베이스 PostgreSQL 서버에 대 한 hello 방화벽에 의해 기본적으로 차단 됩니다. 다른 컴퓨터에서 서버를 사용 하 여 toobegin toospecify 하나 필요 또는 서버 수준 방화벽 규칙 tooenable 액세스 tooyour 서버입니다. Hello 방화벽 규칙 toospecify hello 인터넷 tooallow에서 어떤 IP 주소 범위를 사용 합니다. 자체 Azure 포털 웹 사이트 액세스 toohello hello 방화벽 규칙의 영향을 받지 않습니다.
연결 시도 hello 인터넷 및 Azure 통과 해야 hello 방화벽 PostgreSQL 데이터베이스에 영향을 미칠 수 전에 hello 다음 다이어그램에에서 나와 있는 것 처럼:

![Hello 방화벽의 작동 방식 예제 흐름](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Hello 인터넷에서 연결
서버 수준 방화벽 규칙 tooall 데이터베이스를 PostgreSQL 서버에 대 한 hello Azure 데이터베이스에 적용 됩니다. Hello 요청의 hello IP 주소 중 한 hello 서버 수준 방화벽 규칙에 지정 된 hello 범위 내에 있으면 hello 연결이 승인 됩니다.
내에 없으면 hello 요청의 hello IP 주소 hello 데이터베이스 수준 중 하나에 지정 된 hello 범위 또는 서버 수준 방화벽 규칙의 경우, hello 연결 요청이 실패 합니다.
예를 들어 응용 프로그램에 연결 된 경우 JDBC 드라이버와 함께 PostgreSQL에 대 한 hello 방화벽이 hello 연결을 차단 하는 경우 tooconnect 동안이 오류가 발생할 수 있습니다.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>방화벽 규칙을 프로그래밍 방식으로 관리
또한 toohello Azure 포털, 방화벽 규칙 될 수 있습니다 Azure CLI를 사용 하 여 프로그래밍 방식으로 관리 합니다.
[Azure CLI를 사용한 PostgreSQL용 Azure 데이터베이스 방화벽 규칙 만들기 및 관리](howto-manage-firewall-using-cli.md)도 참조하세요.

## <a name="troubleshooting-hello-database-firewall"></a>Hello 데이터베이스 방화벽 문제 해결
Hello를 PostgreSQL 서버 서비스에 대 한 액세스 toohello Microsoft Azure 데이터베이스에는 예상 대로 작동 하지 않는 경우 지점 뒤에 것이 좋습니다.

* **변경 내용을 toohello 허용 목록이 아직 적용 되지 않음:** PostgreSQL 서버 방화벽 구성 tootake 효과 대 한 toohello Azure 데이터베이스를 변경 하는 데 5 분 지연 가능한 많이 있을 수 있습니다.

* **hello 로그인 권한이 없거나 잘못 된 암호를 사용한:** PostgreSQL 서버의 로그인에 사용 권한을 hello Azure 데이터베이스에 사용 되는 PostgreSQL 서버나 hello 암호 잘못 되었습니다. 하는 경우 hello 연결 toohello Azure 데이터베이스 거부 됩니다. Tooyour 서버;에 연결 하는 기회 tooattempt 클라이언트 제공 방화벽 설정 각 클라이언트 hello 필요한 보안 자격 증명을 제공 해야 합니다.

다음 오류가 hello JDBC 클라이언트를 사용 하 여, 예를 들어 나타날 수 있습니다.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"

* **동적 IP 주소:** 동적 IP 주소로 사용 하는 인터넷 연결이 있는 hello 방화벽을 통과 하는 데 문제가 있는 경우 hello 솔루션을 다음 중 하나를 시도할 수 있습니다.

* 인터넷 서비스 공급자 (ISP) hello IP 주소 범위에 대 한 할당 된 클라이언트 컴퓨터 tooyour 해당 액세스 hello Azure 데이터베이스 PostgreSQL 서버에 대 한 게 문의 하 고 방화벽 규칙으로 hello IP 주소 범위를 추가 합니다.

* 고정 IP 주소를 대신 클라이언트 컴퓨터에 대 한 가져오고 방화벽 규칙으로 hello IP 주소를 추가 합니다.

## <a name="next-steps"></a>다음 단계
서버 수준 및 데이터베이스 수준 방화벽 규칙 만들기에 대한 문서를 보려면 다음을 참조하세요.
* [만들기 및 hello Azure 포털을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리](howto-manage-firewall-using-portal.md)
* [Azure CLI를 사용한 PostgreSQL용 Azure 데이터베이스 방화벽 규칙 만들기 및 관리](howto-manage-firewall-using-cli.md)