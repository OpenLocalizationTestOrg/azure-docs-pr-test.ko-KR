---
title: "Azure 백업 자격 증명 모음 aaaManage hello 클래식 배포 모델을 사용 하 여 Azure 서버 및 | Microsoft Docs"
description: "이 자습서 toolearn toomanage Azure 백업 자격 증명 모음 및 서버를 사용 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="75bb9-103">Azure 백업 자격 증명 모음 및 hello 클래식 배포 모델을 사용 하 여 서버 관리</span><span class="sxs-lookup"><span data-stu-id="75bb9-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75bb9-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="75bb9-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="75bb9-105">클래식</span><span class="sxs-lookup"><span data-stu-id="75bb9-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="75bb9-106">이 문서에서 hello Azure 클래식 포털을 통해 사용할 수 있는 hello 백업 관리 작업 및 hello Microsoft Azure 백업 에이전트의 개요를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75bb9-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="75bb9-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="75bb9-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75bb9-110">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="75bb9-111">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="75bb9-112">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="75bb9-113">2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="75bb9-114">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="75bb9-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="75bb9-115">모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="75bb9-116">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="75bb9-117">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="75bb9-118">관리 포털 작업</span><span class="sxs-lookup"><span data-stu-id="75bb9-118">Management portal tasks</span></span>
1. <span data-ttu-id="75bb9-119">Toohello 로그인 [관리 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="75bb9-120">클릭 **복구 서비스**, 백업 자격 증명 모음 tooview hello 빠른 시작 페이지의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![복구 서비스](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="75bb9-122">Hello 빠른 시작 페이지의 hello 위쪽 hello 옵션을 선택 하면 hello 사용 가능한 관리 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![관리 탭](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="75bb9-124">대시보드</span><span class="sxs-lookup"><span data-stu-id="75bb9-124">Dashboard</span></span>
<span data-ttu-id="75bb9-125">선택 **대시보드** toosee hello 사용 개요에 대 한 hello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="75bb9-126">hello **사용 개요** 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="75bb9-127">Windows 서버 hello 수 toocloud 등록</span><span class="sxs-lookup"><span data-stu-id="75bb9-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="75bb9-128">클라우드에서 보호 되는 Azure 가상 컴퓨터의 hello 수</span><span class="sxs-lookup"><span data-stu-id="75bb9-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="75bb9-129">hello Azure에서 사용 되는 총 저장소</span><span class="sxs-lookup"><span data-stu-id="75bb9-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="75bb9-130">최근 작업의 hello 상태</span><span class="sxs-lookup"><span data-stu-id="75bb9-130">hello status of recent jobs</span></span>

<span data-ttu-id="75bb9-131">Hello hello 대시보드 맨 아래에 hello 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="75bb9-132">**인증서 관리** -인증서를 사용 하는 tooregister hello 서버 인지 다음이 tooupdate hello 인증서를 사용 하 여 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="75bb9-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="75bb9-133">저장소 자격 증명을 사용하는 경우에는 **인증서 관리**를 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="75bb9-134">**삭제** -삭제 hello 현재 백업 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="75bb9-135">백업 자격 증명 모음이 더 이상 사용 중인 경우 toofree 저장 공간을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="75bb9-136">**삭제** hello 자격 증명 모음에서 등록 된 모든 서버를 삭제 한 후에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![백업 대시보드 작업](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="75bb9-138">등록된 항목</span><span class="sxs-lookup"><span data-stu-id="75bb9-138">Registered items</span></span>
<span data-ttu-id="75bb9-139">선택 **등록 된 항목** 한 hello 서버 tooview hello 이름을 toothis 자격 증명 모음을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![등록된 항목](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="75bb9-141">hello **형식** 필터 tooAzure 가상 컴퓨터의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="75bb9-142">자격 증명 모음 등록된 toothis hello 서버 tooview hello 이름 선택 **Windows server** hello에서 드롭다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="75bb9-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="75bb9-143">여기에서 hello 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="75bb9-144">**재등록을 허용** -사용할 수는 서버에 대해이 옵션을 선택 하는 경우 hello **등록 마법사** hello 온-프레미스 Microsoft Azure 백업 에이전트 tooregister hello 서버를 두 번째로 hello 백업 자격 증명 모음에 .</span><span class="sxs-lookup"><span data-stu-id="75bb9-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="75bb9-145">Hello 인증서 또는 서버를 다시 작성 toobe를 갖는 경우에 tooan 오류가 인해 toore 레지스터를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="75bb9-146">**삭제** -hello 백업 자격 증명 모음에서 서버를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="75bb9-147">모든 hello 서버와 관련 된 hello 저장 데이터가 즉시 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![등록된 항목 작업](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="75bb9-149">보호된 항목</span><span class="sxs-lookup"><span data-stu-id="75bb9-149">Protected items</span></span>
<span data-ttu-id="75bb9-150">선택 **보호 된 항목** hello 서버에서 백업 된 tooview hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![보호된 항목](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="75bb9-152">구성</span><span class="sxs-lookup"><span data-stu-id="75bb9-152">Configure</span></span>
<span data-ttu-id="75bb9-153">Hello에서 **구성** 탭 hello 적절 한 저장소 중복 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="75bb9-154">hello 최상의 시간 tooselect hello 저장소 중복 옵션은 자격 증명 모음을 만드는 바로 뒤와 모든 컴퓨터는 등록 된 tooit 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="75bb9-155">항목에 대 한 자격 증명 모음 등록된 toohello를 수행한 후 hello 저장소 중복 옵션이 잠겨 있으며 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![구성](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="75bb9-157">[저장소 중복](../storage/common/storage-redundancy.md)에 대한 자세한 내용은 이 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75bb9-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="75bb9-158">Microsoft Azure 백업 에이전트 작업</span><span class="sxs-lookup"><span data-stu-id="75bb9-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="75bb9-159">콘솔</span><span class="sxs-lookup"><span data-stu-id="75bb9-159">Console</span></span>
<span data-ttu-id="75bb9-160">열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 수 있습니다 *Microsoft Azure 백업*).</span><span class="sxs-lookup"><span data-stu-id="75bb9-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![백업 에이전트](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="75bb9-162">Hello에서 **동작** hello hello 백업 에이전트가 있는 경우 콘솔의 오른쪽에 사용할 수 있는 수행할 수 있습니다 관리 작업을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="75bb9-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="75bb9-163">서버 등록</span><span class="sxs-lookup"><span data-stu-id="75bb9-163">Register Server</span></span>
* <span data-ttu-id="75bb9-164">백업 예약</span><span class="sxs-lookup"><span data-stu-id="75bb9-164">Schedule Backup</span></span>
* <span data-ttu-id="75bb9-165">지금 백업</span><span class="sxs-lookup"><span data-stu-id="75bb9-165">Back Up now</span></span>
* <span data-ttu-id="75bb9-166">속성 변경</span><span class="sxs-lookup"><span data-stu-id="75bb9-166">Change Properties</span></span>

![에이전트 콘솔 작업](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="75bb9-168">너무**데이터 복구**, 참조 [파일 tooa Windows server 또는 Windows 클라이언트 컴퓨터 복원](backup-azure-restore-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="75bb9-169">기존 백업 수정</span><span class="sxs-lookup"><span data-stu-id="75bb9-169">Modify an existing backup</span></span>
1. <span data-ttu-id="75bb9-170">Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="75bb9-172">Hello에 **백업 예약 마법사** hello 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![예약된 백업 수정](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="75bb9-174">Tooadd 원하는 하거나 hello에 항목을 변경 하면 **항목 선택 tooBackup** 화면 클릭 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="75bb9-175">설정할 수도 있습니다 **제외 설정** hello 마법사의이 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="75bb9-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="75bb9-176">Tooexclude 파일 또는 파일 형식을 추가 하기 위한 hello 프로시저를 읽을 경우 [제외 설정](#exclusion-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="75bb9-177">Hello 파일 및 폴더를 누르고 tooback를 원하는 선택 **알겠습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![항목 추가](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="75bb9-179">Hello 지정 **백업 일정** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="75bb9-180">매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![백업 일정 변경](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="75bb9-182">Hello 백업 일정은이에 자세히 설명 되어 지정 [문서](backup-azure-backup-cloud-as-tape.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="75bb9-183">선택 hello **보존 정책** hello 백업 복사본 및 클릭에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![재방문 주기 정책 선택](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="75bb9-185">Hello에 **확인** 화면 hello 정보를 검토 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="75bb9-186">Hello 마법사 hello 만들기가 완료 되 면 **백업 일정**, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="75bb9-187">보호를 수정한 후 확인할 수 있습니다 toohello 이동 하 여 백업을 올바르게 트리거될 **작업** 백업 작업을 탭 하 고 hello에 변경 내용이 반영 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="75bb9-188">네트워크 제한 사용</span><span class="sxs-lookup"><span data-stu-id="75bb9-188">Enable Network Throttling</span></span>
<span data-ttu-id="75bb9-189">hello Azure 백업 에이전트 데이터 전송 시 네트워크 대역폭을 어떻게 사용 되는지 toocontrol 수 있는 조정 탭을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="75bb9-190">이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="75bb9-191">데이터의 제한 전송 tooback를 적용 하 고 활동을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="75bb9-192">tooenable 제한:</span><span class="sxs-lookup"><span data-stu-id="75bb9-192">tooenable throttling:</span></span>

1. <span data-ttu-id="75bb9-193">Hello에 **백업 에이전트**, 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="75bb9-194">선택 hello **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![네트워크 제한](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="75bb9-196">제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="75bb9-197">hello 대역폭 값 512kbps (초당) 크기는 512kb부터 시작 하 고 too1023 m b / 초 (Mbps)을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="75bb9-198">Hello 시작을 지정 하 고 완료를 수도 있습니다 **근무 시간**, hello 요일을 어떤 작업 것으로 간주 됩니다 (일)입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="75bb9-199">근무 시간을 지정 하는 hello 외부 hello 시간은 간주 toobe 비 작업 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="75bb9-200">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="75bb9-201">제외 설정</span><span class="sxs-lookup"><span data-stu-id="75bb9-201">Exclusion settings</span></span>
1. <span data-ttu-id="75bb9-202">열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 수 있습니다 *Microsoft Azure 백업*).</span><span class="sxs-lookup"><span data-stu-id="75bb9-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![백업 에이전트 열기](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="75bb9-204">Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="75bb9-206">백업 예약 마법사 hello hello를 그대로 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![일정 수정](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="75bb9-208">**제외 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-208">Click **Exclusions Settings**.</span></span>

    ![선택 항목 tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="75bb9-210">**제외 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-210">Click **Add Exclusion**.</span></span>

    ![제외 추가](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="75bb9-212">Hello 위치를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-212">Select hello location and then, click **OK**.</span></span>

    ![제외할 위치 선택](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="75bb9-214">Hello에 hello 파일 확장명 추가 **파일 형식을** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-214">Add hello file extension in hello **File Type** field.</span></span>

    ![파일 형식별 제외](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="75bb9-216">.mp3 확장명 추가</span><span class="sxs-lookup"><span data-stu-id="75bb9-216">Adding an .mp3 extension</span></span>

    ![파일 형식 예](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="75bb9-218">tooadd 다른 확장 클릭 **제외 추가** 하 고 다른 파일 형식 확장명 (.jpeg 확장명을 추가 합니다.)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![다른 파일 형식 예](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="75bb9-220">모든 hello 확장을 추가 했으므로 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="75bb9-221">클릭 하 여 hello 백업 예약 마법사를 통해 계속 **다음** hello까지 **확인 페이지**, 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="75bb9-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![제외 확인](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="75bb9-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75bb9-223">Next steps</span></span>
* [<span data-ttu-id="75bb9-224">Azure에서 Windows Server 또는 Windows 클라이언트 복원</span><span class="sxs-lookup"><span data-stu-id="75bb9-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="75bb9-225">Azure 백업에 대해 자세히 toolearn 참조 [Azure 백업 개요](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="75bb9-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="75bb9-226">Hello 방문 [Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="75bb9-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
