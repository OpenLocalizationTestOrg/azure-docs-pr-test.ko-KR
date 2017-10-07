---
title: "Azure 백업 서버를 사용 하 여 SQL Server 작업에 대 한 백업 aaaAzure | Microsoft Docs"
description: "Azure 백업 서버를 사용 하 여 SQL Server 데이터베이스를 소개 toobacking는"
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3a94338e8aca3f9d8611a72bcd223397ffb96f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a>SQL Server tooAzure Azure 백업 서버를 백업
이 문서에서는 Microsoft Azure 백업 서버 (MABS)를 사용 하 여 SQL Server 데이터베이스의 백업에 대 한 hello 구성 단계를 안내 합니다.

SQL Server 데이터베이스 백업 tooAzure 및 Azure에서 복구의 hello 관리에는 세 가지 단계가 포함 됩니다.

1. 백업 정책 tooprotect SQL Server 데이터베이스 tooAzure를 만듭니다.
2. TooAzure 주문형 백업 복사본을 만듭니다.
3. Azure에서 hello 데이터베이스를 복구 합니다.

## <a name="before-you-start"></a>시작하기 전에
시작 하기 전에 갖추어야 할 [설치 하 고 hello Azure 백업 서버를 준비](backup-azure-microsoft-azure-backup.md)합니다.

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>백업 정책 tooprotect SQL Server 데이터베이스 tooAzure 만들기
1. Azure 백업 서버 UI hello 클릭 hello **보호** 작업 영역입니다.
2. Hello 도구 리본에서 클릭 **새로** toocreate 새 보호 그룹입니다.

    ![보호 그룹 만들기](./media/backup-azure-backup-sql/protection-group.png)
3. MABS를 만드는 방법에 hello 지침과 함께 hello 시작 화면을 표시 한 **보호 그룹**합니다. **다음**을 누릅니다.
4. **서버**를 선택합니다.

    ![선택하는 보호 그룹 종류 - '서버'](./media/backup-azure-backup-sql/pg-servers.png)
5. 백업 hello 데이터베이스 toobe 사용 되는 hello SQL Server 컴퓨터를 확장 합니다. MABS는 해당 서버에서 백업할 수 있는 다양한 데이터 원본을 표시합니다. Hello 확장 **모든 SQL 공유** (이 경우 선택한 ReportServer$ MSDPM2012 및 ReportServer$ MSDPM2012TempDB) hello 데이터베이스를 선택 하 고 toobe를 백업 합니다. **다음**을 누릅니다.

    ![SQL DB를 선택합니다.](./media/backup-azure-backup-sql/pg-databases.png)
