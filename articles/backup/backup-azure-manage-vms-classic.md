---
title: "Azure 가상 컴퓨터 백업 관리 및 모니터링 | Microsoft Docs"
description: "Azure 가상 컴퓨터 백업을 관리하고 모니터링하는 방법에 관해 알아봅니다."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d876bb1759600fa29a26730bfa8b4ec19db1e442
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-the-classic-portal"></a><span data-ttu-id="edee3-103">클래식 포털에서 일반적인 Azure Backup 작업 및 트리거 경고 관리</span><span class="sxs-lookup"><span data-stu-id="edee3-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="edee3-104">Azure VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="edee3-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="edee3-105">클래식 VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="edee3-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="edee3-106">이 문서에서는 Azure에서 보호되는 클랙식 모델 가상 컴퓨터에 대한 일반적인 관리 및 모니터링 관련 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="edee3-107">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="edee3-108">클래식 배포 모델 VM 작업에 대한 자세한 내용은 [Azure 가상 컴퓨터를 백업하기 위한 환경 준비](backup-azure-vms-prepare.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edee3-108">See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="edee3-109">2017년 3월부터는 백업 자격 증명 모음을 만드는 데 더 이상 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-109">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="edee3-110">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="edee3-111">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edee3-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="edee3-112">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="edee3-113">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="edee3-114">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="edee3-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="edee3-115">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="edee3-116">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="edee3-117">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="edee3-118">보호된 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="edee3-118">Manage protected virtual machines</span></span>
<span data-ttu-id="edee3-119">보호된 가상 컴퓨터 관리하려면</span><span class="sxs-lookup"><span data-stu-id="edee3-119">To manage protected virtual machines:</span></span>

1. <span data-ttu-id="edee3-120">가상 컴퓨터에 대한 백업 설정을 보고 관리하려면 **보호된 항목** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-120">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span></span>
2. <span data-ttu-id="edee3-121">**백업 세부 정보** 탭을 볼 보호된 항목의 이름을 클릭하면 마지막 백업에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-121">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span></span>

    ![가상 컴퓨터 백업](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="edee3-123">가상 컴퓨터에 대한 백업 정책 설정을 보고 관리하려면 **정책** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-123">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span></span>

    ![가상 컴퓨터 정책](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="edee3-125">**백업 정책** 탭에는 기존 정책이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-125">The **Backup Policies** tab shows you the existing policy.</span></span> <span data-ttu-id="edee3-126">필요에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-126">You can modify as needed.</span></span> <span data-ttu-id="edee3-127">새 정책을 만들어야 하는 경우 **정책** 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-127">If you need to create a new policy click **Create** on the **Policies** page.</span></span> <span data-ttu-id="edee3-128">정책을 제거하려는 경우 해당 정책과 연결된 가상 컴퓨터가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-128">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![가상 컴퓨터 정책](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="edee3-130">가상 컴퓨터의 동작 또는 상태에 대한 자세한 정보는 **작업** 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-130">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span></span> <span data-ttu-id="edee3-131">자세한 정보를 보려면 목록에서 작업을 클릭하거나 특정 가상 컴퓨터에 대한 작업을 필터링하세요.</span><span class="sxs-lookup"><span data-stu-id="edee3-131">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span></span>

    ![작업](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="edee3-133">가상 컴퓨터의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="edee3-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="edee3-134">보호를 위해 구성한 후에는 가상 컴퓨터의 주문형 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="edee3-135">가상 컴퓨터에 대한 초기 백업이 보류 중인 경우 주문형 백업은 Azure 백업 자격 증명 모음에 가상 컴퓨터의 전체 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-135">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span></span> <span data-ttu-id="edee3-136">첫 번째 백업이 완료된 경우 주문형 백업은 이전 백업의 변경 내용(즉, 항상 증분)만 Azure 백업 자격 증명 모음으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-136">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="edee3-137">주문형 백업의 보존 범위는 VM에 해당하는 백업 정책의 일 단위 보존에 대해 지정된 보존 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-137">Retention range of an on-demand backup is set to retention value specified for Daily retention in backup policy corresponding to the VM.</span></span>  
>
>

<span data-ttu-id="edee3-138">가상 컴퓨터의 주문형 백업을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="edee3-138">To take an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="edee3-139">**보호 항목** 페이지로 이동하고 **Azure 가상 컴퓨터**를 **형식**으로 선택한(선택되지 않은 경우) 다음 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-139">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="edee3-141">주문형 백업을 수행할 가상 컴퓨터를 선택하고 페이지 맨 아래에 있는 **지금 백업** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-141">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span></span>

    ![지금 백업](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="edee3-143">선택한 가상 컴퓨터에 대한 백업 작업이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-143">This will create a backup job on the selected virtual machine.</span></span> <span data-ttu-id="edee3-144">이 작업을 통해 만든 복구 지점의 보존 범위는 가상 컴퓨터와 연결된 정책에 지정된 범위와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-144">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span></span>

    ![백업 작업 만들기](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="edee3-146">가상 컴퓨터와 연결된 정책을 보려면 **보호되는 항목** 페이지에서 가상 컴퓨터로 드릴다운하고 백업 정책 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-146">To view the policy associated with a virtual machine, drill down into virtual machine in the **Protected Items** page and go to backup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="edee3-147">작업이 생성된 후에는 알림 표시줄의 **작업 보기** 단추를 클릭하여 작업 페이지에서 해당 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-147">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span></span>

    ![백업 작업 생성됨](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="edee3-149">작업이 성공적으로 완료되면 가상 컴퓨터를 복원하는 데 사용할 수 있는 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-149">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span></span> <span data-ttu-id="edee3-150">또한 **보호되는 항목** 페이지에서 복구 지점 열 값이 1씩 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-150">This will also increment the recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="edee3-151">가상 컴퓨터 보호 중지</span><span class="sxs-lookup"><span data-stu-id="edee3-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="edee3-152">다음 옵션으로 가상 컴퓨터의 향후 백업을 중지하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-152">You can choose to stop the future backups of a virtual machine with the following options:</span></span>

* <span data-ttu-id="edee3-153">Azure 백업 자격 증명 모음에 가상 컴퓨터와 연결된 백업 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="edee3-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="edee3-154">가상 컴퓨터와 연결된 백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="edee3-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="edee3-155">가상 컴퓨터와 연결된 백업 데이터를 유지하도록 선택한 경우 백업 데이터를 사용하여 가상 컴퓨터를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-155">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span></span> <span data-ttu-id="edee3-156">이러한 가상 컴퓨터의 가격 정보를 보려면 [여기](https://azure.microsoft.com/pricing/details/backup/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="edee3-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="edee3-157">가상 컴퓨터에 대한 보호를 중지하려면</span><span class="sxs-lookup"><span data-stu-id="edee3-157">To Stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="edee3-158">**보호 항목** 페이지로 이동하고 **Azure 가상 컴퓨터**를 필터 형식으로 선택한(선택되지 않은 경우) 다음 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-158">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="edee3-160">가상 컴퓨터를 선택하고 페이지 맨 아래에 있는 **보호 중지** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-160">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span></span>

    ![보호 중지](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="edee3-162">기본적으로 Azure 백업은 가상 컴퓨터와 연결된 백업 데이터를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-162">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span></span>

    ![보호 중지 확인](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="edee3-164">백업 데이터를 삭제하려면 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-164">If you want to delete backup data, select the check box.</span></span>

    ![확인란](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="edee3-166">백업을 중지하는 이유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-166">Please select a reason for stopping the backup.</span></span> <span data-ttu-id="edee3-167">선택 사항이지만, 이유를 제공하면 Azure 백업이 피드백에 따라 작동하고 고객 시나리오의 우선 순위를 지정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-167">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span></span>
4. <span data-ttu-id="edee3-168">**제출** 단추를 클릭하여 **보호 중지** 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-168">Click on **Submit** button to submit the **Stop protection** job.</span></span> <span data-ttu-id="edee3-169">**작업 보기**를 클릭하여 **작업** 페이지에서 해당 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-169">Click on **View Job** to see the corresponding the job in **Jobs** page.</span></span>

    ![보호 중지](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="edee3-171">**보호 중지** 마법사에서 **연결된 백업 데이터 삭제** 옵션을 선택하지 않은 경우 작업 완료 후 보호 상태는 **보호 중지됨**으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span></span> <span data-ttu-id="edee3-172">명시적으로 삭제될 때까지 Azure 백업을 사용하여 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-172">The data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="edee3-173">**보호 항목** 페이지에서 가상 컴퓨터를 선택하고 **삭제**를 클릭하면 언제든지 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-173">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span></span>

    ![보호 중지됨](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="edee3-175">**연결된 백업 데이터 삭제** 옵션을 선택한 경우 가상 컴퓨터가 **보호 항목** 페이지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-175">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="edee3-176">가상 컴퓨터 다시 보호</span><span class="sxs-lookup"><span data-stu-id="edee3-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="edee3-177">**보호 중지**에서 **연결된 백업 데이터 삭제** 옵션을 선택하지 않은 경우 등록된 가상 컴퓨터의 백업과 유사한 단계를 수행하면 해당 가상 컴퓨터를 다시 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-177">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span></span> <span data-ttu-id="edee3-178">보호하고 나면 이 가상 컴퓨터는 보호를 중지하기 전에 유지된 백업 데이터와 다시 보호한 후 생성된 복구 지점을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-178">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="edee3-179">다시 보호한 후에 **보호 중지** 이전의 복구 지점이 있는 경우 가상 컴퓨터의 보호 상태는 **보호됨**으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-179">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span></span>

  ![다시 보호된 VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="edee3-181">가상 컴퓨터를 다시 보호하는 경우 가상 컴퓨터가 처음에 보호된 정책과 다른 정책을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-181">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="edee3-182">가상 컴퓨터 등록 취소</span><span class="sxs-lookup"><span data-stu-id="edee3-182">Unregister virtual machines</span></span>
<span data-ttu-id="edee3-183">백업 자격 증명 모음에서 가상 컴퓨터를 제거하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-183">If you want to remove the virtual machine from the backup vault:</span></span>

1. <span data-ttu-id="edee3-184">페이지 아래쪽에서 **등록 취소** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-184">Click on the **UNREGISTER** button at the bottom of the page.</span></span>

    ![보호 사용 안 함](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="edee3-186">화면 아래쪽에 확인을 요청하는 토스트 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-186">A toast notification will appear at the bottom of the screen requesting confirmation.</span></span> <span data-ttu-id="edee3-187">**예** 를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-187">Click **YES** to continue.</span></span>

    ![보호 사용 안 함](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="edee3-189">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="edee3-189">Delete Backup data</span></span>
<span data-ttu-id="edee3-190">다음 중 하나에 가상 컴퓨터와 연결된 백업 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-190">You can delete the backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="edee3-191">보호 중지 작업 중</span><span class="sxs-lookup"><span data-stu-id="edee3-191">During Stop Protection Job</span></span>
* <span data-ttu-id="edee3-192">가상 컴퓨터에서 보호 중지 작업이 완료된 후</span><span class="sxs-lookup"><span data-stu-id="edee3-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="edee3-193">*백업 중지* 작업이 성공적으로 완료된 후 **보호 중지됨** 상태인 백업 데이터를 가상 컴퓨터에서 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="edee3-193">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="edee3-194">**보호 항목** 페이지로 이동하고 **Azure 가상 컴퓨터**를 *형식*으로 선택한 다음 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-194">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="edee3-196">가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-196">Select the virtual machine.</span></span> <span data-ttu-id="edee3-197">가상 컴퓨터가 **보호 중지됨** 상태로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-197">The virtual machine will be in **Protection Stopped** state.</span></span>

    ![보호 중지됨](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="edee3-199">페이지 맨 아래에 있는 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-199">Click the **DELETE** button at the bottom of the page.</span></span>

    ![백업 삭제](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="edee3-201">**백업 데이터 삭제** 마법사에서 백업 데이터를 삭제하는 이유를 선택하고(권장) **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-201">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="edee3-203">선택한 가상 컴퓨터의 백업 데이터를 삭제하는 작업이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-203">This will create a job to delete backup data of selected virtual machine.</span></span> <span data-ttu-id="edee3-204">**작업 보기** 를 클릭하여 작업 페이지에서 해당 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-204">Click **View job** to see corresponding job in Jobs page.</span></span>

    ![데이터 삭제 성공](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="edee3-206">작업이 완료되면 가상 컴퓨터에 해당하는 항목이 **보호되는 항목** 페이지에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-206">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="edee3-207">대시보드</span><span class="sxs-lookup"><span data-stu-id="edee3-207">Dashboard</span></span>
<span data-ttu-id="edee3-208">**대시보드** 페이지에서 Azure 가상 컴퓨터, 저장소 및 최근 24시간 동안의 관련 작업에 대한 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-208">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span></span> <span data-ttu-id="edee3-209">백업 상태 및 연결된 백업 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-209">You can view backup status and any associated backup errors.</span></span>

![대시보드](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="edee3-211">대시보드의 값은 24시간마다 한 번 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-211">Values in the dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="edee3-212">작업 감사</span><span class="sxs-lookup"><span data-stu-id="edee3-212">Auditing Operations</span></span>
<span data-ttu-id="edee3-213">Azure 백업은  백업 자격 증명 모음에서 관리 작업이 무엇을 수행하는지 정확하게 볼 수 있도록고객에 의해 트리거된 백업 작업의 "작업 로그"를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-213">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span></span> <span data-ttu-id="edee3-214">작업 로그를 사용하면 백업 작업에 대한 post-mortem 및 감사 지원이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-214">Operations logs enable great post-mortem and audit support for the backup operations.</span></span>

<span data-ttu-id="edee3-215">다음 작업은 작업 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-215">The following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="edee3-216">등록</span><span class="sxs-lookup"><span data-stu-id="edee3-216">Register</span></span>
* <span data-ttu-id="edee3-217">등록 취소</span><span class="sxs-lookup"><span data-stu-id="edee3-217">Unregister</span></span>
* <span data-ttu-id="edee3-218">보호 구성</span><span class="sxs-lookup"><span data-stu-id="edee3-218">Configure protection</span></span>
* <span data-ttu-id="edee3-219">백업(예약된 백업 및 BackupNow 통해 요청된 백업 모두)</span><span class="sxs-lookup"><span data-stu-id="edee3-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="edee3-220">복원</span><span class="sxs-lookup"><span data-stu-id="edee3-220">Restore</span></span>
* <span data-ttu-id="edee3-221">보호 중지</span><span class="sxs-lookup"><span data-stu-id="edee3-221">Stop protection</span></span>
* <span data-ttu-id="edee3-222">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="edee3-222">Delete backup data</span></span>
* <span data-ttu-id="edee3-223">정책 추가</span><span class="sxs-lookup"><span data-stu-id="edee3-223">Add policy</span></span>
* <span data-ttu-id="edee3-224">정책 삭제</span><span class="sxs-lookup"><span data-stu-id="edee3-224">Delete policy</span></span>
* <span data-ttu-id="edee3-225">정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="edee3-225">Update policy</span></span>
* <span data-ttu-id="edee3-226">작업 취소</span><span class="sxs-lookup"><span data-stu-id="edee3-226">Cancel job</span></span>

<span data-ttu-id="edee3-227">백업 자격 증명 모음에 해당하는 작업 로그를 보려면</span><span class="sxs-lookup"><span data-stu-id="edee3-227">To view operation logs corresponding to a backup vault:</span></span>

1. <span data-ttu-id="edee3-228">Azure Portal에서 **관리 서비스**로 이동한 다음 **작업 로그** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-228">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span></span>

    ![작업 로그](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="edee3-230">필터에서 **백업**을 *형식*으로 선택하고 *서비스 이름*에서 백업 자격 증명 모음 이름을 지정한 다음 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-230">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span></span>

    ![작업 로그 필터](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="edee3-232">작업 로그에서 작업을 선택하고 **세부 정보**를 클릭하여 작업에 해당하는 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-232">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span></span>

    ![작업 로그 Fetching 세부 정보](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="edee3-234">**세부 정보 마법사** 는 트리거된 작업, 작업 ID, 이 작업은 트리거되는 리소스 및 작업의 시작 시간에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-234">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span></span>

    ![작업 세부 정보](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="edee3-236">경고 알림</span><span class="sxs-lookup"><span data-stu-id="edee3-236">Alert notifications</span></span>
<span data-ttu-id="edee3-237">포털에서 작업에 대한 사용자 지정 경고 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-237">You can get custom alert notifications for the jobs in portal.</span></span> <span data-ttu-id="edee3-238">작업 로그 이벤트에서 PowerShell 기반 경고 규칙을 정의하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="edee3-239">*PowerShell 버전 1.3.0 이상*을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="edee3-240">사용자 지정 알림을 정의하여 백업 실패에 대해 경고하려면 예제 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-240">To define a custom notification to alert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="edee3-241">**ResourceId**: 이 섹션에서 설명한 것처럼 작업 로그 팝업에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="edee3-242">작업의 세부 정보 팝업 창에서 ResourceUri는 이 cmdlet를 위해 제공된 ResourceId입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-242">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span></span>

<span data-ttu-id="edee3-243">**OperationName**: "Microsoft.Backup/backupvault/<EventName>" 형식이며, 여기서 EventName은 Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy 중하나입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-243">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="edee3-244">**상태**: 지원되는 값은 시작함, 성공함 및 실패함입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="edee3-245">**ResourceGroup**: 작업이 트리거되는 리소스의 ResourceGroup입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-245">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span></span> <span data-ttu-id="edee3-246">ResourceId 값에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="edee3-247">ResourceId 값에서 */resourceGroups/* 및 */providers/* 필드 사이의 값은 ResourceGroup의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span></span>

<span data-ttu-id="edee3-248">**이름**: 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-248">**Name**: Name of the Alert Rule.</span></span>

<span data-ttu-id="edee3-249">**CustomEmail**: 경고 알림을 보낼 사용자 지정 메일 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-249">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span></span>

<span data-ttu-id="edee3-250">**SendToServiceOwners**: 이 옵션은 구독의 모든 관리자 및 공동 관리자에게 경고 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-250">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="edee3-251">**New-AzureRmAlertRuleEmail** cmdlet에 사용될 수 있음</span><span class="sxs-lookup"><span data-stu-id="edee3-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="edee3-252">경고에 대한 제한</span><span class="sxs-lookup"><span data-stu-id="edee3-252">Limitations on Alerts</span></span>
<span data-ttu-id="edee3-253">이벤트 기반 경고는 다음과 같은 제한 사항에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-253">Event-based alerts are subjected to the following limitations:</span></span>

1. <span data-ttu-id="edee3-254">백업 자격 증명 모음의 모든 가상 컴퓨터에서 경고를 유발합니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-254">Alerts are triggered on all virtual machines in the backup vault.</span></span> <span data-ttu-id="edee3-255">이에 사용자 지정으로 백업 자격 증명 모음에서 가상 컴퓨터의 특정 집합에 대한 경고를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-255">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="edee3-256">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-256">This feature is in Preview.</span></span> [<span data-ttu-id="edee3-257">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="edee3-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="edee3-258">“alerts-noreply@mail.windowsazure.com”에서 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="edee3-259">현재는 전자 메일 보낸 사람을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edee3-259">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edee3-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edee3-260">Next steps</span></span>
* [<span data-ttu-id="edee3-261">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="edee3-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
