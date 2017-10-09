---
title: "Windows 시스템 상태 tooAzure aaaBack | Microsoft Docs"
description: "Windows Server 및/또는 Windows 컴퓨터 tooAzure hello 시스템 상태를 tooback에 알아봅니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "어떻게 toobackup; 어떻게 tooback; 백업 파일 및 폴더"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="e9828-104">Resource Manager 배포에서 Windows 시스템 상태 백업</span><span class="sxs-lookup"><span data-stu-id="e9828-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="e9828-105">이 문서에서는 Windows 서버 시스템을 tooback tooAzure를 명시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="e9828-106">자습서 의도 한 toowalk는 hello 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="e9828-107">Azure 백업에 대 한 자세한 tooknow 하려는 경우이 내용을 읽고 [개요](backup-introduction-to-azure-backup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="e9828-108">Azure 구독이 없는 경우 모든 Azure 서비스에 액세스할 수 있는 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e9828-109">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="e9828-109">Create a recovery services vault</span></span>
<span data-ttu-id="e9828-110">파일 및 폴더를 tooback, toocreate hello 지역 toostore hello 데이터를 원하는 위치에 복구 서비스 자격 증명 모음 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="e9828-111">Toodetermine 원하는 저장소를 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="e9828-112">복구 서비스 자격 증명 모음 toocreate</span><span class="sxs-lookup"><span data-stu-id="e9828-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="e9828-113">그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="e9828-114">Hello 허브 메뉴에서 클릭 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스** 클릭 **복구 서비스 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="e9828-116">Hello 구독에서 복구 서비스 자격 증명 모음 인 경우 hello 자격 증명 모음 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="e9828-117">Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="e9828-119">hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="e9828-121">에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="e9828-122">hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="e9828-123">이름을 2~50자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="e9828-124">문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="e9828-125">Hello에 **구독** 섹션 hello 드롭 다운 메뉴 toochoose hello Azure 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="e9828-126">단일 구독을 사용 하는 경우 해당 구독 표시 되 고 toohello 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="e9828-127">어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="e9828-128">조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="e9828-129">Hello에 **리소스 그룹** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e9828-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="e9828-130">선택 **새로 만들기** toocreate 리소스 그룹에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="e9828-131">또는</span><span class="sxs-lookup"><span data-stu-id="e9828-131">Or</span></span>
    * <span data-ttu-id="e9828-132">선택 **기존 항목 사용** hello 드롭 다운 메뉴 toosee hello 사용 가능한 리소스 그룹의 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="e9828-133">리소스 그룹에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="e9828-134">클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="e9828-135">여기에서이 선택한 hello 지리적 지역에 백업 데이터를 보내는 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="e9828-136">Hello 복구 서비스 자격 증명 모음 블레이드의 hello 아래쪽 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="e9828-137">복구 서비스 자격 증명 모음에 만든 toobe hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="e9828-138">Hello 포털의 상단 오른쪽 영역 hello에서에서 hello 상태 알림을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="e9828-139">자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="e9828-140">몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="e9828-142">자격 증명 모음 자격 증명 모음은 복구 서비스의 hello 목록에 표시 되는 경우 준비 tooset hello 저장소 중복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="e9828-143">Hello 자격 증명 모음에 대 한 저장소 중복성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="e9828-144">복구 서비스 자격 증명 모음을 만들 때 저장소 중복 구성 된 hello 방식으로 원하는 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="e9828-145">Hello에서 **복구 서비스 자격 증명 모음** 블레이드에서 hello 새 자격 증명 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![복구 서비스 자격 증명 모음의 hello 목록에서 hello 새 자격 증명 모음을 선택 합니다.](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="e9828-147">Hello 자격 증명 모음을 선택 하면 hello **복구 서비스 자격 증명 모음** 블레이드 좁힐 및 hello 설정 블레이드에서 (*hello hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) 및 hello 자격 증명 모음 세부 정보 블레이드에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![새 자격 증명 모음에 대 한 hello 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="e9828-149">Hello 새 자격 증명 모음의 설정 블레이드에서 toohello 관리 섹션 아래로 수직 슬라이드 tooscroll hello를 사용 하 여 마우스 클릭 **백업 인프라**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="e9828-150">hello 백업 인프라 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="e9828-151">Hello 백업 인프라 블레이드에서 클릭 **백업 구성** tooopen hello **백업 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![새 자격 증명 모음에 대 한 저장소 구성을 hello 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="e9828-153">자격 증명 모음에 대 한 hello 적절 한 저장소 복제 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="e9828-155">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="e9828-156">기본 백업 저장소 끝점으로 Azure를 사용 하는 경우 계속 toouse **지리적 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="e9828-157">기본 백업 저장소 끝점으로 Azure를 사용 하지 않는 경우 선택할 **로컬 중복**, hello Azure 저장소 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="e9828-158">[지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9828-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="e9828-159">이제 자격 증명 모음을 만들었으므로 Windows 시스템 상태를 백업하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="e9828-160">Hello 자격 증명 모음 구성</span><span class="sxs-lookup"><span data-stu-id="e9828-160">Configure hello vault</span></span>
1. <span data-ttu-id="e9828-161">Hello 시작 섹션에 복구 서비스 자격 증명 모음 블레이드 (hello 모음 방금 만든)에 대 한 hello, 클릭 **백업**, 그 다음에 hello **백업 시작** 블레이드를  **백업 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="e9828-163">hello **백업 목표** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-163">hello **Backup Goal** blade opens.</span></span>

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="e9828-165">Hello에서 **여기서 작업이 실행 되는?** 드롭 다운 메뉴 **온-프레미스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="e9828-166">Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="e9828-167">Hello에서 **하 신 toobackup 원하는?** 메뉴 선택 **시스템 상태**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![파일 및 폴더 구성](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="e9828-169">확인을 클릭 하면 확인 표시가 나타납니다 다음 너무**백업 목표**, 및 hello **준비 인프라** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![백업 목표 구성, 다음으로 인프라 준비](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="e9828-171">Hello에 **준비 인프라** 블레이드에서 클릭 **Windows Server 용 에이전트 다운로드 또는 Windows Client**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="e9828-173">Windows Server 필수 항목을 사용 하는, 용 Windows Server 필수 toodownload hello 에이전트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="e9828-174">팝업 메뉴 toorun 묻는 또는 MARSAgentInstaller.exe 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller 대화 상자](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="e9828-176">Hello 다운로드 팝업 메뉴에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="e9828-177">기본적으로 hello **MARSagentinstaller.exe** 파일이 tooyour Downloads 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="e9828-178">Hello 설치 관리자가 완료 되 면 toorun hello installer 또는 hello 폴더를 열 경우 묻는 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="e9828-180">Tooinstall hello 에이전트를 아직 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="e9828-181">Hello 자격 증명 모음 자격 증명을 다운로드 한 후 hello 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="e9828-182">Hello에 **준비 인프라** 블레이드에서 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![자격 증명 모음 자격 증명 다운로드](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="e9828-184">자격 증명 모음 hello tooyour 다운로드 폴더를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="e9828-185">Hello 자격 증명 모음 자격 증명 다운로드를 완료 한 후 tooopen 원하는 또는 hello 자격 증명을 저장 하는 경우 요청 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="e9828-186">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-186">Click **Save**.</span></span> <span data-ttu-id="e9828-187">실수로 누르면 **열려**, tooopen hello에 대 한 자격 증명 모음 자격 증명을 시도 하는 hello 대화 상자, 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="e9828-188">Hello 자격 증명 모음을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="e9828-189">Toohello 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-189">Proceed toohello next step.</span></span> <span data-ttu-id="e9828-190">hello 자격 증명 모음 자격 증명이 hello Downloads 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![자격 증명 모음 자격 증명 다운로드 완료](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="e9828-192">설치 하 고 hello 에이전트 등록</span><span class="sxs-lookup"><span data-stu-id="e9828-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="e9828-193">Hello Azure 포털을 통해 사용할 수 있도록 백업을 사용할 수 없는 경우, 아직</span><span class="sxs-lookup"><span data-stu-id="e9828-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="e9828-194">Windows 서버 시스템 상태를 Microsoft Azure 복구 서비스 에이전트 tooback hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="e9828-195">Hello를 두 번 클릭 **MARSagentinstaller.exe** hello 다운로드 폴더 (또는 다른 저장된 위치).</span><span class="sxs-lookup"><span data-stu-id="e9828-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="e9828-196">hello 설치 관리자는 일련의 메시지를, 추출할 때는 설치 및 hello 복구 서비스 에이전트 등록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Recovery Services 에이전트 설치 관리자 자격 증명을 실행](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="e9828-198">Hello Microsoft Azure 복구 서비스 에이전트 설치 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="e9828-199">toocomplete hello 마법사 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="e9828-200">Hello 설치 및 캐시 폴더의 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="e9828-201">프록시 서버 tooconnect toohello를 사용 하는 경우 프록시 서버 정보를 제공 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="e9828-202">인증된 프록시를 사용하는 경우에는 사용자 이름 및 암호 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="e9828-203">Hello 다운로드 한 자격 증명 모음 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="e9828-204">Hello 암호화의 암호를 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e9828-205">끊어지거나 hello 암호를 잊은 경우 Microsoft hello 백업 데이터를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="e9828-206">Hello 파일을 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-206">Save hello file in a secure location.</span></span> <span data-ttu-id="e9828-207">것이 필수 toorestore 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="e9828-208">hello 에이전트를 지금 설치 하 고 등록 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="e9828-209">준비 tooconfigure 하 고 백업을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="e9828-210">Windows Server 시스템 상태 백업(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="e9828-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="e9828-211">hello 초기 백업에는 세 가지 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="e9828-212">Hello Azure 백업 에이전트를 사용 하 여 시스템 상태 백업을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e9828-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="e9828-213">Hello 백업 예약</span><span class="sxs-lookup"><span data-stu-id="e9828-213">Schedule hello backup</span></span>
* <span data-ttu-id="e9828-214">처음으로 파일 및 hello에 대 한 폴더를 백업</span><span class="sxs-lookup"><span data-stu-id="e9828-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="e9828-215">toocomplete hello 초기 백업을 사용 하 여 hello Microsoft Azure 복구 서비스 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="e9828-216">hello Azure 백업 에이전트를 사용 하 여 tooenable 시스템 상태 백업</span><span class="sxs-lookup"><span data-stu-id="e9828-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="e9828-217">PowerShell 세션에서 다음 명령 toostop hello Azure 백업 엔진 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="e9828-218">Hello Windows 레지스트리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="e9828-219">DWord 값을 지정 하는 hello 다음 hello로 레지스트리 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="e9828-220">레지스트리 경로</span><span class="sxs-lookup"><span data-stu-id="e9828-220">Registry path</span></span> | <span data-ttu-id="e9828-221">레지스트리 키</span><span class="sxs-lookup"><span data-stu-id="e9828-221">Registry key</span></span> | <span data-ttu-id="e9828-222">DWord 값</span><span class="sxs-lookup"><span data-stu-id="e9828-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="e9828-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="e9828-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="e9828-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="e9828-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="e9828-225">2</span><span class="sxs-lookup"><span data-stu-id="e9828-225">2</span></span> |

4. <span data-ttu-id="e9828-226">Hello 다음 관리자 권한 명령 프롬프트에서 명령을 실행 하 여 hello 백업 엔진을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="e9828-227">tooschedule hello에 대 한 백업 작업</span><span class="sxs-lookup"><span data-stu-id="e9828-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="e9828-228">Hello Microsoft Azure 복구 서비스 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="e9828-229">**Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure 복구 서비스 에이전트를 시작 합니다.](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="e9828-231">Hello 복구 서비스 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="e9828-233">Hello에 시작 hello 백업 예약 마법사의 페이지를 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="e9828-234">Hello 항목 선택 tooBackup 페이지에서 클릭 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="e9828-235">**시스템 상태**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="e9828-236">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-236">Click **Next**.</span></span>

7. <span data-ttu-id="e9828-237">hello 시스템 상태 백업 및 보존 일정 자동으로 설정 되어 tooback 매주 일요일을 현지 시간으로 오후 9시에 hello 보존 기간을 설정 및 too60 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e9828-238">시스템 상태 백업 및 보존 정책이 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="e9828-239">파일 및 폴더 또한 toohello Windows 서버 시스템 상태를 백업할 경우 hello 마법사에서 파일 백업에 대 한 유일한 hello 백업 및 보존 정책을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="e9828-240">Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="e9828-241">Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="e9828-242">처음으로 hello에 대 한 Windows 서버 시스템 상태를 tooback</span><span class="sxs-lookup"><span data-stu-id="e9828-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="e9828-243">다시 부팅해야 하는 Windows Server에 보류 중인 업데이트가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="e9828-244">Hello 복구 서비스 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server 지금 백업](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="e9828-246">Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="e9828-247">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="e9828-248">클릭 **닫기** tooclose hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="e9828-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="e9828-249">Hello 백업 프로세스를 완료 전에 hello 마법사를 닫으면 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="e9828-250">백업할 파일 및 폴더를 서버의 또한 toohello Windows 서버 시스템 상태, hello 지금 백업 마법사는 백업 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="e9828-251">tooperform 없는 임시 시스템 상태를 백업, 다음 PowerShell 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="e9828-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="e9828-252">Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![IR 완료](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="e9828-254">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="e9828-254">Frequently asked questions</span></span>

<span data-ttu-id="e9828-255">hello 다음 질문과 대답을 제공 보충 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="e9828-256">Hello 준비 볼륨 란?</span><span class="sxs-lookup"><span data-stu-id="e9828-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="e9828-257">hello 준비 볼륨 hello 중간 위치가 hello 고유 하 게 사용할 수 있는 Windows Server 백업 hello 시스템 상태 백업을 준비 하는 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="e9828-258">Azure 백업 에이전트 다음 압축 및이 중간 백업을 암호화 하 고 복구 서비스 자격 증명 모음 구성 보안 HTTPS 프로토콜 toohello 통해 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="e9828-259">**비-Windows-OS 볼륨에서 hello 준비 볼륨을 설정 하는 것이 좋습니다. 시스템 상태 백업에 문제가 발견 될 경우 hello 첫 번째 문제 해결 단계는 준비 볼륨의 hello 위치를 확인 하는 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="e9828-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="e9828-260">Hello hello Azure 백업 에이전트에서 지정 된 준비 볼륨 경로 변경 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="e9828-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="e9828-261">기본적으로 hello 준비 볼륨 hello 캐시 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="e9828-262">toochange이이 위치를 사용 하 여 hello 다음 명령을 관리자 권한 명령 프롬프트) (에:</span><span class="sxs-lookup"><span data-stu-id="e9828-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="e9828-263">Hello 다음 hello 경로 toohello 새 볼륨 준비 폴더와 레지스트리 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="e9828-264">레지스트리 경로</span><span class="sxs-lookup"><span data-stu-id="e9828-264">Registry path</span></span>|<span data-ttu-id="e9828-265">레지스트리 키</span><span class="sxs-lookup"><span data-stu-id="e9828-265">Registry key</span></span>|<span data-ttu-id="e9828-266">값</span><span class="sxs-lookup"><span data-stu-id="e9828-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="e9828-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="e9828-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="e9828-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="e9828-268">SSBStagingPath</span></span> | <span data-ttu-id="e9828-269">새 스테이징 볼륨 위치</span><span class="sxs-lookup"><span data-stu-id="e9828-269">new staging volume location</span></span> |

<span data-ttu-id="e9828-270">hello 준비 경로 대/소문자 구분 및 hello 정확히 동일한 대/소문자 hello 서버에 존재 하는 기능으로 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="e9828-271">Hello 준비 볼륨 경로 변경한 후에 hello 백업 엔진 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="e9828-272">hello 변경 된 경로, 열기 hello Microsoft Azure 복구 서비스 에이전트 및 시스템 상태의 임시 백업 트리거를 toopick 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="e9828-273">기본 보존 설정 too60 일 hello 시스템 상태 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e9828-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="e9828-274">시스템 상태 백업의 연수 hello hello Windows Server Active Directory 역할에 대 한 "삭제 표시 수명" hello 설정으로 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="e9828-275">hello hello 삭제 표시 수명 항목에 대 한 기본값은 60 일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="e9828-276">Hello 디렉터리 서비스 (NTDS) 구성 개체에서이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="e9828-277">Hello 기본 백업 및 시스템 상태에 대 한 보존 정책을 변경 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="e9828-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="e9828-278">toochange hello 기본 백업 및 보존 정책에 대 한 시스템 상태:</span><span class="sxs-lookup"><span data-stu-id="e9828-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="e9828-279">Hello 백업 엔진을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-279">Stop hello Backup engine.</span></span> <span data-ttu-id="e9828-280">Hello 상승된 된 명령 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="e9828-281">추가 하거나 hello 다음 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider에서 레지스트리 키 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="e9828-282">레지스트리 이름</span><span class="sxs-lookup"><span data-stu-id="e9828-282">Registry Name</span></span>|<span data-ttu-id="e9828-283">설명</span><span class="sxs-lookup"><span data-stu-id="e9828-283">Description</span></span>|<span data-ttu-id="e9828-284">값</span><span class="sxs-lookup"><span data-stu-id="e9828-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="e9828-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="e9828-285">SSBScheduleTime</span></span>|<span data-ttu-id="e9828-286">Tooconfigure hello 백업 시간을 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="e9828-287">기본값은 현지 시간으로 오후 9시입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-287">Default is 9PM local time.</span></span>|<span data-ttu-id="e9828-288">DWord: HHMM 형식(10진수)으로 예를 들어 2130은 현지 시간으로 오후 9시 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="e9828-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="e9828-289">SSBScheduleDays</span></span>|<span data-ttu-id="e9828-290">시스템 상태 백업의 hello에 수행 해야 하는 경우 사용 되는 tooconfigure hello 일 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="e9828-291">개별 숫자 hello 주의 일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="e9828-292">0은 일요일, 1은 월요일 등입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="e9828-293">백업의 기본 요일은 일요일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="e9828-294">Hello 주 toorun 백업 (10 진수) 예를 들어 월요일, 화요일, 수요일 및 일요일에 백업 일정을 1230 DWord: 요일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="e9828-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="e9828-295">SSBRetentionDays</span></span>|<span data-ttu-id="e9828-296">사용 되는 tooconfigure hello 일 tooretain 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="e9828-297">기본값은 60입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-297">Default value is 60.</span></span> <span data-ttu-id="e9828-298">허용되는 최대값은 180입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="e9828-299">DWord: 일 tooretain 백업 (10 진수)입니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="e9828-300">다음 명령 toorestart hello 백업 엔진 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="e9828-301">Hello Microsoft 복구 서비스 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="e9828-302">클릭 **백업 예약** 클릭 하 고 **다음** 반영 된 hello 변경 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="e9828-303">클릭 **마침** tooapply hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="e9828-304">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="e9828-304">Questions?</span></span>
<span data-ttu-id="e9828-305">기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9828-306">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9828-306">Next steps</span></span>
* <span data-ttu-id="e9828-307">[Windows 컴퓨터 백업](backup-configure-vault.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e9828-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="e9828-308">파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="e9828-309">Toorestore 백업 해야 할 경우 사용 하 여이 문서 너무[tooa Windows 컴퓨터 파일을 복원](backup-azure-restore-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9828-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