6. Hello 보호 그룹에 대 한 이름을 제공 하 고 hello 선택 **온라인 보호** 확인란을 선택 합니다.

    ![데이터 보호 방법 - 단기 디스크 및 온라인 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. Hello에 **단기 목표 지정** 화면에서 필요한 입력 toocreate 백업 지점을 toodisk hello를 포함 합니다.

    여기 것을 확인할 **보존 범위** 너무 설정*5 일*, **동기화 빈도** tooonce 설정 되어 모든 *15 분* 하는 hello 백업이 수행 되는 빈도입니다. **빠른 전체 백업** 너무 설정*오후 8시*합니다.

    ![단기 목표](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > 오후 8시 (toohello 화면 입력에 따라)에 백업 지점 매일 만들어지는 hello에서 수정 된 hello 데이터를 전송 하 여 이전 날짜의 오후 8시 백업 지점입니다. 이 프로세스를 **빠른 전체 백업**이라고 합니다. 트랜잭션 로그의 hello 동기화 되는 동안 데이터베이스가 있는 경우는 필요 toorecover hello 오후 9시 – hello 지점이 hello에서 hello 로그를 재생 하 여 생성 된 후 15 분 마다 마지막 전체 백업 지점 (이 경우에 오후 8)을 표현 합니다.
   >
   >

8. **다음**을 누릅니다

    MABS 표시에 사용 가능한 전체 저장소 공간 및 디스크 공간 사용률을 잠재적인 hello hello 합니다.

    ![디스크 할당](./media/backup-azure-backup-sql/pg-storage.png)

    기본적으로 MABS hello 초기 백업 복사본에 사용 되는 데이터 원본 (SQL Server 데이터베이스) 당 하나의 볼륨을 만듭니다. 이 방법을 사용 하면 관리자 LDM (논리 디스크) hello MABS 보호 too300 데이터 원본 (SQL Server 데이터베이스)를 제한 합니다. 이 제한 사항을 선택 hello toowork **DPM 저장소 풀에 데이터 배치**, 옵션입니다. 이 옵션을 사용 하는 경우 MABS 사용 하 여 단일 볼륨 여러 데이터 원본에 대 한 too2000 SQL 데이터베이스를 MABS tooprotect 수 있도록 해줍니다.

    경우 **hello 볼륨 자동 증가** 옵션을 선택 하면 hello 프로덕션 데이터까지 확장 되면서 증가 hello 백업 볼륨을 MABS 미칠 수 있습니다. 경우 **hello 볼륨 자동 증가** 옵션 선택 하지 않으면, MABS hello 보호 그룹의 hello toohello 데이터 소스를 사용 하는 백업 저장소를 제한 합니다.
9. 관리자에는 초기 수동으로 (off 네트워크) 백업 tooavoid 대역폭 혼잡이 전송 또는 hello 네트워크를 통해 hello 옵션이 제공 됩니다. Hello 시간 초기 전송 발생할 수 있는 hello에 구성할 수도 있습니다. **다음**을 누릅니다.

    ![초기 복제 방법](./media/backup-azure-backup-sql/pg-manual.png)

    초기 백업 복사본이 hello 프로덕션 서버 (SQL Server 시스템) tooMABS hello 전체 데이터 원본 (SQL Server 데이터베이스)의 전송이 필요합니다. 이 데이터는 크기가 클 수 있습니다 및 hello 네트워크를 통해 데이터를 전송할 hello 대역폭을 초과할 수 있습니다. 이러한 이유로 관리자 tootransfer hello 초기 백업을 선택할 수 있습니다: **수동으로** (이동식 미디어 사용) tooavoid 대역폭 정체 또는 **hello 네트워크를 통해 자동으로** (에 지정 된 시간)입니다.

    Hello 초기 백업이 완료 되 면 hello 백업의 hello rest hello 초기 백업 복사본에 대해 증분 백업 됩니다. 증분 백업을 toobe 작은 경향이 및 hello 네트워크를 통해 손쉽게 전송 됩니다.
10. Hello 일관성 검사 toorun 하려는 경우 선택 하 고 클릭 **다음**합니다.

    ![일관성 확인](./media/backup-azure-backup-sql/pg-consistent.png)

    MABS는 hello 백업 지점 일관성 검사 toocheck hello 무결성을 수행할 수 있습니다. MABS에서 해당 파일에 대 한 hello 프로덕션 서버 (이 시나리오에서는 SQL Server 컴퓨터) 및 hello 백업 된 데이터에서 hello 백업 파일의 hello 체크섬을 계산합니다. Hello 충돌의 경우에서 해당 hello 가정 MABS 백업 파일이 손상 되었습니다. MABS는 hello 백업 된 데이터를 균형 있게 조정 toohello 체크섬 불일치에 해당 하는 hello 블록을 전송 하 여 합니다. 일관성 확인 및 hello 성능 중심 작업 이기 관리자 hello hello 일관성 확인 예약 하거나 자동으로 실행 옵션을 가집니다.
11. 온라인 보호 데이터 원본을 hello toospecify, 선택 hello 데이터베이스 toobe 보호 tooAzure 및 클릭 **다음**합니다.

    ![데이터 원본 선택](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. 관리자는 자신의 조직 정책에 맞게 백업 일정 및 보존 정책을 선택할 수 있습니다.

    ![일정 및 보존](./media/backup-azure-backup-sql/pg-schedule.png)

    이 예제에서는 백업 하는 하루에 한 번 오후 12시 및 오후 8 시 (hello 화면 아래쪽 부분)에

    > [!NOTE]
    > 것이 좋습니다 toohave 빠른 복구를 위해 디스크에 단기 복구 지점 몇 가지 있습니다. 이러한 복구 지점은 “운영 복구"에 사용됩니다. Azure는 높은 SLA 및 보장된 가용성이 있는 좋은 오프사이트 위치를 제공합니다.
    >
    >

    **모범 사례**: Azure 백업은 DPM를 사용 하 여 로컬 디스크 백업 hello 완료 된 후 예약 된 확인 합니다. 따라서 hello 최신 디스크 복사 백업 toobe tooAzure 수 있습니다.

13. Hello 보존 정책 일정을 선택 합니다. hello 보존 정책이 작동 하는 방법에 hello 세부 정보에 제공 되어 [사용 하 여 Azure 백업 tooreplace 테이프 인프라 문서](backup-azure-backup-cloud-as-tape.md)합니다.

    ![보존 정책](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    이 예제에서:

    * 백업은 오후 12시 및 오후 8 시 (hello 화면 아래쪽 부분)에 하루에 한 번 수행 하 고 180 일 동안 유지 됩니다.
    * 토요일 오전 12: 00에 hello 백업 104주 동안 유지됩니다.
    * 마지막 토요일 오전 12: 00에 hello 백업 60개월 동안 유지됩니다.
    * 오후 12시 3 월의 마지막 토요일에 hello 백업 10년 동안 유지됩니다.
14. 클릭 **다음** 선택 hello hello 초기 백업 복사본이 tooAzure 전송 하기 위한 적절 한 옵션 및 합니다. 선택할 수 있습니다 **hello 네트워크를 통해 자동으로** 또는 **오프 라인 백업**합니다.

    * **Hello 네트워크를 통해 자동으로** 전송 hello 백업을 위해 선택 하는 hello 일정에 따라 백업 데이터 tooAzure 합니다.
    * **오프 라인 백업** 이 작동하는 방법을 [Azure 백업에서 오프라인 백업 워크플로](backup-azure-backup-import-export.md)에서 설명합니다.

    선택한 hello 관련 전송 메커니즘 toosend hello 초기 백업 복사본이 tooAzure 클릭 **다음**합니다.
15. Hello에서 hello 정책 정보를 검토 한 후 **요약** 화면에서 hello에 **그룹 만들기** 단추 toocomplete hello 워크플로 합니다. Hello를 클릭할 수 있는 **닫기** 모니터링 작업 영역에서 단추 및 모니터 hello 작업 진행률입니다.

    ![진행 중인 보호 그룹 만들기](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>SQL Server 데이터베이스의 주문형 백업
Hello 이전 단계에 백업 정책을 생성 하는 동안에 "복구 지점은" hello 첫 번째 백업이 발생 하는 경우에 만들어집니다. 스케줄러 tookick hello 기다리는 대신 복구 트리거 hello 작성 하는 다음 hello 단계는 수동으로 가리킵니다.

1. Hello 보호 그룹 상태가 표시 될 때까지 기다렸다가 **확인** hello 복구 지점을 만들기 전에 hello 데이터베이스에 대 한 합니다.

    ![보호 그룹 멤버](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Hello 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 **복구 지점 만들기**합니다.

    ![온라인 복구 지점 만들기](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. 선택 **온라인 보호** hello 드롭 다운 메뉴에서 **확인**합니다. 이 Azure의 hello 복구 지점 만들기를 시작합니다.

    ![복구 지점 만들기](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Hello에 hello 작업 진행 상황을 볼 수 있습니다 **모니터링** hello 다음 그림에 표시 된 하나 hello 처럼 진행 중인를 찾을 수 있는 작업 영역에서 작업 합니다.

    ![콘솔 모니터링](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Azure에서 SQL Server 데이터베이스 복구
hello 다음 단계는 필요한 toorecover Azure에서 보호 되는 엔터티 (SQL Server 데이터베이스).

1. Hello DPM 서버 관리 콘솔을 엽니다. 너무 이동**복구** DPM으로 백업 작업 영역 서버 hello를 볼 수 있습니다. Hello (이 경우 ReportServer$ MSDPM2012)에 필요한 데이터베이스를 이동 합니다. **온라인**으로 끝나는 시간**에서 복구**를 선택합니다.

    ![복구 지점 선택](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Hello 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **복구**합니다.

    ![Azure에서 복구](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM은 hello 복구 지점의 hello 세부 정보를 표시 합니다. **다음**을 누릅니다. 복구 유형 선택 hello toooverwrite hello 데이터베이스 **SQL Server 복구 toooriginal 인스턴스**합니다. **다음**을 누릅니다.

    ![TooOriginal 위치 복구](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    이 예제에서는 DPM hello 데이터베이스 tooanother SQL Server 인스턴스 또는 tooa 독립 실행형 네트워크 폴더를 복구할 수 있도록 합니다.
4. Hello에 **지정 복구 옵션** 화면에서 네트워크 대역폭 사용 제한을 복구 작업에서 사용 되는 toothrottle hello 대역폭 같은 hello 복구 옵션을 선택할 수 있습니다. **다음**을 누릅니다.
5. Hello에 **요약** 화면에서 지금까지 제공 하는 모든 hello 복구 구성을 표시 합니다. **복구**를 클릭합니다.

    복구 상태 hello hello 데이터베이스가 복구 되 고 표시 합니다. 클릭할 수 있는 **닫기** hello에서 tooclose hello 마법사 및 보기 hello 진행률 **모니터링** 작업 영역입니다.

    ![복구 프로세스 시작](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Hello 복구 완료 되 면 hello 복원 된 데이터베이스는 응용 프로그램 일치입니다.

### <a name="next-steps"></a>다음 단계:
•   [Azure Backup FAQ](backup-azure-backup-faq.md)
