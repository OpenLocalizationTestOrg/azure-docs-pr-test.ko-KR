---
title: " Azure에서 Recovery Services 자격 증명 모음 삭제 | Microsoft Docs "
description: "어떻게 toodelete Azure 백업 및 복구 서비스 자격 증명 모음입니다. 백업 자격 증명 모음은 Azure 클라우드 자격 증명 모음 또는 Azure 복구 자격 증명 모음이라고 할 수 있습니다. 문제 해결 hello 클래식 포털 또는 Azure 포털에서 백업 자격 증명 모음을 삭제할 수 없습니다."
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
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a><span data-ttu-id="5a66e-105">Recovery Services 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="5a66e-105">Delete a Recovery Services vault</span></span>
<span data-ttu-id="5a66e-106">hello Azure 백업 서비스에는 두 가지 유형의 자격 증명 모음-hello 백업 자격 증명 모음 및 hello 복구 서비스 자격 증명 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-106">hello Azure Backup service has two types of vaults - hello Backup vault and hello Recovery Services vault.</span></span> <span data-ttu-id="5a66e-107">hello 백업 자격 증명 모음 먼저 도착 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-107">hello Backup vault came first.</span></span> <span data-ttu-id="5a66e-108">다음 복구 서비스 자격 증명 모음에 hello toosupport 확장 hello 리소스 관리자 배포와 함께 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-108">Then hello Recovery Services vault came along toosupport hello expanded Resource Manager deployments.</span></span> <span data-ttu-id="5a66e-109">Hello 때문에 확장 된 기능 및 hello 자격 증명 모음을 삭제 한 백업 또는 복구 서비스 자격 증명 모음에 저장 해야 하는 hello 정보 종속성 혼동 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-109">Because of hello expanded capabilities and hello information dependencies that must be stored in hello vault, deleting a Backup or Recovery Services vault can be confusing.</span></span> <span data-ttu-id="5a66e-110">이 문서에서는 toodelete hello hello 클래식 포털 및 hello Azure 포털에서 자격 증명 모음는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-110">This article explains how toodelete hello vaults in hello classic portal and hello Azure portal.</span></span>  

| <span data-ttu-id="5a66e-111">**배포 유형**</span><span class="sxs-lookup"><span data-stu-id="5a66e-111">**Deployment Type**</span></span> | <span data-ttu-id="5a66e-112">**포털**</span><span class="sxs-lookup"><span data-stu-id="5a66e-112">**Portal**</span></span> | <span data-ttu-id="5a66e-113">**자격 증명 모음 이름**</span><span class="sxs-lookup"><span data-stu-id="5a66e-113">**Vault name**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a66e-114">클래식</span><span class="sxs-lookup"><span data-stu-id="5a66e-114">Classic</span></span> |<span data-ttu-id="5a66e-115">클래식</span><span class="sxs-lookup"><span data-stu-id="5a66e-115">Classic</span></span> |<span data-ttu-id="5a66e-116">백업 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="5a66e-116">Backup vault</span></span> |
| <span data-ttu-id="5a66e-117">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="5a66e-117">Resource Manager</span></span> |<span data-ttu-id="5a66e-118">Azure</span><span class="sxs-lookup"><span data-stu-id="5a66e-118">Azure</span></span> |<span data-ttu-id="5a66e-119">복구 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="5a66e-119">Recovery Services vault</span></span> |

> [!NOTE]
> <span data-ttu-id="5a66e-120">백업 자격 증명 모음을 사용하여 Resource Manager에서 배포한 솔루션을 보호할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-120">Backup vaults cannot protect Resource Manager-deployed solutions.</span></span> <span data-ttu-id="5a66e-121">그러나 복구 서비스 자격 증명 모음을 사용할 수 tooprotect 일반적 서버 및 Vm을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-121">However, you can use a Recovery Services vault tooprotect classically deployed servers and VMs.</span></span>  
>

> [!IMPORTANT]
> <span data-ttu-id="5a66e-122">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-122">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="5a66e-123">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="5a66e-124">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="5a66e-125">**2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-125">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="5a66e-126">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="5a66e-126">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="5a66e-127">나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-127">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="5a66e-128">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="5a66e-129">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="5a66e-130">이 문서에서는 hello 용어, 자격 증명 모음, toorefer toohello 제네릭 형식 hello 백업 자격 증명 모음 또는 복구 서비스 자격 증명 모음으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-130">In this article, we use hello term, vault, toorefer toohello generic form of hello Backup vault or Recovery Services vault.</span></span> <span data-ttu-id="5a66e-131">Hello 자격 증명 모음 간에 필요한 toodistinguish 되었을 때 hello 정식 이름, 백업 자격 증명 모음 또는 복구 서비스 자격 증명 모음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-131">We use hello formal name, Backup vault, or Recovery Services vault, when it is necessary toodistinguish between hello vaults.</span></span>

