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
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a><span data-ttu-id="0d702-103">SQL Server tooAzure Azure 백업 서버를 백업</span><span class="sxs-lookup"><span data-stu-id="0d702-103">Back up SQL Server tooAzure With Azure Backup Server</span></span>
<span data-ttu-id="0d702-104">이 문서에서는 Microsoft Azure 백업 서버 (MABS)를 사용 하 여 SQL Server 데이터베이스의 백업에 대 한 hello 구성 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-104">This article leads you through hello configuration steps for backup of SQL Server databases using Microsoft Azure Backup Server (MABS).</span></span>

<span data-ttu-id="0d702-105">SQL Server 데이터베이스 백업 tooAzure 및 Azure에서 복구의 hello 관리에는 세 가지 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-105">hello management of SQL Server database backup tooAzure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="0d702-106">백업 정책 tooprotect SQL Server 데이터베이스 tooAzure를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-106">Create a backup policy tooprotect SQL Server databases tooAzure.</span></span>
2. <span data-ttu-id="0d702-107">TooAzure 주문형 백업 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-107">Create on-demand backup copies tooAzure.</span></span>
3. <span data-ttu-id="0d702-108">Azure에서 hello 데이터베이스를 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-108">Recover hello database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0d702-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0d702-109">Before you start</span></span>
<span data-ttu-id="0d702-110">시작 하기 전에 갖추어야 할 [설치 하 고 hello Azure 백업 서버를 준비](backup-azure-microsoft-azure-backup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-110">Before you begin, ensure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a><span data-ttu-id="0d702-111">백업 정책 tooprotect SQL Server 데이터베이스 tooAzure 만들기</span><span class="sxs-lookup"><span data-stu-id="0d702-111">Create a backup policy tooprotect SQL Server databases tooAzure</span></span>
1. <span data-ttu-id="0d702-112">Azure 백업 서버 UI hello 클릭 hello **보호** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-112">On hello Azure Backup Server UI, click hello **Protection** workspace.</span></span>
2. <span data-ttu-id="0d702-113">Hello 도구 리본에서 클릭 **새로** toocreate 새 보호 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-113">On hello tool ribbon, click **New** toocreate a new protection group.</span></span>

    ![보호 그룹 만들기](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="0d702-115">MABS를 만드는 방법에 hello 지침과 함께 hello 시작 화면을 표시 한 **보호 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-115">MABS shows hello start screen with hello guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="0d702-116">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-116">Click **Next**.</span></span>
4. <span data-ttu-id="0d702-117">**서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-117">Select **Servers**.</span></span>

    ![선택하는 보호 그룹 종류 - '서버'](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="0d702-119">백업 hello 데이터베이스 toobe 사용 되는 hello SQL Server 컴퓨터를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-119">Expand hello SQL Server machine where hello databases toobe backed up are present.</span></span> <span data-ttu-id="0d702-120">MABS는 해당 서버에서 백업할 수 있는 다양한 데이터 원본을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-120">MABS shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="0d702-121">Hello 확장 **모든 SQL 공유** (이 경우 선택한 ReportServer$ MSDPM2012 및 ReportServer$ MSDPM2012TempDB) hello 데이터베이스를 선택 하 고 toobe를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-121">Expand hello **All SQL Shares** and select hello databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) toobe backed up.</span></span> <span data-ttu-id="0d702-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-122">Click **Next**.</span></span>

    ![SQL DB를 선택합니다.](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="0d702-124">Hello 보호 그룹에 대 한 이름을 제공 하 고 hello 선택 **온라인 보호** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-124">Provide a name for hello protection group and select hello **I want online Protection** checkbox.</span></span>

    ![데이터 보호 방법 - 단기 디스크 및 온라인 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="0d702-126">Hello에 **단기 목표 지정** 화면에서 필요한 입력 toocreate 백업 지점을 toodisk hello를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-126">In hello **Specify Short-Term Goals** screen, include hello necessary inputs toocreate backup points toodisk.</span></span>

    <span data-ttu-id="0d702-127">여기 것을 확인할 **보존 범위** 너무 설정*5 일*, **동기화 빈도** tooonce 설정 되어 모든 *15 분* 하는 hello 백업이 수행 되는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-127">Here we see that **Retention range** is set too*5 days*, **Synchronization frequency** is set tooonce every *15 minutes* which is hello frequency at which backup is taken.</span></span> <span data-ttu-id="0d702-128">**빠른 전체 백업** 너무 설정*오후 8시*합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-128">**Express Full Backup** is set too*8:00 P.M*.</span></span>

    ![단기 목표](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="0d702-130">오후 8시 (toohello 화면 입력에 따라)에 백업 지점 매일 만들어지는 hello에서 수정 된 hello 데이터를 전송 하 여 이전 날짜의 오후 8시 백업 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-130">At 8:00 PM (according toohello screen input) a backup point is created every day by transferring hello data that has been modified from hello previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="0d702-131">이 프로세스를 **빠른 전체 백업**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-131">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="0d702-132">트랜잭션 로그의 hello 동기화 되는 동안 데이터베이스가 있는 경우는 필요 toorecover hello 오후 9시 – hello 지점이 hello에서 hello 로그를 재생 하 여 생성 된 후 15 분 마다 마지막 전체 백업 지점 (이 경우에 오후 8)을 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-132">While hello transaction logs are synchronized every 15 minutes, if there is a need toorecover hello database at 9:00 PM – then hello point is created by replaying hello logs from hello last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="0d702-133">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="0d702-133">Click **Next**</span></span>

    <span data-ttu-id="0d702-134">MABS 표시에 사용 가능한 전체 저장소 공간 및 디스크 공간 사용률을 잠재적인 hello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-134">MABS shows hello overall storage space available and hello potential disk space utilization.</span></span>

    ![디스크 할당](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="0d702-136">기본적으로 MABS hello 초기 백업 복사본에 사용 되는 데이터 원본 (SQL Server 데이터베이스) 당 하나의 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-136">By default, MABS creates one volume per data source (SQL Server database) which is used for hello initial backup copy.</span></span> <span data-ttu-id="0d702-137">이 방법을 사용 하면 관리자 LDM (논리 디스크) hello MABS 보호 too300 데이터 원본 (SQL Server 데이터베이스)를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-137">Using this approach, hello Logical Disk Manager (LDM) limits MABS protection too300 data sources (SQL Server databases).</span></span> <span data-ttu-id="0d702-138">이 제한 사항을 선택 hello toowork **DPM 저장소 풀에 데이터 배치**, 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-138">toowork around this limitation, select hello **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="0d702-139">이 옵션을 사용 하는 경우 MABS 사용 하 여 단일 볼륨 여러 데이터 원본에 대 한 too2000 SQL 데이터베이스를 MABS tooprotect 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-139">If you use this option, MABS uses a single volume for multiple data sources, which allows MABS tooprotect up too2000 SQL databases.</span></span>

    <span data-ttu-id="0d702-140">경우 **hello 볼륨 자동 증가** 옵션을 선택 하면 hello 프로덕션 데이터까지 확장 되면서 증가 hello 백업 볼륨을 MABS 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-140">If **Automatically grow hello volumes** option is selected, MABS can account for hello increased backup volume as hello production data grows.</span></span> <span data-ttu-id="0d702-141">경우 **hello 볼륨 자동 증가** 옵션 선택 하지 않으면, MABS hello 보호 그룹의 hello toohello 데이터 소스를 사용 하는 백업 저장소를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-141">If **Automatically grow hello volumes** option is not selected, MABS limits hello backup storage used toohello data sources in hello protection group.</span></span>
9. <span data-ttu-id="0d702-142">관리자에는 초기 수동으로 (off 네트워크) 백업 tooavoid 대역폭 혼잡이 전송 또는 hello 네트워크를 통해 hello 옵션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-142">Administrators are given hello choice of transferring this initial backup manually (off network) tooavoid bandwidth congestion or over hello network.</span></span> <span data-ttu-id="0d702-143">Hello 시간 초기 전송 발생할 수 있는 hello에 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-143">They can also configure hello time at which hello initial transfer can happen.</span></span> <span data-ttu-id="0d702-144">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-144">Click **Next**.</span></span>

    ![초기 복제 방법](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="0d702-146">초기 백업 복사본이 hello 프로덕션 서버 (SQL Server 시스템) tooMABS hello 전체 데이터 원본 (SQL Server 데이터베이스)의 전송이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-146">hello initial backup copy requires transfer of hello entire data source (SQL Server database) from production server (SQL Server machine) tooMABS.</span></span> <span data-ttu-id="0d702-147">이 데이터는 크기가 클 수 있습니다 및 hello 네트워크를 통해 데이터를 전송할 hello 대역폭을 초과할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-147">This data might be large, and transferring hello data over hello network could exceed bandwidth.</span></span> <span data-ttu-id="0d702-148">이러한 이유로 관리자 tootransfer hello 초기 백업을 선택할 수 있습니다: **수동으로** (이동식 미디어 사용) tooavoid 대역폭 정체 또는 **hello 네트워크를 통해 자동으로** (에 지정 된 시간)입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-148">For this reason, administrators can choose tootransfer hello initial backup: **Manually** (using removable media) tooavoid bandwidth congestion, or **Automatically over hello network** (at a specified time).</span></span>

    <span data-ttu-id="0d702-149">Hello 초기 백업이 완료 되 면 hello 백업의 hello rest hello 초기 백업 복사본에 대해 증분 백업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-149">Once hello initial backup is complete, hello rest of hello backups are incremental backups on hello initial backup copy.</span></span> <span data-ttu-id="0d702-150">증분 백업을 toobe 작은 경향이 및 hello 네트워크를 통해 손쉽게 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-150">Incremental backups tend toobe small and are easily transferred across hello network.</span></span>
10. <span data-ttu-id="0d702-151">Hello 일관성 검사 toorun 하려는 경우 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-151">Choose when you want hello consistency check toorun and click **Next**.</span></span>

    ![일관성 확인](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="0d702-153">MABS는 hello 백업 지점 일관성 검사 toocheck hello 무결성을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-153">MABS can perform a consistency check toocheck hello integrity of hello backup point.</span></span> <span data-ttu-id="0d702-154">MABS에서 해당 파일에 대 한 hello 프로덕션 서버 (이 시나리오에서는 SQL Server 컴퓨터) 및 hello 백업 된 데이터에서 hello 백업 파일의 hello 체크섬을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-154">It calculates hello checksum of hello backup file on hello production server (SQL Server machine in this scenario) and hello backed-up data for that file at MABS.</span></span> <span data-ttu-id="0d702-155">Hello 충돌의 경우에서 해당 hello 가정 MABS 백업 파일이 손상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-155">In hello case of a conflict, it is assumed that hello backed-up file at MABS is corrupt.</span></span> <span data-ttu-id="0d702-156">MABS는 hello 백업 된 데이터를 균형 있게 조정 toohello 체크섬 불일치에 해당 하는 hello 블록을 전송 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-156">MABS rectifies hello backed-up data by sending hello blocks corresponding toohello checksum mismatch.</span></span> <span data-ttu-id="0d702-157">일관성 확인 및 hello 성능 중심 작업 이기 관리자 hello hello 일관성 확인 예약 하거나 자동으로 실행 옵션을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-157">As hello consistency check is a performance-intensive operation, administrators have hello option of scheduling hello consistency check or running it automatically.</span></span>
11. <span data-ttu-id="0d702-158">온라인 보호 데이터 원본을 hello toospecify, 선택 hello 데이터베이스 toobe 보호 tooAzure 및 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-158">toospecify online protection of hello datasources, select hello databases toobe protected tooAzure and click **Next**.</span></span>

    ![데이터 원본 선택](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="0d702-160">관리자는 자신의 조직 정책에 맞게 백업 일정 및 보존 정책을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-160">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![일정 및 보존](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="0d702-162">이 예제에서는 백업 하는 하루에 한 번 오후 12시 및 오후 8 시 (hello 화면 아래쪽 부분)에</span><span class="sxs-lookup"><span data-stu-id="0d702-162">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of hello screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="0d702-163">것이 좋습니다 toohave 빠른 복구를 위해 디스크에 단기 복구 지점 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-163">It’s a good practice toohave a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="0d702-164">이러한 복구 지점은 “운영 복구"에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-164">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="0d702-165">Azure는 높은 SLA 및 보장된 가용성이 있는 좋은 오프사이트 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-165">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="0d702-166">**모범 사례**: Azure 백업은 DPM를 사용 하 여 로컬 디스크 백업 hello 완료 된 후 예약 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-166">**Best Practice**: Make sure that Azure Backups are scheduled after hello completion of local disk backups using DPM.</span></span> <span data-ttu-id="0d702-167">따라서 hello 최신 디스크 복사 백업 toobe tooAzure 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-167">This enables hello latest disk backup toobe copied tooAzure.</span></span>

13. <span data-ttu-id="0d702-168">Hello 보존 정책 일정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-168">Choose hello retention policy schedule.</span></span> <span data-ttu-id="0d702-169">hello 보존 정책이 작동 하는 방법에 hello 세부 정보에 제공 되어 [사용 하 여 Azure 백업 tooreplace 테이프 인프라 문서](backup-azure-backup-cloud-as-tape.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-169">hello details on how hello retention policy works are provided at [Use Azure Backup tooreplace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![보존 정책](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="0d702-171">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="0d702-171">In this example:</span></span>

    * <span data-ttu-id="0d702-172">백업은 오후 12시 및 오후 8 시 (hello 화면 아래쪽 부분)에 하루에 한 번 수행 하 고 180 일 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-172">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of hello screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="0d702-173">토요일 오전 12: 00에 hello 백업</span><span class="sxs-lookup"><span data-stu-id="0d702-173">hello backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="0d702-174">104주 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-174">is retained for 104 weeks</span></span>
    * <span data-ttu-id="0d702-175">마지막 토요일 오전 12: 00에 hello 백업</span><span class="sxs-lookup"><span data-stu-id="0d702-175">hello backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="0d702-176">60개월 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-176">is retained for 60 months</span></span>
    * <span data-ttu-id="0d702-177">오후 12시 3 월의 마지막 토요일에 hello 백업</span><span class="sxs-lookup"><span data-stu-id="0d702-177">hello backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="0d702-178">10년 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-178">is retained for 10 years</span></span>
14. <span data-ttu-id="0d702-179">클릭 **다음** 선택 hello hello 초기 백업 복사본이 tooAzure 전송 하기 위한 적절 한 옵션 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-179">Click **Next** and select hello appropriate option for transferring hello initial backup copy tooAzure.</span></span> <span data-ttu-id="0d702-180">선택할 수 있습니다 **hello 네트워크를 통해 자동으로** 또는 **오프 라인 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-180">You can choose **Automatically over hello network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="0d702-181">**Hello 네트워크를 통해 자동으로** 전송 hello 백업을 위해 선택 하는 hello 일정에 따라 백업 데이터 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-181">**Automatically over hello network** transfers hello backup data tooAzure as per hello schedule chosen for backup.</span></span>
    * <span data-ttu-id="0d702-182">**오프 라인 백업** 이 작동하는 방법을 [Azure 백업에서 오프라인 백업 워크플로](backup-azure-backup-import-export.md)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-182">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="0d702-183">선택한 hello 관련 전송 메커니즘 toosend hello 초기 백업 복사본이 tooAzure 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-183">Choose hello relevant transfer mechanism toosend hello initial backup copy tooAzure and click **Next**.</span></span>
15. <span data-ttu-id="0d702-184">Hello에서 hello 정책 정보를 검토 한 후 **요약** 화면에서 hello에 **그룹 만들기** 단추 toocomplete hello 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-184">Once you review hello policy details in hello **Summary** screen, click on hello **Create group** button toocomplete hello workflow.</span></span> <span data-ttu-id="0d702-185">Hello를 클릭할 수 있는 **닫기** 모니터링 작업 영역에서 단추 및 모니터 hello 작업 진행률입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-185">You can click hello **Close** button and monitor hello job progress in Monitoring workspace.</span></span>

    ![진행 중인 보호 그룹 만들기](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="0d702-187">SQL Server 데이터베이스의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="0d702-187">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="0d702-188">Hello 이전 단계에 백업 정책을 생성 하는 동안에 "복구 지점은" hello 첫 번째 백업이 발생 하는 경우에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-188">While hello previous steps created a backup policy, a “recovery point” is created only when hello first backup occurs.</span></span> <span data-ttu-id="0d702-189">스케줄러 tookick hello 기다리는 대신 복구 트리거 hello 작성 하는 다음 hello 단계는 수동으로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-189">Rather than waiting for hello scheduler tookick in, hello steps below trigger hello creation of a recovery point manually.</span></span>

1. <span data-ttu-id="0d702-190">Hello 보호 그룹 상태가 표시 될 때까지 기다렸다가 **확인** hello 복구 지점을 만들기 전에 hello 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-190">Wait until hello protection group status shows **OK** for hello database before creating hello recovery point.</span></span>

    ![보호 그룹 멤버](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="0d702-192">Hello 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 **복구 지점 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-192">Right-click on hello database and select **Create Recovery Point**.</span></span>

    ![온라인 복구 지점 만들기](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="0d702-194">선택 **온라인 보호** hello 드롭 다운 메뉴에서 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-194">Choose **Online Protection** in hello drop-down menu and click **OK**.</span></span> <span data-ttu-id="0d702-195">이 Azure의 hello 복구 지점 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-195">This starts hello creation of a recovery point in Azure.</span></span>

    ![복구 지점 만들기](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="0d702-197">Hello에 hello 작업 진행 상황을 볼 수 있습니다 **모니터링** hello 다음 그림에 표시 된 하나 hello 처럼 진행 중인를 찾을 수 있는 작업 영역에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-197">You can view hello job progress in hello **Monitoring** workspace where you'll find an in progress job like hello one depicted in hello next figure.</span></span>

    ![콘솔 모니터링](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="0d702-199">Azure에서 SQL Server 데이터베이스 복구</span><span class="sxs-lookup"><span data-stu-id="0d702-199">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="0d702-200">hello 다음 단계는 필요한 toorecover Azure에서 보호 되는 엔터티 (SQL Server 데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="0d702-200">hello following steps are required toorecover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="0d702-201">Hello DPM 서버 관리 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-201">Open hello DPM server Management Console.</span></span> <span data-ttu-id="0d702-202">너무 이동**복구** DPM으로 백업 작업 영역 서버 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-202">Navigate too**Recovery** workspace where you can see hello servers backed up by DPM.</span></span> <span data-ttu-id="0d702-203">Hello (이 경우 ReportServer$ MSDPM2012)에 필요한 데이터베이스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-203">Browse hello required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="0d702-204">**온라인**으로 끝나는 시간**에서 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-204">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![복구 지점 선택](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="0d702-206">Hello 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-206">Right-click hello database name and click **Recover**.</span></span>

    ![Azure에서 복구](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="0d702-208">DPM은 hello 복구 지점의 hello 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-208">DPM shows hello details of hello recovery point.</span></span> <span data-ttu-id="0d702-209">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-209">Click **Next**.</span></span> <span data-ttu-id="0d702-210">복구 유형 선택 hello toooverwrite hello 데이터베이스 **SQL Server 복구 toooriginal 인스턴스**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-210">toooverwrite hello database, select hello recovery type **Recover toooriginal instance of SQL Server**.</span></span> <span data-ttu-id="0d702-211">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-211">Click **Next**.</span></span>

    ![TooOriginal 위치 복구](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="0d702-213">이 예제에서는 DPM hello 데이터베이스 tooanother SQL Server 인스턴스 또는 tooa 독립 실행형 네트워크 폴더를 복구할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-213">In this example, DPM allows recovery of hello database tooanother SQL Server instance or tooa standalone network folder.</span></span>
4. <span data-ttu-id="0d702-214">Hello에 **지정 복구 옵션** 화면에서 네트워크 대역폭 사용 제한을 복구 작업에서 사용 되는 toothrottle hello 대역폭 같은 hello 복구 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-214">In hello **Specify Recovery options** screen, you can select hello recovery options like Network bandwidth usage throttling toothrottle hello bandwidth used by recovery.</span></span> <span data-ttu-id="0d702-215">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-215">Click **Next**.</span></span>
5. <span data-ttu-id="0d702-216">Hello에 **요약** 화면에서 지금까지 제공 하는 모든 hello 복구 구성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-216">In hello **Summary** screen, you see all hello recovery configurations provided so far.</span></span> <span data-ttu-id="0d702-217">**복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-217">Click **Recover**.</span></span>

    <span data-ttu-id="0d702-218">복구 상태 hello hello 데이터베이스가 복구 되 고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-218">hello Recovery status shows hello database being recovered.</span></span> <span data-ttu-id="0d702-219">클릭할 수 있는 **닫기** hello에서 tooclose hello 마법사 및 보기 hello 진행률 **모니터링** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-219">You can click **Close** tooclose hello wizard and view hello progress in hello **Monitoring** workspace.</span></span>

    ![복구 프로세스 시작](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="0d702-221">Hello 복구 완료 되 면 hello 복원 된 데이터베이스는 응용 프로그램 일치입니다.</span><span class="sxs-lookup"><span data-stu-id="0d702-221">Once hello recovery is completed, hello restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="0d702-222">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="0d702-222">Next Steps:</span></span>
<span data-ttu-id="0d702-223">•   [Azure Backup FAQ](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0d702-223">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
