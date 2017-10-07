---
title: "어떻게 tooRestore PostgreSQL에 대 한 Azure 데이터베이스의 서버 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toorestore PostgreSQL 사용에 대 한 Azure 데이터베이스의 서버 hello Azure 포털입니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>어떻게 tooBackup 및 복원 PostgreSQL 사용에 대 한 Azure 데이터베이스의 서버 hello Azure 포털

## <a name="backup-happens-automatically"></a>자동으로 수행되는 백업
PostgreSQL에 대 한 Azure 데이터베이스를 사용할 때는 hello 데이터베이스 서비스가 자동으로 hello 서비스의 백업을 5 분 마다. 

hello 백업은 7 일 동안 사용할 수 있는 기본 계층과 35 일을 사용 하는 경우 표준 계층을 사용 하는 경우. 자세한 내용은 [PostgreSQL용 Azure Database 서비스 계층](concepts-service-tiers.md)을 참조하세요.

이 자동 백업 기능을 사용 하 여 hello 서버와 모든 데이터베이스는 새 서버 tooan 이전 지정 시간으로 복원할 수 있습니다.

## <a name="restore-in-hello-azure-portal"></a>Hello Azure 포털에서 복원
Azure 데이터베이스 PostgreSQL에 대 한를 통해 toorestore hello 서버 백 tooa 지점 시간에서 및 tooa hello 서버의 새 복사본으로 합니다. 이 새 서버 toorecover 데이터를 사용할 수 있습니다. 

예를 들어 테이블 실수로 되었으면 정오에 오늘 삭제 있습니다 수 복원 정오 직전 toohello 시간 및 hello 누락 된 테이블 및 hello 서버 새 복사본에서 데이터를 검색 합니다.

hello 다음 단계 hello 샘플 서버 tooa 지점 시간으로 복원 합니다.
1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)
2. PostgreSQL용 Azure 데이터베이스 서버를 찾습니다. Hello Azure 포털에서에서 클릭 **모든 리소스** hello 왼쪽 메뉴 및 hello 이름에는 형식에서와 같은 **mypgserver 20170401**, 기존 서버에 대 한 toosearch 합니다. Hello 검색 결과에 나열 된 hello 서버 이름을 클릭 합니다. hello **개요** 페이지 서버 열리고 더 이상의 구성에 대 한 옵션을 제공 합니다.

   ![Azure 포털-toolocate 서버 검색](media/postgresql-howto-restore-server-portal/1-locate.png)

3. Hello 서버 개요 블레이드의 hello 위쪽에 클릭 **복원** hello 도구 모음입니다. hello 블레이드를 엽니다.

   ![PostgreSQL용 Azure Database - 개요 - 복원 단추](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Hello 복원 양식 hello 필요한 정보로 채웁니다.

   ![PostgreSQL용 Azure Database - 정보 복원 ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **복원 지점**:에-시간 hello 서버 변경 되기 전에 발생 하는 선택
  - **대상 서버**: toorestore에 사용할 새 서버 이름을 제공 합니다.
  - **위치**: hello 영역을 선택할 수 없습니다, 기본적으로 hello 원본 서버와 동일한은
  - **가격 책정 계층**: 이 값은 서버를 복원할 때 변경할 수 없습니다. Hello 원본 서버와 같습니다. 

5. 클릭 **확인** toorestore hello 서버 toorestore tooa 지정 시간입니다. 

6. Hello 복원이 완료 되 면 데이터가 예상 대로 복원 된 tooverify hello 만들어지는 hello 새 서버를 찾습니다.

## <a name="next-steps"></a>다음 단계
- [PostgreSQL용 Azure Database에 대한 연결 라이브러리](concepts-connection-libraries.md)
