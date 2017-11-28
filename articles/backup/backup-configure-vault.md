---
title: "Azure Backup 에이전트를 사용하여 파일 및 폴더 백업 | Microsoft Docs"
description: "Microsoft Azure Backup 에이전트를 사용하여 Windows 파일과 폴더를 Azure에 백업합니다. Recovery Services 자격 증명 모음을 만들고, 백업 에이전트를 설치하고, 백업 정책을 정의하고, 파일 및 폴더에 초기 백업을 실행합니다."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="20c69-105">Resource Manager 배포 모델을 사용하여 Azure로 Windows Server 또는 클라이언트 백업</span><span class="sxs-lookup"><span data-stu-id="20c69-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20c69-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="20c69-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="20c69-107">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="20c69-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="20c69-108">이 문서는 Resource Manager 배포 모델을 사용하여 Azure 백업이 포함된 Azure에 Windows 서버(또는 Windows 클라이언트) 파일 및 폴더를 백업하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![백업 프로세스 단계](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="20c69-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="20c69-110">Before you start</span></span>
<span data-ttu-id="20c69-111">서버 또는 클라이언트를 Azure에 백업하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="20c69-112">계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="20c69-113">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="20c69-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="20c69-114">복구 서비스 자격 증명 모음은 시간이 경과되면서 만든 모든 백업과 복구 지점을 저장하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="20c69-115">복구 서비스 자격 증명 모음에는 보호된 파일과 폴더에 적용된 백업 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="20c69-116">복구 서비스 자격 증명 모음을 만들 때는 적절한 저장소 중복 옵션도 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="20c69-117">복구 서비스 자격 증명 모음을 만들려면</span><span class="sxs-lookup"><span data-stu-id="20c69-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="20c69-118">[Azure 포털](https://portal.azure.com/) 에 아직 로그인하지 않은 경우 Azure 구독을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="20c69-119">[허브] 메뉴에서 **추가 서비스**를 클릭하고 리소스 목록에서 **Recovery Services**를 입력한 다음 **Recovery Services 자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="20c69-121">구독에 복구 서비스 자격 증명 모음이 있는 경우 자격 증명 모음이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="20c69-122">**Recovery Services 자격 증명 모음** 메뉴에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="20c69-124">복구 서비스 자격 증명 모음 블레이드가 열리고 **이름**, **구독**, **리소스 그룹** 및 **위치**를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="20c69-126">**이름**에 자격 증명 모음을 식별하기 위한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="20c69-127">이름은 Azure 구독에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="20c69-128">이름을 2~50자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="20c69-129">문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="20c69-130">**구독** 섹션에서 드롭다운 메뉴를 사용하여 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="20c69-131">구독을 하나만 사용하면 해당 구독이 나타나고 다음 단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="20c69-132">사용할 구독을 잘 모르는 경우 기본(또는 제안된) 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="20c69-133">조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="20c69-134">**리소스 그룹** 섹션에서:</span><span class="sxs-lookup"><span data-stu-id="20c69-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="20c69-135">리소스 그룹을 새로 만들려면 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="20c69-136">또는</span><span class="sxs-lookup"><span data-stu-id="20c69-136">Or</span></span>
    * <span data-ttu-id="20c69-137">**기존 그룹 사용**을 선택하고 드롭다운 메뉴를 클릭하여 사용 가능한 리소스 그룹 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="20c69-138">리소스 그룹에 대한 전체 정보는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20c69-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="20c69-139">**위치** 를 클릭하여 자격 증명 모음에 대한 지리적 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="20c69-140">선택에 따라 백업 데이터가 전송되는 지역이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="20c69-141">Recovery Services 자격 증명 모음 블레이드의 하단에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="20c69-142">Recovery Services 자격 증명 모음을 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="20c69-143">포털의 오른쪽 위 영역에 있는 상태 알림을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="20c69-144">자격 증명 모음이 생성되면 복구 서비스 자격 증명 모음 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="20c69-145">몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="20c69-147">Recovery Services 자격 증명 모음 목록에 사용자의 자격 증명 모음이 보이면 저장소 중복을 설정할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="20c69-148">저장소 중복 설정</span><span class="sxs-lookup"><span data-stu-id="20c69-148">Set storage redundancy</span></span>
<span data-ttu-id="20c69-149">처음으로 복구 서비스 자격 증명 모음을 만들 때 저장소가 복제되는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="20c69-150">**Recovery Services 자격 증명 모음** 블레이드에서 새 자격 증명 모음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Recovery Services 자격 증명 모음 목록에서 새 자격 증명 모음 선택](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="20c69-152">자격 증명 모음을 선택하면 **Recovery Services 자격 증명 모음** 블레이드가 좁아지고 설정 블레이드(*맨 위에 자격 증명 모음 이름이 있음*) 및 자격 증명 모음 세부 정보 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![새 자격 증명 모음의 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="20c69-154">새 자격 증명 모음의 설정 블레이드에서 세로 슬라이드를 사용하여 관리 섹션 쪽으로 아래로 스크롤하여 **백업 인프라**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="20c69-155">[백업 인프라] 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="20c69-156">[백업 인프라] 블레이드에서 **백업 구성**을 클릭하여 **백업 구성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![새 자격 증명 모음의 저장소 구성 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="20c69-158">자격 증명 모음에 대해 적절한 저장소 복제 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="20c69-160">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="20c69-161">Azure를 기본 백업 저장소 끝점으로 사용하는 경우 **지역 중복**을 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="20c69-162">Azure를 기본 백업 저장소 끝점으로 사용하지 않는 경우 Azure Storage 비용이 감소되는 **로컬 중복**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="20c69-163">[지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20c69-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="20c69-164">자격 증명 모음을 만들었으니, Microsoft Azure Recovery Services 에이전트를 다운로드하여 설치하고, 보관 자격 증명을 다운로드한 다음 그 자격 증명을 사용하여 에이전트를 자격 증명 모음에 등록하여, 파일과 폴더를 백업할 인프라를 준비하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="20c69-165">자격 증명 모음 구성</span><span class="sxs-lookup"><span data-stu-id="20c69-165">Configure the vault</span></span>

1. <span data-ttu-id="20c69-166">Recovery Services 자격 증명 모음(방금 만든 자격 증명 모음) 블레이드의 [시작] 섹션에서 **백업**을 클릭한 다음 **백업 시작** 블레이드에서 **백업 목표**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="20c69-168">**백업 목표** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="20c69-169">Recovery Services 자격 증명 모음을 이전에 구성한 경우 Recovery Services 자격 증명 모음에서 **백업**을 클릭하면 **백업 목표** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="20c69-171">**작업이 실행되는 위치** 드롭다운 메뉴에서 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="20c69-172">Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="20c69-173">**백업할 항목** 메뉴에서 **파일 및 폴더**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![파일 및 폴더 구성](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="20c69-175">[확인]을 클릭하면 **백업 목표** 옆에 확인 표시가 나타나고 **인프라 준비** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![백업 목표 구성, 다음으로 인프라 준비](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="20c69-177">**인프라 준비** 블레이드에서 **Windows Server 또는 Windows Client용 에이전트 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="20c69-179">Windows Server Essential을 사용하는 경우 Windows Server Essential 용 에이전트를 다운로드하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="20c69-180">MARSAgentInstaller.exe를 실행하거나 저장하라는 팝업 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller 대화 상자](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="20c69-182">다운로드 팝업 메뉴에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="20c69-183">기본적으로 **MARSagentinstaller.exe** 파일이 다운로드 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="20c69-184">설치 관리자가 완료되면 설치 관리자를 실행할지 아니면 폴더를 열지 묻는 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![인프라 준비](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="20c69-186">에이전트를 아직 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="20c69-187">에이전트는 자격 증명 모음을 다운로드한 후에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="20c69-188">**인프라 준비** 블레이드에서 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![자격 증명 모음 자격 증명 다운로드](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="20c69-190">자격 증명 모음 자격 증명이 [다운로드] 폴더로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="20c69-191">자격 증명 모음 다운로드가 완료되면 자격 증명을 열거나 저장할지 묻는 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="20c69-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-192">Click **Save**.</span></span> <span data-ttu-id="20c69-193">실수로 **열기**를 클릭하면 자격 증명 모음 자격 증명을 열려고 하는 대화 상자가 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="20c69-194">자격 증명 모음 자격 증명을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="20c69-195">다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-195">Proceed to the next step.</span></span> <span data-ttu-id="20c69-196">자격 증명 모음은 다운로드 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-196">The vault credentials are in the Downloads folder.</span></span>   

  ![자격 증명 모음 자격 증명 다운로드 완료](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="20c69-198">에이전트 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="20c69-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="20c69-199">Azure Portal을 통한 백업 활성화는 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="20c69-200">Microsoft Azure Recovery Services 에이전트를 사용하여 파일과 폴더를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="20c69-201">다운로드 폴더(또는 기타 저장 위치)에서 **MARSagentinstaller.exe**를 찾아서 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="20c69-202">설치 관리자는 Recovery Services 에이전트를 추출, 설치 및 등록할 때 일련의 메시지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![Recovery Services 에이전트 설치 관리자 자격 증명을 실행](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="20c69-204">Microsoft Azure 복구 서비스 에이전트 설치 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="20c69-205">마법사를 완료하려면 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="20c69-206">설치 및 캐시 폴더의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="20c69-207">프록시 서버를 사용하여 인터넷에 연결하는 경우에는 프록시 서버 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="20c69-208">인증된 프록시를 사용하는 경우에는 사용자 이름 및 암호 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="20c69-209">다운로드한 자격 증명 모음 제공</span><span class="sxs-lookup"><span data-stu-id="20c69-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="20c69-210">암호화 암호를 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="20c69-211">암호를 분실하거나 잊어버린 경우 Microsoft에서 백업 데이터의 복구를 도와드릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="20c69-212">파일을 안전한 위치에 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="20c69-212">Save the file in a secure location.</span></span> <span data-ttu-id="20c69-213">백업을 복원할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="20c69-214">이제 에이전트가 설치되었고 컴퓨터가 자격 증명 모음에 등록되었습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="20c69-215">백업을 구성하고 일정을 예약할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="20c69-216">네트워크 및 연결 요구 사항</span><span class="sxs-lookup"><span data-stu-id="20c69-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="20c69-217">컴퓨터/프록시의 인터넷 액세스가 제한된 경우 컴퓨터/프록시의 방화벽 설정이 다음 URL을 허용하도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="20c69-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="20c69-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="20c69-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="20c69-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="20c69-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="20c69-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="20c69-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="20c69-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="20c69-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="20c69-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="20c69-223">백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="20c69-223">Create the backup policy</span></span>
<span data-ttu-id="20c69-224">백업 정책은 복구 지점이 만들어지는 일정이고 복구 지점이 유지되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="20c69-225">Microsoft Azure Backup 에이전트를 사용하여 파일과 폴더에 대한 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="20c69-226">백업 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="20c69-226">To create a backup schedule</span></span>
1. <span data-ttu-id="20c69-227">Microsoft Azure 백업 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="20c69-228">**Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Azure 백업 에이전트 시작](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="20c69-230">Backup 에이전트의 **작업** 창에서 **백업 일정**을 클릭하여 백업 예약 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Windows Server 백업 예약](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="20c69-232">백업 예약 마법사의 **시작** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="20c69-233">**백업할 항목 선택** 페이지에서 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="20c69-234">항목 선택 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="20c69-235">보호하려는 파일 및 폴더를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="20c69-236">**백업할 항목 선택** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="20c69-237">**백업 일정 지정** 페이지에서 백업 일정을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="20c69-238">매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="20c69-240">백업 일정을 지정하는 방법은 [Azure 백업을 사용하여 테이프 인프라 대체](backup-azure-backup-cloud-as-tape.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20c69-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="20c69-241">**보존 정책 선택** 페이지에서 백업 복사본에 대한 특정 보존 정책을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="20c69-242">보존 정책은 백업이 저장되는 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="20c69-243">모든 백업 지점에 대한 "일반 정책"을 지정하는 대신 백업이 발생하는 시기에 따라 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="20c69-244">매일, 매주, 매월 및 매년 보존 정책을 요구 사항에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="20c69-245">초기 백업 유형 선택 페이지에서 초기 백업 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="20c69-246">**네트워크를 통해 자동으로** 옵션이 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="20c69-247">네트워크를 통해 자동으로 백업하거나 오프라인으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="20c69-248">이 문서의 나머지 부분은 자동 백업 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="20c69-249">오프라인 백업을 선호하는 경우 [Azure 백업의 오프라인 백업 워크플로](backup-azure-backup-import-export.md) 문서에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20c69-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="20c69-250">확인 페이지에서 정보를 검토한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="20c69-251">마법사가 백업 일정 생성을 완료하면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="20c69-252">네트워크 제한 사용</span><span class="sxs-lookup"><span data-stu-id="20c69-252">Enable network throttling</span></span>
<span data-ttu-id="20c69-253">Microsoft Azure Backup 에이전트는 네트워크 제한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="20c69-254">제한 기능은 데이터 전송 중에 사용되는 네트워크 대역폭의 양을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="20c69-255">근무 시간에 데이터를 백업해야 하는데 백업 프로세스가 다른 인터넷 트래픽을 방해하지 말아야 할 때 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="20c69-256">제한은 백업 및 복원 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="20c69-257">네트워크 제한은 Windows Server 2008 R2 SP1, Windows Server 2008 SP2 또는 Windows 7(서비스 팩 포함)에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="20c69-258">Azure 백업 네트워크 제한 기능은 로컬 운영 체제에 대한 QoS(서비스 품질)에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="20c69-259">Azure 백업이 이러한 운영 체제를 보호할 수 있지만 이러한 플랫폼에서 사용할 수 있는 QoS의 버전은 Azure 백업 네트워크 제한과 함께 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="20c69-260">네트워크 제한은 다른 모든 [지원되는 운영 체제](backup-azure-backup-faq.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="20c69-261">**네트워크 제한을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="20c69-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="20c69-262">Microsoft Azure Backup 에이전트에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![속성 변경](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="20c69-264">**제한** 탭에서 **백업 작업에 인터넷 대역폭 사용 제한 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![네트워크 제한](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="20c69-266">제한을 사용하도록 설정했으면 **근무 시간** 및 **휴무 시간** 중에 백업 데이터 전송에 허용되는 대역폭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="20c69-267">대역폭 값은 512Kbps(초당 킬로비트)에서 시작하여 최대 1023MBps(초당 메가바이트)까지 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="20c69-268">또한 **근무 시간**의 시작 및 완료 시간과 근무일로 간주되는 요일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="20c69-269">지정된 작업 시간 이외의 시간은 비 작업 시간으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="20c69-270">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="20c69-271">처음으로 파일 및 폴더를 백업하려면</span><span class="sxs-lookup"><span data-stu-id="20c69-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="20c69-272">백업 에이전트에서 **지금 백업** 을 클릭하여 네트워크를 통한 초기 시드 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![지금 Windows Server 백업](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="20c69-274">확인 페이지에서 컴퓨터를 백업하는 데 지금 백업 마법사가 사용할 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="20c69-275">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="20c69-276">**닫기** 를 클릭하여 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="20c69-277">백업 프로세스가 완료되기 전에 이를 수행한 경우 마법사는 백그라운드에서 계속해서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="20c69-278">초기 백업 작업이 완료되면 백업 콘솔에 **작업 완료** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR 완료](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="20c69-280">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="20c69-280">Questions?</span></span>
<span data-ttu-id="20c69-281">질문이 있거나 포함되었으면 하는 기능이 있는 경우 [의견을 보내 주세요](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="20c69-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20c69-282">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20c69-282">Next steps</span></span>
<span data-ttu-id="20c69-283">VM 또는 다른 워크로드를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20c69-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="20c69-284">파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="20c69-285">백업을 복원해야 하는 경우 이 문서를 참조하여 [Windows 컴퓨터에 파일을 복원](backup-azure-restore-windows-server.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c69-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
