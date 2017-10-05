---
title: "DPM을 사용한 SQL Server 워크로드에 대한 Azure 백업 | Microsoft Docs"
description: "Azure 백업 서비스를 사용하여 SQL Server 데이터베이스를 백업하는 방법 소개"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: c9edc066ea2edc9cd4b8453047d5584a588174dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-sql-server-to-azure-as-a-dpm-workload"></a><span data-ttu-id="955fd-103">SQL Server를 DPM 작업으로 Azure에 백업</span><span class="sxs-lookup"><span data-stu-id="955fd-103">Back up SQL Server to Azure as a DPM workload</span></span>
<span data-ttu-id="955fd-104">이 문서는 Azure Backup을 사용한 SQL Server 데이터베이스 백업의 구성 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-104">This article leads you through the configuration steps for backup of SQL Server databases using Azure Backup.</span></span>

<span data-ttu-id="955fd-105">SQL Server 데이터베이스를 Azure에 백업하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-105">To back up SQL Server databases to Azure, you need an Azure account.</span></span> <span data-ttu-id="955fd-106">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-106">If you don’t have an account, you can create a free trial account in just couple of minutes.</span></span> <span data-ttu-id="955fd-107">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955fd-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="955fd-108">Azure에 SQL Server 데이터베이스를 백업하고 Azure에서 데이터베이스를 복구하는 것을 관리하는 작업에는 세 가지 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-108">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="955fd-109">Azure에 대해 SQL server 데이터베이스를 보호하기 위한 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-109">Create a backup policy to protect SQL Server databases to Azure.</span></span>
2. <span data-ttu-id="955fd-110">Azure에 주문형 백업 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-110">Create on-demand backup copies to Azure.</span></span>
3. <span data-ttu-id="955fd-111">Azure에서 데이터베이스를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-111">Recover the database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="955fd-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="955fd-112">Before you start</span></span>
<span data-ttu-id="955fd-113">시작하기 전에, 워크로드를 보호하기 위하여 Microsoft Azure 백업 사용을 위한 [필수 구성 요소](backup-azure-dpm-introduction.md#prerequisites)를 모두 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-113">Before you begin, ensure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="955fd-114">필수 구성 요소는 백업 저장소 만들기, 보관 자격 증명 다운로드, Azure 백업 에이전트 설치 및 저장소에 서버 등록 등의 작업들을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-114">The prerequisites cover tasks such as: creating a backup vault, downloading vault credentials, installing the Azure Backup Agent, and registering the server with the vault.</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="955fd-115">Azure에 대해 SQL server 데이터베이스를 보호하기 위한 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-115">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="955fd-116">DPM 서버에서 **보호** 작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-116">On the DPM server, click the **Protection** workspace.</span></span>
2. <span data-ttu-id="955fd-117">도구 리본에서 **새로 만들기**를 클릭하여 새 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-117">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![보호 그룹 만들기](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="955fd-119">DPM은 **보호 그룹**을 만드는 지침으로 시작 화면을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-119">DPM shows the start screen with the guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="955fd-120">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-120">Click **Next**.</span></span>
4. <span data-ttu-id="955fd-121">**서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-121">Select **Servers**.</span></span>

    ![선택하는 보호 그룹 종류 - '서버'](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="955fd-123">백업할 데이터베이스가 있는 SQL Server 컴퓨터를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-123">Expand the SQL Server machine where the databases to be backed up are present.</span></span> <span data-ttu-id="955fd-124">DPM은 해당 서버에서 백업할 수 있는 다양한 데이터 원본을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-124">DPM shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="955fd-125">**모든 SQL 공유**를 확장하고 백업할 데이터베이스를 선택합니다(이 경우 ReportServer$ MSDPM2012 및 ReportServer$ MSDPM2012TempDB를 선택함).</span><span class="sxs-lookup"><span data-stu-id="955fd-125">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span></span> <span data-ttu-id="955fd-126">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-126">Click **Next**.</span></span>

    ![SQL DB를 선택합니다.](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="955fd-128">보호 그룹의 이름을 입력하고 **온라인 보호** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-128">Provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![데이터 보호 방법 - 단기 디스크 및 온라인 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="955fd-130">**단기 목표 지정** 화면에서 필요한 입력을 포함하여 디스크에 백업 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-130">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span></span>

    <span data-ttu-id="955fd-131">여기서 **보존 범위**가 *5일*, **동기화 빈도**가 백업이 수행되는 빈도인 *15분*마다 한 번으로 설정된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-131">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span></span> <span data-ttu-id="955fd-132">**빠른 전체 백업** 을 *오후 8시*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-132">**Express Full Backup** is set to *8:00 P.M*.</span></span>

    ![단기 목표](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="955fd-134">백업 시점은 전날의 오후 8시 백업 시점에서 수정된 데이터를 전송하여 오후 8시에(화면 입력에 따라) 매일 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-134">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="955fd-135">이 프로세스를 **빠른 전체 백업**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-135">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="955fd-136">트랜잭션 로그를 15분마다 동기화하는 반면 오후 9시에 데이터베이스를 복구해야 할 경우 마지막 빠른 전체 백업 지점에서 로그를 재생하여 지점을 만듭니다.(이 경우에 오후 8시)</span><span class="sxs-lookup"><span data-stu-id="955fd-136">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="955fd-137">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="955fd-137">Click **Next**</span></span>

    <span data-ttu-id="955fd-138">DPM에서는 사용 가능한 전체 저장소 공간 및 잠재적인 디스크 공간 사용률을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-138">DPM shows the overall storage space available and the potential disk space utilization.</span></span>

    ![디스크 할당](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="955fd-140">기본적으로 DPM에서는 초기 백업 복사본에 사용되는 데이터 원본(SQL Server 데이터베이스)당 하나의 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-140">By default, DPM creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span></span> <span data-ttu-id="955fd-141">이 방법을 사용하여 논리 디스크 관리자(LDM)는 DPM 보호를 300개 데이터 원본(SQL Server 데이터베이스)으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-141">Using this approach, the Logical Disk Manager (LDM) limits DPM protection to 300 data sources (SQL Server databases).</span></span> <span data-ttu-id="955fd-142">이 제한을 해결하려면 **DPM 저장소 풀에 데이터 배치**옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-142">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="955fd-143">이 옵션을 사용하면 DPM에서 여러 데이터 원본에 단일 볼륨을 사용하므로 DPM이 최대 2000개의 SQL 데이터베이스를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-143">If you use this option, DPM uses a single volume for multiple data sources, which allows DPM to protect up to 2000 SQL databases.</span></span>

    <span data-ttu-id="955fd-144">**볼륨 자동 증가** 옵션을 선택할 경우 프로덕션 데이터가 증가함에 따라 DPM은 백업 볼륨 증가를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-144">If **Automatically grow the volumes** option is selected, DPM can account for the increased backup volume as the production data grows.</span></span> <span data-ttu-id="955fd-145">**볼륨 자동 증가** 옵션을 선택하지 않으면 DPM은 백업 저장소 사용을 보호 그룹의 데이터 원본으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-145">If **Automatically grow the volumes** option is not selected, DPM limits the backup storage used to the data sources in the protection group.</span></span>
9. <span data-ttu-id="955fd-146">관리자는 해당 초기 백업을 수동으로 전송하도록 선택하여(오프 네트워크) 네트워크를 통한 대역폭 정체를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-146">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="955fd-147">또한 초기 전송이 발생할 수 있는 시간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-147">They can also configure the time at which the initial transfer can happen.</span></span> <span data-ttu-id="955fd-148">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-148">Click **Next**.</span></span>

    ![초기 복제 방법](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="955fd-150">초기 백업 복사본은 프로덕션 서버(SQL Server 컴퓨터)에서 DPM 서버로 전체 데이터 원본(SQL Server 데이터베이스)을 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-150">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to the DPM server.</span></span> <span data-ttu-id="955fd-151">이 데이터는 규모가 클 수 있으며 네트워크를 통한 데이터 전송이 대역폭을 초과할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-151">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="955fd-152">이 때문에 관리자는 최초 백업을 **수동**(이동식 미디어 사용)으로 전송하여 대역폭 혼잡을 방지하거나, **네트워크를 통해 자동으로 전송**(지정된 시간에)하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-152">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="955fd-153">초기 백업을 완료하면 백업의 나머지 부분은 초기 백업 복사본의 증분 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-153">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="955fd-154">증분 백업은 크기가 작으며 네트워크를 통해 간편하게 전송될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-154">Incremental backups tend to be small and are easily transferred across the network.</span></span>
10. <span data-ttu-id="955fd-155">일관성 확인을 실행하려는 경우 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-155">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![일관성 확인](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="955fd-157">DPM은 일관성 확인을 수행하여 백업 시점의 무결성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-157">DPM can perform a consistency check to check the integrity of the backup point.</span></span> <span data-ttu-id="955fd-158">프로덕션 서버(이 시나리오에서 SQL Server 컴퓨터)에서 백업 파일의 체크섬 및 DPM에서 해당 파일에 대한 백업 데이터를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-158">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at DPM.</span></span> <span data-ttu-id="955fd-159">충돌이 있을 경우 DPM에서 백업된 파일이 손상되었음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-159">In the case of a conflict, it is assumed that the backed-up file at DPM is corrupt.</span></span> <span data-ttu-id="955fd-160">DPM은 체크섬 불일치에 해당하는 블록을 전송하여 백업된 데이터를 균형있게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-160">DPM rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="955fd-161">일관성 확인은 성능 집약적인 작업이므로 관리자는 일관성 확인을 예약하거나 자동으로 실행하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-161">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span></span>
11. <span data-ttu-id="955fd-162">데이터 원본에 온라인 보호를 지정하려면 데이터베이스를 Azure에 보호되도록 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-162">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![데이터 원본 선택](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="955fd-164">관리자는 자신의 조직 정책에 맞게 백업 일정 및 보존 정책을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-164">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![일정 및 보존](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="955fd-166">이 예에서 백업은 매일 한 번 오후 12시 및 오후 8시에 수행됩니다.(화면의 아래쪽 부분)</span><span class="sxs-lookup"><span data-stu-id="955fd-166">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="955fd-167">신속한 복구를 위해 디스크에 몇 가지 단기 복구 지점이 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-167">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="955fd-168">이러한 복구 지점은 “운영 복구"에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-168">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="955fd-169">Azure는 높은 SLA 및 보장된 가용성이 있는 좋은 오프사이트 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-169">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="955fd-170">**모범 사례**: DPM을 사용하여 로컬 디스크 백업이 완료된 후에 Azure 백업을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-170">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span></span> <span data-ttu-id="955fd-171">이를 통해 최신 디스크 백업이 Azure에 복사될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-171">This enables the latest disk backup to be copied to Azure.</span></span>

13. <span data-ttu-id="955fd-172">보존 정책 일정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-172">Choose the retention policy schedule.</span></span> <span data-ttu-id="955fd-173">보존 정책이 작동하는 방법에 대한 자세한 내용은 [Azure 백업을 사용하여 테이프 인프라 대체 문서](backup-azure-backup-cloud-as-tape.md)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-173">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![보존 정책](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="955fd-175">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="955fd-175">In this example:</span></span>

    * <span data-ttu-id="955fd-176">백업은 매일 한 번 오후 12시 및 오후 8시에 수행되며(화면의 아래쪽 부분) 180일 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-176">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="955fd-177">토요일 오후 12시에 수행되는 백업은</span><span class="sxs-lookup"><span data-stu-id="955fd-177">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="955fd-178">104주 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-178">is retained for 104 weeks</span></span>
    * <span data-ttu-id="955fd-179">마지막 주 토요일 오후 12시에 수행되는 백업은</span><span class="sxs-lookup"><span data-stu-id="955fd-179">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="955fd-180">60개월 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-180">is retained for 60 months</span></span>
    * <span data-ttu-id="955fd-181">3월 마지막 주 토요일 오후 12시에 수행되는 백업은</span><span class="sxs-lookup"><span data-stu-id="955fd-181">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="955fd-182">10년 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-182">is retained for 10 years</span></span>
14. <span data-ttu-id="955fd-183">**다음** 을 클릭하고 초기 백업 복사본을 Azure에 전송하기 위한 적절한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-183">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="955fd-184">**네트워크를 통해 자동으로** 또는 **오프라인 백업**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-184">You can choose **Automatically over the network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="955fd-185">**네트워크를 통해 자동으로** 는 백업에 선택한 일정에 따라 Azure에 백업 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-185">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span></span>
    * <span data-ttu-id="955fd-186">**오프 라인 백업** 이 작동하는 방법을 [Azure 백업에서 오프라인 백업 워크플로](backup-azure-backup-import-export.md)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-186">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="955fd-187">관련 전송 메커니즘을 선택하여 초기 백업 복사본을 Azure로 보내고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-187">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span></span>
15. <span data-ttu-id="955fd-188">**요약** 화면에서 정책 세부 정보를 검토하면 **그룹 만들기** 단추를 클릭하여 워크플로를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-188">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span></span> <span data-ttu-id="955fd-189">**닫기** 단추를 클릭하고 작업 영역 모니터링에서 작업 진행 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-189">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span></span>

    ![진행 중인 보호 그룹 만들기](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="955fd-191">SQL Server 데이터베이스의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="955fd-191">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="955fd-192">이전 단계가 백업 정책을 만드는 동안 첫 번째 백업이 발생하면 "복구 지점"을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-192">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="955fd-193">스케줄러가 시작되기를 기다리는 대신 다음 단계는 수동으로 복구 지점의 생성을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-193">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="955fd-194">복구 지점을 만들기 전에 보호 그룹 상태가 데이터베이스를 **확인**으로 표시될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-194">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![보호 그룹 멤버](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="955fd-196">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **복구 지점 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-196">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![온라인 복구 지점 만들기](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="955fd-198">드롭다운 메뉴에서 **온라인 보호**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-198">Choose **Online Protection** in the drop-down menu and click **OK**.</span></span> <span data-ttu-id="955fd-199">그러면 Azure에서 복구 지점 만들기가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-199">This starts the creation of a recovery point in Azure.</span></span>

    ![복구 지점 만들기](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="955fd-201">다음 그림에서처럼 **모니터링** 작업 영역에서 진행 중인 작업의 진행 상황을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-201">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span></span>

    ![콘솔 모니터링](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="955fd-203">Azure에서 SQL Server 데이터베이스 복구</span><span class="sxs-lookup"><span data-stu-id="955fd-203">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="955fd-204">Azure에서 보호되는 엔터티(SQL Server 데이터베이스)를 복구하려면 다음 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-204">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="955fd-205">DPM 서버 관리 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-205">Open the DPM server Management Console.</span></span> <span data-ttu-id="955fd-206">DPM에서 백업된 서버를 확인할 수 있는 **복구** 작업 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-206">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span></span> <span data-ttu-id="955fd-207">필요한 데이터베이스로 이동합니다.(이 경우 ReportServer$ MSDPM2012)</span><span class="sxs-lookup"><span data-stu-id="955fd-207">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="955fd-208">**온라인**으로 끝나는 시간**에서 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-208">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![복구 지점 선택](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="955fd-210">데이터베이스 이름을 마우스 오른쪽 단추로 클릭하고 **복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-210">Right-click the database name and click **Recover**.</span></span>

    ![Azure에서 복구](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="955fd-212">DPM에서는 복구 지점에 대한 세부 정보를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-212">DPM shows the details of the recovery point.</span></span> <span data-ttu-id="955fd-213">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-213">Click **Next**.</span></span> <span data-ttu-id="955fd-214">데이터베이스를 덮어쓰려면 복구 형식 **SQL Server의 원본 인스턴스에 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-214">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="955fd-215">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-215">Click **Next**.</span></span>

    ![원래 위치로 복구](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="955fd-217">이 예제에서 DPM를 사용하면 다른 SQL Server 인스턴스 또는 독립 실행형 네트워크 폴더에 데이터베이스를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-217">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span></span>
4. <span data-ttu-id="955fd-218">**복구 옵션 지정** 화면에서 네트워크 대역폭 사용 제한을 같은 복구 옵션을 선택하여 복구에서 사용되는 대역폭을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-218">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="955fd-219">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-219">Click **Next**.</span></span>
5. <span data-ttu-id="955fd-220">**요약** 화면에서는 지금까지 제공하는 모든 복구 구성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-220">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="955fd-221">**복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-221">Click **Recover**.</span></span>

    <span data-ttu-id="955fd-222">복구 상태는 복구 중인 데이터베이스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-222">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="955fd-223">**닫기**를 클릭하여 마법사를 닫고 **모니터링** 작업 영역에서 진행률을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-223">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![복구 프로세스 시작](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="955fd-225">복구가 완료되면 복원된 데이터베이스는 응용 프로그램과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="955fd-225">Once the recovery is completed, the restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="955fd-226">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="955fd-226">Next Steps:</span></span>
<span data-ttu-id="955fd-227">•   [Azure Backup FAQ](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="955fd-227">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
