---
title: "Azure SQL 데이터 웨어하우스에 aaaManage 데이터베이스 | Microsoft Docs"
description: "SQL 데이터 웨어하우스 데이터베이스 관리 개요. 관리 도구, DWU 및 성능 확장, 쿼리 성능 문제 해결, 보안 정책 설정, 데이터 손상 또는 지역적 중단으로부터 데이터베이스 복원 등이 포함되어 있습니다."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스의 데이터베이스 관리
SQL 데이터 웨어하우스는 데이터베이스 관리의 여러 측면을 자동화합니다. 예를 들어 tooscale 성능 tooadjust 하기만 하 고 계산 리소스의 오른쪽 수준 hello에 대 한 비용을 지불 하 고 후자의 경우 나중에 SQL 데이터 웨어하우스 확장 및 업그레이드 뒷면의 모든 hello 작업을 수행 합니다.

경우에 합니다 toomonitor 프로그램 작업 부하 tooidentify 성능이 필요한으로 장기 실행 쿼리 문제를 해결 합니다. 또한 권한이 필요 합니다 tooperform 몇 가지 보안 작업 toomanage 사용자와 로그인에 대 한 합니다.

이 개요에서는 SQL 데이터 웨어하우스 관리에 대한 이러한 측면에 대해 다룹니다.

* 관리 도구
* 계산 조정
* 일지 중지 및 다시 시작
* 성능 모범 사례
* 쿼리 모니터링
* 보안
* 백업 및 복원

## <a name="management-tools"></a>관리 도구
SQL 데이터 웨어하우스의 다양 한 도구 toomanage 데이터베이스를 사용할 수 있습니다. 기본 설정 도구에서 개발 데이터베이스를 관리 하는 대로 tooperform 각 유형의 태스크에 대 한 필요 합니다.

### <a name="azure-portal"></a>Azure portal
hello [Azure 포털] [ Azure portal] 은 웹 기반 포털 수, 업데이트 및 데이터베이스를 삭제 만들고 있는 데이터베이스 리소스를 모니터링 합니다. 이 도구는 좋은 경우 적은 수의 데이터 웨어하우스 데이터베이스를 관리 하는 azure를 시작 방금 또는 필요한 tooquickly 작업을 수행 합니다.

Azure 포털 hello로 시작 하는 tooget 참조 [SQL 데이터 웨어하우스 (Azure 포털)을 만들][Create a SQL Data Warehouse (Azure portal)]합니다.

### <a name="sql-server-data-tools-in-visual-studio"></a>Visual Studio에서 SQL Server 데이터 도구
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) Visual Studio에서 사용 하면 tooconnect를 관리 하 고 데이터베이스를 개발 합니다. Visual Studio 또는 다른 IDE(통합 개발 환경)에 익숙한 응용 프로그램 개발자라면 Visual Studio에서 SSDT를 사용해 보세요.

SSDT hello toovisualize 사용할 수 있는 SQL Server 개체 탐색기에 포함 되어, 연결 하 고 SQL 데이터 웨어하우스 데이터베이스에 대 한 스크립트를 실행 합니다. tooquickly tooSQL 데이터 웨어하우스 연결, hello 클릭 **Visual Studio에서 열기** hello Azure 클래식 포털에서에서 hello 데이터베이스 세부 정보를 볼 때 hello 명령 모음에서 단추입니다.  

Visual Studio에서 SSDT 시작 tooget 참조 [Visual Studio와 함께 Azure SQL 데이터 웨어하우스 쿼리][Query Azure SQL Data Warehouse with Visual Studio]합니다.

### <a name="command-line-tools"></a>명령줄 도구
명령줄은 워크로드 자동화에 적합합니다.  PowerShell 및 sqlcmd는 두 가지 유용한 방법은 tooautomate 프로세스입니다.  이러한 도구를 관리 하기 위한 많은 수의 논리 서버는 프로덕션 환경에서 리소스 변경 필요한 hello 작업 이름이 스크립팅되고 후 자동으로 사용 하는 것이 좋습니다.

### <a name="dynamic-management-views"></a>동적 관리 뷰
Dmv는 hello 측면도 SQL 데이터 웨어하우스를 관리 합니다. Hello 포털에서 표시 하는 거의 모든 정보는 Dmv를 사용 합니다. SQL 데이터 웨어하우스 Dmv 목록이 toosee 참조 [SQL 데이터 웨어하우스 시스템 뷰][SQL Data Warehouse system views]합니다.

