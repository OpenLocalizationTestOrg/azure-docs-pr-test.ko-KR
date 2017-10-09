---
title: "파일 및 폴더를 Azure 백업 에이전트 tooback aaaUse | Microsoft Docs"
description: "Windows 파일 및 폴더 tooAzure Microsoft Azure 백업 에이전트 tooback hello를 사용 합니다. 복구 서비스 자격 증명 모음 만들기, hello 백업 에이전트를 설치, hello 백업 정책을 정의 및 hello 파일 및 폴더에 hello 초기 백업을 실행 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 자격 증명 모음, Windows 서버 백업, Windows 백업"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="ae3b1-105">Windows 서버 또는 클라이언트 tooAzure hello 리소스 관리자 배포 모델을 사용 하 여 백업</span><span class="sxs-lookup"><span data-stu-id="ae3b1-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae3b1-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ae3b1-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="ae3b1-107">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="ae3b1-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="ae3b1-108">이 문서에서는 Azure 백업을 사용 하 여 Windows Server (또는 Windows 클라이언트)을 tooback 파일 및 폴더 tooAzure 리소스 관리자 배포 모델을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![백업 프로세스 단계](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="ae3b1-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ae3b1-110">Before you start</span></span>
<span data-ttu-id="ae3b1-111">서버 또는 클라이언트 tooAzure tooback, Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="ae3b1-112">계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ae3b1-113">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="ae3b1-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="ae3b1-114">복구 서비스 자격 증명 모음에는 모든 hello 백업 및 시간에 따라 만든 복구 지점을 저장 하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="ae3b1-115">hello 복구 서비스 자격 증명 모음 hello 백업 정책이 적용 toohello 보호 된 파일 및 폴더에도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="ae3b1-116">복구 서비스 자격 증명 모음을 만들 때도 hello 적절 한 저장소 중복 옵션을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="ae3b1-117">복구 서비스 자격 증명 모음 toocreate</span><span class="sxs-lookup"><span data-stu-id="ae3b1-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="ae3b1-118">그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="ae3b1-119">Hello 허브 메뉴에서 클릭 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스** 클릭 **복구 서비스 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="ae3b1-121">Hello 구독에서 복구 서비스 자격 증명 모음 인 경우 hello 자격 증명 모음 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="ae3b1-122">Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="ae3b1-124">hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="ae3b1-126">에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="ae3b1-127">hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="ae3b1-128">이름을 2~50자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="ae3b1-129">문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="ae3b1-130">Hello에 **구독** 섹션 hello 드롭 다운 메뉴 toochoose hello Azure 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="ae3b1-131">단일 구독을 사용 하는 경우 해당 구독 표시 되 고 toohello 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="ae3b1-132">어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="ae3b1-133">조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="ae3b1-134">Hello에 **리소스 그룹** 섹션:</span><span class="sxs-lookup"><span data-stu-id="ae3b1-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="ae3b1-135">선택 **새로 만들기** toocreate 새 리소스 그룹에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="ae3b1-136">또는</span><span class="sxs-lookup"><span data-stu-id="ae3b1-136">Or</span></span>
    * <span data-ttu-id="ae3b1-137">선택 **기존 항목 사용** hello 드롭 다운 메뉴 toosee hello 사용 가능한 리소스 그룹의 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="ae3b1-138">리소스 그룹에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="ae3b1-139">클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="ae3b1-140">여기에서이 선택한 hello 지리적 지역에 백업 데이터를 보내는 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="ae3b1-141">Hello 복구 서비스 자격 증명 모음 블레이드의 hello 아래쪽 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="ae3b1-142">복구 서비스 자격 증명 모음에 만든 toobe hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="ae3b1-143">Hello 포털의 상단 오른쪽 영역 hello에서에서 hello 상태 알림을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="ae3b1-144">자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="ae3b1-145">몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="ae3b1-147">자격 증명 모음 자격 증명 모음은 복구 서비스의 hello 목록에 표시 되는 경우 준비 tooset hello 저장소 중복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="ae3b1-148">저장소 중복 설정</span><span class="sxs-lookup"><span data-stu-id="ae3b1-148">Set storage redundancy</span></span>
<span data-ttu-id="ae3b1-149">처음으로 복구 서비스 자격 증명 모음을 만들 때 저장소가 복제되는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="ae3b1-150">Hello에서 **복구 서비스 자격 증명 모음** 블레이드에서 hello 새 자격 증명 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![복구 서비스 자격 증명 모음의 hello 목록에서 hello 새 자격 증명 모음을 선택 합니다.](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="ae3b1-152">Hello 자격 증명 모음을 선택 하면 hello **복구 서비스 자격 증명 모음** 블레이드 좁힐 및 hello 설정 블레이드에서 (*hello hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) 및 hello 자격 증명 모음 세부 정보 블레이드에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![새 자격 증명 모음에 대 한 hello 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="ae3b1-154">Hello 새 자격 증명 모음의 설정 블레이드에서 toohello 관리 섹션 아래로 수직 슬라이드 tooscroll hello를 사용 하 여 마우스 클릭 **백업 인프라**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="ae3b1-155">hello 백업 인프라 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="ae3b1-156">Hello 백업 인프라 블레이드에서 클릭 **백업 구성** tooopen hello **백업 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![새 자격 증명 모음에 대 한 저장소 구성을 hello 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="ae3b1-158">자격 증명 모음에 대 한 hello 적절 한 저장소 복제 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="ae3b1-160">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="ae3b1-161">기본 백업 저장소 끝점으로 Azure를 사용 하는 경우 계속 toouse **지리적 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="ae3b1-162">기본 백업 저장소 끝점으로 Azure를 사용 하지 않는 경우 선택할 **로컬 중복**, hello Azure 저장소 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="ae3b1-163">[지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="ae3b1-164">자격 증명 모음을 만든 했으므로 사용자 인프라 tooback 파일 및 폴더를 다운로드 하 고 hello Microsoft Azure 복구 서비스 에이전트를 설치, 자격 증명 모음 자격 증명 다운로드 이러한 자격 증명 tooregister hello 에이전트를 사용 하 여 준비 hello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="ae3b1-165">Hello 자격 증명 모음 구성</span><span class="sxs-lookup"><span data-stu-id="ae3b1-165">Configure hello vault</span></span>

1. <span data-ttu-id="ae3b1-166">Hello 시작 섹션에 복구 서비스 자격 증명 모음 블레이드 (hello 모음 방금 만든)에 대 한 hello, 클릭 **백업**, 그 다음에 hello **백업 시작** 블레이드를  **백업 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="ae3b1-168">hello **백업 목표** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="ae3b1-169">복구 서비스 자격 증명 모음에 hello 이전에 구성한 경우 다음 hello **백업 목표** 클릭 하면 블레이드가 열립니다 **백업** hello 복구 서비스에 블레이드를 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="ae3b1-171">Hello에서 **여기서 작업이 실행 되는?** 드롭 다운 메뉴 **온-프레미스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="ae3b1-172">Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="ae3b1-173">Hello에서 **하 신 toobackup 원하는?** 메뉴 선택 **파일 및 폴더**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![파일 및 폴더 구성](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="ae3b1-175">확인을 클릭 하면 확인 표시가 나타납니다 다음 너무**백업 목표**, 및 hello **준비 인프라** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![백업 목표 구성, 다음으로 인프라 준비](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="ae3b1-177">Hello에 **준비 인프라** 블레이드에서 클릭 **Windows Server 용 에이전트 다운로드 또는 Windows Client**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="ae3b1-179">Windows Server 필수 항목을 사용 하는, 용 Windows Server 필수 toodownload hello 에이전트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="ae3b1-180">팝업 메뉴 toorun 묻는 또는 MARSAgentInstaller.exe 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller 대화 상자](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="ae3b1-182">Hello 다운로드 팝업 메뉴에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="ae3b1-183">기본적으로 hello **MARSagentinstaller.exe** 파일이 tooyour Downloads 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="ae3b1-184">Hello 설치 관리자가 완료 되 면 toorun hello installer 또는 hello 폴더를 열 경우 묻는 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="ae3b1-186">Tooinstall hello 에이전트를 아직 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="ae3b1-187">Hello 자격 증명 모음 자격 증명을 다운로드 한 후 hello 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="ae3b1-188">Hello에 **준비 인프라** 블레이드에서 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![자격 증명 모음 자격 증명 다운로드](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="ae3b1-190">자격 증명 모음 hello tooyour 다운로드 폴더를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="ae3b1-191">Hello 자격 증명 모음 자격 증명 다운로드를 완료 한 후 tooopen 원하는 또는 hello 자격 증명을 저장 하는 경우 요청 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="ae3b1-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-192">Click **Save**.</span></span> <span data-ttu-id="ae3b1-193">실수로 누르면 **열려**, tooopen hello에 대 한 자격 증명 모음 자격 증명을 시도 하는 hello 대화 상자, 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="ae3b1-194">Hello 자격 증명 모음을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="ae3b1-195">Toohello 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-195">Proceed toohello next step.</span></span> <span data-ttu-id="ae3b1-196">hello 자격 증명 모음 자격 증명이 hello Downloads 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![자격 증명 모음 자격 증명 다운로드 완료](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="ae3b1-198">설치 하 고 hello 에이전트 등록</span><span class="sxs-lookup"><span data-stu-id="ae3b1-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="ae3b1-199">Hello Azure 포털을 통해 사용할 수 있도록 백업을 사용할 수 없는 경우, 아직</span><span class="sxs-lookup"><span data-stu-id="ae3b1-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="ae3b1-200">파일 및 폴더를 Microsoft Azure 복구 서비스 에이전트 tooback hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="ae3b1-201">Hello를 두 번 클릭 **MARSagentinstaller.exe** hello 다운로드 폴더 (또는 다른 저장된 위치).</span><span class="sxs-lookup"><span data-stu-id="ae3b1-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="ae3b1-202">hello 설치 관리자는 일련의 메시지를, 추출할 때는 설치 및 hello 복구 서비스 에이전트 등록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![Recovery Services 에이전트 설치 관리자 자격 증명을 실행](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="ae3b1-204">Hello Microsoft Azure 복구 서비스 에이전트 설치 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="ae3b1-205">toocomplete hello 마법사 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="ae3b1-206">Hello 설치 및 캐시 폴더의 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="ae3b1-207">프록시 서버 tooconnect toohello를 사용 하는 경우 프록시 서버 정보를 제공 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="ae3b1-208">인증된 프록시를 사용하는 경우에는 사용자 이름 및 암호 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="ae3b1-209">Hello 다운로드 한 자격 증명 모음 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="ae3b1-210">Hello 암호화의 암호를 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ae3b1-211">끊어지거나 hello 암호를 잊은 경우 Microsoft hello 백업 데이터를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="ae3b1-212">Hello 파일을 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-212">Save hello file in a secure location.</span></span> <span data-ttu-id="ae3b1-213">것이 필수 toorestore 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="ae3b1-214">hello 에이전트를 지금 설치 하 고 등록 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="ae3b1-215">준비 tooconfigure 하 고 백업을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="ae3b1-216">네트워크 및 연결 요구 사항</span><span class="sxs-lookup"><span data-stu-id="ae3b1-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="ae3b1-217">컴퓨터/프록시는 인터넷에 연결을 제한 한 경우 hello 컴퓨터/프록시에 방화벽 설정이 다음 Url 구성된 tooallow hello 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="ae3b1-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ae3b1-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="ae3b1-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ae3b1-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="ae3b1-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="ae3b1-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="ae3b1-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ae3b1-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="ae3b1-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="ae3b1-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="ae3b1-223">Hello 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ae3b1-223">Create hello backup policy</span></span>
<span data-ttu-id="ae3b1-224">복구 지점, 수행 및 hello 복구 지점이 보존 되는 시간의 길이 hello hello 백업 정책이 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="ae3b1-225">파일 및 폴더에 대 한 hello Microsoft Azure 백업 에이전트 toocreate hello 백업 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="ae3b1-226">toocreate 백업 일정</span><span class="sxs-lookup"><span data-stu-id="ae3b1-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="ae3b1-227">Hello Microsoft Azure 백업 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="ae3b1-228">**Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure 백업 에이전트를 시작 합니다.](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="ae3b1-230">Hello 백업 에이전트에서 **동작** 창에서 클릭 **백업 예약** toolaunch hello 백업 예약 마법사.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Windows Server 백업 예약](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="ae3b1-232">Hello에 **시작** hello 백업 예약 마법사의 페이지 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="ae3b1-233">Hello에 **항목 선택 tooBackup** 페이지 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="ae3b1-234">hello 항목 선택 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="ae3b1-235">Hello 파일 및 폴더, tooprotect 원하고 클릭 한 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="ae3b1-236">Hello에 **항목 선택 tooBackup** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="ae3b1-237">Hello에 **백업 일정 지정** 페이지에서 지정한 백업 일정 hello 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="ae3b1-238">매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="ae3b1-240">Toospecify 백업 일정을 hello 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [사용 하 여 Azure 백업 tooreplace 테이프 인프라](backup-azure-backup-cloud-as-tape.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="ae3b1-241">Hello에 **보존 정책 선택** 페이지 hello 백업 복사본에 대 한 hello 특정 보존 정책을 hello를 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="ae3b1-242">hello 보존 정책은 hello 백업이 저장 된 hello 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="ae3b1-243">모든 백업 지점에 대 한 "플랫 정책을"를 방금 지정 하는 대신 hello 백업이 발생 하는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="ae3b1-244">매일, 매주, 매월 및 매년 보존 정책을 toomeet hello 요구에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="ae3b1-245">Hello 초기 백업 유형 선택 페이지에서 hello 초기 백업 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="ae3b1-246">Hello 옵션인 **hello 네트워크를 통해 자동으로** 을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="ae3b1-247">Hello 네트워크를 통해 자동으로를 백업할 수 있습니다 또는 오프 라인으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="ae3b1-248">이 문서의 나머지 부분에서는 hello 자동으로 백업에 대 한 hello 프로세스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="ae3b1-249">오프 라인 백업을 toodo 원한다 면 hello 문서를 검토 [Azure 백업에서 오프 라인 백업 워크플로](backup-azure-backup-import-export.md) 추가 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="ae3b1-250">Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="ae3b1-251">Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="ae3b1-252">네트워크 제한 사용</span><span class="sxs-lookup"><span data-stu-id="ae3b1-252">Enable network throttling</span></span>
<span data-ttu-id="ae3b1-253">네트워크 제한 hello Microsoft Azure 백업 에이전트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="ae3b1-254">제한 기능은 데이터 전송 중에 사용되는 네트워크 대역폭의 양을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="ae3b1-255">이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="ae3b1-256">제한 tooback를 적용 하 고 복원 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ae3b1-257">네트워크 제한은 Windows Server 2008 R2 SP1, Windows Server 2008 SP2 또는 Windows 7(서비스 팩 포함)에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="ae3b1-258">hello 로컬 운영 체제에서 서비스 품질 (QoS)를 예약 하는 hello Azure 백업 네트워크 기능을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="ae3b1-259">Azure 백업에서 이러한 운영 체제를 보호 하려면 경우에 이러한 플랫폼에서 사용할 수 있는 QoS의 hello 버전 Azure 백업 네트워크 제한이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="ae3b1-260">네트워크 제한은 다른 모든 [지원되는 운영 체제](backup-azure-backup-faq.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="ae3b1-261">**tooenable 네트워크 제한**</span><span class="sxs-lookup"><span data-stu-id="ae3b1-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="ae3b1-262">Hello Microsoft Azure 백업 에이전트에서 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![속성 변경](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="ae3b1-264">Hello에 **제한** 탭, 선택 hello **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![네트워크 제한](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="ae3b1-266">제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="ae3b1-267">hello 대역폭 값 (Kbps) 초당 킬로 비트부터 시작 하 고 too1, 023 m b / 초 (MBps) 위로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="ae3b1-268">또한 hello 시작을 지정 하 고 완료 수 **근무 시간**, hello 요일을 작업일 수로 간주 되며 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="ae3b1-269">지정된 작업 시간 이외의 시간은 비 작업 시간으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="ae3b1-270">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="ae3b1-271">파일 및 처음으로 hello에 대 한 폴더를 tooback</span><span class="sxs-lookup"><span data-stu-id="ae3b1-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="ae3b1-272">Hello 백업 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![지금 Windows Server 백업](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="ae3b1-274">Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="ae3b1-275">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="ae3b1-276">클릭 **닫기** tooclose hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="ae3b1-277">이렇게 하면 hello 백업 프로세스를 완료 하기 전에 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="ae3b1-278">Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR 완료](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="ae3b1-280">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="ae3b1-280">Questions?</span></span>
<span data-ttu-id="ae3b1-281">기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae3b1-282">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae3b1-282">Next steps</span></span>
<span data-ttu-id="ae3b1-283">VM 또는 다른 워크로드를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="ae3b1-284">파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="ae3b1-285">Toorestore 백업 해야 할 경우 사용 하 여이 문서 너무[tooa Windows 컴퓨터 파일을 복원](backup-azure-restore-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae3b1-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
