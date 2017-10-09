---
title: "aaaAzure SQL 데이터 웨어하우스 백업 스냅숏, 지리적 중복 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 tooa 복원 지점 또는 다른 지리적 지역 toorestore 수 있도록 하는 SQL 데이터 웨어하우스 기본 제공 데이터베이스 백업에 알아봅니다."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>SQL Data Warehouse 백업
SQL Data Warehouse는 데이터 웨어하우스 백업 기능의 일부로 로컬 및 지리적 백업을 제공합니다. 여기에는 Azure Storage Blob 스냅숏 및 지역 중복 저장소가 포함됩니다. 데이터 웨어하우스 백업 toorestore 데이터 웨어하우스 tooa 복원 hello 기본 지역의 가리키거나 복원 tooa 서로 다른 지리적 위치 영역을 사용 합니다. 이 문서에서는 SQL 데이터 웨어하우스에 백업의 hello 세부 사항을 설명 합니다.

## <a name="what-is-a-data-warehouse-backup"></a>데이터 웨어하우스 백업이란?
데이터 웨어하우스 백업은 사용할 수 있는 toorestore 데이터 웨어하우스 tooa 특정 시간 hello 데이터입니다.  SQL Data Warehouse는 분산 시스템이므로 Azure blob에 저장된 여러 파일이 데이터 웨어하우스 백업을 구성합니다. 

데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다. 자세한 내용은 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.

## <a name="data-redundancy"></a>데이터 중복
SQL Data Warehouse는 데이터를 로컬 중복(LRS) Azure Premium Storage에 저장하여 데이터를 보호합니다. 이 Azure 저장소 기능 지역화 된 오류가 발생 하는 경우 hello 로컬 데이터 센터 tooguarantee 투명 한 데이터 보호에 여러 동기 hello 데이터 복사본을 저장 합니다. 데이터 중복을 사용하면 데이터는 디스크 오류 등의 인프라 문제를 감당할 수 있습니다. 데이터 중복은 내결함성이 있는 비즈니스 연속성 및 고가용성 인프라를 보장합니다.

에 대 한 자세한 toolearn:

