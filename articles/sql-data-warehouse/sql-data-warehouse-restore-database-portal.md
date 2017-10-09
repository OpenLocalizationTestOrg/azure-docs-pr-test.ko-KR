---
title: "Azure SQL 데이터 웨어하우스 (Azure 포털) aaaRestore | Microsoft Docs"
description: "Azure SQL Data Warehouse 복원을 위한 Azure Portal 작업"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Azure SQL Data Warehouse 복원(포털)
> [!div class="op_single_selector"]
> * [개요][Overview]
> * [포털][Portal]
> * [PowerShell][PowerShell]
> * [REST (영문)][REST]
>
>
이 문서에서는 toorestore Azure SQL 데이터 웨어하우스를 사용 하 여 Azure 포털을 hello 하는 방법을 배웁니다.

## <a name="before-you-begin"></a>시작하기 전에
**DTU 용량을 확인합니다.** SQL Data Warehouse의 각 인스턴스는 기본 DTU(데이터 처리량 단위) 할당량이 있는 SQL Server(예 : myserver.database.windows.net)에 의해 호스트됩니다. SQL 데이터 웨어하우스를 복원 하기 전에 SQL server에 복원 하려는 hello 데이터베이스에 대 한 DTU 할당량이 충분히 남아 있는지 확인 합니다. toolearn toocalculate DTU 할당량 또는 toorequest 자세한 Dtu 확인 하려면 어떻게 해야 [DTU 할당량 변경 요청][Request a DTU quota change]합니다.

## <a name="restore-an-active-or-paused-database"></a>활성 또는 일시 중지된 데이터베이스 복원
toorestore 데이터베이스:

1. Toohello 로그인 [Azure 포털][Azure portal]합니다.
2. Hello 왼쪽된 창에서 선택 **찾아보기**를 선택한 후 **SQL server**합니다.

    ![찾아보기 > SQL Servers 선택](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. 서버를 찾아 선택합니다.

    ![서버 선택](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. From, toorestore 원하고 선택 SQL 데이터 웨어하우스의 hello 인스턴스를 찾습니다.

    ![SQL 데이터 웨어하우스 toorestore의 hello 인스턴스를 선택 합니다.](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. 데이터 웨어하우스 블레이드 hello의 hello 위쪽 선택 **복원**합니다.

    ![복원 선택](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. 새 **데이터베이스 이름**을 지정합니다.
7. 선택 hello 최신 **복원 지점을**합니다.

   Hello 최신 복원 지점을 선택 하 고 있는지 확인 합니다. 복원 지점을 utc (협정 세계시)로 표시, 되므로 hello 기본 옵션 hello 최근 복원 지점 아닐 수 있습니다.

      ![복원 지점 선택](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. **확인**을 선택합니다.
9. hello 데이터베이스 복원 프로세스가 시작 됩니다 및 사용 하 여 **알림** toomonitor hello 프로세스입니다.

> [!NOTE]
> 수행 하 여 복구 된 데이터베이스를 구성할 수 hello 복원이 완료 된 후 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.
>
>

## <a name="restore-a-deleted-database"></a>삭제된 데이터베이스 복원
삭제 된 데이터베이스는 toorestore:

1. Toohello 로그인 [Azure 포털][Azure portal]합니다.
2. Hello 왼쪽된 창에서 선택 **찾아보기**를 선택한 후 **SQL server**합니다.

    ![찾아보기 > SQL Servers 선택](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. 서버를 찾아 선택합니다.

    ![서버 선택](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Toohello 아래로 스크롤하여 **작업** 서버 블레이드의 섹션.
5. 선택 hello **삭제 데이터베이스** 바둑판식으로 배열입니다.

    ![Hello 삭제 된 데이터베이스 타일을 선택 합니다.](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Toorestore hello 삭제 된 데이터베이스를 선택 합니다.

    ![데이터베이스 toorestore 선택](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. 새 **데이터베이스 이름**을 지정합니다.

    ![Hello 데이터베이스에 대 한 이름을 추가 합니다.](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. **확인**을 선택합니다.
9. hello 데이터베이스 복원 프로세스가 시작 됩니다 및 사용 하 여 **알림** toomonitor hello 프로세스입니다.

> [!NOTE]
> tooconfigure hello 복원이 완료 된 후 데이터베이스 참조 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.
>
>

## <a name="next-steps"></a>다음 단계
Azure SQL 데이터베이스 버전을 읽을 hello의 hello 비즈니스 연속성 기능에 대 한 toolearn [Azure SQL 데이터베이스 비즈니스 연속성 개요][Azure SQL Database business continuity overview]합니다.

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
