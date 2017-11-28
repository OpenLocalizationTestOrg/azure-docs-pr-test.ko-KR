---
title: "Azure 백업 서버에서 데이터 aaaRecover | Microsoft Docs"
description: "복구 hello 데이터를 보호 한 모든 Azure 백업 서버 등록된 toothat 자격 증명 모음에서 tooa 복구 서비스 자격 증명 모음입니다."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a><span data-ttu-id="8bd7a-103">Azure Backup Server에서 데이터 복구</span><span class="sxs-lookup"><span data-stu-id="8bd7a-103">Recover data from Azure Backup Server</span></span>
<span data-ttu-id="8bd7a-104">복구 서비스 자격 증명 모음 tooa을 백업한 toorecover hello 데이터를 Azure 백업 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-104">You can use Azure Backup Server toorecover hello data you've backed up tooa Recovery Services vault.</span></span> <span data-ttu-id="8bd7a-105">hello 프로세스가 위한 작업 하므로 hello Azure 백업 서버 관리 콘솔에 통합 되 고 다른 Azure 백업 구성 요소에 대해 비슷한 toohello 복구 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-105">hello process for doing so is integrated into hello Azure Backup Server management console, and is similar toohello recovery workflow for other Azure Backup components.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd7a-106">이 문서는 [System Center Data Protection Manager 2012 R2 UR7 이상] (https://support.microsoft.com/en-us/kb/3065246)에 적용할 수 hello와 결합 [최신 Azure 백업 에이전트](http://aka.ms/azurebackup_agent)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-106">This article is applicable for [System Center Data Protection Manager 2012 R2 with UR7 or later] (https://support.microsoft.com/en-us/kb/3065246), combined with hello [latest Azure Backup agent](http://aka.ms/azurebackup_agent).</span></span>
>
>

<span data-ttu-id="8bd7a-107">Azure 백업 서버에서 toorecover 데이터:</span><span class="sxs-lookup"><span data-stu-id="8bd7a-107">toorecover data from an Azure Backup Server:</span></span>

1. <span data-ttu-id="8bd7a-108">Hello에서 **복구** hello Azure 백업 서버 관리 콘솔의 탭을 클릭 **외부 DPM 추가 '** (hello에 hello 화면 맨 왼쪽).</span><span class="sxs-lookup"><span data-stu-id="8bd7a-108">From hello **Recovery** tab of hello Azure Backup Server management console, click **'Add External DPM'** (at hello top left of hello screen).</span></span>   
    <span data-ttu-id="8bd7a-109">![외부 DPM 추가](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span><span class="sxs-lookup"><span data-stu-id="8bd7a-109">![Add External DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span></span>
2. <span data-ttu-id="8bd7a-110">새 다운로드 **자격 증명을 자격 증명 모음** hello hello와 연결 된 자격 증명 모음에서 **Azure 백업 서버** hello 데이터 복구 중인 경우 Azure 백업 서버 hello Azure 백업 서버 hello 목록에서 선택 hello 복구 서비스 자격 증명 모음에 등록 하 고 hello 제공 **암호화의 암호** 해당 데이터를 복구 중인 hello 서버와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-110">Download new **vault credentials** from hello vault associated with hello **Azure Backup Server** where hello data is being recovered, choose hello Azure Backup Server from hello list of Azure Backup Servers registered with hello Recovery Services vault, and provide hello **encryption passphrase** associated with hello server whose data is being recovered.</span></span>

    ![외부 DPM 자격 증명](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > <span data-ttu-id="8bd7a-112">Azure 백업 서버에 연결 된 hello 동일만 자격 증명 모음 등록 서로의 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-112">Only Azure Backup Servers associated with hello same registration vault can recover each other’s data.</span></span>
   >
   >

    <span data-ttu-id="8bd7a-113">Hello 외부 Azure 백업 서버를 성공적으로 추가 hello 외부 서버 hello 데이터를 검색 하는 hello에서 로컬 Azure 백업 서버 hello **복구** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-113">Once hello External Azure Backup Server is successfully added, you can browse hello data of hello external server and hello local Azure Backup Server from hello **Recovery** tab.</span></span>
3. <span data-ttu-id="8bd7a-114">찾아보기 hello에 의해 보호 되는 프로덕션 서버의 사용 가능한 목록 외부 Azure 백업 서버 hello 고 hello 적절 한 데이터 원본을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-114">Browse hello available list of production servers protected by hello external Azure Backup Server and select hello appropriate data source.</span></span>

    ![외부 DPM 서버 찾아보기](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. <span data-ttu-id="8bd7a-116">선택 **월과 연도 hello** hello에서 **복구 지점을** 드롭다운 선택 hello 필요한 **복구 날짜** hello 복구 지점을 만들고, 선택 hello 된 시기에 대 한 **복구 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-116">Select **hello month and year** from hello **Recovery points** drop down, select hello required **Recovery date** for when hello recovery point was created, and select hello **Recovery time**.</span></span>

    <span data-ttu-id="8bd7a-117">파일 및 폴더의 목록을 찾아볼 수 있으며 tooany 위치 복구는 hello 아래쪽 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-117">A list of files and folders appears in hello bottom pane, which can be browsed and recovered tooany location.</span></span>

    ![외부 DPM 서버 복구 지점](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. <span data-ttu-id="8bd7a-119">Hello 적절 한 항목을 마우스 오른쪽 단추로 클릭 하 고 클릭 **복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-119">Right click hello appropriate item and click **Recover**.</span></span>

    ![외부 DPM 복구](./media/backup-azure-alternate-dpm-server/recover.png)
6. <span data-ttu-id="8bd7a-121">검토 hello **복구 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-121">Review hello **Recover Selection**.</span></span> <span data-ttu-id="8bd7a-122">Hello 백업 복사본 생성 된 hello 소스 뿐 아니라 hello 데이터 복구 되 고 hello 백업 복사본의 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-122">Verify hello data and time of hello backup copy being recovered, as well as hello source from which hello backup copy was created.</span></span> <span data-ttu-id="8bd7a-123">Hello 선택 올바르지 않으면 클릭 **취소** toonavigate 백 toorecovery 탭 tooselect 적절 한 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-123">If hello selection is incorrect, click **Cancel** toonavigate back toorecovery tab tooselect appropriate recovery point.</span></span> <span data-ttu-id="8bd7a-124">클릭 하 여 hello 선택 올바르면 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-124">If hello selection is correct, click **Next**.</span></span>

    ![외부 DPM 복구 요약](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. <span data-ttu-id="8bd7a-126">선택 **tooan 대체 위치 복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-126">Select **Recover tooan alternate location**.</span></span> <span data-ttu-id="8bd7a-127">**찾아보기** toohello hello 복구에 대 한 정확한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-127">**Browse** toohello correct location for hello recovery.</span></span>

    ![외부 DPM 복구 대체 위치](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. <span data-ttu-id="8bd7a-129">너무 관련 hello 옵션을 선택**복사본 만들기**, **Skip**, 또는 **덮어쓰기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-129">Choose hello option related too**create copy**, **Skip**, or **Overwrite**.</span></span>

   * <span data-ttu-id="8bd7a-130">**복사본 만들기** -이름 충돌이 발생 하는 경우 hello 파일의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-130">**Create copy** - creates a copy of hello file if there is a name collision.</span></span>
   * <span data-ttu-id="8bd7a-131">**Skip** -이름 충돌이 발생 하는 경우 hello 원본 파일을 두 hello 파일 복구 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-131">**Skip** - if there is a name collision, does not recover hello file which leaves hello original file.</span></span>
   * <span data-ttu-id="8bd7a-132">**덮어쓰기** -이름 충돌이 발생 하는 경우 hello hello 파일의 기존 복사본을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-132">**Overwrite** - if there is a name collision, overwrites hello existing copy of hello file.</span></span>

     <span data-ttu-id="8bd7a-133">Hello 적절 한 옵션을 너무 선택**보안 복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-133">Choose hello appropriate option too**Restore security**.</span></span> <span data-ttu-id="8bd7a-134">Hello 데이터를 복구 중인 hello 대상 컴퓨터의 보안 설정 hello 또는 hello 복구 지점이 만들어진 hello 시 적용 가능한 tooproduct 있는 hello 보안 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-134">You can apply hello security settings of hello destination computer where hello data is being recovered or hello security settings that were applicable tooproduct at hello time hello recovery point was created.</span></span>

     <span data-ttu-id="8bd7a-135">식별 여부는 **알림** hello 복구를 성공적으로 완료 되 면 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-135">Identify whether a **Notification** is sent, once hello recovery successfully completes.</span></span>

     ![외부 DPM 복구 알림](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. <span data-ttu-id="8bd7a-137">hello **요약** 화면은 지금까지 사용 하도록 선택한 hello 옵션을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-137">hello **Summary** screen lists hello options chosen so far.</span></span> <span data-ttu-id="8bd7a-138">클릭 한 후 **'복구'**, hello 데이터는 복구 된 toohello 온-프레미스 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-138">Once you click **‘Recover’**, hello data is recovered toohello appropriate on-premises location.</span></span>

    ![외부 DPM 복구 옵션 요약](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > <span data-ttu-id="8bd7a-140">hello에서 hello 복구 작업을 모니터링할 수 있습니다 **모니터링** hello Azure 백업 서버를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-140">hello recovery job can be monitored in hello **Monitoring** tab of hello Azure Backup Server.</span></span>
   >
   >

    ![복구 모니터링](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. <span data-ttu-id="8bd7a-142">클릭할 수 있는 **외부 DPM 지우기** hello에 **복구** hello hello 외부 DPM 서버의 DPM 서버 tooremove hello 보기를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-142">You can click **Clear External DPM** on hello **Recovery** tab of hello DPM server tooremove hello view of hello external DPM server.</span></span>

    ![외부 DPM 지우기](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a><span data-ttu-id="8bd7a-144">오류 메시지 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8bd7a-144">Troubleshooting Error Messages</span></span>
| <span data-ttu-id="8bd7a-145">번호</span><span class="sxs-lookup"><span data-stu-id="8bd7a-145">No.</span></span> | <span data-ttu-id="8bd7a-146">오류 메시지</span><span class="sxs-lookup"><span data-stu-id="8bd7a-146">Error Message</span></span> | <span data-ttu-id="8bd7a-147">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="8bd7a-147">Troubleshooting steps</span></span> |
|:---:|:--- |:--- |
| <span data-ttu-id="8bd7a-148">1.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-148">1.</span></span> |<span data-ttu-id="8bd7a-149">이 서버는 등록 된 toohello hello 자격 증명 모음 자격 증명에서 지정한 자격 증명 모음 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-149">This server is not registered toohello vault specified by hello vault credential.</span></span> |<span data-ttu-id="8bd7a-150">**원인:** 때이 오류가 나타나는 선택한 hello 자격 증명 모음 자격 증명 파일에 속하지 않은 toohello 복구 서비스 자격 증명 모음에 있는 hello 복구를 시도 하는 Azure 백업 서버와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-150">**Cause:** This error appears when hello vault credential file selected does not belong toohello Recovery Services vault associated with Azure Backup Server on which hello recovery is attempted.</span></span> <br> <span data-ttu-id="8bd7a-151">**해결 방법:** 다운로드 hello 자격 증명 모음 자격 증명 파일을 hello 복구 서비스 자격 증명 모음 toowhich hello Azure 백업 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-151">**Resolution:** Download hello vault credential file from hello Recovery Services vault toowhich hello Azure Backup Server is registered.</span></span> |
| <span data-ttu-id="8bd7a-152">2.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-152">2.</span></span> |<span data-ttu-id="8bd7a-153">Hello 복구 가능한 데이터를 사용할 수 없습니다 또는 hello 선택한 서버가 DPM 서버가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-153">Either hello recoverable data is not available or hello selected server is not a DPM server.</span></span> |<span data-ttu-id="8bd7a-154">**원인:** hello 서버 hello 메타 데이터를 아직 업로드 하지 않은 또는 hello 선택한 서버를 사용할 수 없습니다 (즉, Windows Server 또는 Windows Client)는 Azure 백업 서버 또는 되어 없는 다른 Azure 백업 서버 등록된 toohello 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-154">**Cause:** There are no other Azure Backup Servers registered toohello Recovery Services vault, or hello servers have not yet uploaded hello metadata, or hello selected server is not an Azure Backup Server (aka Windows Server or Windows Client).</span></span> <br> <span data-ttu-id="8bd7a-155">**해결 방법:** 다른 Azure 백업 서버 등록된 toohello 복구 서비스 자격 증명 모음에 있는 경우 해당 hello 최신 Azure 백업 에이전트가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-155">**Resolution:** If there are other Azure Backup Servers registered toohello Recovery Services vault, ensure that hello latest Azure Backup agent is installed.</span></span> <br><span data-ttu-id="8bd7a-156">다른 Azure 백업 서버 등록된 toohello 복구 서비스 자격 증명 모음에 있는 경우 하루 설치 toostart hello 복구 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-156">If there are other Azure Backup Servers registered toohello Recovery Services vault, wait for a day after installation toostart hello recovery process.</span></span> <span data-ttu-id="8bd7a-157">hello 야간 작업에 대 한 모든 보호 된 hello 백업 toocloud hello 메타 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-157">hello nightly job will upload hello metadata for all hello protected backups toocloud.</span></span> <span data-ttu-id="8bd7a-158">hello 데이터 복구를 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-158">hello data will be available for recovery.</span></span> |
| <span data-ttu-id="8bd7a-159">3.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-159">3.</span></span> |<span data-ttu-id="8bd7a-160">다른 DPM 서버가 없는 경우 등록 된 toothis 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="8bd7a-160">No other DPM server is registered toothis vault.</span></span> |<span data-ttu-id="8bd7a-161">**원인:** 없는 다른 Azure 백업 서버를 등록 된 toohello 자격 증명 모음은 hello에서 복구를 시도 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-161">**Cause:** There are no other Azure Backup Servers  that are registered toohello vault from which hello recovery is being attempted.</span></span><br><span data-ttu-id="8bd7a-162">**해결 방법:** 다른 Azure 백업 서버 등록된 toohello 복구 서비스 자격 증명 모음에 있는 경우 해당 hello 최신 Azure 백업 에이전트가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-162">**Resolution:** If there are other Azure Backup Servers registered toohello Recovery Services vault, ensure that hello latest Azure Backup agent is installed.</span></span><br><span data-ttu-id="8bd7a-163">다른 Azure 백업 서버 등록된 toohello 복구 서비스 자격 증명 모음에 있는 경우 하루 설치 toostart hello 복구 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-163">If there are other Azure Backup Servers registered toohello Recovery Services vault, wait for a day after installation toostart hello recovery process.</span></span> <span data-ttu-id="8bd7a-164">hello 야간 작업에 대 한 모든 보호 된 백업 toocloud hello 메타 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-164">hello nightly job uploads hello metadata for all protected backups toocloud.</span></span> <span data-ttu-id="8bd7a-165">hello 데이터 복구를 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-165">hello data will be available for recovery.</span></span> |
| <span data-ttu-id="8bd7a-166">4.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-166">4.</span></span> |<span data-ttu-id="8bd7a-167">다음 서버 hello와 연결 된 암호는 hello 암호화의 암호가 일치 하지 않습니다.**<server name>**</span><span class="sxs-lookup"><span data-stu-id="8bd7a-167">hello encryption passphrase provided does not match with passphrase associated with hello following server: **<server name>**</span></span> |<span data-ttu-id="8bd7a-168">**원인:** hello 암호화의 암호 hello 프로세스 hello 데이터를 복구 중인 hello Azure 백업 서버 데이터에서에서 암호화에 사용 된 hello 암호화의 암호가 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-168">**Cause:** hello encryption passphrase used in hello process of encrypting hello data from hello Azure Backup Server’s data that is being recovered does not match hello encryption passphrase provided.</span></span> <span data-ttu-id="8bd7a-169">hello 에이전트는 없습니다 toodecrypt hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-169">hello agent is unable toodecrypt hello data.</span></span> <span data-ttu-id="8bd7a-170">따라서 hello 복구가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-170">Hence hello recovery fails.</span></span><br><span data-ttu-id="8bd7a-171">**해결 방법:** hello 정확한 동일한 암호화와 관련 된 암호가 hello 해당 데이터를 복구 중인 Azure 백업 서버를 제공 하세요.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-171">**Resolution:** Please provide hello exact same encryption passphrase associated with hello Azure Backup Server whose data is being recovered.</span></span> |

## <a name="frequently-asked-questions"></a><span data-ttu-id="8bd7a-172">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="8bd7a-172">Frequently asked questions</span></span>

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a><span data-ttu-id="8bd7a-173">UR7과 최신 Azure Backup 에이전트를 설치한 후에 외부 DPM 서버를 추가할 수 없는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8bd7a-173">Why can’t I add an external DPM server after installing UR7 and latest Azure Backup agent?</span></span>

<span data-ttu-id="8bd7a-174">적어도 하루 hello UR7 및 toostart 최신 Azure 백업 에이전트를 설치한 후 기다려야 hello 있는 데이터 원본에 포함 된 DPM 서버 보호 된 toohello 클라우드 (업데이트 롤업 7 이전의 업데이트 롤업을 사용)에서 **외부 DPM 추가 서버** .</span><span class="sxs-lookup"><span data-stu-id="8bd7a-174">For hello DPM servers with data sources that are protected toohello cloud (by using an update rollup earlier than Update Rollup 7), you must wait at least one day after installing hello UR7 and latest Azure Backup agent, toostart **Add External DPM server**.</span></span> <span data-ttu-id="8bd7a-175">hello 하루 기간은 hello DPM 보호 그룹 tooAzure의 필요한 tooupload hello 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-175">hello one-day time period is needed tooupload hello metadata of hello DPM protection groups tooAzure.</span></span> <span data-ttu-id="8bd7a-176">보호 그룹 메타 데이터 업로드 야간 작업을 통해 처음으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-176">Protection group metadata is uploaded hello first time through a nightly job.</span></span>

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a><span data-ttu-id="8bd7a-177">Hello 필요한 hello Microsoft Azure 복구 서비스 에이전트의 최소 버전은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8bd7a-177">What is hello minimum version of hello Microsoft Azure Recovery Services agent needed?</span></span>

<span data-ttu-id="8bd7a-178">최소 버전의 hello Microsoft Azure 복구 서비스 에이전트 또는 Azure 백업 에이전트, 필수 tooenable hello이 기능은 2.0.8719.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-178">hello minimum version of hello Microsoft Azure Recovery Services agent, or Azure Backup agent, required tooenable this feature is 2.0.8719.0.</span></span>  <span data-ttu-id="8bd7a-179">tooview hello 에이전트의 버전: 제어판을 열고  **>**  모든 제어판 항목  **>**  프로그램 및 기능  **>**  Microsoft Azure 복구 서비스 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-179">tooview hello agent's version: open Control Panel **>** All Control Panel items **>** Programs and features **>** Microsoft Azure Recovery Services Agent.</span></span> <span data-ttu-id="8bd7a-180">보다 작은 2.0.8719.0 hello 버전을 사용 하는 경우 다운로드 하 고 hello 설치 [최신 Azure 백업 에이전트](https://go.microsoft.com/fwLink/?LinkID=288905)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd7a-180">If hello version is less than 2.0.8719.0, download and install hello [latest Azure Backup agent](https://go.microsoft.com/fwLink/?LinkID=288905).</span></span>

![외부 DPM 지우기](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a><span data-ttu-id="8bd7a-182">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="8bd7a-182">Next steps:</span></span>
<span data-ttu-id="8bd7a-183">•   [Azure Backup FAQ](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8bd7a-183">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
