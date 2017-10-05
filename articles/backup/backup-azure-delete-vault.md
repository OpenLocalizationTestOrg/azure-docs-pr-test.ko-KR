---
title: " Azure에서 Recovery Services 자격 증명 모음 삭제 | Microsoft Docs "
description: "Azure Backup 및 Recovery Services 자격 증명 모음을 삭제하는 방법입니다. 백업 자격 증명 모음은 Azure 클라우드 자격 증명 모음 또는 Azure 복구 자격 증명 모음이라고 할 수 있습니다. 클래식 포털 또는 Azure Portal에서 백업 자격 증명 모음을 삭제할 수 없을 때 문제를 해결합니다."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: ae4a73d12898c62fe2c5cf3683bc7c1c8c845fdf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-recovery-services-vault"></a><span data-ttu-id="0764c-105">Recovery Services 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-105">Delete a Recovery Services vault</span></span>
<span data-ttu-id="0764c-106">Azure Backup 서비스에는 Backup 자격 증명 모음과 Recovery Services 자격 증명 모음의 두 가지 자격 증명 모음 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-106">The Azure Backup service has two types of vaults - the Backup vault and the Recovery Services vault.</span></span> <span data-ttu-id="0764c-107">Backup 자격 증명 모음을 먼저 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-107">The Backup vault came first.</span></span> <span data-ttu-id="0764c-108">그런 다음 Recovery Services 자격 증명 모음에서 확장된 Resource Manager 배포가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-108">Then the Recovery Services vault came along to support the expanded Resource Manager deployments.</span></span> <span data-ttu-id="0764c-109">자격 증명 모음에 저장해야 하는 정보 종속성 및 확장된 기능으로 인해 Backup 또는 Recovery Services 자격 증명 모음을 삭제하는 것이 혼동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-109">Because of the expanded capabilities and the information dependencies that must be stored in the vault, deleting a Backup or Recovery Services vault can be confusing.</span></span> <span data-ttu-id="0764c-110">이 문서에서는 클래식 포털 및 Azure Portal에서 자격 증명 모음을 삭제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-110">This article explains how to delete the vaults in the classic portal and the Azure portal.</span></span>  

| <span data-ttu-id="0764c-111">**배포 유형**</span><span class="sxs-lookup"><span data-stu-id="0764c-111">**Deployment Type**</span></span> | <span data-ttu-id="0764c-112">**포털**</span><span class="sxs-lookup"><span data-stu-id="0764c-112">**Portal**</span></span> | <span data-ttu-id="0764c-113">**자격 증명 모음 이름**</span><span class="sxs-lookup"><span data-stu-id="0764c-113">**Vault name**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0764c-114">클래식</span><span class="sxs-lookup"><span data-stu-id="0764c-114">Classic</span></span> |<span data-ttu-id="0764c-115">클래식</span><span class="sxs-lookup"><span data-stu-id="0764c-115">Classic</span></span> |<span data-ttu-id="0764c-116">백업 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="0764c-116">Backup vault</span></span> |
| <span data-ttu-id="0764c-117">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="0764c-117">Resource Manager</span></span> |<span data-ttu-id="0764c-118">Azure</span><span class="sxs-lookup"><span data-stu-id="0764c-118">Azure</span></span> |<span data-ttu-id="0764c-119">복구 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="0764c-119">Recovery Services vault</span></span> |

> [!NOTE]
> <span data-ttu-id="0764c-120">백업 자격 증명 모음을 사용하여 Resource Manager에서 배포한 솔루션을 보호할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-120">Backup vaults cannot protect Resource Manager-deployed solutions.</span></span> <span data-ttu-id="0764c-121">그러나 Recovery Services 자격 증명 모음을 사용하면 클래식 방식으로 배포한 서버와 VM을 보호할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-121">However, you can use a Recovery Services vault to protect classically deployed servers and VMs.</span></span>  
>

