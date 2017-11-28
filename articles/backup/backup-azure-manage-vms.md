---
title: "aaaManage 리소스 관리자를 통해 배포 된 가상 컴퓨터 백업을 | Microsoft Docs"
description: "자세한 내용은 방법 toomanage 및 모니터 리소스 관리자를 통해 배포 된 가상 컴퓨터 백업"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="5c14e-103">Azure 가상 컴퓨터 백업 관리</span><span class="sxs-lookup"><span data-stu-id="5c14e-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c14e-104">Azure VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="5c14e-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="5c14e-105">클래식 VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="5c14e-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="5c14e-106">이 문서는 VM 백업이 관리에 대 한 지침을 제공 하 고 hello 포털 대시보드에서 사용할 수 있는 hello 백업 경고 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="5c14e-107">이 문서에 대 한 hello 지침 toousing Vm을 복구 서비스 자격 증명 모음을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="5c14e-108">이 문서는 hello 가상 컴퓨터 만들기를 다루지 않습니다 또는 설명지 않습니다 것 방법을 tooprotect 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="5c14e-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="5c14e-109">Azure에서 Azure 리소스 관리자를 통해 배포 된 Vm을 보호 하기 위해 복구 서비스 자격 증명 모음 primer, 참조 [소개: Vm tooa 복구 서비스 자격 증명 모음에 백업](backup-azure-vms-first-look-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="5c14e-110">자격 증명 모음 및 보호된 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="5c14e-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="5c14e-111">Azure 포털 hello hello 복구 서비스 자격 증명 모음 대시보드 포함 하 여 hello 자격 증명 모음에 대 한 액세스 tooinformation을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="5c14e-112">hello 가장 최근의 백업 스냅숏을 hello 최근 복원 지점 이기도 < b r\></span><span class="sxs-lookup"><span data-stu-id="5c14e-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="5c14e-113">백업 정책 hello < b r\></span><span class="sxs-lookup"><span data-stu-id="5c14e-113">hello backup policy <br\></span></span>
* <span data-ttu-id="5c14e-114">모든 백업 스냅숏의 전체 크기 <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="5c14e-115">hello 자격 증명 모음으로 보호 되는 가상 컴퓨터 수 < b r\></span><span class="sxs-lookup"><span data-stu-id="5c14e-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="5c14e-116">가상 컴퓨터 백업 사용 하 여 많은 관리 작업 hello 대시보드에 hello 자격 증명 모음을 열어로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="5c14e-117">그러나 자격 증명 모음에 사용 되는 tooprotect 여러 항목 (또는 여러 Vm)를 열고 특정 VM에 대 한 세부 정보 tooview 수 있기 때문에 자격 증명 모음 항목 대시보드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="5c14e-118">hello 다음 단계에서는 tooopen hello *자격 증명 모음 대시보드* toohello 후 계속 *자격 증명 모음 항목 대시보드*합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="5c14e-119">주는 tooadd 자격 증명 모음 hello 방법과 항목 toohello 자격 증명 모음 대시보드 Azure hello Pin toodashboard 명령을 사용 하 여 두 절차 모두에서 "팁"입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="5c14e-120">Pin toodashboard는 바로 가기 toohello 자격 증명 모음 또는 항목을 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="5c14e-121">또한 hello 바로 가기에서 일반적인 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="5c14e-122">여러 개인 대시보드가 있는 경우 블레이드를 열고 hello 어둡게, 파랑 슬라이더를 사용 하 여 hello 창 tooslide hello Azure 대시보드 간에 hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![슬라이더가 있는 전체 보기](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="5c14e-124">복구 서비스 자격 증명 모음 hello 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="5c14e-125">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5c14e-126">Hello 허브 메뉴에서 클릭 **찾아보기** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="5c14e-127">입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="5c14e-128">**복구 서비스 자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-128">Click **Recovery Services vault**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="5c14e-130">복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="5c14e-131">복구 서비스 자격 증명 모음 목록</span><span class="sxs-lookup"><span data-stu-id="5c14e-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="5c14e-132">자격 증명 모음 toohello Azure 대시보드를 고정 하는 경우 해당 자격 증명 모음이 hello Azure 포털을 열 때에 즉시 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="5c14e-133">hello 자격 증명 모음 목록에는 자격 증명 모음 toohello 대시보드 toopin hello 자격 증명 모음을 마우스 오른쪽 단추로 클릭 하 고 선택 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="5c14e-134">자격 증명 모음 hello 목록에서 대시보드 hello 자격 증명 모음 tooopen 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="5c14e-135">Hello 자격 증명 모음, 자격 증명 모음 대시보드 hello 및 hello 선택 **설정을** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="5c14e-136">다음 이미지는 hello에서 hello **Contoso-자격 증명 모음** 대시보드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![자격 증명 모음 대시보드 열기 및 설정 블레이드](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="5c14e-138">자격 증명 모음 항목 대시보드 열기</span><span class="sxs-lookup"><span data-stu-id="5c14e-138">Open a vault item dashboard</span></span>
<span data-ttu-id="5c14e-139">Hello 이전 절차에서 hello 자격 증명 모음 대시보드를 열.</span><span class="sxs-lookup"><span data-stu-id="5c14e-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="5c14e-140">tooopen hello 자격 증명 모음 항목 대시보드:</span><span class="sxs-lookup"><span data-stu-id="5c14e-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="5c14e-141">Hello 자격 증명 모음 대시보드 hello에서에서 **백업 항목** 타일을 클릭 하 여 **Azure 가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![백업 항목 열기 타일](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="5c14e-143">hello **백업 항목** 블레이드에 hello 각 항목에 대 한 마지막 백업 작업을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="5c14e-144">이 예제에는 자격 증명이 모음에 의해 보호되는 하나의 가상 컴퓨터인 demovm-markgal이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![백업 항목 타일](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="5c14e-146">편리한 액세스에 대 한 자격 증명 모음 항목 toohello Azure 대시보드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="5c14e-147">toopin hello 자격 증명 모음 항목 목록, 오른쪽 클릭 hello 항목 및 선택에서 자격 증명 모음 항목을 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="5c14e-148">Hello에 **백업 항목** 블레이드에서 hello 항목 tooopen hello 자격 증명 모음 항목 대시보드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![백업 항목 타일](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="5c14e-150">hello 자격 증명 모음 항목 대시보드 및 해당 **설정을** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![설정 블레이드에서 백업 항목 대시보드](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="5c14e-152">Hello 자격 증명 모음 항목 대시보드에서 같은 여러 주요 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="5c14e-153">정책 변경 또는 새 백업 정책 만들기 <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="5c14e-154">복원 지점 확인 및 해당 일관성 상태 확인 <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="5c14e-155">가상 컴퓨터의 주문형 백업<br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="5c14e-156">가상 컴퓨터 보호 중지 <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="5c14e-157">가상 컴퓨터 보호 재개 <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="5c14e-158">백업 데이터(또는 복구 지점) 삭제 <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="5c14e-159">[백업 디스크 복원](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="5c14e-160">다음 절차를 수행 하는 hello에 대 한 시작 지점 hello는 hello 자격 증명 모음 항목 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="5c14e-161">백업 정책 관리</span><span class="sxs-lookup"><span data-stu-id="5c14e-161">Manage backup policies</span></span>
1. <span data-ttu-id="5c14e-162">Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **모든 설정을** tooopen hello **설정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![백업 정책 블레이드](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="5c14e-164">Hello에 **설정** 블레이드에서 클릭 **백업 정책** tooopen 해당 블레이드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="5c14e-165">Hello 블레이드에서 hello 백업 빈도 보존 범위 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![백업 정책 블레이드](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="5c14e-167">Hello에서 **백업 정책을 선택** 메뉴:</span><span class="sxs-lookup"><span data-stu-id="5c14e-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="5c14e-168">toochange 정책에 다른 정책을 선택 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="5c14e-169">hello 새 정책이 즉시 적용 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="5c14e-170"><br\></span><span class="sxs-lookup"><span data-stu-id="5c14e-170"><br\></span></span>
   * <span data-ttu-id="5c14e-171">클라이언트는 정책을 toocreate 선택 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-171">toocreate a policy, select **Create New**.</span></span>

     ![가상 컴퓨터 백업](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="5c14e-173">백업 정책을 만드는 지침은 [백업 정책 정의](backup-azure-manage-vms.md#defining-a-backup-policy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c14e-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="5c14e-174">백업 정책, 관리 하는 동안 확인 되었는지 toofollow hello [모범 사례](backup-azure-vms-introduction.md#best-practices) 최적의 성능을 위해서는 백업</span><span class="sxs-lookup"><span data-stu-id="5c14e-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="5c14e-175">가상 컴퓨터의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="5c14e-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="5c14e-176">보호를 위해 구성한 후에는 가상 컴퓨터의 주문형 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="5c14e-177">Hello 초기 백업을 보류 중이면 변경 집합 요청 시 백업을 hello 복구 서비스 자격 증명 모음에 hello 가상 컴퓨터의 전체 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="5c14e-178">Hello 초기 백업이 완료 되 면 요청 시 백업을 hello 이전 스냅숏 toohello 복구 서비스 자격 증명 모음에서에서 변경 내용을만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="5c14e-179">즉, 이후의 백업은 항상 증분형입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="5c14e-180">요청 시 백업에 대 한 보존 범위 hello은 hello 정책에 hello 일일 백업 지점에 대해 지정 된 hello 보존 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="5c14e-181">일일 백업 지점 없는 선택 하는 경우 hello 주간 백업 지점 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="5c14e-182">가상 컴퓨터의 주문형 tootrigger 백업:</span><span class="sxs-lookup"><span data-stu-id="5c14e-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="5c14e-183">Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![지금 백업 아이콘](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="5c14e-185">hello 포털 toostart 주문형 백업 작업을 사용 하지 않겠다고 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="5c14e-186">클릭 **예** toostart hello에 대 한 백업 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-186">Click **Yes** toostart hello backup job.</span></span>

    ![지금 백업 아이콘](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="5c14e-188">hello 백업 작업에는 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="5c14e-189">hello 복구 지점의 보존 범위 hello hello 가상 컴퓨터와 연결 된 hello 정책에 지정 된 보존 범위와 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="5c14e-190">hello 자격 증명 모음 대시보드에서 hello 작업에 대 한 tootrack hello 진행률 클릭 hello **백업 작업이** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="5c14e-191">가상 컴퓨터 보호 중지</span><span class="sxs-lookup"><span data-stu-id="5c14e-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="5c14e-192">가상 컴퓨터 보호 toostop을 선택 하면 tooretain hello 복구 지점을 사용 하려는 경우 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="5c14e-193">두 가지가 toostop 보호 가상 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="5c14e-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="5c14e-194">모든 미래의 백업 작업을 정지하고 모든 복구 지점을 삭제, 또는</span><span class="sxs-lookup"><span data-stu-id="5c14e-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="5c14e-195">이후의 모든 백업 작업을 중단 하지만 hello 복구 지점 유지</span><span class="sxs-lookup"><span data-stu-id="5c14e-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="5c14e-196">저장소를 복구 지점 hello을 그대로 유지 하면서와 관련 된 비용이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="5c14e-197">그러나 복구 지점을 hello를 끝낼 hello 혜택은 나중 hello 가상 컴퓨터를 복원할 수 있습니다 원하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5c14e-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="5c14e-198">복구 지점을 hello를 끝낼 hello 비용에 대 한 정보를 참조 hello [가격 정보](https://azure.microsoft.com/pricing/details/backup/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="5c14e-199">Toodelete 모든 복구 지점을 선택 하면 hello 가상 컴퓨터를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="5c14e-200">가상 컴퓨터에 대 한 toostop 보호:</span><span class="sxs-lookup"><span data-stu-id="5c14e-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="5c14e-201">Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **백업 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![백업 중지 단추](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="5c14e-203">hello 백업 중지 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-203">hello Stop Backup blade opens.</span></span>

    ![백업 중지 블레이드](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="5c14e-205">Hello에 **백업 중지** 블레이드에서 tooretain 또는 delete 백업 데이터 hello 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="5c14e-206">hello 정보 상자 사용자가 선택한 방법에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-206">hello information box provides details about your choice.</span></span>

    ![보호 중지](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="5c14e-208">Tooretain hello 백업 데이터를 선택한 경우에 4 toostep을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="5c14e-209">Toodelete 백업 데이터를 선택한 경우 toostop hello에 대 한 백업 작업을 원하는 hello 항목의 형식 hello 이름은-hello 복구 지점이 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![백업 확인](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5c14e-211">Hello 항목 이름이 확실 하지 않은 경우 hello 느낌표 tooview hello 이름 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="5c14e-212">또한 hello hello 항목 이름은 아래 **백업 중지** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="5c14e-213">필요에 따라 **이유** 또는 **주석**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="5c14e-214">hello toostop hello 현재 항목에 대 한 백업 작업 클릭 ![백업 중지 단추](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="5c14e-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="5c14e-215">알림 메시지를 사용 하면 hello 백업 작업이 중지 된 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![보호 중지 확인](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="5c14e-217">가상 컴퓨터 보호 재개</span><span class="sxs-lookup"><span data-stu-id="5c14e-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="5c14e-218">경우 hello **백업 데이터 보관** 옵션이 hello 가상 컴퓨터에 대 한 보호 중지 되었을 때 가능한 tooresume 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="5c14e-219">경우 hello **백업 데이터 삭제** 옵션을 선택 했습니다. 다음 hello 가상 컴퓨터에 대 한 보호를 다시 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="5c14e-220">hello 가상 컴퓨터에 대 한 tooresume 보호</span><span class="sxs-lookup"><span data-stu-id="5c14e-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="5c14e-221">Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **백업 다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![보호 다시 시작](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="5c14e-223">hello 백업 정책 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c14e-224">Hello 가상 컴퓨터를 다시 보호 된 가상 컴퓨터를 보호 처음 hello 정책 보다 다른 정책을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="5c14e-225">Hello 단계에 따라 [백업 정책 관리](backup-azure-manage-vms.md#manage-backup-policies) hello 가상 컴퓨터에 대 한 tooassign hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="5c14e-226">Hello 백업 정책이 적용 된 toohello 가상 컴퓨터를 hello 메시지의 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![성공적으로 보호된 VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="5c14e-228">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="5c14e-228">Delete Backup data</span></span>
<span data-ttu-id="5c14e-229">Hello 하는 동안 가상 컴퓨터와 연결 된 hello 백업 데이터를 삭제할 수 있습니다 **백업 중지** 작업, 백업 작업이 완료 된 hello 후 언제 든 지 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="5c14e-230">유용한 toowait 일 또는 주로 hello 복구 지점도 삭제 하기 전에 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="5c14e-231">백업 데이터를 삭제할 때 복구 지점, 복원와 달리 특정 복구 지점 toodelete를 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="5c14e-232">Toodelete 백업 데이터를 선택할 경우 hello 항목과 연결 된 모든 복구 지점을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="5c14e-233">hello 다음 절차에서는 가정 hello 가상 컴퓨터에 대 한 백업 작업 hello 중지 되었거나 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="5c14e-234">Hello 백업 작업이 해제 되 면 hello **백업 다시 시작** 및 **Delete 백업** hello 자격 증명 모음 항목 대시보드에서 사용할 수 있는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![다시 시작 및 삭제 단추](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="5c14e-236">hello로 가상 컴퓨터에서 백업 데이터 toodelete *백업 사용 안 함*:</span><span class="sxs-lookup"><span data-stu-id="5c14e-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="5c14e-237">Hello에 [자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard), 클릭 **Delete 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="5c14e-239">hello **백업 데이터 삭제** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-239">hello **Delete Backup Data** blade opens.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="5c14e-241">형식 hello 이름 toodelete hello 복구 지점을 만들려는 hello 항목 tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![백업 확인](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5c14e-243">Hello 항목 이름이 확실 하지 않은 경우 hello 느낌표 tooview hello 이름 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="5c14e-244">또한 hello hello 항목 이름은 아래 **백업 데이터 삭제** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="5c14e-245">필요에 따라 **이유** 또는 **주석**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="5c14e-246">hello toodelete hello 현재 항목에 대 한 백업 데이터 클릭 ![백업 중지 단추](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="5c14e-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="5c14e-247">알림 메시지를 사용 하면 hello 백업 데이터가 삭제 되었는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c14e-248">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c14e-248">Next steps</span></span>
<span data-ttu-id="5c14e-249">복구 지점에서 가상 컴퓨터를 다시 만드는 방법에 대한 내용은 [Azure VM 복원](backup-azure-restore-vms.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5c14e-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="5c14e-250">가상 컴퓨터 보호에 대 한 정보를 보려면 참고 [소개: Vm tooa 복구 서비스 자격 증명 모음에 백업](backup-azure-vms-first-look-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c14e-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="5c14e-251">이벤트 모니터링에 대한 자세한 내용은 [Azure 가상 컴퓨터 백업에 대한 경고 모니터링](backup-azure-monitor-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c14e-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
