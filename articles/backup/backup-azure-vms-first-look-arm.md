---
title: "소개: Recovery Services 자격 증명 모음으로 Azure VM 보호 | Microsoft 문서"
description: "복구 서비스 자격 증명 모음으로 Azure VM 보호. 리소스 관리자를 통해 배포 된 Vm, Vm 클래식 배포 및 프리미엄 저장소 Vm, Vm 암호화 tooprotect 관리 하는 디스크에 있는 Vm의 백업 데이터를 사용 합니다. 복구 서비스 자격 증명 모음을 만들고 등록합니다. Azure에서 VM을 등록하고 정책을 만들며 VM을 보호합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a><span data-ttu-id="b13ce-106">Azure 가상 컴퓨터 tooRecovery 서비스 자격 증명 모음에 백업</span><span class="sxs-lookup"><span data-stu-id="b13ce-106">Back up Azure virtual machines tooRecovery Services vaults</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b13ce-107">복구 서비스 자격 증명 모음으로 VM 보호</span><span class="sxs-lookup"><span data-stu-id="b13ce-107">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="b13ce-108">백업 자격 증명으로 VM 보호</span><span class="sxs-lookup"><span data-stu-id="b13ce-108">Protect VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="b13ce-109">이 자습서에서는 복구 서비스 자격 증명 모음을 만들고 Azure 가상 컴퓨터 (VM)를 백업 하기 위한 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-109">This tutorial takes you through hello steps for creating a recovery services vault and backing up an Azure virtual machine (VM).</span></span> <span data-ttu-id="b13ce-110">복구 서비스 자격 증명 모음이 보호하는 항목:</span><span class="sxs-lookup"><span data-stu-id="b13ce-110">Recovery services vaults protect:</span></span>

* <span data-ttu-id="b13ce-111">Azure Resource Manager 배포 VM</span><span class="sxs-lookup"><span data-stu-id="b13ce-111">Azure Resource Manager-deployed VMs</span></span>
* <span data-ttu-id="b13ce-112">클래식 VM</span><span class="sxs-lookup"><span data-stu-id="b13ce-112">Classic VMs</span></span>
* <span data-ttu-id="b13ce-113">표준 저장소 VM</span><span class="sxs-lookup"><span data-stu-id="b13ce-113">Standard storage VMs</span></span>
* <span data-ttu-id="b13ce-114">프리미엄 저장소 VM</span><span class="sxs-lookup"><span data-stu-id="b13ce-114">Premium storage VMs</span></span>
* <span data-ttu-id="b13ce-115">Managed Disks에서 실행 중인 VM</span><span class="sxs-lookup"><span data-stu-id="b13ce-115">VMs running on Managed Disks</span></span>
* <span data-ttu-id="b13ce-116">Azure Disk Encryption와 BEK 및 KEK를 사용하여 암호화된 VM</span><span class="sxs-lookup"><span data-stu-id="b13ce-116">VMs encrypted using Azure Disk Encryption, with BEK and KEK</span></span>
* <span data-ttu-id="b13ce-117">사용자 지정 사전 스냅숏 및 사후 스냅숏 스크립트를 사용하는 VSS 및 Linux VM을 사용하여 Windows VM의 응용 프로그램 일치 백업</span><span class="sxs-lookup"><span data-stu-id="b13ce-117">Application consistent backup of Windows VMs using VSS and Linux VMs using custom pre-snapshot and post-snapshot scripts</span></span>