시작 tooget 참조 [연결 및 sqlcmd 사용 하 여 쿼리][Connect and query with sqlcmd], 및 [(PowerShell) 데이터베이스를 만들][Create a database (PowerShell)]합니다.

## <a name="scale-compute"></a>계산 조정
SQL 데이터 웨어하우스에서 CPU의 계산 리소스, 메모리, I/O 대역폭을 늘리거나 줄여 성능을 빠르게 확장 또는 축소할 수 있습니다. tooscale 성능이 조정 hello 단위의 수 데이터 웨어하우스 (Dwu) SQL 데이터 웨어하우스 tooyour 데이터베이스를 할당 하기만 하면 toodo 됩니다. SQL 데이터 웨어하우스를 변경 하는 hello 신속 하 게 만들고 모든 변경 내용 toohardware를 원본으로 사용 하는 hello 또는 소프트웨어를 처리 합니다.

Dwu, 확장에 대 한 더 toolearn 참조 [성능을 확장]합니다.

## <a name="pause-and-resume"></a>일지 중지 및 다시 시작
toosave 비용을 일시 중지할 수 있습니다 및 다시 시작 요청 시 리소스를 계산 합니다. 예를 들어 사용 하지 않을 hello 데이터베이스 hello 밤 및 주말에, 하는 경우 해당 시간 동안 일시 중지 하 고 hello 일 동안 다시 시작 수 있습니다. Hello 데이터베이스 일시 중지 된 동안 Dwu를 청구 되지는지 않습니다.

자세한 내용은 [계산 일시 중지][Pause compute] 및 [계산 다시 시작][Resume compute]을 참조하세요.

## <a name="performance-best-practices"></a>성능 모범 사례
새로운 기술을 시작 hello 팁과 요령 hello 시작에서 가장 오른쪽 작동 하는 검색을 절약할 수 있는 시간입니다.  Microsoft의 다양한 항목에 모범 사례가 나와 있습니다.

여러 워크 로드를 개발할 때 가장 중요 한 고려 hello 요약 toosee 참조 [SQL 데이터 웨어하우스 모범 사례][SQL Data Warehouse Best Practices]합니다.

## <a name="query-monitoring"></a>쿼리 모니터링
쿼리가 너무 오래 실행 중인 경우에 따라 하지만 아닌 어느 것을 hello 오류의 원인이 있는지 확인 합니다. SQL 데이터 웨어하우스 쿼리 너무 오래 걸리면 아웃 동적 관리 뷰 (Dmv) toofigure를 사용할 수 있는 있습니다.

toofind 장기 실행 쿼리 참조 [Dmv를 사용 하 여 작업을 모니터링][Monitor your workload using DMVs]합니다.

## <a name="security"></a>보안
보안 시스템 toomaintain hello 경고 이며 모든 종류의 무단된 액세스 로부터 보호 합니다. 보안 시스템 toomake 방화벽 규칙이 충족 되는지 권한이 부여 되므로 IP 주소에 연결할 수 있어야 합니다. 사용자 자격 증명을 올바르게 인증해야 합니다. 사용자가 toohello 데이터베이스를 연결한 다음 hello 사용자만 있어야 권한을 tooperform 작업 수는 최소화 합니다. toosecure 데이터 암호화를 사용할 수 있습니다. 감사 및 추적 하는 의심 스러운 활동 하는 경우에 이벤트를 재 추적할 수 있도록 중요 한 toohave 이기도 합니다.

보안, toohello 찾아보려면 관리 하는 방법에 대 한 toolearn [보안 개요][Security overview]합니다.

## <a name="backup-and-restore"></a>백업 및 복원
데이터의 신뢰할 수 있는 백업을 만드는 것은 프로덕션 데이터베이스의 필수적인 부분입니다. SQL 데이터 웨어하우스는 정기적으로 활성 데이터베이스를 자동으로 백업하여 데이터를 안전하게 보관합니다. 이러한 백업을 사용 하면 데이터를 손상 하거나 데이터 나 데이터베이스를 실수로 삭제 한 시나리오에서 toorecover 있습니다.  Hello 데이터 백업 일정을 보존 정책에 대 한 toorestore 데이터베이스를 확인 하는 방법 및 [스냅숏에서 복원][Restore from snapshot]합니다.

## <a name="next-steps"></a>다음 단계
최적의 데이터베이스 디자인 원칙을 사용 하면 더욱 쉽게 toomanage SQL 데이터 웨어하우스 데이터베이스. toolearn 더 toohello 찾아보려면 [개발 개요][Development overview]합니다.

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[성능을 확장]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
