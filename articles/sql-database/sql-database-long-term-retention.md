---
title: "aaaStore Azure SQL 데이터베이스 백업에 대 한 too10 년 | Microsoft Docs"
description: "Azure SQL 데이터베이스에 대 한 백업을 too10 연도를 저장을 지 원하는 방법에 대해 알아봅니다."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Too10 년 구성에 대 한 Azure SQL 데이터베이스 백업 저장
대부분의 응용 프로그램 규정을 준수, 또는 기타 비즈니스 purposes는 해야 tooretain hello 이상으로 데이터베이스 백업을 Azure SQL 데이터베이스에서 제공 하는 7-35 일 [자동 백업](sql-database-automated-backups.md)합니다. Hello 장기 백업 보존 기능을 사용 하면 SQL 데이터베이스 백업에는 Azure 복구 서비스 자격 증명 모음에 대 한 too10 년을 저장할 수 있습니다. Too1, 자격 증명 모음 당 000 데이터베이스를 저장할 수 있습니다. 그런 다음 자격 증명 모음 toorestore hello에에서 백업을 모두를 선택할 수로 새 데이터베이스입니다.

> [!IMPORTANT]
> 장기 백업 보존 되어 미리 보기에서 현재 사용할 수 있는 영역을 다음 hello에: 오스트레일리아 동부, 오스트레일리아 남동부, 브라질 남쪽, 중앙 미국, 아시아 동부, 미국 동부, 미국 동부 2, 중앙 인도, 인도 남부, 일본 동부, 일본 서 부, 미국 중 북부, 북부 유럽, 남 중앙 미국, 동남 아시아, 서 부 유럽 및 미국 서 부
>

> [!NOTE]
> 24 시간 동안 자격 증명 모음 당 too200 데이터베이스를 사용할 수 있습니다. 이 제한은 각 서버 toominimize hello 영향에 대 한 별도 자격 증명 모음을 사용 하는 것이 좋습니다. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>SQL Database 장기 백업 보존의 작동 방식

장기 백업 보존을 사용하면 SQL 데이터베이스 서버를Azure Recovery Services 자격 증명 모음과 연결할 수 있습니다. 

* Hello 자격 증명 모음을 만들어야 합니다 hello SQL server를 만든 동일한 Azure 구독 hello와 같은 hello 지리적 지역 및 리소스 그룹입니다. 
* 그런 다음 데이터베이스에 대한 보존 정책을 구성합니다. hello 정책 원인 hello 주별 전체 데이터베이스 백업 toobe toohello 복구 서비스 자격 증명 모음을 복사 하 고 hello 지정 된 보존 기간 (위쪽 too10 년)에 대 한 유지 합니다. 
* 그런 다음 hello 구독에서 모든 서버에 이러한 백업 tooa 새 데이터베이스 중 하나에서 hello 데이터베이스를 복원할 수 있습니다. Hello 복사본 성능에 어떠한 영향도 미치지 hello 기존 데이터베이스 및 azure 저장소 기존 백업에서 복사본을 만듭니다.

> [!TIP]
> 방법 tooguide 참조 [구성 및 장기 백업 보존 Azure SQL 데이터베이스에서에서 복원](sql-database-long-term-backup-retention-configure.md)합니다.

## <a name="enable-long-term-backup-retention"></a>장기 백업 보존 사용

tooconfigure 데이터베이스에 대 한 장기 백업 보존:

1. Hello에는 Azure 복구 서비스 자격 증명 모음 만들기 SQL 데이터베이스 서버와 동일한 지역, 구독 및 리소스 그룹입니다. 
2. Hello 서버 toohello 자격 증명 모음을 등록 합니다.
3. Azure Recovery Services 보호 정책을 만듭니다.
4. 장기 백업 보존 해야 하는 hello 보호 정책 toohello 데이터베이스 적용 됩니다.

tooconfigure, 관리 및 장기 백업 보존은 Azure 복구 서비스 자격 증명 모음에서 자동화 된 백업에서 데이터베이스를 복원, hello 다음 중 하나를 수행 합니다.