> [!IMPORTANT]
> <span data-ttu-id="0764c-122">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-122">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="0764c-123">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0764c-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0764c-124">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="0764c-125">**2017년 10월 15일**부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-125">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="0764c-126">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="0764c-126">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="0764c-127">나머지 모든 Backup 자격 증명 모음은 자동으로 Recovery Services 자격 증명 모음으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-127">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="0764c-128">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="0764c-129">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="0764c-130">이 문서에서는 자격 증명 모음이라는 용어를 사용하여 일반 형식의 Backup 자격 증명 모음 또는 Recovery Services 자격 증명 모음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-130">In this article, we use the term, vault, to refer to the generic form of the Backup vault or Recovery Services vault.</span></span> <span data-ttu-id="0764c-131">자격 증명 모음을 구분할 필요가 있을 경우 공식 이름(Backup 자격 증명 모음 또는 Recovery Services 자격 증명 모음)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-131">We use the formal name, Backup vault, or Recovery Services vault, when it is necessary to distinguish between the vaults.</span></span>

## <a name="deleting-a-recovery-services-vault"></a><span data-ttu-id="0764c-132">Recovery Services 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-132">Deleting a Recovery Services vault</span></span>
<span data-ttu-id="0764c-133">Recovery Services 자격 증명 모음을 삭제하는 것은 1단계 프로세스입니다. - *자격 증명 모음에 어떤 리소스도 포함되어 있지 않은 경우*</span><span class="sxs-lookup"><span data-stu-id="0764c-133">Deleting a Recovery Services vault is a one-step process - *provided the vault doesn't contain any resources*.</span></span> <span data-ttu-id="0764c-134">Recovery Services 자격 증명 모음을 삭제하려면 먼저 자격 증명 모음의 모든 리소스를 제거하거나 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-134">Before you can delete a Recovery Services vault, you must remove or delete all resources in the vault.</span></span> <span data-ttu-id="0764c-135">리소스를 포함하는 자격 증명 모음을 삭제하려면 다음 이미지와 같이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-135">If you attempt to delete a vault that contains resources, you get an error like the following image:</span></span>

