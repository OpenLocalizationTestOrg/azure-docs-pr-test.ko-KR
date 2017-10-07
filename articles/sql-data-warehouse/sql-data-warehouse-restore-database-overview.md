---
title: "Azure 데이터 웨어하우스-로컬 및 지리적 중복 aaaRestore | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 데이터베이스를 복구 하기 위한 hello 데이터베이스 복원 옵션의 개요입니다."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>SQL Data Warehouse 복원
> [!div class="op_single_selector"]
> * [개요][Overview]
> * [포털][Portal]
> * [PowerShell][PowerShell]
> * [REST (영문)][REST]
> 
> 

SQL Data Warehouse는 데이터 웨어하우스 재해 복구 기능의 일부로 로컬 및 지리적 복원을 제공합니다. 데이터 웨어하우스 tooa 복원 hello 기본 지역의 가리키거나 지역 중복 백업을 toorestore tooa 서로 다른 지리적 위치 영역을 사용 하 여 데이터 웨어하우스 백업 toorestore를 사용 합니다. 이 문서에서는 데이터 웨어하우스를 복원의 hello 세부 사항.

## <a name="what-is-a-data-warehouse-restore"></a>데이터 웨어하우스 복원이란?
데이터 웨어하우스 복원은 기존 데이터 웨어하우스 또는 삭제된 데이터 웨어하우스의 백업에서 생성되는 새 데이터 웨어하우스입니다. hello 복원 된 데이터 웨어하우스를 특정 시간에 hello 백업 된 데이터 웨어하우스를 다시 만듭니다. SQL Data Warehouse는 분산 시스템이므로 Azure blob에 저장된 여러 백업 파일에서 데이터 웨어하우스 복원이 생성됩니다. 

데이터베이스 복원은 실수로 손상되거나 삭제된 후 데이터를 다시 만들기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다.

자세한 내용은 다음을 참조하세요.

* [SQL Data Warehouse 백업](sql-data-warehouse-backups.md)
* [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>데이터 웨어하우스 복원 지점
Azure 프리미엄 저장소를 사용 하 여 가지이 점으로, SQL 데이터 웨어하우스는 Azure 저장소 Blob 스냅숏을 toobackup hello 기본 데이터 웨어하우스를 사용 합니다. 각 스냅숏은 hello 시간을 나타내는 있는 복원 지점에 hello 스냅숏 시작 합니다. 데이터 웨어하우스 toorestore 복원 지점을 선택한 복원 명령을 실행 합니다.  

SQL 데이터 웨어하우스는 항상 hello 백업 tooa 새 데이터 웨어하우스를 복원합니다. Hello 복원 된 데이터 웨어하우스를 유지 하 고 현재 hello 하거나 그 중 하나를 삭제 합니다. 원하는 tooreplace hello 현재 hello로 데이터 웨어하우스 데이터 웨어하우스를 복원, 이름을 바꿀 수 있습니다.

삭제 또는 일시 중지 된 데이터 웨어하우스 toorestore 해야 할 경우 다음을 할 수 있습니다 [지원 티켓을 만드세요](sql-data-warehouse-get-started-create-support-ticket.md)합니다. 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>지역 중복 복원
선택한 성능 수준에서 Azure SQL 데이터 웨어하우스를 지 원하는 데이터 웨어하우스 tooany 영역은 복원할 수 있습니다. Hello 미리 보기 동안 9000 및 18000 DWU 모든 지역에서 지원 되지 않는 note 하십시오.

> [!NOTE]
> 지리적 중복 tooperform 복원 하는이 기능을 옵트아웃 하지 하도록 선택 해야 합니다.
> 
> 

## <a name="restore-timeline"></a>복원 타임라인
지난 7 일 내 hello 데이터베이스 tooany 사용 가능한 복원 지점을 복원할 수 있습니다. 스냅숏은은 tooeight 매 4 시간 마다 시작 하며 7 일 동안 사용할 수 있는 합니다. 7일보다 오래된 스냅숏은 만료되고 해당 복원 지점을 더 이상 사용할 수 없게 됩니다.

## <a name="restore-costs"></a>복원 비용
hello 복원 된 데이터 웨어하우스 저장소 비용이 부과 hello hello Azure 프리미엄 저장소 요금이 청구 됩니다. 

복원 된 데이터 웨어하우스를 일시 중지 하면 hello Azure 프리미엄 저장소 속도로 저장소에 대 한 요금이 청구 됩니다. 일시 중지 hello 장점은 hello DWU 컴퓨팅 리소스에 대 한 요금이 부과 되지 않으므로입니다.

SQL Data Warehouse 가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.

## <a name="uses-for-restore"></a>복원의 용도
실수로 인 한 데이터 손실 또는 손상 후 toorecover 데이터는 하는 hello 기본으로 사용 되는 데이터 웨어하우스 복원 됩니다.

7 일 이상에 대 한 데이터 웨어하우스 복원 tooretain 백업도 사용할 수 있습니다. Hello 백업이 복원 되 면 hello 데이터 웨어하우스 온라인 있고 일시 중지할 수 무기한 toosave 계산 비용이 합니다. hello 일시 중지 된 데이터베이스에는 hello Azure 프리미엄 저장소 속도로 저장소 요금이 부과 됩니다. 

## <a name="related-topics"></a>관련된 항목
### <a name="scenarios"></a>시나리오
* 비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.

<!-- ### Tasks -->

데이터 웨어하우스 tooperform 복원를 사용 하 여 복원 합니다.

* Azure 포털에서 참조 [hello Azure 포털을 사용 하 여 데이터 웨어하우스를 복원 합니다.](sql-data-warehouse-restore-database-portal.md)
* PowerShell cmdlet의 경우 [PowerShell cmdlet을 사용하여 데이터 웨어하우스 복원](sql-data-warehouse-restore-database-powershell.md)을 참조하세요.
* REST Api 참조, [hello REST Api를 사용 하 여 데이터 웨어하우스를 복원 합니다.](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
