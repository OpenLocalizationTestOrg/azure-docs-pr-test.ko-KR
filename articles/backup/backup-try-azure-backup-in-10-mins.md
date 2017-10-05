---
title: "Azure(Resource Manager)에 Windows 파일 및 폴더 백업 | Microsoft Docs"
description: "Resource Manager 배포를 통해 Windows 파일 및 폴더를 Azure로 백업하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 방법; 백업 방법; 파일 및 폴더 백업"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: b21edb70eca3ec9552dc157ee3bb658d243b8fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="cb479-104">먼저 보기: Resource Manager 배포에서 파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="cb479-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="cb479-105">이 문서는 Resource Manager 배포를 사용하여 Windows Server(또는 Windows 컴퓨터) 파일 및 폴더를 Azure에 백업하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span></span> <span data-ttu-id="cb479-106">기본 사항을 안내하기 위해 마련된 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-106">It's a tutorial intended to walk you through the basics.</span></span> <span data-ttu-id="cb479-107">Azure 백업을 시작하려는 분들은 여기서 시작하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-107">If you want to get started using Azure Backup, you're in the right place.</span></span>

<span data-ttu-id="cb479-108">Azure 백업에 대해 자세히 알아보려면 이 [개요](backup-introduction-to-azure-backup.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="cb479-109">Azure 구독이 없는 경우 모든 Azure 서비스에 액세스할 수 있는 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="cb479-110">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="cb479-110">Create a recovery services vault</span></span>
<span data-ttu-id="cb479-111">파일과 폴더를 백업하려면 데이터를 저장하려는 지역에 복구 서비스 자격 증명 모음을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="cb479-112">저장소를 복제할 방식도 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-112">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="cb479-113">복구 서비스 자격 증명 모음을 만들려면</span><span class="sxs-lookup"><span data-stu-id="cb479-113">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="cb479-114">[Azure 포털](https://portal.azure.com/) 에 아직 로그인하지 않은 경우 Azure 구독을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="cb479-115">[허브] 메뉴에서 **추가 서비스**를 클릭하고 리소스 목록에서 **Recovery Services**를 입력한 다음 **Recovery Services 자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="cb479-117">구독에 복구 서비스 자격 증명 모음이 있는 경우 자격 증명 모음이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-117">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="cb479-118">**Recovery Services 자격 증명 모음** 메뉴에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-118">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="cb479-120">복구 서비스 자격 증명 모음 블레이드가 열리고 **이름**, **구독**, **리소스 그룹** 및 **위치**를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="cb479-122">**이름**에 자격 증명 모음을 식별하기 위한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-122">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="cb479-123">이름은 Azure 구독에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-123">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="cb479-124">이름을 2~50자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="cb479-125">문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="cb479-126">**구독** 섹션에서 드롭다운 메뉴를 사용하여 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="cb479-127">구독을 하나만 사용하면 해당 구독이 나타나고 다음 단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="cb479-128">사용할 구독을 잘 모르는 경우 기본(또는 제안된) 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="cb479-129">조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="cb479-130">**리소스 그룹** 섹션에서:</span><span class="sxs-lookup"><span data-stu-id="cb479-130">In the **Resource group** section:</span></span>

    * <span data-ttu-id="cb479-131">리소스 그룹을 새로 만들려면 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-131">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="cb479-132">또는</span><span class="sxs-lookup"><span data-stu-id="cb479-132">Or</span></span>
    * <span data-ttu-id="cb479-133">**기존 그룹 사용**을 선택하고 드롭다운 메뉴를 클릭하여 사용 가능한 리소스 그룹 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="cb479-134">리소스 그룹에 대한 전체 정보는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="cb479-135">**위치** 를 클릭하여 자격 증명 모음에 대한 지리적 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-135">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="cb479-136">선택에 따라 백업 데이터가 전송되는 지역이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-136">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="cb479-137">Recovery Services 자격 증명 모음 블레이드의 하단에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-137">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="cb479-138">Recovery Services 자격 증명 모음을 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-138">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="cb479-139">포털의 오른쪽 위 영역에 있는 상태 알림을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-139">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="cb479-140">자격 증명 모음이 생성되면 복구 서비스 자격 증명 모음 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="cb479-141">몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="cb479-143">Recovery Services 자격 증명 모음 목록에 사용자의 자격 증명 모음이 보이면 저장소 중복을 설정할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="cb479-144">자격 증명 모음에 저장소 중복 설정</span><span class="sxs-lookup"><span data-stu-id="cb479-144">Set storage redundancy for the vault</span></span>
<span data-ttu-id="cb479-145">Recovery Services 자격 증명 모음을 만드는 경우 저장소 중복을 원하는 대로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="cb479-146">**Recovery Services 자격 증명 모음** 블레이드에서 새 자격 증명 모음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-146">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Recovery Services 자격 증명 모음 목록에서 새 자격 증명 모음 선택](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="cb479-148">자격 증명 모음을 선택하면 **Recovery Services 자격 증명 모음** 블레이드가 좁아지고 설정 블레이드(*맨 위에 자격 증명 모음 이름이 있음*) 및 자격 증명 모음 세부 정보 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![새 자격 증명 모음의 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="cb479-150">새 자격 증명 모음의 설정 블레이드에서 세로 슬라이드를 사용하여 관리 섹션 쪽으로 아래로 스크롤하여 **백업 인프라**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="cb479-151">[백업 인프라] 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-151">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="cb479-152">[백업 인프라] 블레이드에서 **백업 구성**을 클릭하여 **백업 구성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![새 자격 증명 모음의 저장소 구성 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="cb479-154">자격 증명 모음에 대해 적절한 저장소 복제 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-154">Choose the appropriate storage replication option for your vault.</span></span>

    ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="cb479-156">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="cb479-157">Azure를 기본 백업 저장소 끝점으로 사용하는 경우 **지역 중복**을 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="cb479-158">Azure를 기본 백업 저장소 끝점으로 사용하지 않는 경우 Azure Storage 비용이 감소되는 **로컬 중복**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="cb479-159">[지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="cb479-160">이제 자격 증명 모음을 만들었으므로 파일과 폴더를 백업하도록 자격 증명 모음을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="cb479-161">자격 증명 모음 구성</span><span class="sxs-lookup"><span data-stu-id="cb479-161">Configure the vault</span></span>
1. <span data-ttu-id="cb479-162">Recovery Services 자격 증명 모음(방금 만든 자격 증명 모음) 블레이드의 [시작] 섹션에서 **백업**을 클릭한 다음 **백업 시작** 블레이드에서 **백업 목표**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="cb479-164">**백업 목표** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-164">The **Backup Goal** blade opens.</span></span>

    ![백업 목표 블레이드 열기](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="cb479-166">**작업이 실행되는 위치** 드롭다운 메뉴에서 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="cb479-167">Windows Server 또는 Windows 컴퓨터가 Azure에 있지 않은 실제 컴퓨터이므로 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="cb479-168">**백업할 항목** 메뉴에서 **파일 및 폴더**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![파일 및 폴더 구성](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="cb479-170">[확인]을 클릭하면 **백업 목표** 옆에 확인 표시가 나타나고 **인프라 준비** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![백업 목표 구성, 다음으로 인프라 준비](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="cb479-172">**인프라 준비** 블레이드에서 **Windows Server 또는 Windows Client용 에이전트 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Windows Server 또는 Windows 클라이언트의 에이전트 다운로드](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="cb479-174">Windows Server Essential을 사용하는 경우 Windows Server Essential 용 에이전트를 다운로드하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="cb479-175">MARSAgentInstaller.exe를 실행하거나 저장하라는 팝업 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller 대화 상자](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="cb479-177">다운로드 팝업 메뉴에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-177">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="cb479-178">기본적으로 **MARSagentinstaller.exe** 파일이 다운로드 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="cb479-179">설치 관리자가 완료되면 설치 관리자를 실행할지 아니면 폴더를 열지 묻는 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![인프라 준비](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="cb479-181">에이전트를 아직 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-181">You don't need to install the agent yet.</span></span> <span data-ttu-id="cb479-182">에이전트는 자격 증명 모음을 다운로드한 후에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-182">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="cb479-183">**인프라 준비** 블레이드에서 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-183">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![자격 증명 모음 자격 증명 다운로드](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="cb479-185">자격 증명 모음 자격 증명이 [다운로드] 폴더로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-185">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="cb479-186">자격 증명 모음 다운로드가 완료되면 자격 증명을 열거나 저장할지 묻는 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="cb479-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-187">Click **Save**.</span></span> <span data-ttu-id="cb479-188">실수로 **열기**를 클릭하면 자격 증명 모음 자격 증명을 열려고 하는 대화 상자가 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="cb479-189">자격 증명 모음 자격 증명을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-189">You cannot open the vault credentials.</span></span> <span data-ttu-id="cb479-190">다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-190">Proceed to the next step.</span></span> <span data-ttu-id="cb479-191">자격 증명 모음은 다운로드 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-191">The vault credentials are in the Downloads folder.</span></span>   

    ![자격 증명 모음 자격 증명 다운로드 완료](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="cb479-193">에이전트 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="cb479-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="cb479-194">Azure Portal을 통한 백업 활성화는 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="cb479-195">Microsoft Azure Recovery Services 에이전트를 사용하여 파일과 폴더를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="cb479-196">다운로드 폴더(또는 기타 저장 위치)에서 **MARSagentinstaller.exe**를 찾아서 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="cb479-197">설치 관리자는 Recovery Services 에이전트를 추출, 설치 및 등록할 때 일련의 메시지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Recovery Services 에이전트 설치 관리자 자격 증명을 실행](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="cb479-199">Microsoft Azure 복구 서비스 에이전트 설치 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="cb479-200">마법사를 완료하려면 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="cb479-201">설치 및 캐시 폴더의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="cb479-202">프록시 서버를 사용하여 인터넷에 연결하는 경우에는 프록시 서버 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="cb479-203">인증된 프록시를 사용하는 경우에는 사용자 이름 및 암호 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="cb479-204">다운로드한 자격 증명 모음 제공</span><span class="sxs-lookup"><span data-stu-id="cb479-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="cb479-205">암호화 암호를 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cb479-206">암호를 분실하거나 잊어버린 경우 Microsoft에서 백업 데이터의 복구를 도와드릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="cb479-207">파일을 안전한 위치에 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-207">Save the file in a secure location.</span></span> <span data-ttu-id="cb479-208">백업을 복원할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="cb479-209">이제 에이전트가 설치되었고 컴퓨터가 자격 증명 모음에 등록되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="cb479-210">백업을 구성하고 일정을 예약할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-210">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="cb479-211">네트워크 및 연결 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cb479-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="cb479-212">컴퓨터/프록시의 인터넷 액세스가 제한되어 있으면 컴퓨터/프록시의 방화벽 설정에서 다음 URL을 허용하도록 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-212">If your machine/proxy has limited internet access, ensure that firewall settings on the mcahine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="cb479-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="cb479-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="cb479-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="cb479-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="cb479-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="cb479-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="cb479-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cb479-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="cb479-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="cb479-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="cb479-218">파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="cb479-218">Back up your files and folders</span></span>
<span data-ttu-id="cb479-219">초기 백업에는 두 가지 주요 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-219">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="cb479-220">백업 예약</span><span class="sxs-lookup"><span data-stu-id="cb479-220">Schedule the backup</span></span>
* <span data-ttu-id="cb479-221">처음으로 파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="cb479-221">Back up files and folders for the first time</span></span>

<span data-ttu-id="cb479-222">최초 백업을 완료하려면 Microsoft Azure Recovery Services 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-222">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="cb479-223">백업 작업을 예약하려면</span><span class="sxs-lookup"><span data-stu-id="cb479-223">To schedule the backup job</span></span>
1. <span data-ttu-id="cb479-224">Microsoft Azure 복구 서비스 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-224">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="cb479-225">**Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Azure 복구 서비스 에이전트 시작](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="cb479-227">복구 서비스 에이전트에서 **백업 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-227">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="cb479-229">백업 예약 마법사의 시작 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-229">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="cb479-230">백업할 항목 선택 페이지에서 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-230">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="cb479-231">백업할 파일 및 폴더를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-231">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="cb479-232">**Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-232">Click **Next**.</span></span>
7. <span data-ttu-id="cb479-233">**백업 일정 지정** 페이지에서 **백업 일정**을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-233">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="cb479-234">매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 백업 항목](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="cb479-236">백업 일정을 지정하는 방법은 [Azure 백업을 사용하여 테이프 인프라 대체](backup-azure-backup-cloud-as-tape.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-236">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="cb479-237">**보존 정책 선택** 페이지에서 백업 복사본의 **보존 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-237">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="cb479-238">보존 정책은 백업 데이터가 저장되는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-238">The retention policy specifies how long the backup data is stored.</span></span> <span data-ttu-id="cb479-239">모든 백업 지점에 대한 "일반 정책"을 지정하는 대신 백업이 발생하는 시기에 따라 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="cb479-240">매일, 매주, 매월 및 매년 보존 정책을 요구 사항에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-240">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="cb479-241">초기 백업 유형 선택 페이지에서 초기 백업 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-241">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="cb479-242">**네트워크를 통해 자동으로** 옵션이 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-242">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="cb479-243">네트워크를 통해 자동으로 백업하거나 오프라인으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-243">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="cb479-244">이 문서의 나머지 부분은 자동 백업 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-244">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="cb479-245">오프라인 백업을 선호하는 경우 [Azure 백업의 오프라인 백업 워크플로](backup-azure-backup-import-export.md) 문서에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-245">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="cb479-246">확인 페이지에서 정보를 검토한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-246">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="cb479-247">마법사가 백업 일정 생성을 완료하면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-247">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="cb479-248">처음으로 파일 및 폴더를 백업하려면</span><span class="sxs-lookup"><span data-stu-id="cb479-248">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="cb479-249">복구 서비스 에이전트에서 **지금 백업** 을 클릭하여 네트워크를 통한 초기 시드 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-249">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server 지금 백업](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="cb479-251">확인 페이지에서 컴퓨터를 백업하는 데 지금 백업 마법사가 사용할 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-251">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="cb479-252">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="cb479-253">**닫기** 를 클릭하여 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-253">Click **Close** to close the wizard.</span></span> <span data-ttu-id="cb479-254">백업 프로세스가 완료되기 전에 마법사를 닫으면 마법사가 백그라운드에서 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-254">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="cb479-255">초기 백업 작업이 완료되면 백업 콘솔에 **작업 완료** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-255">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR 완료](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="cb479-257">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="cb479-257">Questions?</span></span>
<span data-ttu-id="cb479-258">질문이 있거나 포함되었으면 하는 기능이 있는 경우 [의견을 보내 주세요](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="cb479-258">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb479-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb479-259">Next steps</span></span>
* <span data-ttu-id="cb479-260">[Windows 컴퓨터 백업](backup-configure-vault.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cb479-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="cb479-261">파일과 폴더를 백업했으므로 이제 [자격 증명 모음 및 서버](backup-azure-manage-windows-server.md)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="cb479-262">백업을 복원해야 하는 경우 이 문서를 참조하여 [Windows 컴퓨터에 파일을 복원](backup-azure-restore-windows-server.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb479-262">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