![자격 증명 모음 삭제 오류](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

<span data-ttu-id="0764c-137">자격 증명 모음에서 리소스를 지우기 전에는 **다시 시도** 를 클릭해도 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-137">Until you have cleared the resources from the vault, clicking **Retry** produces the same error.</span></span> <span data-ttu-id="0764c-138">이 오류 메시지에서 멈춰 있는 경우 **취소** 를 클릭하고 다음 단계를 사용하여 자격 증명 모음에 있는 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-138">If you're stuck on this error message, click **Cancel** and use the following steps to delete the resources in the vault.</span></span>

### <a name="removing-the-items-from-a-vault-protecting-a-vm"></a><span data-ttu-id="0764c-139">VM을 보호하는 자격 증명 모음에서 항목 제거</span><span class="sxs-lookup"><span data-stu-id="0764c-139">Removing the items from a vault protecting a VM</span></span>
<span data-ttu-id="0764c-140">Recovery Services 자격 증명 모음이 이미 열려 있는 경우 두 번째 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-140">If you already have the Recovery Services vault open, skip to the second step.</span></span>

1. <span data-ttu-id="0764c-141">Azure Portal을 열고 대시보드에서 삭제할 자격 증명 모음을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-141">Open the Azure portal, and from the Dashboard open the vault you want to delete.</span></span>

   <span data-ttu-id="0764c-142">허브 메뉴에서 대시보드에 고정된 Recovery Services 자격 증명 모음이 없는 경우 **서비스 더 보기**를 클릭하고 리소스 목록에서 **Recovery Services**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-142">If you don't have the Recovery Services vault pinned to the Dashboard, on the Hub menu, click **More Services** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="0764c-143">입력을 시작하면 입력한 내용을 바탕으로 목록이 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-143">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="0764c-144">**복구 서비스 자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-144">Click **Recovery Services vaults**.</span></span>

   ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   <span data-ttu-id="0764c-146">복구 서비스 자격 증명 모음의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-146">The list of Recovery Services vaults is displayed.</span></span> <span data-ttu-id="0764c-147">목록에서 삭제할 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-147">From the list, select the vault you want to delete.</span></span>

   ![목록에서 자격 증명 모음 선택](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. <span data-ttu-id="0764c-149">자격 증명 모음 보기에서 **필수** 창을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-149">In the vault view, look at the **Essentials** pane.</span></span> <span data-ttu-id="0764c-150">자격 증명 모음을 삭제하려면 보호된 항목이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-150">To delete a vault, there cannot be any protected items.</span></span> <span data-ttu-id="0764c-151">0이 아닌 숫자가 있는 경우 **백업 항목** 또는 **백업 관리 서버** 아래에서 해당 항목을 제거해야 자격 증명 모음을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-151">If you see a number other than zero, under either **Backup Items** or **Backup management servers**, you must remove those items before you can delete the vault.</span></span>

    ![보호된 항목에 대한 필수 창 확인](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    <span data-ttu-id="0764c-153">VM 및 파일/폴더는 백업 항목으로 간주되고 필수 창의 **백업 항목** 영역에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-153">VMs and Files/Folders are considered Backup Items, and are listed in the **Backup Items** area of the Essentials pane.</span></span> <span data-ttu-id="0764c-154">DPM 서버는 필수 창의 **백업 관리 서버** 영역에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-154">A DPM server is listed in the **Backup Management Server** area of the Essentials pane.</span></span> <span data-ttu-id="0764c-155">**복제된 항목** 은 Azure Site Recovery 서비스와 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-155">**Replicated Items** pertain to the Azure Site Recovery service.</span></span>
3. <span data-ttu-id="0764c-156">자격 증명 모음에서 보호된 항목을 제거하기 시작하려면 자격 증명 모음에서 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-156">To begin removing the protected items from the vault, find the items in the vault.</span></span> <span data-ttu-id="0764c-157">자격 증명 모음 대시보드에서 **설정**을 클릭한 다음 **백업 항목**을 클릭하여 해당 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-157">In the vault dashboard click **Settings**, and then click **Backup items** to open that blade.</span></span>

    ![목록에서 자격 증명 모음 선택](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    <span data-ttu-id="0764c-159">**백업 항목** 블레이드에는 Azure Virtual Machines 또는 파일-폴더 등 항목 형식에 따라 별도의 목록이 있습니다(이미지 참조).</span><span class="sxs-lookup"><span data-stu-id="0764c-159">The **Backup Items** blade has separate lists, based on the Item Type: Azure Virtual Machines or File-Folders (see image).</span></span> <span data-ttu-id="0764c-160">표시된 기본 항목 형식 목록은 Azure Virtual Machines입니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-160">The default Item Type list shown is Azure Virtual Machines.</span></span> <span data-ttu-id="0764c-161">자격 증명 모음에서 파일-폴더 항목의 목록을 보려면 드롭다운 메뉴에서 **파일-폴더** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-161">To view the list of File-Folders items in the vault, select **File-Folders** from the drop-down menu.</span></span>
4. <span data-ttu-id="0764c-162">VM을 보호하는 자격 증명 모음에서 항목을 삭제하려면 먼저 항목의 백업 작업을 중지하고 복구 지점 데이터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-162">Before you can delete an item from the vault protecting a VM, you must stop the item's backup job and delete the recovery point data.</span></span> <span data-ttu-id="0764c-163">자격 증명 모음의 각 항목에 대해 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0764c-163">For each item in the vault, follow these steps:</span></span>

    <span data-ttu-id="0764c-164">a.</span><span class="sxs-lookup"><span data-stu-id="0764c-164">a.</span></span> <span data-ttu-id="0764c-165">**백업 항목** 블레이드에서 해당 항목을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **백업 중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-165">On the **Backup Items** blade, right-click the item, and from the context menu, select **Stop backup**.</span></span>

    ![백업 작업 중지](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    <span data-ttu-id="0764c-167">백업 중지 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-167">The Stop Backup blade opens.</span></span>

    <span data-ttu-id="0764c-168">b.</span><span class="sxs-lookup"><span data-stu-id="0764c-168">b.</span></span> <span data-ttu-id="0764c-169">**백업 중지** 블레이드의 **옵션 선택** 메뉴에서 **백업 데이터 삭제** > 항목 이름 입력을 선택하고 **백업 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-169">On the **Stop Backup** blade, from the **Choose an option** menu, select **Delete Backup Data** > type the name of the item > and click **Stop backup**.</span></span>

    <span data-ttu-id="0764c-170">항목 이름을 입력하여 항목을 삭제할지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-170">Type the name of the item, to verify you want to delete it.</span></span> <span data-ttu-id="0764c-171">항목을 확인하면 **백업 중지** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-171">The **Stop Backup** button activates once you verify the item.</span></span> <span data-ttu-id="0764c-172">백업 항목의 이름을 입력할 대화 상자가 보이지 않으면 **백업 데이터 보관** 옵션을 선택한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-172">If you do not see the dialog box to type the name of the backup item, you chose the **Retain Backup Data** option.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="0764c-174">필요에 따라 데이터를 삭제하는 이유를 제공하고 메모를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-174">Optionally, you can provide a reason why you are deleting the data, and add comments.</span></span> <span data-ttu-id="0764c-175">**백업 중지**를 클릭하면 삭제 작업이 완료되어 자격 증명 모음을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-175">After you click **Stop Backup**, allow the delete job to complete before attempting to delete the vault.</span></span> <span data-ttu-id="0764c-176">작업이 완료되었는지 확인하려면 Azure 메시지 ![delete backup data](./media/backup-azure-delete-vault/messages.png)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-176">To verify that the job has completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="0764c-177">작업이 완료되면 백업 프로세스가 중지되고 해당 항목에 대한 백업 데이터가 삭제되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-177">Once the job is complete, you receive a message stating the backup process was stopped and the backup data, for that item, was deleted.</span></span>

    <span data-ttu-id="0764c-178">c.</span><span class="sxs-lookup"><span data-stu-id="0764c-178">c.</span></span> <span data-ttu-id="0764c-179">목록에서 항목을 삭제한 후 **백업 항목** 메뉴에서 **새로 고침**을 클릭하면 자격 증명 모음의 나머지 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-179">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span></span>

      ![백업 데이터 삭제](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="0764c-181">목록에 항목이 없는 경우 Backup 자격 증명 모음 블레이드에서 **필수** 창을 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-181">When there are no items in the list, scroll to the **Essentials** pane in the Backup vault blade.</span></span> <span data-ttu-id="0764c-182">어떤 **백업 항목**, **백업 관리 서버** 또는 **복제된 항목**도 나열되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-182">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="0764c-183">자격 증명 모음에 항목이 아직 나타날 경우 3단계로 돌아가서 다른 항목 유형 목록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-183">If items still appear in the vault, return to step three and choose a different item type list.</span></span>  
5. <span data-ttu-id="0764c-184">자격 증명 모음 도구 모음에 더 이상 항목이 없을 때 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-184">When there are no more items in the vault toolbar, click **Delete**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-vault.png)
6. <span data-ttu-id="0764c-186">자격 증명 모음을 삭제할 것인지 확인하려면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-186">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="0764c-187">자격 증명 모음이 삭제되고 포털이 **새로 만들기** 서비스 메뉴로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-187">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="what-if-i-stopped-the-backup-process-but-retained-the-data"></a><span data-ttu-id="0764c-188">백업 프로세스를 중지했지만 데이터가 남아 있는 경우</span><span class="sxs-lookup"><span data-stu-id="0764c-188">What if I stopped the backup process but retained the data?</span></span>
<span data-ttu-id="0764c-189">백업 프로세스를 중지했지만 실수로 데이터가 *남아 있는* 경우 자격 증명 모음을 삭제하려면 먼저 백업 데이터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-189">If you stopped the backup process but accidentally *retained* the data, you must delete the backup data before you can delete the vault.</span></span> <span data-ttu-id="0764c-190">백업 데이터를 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-190">To delete the backup data:</span></span>

1. <span data-ttu-id="0764c-191">**백업 항목** 블레이드에서 항목을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **백업 데이터 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-191">On the **Backup Items** blade, right-click the item, and on the context menu click **Delete backup data**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    <span data-ttu-id="0764c-193">**백업 데이터 삭제** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-193">The **Delete Backup Data** blade opens.</span></span>
2. <span data-ttu-id="0764c-194">**백업 데이터 삭제** 블레이드에서 항목 이름을 입력하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-194">On the **Delete Backup Data** blade, type the name of the item, and click **Delete**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-retained-vault.png)

    <span data-ttu-id="0764c-196">데이터를 삭제한 후 4c단계로 돌아가서 프로세스를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-196">Once you have deleted the data, return to step 4c and continue with the process.</span></span>

## <a name="delete-a-vault-used-to-protect-a-dpm-server"></a><span data-ttu-id="0764c-197">DPM 서버를 보호하는 데 사용되는 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-197">Delete a vault used to protect a DPM server</span></span>
<span data-ttu-id="0764c-198">DPM 서버를 보호하는 데 사용되는 자격 증명 모음을 삭제하려면 먼저 만들어진 모든 복구 지점을 지운 다음 자격 증명 모음에서 서버 등록을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-198">Before you can delete a vault used to protect a DPM server, you must clear any recovery points that have been created, and then unregister the server from the vault.</span></span>

<span data-ttu-id="0764c-199">보호 그룹과 연결된 데이터를 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-199">To delete the data associated with a protection group:</span></span>

1. <span data-ttu-id="0764c-200">DPM 관리자 콘솔에서 **보호**를 클릭하고, 보호 그룹을 선택하고, 보호 그룹 구성원을 선택하고, 도구 리본에서 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-200">In the DPM Administrator Console, click **Protection** > select a protection group > select the Protection Group Member > and in the tool ribbon, click **Remove**.</span></span>

  <span data-ttu-id="0764c-201">도구 리본의 **제거** 단추를 활성화하려면 보호 그룹 구성원을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-201">Select the Protection Group Member to activate the **Remove** button in the tool ribbon.</span></span> <span data-ttu-id="0764c-202">예제에서 구성원은 **dummyvm9**입니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-202">In the example, the member is **dummyvm9**.</span></span> <span data-ttu-id="0764c-203">보호 그룹에서 여러 구성원을 선택하려면 Ctrl 키를 누른 채로 구성원을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-203">To select multiple members in the protection group, hold down the Ctrl key while clicking on the members.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    <span data-ttu-id="0764c-205">**보호 중지** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-205">The **Stop Protection** dialog opens.</span></span>
2. <span data-ttu-id="0764c-206">**보호 중지** 대화 상자에서 **보호된 데이터 삭제**를 선택하고 **보호 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-206">In the **Stop Protection** dialog, select **Delete protected data**, and click **Stop Protection**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    <span data-ttu-id="0764c-208">자격 증명 모음을 삭제하려면 보호된 데이터의 자격 증명 모음을 선택 취소하거나 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-208">To delete a vault, you must clear, or delete, the vault of protected data.</span></span> <span data-ttu-id="0764c-209">보호 그룹의 복구 지점 수와 데이터에 따라 데이터를 삭제하는 데 수 초에서 수 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-209">Depending on the number of recovery points and data in the protection group, it may take anywhere from a few seconds to several minutes to delete the data.</span></span> <span data-ttu-id="0764c-210">작업이 완료되면 **보호 중지** 대화 상자에 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-210">The **Stop Protection** dialog shows the status when the job has completed.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. <span data-ttu-id="0764c-212">모든 보호 그룹의 모든 멤버에 대해 이 프로세스를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-212">Continue this process for all members in all protection groups.</span></span>

    <span data-ttu-id="0764c-213">모든 보호된 데이터와 보호 그룹을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-213">Remove all protected data and protection groups.</span></span>
4. <span data-ttu-id="0764c-214">보호 그룹에서 모든 구성원을 삭제한 후 Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-214">After deleting all members from the protection group, switch to the Azure portal.</span></span> <span data-ttu-id="0764c-215">자격 증명 모음 대시보드를 열고 **백업 항목**, **백업 관리 서버** 또는 **복제된 항목**이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-215">Open the vault dashboard, and make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="0764c-216">자격 증명 모음 도구 모음에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-216">On the vault toolbar, click **Delete**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-vault.png)

    <span data-ttu-id="0764c-218">자격 증명 모음에 등록된 Backup 관리 서버가 있는 경우 자격 증명 모음에 데이터가 없더라도 자격 증명 모음을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-218">If there are Backup management servers registered to the vault, you can't delete the vault even if there is no data in the vault.</span></span> <span data-ttu-id="0764c-219">자격 증명 모음과 연결된 Backup 관리 서버를 삭제했지만 **필수** 창에 서버가 나열되는 경우 [자격 증명 모음에 등록된 Backup 관리 서버 찾기](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0764c-219">If you deleted the Backup management servers associated with the vault, but there are servers listed in the **Essentials** pane, see [Find the Backup management servers registered to the vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span></span>
5. <span data-ttu-id="0764c-220">자격 증명 모음을 삭제할 것인지 확인하려면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-220">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="0764c-221">자격 증명 모음이 삭제되고 포털이 **새로 만들기** 서비스 메뉴로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-221">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="delete-a-vault-used-to-protect-a-production-server"></a><span data-ttu-id="0764c-222">프로덕션 서버를 보호하는 데 사용되는 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-222">Delete a vault used to protect a Production server</span></span>
<span data-ttu-id="0764c-223">프로덕션 서버를 보호하는 데 사용되는 자격 증명 모음을 삭제하려면 먼저 자격 증명 모음에서 서버를 삭제하거나 등록을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-223">Before you can delete a vault used to protect a Production server, you must delete or unregister the server from the vault.</span></span>

<span data-ttu-id="0764c-224">자격 증명 모음과 연결된 프로덕션 서버를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="0764c-224">To delete the Production server associated with the vault:</span></span>

1. <span data-ttu-id="0764c-225">Azure Portal에서 자격 증명 모음 대시보드를 열고 **설정** > **백업 인프라** > **프로덕션 서버**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-225">In the Azure portal, open the vault dashboard and click **Settings** > **Backup Infrastructure** > **Production Servers**.</span></span>

    ![프로덕션 서버 블레이드 열기](./media/backup-azure-delete-vault/delete-production-server.png)

    <span data-ttu-id="0764c-227">**프로덕션 서버** 블레이드가 열리고 자격 증명 모음에 모든 프로덕션 서버가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-227">The **Production Servers** blade opens and lists all Production servers in the vault.</span></span>

    ![프로덕션 서버 목록](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. <span data-ttu-id="0764c-229">**프로덕션 서버** 블레이드에서 서버를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-229">On the **Production Servers** blade, right-click on the server, and click **Delete**.</span></span>

    ![<span data-ttu-id="0764c-230">프로덕션 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-230">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    <span data-ttu-id="0764c-231">**삭제** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-231">The **Delete** blade opens.</span></span>

    ![<span data-ttu-id="0764c-232">프로덕션 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-232">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-blade.png)
3. <span data-ttu-id="0764c-233">**삭제** 블레이드에서 서버 이름을 확인하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-233">On the **Delete** blade, confirm the server name, and click **Delete**.</span></span> <span data-ttu-id="0764c-234">**삭제** 단추를 활성화하려면 서버의 이름을 올바르게 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-234">You must correctly name the server, to activate the **Delete** button.</span></span>

    <span data-ttu-id="0764c-235">자격 증명 모음이 삭제되면 자격 증명 모음이 삭제되었다는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-235">Once the vault is deleted, you receive a message stating the vault has been deleted.</span></span> <span data-ttu-id="0764c-236">자격 증명 모음에서 모든 서버를 삭제한 후 자격 증명 모음 대시보드의 필수 창으로 다시 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-236">After deleting all servers in the vault, scroll back to the Essentials pane in the vault dashboard.</span></span>
4. <span data-ttu-id="0764c-237">자격 증명 모음 대시보드에서 **백업 항목**, **백업 관리 서버** 또는 **복제된 항목**이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-237">In the vault dashboard, make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="0764c-238">자격 증명 모음 도구 모음에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-238">On the vault toolbar, click **Delete**.</span></span>
5. <span data-ttu-id="0764c-239">자격 증명 모음을 삭제할 것인지 확인하려면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-239">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="0764c-240">자격 증명 모음이 삭제되고 포털이 **새로 만들기** 서비스 메뉴로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-240">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="delete-a-backup-vault-in-classic-portal"></a><span data-ttu-id="0764c-241">클래식 포털에서 백업 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="0764c-241">Delete a backup vault in classic portal</span></span>
<span data-ttu-id="0764c-242">다음은 클래식 포털에서 Backup 자격 증명 모음을 삭제하기 위한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-242">The following instructions are for deleting a Backup vault in the classic portal.</span></span> <span data-ttu-id="0764c-243">Backup 자격 증명 모음을 삭제하려면 먼저 복구 지점 또는 백업된 항목을 삭제하고 등록된 서버를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-243">Before you can delete the Backup vault, you must delete the recovery points, or backed up items, and remove the registered servers.</span></span> <span data-ttu-id="0764c-244">등록된 서버는 Windows 서버, 워크스테이션 또는 자격 증명 모음에 등록된 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-244">The registered servers are the Windows Server, workstation, or virtual machines that were registered to the vault.</span></span>

1. <span data-ttu-id="0764c-245">[클래식 포털](https://manage.windowsazure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-245">Open the [Classic portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="0764c-246">백업 자격 증명 모음 목록에서 삭제할 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-246">From the list of backup vaults, select the vault you want to delete.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    <span data-ttu-id="0764c-248">자격 증명 모음 대시보드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-248">The vault dashboard opens.</span></span> <span data-ttu-id="0764c-249">자격 증명 모음과 연결된 Windows 서버 및/또는 Azure Virtual Machines의 수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-249">Look at the number of Windows Servers and/or Azure virtual machines associated with the vault.</span></span> <span data-ttu-id="0764c-250">또한 Azure에서 사용된 총 저장소를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-250">Also, look at the total storage consumed in Azure.</span></span> <span data-ttu-id="0764c-251">자격 증명 모음을 삭제하기 전에 모든 백업 작업을 중지하고 모든 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-251">Stop all backup jobs and delete all data before deleting the vault.</span></span>

3. <span data-ttu-id="0764c-252">**보호된 항목** 탭을 클릭한 다음 **보호 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-252">Click the **Protected Items** tab, and then click **Stop Protection**</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    <span data-ttu-id="0764c-254">**'자격 증명 모음' 보호 중지** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-254">The **Stop protection of 'your vault'** dialog appears.</span></span>
4. <span data-ttu-id="0764c-255">**'자격 증명 모음' 보호 중지** 대화 상자에서 **연결된 백업 데이터 삭제**를 선택하고 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-255">In the **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](./media/backup-azure-delete-vault/checkmark.png).</span></span> <br/>
    <span data-ttu-id="0764c-256">필요에 따라 보호를 중지하는 이유를 선택하고 메모를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-256">Optionally, you can choose a reason for stopping protection, and provide a comment.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    <span data-ttu-id="0764c-258">자격 증명 모음에서 항목을 삭제한 후 자격 증명 모음을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-258">After deleting the items in the vault, the vault will be empty.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. <span data-ttu-id="0764c-260">탭 목록에서 **등록된 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-260">In the list of tabs, click **Registered Items**.</span></span> <span data-ttu-id="0764c-261">**유형** 드롭다운 메뉴를 사용하여 자격 증명 모음에 등록된 서버 유형을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-261">The **Type** drop-down menu, enables you to choose the type of server registered to the vault.</span></span> <span data-ttu-id="0764c-262">유형은 Windows Server 또는 Azure 가상 컴퓨터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-262">The type can be Windows Server or Azure Virtual Machine.</span></span> <span data-ttu-id="0764c-263">다음 예제에서 자격 증명 모음에 등록된 가상 컴퓨터를 선택하고 **등록 취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-263">In the following example, select the virtual machine registered to the vault, and click **Unregister**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  <span data-ttu-id="0764c-265">Windows Server에 대한 등록을 삭제하려는 경우 **유형** 드롭다운 메뉴에서 **Windows Server**를 선택하고 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)를 클릭하여 화면을 새로 고친 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-265">If you want to delete the registration for a Windows Server, from the **Type** drop-down menu, select **Windows Server**, click ![checkmark](./media/backup-azure-delete-vault/checkmark.png) to refresh the screen, and then click **Delete**.</span></span> <br/>

  ![Windows Server 선택](./media/backup-azure-delete-vault/select-windows-server.png)

6. <span data-ttu-id="0764c-267">탭 목록에서 **대시보드** 를 클릭하여 해당 탭을 엽니다. 클라우드에 보호된 Azure Virtual Machines 또는 등록된 서버가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-267">In the list of tabs, click **Dashboard** to open that tab. Verify there are no registered servers or Azure virtual machines protected in the cloud.</span></span> <span data-ttu-id="0764c-268">또한 저장소에 데이터가 없는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-268">Also, verify there is no data in storage.</span></span> <span data-ttu-id="0764c-269">**삭제** 를 클릭하여 자격 증명 모음을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-269">Click **Delete** to delete the vault.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    <span data-ttu-id="0764c-271">Backup 자격 증명 모음 삭제 확인 화면이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-271">The Delete Backup vault confirmation screen opens.</span></span> <span data-ttu-id="0764c-272">자격 증명 모음을 삭제하는 이유에 대한 옵션을 선택하고 </span><span class="sxs-lookup"><span data-stu-id="0764c-272">Select an option why you're deleting the vault, and click</span></span> ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)<span data-ttu-id="0764c-274">를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-274">.</span></span> <br/>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    <span data-ttu-id="0764c-276">자격 증명 모음이 삭제되면 클래식 포털 대시보드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-276">The vault is deleted, and you return to the classic portal dashboard.</span></span>

### <a name="find-the-backup-management-servers-registered-to-the-vault"></a><span data-ttu-id="0764c-277">자격 증명 모음에 등록된 백업 관리 서버 찾기</span><span class="sxs-lookup"><span data-stu-id="0764c-277">Find the Backup Management servers registered to the vault</span></span>
<span data-ttu-id="0764c-278">자격 증명 모음에 여러 서버가 등록되어 있는 경우 기억하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-278">If you have multiple servers registered to a vault, it can be difficult to remember them.</span></span> <span data-ttu-id="0764c-279">자격 증명 모음에 등록된 서버를 확인하고 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="0764c-279">To see the servers registered to the vault, and delete them:</span></span>

1. <span data-ttu-id="0764c-280">자격 증명 모음 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-280">Open the vault dashboard.</span></span>
2. <span data-ttu-id="0764c-281">**필수** 창에서 **설정**을 클릭하여 해당 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-281">In the **Essentials** pane, click **Settings** to open that blade.</span></span>

    ![설정 블레이드 열기](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. <span data-ttu-id="0764c-283">**설정 블레이드**에서 **백업 인프라**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-283">On the **Settings blade**, click **Backup Infrastructure**.</span></span>
4. <span data-ttu-id="0764c-284">**백업 인프라** 블레이드에서 **백업 관리 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-284">On the **Backup Infrastructure** blade, click **Backup Management Servers**.</span></span> <span data-ttu-id="0764c-285">Backup 관리 서버 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-285">The Backup Management Servers blade opens.</span></span>

    ![백업 관리 서버 목록](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. <span data-ttu-id="0764c-287">목록에서 서버를 삭제하려면 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-287">To delete a server from the list, right-click the name of the server and then click **Delete**.</span></span>
    <span data-ttu-id="0764c-288">**삭제** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-288">The **Delete** blade opens.</span></span>
6. <span data-ttu-id="0764c-289">**삭제** 블레이드에서 서버 이름이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-289">On the **Delete** blade, provide the name of the server.</span></span> <span data-ttu-id="0764c-290">이름이 긴 경우 Backup 관리 서버 목록에서 복사하고 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-290">If it is a long name, you can copy and paste it from the list of Backup Management Servers.</span></span> <span data-ttu-id="0764c-291">그런 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0764c-291">Then click **Delete**.</span></span>  
