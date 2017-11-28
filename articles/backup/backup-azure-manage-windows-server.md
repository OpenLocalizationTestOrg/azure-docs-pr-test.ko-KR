---
title: "aaaManage Azure 복구 서비스 자격 증명 모음 및 서버 | Microsoft Docs"
description: "이 자습서 toolearn toomanage Azure 복구 서비스 자격 증명 모음 및 서버를 사용 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="9d1fd-103">Windows 컴퓨터용 Azure 복구 서비스 자격 증명 모음 및 서버 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="9d1fd-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d1fd-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="9d1fd-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="9d1fd-105">클래식</span><span class="sxs-lookup"><span data-stu-id="9d1fd-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="9d1fd-106">이 문서에서 hello Azure 포털 및 hello Microsoft Azure 백업 에이전트를 통해 사용할 수 있는 모니터 및 관리 작업이 백업 hello의 개요를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="9d1fd-107">이 문서에서는 이미 Azure 구독이 있으며 하나 이상의 Recovery Services Vault 를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="9d1fd-108">Recovery Services Vault 열기</span><span class="sxs-lookup"><span data-stu-id="9d1fd-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="9d1fd-109">hello 복구 서비스 자격 증명 모음 대시보드 hello 세부 정보 또는 특성 복구 서비스 자격 증명 모음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="9d1fd-110">Toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="9d1fd-111">Hello 허브 메뉴에서 클릭 **더 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-111">On hello Hub menu, click **More Services**.</span></span>

    ![Recovery Services Vault 목록 열기 1단계](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="9d1fd-113">복구 서비스 자격 증명 모음 tooopen 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="9d1fd-114">Hello 대화 상자에서 입력을 시작 **복구 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="9d1fd-115">Hello 목록이 필터링 됩니다 입력을 시작 하면 사용자의 입력에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="9d1fd-116">클릭 **복구 서비스 자격 증명 모음** toodisplay hello 목록이 복구 서비스 구독에 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="9d1fd-118">복구 서비스 자격 증명 모음 hello 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-118">hello list of Recovery Services vaults opens.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="9d1fd-120">자격 증명 모음 hello 목록에서 hello hello tooopen 원하는 복구 서비스 자격 증명 모음 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="9d1fd-121">hello 복구 서비스 자격 증명 모음 대시보드 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![복구 서비스 자격 증명 모음 대시보드](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="9d1fd-123">Hello 복구 서비스 자격 증명 모음을 연 했으므로 hello 모니터링 또는 관리 작업 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="9d1fd-124">백업 작업 및 경고 모니터링</span><span class="sxs-lookup"><span data-stu-id="9d1fd-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="9d1fd-125">작업을 모니터링 및 경고 hello에서 복구 서비스 자격 증명 모음 대시보드를 볼 위치:</span><span class="sxs-lookup"><span data-stu-id="9d1fd-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="9d1fd-126">백업 경고 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9d1fd-126">Backup alerts details</span></span>
* <span data-ttu-id="9d1fd-127">파일 및 폴더 뿐 아니라 hello 클라우드에서 보호 되는 Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9d1fd-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="9d1fd-128">Azure에서 사용되는 총 저장소</span><span class="sxs-lookup"><span data-stu-id="9d1fd-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="9d1fd-129">백업 작업 상태</span><span class="sxs-lookup"><span data-stu-id="9d1fd-129">Backup job status</span></span>

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="9d1fd-131">각이 타일에 hello 정보를 클릭 하면 관련된 작업을 관리 하는 hello 관련된 블레이드를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="9d1fd-132">Hello 맨 hello 대시보드</span><span class="sxs-lookup"><span data-stu-id="9d1fd-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="9d1fd-133">사용할 수 있는 백업 작업에 대한 액세스를 제공하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="9d1fd-134">자격 증명 모음에 백업-toohello 복구 서비스 새 파일 및 폴더 (또는 Azure Vm)를 백업 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="9d1fd-135">Delete-복구 서비스 자격 증명 모음 더 이상 사용 되지, toofree 저장 공간을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="9d1fd-136">삭제는 모든 보호 된 서버 hello 자격 증명 모음에서 삭제 한 후에 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="9d1fd-138">Azure 백업 에이전트에 의한 백업 경고</span><span class="sxs-lookup"><span data-stu-id="9d1fd-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="9d1fd-139">경고 수준</span><span class="sxs-lookup"><span data-stu-id="9d1fd-139">Alert Level</span></span> | <span data-ttu-id="9d1fd-140">전송되는 경고</span><span class="sxs-lookup"><span data-stu-id="9d1fd-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="9d1fd-141">중요</span><span class="sxs-lookup"><span data-stu-id="9d1fd-141">Critical</span></span> |<span data-ttu-id="9d1fd-142">백업 실패, 복구 실패</span><span class="sxs-lookup"><span data-stu-id="9d1fd-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="9d1fd-143">Warning</span><span class="sxs-lookup"><span data-stu-id="9d1fd-143">Warning</span></span> |<span data-ttu-id="9d1fd-144">(1 백 미만의 파일 toocorruption 문제 인해 백업 되지 않습니다 및 1 백만 개 이상의 파일이 성공적으로 백업) 경우 경고와 함께 완료 된 백업</span><span class="sxs-lookup"><span data-stu-id="9d1fd-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="9d1fd-145">정보 제공</span><span class="sxs-lookup"><span data-stu-id="9d1fd-145">Informational</span></span> |<span data-ttu-id="9d1fd-146">없음</span><span class="sxs-lookup"><span data-stu-id="9d1fd-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="9d1fd-147">백업 경고 관리</span><span class="sxs-lookup"><span data-stu-id="9d1fd-147">Manage Backup alerts</span></span>
<span data-ttu-id="9d1fd-148">Hello 클릭 **백업 경고** 타일 tooopen hello **백업 경고** 블레이드 경고 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![백업 경고](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="9d1fd-150">타일에 표시 하는 hello 백업 경고 수가 hello:</span><span class="sxs-lookup"><span data-stu-id="9d1fd-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="9d1fd-151">지난 24 시간 동안 확인되지 않은 중요한 경고</span><span class="sxs-lookup"><span data-stu-id="9d1fd-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="9d1fd-152">지난 24 시간 동안 확인되지 않은 경고</span><span class="sxs-lookup"><span data-stu-id="9d1fd-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="9d1fd-153">클릭는 각이 링크에서 이동할 toohello **백업 경고** 블레이드 (위험 또는 경고) 이러한 경고에 대 한 필터링 된 보기를 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="9d1fd-154">Hello 백업 경고 블레이드에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="9d1fd-155">경고와 적절 한 정보 tooinclude hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![열 선택](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="9d1fd-157">심각도, 상태 및 시작/종료 시간에 대한 경고를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-157">Filter alerts for severity, status and start/end times.</span></span>

    ![경고 필터링](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="9d1fd-159">심각도, 빈도 및 받는 사람에 대한 알림을 구성하며 경고를 켜거나 끕니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![경고 필터링](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="9d1fd-161">경우 **당 경고** 를 hello로 선택 **알림** 그룹화 또는 발생 하지 않습니다 전자 메일에 감소 하는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="9d1fd-162">모든 경고에 대해 알림 1개가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="9d1fd-163">Hello 기본 설정 이며 hello 확인 전자 메일 즉시 전송도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="9d1fd-164">경우 **시간별 다이제스트** 를 hello로 선택 **알림** 하나의 전자 메일에는 인하 toohello 사용자 보내집니다 주파수 지난 1 시간 동안 hello에 생성 된 새 경고를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="9d1fd-165">확인 전자 메일 hello 시간 hello 끝에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="9d1fd-166">심각도 수준에 따라 hello에 대 한 경고를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="9d1fd-167">중요</span><span class="sxs-lookup"><span data-stu-id="9d1fd-167">critical</span></span>
* <span data-ttu-id="9d1fd-168">Warning</span><span class="sxs-lookup"><span data-stu-id="9d1fd-168">warning</span></span>
* <span data-ttu-id="9d1fd-169">정보</span><span class="sxs-lookup"><span data-stu-id="9d1fd-169">information</span></span>

<span data-ttu-id="9d1fd-170">Hello로 hello 경고를 비활성화 **비활성화** hello 작업 세부 정보 블레이드에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="9d1fd-171">비활성화를 클릭하면 확인 참고 사항을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="9d1fd-172">Hello 열을 선택 하면 tooappear hello로 hello 경고의 일환으로 원하는 **열 선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="9d1fd-173">Hello에서 **설정** 블레이드를 선택 하 여 백업 경고를 관리 **모니터링 및 보고서 > 경고 및 이벤트 > 백업 경고** 클릭 한 다음 **필터** 또는  **알림을 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="9d1fd-174">백업 항목 관리</span><span class="sxs-lookup"><span data-stu-id="9d1fd-174">Manage Backup items</span></span>
<span data-ttu-id="9d1fd-175">이제 온-프레미스 백업 관리 hello 관리 포털에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="9d1fd-176">Hello 대시보드의 hello 백업 섹션에서는 hello **백업 항목** 타일 hello 백업 항목 수가 보호 toohello 자격 증명 모음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="9d1fd-177">클릭 **파일 폴더** hello 백업 항목 타일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![백업 항목 타일](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="9d1fd-179">각각의 특정 백업 나열 된 항목 표시 집합 tooFile 폴더를 필터링 하는 hello 백업 항목 hello로 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![백업 항목](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="9d1fd-181">Hello 목록에서 특정 백업 항목을 선택 하는 경우 해당 항목에 대 한 hello 필수 세부 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="9d1fd-182">Hello에서 **설정** 블레이드를 선택 하 여 파일 및 폴더 관리 **보호 된 항목 > 백업 항목** 다음를 선택 하 고 **파일 폴더** hello에서 드롭다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![설정에서 항목 백업](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="9d1fd-184">백업 작업 관리</span><span class="sxs-lookup"><span data-stu-id="9d1fd-184">Manage Backup jobs</span></span>
<span data-ttu-id="9d1fd-185">온-프레미스 (hello 온-프레미스 서버는 tooAzure 백업) 하는 경우와 Azure 백업에 대 한 백업 작업 hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="9d1fd-186">Hello hello 대시보드의 백업 섹션, hello 백업 작업 타일 hello 작업 수를 표시:</span><span class="sxs-lookup"><span data-stu-id="9d1fd-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="9d1fd-187">진행 중</span><span class="sxs-lookup"><span data-stu-id="9d1fd-187">in progress</span></span>
* <span data-ttu-id="9d1fd-188">지난 24 시간 동안 hello에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="9d1fd-189">toomanage 백업 작업을 클릭 하 여 hello **백업 작업** 타일을 hello 백업 작업 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![설정에서 항목 백업](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="9d1fd-191">Hello 백업 작업 블레이드에서 hello로 사용할 수 있는 hello 정보를 수정 하면 **열 선택** hello hello 페이지 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="9d1fd-192">사용 하 여 hello **필터** Azure 가상 컴퓨터 백업 파일 및 폴더 간에 단추 tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="9d1fd-193">백업 된 파일 및 폴더를 표시 되지 않으면, 클릭 **필터** hello 페이지를 선택 hello 위쪽에 단추 **파일 및 폴더** hello 항목 유형 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="9d1fd-194">Hello에서 **설정** 블레이드를 선택 하 여 백업 작업을 관리 **모니터링 및 보고서 > 작업 > 백업 작업** 다음를 선택 하 고 **파일 폴더** hello 드롭다운에서 드롭다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="9d1fd-195">백업 사용 모니터링</span><span class="sxs-lookup"><span data-stu-id="9d1fd-195">Monitor Backup usage</span></span>
<span data-ttu-id="9d1fd-196">Hello hello 대시보드의 백업 섹션, hello 백업 사용량 타일 Azure에서 사용 되는 hello 저장소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="9d1fd-197">다음에 대한 저장소 사용량이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="9d1fd-198">Hello 자격 증명 모음과 연결 된 클라우드 LRS 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="9d1fd-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="9d1fd-199">Hello 자격 증명 모음과 연결 된 클라우드 GRS 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="9d1fd-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="9d1fd-200">프로덕션 서버 관리</span><span class="sxs-lookup"><span data-stu-id="9d1fd-200">Manage your production servers</span></span>
<span data-ttu-id="9d1fd-201">toomanage 프로덕션 서버를 클릭 하 여 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="9d1fd-202">관리 아래에서 **백업 인프라 > 프로덕션 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="9d1fd-203">모든 사용 가능한 환경 서버 hello 프로덕션 서버 블레이드 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="9d1fd-204">서버 hello 목록 tooopen hello 서버 세부 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-204">Click on a server in hello list tooopen hello server details.</span></span>

![보호된 항목](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="9d1fd-206">열기 hello Azure 백업 에이전트</span><span class="sxs-lookup"><span data-stu-id="9d1fd-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="9d1fd-207">열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 *Microsoft Azure 백업*).</span><span class="sxs-lookup"><span data-stu-id="9d1fd-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="9d1fd-209">Hello에서 **동작** hello hello 백업 에이전트가 있는 경우 콘솔의 오른쪽에 사용할 수 있는 수행한 관리 작업을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="9d1fd-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="9d1fd-210">서버 등록</span><span class="sxs-lookup"><span data-stu-id="9d1fd-210">Register Server</span></span>
* <span data-ttu-id="9d1fd-211">백업 예약</span><span class="sxs-lookup"><span data-stu-id="9d1fd-211">Schedule Backup</span></span>
* <span data-ttu-id="9d1fd-212">지금 백업</span><span class="sxs-lookup"><span data-stu-id="9d1fd-212">Back Up now</span></span>
* <span data-ttu-id="9d1fd-213">속성 변경</span><span class="sxs-lookup"><span data-stu-id="9d1fd-213">Change Properties</span></span>

![Microsoft Azure 백업 에이전트 콘솔 작업](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="9d1fd-215">너무**데이터 복구**, 참조 [파일 tooa Windows server 또는 Windows 클라이언트 컴퓨터 복원](backup-azure-restore-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="9d1fd-216">Hello 백업 일정 수정</span><span class="sxs-lookup"><span data-stu-id="9d1fd-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="9d1fd-217">Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="9d1fd-219">Hello에 **백업 예약 마법사** hello 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="9d1fd-221">Tooadd 원하는 하거나 hello에 항목을 변경 하면 **항목 선택 tooBackup** 화면 클릭 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="9d1fd-222">설정할 수도 있습니다 **제외 설정** hello 마법사의이 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="9d1fd-223">Tooexclude 파일 또는 파일 형식을 추가 하기 위한 hello 프로시저를 읽을 경우 [제외 설정](#manage-exclusion-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="9d1fd-224">Hello 파일 및 폴더를 누르고 tooback를 원하는 선택 **알겠습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="9d1fd-226">Hello 지정 **백업 일정** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="9d1fd-227">매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="9d1fd-229">Hello 백업 일정은이에 자세히 설명 되어 지정 [문서](backup-azure-backup-cloud-as-tape.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="9d1fd-230">선택 hello **보존 정책** hello 백업 복사본 및 클릭에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="9d1fd-232">Hello에 **확인** 화면 hello 정보를 검토 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="9d1fd-233">Hello 마법사 hello 만들기가 완료 되 면 **백업 일정**, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="9d1fd-234">보호를 수정한 후 확인할 수 있습니다 toohello 이동 하 여 백업을 올바르게 트리거될 **작업** 백업 작업을 탭 하 고 hello에 변경 내용이 반영 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="9d1fd-235">네트워크 제한 사용</span><span class="sxs-lookup"><span data-stu-id="9d1fd-235">Enable Network Throttling</span></span>

<span data-ttu-id="9d1fd-236">hello Azure 백업 에이전트 데이터 전송 시 네트워크 대역폭을 어떻게 사용 되는지 toocontrol 수 있는 조정 탭을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="9d1fd-237">이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="9d1fd-238">데이터의 제한 전송 tooback를 적용 하 고 활동을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="9d1fd-239">tooenable 제한:</span><span class="sxs-lookup"><span data-stu-id="9d1fd-239">tooenable throttling:</span></span>

1. <span data-ttu-id="9d1fd-240">Hello에 **백업 에이전트**, 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="9d1fd-241">Hello에 * * 조정 탭을 선택 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![네트워크 제한](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="9d1fd-243">제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="9d1fd-244">hello 대역폭 값 512kbps (초당) 크기는 512kb부터 시작 하 고 too1023 m b / 초 (Mbps)을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="9d1fd-245">Hello 시작을 지정 하 고 완료를 수도 있습니다 **근무 시간**, hello 요일을 어떤 작업 것으로 간주 됩니다 (일)입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="9d1fd-246">근무 시간을 지정 하는 hello 외부 hello 시간은 간주 toobe 비 작업 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="9d1fd-247">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="9d1fd-248">제외 설정 관리</span><span class="sxs-lookup"><span data-stu-id="9d1fd-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="9d1fd-249">열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 수 있습니다 *Microsoft Azure 백업*).</span><span class="sxs-lookup"><span data-stu-id="9d1fd-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="9d1fd-251">Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="9d1fd-253">백업 예약 마법사 hello hello를 그대로 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="9d1fd-255">**제외 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-255">Click **Exclusions Settings**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="9d1fd-257">**제외 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-257">Click **Add Exclusion**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="9d1fd-259">Hello 위치를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-259">Select hello location and then, click **OK**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="9d1fd-261">Hello에 hello 파일 확장명 추가 **파일 형식을** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="9d1fd-263">.mp3 확장명 추가</span><span class="sxs-lookup"><span data-stu-id="9d1fd-263">Adding an .mp3 extension</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="9d1fd-265">tooadd 다른 확장 클릭 **제외 추가** 하 고 다른 파일 형식 확장명 (.jpeg 확장명을 추가 합니다.)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="9d1fd-267">모든 hello 확장을 추가 했으므로 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="9d1fd-268">클릭 하 여 hello 백업 예약 마법사를 통해 계속 **다음** hello까지 **확인 페이지**, 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="9d1fd-270">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="9d1fd-270">Frequently asked questions</span></span>
<span data-ttu-id="9d1fd-271">**Q 1입니다. hello 백업 작업 상태 이유 하지 않는 것 가져오기에 즉시 반영 포털 hello Azure 백업 에이전트에서에서 완료 된 것으로 표시?**</span><span class="sxs-lookup"><span data-stu-id="9d1fd-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="9d1fd-272">A1.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-272">A1.</span></span> <span data-ttu-id="9d1fd-273">없는 최대 지연 시간을 15 분 hello 백업 작업 상태 사이에 반영 됩니다 hello Azure 백업 에이전트 및 hello Azure 포털.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="9d1fd-274">**백업 작업이 실패할 때 Q.2, 얼마나 오래 걸립니까 tooraise 경고?**</span><span class="sxs-lookup"><span data-stu-id="9d1fd-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="9d1fd-275">A. 2가 경고는 hello Azure 백업 실패의 20 분 내에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="9d1fd-276">**Q3. 알림이 구성된 경우 메일이 전송되지 않는 경우가 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9d1fd-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="9d1fd-277">A3.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-277">A3.</span></span> <span data-ttu-id="9d1fd-278">다음 경우 hello hello 알림 순서 tooreduce hello 경고 노이즈에 전송 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="9d1fd-279">알림이 1 시간 마다 구성 및 경고가 발생 되 고 hello 시간 내에서 확인 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9d1fd-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="9d1fd-280">작업이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-280">Job is canceled.</span></span>
* <span data-ttu-id="9d1fd-281">원래 백업 작업이 진행 중이므로 두 번째 백업 작업이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="9d1fd-282">모니터링 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9d1fd-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="9d1fd-283">**문제:** 작업 및/또는 hello Azure 백업 에이전트에서 경고 hello 포털에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="9d1fd-284">**문제 해결 단계:** 프로세스 hello ```OBRecoveryServicesManagementAgent```, 보냅니다 hello 작업 및 경고 데이터 toohello Azure 백업 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="9d1fd-285">때때로 이 프로세스가 멈추거나 종료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="9d1fd-286">tooverify hello 프로세스가 실행 되지 않는, 열기 **작업 관리자** 하 고 있는지 확인 합니다. hello ```OBRecoveryServicesManagementAgent``` 프로세스가 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="9d1fd-287">Hello 프로세스를 실행 하지 않는 이라고 가정할 엽니다 **제어판** hello 서비스 목록을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="9d1fd-288">**Microsoft Azure Recovery Services 관리 에이전트**를 시작하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="9d1fd-289">자세한 내용은 hello 로그, 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9d1fd-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="9d1fd-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` 예:</span><span class="sxs-lookup"><span data-stu-id="9d1fd-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="9d1fd-291">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d1fd-291">Next steps</span></span>
* [<span data-ttu-id="9d1fd-292">Azure에서 Windows Server 또는 Windows 클라이언트 복원</span><span class="sxs-lookup"><span data-stu-id="9d1fd-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="9d1fd-293">Azure 백업에 대해 자세히 toolearn 참조 [Azure 백업 개요](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="9d1fd-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="9d1fd-294">Hello 방문 [Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="9d1fd-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