<span data-ttu-id="b13ce-118">프리미엄 저장소 Vm 보호에 대 한 자세한 내용은 hello 문서 참조 [백업 및 복원 프리미엄 저장소 Vm](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-118">For more information on protecting Premium storage VMs, see hello article, [Back up and Restore Premium Storage VMs](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup).</span></span> <span data-ttu-id="b13ce-119">Managed Disks VM 지원에 대한 자세한 내용은 [Managed Disks의 VM 백업 및 복원](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b13ce-119">For more information on support for managed disk VMs, see [Back up and restore VMs on managed disks](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).</span></span> <span data-ttu-id="b13ce-120">Linux VM을 백업하기 위한 사전 및 사후 스크립트 프레임워크에 대한 자세한 내용은 [사전 및 사후 스크립트를 사용하여 응용 프로그램 일치 Linux VM 백업](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b13ce-120">For more information on pre and post-script framework for Linux VM backup see [Application consistent Linux VM backup using pre-script and post-script] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span>

<span data-ttu-id="b13ce-121">더에 대 한 백업 있습니다 수 및 없습니다, toofind 참조 [여기](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span><span class="sxs-lookup"><span data-stu-id="b13ce-121">toofind out more about what can you backup and what you can't, refer [here](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span></span>

> [!NOTE]
> <span data-ttu-id="b13ce-122">이 자습서를 수행 하 여 측정값 tooallow hello 백업 서비스 tooaccess hello VM 및 Azure 구독에서 이미 VM이 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-122">This tutorial assumes you already have a VM in your Azure subscription and that you have taken measures tooallow hello backup service tooaccess hello VM.</span></span>
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="b13ce-123">가상 컴퓨터의 hello 수에 따라 tooprotect 5d; 여러 시작 지점에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-123">Depending on hello number of virtual machines you want tooprotect, you can begin from different starting points.</span></span> <span data-ttu-id="b13ce-124">한 번에 여러 가상 컴퓨터를 tooback 원한다 면 이동 toohello 복구 서비스 자격 증명 모음 및 [hello 자격 증명 모음 대시보드에서 백업 작업 시작 hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-124">If you want tooback up multiple virtual machines in one operation, go toohello Recovery Services vault and [initiate hello backup job from hello vault dashboard](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault).</span></span> <span data-ttu-id="b13ce-125">단일 가상 컴퓨터를 tooback 원한다 면 hello VM 관리 블레이드에서 백업 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-125">If you want tooback up a single virtual machine, you can initiate hello backup job from VM management blade.</span></span>

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a><span data-ttu-id="b13ce-126">Hello hello VM 관리 블레이드에서 백업 작업 구성</span><span class="sxs-lookup"><span data-stu-id="b13ce-126">Configure hello backup job from hello VM management blade</span></span>

<span data-ttu-id="b13ce-127">Hello Azure 포털에서에서 가상 컴퓨터 관리 블레이드 hello에서에서 단계 tooconfigure hello에 대 한 백업 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-127">Use hello following steps tooconfigure hello backup job from hello virtual machine management blade in hello Azure portal.</span></span> <span data-ttu-id="b13ce-128">이러한 단계는 hello 클래식 포털에서 가상 컴퓨터 toohello 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-128">These steps do not apply toohello virtual machines in hello classic portal.</span></span>

1. <span data-ttu-id="b13ce-129">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-129">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b13ce-130">Hello 허브 메뉴에서 클릭 **더 서비스** hello 필터 대화 상자에서 입력 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-130">On hello Hub menu, click **More Services** and in hello Filter dialog, type **Virtual machines**.</span></span> <span data-ttu-id="b13ce-131">입력 하는 동안 리소스의 hello 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-131">As you type, hello list of resources filters.</span></span> <span data-ttu-id="b13ce-132">가상 컴퓨터가 표시되면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-132">When you see Virtual machines, select it.</span></span>

  ![허브 메뉴에서 서비스 보다 tooopen 텍스트 대화 상자에서를 클릭 하 고 가상 컴퓨터를 입력 합니다.](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  <span data-ttu-id="b13ce-134">hello 구독에서 가상 컴퓨터 (VM) hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-134">hello list of virtual machines (VM) in hello subscription, appears.</span></span>

  ![hello 구독에서 Vm의 hello 목록이 나타납니다.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. <span data-ttu-id="b13ce-136">Hello 목록에서 VM tooback를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-136">From hello list, select a VM tooback up.</span></span>

  ![hello 구독에서 Vm의 hello 목록이 나타납니다.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  <span data-ttu-id="b13ce-138">Hello VM을 선택 하면 가상 컴퓨터의 목록을 hello 프로비저닝으로 전환 toohello 왼쪽 및 hello 가상 컴퓨터 관리 블레이드 hello 가상 컴퓨터 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-138">When you select hello VM, hello list of virtual machines shifts toohello left, and hello virtual machine management blade and hello virtual machine dashboard, open.</span></span> </br><span data-ttu-id="b13ce-139">
 ![VM 관리 블레이드](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)</span><span class="sxs-lookup"><span data-stu-id="b13ce-139">
![VM Management blade](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)</span></span>

4. <span data-ttu-id="b13ce-140">Hello VM 관리 블레이드의 hello **설정** 섹션에서 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-140">On hello VM management blade, in hello **Settings** section, click **Backup**.</span></span> </br>

  ![VM 관리 블레이드의 백업 옵션](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  <span data-ttu-id="b13ce-142">hello 사용 백업 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-142">hello Enable backup blade opens.</span></span>

  ![VM 관리 블레이드의 백업 옵션](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. <span data-ttu-id="b13ce-144">Hello 복구 서비스 자격 증명 모음에 대 한 클릭 **기존 선택** hello 드롭 다운 목록에서 hello 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-144">For hello Recovery Services vault, click **Select existing** and choose hello vault from hello drop-down list.</span></span>

  ![백업 마법사 사용](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  <span data-ttu-id="b13ce-146">복구 서비스 자격 증명 모음는 않거나 toouse 새 자격 증명 모음을 클릭 하 여 **새로 만들기** hello hello 새 자격 증명 모음 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-146">If there are no Recovery Services vaults, or you want toouse a new vault, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="b13ce-147">새 자격 증명 모음에서에서 만든 hello 동일한 리소스 그룹 및 hello 가상 컴퓨터와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-147">A new vault is created in hello same Resource Group and same location as hello virtual machine.</span></span> <span data-ttu-id="b13ce-148">Toocreate 값이 서로 다른 복구 서비스 자격 증명 모음을 사용 하도록 하려는 경우 hello에 섹션을 참조 방법을 너무[복구 서비스 자격 증명 모음 만들기](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-148">If you want toocreate a Recovery Services vault with different values, see hello section on how too[create a recovery services vault](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).</span></span>

6. <span data-ttu-id="b13ce-149">백업 정책 hello의 tooview hello 세부 정보 클릭 **백업 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-149">tooview hello details of hello Backup policy, click **Backup policy**.</span></span>

  <span data-ttu-id="b13ce-150">hello **백업 정책** 블레이드가 열리고 선택한 hello 정책 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-150">hello **Backup policy** blade opens and provides hello details of hello selected policy.</span></span> <span data-ttu-id="b13ce-151">다른 정책이 있는 경우에 hello 드롭 다운 메뉴 toochoose 다른 백업 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-151">If other policies exist, use hello drop-down menu toochoose a different backup policy.</span></span> <span data-ttu-id="b13ce-152">Toocreate 정책을 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-152">If you want toocreate a policy, select **Create New** from hello drop-down menu.</span></span> <span data-ttu-id="b13ce-153">백업 정책 정의에 대한 지침은 [백업 정책 정의](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b13ce-153">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span></span> <span data-ttu-id="b13ce-154">toosave hello 변경 toohello 백업 정책 및 반환 toohello 사용 백업 블레이드 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-154">toosave hello changes toohello backup policy and return toohello Enable backup blade, click **OK**.</span></span>

  ![백업 정책 선택](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. <span data-ttu-id="b13ce-156">Hello 사용 백업 블레이드에서 클릭 **백업 사용** toodeploy hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-156">On hello Enable backup blade, click **Enable Backup** toodeploy hello policy.</span></span> <span data-ttu-id="b13ce-157">Hello 정책을 배포 하는 hello 자격 증명 모음 및 hello 가상 컴퓨터와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-157">Deploying hello policy associates it with hello vault and hello virtual machines.</span></span>

  ![백업 사용 단추](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. <span data-ttu-id="b13ce-159">Hello 포털에 표시 되는 hello 알림을 통해 hello 구성 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-159">You can track hello configuration progress through hello notifications that appear in hello portal.</span></span> <span data-ttu-id="b13ce-160">다음 예제는 hello 배포 시작 되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-160">hello following example shows that Deployment started.</span></span>

  ![백업 사용 알림](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. <span data-ttu-id="b13ce-162">Hello VM 관리 블레이드의 hello 구성 진행률 완료 되 면 클릭 **백업** tooopen hello 백업 항목 블레이드 뷰와 hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-162">Once hello configuration progress has completed, on hello VM management blade, click **Backup** tooopen hello Backup Item blade and view hello details.</span></span>

  ![VM 백업 항목 보기](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  <span data-ttu-id="b13ce-164">Hello 초기 백업을 완료 되기 전 까지는 **마지막 백업 상태** 표시 **경고 (초기 백업 보류 중인)**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-164">Until hello initial backup has completed, **Last backup status** shows as **Warning(Initial backup pending)**.</span></span> <span data-ttu-id="b13ce-165">toosee hello 다음 백업 작업을 예약 하는 경우 발생 **백업 정책** hello 정책 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-165">toosee when hello next scheduled backup job occurs, under **Backup policy** click hello name of hello policy.</span></span> <span data-ttu-id="b13ce-166">hello 백업 정책 블레이드에서 열리고 hello hello 예약 된 백업 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-166">hello Backup Policy blade opens and shows hello time of hello scheduled backup.</span></span>

10. <span data-ttu-id="b13ce-167">toorun 백업 작업 및 hello 초기 복구 지점 만들기, 백업 hello에 블레이드 클릭 자격 증명 모음에 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-167">toorun a Backup job and create hello initial recovery point, on hello Backup vault blade click **Backup now**.</span></span>

  ![백업 지금 toorun hello 초기 백업을 클릭합니다](./media/backup-azure-vms-first-look-arm/backup-now.png)

  <span data-ttu-id="b13ce-169">hello 지금 백업 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-169">hello Backup Now blade opens.</span></span>

  ![hello 지금 백업 블레이드를 표시합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. <span data-ttu-id="b13ce-171">Hello 지금 백업 블레이드의 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-171">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![hello 마지막 날 hello 지금 백업 복구 지점을 유지 되는 설정](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="b13ce-173">배포 알림 hello 백업 작업 트리거 되었으며 hello 작업 hello 백업 작업 페이지의 hello 진행률을 모니터링할 수 있습니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-173">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span>

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a><span data-ttu-id="b13ce-174">Hello hello 복구 서비스 자격 증명 모음에서 백업 작업 구성</span><span class="sxs-lookup"><span data-stu-id="b13ce-174">Configure hello backup job from hello Recovery Services vault</span></span>
<span data-ttu-id="b13ce-175">tooconfigure hello 백업 작업을 마친 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-175">tooconfigure hello backup job, you complete hello following steps.</span></span>  

1. <span data-ttu-id="b13ce-176">가상 컴퓨터에 대한 Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-176">Create a Recovery Services vault for a virtual machine.</span></span>
2. <span data-ttu-id="b13ce-177">사용 하 여 hello Azure 포털 tooselect 시나리오에서는 백업 정책을 설정 하 고 항목 tooprotect를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-177">Use hello Azure portal tooselect a Scenario, set a Backup policy, and identify items tooprotect.</span></span>
3. <span data-ttu-id="b13ce-178">Hello 초기 백업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-178">Run hello initial backup.</span></span>

## <a name="create-a-recovery-services-vault-for-a-vm"></a><span data-ttu-id="b13ce-179">VM에 대한 복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="b13ce-179">Create a recovery services vault for a VM</span></span>
<span data-ttu-id="b13ce-180">복구 서비스 자격 증명 모음에는 모든 hello 백업 및 시간에 따라 생성 된 복구 지점을 저장 하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-180">A Recovery Services vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="b13ce-181">hello 복구 서비스 자격 증명 모음도 포함 hello 백업 정책이 적용 toohello Vm을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-181">hello Recovery Services vault also contains hello backup policy applied toohello protected VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="b13ce-182">VM 백업은 로컬 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-182">Backing up VMs is a local process.</span></span> <span data-ttu-id="b13ce-183">다른 위치에 있는 한 위치 tooa 복구 서비스 자격 증명 모음에서 Vm 백업할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-183">You cannot back up VMs from one location tooa Recovery Services vault in another location.</span></span> <span data-ttu-id="b13ce-184">따라서 Vm toobe 백업에 있는 모든 Azure 위치에 대 한 해당 위치에 복구 서비스 자격 증명 모음을 하나 이상 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-184">So, for every Azure location that has VMs toobe backed up, at least one Recovery Services vault must exist in that location.</span></span>
>
>

<span data-ttu-id="b13ce-185">toocreate 복구 서비스 자격 증명 모음:</span><span class="sxs-lookup"><span data-stu-id="b13ce-185">toocreate a Recovery Services vault:</span></span>

1. <span data-ttu-id="b13ce-186">그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-186">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="b13ce-187">Hello 허브 메뉴에서 클릭 **더 많은 서비스** 및 필터 대화 상자 유형 hello **복구 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-187">On hello Hub menu, click **More services** and in hello Filter dialog type **Recovery Services**.</span></span> <span data-ttu-id="b13ce-188">입력 하는 동안 리소스의 hello 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-188">As you type, hello list of resources filters.</span></span> <span data-ttu-id="b13ce-189">복구 서비스 자격 증명 모음 hello 목록에 표시 되는 경우 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-189">When you see Recovery Services vaults in hello list, click it.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="b13ce-191">Hello 구독에서 복구 서비스 자격 증명 모음 인 경우 hello 자격 증명 모음 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-191">If there are Recovery Services vaults in hello subscription, hello vaults are listed.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. <span data-ttu-id="b13ce-193">Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-193">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="b13ce-195">hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-195">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Recovery Services 자격 증명 모음 만들기 3단계](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="b13ce-197">에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-197">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="b13ce-198">hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-198">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="b13ce-199">이름을 2~50자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-199">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="b13ce-200">문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-200">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="b13ce-201">Hello에 **구독** 섹션 hello 드롭 다운 메뉴 toochoose hello Azure 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-201">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="b13ce-202">단일 구독을 사용 하는 경우 해당 구독 표시 되 고 toohello 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-202">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="b13ce-203">어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-203">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="b13ce-204">조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-204">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="b13ce-205">Hello에 **리소스 그룹** 섹션:</span><span class="sxs-lookup"><span data-stu-id="b13ce-205">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="b13ce-206">선택 **새로 만들기** toocreate 리소스 그룹에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-206">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="b13ce-207">또는</span><span class="sxs-lookup"><span data-stu-id="b13ce-207">Or</span></span>
    * <span data-ttu-id="b13ce-208">선택 **기존 항목 사용** hello 드롭 다운 메뉴 toosee hello 사용 가능한 리소스 그룹의 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-208">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="b13ce-209">리소스 그룹에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-209">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="b13ce-210">클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-210">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="b13ce-211">여기에서이 선택한 hello 지리적 지역에 백업 데이터를 보내는 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-211">This choice determines hello geographic region where your backup data is sent.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b13ce-212">VM 존재 하는 hello 위치의 확실 하지 않은, hello 자격 증명 모음 만들기 대화 상자를 닫은 hello 포털에서 가상 컴퓨터의 toohello 목록을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-212">If you are unsure of hello location in which your VM exists, close out of hello vault creation dialog, and go toohello list of Virtual Machines in hello portal.</span></span> <span data-ttu-id="b13ce-213">가상 컴퓨터가 여러 지역에 있는 경우 각 지역에 Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-213">If you have virtual machines in multiple regions, create a Recovery Services vault in each region.</span></span> <span data-ttu-id="b13ce-214">Toohello 다음 위치를 진행 하기 전에 hello 첫 번째 위치에 hello 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-214">Create hello vault in hello first location before going toohello next location.</span></span> <span data-ttu-id="b13ce-215">Toostore hello 백업 데이터-hello 복구 서비스 자격 증명 모음을 사용 하는 필요성 toospecify hello 저장소 계정이 없습니다 않으며 hello Azure 백업 서비스는 hello 저장소를 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-215">There is no need toospecify hello storage accounts used toostore hello backup data--hello Recovery Services vault and hello Azure Backup service automatically handle hello storage.</span></span>
  >

8. <span data-ttu-id="b13ce-216">Hello 복구 서비스 자격 증명 모음 블레이드의 hello 아래쪽 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-216">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="b13ce-217">복구 서비스 자격 증명 모음에 만든 toobe hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-217">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="b13ce-218">Hello 포털의 상단 오른쪽 영역 hello에서에서 hello 상태 알림을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-218">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="b13ce-219">자격 증명 모음을 만든 후의 복구 서비스 자격 증명 모음 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-219">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="b13ce-220">몇 분이 지나도 자격 증명 모음이 보이지 않으면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-220">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![새로 고침 단추 클릭](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="b13ce-222">자격 증명 모음 자격 증명 모음은 복구 서비스의 hello 목록에 표시 되는 경우 준비 tooset hello 저장소 중복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-222">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

<span data-ttu-id="b13ce-223">자격 증명 모음을 만든 했으므로 tooset 저장소 복제 hello 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-223">Now that you've created your vault, learn how tooset hello storage replication.</span></span>

### <a name="set-storage-replication"></a><span data-ttu-id="b13ce-224">저장소 복제 설정</span><span class="sxs-lookup"><span data-stu-id="b13ce-224">Set Storage Replication</span></span>
<span data-ttu-id="b13ce-225">hello 저장소 복제 옵션 지역 중복 저장소와 로컬 중복 저장소는 toochoose가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-225">hello storage replication option allows you toochoose between geo-redundant storage and locally redundant storage.</span></span> <span data-ttu-id="b13ce-226">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-226">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="b13ce-227">복구 서비스 자격 증명 모음에 hello 기본 백업을 이면 hello 저장소 복제 옵션 집합 toogeo 중복 저장소를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-227">If hello Recovery Services vault is your primary backup, leave hello storage replication option set toogeo-redundant storage.</span></span> <span data-ttu-id="b13ce-228">오래 지속되지 않는 저렴한 옵션을 원하는 경우에는 로컬 중복 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-228">Choose locally redundant storage if you want a cheaper option that isn't as durable.</span></span> <span data-ttu-id="b13ce-229">에 대해 자세히 알아보세요 [지리적 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) hello에 대 한 저장소 옵션 [Azure 저장소 복제 개요](../storage/common/storage-redundancy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-229">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in hello [Azure Storage replication overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="b13ce-230">tooedit hello 저장소 복제 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-230">tooedit hello storage replication setting:</span></span>

1. <span data-ttu-id="b13ce-231">Hello에서 **복구 서비스 자격 증명 모음** 블레이드, 선택 hello 새 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-231">From hello **Recovery Services vaults** blade, select hello new vault.</span></span>

  ![복구 서비스 자격 증명 모음의 hello 목록에서 hello 새 자격 증명 모음을 선택 합니다.](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  <span data-ttu-id="b13ce-233">Hello 자격 증명 모음을 선택 하면 hello 설정 블레이드에서 (*hello 자격 증명 모음의 이름을 hello 위쪽에 있는*) 및 hello 자격 증명 모음 세부 정보 블레이드에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-233">When you select hello vault, hello Settings blade (*which has hello vault's name at hello top*) and hello vault details blade open.</span></span>

  ![새 자격 증명 모음에 대 한 hello 저장소 구성 보기](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="b13ce-235">Hello 새 자격 증명 모음의 설정 블레이드에서 toohello 관리 섹션 아래로 수직 슬라이드 tooscroll hello를 사용 하 여 마우스 클릭 **백업 인프라**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-235">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="b13ce-236">hello 백업 인프라 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-236">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="b13ce-237">Hello 백업 인프라 블레이드에서 클릭 **백업 구성** tooopen hello **백업 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-237">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![새 자격 증명 모음에 대 한 저장소 구성을 hello 설정](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="b13ce-239">자격 증명 모음에 대 한 hello 적절 한 저장소 복제 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-239">Choose hello appropriate storage replication option for your vault.</span></span>

    ![저장소 구성 선택 항목](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="b13ce-241">기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-241">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="b13ce-242">기본 백업 저장소 끝점으로 Azure를 사용 하는 경우 계속 toouse **지리적 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-242">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="b13ce-243">기본 백업 저장소 끝점으로 Azure를 사용 하지 않는 경우 선택할 **로컬 중복**, hello Azure 저장소 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-243">If you don't use Azure as a primary backup storage endpoint, then choose **Locally redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="b13ce-244">[지역 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) 저장소 옵션에 대한 자세한 내용은 [저장소 중복 개요](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b13ce-244">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a><span data-ttu-id="b13ce-245">백업 목표를 선택 하 고 정책 설정 항목 tooprotect 정의</span><span class="sxs-lookup"><span data-stu-id="b13ce-245">Select a backup goal, set policy and define items tooprotect</span></span>
<span data-ttu-id="b13ce-246">자격 증명 모음으로 VM을 등록 하기 전에 실행 hello 검색 프로세스 tooensure toohello 구독에 추가 된 모든 새 가상 컴퓨터를 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-246">Before registering a VM with a vault, run hello discovery process tooensure that any new virtual machines that have been added toohello subscription are identified.</span></span> <span data-ttu-id="b13ce-247">추가 정보와 함께 hello 구독에서 가상 컴퓨터의 hello 목록에 대 한 hello 프로세스 쿼리 Azure hello 클라우드 서비스 이름 및 hello 영역 같은입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-247">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span> <span data-ttu-id="b13ce-248">Hello Azure 포털, 시나리오는 toowhat hello 복구 서비스 자격 증명 모음에 tooput는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-248">In hello Azure portal, scenario refers toowhat you are going tooput into hello recovery services vault.</span></span> <span data-ttu-id="b13ce-249">정책에는 복구 지점을 수행 빈도 및 시기에 대 한 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-249">Policy is hello schedule for how often and when recovery points are taken.</span></span> <span data-ttu-id="b13ce-250">또한 정책은 hello 복구 지점에 대 한 hello 보존 범위를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-250">Policy also includes hello retention range for hello recovery points.</span></span>

1. <span data-ttu-id="b13ce-251">자격 증명 모음을 열고 복구 서비스를 이미 있는 경우에 2 toostep을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-251">If you already have a recovery services vault open, proceed toostep 2.</span></span> <span data-ttu-id="b13ce-252">그렇지 않은 경우 hello 허브 메뉴에서 클릭 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **복구 서비스** 클릭 **복구 서비스 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-252">Otherwise, on hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="b13ce-254">복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-254">hello list of recovery services vaults appears.</span></span>

    ![Hello 복구 서비스의 보기 목록 자격 증명 모음](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    <span data-ttu-id="b13ce-256">복구 서비스 자격 증명 모음의 hello 목록에서 자격 증명 모음 tooopen 대시보드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-256">From hello list of recovery services vaults, select a vault tooopen its dashboard.</span></span>

     ![자격 증명 모음 블레이드 열기](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. <span data-ttu-id="b13ce-258">Hello 자격 증명 모음 대시보드 메뉴를 클릭 **백업** tooopen hello 백업 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-258">On hello vault dashboard menu, click **Backup** tooopen hello Backup blade.</span></span>

    ![백업 블레이드 열기](./media/backup-azure-arm-vms-prepare/backup-button.png)

    <span data-ttu-id="b13ce-260">hello 백업 및 백업 목표 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-260">hello Backup and Backup Goal blades open.</span></span>

    ![시나리오 블레이드 열기](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. <span data-ttu-id="b13ce-262">Hello에서 hello 백업 목표 블레이드에서 **여기서 작업이 실행 되는** 드롭 다운 메뉴에서 Azure를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-262">On hello Backup Goal blade, from hello **Where is your workload running** drop-down menu, choose Azure.</span></span> <span data-ttu-id="b13ce-263">Hello에서 **하 신 toobackup 원하는** 드롭 다운을 가상 컴퓨터를 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-263">From hello **What do you want toobackup** drop-down, choose Virtual machine, then click **OK**.</span></span>

    <span data-ttu-id="b13ce-264">이러한 동작은 hello 자격 증명 모음과 hello VM 확장을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-264">These actions register hello VM extension with hello vault.</span></span> <span data-ttu-id="b13ce-265">hello 블레이드를 닫고 백업 목표 및 hello **백업 정책** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-265">hello Backup Goal blade closes and hello **Backup policy** blade opens.</span></span>

    ![시나리오 블레이드 열기](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. <span data-ttu-id="b13ce-267">Hello 백업 정책 블레이드에서 hello 백업 정책을 원하는 tooapply toohello 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-267">On hello Backup policy blade, select hello backup policy you want tooapply toohello vault.</span></span>

    ![백업 정책 선택](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    <span data-ttu-id="b13ce-269">hello 기본 정책의 hello 세부 정보는 hello 드롭 다운 메뉴 아래에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-269">hello details of hello default policy are listed under hello drop-down menu.</span></span> <span data-ttu-id="b13ce-270">Toocreate 정책을 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-270">If you want toocreate a policy, select **Create New** from hello drop-down menu.</span></span> <span data-ttu-id="b13ce-271">백업 정책 정의에 대한 지침은 [백업 정책 정의](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b13ce-271">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span></span>
    <span data-ttu-id="b13ce-272">클릭 **확인** tooassociate hello 백업 정책을 hello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-272">Click **OK** tooassociate hello backup policy with hello vault.</span></span>

    <span data-ttu-id="b13ce-273">백업 정책 블레이드 닫히고 hello hello **가상 컴퓨터 선택** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-273">hello Backup policy blade closes and hello **Select virtual machines** blade opens.</span></span>
5. <span data-ttu-id="b13ce-274">Hello에 **가상 컴퓨터 선택** 블레이드에서 hello로 가상 컴퓨터 tooassociate hello 정책 지정 및 클릭 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-274">In hello **Select virtual machines** blade, choose hello virtual machines tooassociate with hello specified policy and click **OK**.</span></span>

    ![워크로드 선택](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    <span data-ttu-id="b13ce-276">가상 컴퓨터를 선택 하는 hello 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-276">hello selected virtual machine is validated.</span></span> <span data-ttu-id="b13ce-277">Hello 가상 표시 되지 않으면 toosee에 존재 하는 검사를 예상 하는 컴퓨터 hello 복구 서비스 자격 증명 모음으로 동일한 Azure 위치를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-277">If you do not see hello virtual machines that you expected toosee, check that they exist in hello same Azure location as hello Recovery Services vault.</span></span> <span data-ttu-id="b13ce-278">복구 서비스 자격 증명 모음에 hello의 hello 위치 hello 자격 증명 모음 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-278">hello location of hello Recovery Services vault is shown on hello vault dashboard.</span></span>

6. <span data-ttu-id="b13ce-279">이제 hello 자격 증명 모음에 대 한 모든 설정을 hello 백업 블레이드에서 정의한 클릭 **백업 사용** toodeploy hello 정책 toohello 자격 증명 모음 및 Vm hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-279">Now that you have defined all settings for hello vault, in hello Backup blade, click **Enable Backup** toodeploy hello policy toohello vault and hello VMs.</span></span> <span data-ttu-id="b13ce-280">Hello 백업 정책을 배포 하는 hello 가상 컴퓨터에 대 한 hello 초기 복구 지점을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-280">Deploying hello backup policy does not create hello initial recovery point for hello virtual machine.</span></span>

    ![백업 사용](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

<span data-ttu-id="b13ce-282">Hello 백업을 성공적으로 활성화 한 다음 백업 정책 일정에 따라 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-282">After successfully enabling hello backup, your backup policy will execute on schedule.</span></span> <span data-ttu-id="b13ce-283">그러나 tooinitiate hello 첫 번째 백업 작업을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-283">However, proceed tooinitiate hello first backup job.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="b13ce-284">초기 백업</span><span class="sxs-lookup"><span data-stu-id="b13ce-284">Initial backup</span></span>
<span data-ttu-id="b13ce-285">백업 정책을 의미가 있는 hello 가상 컴퓨터에 배포 된 hello 데이터가 백업 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-285">Once a backup policy has been deployed on hello virtual machine, that does not mean hello data has been backed up.</span></span> <span data-ttu-id="b13ce-286">기본적으로 첫 번째 예약 된 백업을 hello (정의 된 대로 hello 백업 정책에)는 hello 초기 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-286">By default, hello first scheduled backup (as defined in hello backup policy) is hello initial backup.</span></span> <span data-ttu-id="b13ce-287">Hello 초기 백업을 수행 될 때까지 hello에서 마지막 백업 상태 hello **백업 작업** 블레이드로 표시 **경고 (초기 백업 보류 중인)**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-287">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![보류 중인 백업](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="b13ce-289">초기 백업 기간이 하지 않는 한 toobegin 곧 것이 좋습니다를 실행 하는 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-289">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span>

<span data-ttu-id="b13ce-290">toorun hello 초기 백업 작업:</span><span class="sxs-lookup"><span data-stu-id="b13ce-290">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="b13ce-291">Hello 자격 증명 모음 대시보드에서 hello 숫자 아래를 클릭 합니다. **백업 항목**, 하거나 클릭 hello **백업 항목** 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-291">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="b13ce-292">
  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="b13ce-292">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="b13ce-293">hello **백업 항목** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-293">hello **Backup Items** blade opens.</span></span>

  ![항목 백업](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="b13ce-295">Hello에 **백업 항목** 블레이드, hello 선택 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-295">On hello **Backup Items** blade, select hello item.</span></span>

  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="b13ce-297">hello **백업 항목** 목록 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-297">hello **Backup Items** list opens.</span></span> <br/>

  ![백업 작업 트리거됨](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="b13ce-299">Hello에 **백업 항목** 목록에서 줄임표 hello **...**  tooopen hello 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-299">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="b13ce-301">hello 상황에 맞는 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-301">hello Context menu appears.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="b13ce-303">Hello 상황에 맞는 메뉴에서 클릭 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-303">On hello Context menu, click **Backup now**.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="b13ce-305">hello 지금 백업 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-305">hello Backup Now blade opens.</span></span>

  ![hello 지금 백업 블레이드를 표시합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="b13ce-307">Hello 지금 백업 블레이드의 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-307">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![hello 마지막 날 hello 지금 백업 복구 지점을 유지 되는 설정](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="b13ce-309">배포 알림 hello 백업 작업 트리거 되었으며 hello 작업 hello 백업 작업 페이지의 hello 진행률을 모니터링할 수 있습니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-309">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="b13ce-310">VM의 hello 크기에 따라 hello 초기 백업을 만드는 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-310">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="b13ce-311">hello에 hello 자격 증명 모음 대시보드에서 hello 초기 백업 tooview 또는 트랙 hello 상태 **백업 작업** 타일 클릭 **진행에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-311">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="b13ce-313">hello 백업 작업이 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-313">hello Backup Jobs blade opens.</span></span>

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="b13ce-315">Hello에 **백업 작업** 블레이드에서 모든 작업의 hello 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-315">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="b13ce-316">Hello VM에 대 한 백업 작업이 아직 진행 중인 경우, 또는 마친 경우 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b13ce-316">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="b13ce-317">백업 작업이 완료 되 면 hello 상태는 *Completed*합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-317">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b13ce-318">Hello 백업 작업의 일부로 hello Azure 백업 서비스에 모두 작성 하 고 일관 된 스냅숏을 각 VM tooflush 명령 toohello 백업 확장을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-318">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="b13ce-319">Hello 가상 컴퓨터에 hello VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="b13ce-319">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="b13ce-320">필요한 경우 이 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-320">This information is provided in case it is needed.</span></span> <span data-ttu-id="b13ce-321">Azure VM 에이전트 hello hello 백업 확장 toowork hello에 대 한 Azure 가상 컴퓨터에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-321">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="b13ce-322">그러나, hello Azure 갤러리에서에서 VM을 만든 경우 다음 hello VM 에이전트는 이미에 hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="b13ce-322">However, if your VM was created from hello Azure gallery, then hello VM Agent is already present on hello virtual machine.</span></span> <span data-ttu-id="b13ce-323">Hello VM 에이전트가 설치 되어 있지는 온-프레미스 데이터 센터에서 마이그레이션하는 하는 Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-323">VMs that are migrated from on-premises datacenters would not have hello VM Agent installed.</span></span> <span data-ttu-id="b13ce-324">이 경우 hello VM 에이전트 설치 toobe 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-324">In such a case, hello VM Agent needs toobe installed.</span></span> <span data-ttu-id="b13ce-325">Azure VM 에이전트 hello 검사 hello 가상 컴퓨터에 제대로 설치 hello Azure VM을 백업 하는 데 문제가 있으면 (hello 다음 표 참조).</span><span class="sxs-lookup"><span data-stu-id="b13ce-325">If you have problems backing up hello Azure VM, check that hello Azure VM Agent is correctly installed on hello virtual machine (see hello following table).</span></span> <span data-ttu-id="b13ce-326">사용자 지정 VM을 만들 경우 [hello 확인 **VM 에이전트 설치 hello** 확인란이 선택 되어](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) hello 가상 컴퓨터 프로 비전 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="b13ce-326">If you create a custom VM, [ensure hello **Install hello VM Agent** check box is selected](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) before hello virtual machine is provisioned.</span></span>

<span data-ttu-id="b13ce-327">Hello에 대 한 자세한 내용은 [VM 에이전트](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) 및 [어떻게 tooinstall 것](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-327">Learn about hello [VM Agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how tooinstall it](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="b13ce-328">다음 표에서 hello hello VM 에이전트에 대 한 Windows 및 Linux Vm에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-328">hello following table provides additional information about hello VM Agent for Windows and Linux VMs.</span></span>

| <span data-ttu-id="b13ce-329">**작업**</span><span class="sxs-lookup"><span data-stu-id="b13ce-329">**Operation**</span></span> | <span data-ttu-id="b13ce-330">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b13ce-330">**Windows**</span></span> | <span data-ttu-id="b13ce-331">**Linux**</span><span class="sxs-lookup"><span data-stu-id="b13ce-331">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b13ce-332">Hello VM 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-332">Installing hello VM Agent</span></span> |<li><span data-ttu-id="b13ce-333">다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-333">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="b13ce-334">관리자 권한 toocomplete hello 설치를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-334">You need Administrator privileges toocomplete hello installation.</span></span> <li><span data-ttu-id="b13ce-335">[Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-335">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |<li> <span data-ttu-id="b13ce-336">Hello 최신 설치 [Linux 에이전트](https://github.com/Azure/WALinuxAgent) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-336">Install hello latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="b13ce-337">관리자 권한 toocomplete hello 설치를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-337">You need Administrator privileges toocomplete hello installation.</span></span> <li> <span data-ttu-id="b13ce-338">[Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-338">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |
| <span data-ttu-id="b13ce-339">Hello VM 에이전트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-339">Updating hello VM Agent</span></span> |<span data-ttu-id="b13ce-340">업데이트 hello VM 에이전트를 다시 설치 하는 hello [VM 에이전트 이진 파일](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-340">Updating hello VM Agent is as simple as reinstalling hello [VM Agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><span data-ttu-id="b13ce-341">Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-341">Ensure that no backup operation is running while hello VM agent is being updated.</span></span> |<span data-ttu-id="b13ce-342">Hello 지침에 따라 [Linux VM 에이전트를 hello 업데이트](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-342">Follow hello instructions on [updating hello Linux VM Agent](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><span data-ttu-id="b13ce-343">백업 작업이 수행 되지 hello VM 에이전트를 업데이트 하는 동안 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-343">Ensure that no backup operation is running while hello VM Agent is being updated.</span></span> |
| <span data-ttu-id="b13ce-344">Hello VM 에이전트 설치 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="b13ce-344">Validating hello VM Agent installation</span></span> |<li><span data-ttu-id="b13ce-345">Toohello 이동 *C:\WindowsAzure\Packages* hello Azure VM에서에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-345">Navigate toohello *C:\WindowsAzure\Packages* folder in hello Azure VM.</span></span> <li><span data-ttu-id="b13ce-346">Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-346">You should find hello WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="b13ce-347">Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 선택한 후 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 합니다. 이상.</span><span class="sxs-lookup"><span data-stu-id="b13ce-347">Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="b13ce-348">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b13ce-348">N/A</span></span> |

### <a name="backup-extension"></a><span data-ttu-id="b13ce-349">백업 확장</span><span class="sxs-lookup"><span data-stu-id="b13ce-349">Backup extension</span></span>
<span data-ttu-id="b13ce-350">한 번 hello 가상 컴퓨터를 hello Azure 백업 서비스에 VM 에이전트가 설치 되어 hello hello 예비 내선 번호 toohello VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-350">Once hello VM Agent is installed on hello virtual machine, hello Azure Backup service installs hello backup extension toohello VM Agent.</span></span> <span data-ttu-id="b13ce-351">hello Azure 백업 서비스에 원활 하 게 업그레이드 및 추가 사용자 개입 없이 hello 예비 내선 번호를 패치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-351">hello Azure Backup service seamlessly upgrades and patches hello backup extension without additional user intervention.</span></span>

<span data-ttu-id="b13ce-352">hello 백업 서비스는 hello VM이 실행 되지 않는 경우에 hello 예비 내선 번호를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-352">hello Backup service installs hello backup extension, even if hello VM is not running.</span></span> <span data-ttu-id="b13ce-353">실행 중인 VM 응용 프로그램 일치 복구 지점의 얻을의 hello 가장 큰 기회를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-353">A running VM provides hello greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="b13ce-354">그러나 hello Azure 백업 서비스를 해제 되어 있으면 및 hello 확장을 설치할 수 하는 경우에 tooback hello VM 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-354">However, hello Azure Backup service continues tooback up hello VM even if it is turned off, and hello extension could not be installed.</span></span> <span data-ttu-id="b13ce-355">이러한 유형의 백업 오프 라인 VM 이라고 하며 hello 복구 지점은 *크래시 일관성이 있는*합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-355">This type of backup is known as Offline VM, and hello recovery point is *crash consistent*.</span></span>

## <a name="troubleshooting-information"></a><span data-ttu-id="b13ce-356">문제 해결 정보</span><span class="sxs-lookup"><span data-stu-id="b13ce-356">Troubleshooting information</span></span>
<span data-ttu-id="b13ce-357">이 문서에서 hello 작업을 수행 하는 문제를 사용 하는 경우 참조는 [문제 해결 지침](backup-azure-vms-troubleshoot.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-357">If you have issues accomplishing some of hello tasks in this article, consult the [Troubleshooting guidance](backup-azure-vms-troubleshoot.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="b13ce-358">가격</span><span class="sxs-lookup"><span data-stu-id="b13ce-358">Pricing</span></span>
<span data-ttu-id="b13ce-359">Azure Vm 백업의 hello 비용 hello 보호 된 인스턴스 수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-359">hello cost of backing up Azure VMs is based on hello number of protected instances.</span></span> <span data-ttu-id="b13ce-360">보호된 인스턴스에 대한 정의는 [보호된 인스턴스란 무엇인가요?](backup-introduction-to-azure-backup.md#what-is-a-protected-instance)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b13ce-360">For a definition of a protected instance, see [What is a protected instance](backup-introduction-to-azure-backup.md#what-is-a-protected-instance).</span></span> <span data-ttu-id="b13ce-361">가상 컴퓨터를 백업 hello 비용 계산의 예제를 보려면 [보호 된 인스턴스 계산 되는 방식을](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-361">For an example of calculating hello cost of backing up a virtual machine, see [How are protected instances calculated](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances).</span></span> <span data-ttu-id="b13ce-362">Azure 백업 가격 hello 참조에 대 한 정보에 대 한 페이지 [백업 가격](https://azure.microsoft.com/pricing/details/backup/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-362">See hello Azure Backup Pricing page for information about [Backup Pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>

## <a name="questions"></a><span data-ttu-id="b13ce-363">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="b13ce-363">Questions?</span></span>
<span data-ttu-id="b13ce-364">기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.</span><span class="sxs-lookup"><span data-stu-id="b13ce-364">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