* Azure 프리미엄 저장소 참조 [소개 tooAzure 프리미엄 저장소](../storage/common/storage-premium-storage.md)합니다.
* 로컬 중복 저장소에 대한 자세한 내용은 [Azure Storage 복제](../storage/common/storage-redundancy.md#locally-redundant-storage)를 참조하세요.

## <a name="azure-storage-blob-snapshots"></a>Azure Storage Blob 스냅숏
Azure 프리미엄 저장소를 사용 하 여 가지이 점으로, SQL 데이터 웨어하우스 로컬로 Azure 저장소 Blob 스냅숏을 toobackup hello 데이터 웨어하우스를 사용 합니다. 데이터 웨어하우스 tooa 스냅숏 복원 지점으로 복원할 수 있습니다. 스냅숏은 최소 8시간마다 시작되며 7일 동안 사용할 수 있습니다.  

에 대 한 자세한 toolearn:

* Azure blob 스냅숏에 대한 자세한 내용은 [blob 스냅숏 만들기](../storage/blobs/storage-blob-snapshots.md)를 참조하세요.

## <a name="geo-redundant-backups"></a>지역 중복 저장소
24 시간 마다 SQL 데이터 웨어하우스 hello 전체 데이터 웨어하우스 표준 저장소에 저장합니다. hello 전체 데이터 웨어하우스가 생성 되 toomatch hello hello 마지막 스냅숏이의 시간입니다. 표준 저장소 hello tooa 지역 중복 저장소 계정에 대 한 읽기 액세스 (RA-GRS) 속해 있습니다. hello Azure 저장소 RA-GRS 기능 hello 백업 파일 tooa 복제 [쌍 이룬된 데이터 센터](../best-practices-availability-paired-regions.md)합니다. 이 지역에서 복제 하면 하면 기본 지역의 hello 스냅숏을 액세스할 수 없는 경우 데이터 웨어하우스를 복원할 수 있습니다. 

이 기능은 기본적으로 켜져 있습니다. [옵트아웃할 수] 있습니다 toouse 지역 중복 백업을 않도록 (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> Azure 저장소에 hello 용어 *복제* toocopying 파일 tooanother 한 위치에서에서 참조 합니다. SQL의 *데이터베이스 복제* 참조 tookeeping toomultiple 보조 데이터베이스가 주 데이터베이스와 동기화 합니다. 
> 
> 

> [!NOTE]
> DWU 9000 및 DWU 18000을 사용한 지역 중복 백업은 옵트아웃(opt out)할 수 없습니다. 
>
> 

에 대 한 자세한 toolearn:

* 지역 중복 저장소는 [Azure Storage 복제](../storage/common/storage-redundancy.md)를 참조하세요.
* RA-GRS 저장소는 [읽기 액세스 지역 중복 저장소](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)를 참조하세요.

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>데이터 웨어하우스 백업 일정 및 보존 기간
SQL 데이터 웨어하우스 마다 4 개의 tooeight 시간 및 각 스냅숏 7 일 동안 유지 온라인 데이터 웨어하우스의 스냅숏을 만듭니다. 지난 7 일간 hello에서 hello 복원 지점 온라인 데이터베이스 tooone 사용자를 복원할 수 있습니다. 

toosee hello 마지막 스냅숏이 시작 될 때 온라인 SQL 데이터 웨어하우스에서이 쿼리를 실행 합니다. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

7 일 보다 오래 tooretain 스냅숏으로 해야 할 경우에 복원 지점 tooa 새 데이터 웨어하우스를 복원할 수 있습니다. Hello 복원이 완료 되 면 SQL 데이터 웨어하우스 hello 새 데이터 웨어하우스에 대 한 스냅숏 만들기를 시작 합니다. 변경 내용을 toohello 새 데이터 웨어하우스를 지정 하지 않는 경우 빈 hello 스냅숏을 유지와 hello 스냅숏 비용 최소화 이므로 합니다. Hello 데이터베이스 tookeep SQL 데이터 웨어하우스를 일시 중지할에서 스냅샷을 만들 수도 있습니다.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>데이터 웨어하우스 내 일시 중지 된 동안 toomy 백업 보존 되나요?
SQL Data Warehouse는 데이터 웨어하우스가 일시 중지된 동안에는 스냅숏을 만들지 않으며 데이터 웨어하우스가 만료되지 않습니다. hello 스냅숏 age hello 데이터 웨어하우스 일시 중지 된 동안 변경 되지 않습니다. 스냅숏 보존이 hello hello 데이터 웨어하우스는 온라인으로 되지 일 하는 일 수를 기반으로 합니다.

예를 들어, 스냅숏으로 오후 4 월 1 일 시작 하는 경우 데이터 웨어하우스 hello 일시 중지 된 년 10 월 3 오후 4 hello 스냅숏 2 일입니다. Hello 데이터 웨어하우스를 다시 온라인 상태가 될 때마다 hello 스냅숏은 2 일입니다. 데이터 웨어하우스 hello 온라인 상태가 된 경우 10 월 5 오후 4, hello 스냅숏 2 일 및 5 일 이상 동안 유지 됩니다.

Hello 데이터 웨어하우스를 다시 온라인 상태가 되 면 SQL 데이터 웨어하우스 새 스냅숏이 다시 시작 이며 스냅숏 데이터의 7 일 이상 없을 때에 만료 됩니다.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>시간 hello 보존 기간은 삭제 된 데이터 웨어하우스에 대 한?
데이터 웨어하우스를 삭제할 때 hello 데이터 웨어하우스 및 hello 스냅숏은 7 일 동안 저장 되며 그런 다음 제거 합니다. 저장 된 hello 복원 지점 데이터 웨어하우스 tooany hello를 복원할 수 있습니다.

> [!IMPORTANT]
> 논리적 SQL server 인스턴스를 삭제 하면 toohello 인스턴스에 속하는 모든 데이터베이스가 삭제 되 고 복구할 수 없습니다. 삭제된 서버는 복원할 수 없습니다.
> 
> 

## <a name="data-warehouse-backup-costs"></a>데이터 웨어하우스 백업 비용
기본 데이터 웨어하우스 및 Azure Blob 스냅숏의 7 일에 대 한 비용 hello 총 TB 가장 가까운 둥근된 toohello입니다. 예를 들어 1.5 t B가 되도록 하 여 데이터 웨어하우스 hello 100GB 사용 하는 경우 2TB Azure 프리미엄 저장소 속도로 데이터에 대 한 요금이 청구 됩니다. 

> [!NOTE]
> 각 스냅숏은 처음 사용 비어 있고 변경 toohello 기본 데이터 웨어하우스를 만들 때 증가 합니다. 모든 스냅숏 크기 hello 데이터 웨어하우스 변경 될 때 증가합니다. 따라서 스냅숏에 대 한 저장소 비용은 hello 변경 toohello 비율에 따라 증가합니다.
> 
> 

지역 중복 저장소를 사용하는 경우 별도의 저장소 비용이 청구됩니다. hello 지역 중복 저장소는 hello 표준 읽기 액세스 지리적 중복 저장소 (RA-GRS) 요금이 청구 됩니다.

SQL Data Warehouse 가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.

## <a name="using-database-backups"></a>데이터베이스 백업 사용
SQL 데이터 웨어하우스 백업에 대 한 hello 주된 용도 hello 보존 기간 내 toorestore hello 데이터 웨어하우스 tooone hello 복원 지점입니다.  

* SQL 데이터 웨어하우스 toorestore 참조 [SQL 데이터 웨어하우스를 복원](sql-data-warehouse-restore-database-overview.md)합니다.

## <a name="related-topics"></a>관련된 항목
### <a name="scenarios"></a>시나리오
* 비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.

<!-- ### Tasks -->

* 데이터 웨어하우스 toorestore 참조 [SQL 데이터 웨어하우스를 복원 합니다.](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