## <a name="deleting-a-recovery-services-vault"></a><span data-ttu-id="5a66e-132">Recovery Services 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="5a66e-132">Deleting a Recovery Services vault</span></span>
<span data-ttu-id="5a66e-133">1 단계 프로세스-복구 서비스 자격 증명 모음을 삭제는 *hello 자격 증명 모음 리소스가 없습니다. 제공 된*합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-133">Deleting a Recovery Services vault is a one-step process - *provided hello vault doesn't contain any resources*.</span></span> <span data-ttu-id="5a66e-134">복구 서비스 자격 증명 모음을 삭제 하려면 먼저 제거 하거나 hello 자격 증명 모음에 있는 모든 리소스를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-134">Before you can delete a Recovery Services vault, you must remove or delete all resources in hello vault.</span></span> <span data-ttu-id="5a66e-135">Toodelete 리소스가 포함 된 자격 증명 모음을 시도 하면 다음 이미지는 hello와 같은 오류 메시지가.</span><span class="sxs-lookup"><span data-stu-id="5a66e-135">If you attempt toodelete a vault that contains resources, you get an error like hello following image:</span></span>

![자격 증명 모음 삭제 오류](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

<span data-ttu-id="5a66e-137">Hello 리소스 hello 자격 증명 모음에서을 지우면 될 때까지 클릭 하면 **을 다시 시도** 생성 hello 동일한 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-137">Until you have cleared hello resources from hello vault, clicking **Retry** produces hello same error.</span></span> <span data-ttu-id="5a66e-138">이 오류 메시지에서 나올 수, 클릭 **취소** 및 사용 하 여 hello 다음 단계 hello 자격 증명 모음에 toodelete hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-138">If you're stuck on this error message, click **Cancel** and use hello following steps toodelete hello resources in hello vault.</span></span>

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a><span data-ttu-id="5a66e-139">VM을 보호 하는 자격 증명 모음에서 hello 항목 제거</span><span class="sxs-lookup"><span data-stu-id="5a66e-139">Removing hello items from a vault protecting a VM</span></span>
<span data-ttu-id="5a66e-140">Hello 복구 서비스 자격 증명 모음을 열고 이미 있는 경우 toohello 두 번째 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-140">If you already have hello Recovery Services vault open, skip toohello second step.</span></span>

1. <span data-ttu-id="5a66e-141">Hello Azure 포털을 열고 hello 대시보드에서에서 원하는 toodelete hello 자격 증명 모음을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-141">Open hello Azure portal, and from hello Dashboard open hello vault you want toodelete.</span></span>

   <span data-ttu-id="5a66e-142">복구 서비스 자격 증명 모음에 hello hello 허브 메뉴에서 대시보드를 toohello 고정 없는 경우, 클릭 **더 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-142">If you don't have hello Recovery Services vault pinned toohello Dashboard, on hello Hub menu, click **More Services** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="5a66e-143">입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-143">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="5a66e-144">**복구 서비스 자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-144">Click **Recovery Services vaults**.</span></span>

   ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   <span data-ttu-id="5a66e-146">복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-146">hello list of Recovery Services vaults is displayed.</span></span> <span data-ttu-id="5a66e-147">Hello 목록에서 원하는 toodelete hello 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-147">From hello list, select hello vault you want toodelete.</span></span>

   ![목록에서 자격 증명 모음 선택](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. <span data-ttu-id="5a66e-149">Hello에 자격 증명 모음 보기 봐 hello에 **Essentials** 창.</span><span class="sxs-lookup"><span data-stu-id="5a66e-149">In hello vault view, look at hello **Essentials** pane.</span></span> <span data-ttu-id="5a66e-150">자격 증명 모음, toodelete 모든 보호 된 항목이 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-150">toodelete a vault, there cannot be any protected items.</span></span> <span data-ttu-id="5a66e-151">아래에서 0이 아닌 숫자로 표시 되 면 **백업 항목** 또는 **관리 서버를 백업**, hello 자격 증명 모음을 삭제 하려면 먼저 해당 항목을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-151">If you see a number other than zero, under either **Backup Items** or **Backup management servers**, you must remove those items before you can delete hello vault.</span></span>

    ![보호된 항목에 대한 필수 창 확인](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    <span data-ttu-id="5a66e-153">백업 항목으로 간주 됩니다 hello에 나열 된 Vm 및 파일/폴더 **백업 항목** hello Essentials 창의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-153">VMs and Files/Folders are considered Backup Items, and are listed in hello **Backup Items** area of hello Essentials pane.</span></span> <span data-ttu-id="5a66e-154">DPM 서버 hello에 나열 된 **백업 관리 서버** hello Essentials 창의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-154">A DPM server is listed in hello **Backup Management Server** area of hello Essentials pane.</span></span> <span data-ttu-id="5a66e-155">**복제 된 항목이** toohello Azure Site Recovery 서비스와 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-155">**Replicated Items** pertain toohello Azure Site Recovery service.</span></span>
3. <span data-ttu-id="5a66e-156">hello 제거 toobegin hello 자격 증명 모음, hello 자격 증명 모음에 찾기 hello 항목에서에서 항목을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-156">toobegin removing hello protected items from hello vault, find hello items in hello vault.</span></span> <span data-ttu-id="5a66e-157">Hello 자격 증명 모음 대시보드 클릭 **설정**, 클릭 하 고 **항목 백업** tooopen 해당 블레이드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-157">In hello vault dashboard click **Settings**, and then click **Backup items** tooopen that blade.</span></span>

    ![목록에서 자격 증명 모음 선택](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    <span data-ttu-id="5a66e-159">hello **백업 항목** 블레이드는 별도 목록, hello 항목 형식에 따라: Azure 가상 컴퓨터 또는 파일 폴더 (이미지 참조).</span><span class="sxs-lookup"><span data-stu-id="5a66e-159">hello **Backup Items** blade has separate lists, based on hello Item Type: Azure Virtual Machines or File-Folders (see image).</span></span> <span data-ttu-id="5a66e-160">hello 기본 항목 형식 표시 된 목록은 Azure 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-160">hello default Item Type list shown is Azure Virtual Machines.</span></span> <span data-ttu-id="5a66e-161">tooview hello 파일 폴더의에서 항목 목록에 hello 자격 **파일 폴더** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-161">tooview hello list of File-Folders items in hello vault, select **File-Folders** from hello drop-down menu.</span></span>
4. <span data-ttu-id="5a66e-162">VM 보호 hello 자격 증명 모음에서 항목을 삭제할 수 있습니다, 전에 hello 항목의 백업 작업을 중지 하 고 hello 복구 지점 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-162">Before you can delete an item from hello vault protecting a VM, you must stop hello item's backup job and delete hello recovery point data.</span></span> <span data-ttu-id="5a66e-163">각 항목 hello 자격 증명 모음에 대해 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="5a66e-163">For each item in hello vault, follow these steps:</span></span>

    <span data-ttu-id="5a66e-164">a.</span><span class="sxs-lookup"><span data-stu-id="5a66e-164">a.</span></span> <span data-ttu-id="5a66e-165">Hello에 **백업 항목** 블레이드에서 마우스 오른쪽 단추로 클릭 hello 항목, hello 상황에 맞는 메뉴에서 선택 **백업 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-165">On hello **Backup Items** blade, right-click hello item, and from hello context menu, select **Stop backup**.</span></span>

    ![hello 백업 작업을 중지 합니다.](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    <span data-ttu-id="5a66e-167">hello 백업 중지 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-167">hello Stop Backup blade opens.</span></span>

    <span data-ttu-id="5a66e-168">b.</span><span class="sxs-lookup"><span data-stu-id="5a66e-168">b.</span></span> <span data-ttu-id="5a66e-169">Hello에 **백업 중지** 블레이드 hello에서 **옵션을 선택** 메뉴 선택 **백업 데이터 삭제** > hello 항목의 형식 hello 이름 >을 클릭 하 고 **중지 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-169">On hello **Stop Backup** blade, from hello **Choose an option** menu, select **Delete Backup Data** > type hello name of hello item > and click **Stop backup**.</span></span>

    <span data-ttu-id="5a66e-170">항목 hello tooverify toodelete를 원하는 형식 hello 이름을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-170">Type hello name of hello item, tooverify you want toodelete it.</span></span> <span data-ttu-id="5a66e-171">hello **백업 중지** hello 항목을 확인 한 후 단추를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-171">hello **Stop Backup** button activates once you verify hello item.</span></span> <span data-ttu-id="5a66e-172">Hello 선택한 hello 백업 항목의 hello 대화 상자 tootype hello 이름, 표시 되지 않으면 **백업 데이터 보관** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-172">If you do not see hello dialog box tootype hello name of hello backup item, you chose hello **Retain Backup Data** option.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="5a66e-174">필요에 따라 hello 데이터를 삭제 하는 이유와 설명을 추가 하는 이유를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-174">Optionally, you can provide a reason why you are deleting hello data, and add comments.</span></span> <span data-ttu-id="5a66e-175">클릭 한 후 **백업 중지**, toodelete hello 자격 증명 모음을 시도 하기 전에 hello 삭제 작업 toocomplete 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-175">After you click **Stop Backup**, allow hello delete job toocomplete before attempting toodelete hello vault.</span></span> <span data-ttu-id="5a66e-176">완료 된 작업 hello tooverify, hello Azure 메시지 확인 ![백업 데이터를 삭제](./media/backup-azure-delete-vault/messages.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-176">tooverify that hello job has completed, check hello Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="5a66e-177">Hello 작업이 완료 되 면 hello 백업 프로세스를 중지 했 고 해당 항목에 대 한 hello 백업 데이터가 삭제 되었다는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-177">Once hello job is complete, you receive a message stating hello backup process was stopped and hello backup data, for that item, was deleted.</span></span>

    <span data-ttu-id="5a66e-178">c.</span><span class="sxs-lookup"><span data-stu-id="5a66e-178">c.</span></span> <span data-ttu-id="5a66e-179">Hello에 hello 목록에서 항목을 삭제 한 후 **백업 항목** 메뉴를 클릭 하 여 **새로 고침** hello 자격 증명 모음에 있는 항목에 남은 toosee hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-179">After deleting an item in hello list, on hello **Backup Items** menu, click **Refresh** toosee hello remaining items in hello vault.</span></span>

      ![백업 데이터 삭제](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="5a66e-181">Hello 목록에 항목이 없는 경우 스크롤 toohello **Essentials** hello 백업 자격 증명 모음 블레이드에서 창.</span><span class="sxs-lookup"><span data-stu-id="5a66e-181">When there are no items in hello list, scroll toohello **Essentials** pane in hello Backup vault blade.</span></span> <span data-ttu-id="5a66e-182">어떤 **백업 항목**, **백업 관리 서버** 또는 **복제된 항목**도 나열되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-182">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="5a66e-183">항목이 hello 자격 증명 모음에 여전히 나타날, toostep 3을 반환 하 고 다른 항목 유형 목록을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-183">If items still appear in hello vault, return toostep three and choose a different item type list.</span></span>  
5. <span data-ttu-id="5a66e-184">Hello 자격 증명 모음 도구 모음에 항목이 더 이상 있을 때 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-184">When there are no more items in hello vault toolbar, click **Delete**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-vault.png)
6. <span data-ttu-id="5a66e-186">toodelete hello 자격 증명 모음을 사용 하지 않겠다고 tooverify 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-186">tooverify that you want toodelete hello vault, click **Yes**.</span></span>

    <span data-ttu-id="5a66e-187">hello 자격 증명 모음 삭제 되 고 hello 포털 반환 toohello **새로** 서비스 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5a66e-187">hello vault is deleted and hello portal returns toohello **New** service menu.</span></span>

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a><span data-ttu-id="5a66e-188">경우에 어떻게 hello 백업 프로세스를 중지 합니다.이 있지만 보관 된 hello 데이터?</span><span class="sxs-lookup"><span data-stu-id="5a66e-188">What if I stopped hello backup process but retained hello data?</span></span>
<span data-ttu-id="5a66e-189">하지만 실수로 hello 백업 프로세스를 중지 한 경우 *유지* hello 데이터 hello 자격 증명 모음을 삭제 하기 전에 hello 백업 데이터 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-189">If you stopped hello backup process but accidentally *retained* hello data, you must delete hello backup data before you can delete hello vault.</span></span> <span data-ttu-id="5a66e-190">toodelete hello 백업 데이터:</span><span class="sxs-lookup"><span data-stu-id="5a66e-190">toodelete hello backup data:</span></span>

1. <span data-ttu-id="5a66e-191">Hello에 **백업 항목** 블레이드에서 마우스 오른쪽 단추로 클릭 hello 항목, hello 상황에 맞는 메뉴에서을 클릭 하 여 **백업 데이터를 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-191">On hello **Backup Items** blade, right-click hello item, and on hello context menu click **Delete backup data**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    <span data-ttu-id="5a66e-193">hello **백업 데이터 삭제** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-193">hello **Delete Backup Data** blade opens.</span></span>
2. <span data-ttu-id="5a66e-194">Hello에 **백업 데이터 삭제** hello 항목과 클릭의 hello 이름을 입력 합니다 블레이드 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-194">On hello **Delete Backup Data** blade, type hello name of hello item, and click **Delete**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-retained-vault.png)

    <span data-ttu-id="5a66e-196">Hello 데이터를 삭제 한 후 4 c toostep 돌아간 hello 프로세스를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-196">Once you have deleted hello data, return toostep 4c and continue with hello process.</span></span>

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a><span data-ttu-id="5a66e-197">사용 되는 자격 증명 모음 tooprotect DPM 서버를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-197">Delete a vault used tooprotect a DPM server</span></span>
<span data-ttu-id="5a66e-198">사용 되는 자격 증명 모음 tooprotect DPM 서버를 삭제 하기 전에 생성 된 모든 복구 지점이 선택을 취소 하 고 hello 서버 hello 자격 증명 모음에서 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-198">Before you can delete a vault used tooprotect a DPM server, you must clear any recovery points that have been created, and then unregister hello server from hello vault.</span></span>

<span data-ttu-id="5a66e-199">보호 그룹과 연결 된 toodelete hello 데이터:</span><span class="sxs-lookup"><span data-stu-id="5a66e-199">toodelete hello data associated with a protection group:</span></span>

1. <span data-ttu-id="5a66e-200">Hello DPM 관리자 콘솔에서에서 클릭 **보호** > 보호 그룹을 선택 > 선택 hello 보호 그룹 구성원 > hello 도구 리본에서을 클릭 하 고 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-200">In hello DPM Administrator Console, click **Protection** > select a protection group > select hello Protection Group Member > and in hello tool ribbon, click **Remove**.</span></span>

  <span data-ttu-id="5a66e-201">보호 그룹 구성원 tooactivate hello 선택 hello **제거** hello 도구 리본에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-201">Select hello Protection Group Member tooactivate hello **Remove** button in hello tool ribbon.</span></span> <span data-ttu-id="5a66e-202">Hello 예제 hello 멤버는 **dummyvm9**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-202">In hello example, hello member is **dummyvm9**.</span></span> <span data-ttu-id="5a66e-203">tooselect hello 보호 그룹의 여러 멤버 hello Ctrl 키를 누른 채 hello 멤버를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-203">tooselect multiple members in hello protection group, hold down hello Ctrl key while clicking on hello members.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    <span data-ttu-id="5a66e-205">hello **보호 중지** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-205">hello **Stop Protection** dialog opens.</span></span>
2. <span data-ttu-id="5a66e-206">Hello에 **보호 중지** 대화 상자에서 **보호 된 데이터 삭제**를 클릭 하 고 **보호 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-206">In hello **Stop Protection** dialog, select **Delete protected data**, and click **Stop Protection**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    <span data-ttu-id="5a66e-208">toodelete 자격 증명 모음을 선택 취소 하거나 삭제 해야, 보호 된 데이터의 hello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-208">toodelete a vault, you must clear, or delete, hello vault of protected data.</span></span> <span data-ttu-id="5a66e-209">복구 지점 및 hello 보호 그룹의 데이터를 hello 수에 따라 소요 아무 곳 이나 몇 초 tooseveral 분 toodelete hello 데이터에서.</span><span class="sxs-lookup"><span data-stu-id="5a66e-209">Depending on hello number of recovery points and data in hello protection group, it may take anywhere from a few seconds tooseveral minutes toodelete hello data.</span></span> <span data-ttu-id="5a66e-210">hello **보호 중지** hello 작업이 완료 되 면 hello 상태 대화 상자에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-210">hello **Stop Protection** dialog shows hello status when hello job has completed.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. <span data-ttu-id="5a66e-212">모든 보호 그룹의 모든 멤버에 대해 이 프로세스를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-212">Continue this process for all members in all protection groups.</span></span>

    <span data-ttu-id="5a66e-213">모든 보호된 데이터와 보호 그룹을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-213">Remove all protected data and protection groups.</span></span>
4. <span data-ttu-id="5a66e-214">Hello 보호 그룹에서 모든 멤버를 삭제 한 후 Azure 포털 toohello를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-214">After deleting all members from hello protection group, switch toohello Azure portal.</span></span> <span data-ttu-id="5a66e-215">Hello 자격 증명 모음 대시보드를 열고 없는지 확인 없는 **백업 항목**, **관리 서버를 백업**, 또는 **복제 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-215">Open hello vault dashboard, and make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="5a66e-216">Hello 자격 증명 모음 도구 모음에서 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-216">On hello vault toolbar, click **Delete**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-vault.png)

    <span data-ttu-id="5a66e-218">백업 관리 서버를 등록 toohello 자격 증명 모음에 있는 경우 hello 자격 증명 모음에 데이터가 없는 경우에 hello 자격 증명 모음을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-218">If there are Backup management servers registered toohello vault, you can't delete hello vault even if there is no data in hello vault.</span></span> <span data-ttu-id="5a66e-219">Hello 자격 증명 모음에 연결 하는 hello 백업 관리 서버를 삭제 되었지만 hello에 나열 된 서버가 없는 경우 **Essentials** 창 참조 [찾기 hello 백업 관리 서버 등록된 toohello 자격 증명 모음](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .</span><span class="sxs-lookup"><span data-stu-id="5a66e-219">If you deleted hello Backup management servers associated with hello vault, but there are servers listed in hello **Essentials** pane, see [Find hello Backup management servers registered toohello vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span></span>
5. <span data-ttu-id="5a66e-220">toodelete hello 자격 증명 모음을 사용 하지 않겠다고 tooverify 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-220">tooverify that you want toodelete hello vault, click **Yes**.</span></span>

    <span data-ttu-id="5a66e-221">hello 자격 증명 모음 삭제 되 고 hello 포털 반환 toohello **새로** 서비스 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5a66e-221">hello vault is deleted and hello portal returns toohello **New** service menu.</span></span>

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a><span data-ttu-id="5a66e-222">사용 되는 자격 증명 모음 tooprotect 프로덕션 서버를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-222">Delete a vault used tooprotect a Production server</span></span>
<span data-ttu-id="5a66e-223">사용 되는 자격 증명 모음 tooprotect 프로덕션 서버를 삭제 하기 전에 삭제 하거나 hello 서버 hello 자격 증명 모음에서 등록을 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-223">Before you can delete a vault used tooprotect a Production server, you must delete or unregister hello server from hello vault.</span></span>

<span data-ttu-id="5a66e-224">toodelete hello 프로덕션 hello 자격 증명 모음과 연결 된 서버:</span><span class="sxs-lookup"><span data-stu-id="5a66e-224">toodelete hello Production server associated with hello vault:</span></span>

1. <span data-ttu-id="5a66e-225">Hello Azure 포털에서에서 자격 증명 모음 대시보드 hello 열고 클릭 **설정** > **백업 인프라** > **프로덕션 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-225">In hello Azure portal, open hello vault dashboard and click **Settings** > **Backup Infrastructure** > **Production Servers**.</span></span>

    ![프로덕션 서버 블레이드 열기](./media/backup-azure-delete-vault/delete-production-server.png)

    <span data-ttu-id="5a66e-227">hello **프로덕션 서버** 블레이드가 열리고 hello 자격 증명 모음에 모든 프로덕션 서버를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-227">hello **Production Servers** blade opens and lists all Production servers in hello vault.</span></span>

    ![프로덕션 서버 목록](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. <span data-ttu-id="5a66e-229">Hello에 **프로덕션 서버** 블레이드에서 hello 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-229">On hello **Production Servers** blade, right-click on hello server, and click **Delete**.</span></span>

    ![<span data-ttu-id="5a66e-230">프로덕션 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="5a66e-230">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    <span data-ttu-id="5a66e-231">hello **삭제** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-231">hello **Delete** blade opens.</span></span>

    ![<span data-ttu-id="5a66e-232">프로덕션 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="5a66e-232">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-blade.png)
3. <span data-ttu-id="5a66e-233">Hello에 **삭제** 블레이드에서 hello 서버 이름을 확인 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-233">On hello **Delete** blade, confirm hello server name, and click **Delete**.</span></span> <span data-ttu-id="5a66e-234">서버 hello tooactivate hello 이름을 올바르게 지정 해야 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-234">You must correctly name hello server, tooactivate hello **Delete** button.</span></span>

    <span data-ttu-id="5a66e-235">Hello 자격 증명 모음 삭제 되 면 hello 자격 증명 모음 삭제 되었음을 알리는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-235">Once hello vault is deleted, you receive a message stating hello vault has been deleted.</span></span> <span data-ttu-id="5a66e-236">Hello 자격 증명 모음에 모든 서버를 삭제 한 후 뒤로 toohello Essentials 창을 hello 자격 증명 모음 대시보드를 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="5a66e-236">After deleting all servers in hello vault, scroll back toohello Essentials pane in hello vault dashboard.</span></span>
4. <span data-ttu-id="5a66e-237">Hello 자격 증명 모음 대시보드에 없는지 확인 없는 **백업 항목**, **관리 서버를 백업**, 또는 **복제 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-237">In hello vault dashboard, make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="5a66e-238">Hello 자격 증명 모음 도구 모음에서 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-238">On hello vault toolbar, click **Delete**.</span></span>
5. <span data-ttu-id="5a66e-239">toodelete hello 자격 증명 모음을 사용 하지 않겠다고 tooverify 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-239">tooverify that you want toodelete hello vault, click **Yes**.</span></span>

    <span data-ttu-id="5a66e-240">hello 자격 증명 모음 삭제 되 고 hello 포털 반환 toohello **새로** 서비스 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5a66e-240">hello vault is deleted and hello portal returns toohello **New** service menu.</span></span>

## <a name="delete-a-backup-vault-in-classic-portal"></a><span data-ttu-id="5a66e-241">클래식 포털에서 백업 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="5a66e-241">Delete a backup vault in classic portal</span></span>
<span data-ttu-id="5a66e-242">hello 다음 지침은에 hello 클래식 포털에서 백업 자격 증명 모음을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-242">hello following instructions are for deleting a Backup vault in hello classic portal.</span></span> <span data-ttu-id="5a66e-243">Hello 백업 자격 증명 모음을 삭제 하려면 먼저 있습니다 hello 복구 지점을 삭제 해야 또는 백업 항목 및 hello 등록 된 서버를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-243">Before you can delete hello Backup vault, you must delete hello recovery points, or backed up items, and remove hello registered servers.</span></span> <span data-ttu-id="5a66e-244">hello 등록 된 서버를 Windows Server hello, 워크스테이션 또는 등록 된 toohello 자격 증명 모음에 있던 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-244">hello registered servers are hello Windows Server, workstation, or virtual machines that were registered toohello vault.</span></span>

1. <span data-ttu-id="5a66e-245">열기 hello [클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-245">Open hello [Classic portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="5a66e-246">백업 자격 증명 모음의 hello 목록에서 원하는 toodelete hello 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-246">From hello list of backup vaults, select hello vault you want toodelete.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    <span data-ttu-id="5a66e-248">hello 자격 증명 모음 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-248">hello vault dashboard opens.</span></span> <span data-ttu-id="5a66e-249">Hello 자격 증명 모음과 연결 하는 Windows 서버 및/또는 Azure 가상 컴퓨터의 hello 숫자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-249">Look at hello number of Windows Servers and/or Azure virtual machines associated with hello vault.</span></span> <span data-ttu-id="5a66e-250">또한 hello Azure에서 사용 되는 총 저장소를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-250">Also, look at hello total storage consumed in Azure.</span></span> <span data-ttu-id="5a66e-251">모든 백업 작업을 중지 하 고 hello 자격 증명 모음을 삭제 하기 전에 모든 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-251">Stop all backup jobs and delete all data before deleting hello vault.</span></span>

3. <span data-ttu-id="5a66e-252">Hello 클릭 **보호 된 항목** 탭을 클릭 한 다음 **보호 중지**</span><span class="sxs-lookup"><span data-stu-id="5a66e-252">Click hello **Protected Items** tab, and then click **Stop Protection**</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    <span data-ttu-id="5a66e-254">hello **'자격 증명 모음'의 보호를 중지** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-254">hello **Stop protection of 'your vault'** dialog appears.</span></span>
4. <span data-ttu-id="5a66e-255">Hello에 **'자격 증명 모음'의 보호를 중지** 대화 상자에서 확인 **연결 된 백업 데이터 삭제** 클릭 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-255">In hello **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](./media/backup-azure-delete-vault/checkmark.png).</span></span> <br/>
    <span data-ttu-id="5a66e-256">필요에 따라 보호를 중지하는 이유를 선택하고 메모를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-256">Optionally, you can choose a reason for stopping protection, and provide a comment.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    <span data-ttu-id="5a66e-258">Hello 자격 증명 모음의 hello 항목을 삭제 한 후 자격 증명 모음 hello 비어 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-258">After deleting hello items in hello vault, hello vault will be empty.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. <span data-ttu-id="5a66e-260">탭의 hello 목록에서 클릭 **등록 된 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-260">In hello list of tabs, click **Registered Items**.</span></span> <span data-ttu-id="5a66e-261">hello **형식** 드롭 다운 메뉴에서 등록 된 서버 toohello 자격 증명 모음의 toochoose hello 입력 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-261">hello **Type** drop-down menu, enables you toochoose hello type of server registered toohello vault.</span></span> <span data-ttu-id="5a66e-262">hello 형식은 Windows Server 또는 Azure 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-262">hello type can be Windows Server or Azure Virtual Machine.</span></span> <span data-ttu-id="5a66e-263">다음 예제는 hello에서 hello 가상 컴퓨터 등록된 toohello 자격 증명 모음을 선택 하 고 클릭 **등록 취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-263">In hello following example, select hello virtual machine registered toohello vault, and click **Unregister**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  <span data-ttu-id="5a66e-265">Windows 서버 hello에 대 한 toodelete hello 등록 하려는 경우 **형식** 드롭 다운 메뉴 **Windows Server**, 클릭 ![확인 표시](./media/backup-azure-delete-vault/checkmark.png) toorefresh hello 화면 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-265">If you want toodelete hello registration for a Windows Server, from hello **Type** drop-down menu, select **Windows Server**, click ![checkmark](./media/backup-azure-delete-vault/checkmark.png) toorefresh hello screen, and then click **Delete**.</span></span> <br/>

  ![Windows Server 선택](./media/backup-azure-delete-vault/select-windows-server.png)

6. <span data-ttu-id="5a66e-267">탭의 hello 목록에서 클릭 **대시보드** tooopen 탭입니다. 등록 된 서버 또는 hello 클라우드에서 보호 되는 Azure 가상 컴퓨터에 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-267">In hello list of tabs, click **Dashboard** tooopen that tab. Verify there are no registered servers or Azure virtual machines protected in hello cloud.</span></span> <span data-ttu-id="5a66e-268">또한 저장소에 데이터가 없는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-268">Also, verify there is no data in storage.</span></span> <span data-ttu-id="5a66e-269">클릭 **삭제** toodelete hello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-269">Click **Delete** toodelete hello vault.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    <span data-ttu-id="5a66e-271">hello 삭제 백업 자격 증명 모음 확인 화면이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-271">hello Delete Backup vault confirmation screen opens.</span></span> <span data-ttu-id="5a66e-272">Hello 자격 증명 모음을 삭제 하는 이유는 옵션을 선택 하 고 클릭</span><span class="sxs-lookup"><span data-stu-id="5a66e-272">Select an option why you're deleting hello vault, and click</span></span> ![확인 표시](./media/backup-azure-delete-vault/checkmark.png)<span data-ttu-id="5a66e-274">를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-274">.</span></span> <br/>

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    <span data-ttu-id="5a66e-276">hello 자격 증명 모음 삭제 되 고, toohello 클래식 포털 대시보드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-276">hello vault is deleted, and you return toohello classic portal dashboard.</span></span>

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a><span data-ttu-id="5a66e-277">자격 증명 모음 백업을 관리 서버 등록된 toohello hello 찾기</span><span class="sxs-lookup"><span data-stu-id="5a66e-277">Find hello Backup Management servers registered toohello vault</span></span>
<span data-ttu-id="5a66e-278">자격 증명 모음 tooa 등록 된 서버를 여러 개 있는 경우는 것이 어려운 tooremember 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-278">If you have multiple servers registered tooa vault, it can be difficult tooremember them.</span></span> <span data-ttu-id="5a66e-279">toosee hello 서버 toohello 자격 증명 모음에 등록 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-279">toosee hello servers registered toohello vault, and delete them:</span></span>

1. <span data-ttu-id="5a66e-280">자격 증명 모음 대시보드 열기 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-280">Open hello vault dashboard.</span></span>
2. <span data-ttu-id="5a66e-281">Hello에 **Essentials** 창에서 클릭 **설정을** tooopen 해당 블레이드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-281">In hello **Essentials** pane, click **Settings** tooopen that blade.</span></span>

    ![설정 블레이드 열기](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. <span data-ttu-id="5a66e-283">Hello에 **설정 블레이드에서**, 클릭 **백업 인프라**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-283">On hello **Settings blade**, click **Backup Infrastructure**.</span></span>
4. <span data-ttu-id="5a66e-284">Hello에 **백업 인프라** 블레이드에서 클릭 **백업 관리 서버를**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-284">On hello **Backup Infrastructure** blade, click **Backup Management Servers**.</span></span> <span data-ttu-id="5a66e-285">hello 백업 관리 서버를 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-285">hello Backup Management Servers blade opens.</span></span>

    ![백업 관리 서버 목록](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. <span data-ttu-id="5a66e-287">toodelete hello 목록에서 서버 hello hello 서버 이름을 마우스 오른쪽 단추로 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-287">toodelete a server from hello list, right-click hello name of hello server and then click **Delete**.</span></span>
    <span data-ttu-id="5a66e-288">hello **삭제** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-288">hello **Delete** blade opens.</span></span>
6. <span data-ttu-id="5a66e-289">Hello에 **삭제** 블레이드에서 hello hello 서버 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-289">On hello **Delete** blade, provide hello name of hello server.</span></span> <span data-ttu-id="5a66e-290">긴 이름인 경우 다음에 복사 및 hello 백업 관리 서버 목록에서 붙여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-290">If it is a long name, you can copy and paste it from hello list of Backup Management Servers.</span></span> <span data-ttu-id="5a66e-291">그런 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a66e-291">Then click **Delete**.</span></span>  