* Azure 포털 hello를 사용 하 여: 클릭 **장기 백업 보존**데이터베이스를 선택한 다음 클릭 **구성**합니다. 

   ![장기 백업 보존할 데이터베이스 선택](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* PowerShell을 사용 하 여: 너무 이동[구성 및 장기 백업 보존 Azure SQL 데이터베이스에서에서 복원](sql-database-long-term-backup-retention-configure.md)합니다.

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>장기 백업 보존 기능 hello로 저장 된 데이터베이스 복원

장기 백업 보존 백업에서 toorecover:

1. 목록 hello 자격 증명 모음 hello 백업이 저장 되어 있습니다.
2. 목록 hello 컨테이너는 매핑된 tooyour 논리적 서버입니다.
3. 매핑된 tooyour 데이터베이스가 hello 자격 증명 모음 내 hello 데이터 원본 목록입니다.
4. 사용 가능한 toorestore 인 목록 hello 복구 지점
5. 구독 내에서 hello 복구 지점 toohello 대상 서버에서 hello 데이터베이스를 복원 합니다.

tooconfigure, 관리 및 장기 백업 보존은 Azure 복구 서비스 자격 증명 모음에서 자동화 된 백업에서 데이터베이스를 복원, hello 다음 중 하나를 수행 합니다.

* Azure 포털 hello를 사용 하 여: 너무 이동[Azure 포털 hello 사용 하 여 관리 장기 백업 보존](sql-database-long-term-backup-retention-configure.md)합니다. 

* PowerShell을 사용 하 여: 너무 이동[PowerShell을 사용 하 여 장기 백업 보존 관리](sql-database-long-term-backup-retention-configure.md)합니다.

## <a name="get-pricing-for-long-term-backup-retention"></a>장기 백업 보존의 가격 책정 정보 가져오기

SQL 데이터베이스의 장기 백업 보존 toohello에 따라 요금이 부과 됩니다 [세요 가격 Azure 백업 서비스](https://azure.microsoft.com/pricing/details/backup/)합니다.

Hello SQL 데이터베이스 서버를 자격 증명 모음 등록된 toohello 되 면 hello 자격 증명 모음에 저장 된 hello 주별 백업에 사용 되는 총 저장소를 hello에 대 한 요금이 청구 됩니다.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>장기 백업 보존에 저장된 사용 가능한 백업 보기

tooconfigure, 관리 및 hello Azure 포털을 사용 하 여 장기 백업 보존은 Azure 복구 서비스 자격 증명 모음에서 자동화 된 백업에서 데이터베이스를 복원, hello 다음 중 하나를 수행 합니다.

* Azure 포털 hello를 사용 하 여: 너무 이동[Azure 포털 hello 사용 하 여 관리 장기 백업 보존](sql-database-long-term-backup-retention-configure.md)합니다. 

* PowerShell을 사용 하 여: 너무 이동[PowerShell을 사용 하 여 장기 백업 보존 관리](sql-database-long-term-backup-retention-configure.md)합니다.

## <a name="disable-long-term-retention"></a>장기 보존 사용 안 함

hello 복구 서비스의 백업 보존 정책에 제공 된 hello에 따라 hello 정리를 자동으로 처리 합니다. 

특정 데이터베이스 toohello 자격 증명 모음에 대 한 보내는 hello 백업을 toostop 해당 데이터베이스에 대 한 hello 보존 정책을 제거 합니다.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> hello 자격 증명 모음에 이미 있는 hello 백업은 영향을 받지 않습니다. 보존 기간 만료 될 때 자동으로 hello 복구 서비스에 의해 삭제 됩니다.

## <a name="long-term-backup-retention-faq"></a>장기 백업 보존 FAQ

**Hello 자격 증명 모음에 있는 특정 백업이 수동으로 삭제할 수 있습니까?**

현재는 아닙니다. hello 자격 증명 모음 hello 보존 기간이 만료 될 때 백업을를 자동으로 정리 합니다.

**내 서버 toostore 백업을 toomore 하나의 자격 증명 모음 보다를 등록할 수 있습니까?**

아니요, 한 번에 백업을 tooonly 하나의 자격 증명 모음을 현재 저장할 수 있습니다.

**다른 구독에서 자격 증명 모음 및 서버를 보유할 수 있나요?**

아니요, 현재 hello 자격 증명 모음 및 서버에에서 있어야 hello 동일한 구독 및 리소스 그룹입니다.

**내 서버의 지역이 아닌 다른 지역에서 만든 자격 증명 모음을 사용할 수 있나요?**

자격 증명 모음 hello와 서버가 있어야 아니요, hello에 동일한 지역의 toominimize 시간 복사한 트래픽 요금을 방지 합니다.

**한 개의 자격 증명 모음에 저장할 수 있는 데이터베이스는 몇 개인가요?**

현재 too1, 자격 증명 모음 당 000 데이터베이스를 지원 합니다. 

**구독당 만들 수 있는 자격 증명 모음은 몇 개인가요?**

구독 당 too25 자격 증명 모음을 만들 수 있습니다.

**자격 증명 모음당 하루에 구성할 수 있는 데이터베이스 개수는 몇 개인가요?**

자격 증명 모음당 하루에 200개의 데이터베이스를 설정할 수 있습니다.

**장기 백업 보존은 탄력적 풀에서 작동하나요?**

예. Hello 보존 정책을 사용 하 여 hello 풀의 모든 데이터베이스를 구성할 수 있습니다.

**Hello 백업 만들어집니다 hello 시간을 선택할 수 있습니까?**

아니요, SQL 데이터베이스 데이터베이스에 hello 백업 일정 toominimize hello 성능 영향을 제어합니다.

**내 데이터베이스에 투명한 데이터 암호화가 활성화되어 있습니다. 사용할 수 있습니까 hello 자격 증명 모음과?** 

예, 투명한 데이터 암호화가 지원됩니다. Hello 원본 데이터베이스에서 더 이상 존재 하는 경우에 hello 자격 증명 모음에서 hello 데이터베이스를 복원할 수 없습니다.

**내 구독 일시 중단 hello 자격 증명 모음에 hello 백업에 미치는 영향** 

구독 일시 중단 했습니다 hello 기존 데이터베이스와 백업을 유지 합니다. 새 백업 자격 증명 모음 복사한 toohello 않습니다. Hello 구독을 다시 활성화 한 후 백업을 toohello 자격 증명 모음 복사 hello 서비스 다시 시작 합니다. 자격 증명 모음 hello 구독 일시 중단 된 전에 있습니다 복사 된 hello 백업을 사용 하 여 액세스할 수 있는 toohello 복원 작업을 수 있습니다. 

**받을 수 있나요 액세스 toohello SQL 데이터베이스 백업 파일을 다운로드 하거나 toohello SQL server를 복원할 수 있나요?**

아니요, 현재는 아닙니다.

**가능한 toohave은 여러 SQL 보존 정책에서 (매일, 매주, 매월, 매년)을 예약 합니다.**

아니요, 현재는 가상 컴퓨터 백업에만 여러 일정을 사용할 수 있습니다.

**활성 지역 복제 보조 데이터베이스에 장기 백업 보존을 설정하면 어떻게 되나요?**

복제본의 백업은 지원되지 않으므로 현재는 보조 데이터베이스에 대한 장기 백업 보존 옵션이 없습니다. 그러나 반드시 활성 지리적 복제 보조 데이터베이스에서 장기 백업 보존을 tooset 사용자에 대 한 이러한 이유로:
* 장애 조치 하는 경우 hello 데이터베이스가 주 데이터베이스에서는 전체 백업을 수행, 업로드 toovault 변수인 합니다.
* 추가 보조 데이터베이스에서 장기 백업 보존을 설정 하기 위한 비용 toohello 고객 합니다.

## <a name="next-steps"></a>다음 단계
데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략에서 필수입니다. 다른 SQL 데이터베이스 비즈니스 연속성 솔루션 hello, 참조에 대 한 정보 toolearn [비즈니스 연속성 개요](sql-database-business-continuity.md)합니다.
