---
title: "PostgreSQL Azure 데이터베이스의 로그 aaaServer | Microsoft Docs"
description: "PostgreSQL용 Azure 데이터베이스에서 쿼리 및 오류 로그를 생성합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>PostgreSQL용 Azure 데이터베이스의 서버 로그 
PostgreSQL용 Azure 데이터베이스에서는 쿼리 및 오류 로그를 생성합니다. 그러나 액세스 tootransaction 로그는 지원 되지 않습니다. 이러한 로그는 사용 되는 tooidentify 수 하 고 해결 하 고, 해도 성능이 최적화 및 구성 오류를 복구 수 있습니다. 자세한 내용은 [오류 보고 및 로깅](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html)을 참조하세요.

## <a name="access-server-logs"></a>서버 로그 액세스
나열 하 고 hello Azure 포털을 사용 하 여 Azure PostgreSQL 서버 오류 로그를 다운로드할 수 [Azure CLI](howto-configure-server-logs-using-cli.md) 및 Azure REST Api입니다.

## <a name="log-retention"></a>로그 보존
시스템 로그를 사용 하 여 hello 보존 기간을 설정할 수 있습니다는 **로그\_보존\_기간** 서버와 관련 된 매개 변수입니다. 이 매개 변수에 대 한 hello 단위는 일 (tooconfirm 필요)입니다. hello 기본값은 3 일입니다. hello 최대 기간은 7 일입니다. 서버에 충분 한 할당 된 저장소 toocontain hello을 해야 로그 파일을 유지 합니다.
중 하나에 먼저으로 hello 로그 파일 1 시간 마다 또는 100MB 크기 회전 합니다.

## <a name="configure-logging-for-azure-postgresql-server"></a>Azure PostgreSQL 서버에 대한 로깅 구성
서버에 대한 쿼리 로깅 및 오류 로그를 사용하도록 설정할 수 있습니다. 오류 로그에는 자동 진공, 연결 및 검사점 정보가 포함될 수 있습니다.

두 개의 서버 매개 변수인 log\_statement 및 log\_min\_duration\_statement를 설정하여 PostgreSQL DB 인스턴스에 대한 쿼리 로깅을 사용하도록 설정할 수 있습니다.

hello **로그\_문을** 매개 변수는 SQL 문이 로깅됩니다를 제어 합니다. 이 매개 변수를 너무 설정 하는 것이 좋습니다***모든*** toolog 모든 문은; hello 기본값은 none (필요 tooconfirm).

hello **로그\_min\_기간\_문을** 기록 문 toobe의 밀리초에서 hello 한도 설정 하는 매개 변수입니다. Hello 매개 변수 설정 보다 오래 실행 되는 모든 SQL 문은 기록 됩니다. 이 매개 변수는 (필요 tooconfirm) 기본적으로 비활성화 하 고 설정 toominus 1 (-1). 이 매개 변수를 사용하도록 설정하면 응용 프로그램에서 최적화되지 않은 쿼리를 추적하는 데 도움이 될 수 있습니다.

hello **로그\_min\_메시지** 있습니다 toocontrol 메시지 수준을 toohello 서버 로그에 기록 됩니다. hello 기본값 (경고). (tooconfirm 필요)

이러한 설정에 대한 자세한 내용은 [오류 보고 및 로깅](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) 설명서를 참조하세요. 특히 PostgreSQL용 Azure 데이터베이스의 서버 매개 변수를 구성하는 경우 [PostgreSQL용 Azure 데이터베이스의 서버 로그](concepts-server-logs.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
- Azure CLI 명령줄 인터페이스를 사용 하 여 tooaccess 로그 참조 [Azure CLI를 사용 하 여 서버 로그를 구성 및 액세스](howto-configure-server-logs-using-cli.md)
- 서버 매개 변수에 대한 자세한 내용은 [Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.