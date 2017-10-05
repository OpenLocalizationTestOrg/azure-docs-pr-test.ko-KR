---
title: "System Center 2012 R2 DPM을 사용하여 Azure 백업에 Exchange 서버 백업 | Microsoft Docs"
description: "System Center 2012 R2 DPM을 사용하여 Azure 백업에 Exchange 서버를 백업하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="75716-103">System Center 2012 R2 DPM을 사용하여 Azure 백업에 Exchange 서버 백업</span><span class="sxs-lookup"><span data-stu-id="75716-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="75716-104">이 문서에서는 System Center 2012 R2 Data Protection Manager(DPM) 서버를 구성하여 Azure 백업에 Microsoft Exchange server를 백업하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="75716-105">업데이트</span><span class="sxs-lookup"><span data-stu-id="75716-105">Updates</span></span>
<span data-ttu-id="75716-106">Azure 백업을 사용하여 DPM 서버를 성공적으로 등록하려면 System Center 2012 R2 DPM 및 Azure 백업 에이전트의 최신 버전에 대한 최신 업데이트 롤업을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="75716-107">[Microsoft 카탈로그](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager)에서 최신 업데이트 롤업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75716-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="75716-108">이 문서의 예의 경우 Azure 백업 에이전트의 2.0.8719.0 버전을 설치하고 업데이트 롤업 6을 System Center 2012 R2 DPM에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="75716-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="75716-109">Prerequisites</span></span>
<span data-ttu-id="75716-110">계속하기 전에 워크로드를 보호하기 위하여 Microsoft Azure 백업 사용을 위한 [필수 구성 요소](backup-azure-dpm-introduction.md#prerequisites) 를 모두 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="75716-111">이러한 필수 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="75716-112">Azure 사이트에서 백업 자격 증명 모음을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="75716-113">DPM 서버에 에이전트 및 자격 증명 모음 자격 증명을 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="75716-114">에이전트는 DPM 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="75716-115">DPM 서버를 등록하는 데 자격 증명 모음 자격 증명이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="75716-116">Exchange 2016을 보호하는 경우, DPM 2012 R2 UR9 이상으로 업그레이드하세요.</span><span class="sxs-lookup"><span data-stu-id="75716-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="75716-117">DPM 보호 에이전트</span><span class="sxs-lookup"><span data-stu-id="75716-117">DPM protection agent</span></span>
<span data-ttu-id="75716-118">Exchange 서버에서 DPM 보호 에이전트를 설치하려면 다음 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="75716-119">방화벽이 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="75716-120">[에이전트에 대한 방화벽 예외 구성](https://technet.microsoft.com/library/Hh758204.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75716-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="75716-121">DPM 관리자 콘솔에서 **관리 > 에이전트 > 설치**를 클릭하여 Exchange 서버에 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="75716-122">자세한 단계는 [DPM 보호 에이전트 설치](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75716-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="75716-123">Exchange 서버에 보호 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="75716-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="75716-124">DPM 관리자 콘솔에서 **보호**를 클릭한 다음 도구 리본에서 **새로 만들기**를 클릭하여 **새 보호 그룹 만들기** 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="75716-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="75716-125">**시작** 화면에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="75716-126">**보호 그룹 형식 선택** 화면에서 **서버**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="75716-127">보호하려는 Exchange 서버 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75716-128">Exchange 2013을 보호하는 경우 [Exchange 2013 필수 구성 요소](https://technet.microsoft.com/library/dn751029.aspx)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="75716-129">다음 예제에서는 Exchange 2010 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![그룹 구성원 선택](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="75716-131">데이터 보호 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-131">Select the data protection method.</span></span>

    <span data-ttu-id="75716-132">보호 그룹의 이름을 지정하고 다음 옵션 모두를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="75716-133">디스크를 사용하여 단기 보호를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="75716-134">온라인 보호를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-134">I want online protection.</span></span>
6. <span data-ttu-id="75716-135">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="75716-135">Click **Next**.</span></span>
7. <span data-ttu-id="75716-136">Exchange Server 데이터베이스의 무결성을 확인하려는 경우 **Eseutil 실행하여 데이터 무결성 확인** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="75716-137">이 옵션을 선택한 후에 Exchange 서버에서 **eseutil** 명령을 실행하여 생성되는 I/O 트래픽을 방지하기 위해 백업 일관성 확인 작업이 DPM 서버에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75716-138">이 옵션을 사용하려면 DPM 서버에서 C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin 디렉터리로 Ese.dll 및 Eseutil.exe 파일을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="75716-139">그렇지 않으면 다음 오류가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="75716-140">![eseutil 오류](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="75716-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="75716-141">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="75716-141">Click **Next**.</span></span>
9. <span data-ttu-id="75716-142">**복사 백업**에 대한 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75716-143">데이터베이스의 DAG 복사본 하나 이상에 대한 "전체 백업"을 선택하지 않으면 로그는 잘리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="75716-144">**단기 백업**에 대한 목표를 구성하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="75716-145">사용 가능한 디스크 공간을 검토하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="75716-146">DPM 서버가 초기 복제 만들 시기를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="75716-147">일관성 확인 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="75716-148">Azure에 백업하려는 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="75716-149">예:</span><span class="sxs-lookup"><span data-stu-id="75716-149">For example:</span></span>

    ![온라인 보호 데이터 지정](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="75716-151">**Azure 백업**에 대한 일정을 정의하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="75716-152">예:</span><span class="sxs-lookup"><span data-stu-id="75716-152">For example:</span></span>

    ![온라인 백업 일정 지정](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="75716-154">온라인 복구 지점은 Express 전체 복구 지점을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="75716-155">따라서 Express 전체 복구 지점에 지정된 시간 후에 온라인 복구 지점을 예약해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="75716-156">**Azure 백업**에 대한 보존 정책을 구성하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="75716-157">온라인 복제 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="75716-158">큰 데이터베이스를 가지고 있다면 네트워크를 통해 만들 초기 백업에 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="75716-159">이 문제를 방지하려면 오프라인 백업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![온라인 보존 정책 지정](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="75716-161">설정을 확인한 다음 **그룹 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="75716-162">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="75716-163">Exchange 데이터베이스 복구</span><span class="sxs-lookup"><span data-stu-id="75716-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="75716-164">Exchange 데이터베이스를 복구하려면 DPM 관리자 콘솔에서 **복구** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="75716-165">복구하려는 Exchange 데이터베이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="75716-166">*복구 시간* 드롭 다운 목록에서 온라인 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="75716-167">**복구**를 클릭하여 **복구 마법사**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75716-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="75716-168">온라인 복구 지점의 경우 다섯 가지 형식의 복구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75716-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="75716-169">**원래 Exchange Server 위치에 복구:** 원래 Exchange 서버에 데이터가 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="75716-170">**Exchange 서버에서 다른 데이터베이스 복구:** 데이터는 다른 Exchange 서버에 있는 다른 데이터베이스에 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="75716-171">**복구 데이터베이스에 복구:** 데이터는 Exchange 복구 데이터베이스(RDB)에 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="75716-172">**네트워크 폴더에 복사:** 데이터는 네트워크 폴더에 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="75716-173">**테이프에 복사:** DPM 서버에 연결되고 구성된 테이프 라이브러리 또는 독립 실행형 테이프 드라이브가 있는 경우 복구 지점은 사용 가능한 테이프에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="75716-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![온라인 복제 선택](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="75716-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75716-175">Next steps</span></span>
* [<span data-ttu-id="75716-176">Azure 백업 - FAQ</span><span class="sxs-lookup"><span data-stu-id="75716-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
