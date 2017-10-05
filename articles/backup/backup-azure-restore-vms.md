---
title: "백업에서 가상 컴퓨터 복원 | Microsoft Docs"
description: "복구 지점에서 Azure 가상 컴퓨터를 복원하는 방법 알아보기"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "백업 복원; 복원하는 방법; 복구 지점;"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: fc52c909df5e91741ec1fa21fb911487be039fdc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-virtual-machines-in-azure"></a><span data-ttu-id="f66d3-104">Azure의 가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-104">Restore virtual machines in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f66d3-105">Azure 포털에서 VM 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-105">Restore VMs in Azure portal</span></span>](backup-azure-arm-restore-vms.md)
> * [<span data-ttu-id="f66d3-106">클래식 포털에서 VM 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-106">Restore VMs in Classic portal</span></span>](backup-azure-restore-vms.md)
>
>

<span data-ttu-id="f66d3-107">다음 단계를 사용하여 Azure Backup 자격 증명에 저장된 백업에서 새 VM에 가상 컴퓨터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-107">Restore a virtual machine to a new VM from the backups stored in an Azure Backup vault with the following steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f66d3-108">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="f66d3-109">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f66d3-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f66d3-110">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="f66d3-111">**2017년 10월 15일**부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="f66d3-112">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="f66d3-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="f66d3-113">나머지 모든 Backup 자격 증명 모음은 자동으로 Recovery Services 자격 증명 모음으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="f66d3-114">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="f66d3-115">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="restore-workflow"></a><span data-ttu-id="f66d3-116">워크플로 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-116">Restore workflow</span></span>
### <a name="step-1-choose-an-item-to-restore"></a><span data-ttu-id="f66d3-117">1단계: 복원할 항목 선택</span><span class="sxs-lookup"><span data-stu-id="f66d3-117">Step 1: Choose an item to restore</span></span>
1. <span data-ttu-id="f66d3-118">**보호된 항목** 탭으로 이동하고 새 VM에 복원할 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-118">Navigate to the **Protected Items** tab and select the virtual machine you want to restore to a new VM.</span></span>

    ![보호된 항목](./media/backup-azure-restore-vms/protected-items.png)

    <span data-ttu-id="f66d3-120">**보호된 항목** 페이지의 **복구 지점** 열에는 가상 컴퓨터의 복구 지점 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-120">The **Recovery Point** column in the **Protected Items** page will tell you the number of recovery points for a virtual machine.</span></span> <span data-ttu-id="f66d3-121">**가장 새로운 복구 지점** 열은 가상 컴퓨터를 복원할 수 있는 가장 최근의 백업 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-121">The **Newest Recovery Point** column tells you the time of the most recent backup from which a virtual machine can be restored.</span></span>
2. <span data-ttu-id="f66d3-122">**복원**을 클릭하여 **항목 복원** 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-122">Click **Restore** to open the **Restore an Item** wizard.</span></span>

    ![항목 복원](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a><span data-ttu-id="f66d3-124">2단계: 복구 지점 선택</span><span class="sxs-lookup"><span data-stu-id="f66d3-124">Step 2: Pick a recovery point</span></span>
1. <span data-ttu-id="f66d3-125">**복구 지점 선택** 화면에서 최신 복구 지점 또는 이전 시점을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-125">In the **select a recovery point** screen, you can restore from the newest recovery point, or from a previous point in time.</span></span> <span data-ttu-id="f66d3-126">마법사가 열릴 때 선택되는 기본 옵션은 *가장 새로운 복구 지점*입니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-126">The default option selected when wizard opens is *Newest Recovery Point*.</span></span>

    ![복구 지점 선택](./media/backup-azure-restore-vms/select-recovery-point.png)
2. <span data-ttu-id="f66d3-128">이전 시점을 선택하려면 드롭다운에서 **날짜 선택** 옵션을 선택하고 **달력 아이콘**을 클릭하여 달력 컨트롤에서 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-128">To pick an earlier point in time, choose the **Select Date** option in the dropdown and select a date in the calendar control by clicking on the **calendar icon**.</span></span> <span data-ttu-id="f66d3-129">컨트롤에서 복구 지점이 있는 모든 날짜는 밝은 회색 음영으로 채워져 있으며 사용자가 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-129">In the control, all dates that have recovery points are filled with a light gray shade and are selectable by the user.</span></span>

    ![날짜 선택](./media/backup-azure-restore-vms/select-date.png)

    <span data-ttu-id="f66d3-131">달력 컨트롤에서 날짜를 클릭하면 해당 날짜에 사용 가능한 복구 지점이 아래의 복구 지점 표에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-131">Once you click a date in the calendar control, the recovery points available on that date will be shown in recovery points table below.</span></span> <span data-ttu-id="f66d3-132">**시간** 열은 스냅숏이 만들어진 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-132">The **Time** column indicates the time at which the snapshot was taken.</span></span> <span data-ttu-id="f66d3-133">**유형** 열은 복구 지점의 [일관성](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) 을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-133">The **Type** column displays the [consistency](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) of the recovery point.</span></span> <span data-ttu-id="f66d3-134">테이블 머리글의 괄호 안에는 해당 날짜에 사용할 수 있는 복구 지점의 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-134">The table header shows the number of recovery points available on that day in parentheses.</span></span>

    ![복구 지점](./media/backup-azure-restore-vms/recovery-points.png)
3. <span data-ttu-id="f66d3-136">**복구 지점** 표에서 복구 지점을 선택하고 다음 화살표를 클릭하여 다음 화면으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-136">Select the recovery point from the **Recovery Points** table and click the Next arrow to go to the next screen.</span></span>

### <a name="step-3-specify-a-destination-location"></a><span data-ttu-id="f66d3-137">3단계: 대상 위치 지정</span><span class="sxs-lookup"><span data-stu-id="f66d3-137">Step 3: Specify a destination location</span></span>
1. <span data-ttu-id="f66d3-138">**복원 인스턴스 선택** 화면에서 가상 컴퓨터를 복원할 위치에 대한 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-138">In the **Select restore instance** screen specify details of where to restore the virtual machine.</span></span>

   * <span data-ttu-id="f66d3-139">가상 컴퓨터 이름 지정: 가상 컴퓨터 이름은 주어진 클라우드 서비스 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-139">Specify the virtual machine name: In a given cloud service, the virtual machine name should be unique.</span></span> <span data-ttu-id="f66d3-140">기본 VM 덮어쓰기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-140">We don't support over-writing existing VM.</span></span>
   * <span data-ttu-id="f66d3-141">VM에 대한 클라우드 서비스 선택: VM을 만들기 위한 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-141">Select a cloud service for the VM: This is mandatory for creating a VM.</span></span> <span data-ttu-id="f66d3-142">기존 클라우드 서비스를 사용하거나 새 클라우드 서비스 만들기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-142">You can choose to either use an existing cloud service or create a new cloud service.</span></span>

        <span data-ttu-id="f66d3-143">선택한 클라우드 서비스 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-143">Whatever cloud service name is picked should be globally unique.</span></span> <span data-ttu-id="f66d3-144">일반적으로 클라우드 서비스 이름은 [cloudservice].cloudapp.net 형식으로 공용 URL과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-144">Typically, the cloud service name gets associated with a public-facing URL in the form of [cloudservice].cloudapp.net.</span></span> <span data-ttu-id="f66d3-145">Azure에서는 이름이 이미 사용된 경우 새 클라우드 서비스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-145">Azure will not allow you to create a new cloud service if the name has already been used.</span></span> <span data-ttu-id="f66d3-146">새 클라우드 서비스를 만들려는 경우 가상 컴퓨터와 동일한 이름이 지정됩니다. 이 경우 VM 이름은 연결된 클라우드 서비스에 적용할 수 있을 정도로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-146">If you choose to create a new cloud service, it will be given the same name as the virtual machine – in which case the VM name picked should be unique enough to be applied to the associated cloud service.</span></span>

        <span data-ttu-id="f66d3-147">선호도 그룹과 연결되지 않은 클라우드 서비스 및 가상 네트워크만 복원 인스턴스 세부 정보에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-147">We only display cloud services and virtual networks that are not associated with any affinity groups in the restore instance details.</span></span> <span data-ttu-id="f66d3-148">[자세한 정보](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="f66d3-148">[Learn More](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
2. <span data-ttu-id="f66d3-149">VM에 대한 저장소 계정 선택: VM을 만들기 위한 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-149">Select a storage account for the VM: This is mandatory for creating the VM.</span></span> <span data-ttu-id="f66d3-150">Azure 백업 자격 증명 모음과 동일한 지역에 있는 기존 저장소 계정 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-150">You can select from existing storage accounts in the same region as the Azure Backup vault.</span></span> <span data-ttu-id="f66d3-151">영역 중복 또는 프리미엄 저장소 형식의 저장소 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-151">We don’t support storage accounts that are Zone redundant or of Premium storage type.</span></span>

    <span data-ttu-id="f66d3-152">지원되는 구성의 저장소 계정이 없는 경우 복원 작업을 시작하기 전에 지원되는 구성의 저장소 계정을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="f66d3-152">If there are no storage accounts with supported configuration, please create a storage account of supported configuration prior to starting restore operation.</span></span>

    ![가상 네트워크 선택](./media/backup-azure-restore-vms/restore-sa.png)
3. <span data-ttu-id="f66d3-154">가상 네트워크 선택: VM을 만들 때 가상 컴퓨터의 가상 네트워크(VNET)를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-154">Select a Virtual Network: The virtual network (VNET) for the virtual machine should be selected at the time of creating the VM.</span></span> <span data-ttu-id="f66d3-155">복원 UI는 이 구독 내에서 사용할 수 있는 모든 VNET을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-155">The restore UI shows all the VNETs within this subscription that can be used.</span></span> <span data-ttu-id="f66d3-156">복원된 VM의 VNET을 선택하는 것은 필수가 아닙니다. VNET을 적용하지 않더라도 인터넷을 통해 복원된 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-156">It is not mandatory to select a VNET for the restored VM – you will be able to connect to the restored virtual machine over the internet even if the VNET is not applied.</span></span>

    <span data-ttu-id="f66d3-157">선택한 클라우드 서비스가 가상 네트워크와 연결 되면 가상 네트워크를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-157">If the cloud service selected is associated with a virtual network, then you cannot change the virtual network.</span></span>

    ![가상 네트워크 선택](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. <span data-ttu-id="f66d3-159">서브넷 선택: VNET에 서브넷이 있는 경우 기본적으로 첫 번째 서브넷이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-159">Select a subnet: In case the VNET has subnets, by default the first subnet will be selected.</span></span> <span data-ttu-id="f66d3-160">드롭다운 옵션 중에서 원하는 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-160">Choose the subnet of your choice from the dropdown options.</span></span> <span data-ttu-id="f66d3-161">서브넷 세부 정보를 보려면 [포털 홈페이지](https://manage.windowsazure.com/)의 네트워크 확장, **가상 네트워크** 로 차례로 이동한 다음 가상 네트워크를 선택하고 구성으로 드릴다운하여 서브넷 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-161">For subnet details, go to Networks extension in the [portal home page](https://manage.windowsazure.com/), go to **Virtual Networks** and select the virtual network and drill down into Configure to see subnet details.</span></span>

    ![서브넷 선택](./media/backup-azure-restore-vms/select-subnet.png)
5. <span data-ttu-id="f66d3-163">마법사에서 **제출** 아이콘을 클릭하여 세부 정보를 제출하고 복원 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-163">Click the **Submit** icon in the wizard to submit the details and create a restore job.</span></span>

## <a name="track-the-restore-operation"></a><span data-ttu-id="f66d3-164">복원 작업 추적</span><span class="sxs-lookup"><span data-stu-id="f66d3-164">Track the Restore operation</span></span>
<span data-ttu-id="f66d3-165">복원 마법사에 모든 정보를 입력하고 제출하면 Azure 백업이 복원 작업을 추적하는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-165">Once you have input all the information into the restore wizard and submitted it Azure Backup will try to create a job to track the restore operation.</span></span>

![복원 작업 생성 중](./media/backup-azure-restore-vms/create-restore-job.png)

<span data-ttu-id="f66d3-167">작업 만들기에 성공하면 작업이 만들어졌음을 알리는 알림 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-167">If the job creation is successful, you will see a toast notification indicating that the job is created.</span></span> <span data-ttu-id="f66d3-168">**작업 보기** 단추를 클릭하면 **작업** 탭으로 이동하여 더 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-168">You can get more details by clicking the **View Job** button that will take you to **Jobs** tab.</span></span>

![복원 작업이 생성됨](./media/backup-azure-restore-vms/restore-job-created.png)

<span data-ttu-id="f66d3-170">복원 작업이 완료되면 **작업** 탭에 완료된 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-170">Once the restore operation is finished, it will be marked as completed in **Jobs** tab.</span></span>

![복원 작업 완료](./media/backup-azure-restore-vms/restore-job-complete.png)

<span data-ttu-id="f66d3-172">가상 컴퓨터를 복원한 후 원래 VM에 있던 확장을 다시 설치하고 Azure 포털에서 가상 컴퓨터에 대한 [끝점을 수정](../virtual-machines/windows/classic/setup-endpoints.md) 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-172">After restoring the virtual machine you may need to re-install the extensions existing on the original VM and [modify the endpoints](../virtual-machines/windows/classic/setup-endpoints.md) for the virtual machine in the Azure portal.</span></span>

## <a name="post-restore-steps"></a><span data-ttu-id="f66d3-173">복원 후 단계</span><span class="sxs-lookup"><span data-stu-id="f66d3-173">Post-Restore steps</span></span>
<span data-ttu-id="f66d3-174">Ubuntu와 같은 클라우드 초기화 기반 Linux 배포를 사용하는 경우 보안상의 이유로 복원 후 암호를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-174">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password will be blocked post restore.</span></span> <span data-ttu-id="f66d3-175">복원된 VM에서 VMAccess 확장을 사용하여 [암호를 재설정](../virtual-machines/linux/classic/reset-access.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="f66d3-175">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span></span> <span data-ttu-id="f66d3-176">복원 후 암호를 다시 설정하지 않으려면 이러한 배포에서 SSH 키를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-176">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span></span>

## <a name="backup-for-restored-vms"></a><span data-ttu-id="f66d3-177">복원된 VM에 대한 백업</span><span class="sxs-lookup"><span data-stu-id="f66d3-177">Backup for Restored VMs</span></span>
<span data-ttu-id="f66d3-178">원래 백업한 VM과 같은 이름으로 같은 클라우드 서비스에 VM을 복원하면, 백업이 VM 사후 복원에 계속 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-178">If you have restored VM to same cloud service with the same name as originally backed up VM, backup will continue on the VM post restore.</span></span> <span data-ttu-id="f66d3-179">VM을 다른 클라우드 서비스에 복원하거나, 복원된 VM에 다른 이름을 지정하면, 새 VM으로 간주되어 복원된 VM에 대한 백업을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-179">If you have either restored VM to a different cloud service or specified a different name for restored VM, this will be treated as a new VM and you need to setup backup for restored VM.</span></span>

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a><span data-ttu-id="f66d3-180">Azure 데이터 센터 재해 중 VM 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-180">Restoring a VM during Azure DataCenter Disaster</span></span>
<span data-ttu-id="f66d3-181">백업 자격 증명 모음을 지리적으로 중복되도록 구성해 놓은 경우, VM이 실행되는 기본 데이터 센터에 재해가 발생하면, Azure 백업을 통해 쌍을 이루는 데이터 센터에 백업한 VM을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-181">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span></span> <span data-ttu-id="f66d3-182">이러한 시나리오가 발생하면, 쌍을 이루는 데이터 센터에 존재하는 저장소 계정을 선택해야 하며 나머지 복원 프로세스는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-182">During such scenarios, you need to select a storage account which is present in paired data center and rest of the restore process remains same.</span></span> <span data-ttu-id="f66d3-183">Azure 백업은 쌍을 이루는 지역의 계산 서비스를 사용하여 복원된 가상 컴퓨터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-183">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span></span> <span data-ttu-id="f66d3-184">[Azure 데이터 센터 복원력](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f66d3-184">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span></span>

## <a name="restoring-domain-controller-vms"></a><span data-ttu-id="f66d3-185">도메인 컨트롤러 VM 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-185">Restoring Domain Controller VMs</span></span>
<span data-ttu-id="f66d3-186">DC(도메인 컨트롤러) 가상 컴퓨터 백업은 Azure 백업을 사용하는 지원되는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-186">Backup of Domain Controller (DC) virtual machines is a supported scenario with Azure Backup.</span></span> <span data-ttu-id="f66d3-187">그러나 복원 프로세스 동안 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-187">However, care must be taken during the restore process.</span></span> <span data-ttu-id="f66d3-188">올바른 복원 프로세스는 도메인의 구조에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-188">The correct restore process depends on the structure of the domain.</span></span> <span data-ttu-id="f66d3-189">단순한 경우에 단일 도메인에 단일 DC가 있기도 하지만,</span><span class="sxs-lookup"><span data-stu-id="f66d3-189">In the simplest case you have a single DC in a single domain.</span></span> <span data-ttu-id="f66d3-190">일반적으로 프로덕션 로드에서는 단일 도메인에 여러 DC가 있고, 일부 DC는 온-프레미스에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-190">More commonly for production loads, you will have a single domain with multiple DCs, perhaps with some DCs on premises.</span></span> <span data-ttu-id="f66d3-191">여러 도메인이 있는 포리스트도 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-191">Finally, you may have a forest with multiple domains.</span></span>

<span data-ttu-id="f66d3-192">Active Directory 관점에서 Azure VM은 지원되는 최신 하이퍼바이저의 다른 VM과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-192">From an Active Directory perspective the Azure VM is like any other VM on a modern supported hypervisor.</span></span> <span data-ttu-id="f66d3-193">온-프레미스 하이퍼바이저와의 주된 차이점은 Azure에서는 사용할 수 없는 VM 콘솔이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-193">The major difference with on-premises hypervisors is that there is no VM console available in Azure.</span></span> <span data-ttu-id="f66d3-194">BMR(완전 복구) 유형 백업을 사용한 복구와 같은 특정 시나리오에서는 콘솔이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-194">A console is required for certain scenarios such as recovering using a Bare Metal Recovery (BMR) type backup.</span></span> <span data-ttu-id="f66d3-195">하지만 백업 자격 증명 모음의 VM 복원이 BMR을 완전히 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-195">However, VM restore from the backup vault is a full replacement for BMR.</span></span> <span data-ttu-id="f66d3-196">Active Directory 복원 모드(DSRM)도 사용할 수 있으므로 모든 Active Directory 복구 모드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-196">Active Directory Restore Mode (DSRM) is also available, so all Active Directory recovery scenarios are viable.</span></span> <span data-ttu-id="f66d3-197">자세한 배경 정보는 [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)(가상화된 도메인 컨트롤러에 대한 백업 및 복원 고려 사항) 및 [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)(Active Directory 포리스트 복구 계획)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f66d3-197">For more background information, please check [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) and [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).</span></span>

### <a name="single-dc-in-a-single-domain"></a><span data-ttu-id="f66d3-198">단일 도메인의 단일 DC</span><span class="sxs-lookup"><span data-stu-id="f66d3-198">Single DC in a single domain</span></span>
<span data-ttu-id="f66d3-199">Azure 포털에서 또는 PowerShell을 사용하여 다른 VM과 마찬가지로 VM을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-199">The VM can be restored (like any other VM) from the Azure portal or using PowerShell.</span></span>

### <a name="multiple-dcs-in-a-single-domain"></a><span data-ttu-id="f66d3-200">단일 도메인의 여러 DC</span><span class="sxs-lookup"><span data-stu-id="f66d3-200">Multiple DCs in a single domain</span></span>
<span data-ttu-id="f66d3-201">네트워크를 통해 동일한 도메인의 다른 DC에 연결할 수 있는 경우 DC를 VM처럼 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-201">When other DCs of the same domain can be reached over the network, the DC can be restored like any VM.</span></span> <span data-ttu-id="f66d3-202">도메인에 남은 마지막 DC이거나 격리된 네트워크에서 복구를 수행하는 경우에는 포리스트 복구 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-202">If it is the last remaining DC in the domain, or a recovery in an isolated network is performed, a forest recovery procedure must be followed.</span></span>

### <a name="multiple-domains-in-one-forest"></a><span data-ttu-id="f66d3-203">한 포리스트의 여러 도메인</span><span class="sxs-lookup"><span data-stu-id="f66d3-203">Multiple domains in one forest</span></span>
<span data-ttu-id="f66d3-204">네트워크를 통해 동일한 도메인의 다른 DC에 연결할 수 있는 경우 DC를 VM처럼 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-204">When other DCs of the same domain can be reached over the network, the DC can be restored like any VM.</span></span> <span data-ttu-id="f66d3-205">그러나 다른 모든 경우에 포리스트 복구를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-205">However, in all other cases a forest recovery is recommended.</span></span>

<!--- WK: this following original supportability statement is incorrect, taking it out.
The challenge arises because DSRM mode is not present in Azure. So to restore such a VM, you cannot use the Azure portal. The only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use the Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about the [USN rollback problem](https://technet.microsoft.com/library/dd363553) and the strategies suggested to fix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a><span data-ttu-id="f66d3-206">특수 네트워크 구성을 가진 Vm 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-206">Restoring VMs with special network configurations</span></span>
<span data-ttu-id="f66d3-207">Azure 백업은 다음 가상 컴퓨터의 특수 네트워크 구성에 대한 백업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-207">Azure Backup supports backup for following special network configurations of virtual machines.</span></span>

* <span data-ttu-id="f66d3-208">부하 분산 장치에서의 VM(내부 및 외부)</span><span class="sxs-lookup"><span data-stu-id="f66d3-208">VMs under load balancer (internal and external)</span></span>
* <span data-ttu-id="f66d3-209">다중의 예약된 IP가 있는 VM</span><span class="sxs-lookup"><span data-stu-id="f66d3-209">VMs with multiple reserved IPs</span></span>
* <span data-ttu-id="f66d3-210">다중 NIC가 있는 VM</span><span class="sxs-lookup"><span data-stu-id="f66d3-210">VMs with multiple NICs</span></span>

<span data-ttu-id="f66d3-211">이러한 구성은 복원 중 다음의 고려 사항을 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-211">These configurations mandate following considerations while restoring them.</span></span>

> [!TIP]
> <span data-ttu-id="f66d3-212">VM 사후 복원의 특수 네트워크 구성을 다시 만들려면 PowerShell 기반 복원 흐름을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="f66d3-212">Please use PowerShell based restore flow to recreate the special network configuration of VMs post restore.</span></span>
>
>

### <a name="restoring-from-the-ui"></a><span data-ttu-id="f66d3-213">UI에서 복원:</span><span class="sxs-lookup"><span data-stu-id="f66d3-213">Restoring from the UI:</span></span>
<span data-ttu-id="f66d3-214">UI에서 복원하는 동안 **항상 새 클라우드 서비스를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-214">While restoring from UI, **always choose a new cloud service**.</span></span> <span data-ttu-id="f66d3-215">포털은 복원 흐름 동안 필수 매개 변수만 사용하므로 UI를 사용하여 복원된 VM이 보유하고 있는 특수 네트워크 구성을 손실할 수 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="f66d3-215">Please note that since portal only takes mandatory parameters during restore flow, VMs restored using UI will lose the special network configuration they possess.</span></span> <span data-ttu-id="f66d3-216">즉, 복원 VM은 부하 분산 장치 또는 다중 NIC 또는 다중 예약된 IP의 구성이 없는 기본 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-216">In other words, restore VMs will be normal VMs without configuration of load balancer or multi NIC or multiple reserved IP.</span></span>

### <a name="restoring-from-powershell"></a><span data-ttu-id="f66d3-217">PowerShell에서 복원:</span><span class="sxs-lookup"><span data-stu-id="f66d3-217">Restoring from PowerShell:</span></span>
<span data-ttu-id="f66d3-218">PowerShell은 백업에서 VM 디스크만 복원하고 가상 컴퓨터를 만들지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-218">PowerShell has the ability to just restore the VM disks from backup and not create the virtual machine.</span></span> <span data-ttu-id="f66d3-219">이는 앞에서 언급된 특수 네트워크 구성을 요구하는 가상 컴퓨터를 복원하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-219">This is helpful when restoring virtual machines which require special network configurations mentioned above.</span></span>

<span data-ttu-id="f66d3-220">가상 컴퓨터 사후 복원 디스크를 완전히 다시 만들려면 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f66d3-220">In order to fully recreate the virtual machine post restoring disks, follow these steps:</span></span>

1. <span data-ttu-id="f66d3-221">[Azure 백업 PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)을 사용하여 백업 자격 증명 모음에서 디스크 복원</span><span class="sxs-lookup"><span data-stu-id="f66d3-221">Restore the disks from backup vault using [Azure Backup PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span></span>
2. <span data-ttu-id="f66d3-222">PowerShell cmdlet을 사용하여 부하 분산 장치/다중 NIC/다중의 예약된 IP에 필요한 VM 구성을 만들어 원하는 구성의 VM을 만드는데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-222">Create the VM config required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span></span>

   * <span data-ttu-id="f66d3-223">[내부 부하 분산 장치 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="f66d3-223">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span></span>
   * <span data-ttu-id="f66d3-224">[인터넷 연결 부하 분산 장치](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)에 연결하기 위한 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f66d3-224">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span></span>
   * <span data-ttu-id="f66d3-225">[다중 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span><span class="sxs-lookup"><span data-stu-id="f66d3-225">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span></span>
   * <span data-ttu-id="f66d3-226">[다중의 예약된 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span><span class="sxs-lookup"><span data-stu-id="f66d3-226">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66d3-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f66d3-227">Next steps</span></span>
* [<span data-ttu-id="f66d3-228">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f66d3-228">Troubleshooting errors</span></span>](backup-azure-vms-troubleshoot.md#restore)
* [<span data-ttu-id="f66d3-229">가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="f66d3-229">Manage virtual machines</span></span>](backup-azure-manage-vms.md)
