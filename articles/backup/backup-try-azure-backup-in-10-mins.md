---
title: "Windows 파일 및 폴더 tooAzure (리소스 관리자)를 aaaBack | Microsoft Docs"
description: "리소스 관리자 배포에서 Windows 파일 및 폴더 tooAzure tooback에 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "어떻게 toobackup; 어떻게 tooback; 백업 파일 및 폴더"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="3039f-104">먼저 보기: Resource Manager 배포에서 파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="3039f-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="3039f-105">이 문서에서는 설명 어떻게 리소스 관리자 배포를 사용 하 여 Windows Server (또는 Windows 컴퓨터)을 tooback 파일 및 폴더 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="3039f-106">자습서 의도 한 toowalk는 hello 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="3039f-107">원하는 tooget Azure 백업을 사용 하 여 시작 하는 경우 hello 올바른 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="3039f-108">Azure 백업에 대 한 자세한 tooknow 하려는 경우이 내용을 읽고 [개요](backup-introduction-to-azure-backup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="3039f-109">Azure 구독이 없는 경우 모든 Azure 서비스에 액세스할 수 있는 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3039f-110">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="3039f-110">Create a recovery services vault</span></span>
<span data-ttu-id="3039f-111">파일 및 폴더를 tooback, toocreate hello 지역 toostore hello 데이터를 원하는 위치에 복구 서비스 자격 증명 모음 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="3039f-112">Toodetermine 원하는 저장소를 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="3039f-113">복구 서비스 자격 증명 모음 toocreate</span><span class="sxs-lookup"><span data-stu-id="3039f-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="3039f-114">그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="3039f-115">Hello 허브 메뉴에서 클릭 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스** 클릭 **복구 서비스 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="3039f-117">Hello 구독에서 복구 서비스 자격 증명 모음 인 경우 hello 자격 증명 모음 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="3039f-118">Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="3039f-120">hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="3039f-122">에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="3039f-123">hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="3039f-124">이름을 2~50자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="3039f-125">문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="3039f-126">Hello에 **구독** 섹션 hello 드롭 다운 메뉴 toochoose hello Azure 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="3039f-127">단일 구독을 사용 하는 경우 해당 구독 표시 되 고 toohello 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="3039f-128">어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="3039f-129">조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="3039f-130">Hello에 **리소스 그룹** 섹션:</span><span class="sxs-lookup"><span data-stu-id="3039f-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="3039f-131">선택 **새로 만들기** toocreate 새 리소스 그룹에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="3039f-132">또는</span><span class="sxs-lookup"><span data-stu-id="3039f-132">Or</span></span>
    * <span data-ttu-id="3039f-133">선택 **기존 항목 사용** hello 드롭 다운 메뉴 toosee hello 사용 가능한 리소스 그룹의 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="3039f-134">리소스 그룹에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="3039f-135">클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="3039f-136">여기에서이 선택한 hello 지리적 지역에 백업 데이터를 보내는 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="3039f-137">Hello 복구 서비스 자격 증명 모음 블레이드의 hello 아래쪽 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="3039f-138">복구 서비스 자격 증명 모음에 만든 toobe hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="3039f-139">Hello 포털의 상단 오른쪽 영역 hello에서에서 hello 상태 알림을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="3039f-140">자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="3039f-141">몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="3039f-143">자격 증명 모음 자격 증명 모음은 복구 서비스의 hello 목록에 표시 되는 경우 준비 tooset hello 저장소 중복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="3039f-144">Hello 자격 증명 모음에 대 한 저장소 중복성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="3039f-145">복구 서비스 자격 증명 모음을 만들 때 저장소 중복 구성 된 hello 방식으로 원하는 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="3039f-146">Hello에서 **복구 서비스 자격 증명 모음** 블레이드에서 hello 새 자격 증명 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![복구 서비스 자격 증명 모음의 hello 목록에서 hello 새 자격 증명 모음을 선택 합니다.](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="3039f-148">Hello 자격 증명 모음을 선택 하면 hello **복구 서비스 자격 증명 모음** 블레이드 좁힐 및 hello 설정 블레이드에서 (*hello hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) 및 hello 자격 증명 모음 세부 정보 블레이드에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![새 자격 증명 모음에 대 한 hello 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="3039f-150">Hello 새 자격 증명 모음의 설정 블레이드에서 toohello 관리 섹션 아래로 수직 슬라이드 tooscroll hello를 사용 하 여 마우스 클릭 **백업 인프라**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="3039f-151">hello 백업 인프라 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="3039f-152">Hello 백업 인프라 블레이드에서 클릭 **백업 구성** tooopen hello **백업 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![새 자격 증명 모음에 대 한 저장소 구성을 hello 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="3039f-154">자격 증명 모음에 대 한 hello 적절 한 저장소 복제 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="3039f-156">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="3039f-157">기본 백업 저장소 끝점으로 Azure를 사용 하는 경우 계속 toouse **지리적 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="3039f-158">기본 백업 저장소 끝점으로 Azure를 사용 하지 않는 경우 선택할 **로컬 중복**, hello Azure 저장소 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="3039f-159">[지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3039f-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="3039f-160">이제 자격 증명 모음을 만들었으므로 파일과 폴더를 백업하도록 자격 증명 모음을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="3039f-161">Hello 자격 증명 모음 구성</span><span class="sxs-lookup"><span data-stu-id="3039f-161">Configure hello vault</span></span>
1. <span data-ttu-id="3039f-162">Hello 시작 섹션에 복구 서비스 자격 증명 모음 블레이드 (hello 모음 방금 만든)에 대 한 hello, 클릭 **백업**, 그 다음에 hello **백업 시작** 블레이드를  **백업 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="3039f-164">hello **백업 목표** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-164">hello **Backup Goal** blade opens.</span></span>

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="3039f-166">Hello에서 **여기서 작업이 실행 되는?** 드롭 다운 메뉴 **온-프레미스**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="3039f-167">Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="3039f-168">Hello에서 **하 신 toobackup 원하는?** 메뉴 선택 **파일 및 폴더**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![파일 및 폴더 구성](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="3039f-170">확인을 클릭 하면 확인 표시가 나타납니다 다음 너무**백업 목표**, 및 hello **준비 인프라** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![백업 목표 구성, 다음으로 인프라 준비](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="3039f-172">Hello에 **준비 인프라** 블레이드에서 클릭 **Windows Server 용 에이전트 다운로드 또는 Windows Client**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="3039f-174">Windows Server 필수 항목을 사용 하는, 용 Windows Server 필수 toodownload hello 에이전트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="3039f-175">팝업 메뉴 toorun 묻는 또는 MARSAgentInstaller.exe 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller 대화 상자](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="3039f-177">Hello 다운로드 팝업 메뉴에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="3039f-178">기본적으로 hello **MARSagentinstaller.exe** 파일이 tooyour Downloads 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="3039f-179">Hello 설치 관리자가 완료 되 면 toorun hello installer 또는 hello 폴더를 열 경우 묻는 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="3039f-181">Tooinstall hello 에이전트를 아직 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="3039f-182">Hello 자격 증명 모음 자격 증명을 다운로드 한 후 hello 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="3039f-183">Hello에 **준비 인프라** 블레이드에서 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![자격 증명 모음 자격 증명 다운로드](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="3039f-185">자격 증명 모음 hello tooyour 다운로드 폴더를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="3039f-186">Hello 자격 증명 모음 자격 증명 다운로드를 완료 한 후 tooopen 원하는 또는 hello 자격 증명을 저장 하는 경우 요청 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="3039f-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-187">Click **Save**.</span></span> <span data-ttu-id="3039f-188">실수로 누르면 **열려**, tooopen hello에 대 한 자격 증명 모음 자격 증명을 시도 하는 hello 대화 상자, 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="3039f-189">Hello 자격 증명 모음을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="3039f-190">Toohello 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-190">Proceed toohello next step.</span></span> <span data-ttu-id="3039f-191">hello 자격 증명 모음 자격 증명이 hello Downloads 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![자격 증명 모음 자격 증명 다운로드 완료](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="3039f-193">설치 하 고 hello 에이전트 등록</span><span class="sxs-lookup"><span data-stu-id="3039f-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="3039f-194">Hello Azure 포털을 통해 사용할 수 있도록 백업을 사용할 수 없는 경우, 아직</span><span class="sxs-lookup"><span data-stu-id="3039f-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="3039f-195">파일 및 폴더를 Microsoft Azure 복구 서비스 에이전트 tooback hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="3039f-196">Hello를 두 번 클릭 **MARSagentinstaller.exe** hello 다운로드 폴더 (또는 다른 저장된 위치).</span><span class="sxs-lookup"><span data-stu-id="3039f-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="3039f-197">hello 설치 관리자는 일련의 메시지를, 추출할 때는 설치 및 hello 복구 서비스 에이전트 등록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Recovery Services 에이전트 설치 관리자 자격 증명을 실행](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="3039f-199">Hello Microsoft Azure 복구 서비스 에이전트 설치 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="3039f-200">toocomplete hello 마법사 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="3039f-201">Hello 설치 및 캐시 폴더의 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="3039f-202">프록시 서버 tooconnect toohello를 사용 하는 경우 프록시 서버 정보를 제공 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="3039f-203">인증된 프록시를 사용하는 경우에는 사용자 이름 및 암호 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="3039f-204">Hello 다운로드 한 자격 증명 모음 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="3039f-205">Hello 암호화의 암호를 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3039f-206">끊어지거나 hello 암호를 잊은 경우 Microsoft hello 백업 데이터를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="3039f-207">Hello 파일을 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-207">Save hello file in a secure location.</span></span> <span data-ttu-id="3039f-208">것이 필수 toorestore 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="3039f-209">hello 에이전트를 지금 설치 하 고 등록 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="3039f-210">준비 tooconfigure 하 고 백업을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="3039f-211">네트워크 및 연결 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3039f-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="3039f-212">컴퓨터/프록시는 인터넷에 연결을 제한 한 경우 hello mcahine/프록시에 방화벽 설정이 다음 Url 구성된 tooallow hello 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="3039f-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="3039f-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="3039f-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3039f-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="3039f-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="3039f-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="3039f-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3039f-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="3039f-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="3039f-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="3039f-218">파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="3039f-218">Back up your files and folders</span></span>
<span data-ttu-id="3039f-219">초기 백업을 hello 두 가지 주요 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="3039f-220">Hello 백업 예약</span><span class="sxs-lookup"><span data-stu-id="3039f-220">Schedule hello backup</span></span>
* <span data-ttu-id="3039f-221">처음으로 파일 및 hello에 대 한 폴더를 백업</span><span class="sxs-lookup"><span data-stu-id="3039f-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="3039f-222">toocomplete hello 초기 백업을 사용 하 여 hello Microsoft Azure 복구 서비스 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="3039f-223">tooschedule hello에 대 한 백업 작업</span><span class="sxs-lookup"><span data-stu-id="3039f-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="3039f-224">Hello Microsoft Azure 복구 서비스 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="3039f-225">**Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure 복구 서비스 에이전트를 시작 합니다.](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="3039f-227">Hello 복구 서비스 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="3039f-229">Hello에 시작 hello 백업 예약 마법사의 페이지를 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="3039f-230">Hello 항목 선택 tooBackup 페이지에서 클릭 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="3039f-231">Hello 파일 및 폴더, tooback 원하는 클릭 한 다음 선택 **알겠습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="3039f-232">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-232">Click **Next**.</span></span>
7. <span data-ttu-id="3039f-233">Hello에 **백업 일정 지정** 페이지에서 지정 하는 hello **백업 일정** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="3039f-234">매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 백업 항목](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="3039f-236">Toospecify 백업 일정을 hello 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [사용 하 여 Azure 백업 tooreplace 테이프 인프라](backup-azure-backup-cloud-as-tape.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="3039f-237">Hello에 **보존 정책 선택** 페이지, 선택 hello **보존 정책** hello 백업 복사본에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="3039f-238">hello 보존 정책은 hello 백업 데이터 저장 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="3039f-239">모든 백업 지점에 대 한 "플랫 정책을"를 지정 하는 대신 hello 백업이 발생 하는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="3039f-240">매일, 매주, 매월 및 매년 보존 정책을 toomeet hello 요구에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="3039f-241">Hello 초기 백업 유형 선택 페이지에서 hello 초기 백업 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="3039f-242">Hello 옵션인 **hello 네트워크를 통해 자동으로** 을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="3039f-243">Hello 네트워크를 통해 자동으로를 백업할 수 있습니다 또는 오프 라인으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="3039f-244">이 문서의 나머지 부분에서는 hello 자동으로 백업에 대 한 hello 프로세스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="3039f-245">오프 라인 백업을 toodo 원한다 면 hello 문서를 검토 [Azure 백업에서 오프 라인 백업 워크플로](backup-azure-backup-import-export.md) 추가 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="3039f-246">Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="3039f-247">Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="3039f-248">파일 및 처음으로 hello에 대 한 폴더를 tooback</span><span class="sxs-lookup"><span data-stu-id="3039f-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="3039f-249">Hello 복구 서비스 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server 지금 백업](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="3039f-251">Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="3039f-252">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="3039f-253">클릭 **닫기** tooclose hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="3039f-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="3039f-254">Hello 백업 프로세스를 완료 전에 hello 마법사를 닫으면 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="3039f-255">Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR 완료](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="3039f-257">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="3039f-257">Questions?</span></span>
<span data-ttu-id="3039f-258">기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3039f-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3039f-259">Next steps</span></span>
* <span data-ttu-id="3039f-260">[Windows 컴퓨터 백업](backup-configure-vault.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3039f-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="3039f-261">파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="3039f-262">Toorestore 백업 해야 할 경우 사용 하 여이 문서 너무[tooa Windows 컴퓨터 파일을 복원](backup-azure-restore-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3039f-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
