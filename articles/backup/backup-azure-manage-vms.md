---
title: "Resource Manager로 배포된 가상 컴퓨터 백업 관리 | Microsoft Docs"
description: "Resource Manager로 배포된 가상 컴퓨터 백업을 관리하고 모니터링하는 방법을 알아봅니다."
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
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="3379f-103">Azure 가상 컴퓨터 백업 관리</span><span class="sxs-lookup"><span data-stu-id="3379f-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3379f-104">Azure VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="3379f-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="3379f-105">클래식 VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="3379f-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="3379f-106">이 문서는 VM 백업 관리 지침을 제공하며, 포털 대시보드에서 사용할 수 있는 백업 경고 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="3379f-107">복구 서비스 자격 증명 모음이 있는 VM을 사용하는 경우 이 문서의 지침을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="3379f-108">이 문서에서는 가상 컴퓨터 만들기에 대해 다루거나 가상 컴퓨터를 보호하는 방법을 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="3379f-109">복구 서비스 자격 증명을 사용하여 Azure의 Azure Resource Manager로 배포된 VM을 보호하기 위한 입문서는 [먼저 보기: 복구 서비스 자격 증명 모음에 VM 백업](backup-azure-vms-first-look-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3379f-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="3379f-110">자격 증명 모음 및 보호된 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="3379f-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="3379f-111">Azure 포털에서 복구 서비스 자격 증명 모음 대시보드는 다음을 포함하는 자격 증명 모음에 대한 정보에 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="3379f-112">가장 최근 복원 지점이기도 한 가장 최근 백업 스냅숏 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="3379f-113">백업 정책 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-113">the backup policy <br\></span></span>
* <span data-ttu-id="3379f-114">모든 백업 스냅숏의 전체 크기 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="3379f-115">자격 증명 모음으로 보호되는 가상 컴퓨터의 수 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="3379f-116">가상 컴퓨터 백업을 사용하는 다양한 관리 작업은 대시보드에서 자격 증명 모음 열기로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="3379f-117">그러나 자격 증명 모음을 사용하여 여러 항목(또는 여러 VM)을 보호할 수 있으므로 특정 VM에 대한 세부 정보를 보려면 자격 증명 모음 항목 대시보드를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="3379f-118">다음 절차는 *자격 증명 모음 대시보드*를 열고 *자격 증명 모음 항목 대시보드*를 진행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="3379f-119">절차 모두에는 대시보드 명령에 고정을 사용하여 Azure 대시보드에 자격 증명 모음 및 자격 증명 모음 항목을 추가하는 방법을 알려주는 "팁"이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="3379f-120">대시보드에 고정은 자격 증명 모음 또는 항목에 바로 가기를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="3379f-121">바로 가기에서 일반적인 명령을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="3379f-122">여러 대시보드와 블레이드를 연 경우 창의 아래쪽에 있는 진한 파란색 슬라이더를 사용하여 Azure 대시보드에서 앞뒤로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![슬라이더가 있는 전체 보기](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="3379f-124">대시보드에서 복구 서비스 자격 증명 모음을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="3379f-125">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3379f-126">허브 메뉴에서 **찾아보기**를 클릭하고 리소스 목록에서 **복구 서비스**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="3379f-127">입력을 시작하면 입력한 내용을 바탕으로 목록이 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="3379f-128">**복구 서비스 자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-128">Click **Recovery Services vault**.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="3379f-130">복구 서비스 자격 증명 모음의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="3379f-131">복구 서비스 자격 증명 모음 목록</span><span class="sxs-lookup"><span data-stu-id="3379f-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="3379f-132">Azure 대시보드에 자격 증명 모음을 고정하는 경우 Azure 포털을 열 경우 해당 자격 증명 모음에 즉시 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="3379f-133">대시보드에 자격 증명 모음을 고정하려면 자격 증명 모음 목록에서 자격 증명 모음을 마우스 오른쪽 단추로 클릭하고 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="3379f-134">자격 증명 모음 목록에서 자격 증명 모음을 선택하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="3379f-135">자격 증명 모음을 선택할 경우 자격 증명 모음 대시보드 및 **설정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="3379f-136">다음 이미지에서 **Contoso-vault** 대시보드가 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![자격 증명 모음 대시보드 열기 및 설정 블레이드](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="3379f-138">자격 증명 모음 항목 대시보드 열기</span><span class="sxs-lookup"><span data-stu-id="3379f-138">Open a vault item dashboard</span></span>
<span data-ttu-id="3379f-139">이전 절차에서 자격 증명 모음 대시보드를 열었습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="3379f-140">자격 증명 모음 항목 대시보드를 열려면:</span><span class="sxs-lookup"><span data-stu-id="3379f-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="3379f-141">자격 증명 모음 대시보드의 **백업 항목** 타일에서 **Azure Virtual Machines**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![백업 항목 열기 타일](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="3379f-143">**백업 항목** 블레이드에서 각 항목에 대한 마지막 백업 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="3379f-144">이 예제에는 자격 증명이 모음에 의해 보호되는 하나의 가상 컴퓨터인 demovm-markgal이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![백업 항목 타일](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="3379f-146">쉽게 액세스하기 위해 자격 증명 모음 항목을 Azure 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="3379f-147">자격 증명 모음을 고정하려면 자격 증명 모음 항목 목록에서 항목을 마우스 오른쪽 단추로 클릭하고 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="3379f-148">**백업 항목** 블레이드에서 항목을 클릭하여 자격 증명 모음 항목 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![백업 항목 타일](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="3379f-150">자격 증명 모음 항목 대시보드 및 해당 **설정** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![설정 블레이드에서 백업 항목 대시보드](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="3379f-152">자격 증명 모음 항목 대시보드에서 다음과 같은 다양한 키 관리 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="3379f-153">정책 변경 또는 새 백업 정책 만들기 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="3379f-154">복원 지점 확인 및 해당 일관성 상태 확인 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="3379f-155">가상 컴퓨터의 주문형 백업<br\></span><span class="sxs-lookup"><span data-stu-id="3379f-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="3379f-156">가상 컴퓨터 보호 중지 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="3379f-157">가상 컴퓨터 보호 재개 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="3379f-158">백업 데이터(또는 복구 지점) 삭제 <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="3379f-159">[백업 디스크 복원](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="3379f-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="3379f-160">다음 절차의 경우 시작점은 자격 증명 모음 항목 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="3379f-161">백업 정책 관리</span><span class="sxs-lookup"><span data-stu-id="3379f-161">Manage backup policies</span></span>
1. <span data-ttu-id="3379f-162">[자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard)에서 **모든 설정**을 클릭하여 **설정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![백업 정책 블레이드](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="3379f-164">**설정** 블레이드에서 **백업 정책**을 클릭하여 해당 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="3379f-165">블레이드에서 백업 빈도 및 보존 범위 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![백업 정책 블레이드](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="3379f-167">**백업 정책 선택** 메뉴에서:</span><span class="sxs-lookup"><span data-stu-id="3379f-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="3379f-168">정책을 변경하려면 다른 정책을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="3379f-169">자격 증명 모음에 새 정책이 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="3379f-170"><br\></span><span class="sxs-lookup"><span data-stu-id="3379f-170"><br\></span></span>
   * <span data-ttu-id="3379f-171">정책을 만들려는 경우 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-171">To create a policy, select **Create New**.</span></span>

     ![가상 컴퓨터 백업](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="3379f-173">백업 정책을 만드는 지침은 [백업 정책 정의](backup-azure-manage-vms.md#defining-a-backup-policy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3379f-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="3379f-174">백업 정책을 관리하는 동안 최적의 백업 성능을 위해 [모범 사례](backup-azure-vms-introduction.md#best-practices)를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="3379f-175">가상 컴퓨터의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="3379f-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="3379f-176">보호를 위해 구성한 후에는 가상 컴퓨터의 주문형 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="3379f-177">초기 백업이 보류 중인 경우 주문형 백업은 복구 서비스 자격 증명 모음에 가상 컴퓨터의 전체 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="3379f-178">초기 백업이 완료되면 주문형 백업은 이전 스냅숏에서 복구 서비스 자격 증명 모음에 변경 내용만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="3379f-179">즉, 이후의 백업은 항상 증분형입니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="3379f-180">주문형 백업에 대한 보존 범위는 정책에서 매일 백업 지점에 대해 지정된 보존 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="3379f-181">매일 백업 시점을 선택하지 않은 경우 주간 백업 지점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="3379f-182">가상 컴퓨터의 주문형 백업을 트리거하려면:</span><span class="sxs-lookup"><span data-stu-id="3379f-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="3379f-183">[자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard)에서 **지금 백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![지금 백업 아이콘](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="3379f-185">포털에서는 주문형 백업 작업을 시작하려는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="3379f-186">**예** 를 클릭하여 백업 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-186">Click **Yes** to start the backup job.</span></span>

    ![지금 백업 아이콘](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="3379f-188">백업 작업에서 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="3379f-189">복구 지점의 재방문 주기 범위는 가상 컴퓨터와 연결된 정책에 지정된 보존 범위와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="3379f-190">작업에 대한 진행률을 추적하려면 자격 증명 모음 대시보드에서 **백업 작업** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="3379f-191">가상 컴퓨터 보호 중지</span><span class="sxs-lookup"><span data-stu-id="3379f-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="3379f-192">가상 컴퓨터에 대한 보호를 중지하려는 경우 복구 지점을 보존할지를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="3379f-193">두 가지 방법으로 가상 컴퓨터 보호를 정지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="3379f-194">모든 미래의 백업 작업을 정지하고 모든 복구 지점을 삭제, 또는</span><span class="sxs-lookup"><span data-stu-id="3379f-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="3379f-195">모든 미래의 백업 작업을 정지하고 복구 지점을 유지 </span><span class="sxs-lookup"><span data-stu-id="3379f-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="3379f-196">저장소에서 복구 지점을 유지하는 데 관련된 비용이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="3379f-197">그러나 복구 지점을 유지하는 장점은 나중에 원하는 경우 가상 컴퓨터를 복원할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="3379f-198">복구 지점을 유지하는 비용에 대한 자세한 내용은 [가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/backup/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3379f-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="3379f-199">모든 복구 지점을 삭제하려는 경우 가상 컴퓨터를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="3379f-200">가상 컴퓨터에 대한 보호를 중지하려면:</span><span class="sxs-lookup"><span data-stu-id="3379f-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="3379f-201">[자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard)에서 **백업 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![백업 중지 단추](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="3379f-203">백업 중지 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-203">The Stop Backup blade opens.</span></span>

    ![백업 중지 블레이드](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="3379f-205">**백업 중지** 블레이드에서 백업 데이터를 유지할지 혹은 삭제할지 여하를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="3379f-206">정보 상자에서는 선택한 항목에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-206">The information box provides details about your choice.</span></span>

    ![보호 중지](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="3379f-208">백업 데이터를 유지하기로 선택한 경우 4단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="3379f-209">백업 데이터 삭제를 삭제하기로 선택하고 백업 작업을 중지하고 복구 지점을 삭제하려는 경우 항목의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![백업 확인](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="3379f-211">항목 이름을 모르는 경우 이름을 보려면 느낌표 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="3379f-212">또한 항목의 이름은 블레이드 맨 위에 있는 **백업 중지** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="3379f-213">필요에 따라 **이유** 또는 **주석**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="3379f-214">현재 항목에 대 한 백업 작업을 중지 하려면 클릭 ![백업 중지 단추](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="3379f-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="3379f-215">알림 메시지를 통해 백업 작업이 중지되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![보호 중지 확인](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="3379f-217">가상 컴퓨터 보호 재개</span><span class="sxs-lookup"><span data-stu-id="3379f-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="3379f-218">가상 컴퓨터에 대한 보호가 중지되었을 때 **백업 데이터 보관** 옵션을 선택한 경우 보호를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="3379f-219">**백업 데이터 삭제** 옵션을 선택한 경우 가상 컴퓨터에 대한 보호를 다시 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="3379f-220">가상 컴퓨터에 대한 보호를 다시 시작하려면</span><span class="sxs-lookup"><span data-stu-id="3379f-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="3379f-221">[자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard)에서 **백업 다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![보호 다시 시작](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="3379f-223">백업 정책 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3379f-224">가상 컴퓨터를 다시 보호하는 경우 가상 컴퓨터가 처음에 보호된 정책과 다른 정책을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="3379f-225">[백업 정책 관리](backup-azure-manage-vms.md#manage-backup-policies)의 단계에 따라 가상 컴퓨터에 대한 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="3379f-226">백업 정책이 가상 컴퓨터에 적용되면 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![성공적으로 보호된 VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="3379f-228">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="3379f-228">Delete Backup data</span></span>
<span data-ttu-id="3379f-229">**백업 중지** 작업 중에 또는 백업이 완료된 후 언제든지 가상 컴퓨터와 연결된 백업 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="3379f-230">복구 지점을 삭제하기 전에 며칠 또는 몇 주 기다리는 것이 도움이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="3379f-231">백업 데이터를 삭제하는 경우 복구 지점을 복원하는 작업과 달리 특정 복구 지점을 삭제하도록 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="3379f-232">백업 데이터를 삭제하려는 경우 항목에 연결된 모든 복구 지점을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="3379f-233">다음 절차에서는 가상 컴퓨터에 대한 백업 작업이 중지 또는 비활성화되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="3379f-234">백업 작업을 사용하지 않는 경우 자격 증명 모음 항목 대시보드에서 **백업 다시 시작** 및 **백업 삭제** 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![다시 시작 및 삭제 단추](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="3379f-236">*백업을 사용하지 않는*가상 컴퓨터의 백업 데이터를 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="3379f-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="3379f-237">[자격 증명 모음 항목 대시보드](backup-azure-manage-vms.md#open-a-vault-item-dashboard)에서 **백업 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="3379f-239">**백업 데이터 삭제** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-239">The **Delete Backup Data** blade opens.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="3379f-241">항목의 이름을 입력하여 복구 지점을 삭제한다고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![백업 확인](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="3379f-243">항목 이름을 모르는 경우 이름을 보려면 느낌표 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="3379f-244">또한 항목의 이름은 블레이드 맨 위에 있는 **백업 데이터 삭제** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="3379f-245">필요에 따라 **이유** 또는 **주석**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="3379f-246">현재 항목에 대 한 백업 데이터를 삭제 하려면 클릭 ![백업 중지 단추](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="3379f-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="3379f-247">알림 메시지를 통해 백업 데이터가 삭제되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3379f-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3379f-248">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3379f-248">Next steps</span></span>
<span data-ttu-id="3379f-249">복구 지점에서 가상 컴퓨터를 다시 만드는 방법에 대한 내용은 [Azure VM 복원](backup-azure-restore-vms.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3379f-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="3379f-250">가상 컴퓨터를 보호하는 방법에 대한 정보가 필요한 경우 [먼저 보기: 복구 서비스 자격 증명 모음에 VM 백업](backup-azure-vms-first-look-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3379f-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="3379f-251">이벤트 모니터링에 대한 자세한 내용은 [Azure 가상 컴퓨터 백업에 대한 경고 모니터링](backup-azure-monitor-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3379f-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
