---
title: "MySQL에 대 한 Azure 데이터베이스의 서버 aaaHow tooRestore | Microsoft Docs"
description: "이 문서에서는 설명 방법을 사용 하 여 MySQL에 대 한 Azure 데이터베이스의 서버 toorestore hello Azure 포털입니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>어떻게 tooBackup 및 복원을 사용 하 여 MySQL에 대 한 Azure 데이터베이스의 서버 hello Azure 포털

## <a name="backup-happens-automatically"></a>자동으로 수행되는 백업
MySQL에 대 한 Azure 데이터베이스를 사용할 때는 hello 데이터베이스 서비스가 자동으로 hello 서비스의 백업을 5 분 마다. 

hello 백업은 7 일 동안 사용할 수 있는 기본 계층과 35 일을 사용 하는 경우 표준 계층을 사용 하는 경우. 자세한 내용은 [MySQL용 Azure Database 서비스 계층](concepts-service-tiers.md)을 참조하세요.

이 자동 백업 기능을 사용 하 여 hello 서버와 모든 데이터베이스는 새 서버 tooan 이전 지정 시간으로 복원할 수 있습니다.

## <a name="restore-in-hello-azure-portal"></a>Hello Azure 포털에서 복원
MySQL에 대 한 azure 데이터베이스가 있습니다 toorestore hello 서버 백 tooa 지점을 시간에서 및 tooa hello 서버의 새 복사본으로. 이 새 서버 toorecover 데이터를 사용할 수 있습니다. 

예를 들어 테이블 실수로 되었으면 정오에 오늘 삭제 있습니다 수 복원 정오 직전 toohello 시간 및 hello 누락 된 테이블 및 hello 서버 새 복사본에서 데이터를 검색 합니다.

hello 다음 단계 hello 샘플 서버 tooa 지점 시간으로 복원 합니다.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)

2. MySQL용 Azure Database 서버를 찾습니다. Hello 왼쪽된 창에서 선택 **모든 리소스**, hello 목록에서 서버를 선택 합니다.

3.  Hello 서버 개요 블레이드의 hello 위쪽에 클릭 **복원** hello 도구 모음입니다. hello 블레이드를 엽니다.
![복원 단추 클릭](./media/howto-restore-server-portal/click-restore-button.png)

4. Hello 복원 양식 hello 필요한 정보로 채웁니다.

- **복원 지점 (UTC)**:를 지정 시간 toorestore hello 날짜 선택 및 시간 선택을 사용 하 여을 선택 합니다. hello 지정 된 시간은 UTC 형식으로 UTC로 가능성이 tooconvert hello 현지 시간을 필요 합니다.
- **Toonew 서버 복원**: 새 서버 이름 toorestore hello에 기존 서버를 제공 합니다.
- **위치**: hello 지역 선택 자동으로 hello 소스 서버 영역 채워집니다 및 변경할 수 없습니다.
- **가격 책정 계층**: hello 계층 선택 항목을 자동으로 가격를 채워 hello 계층 hello 원본 서버와 동일한 가격 및 여기에서 변경할 수 없습니다. 
![PITR 복원](./media/howto-restore-server-portal/pitr-restore.png)

5. 클릭 **확인** toorestore hello 서버 toorestore tooa 지정 시간입니다. 

6. Hello 복원 완료 된 후 예상 대로 데이터베이스가 복원 된 tooverify hello 생성 된 hello 새 서버를 찾습니다.

## <a name="next-steps"></a>다음 단계
- [MySQL용 Azure 데이터베이스에 대한 연결 라이브러리](concepts-connection-libraries.md)