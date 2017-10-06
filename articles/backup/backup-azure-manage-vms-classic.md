---
title: "Azure 가상 컴퓨터 백업을 aaaManage 및 모니터 | Microsoft Docs"
description: "어떻게 toomanage 모니터 Azure 가상 컴퓨터 및 백업에 알아봅니다"
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
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="1becd-103">일반적인 Azure 백업 작업 및 hello 클래식 포털에서 트리거 경고 관리</span><span class="sxs-lookup"><span data-stu-id="1becd-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1becd-104">Azure VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="1becd-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="1becd-105">클래식 VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="1becd-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="1becd-106">이 문서에서는 Azure에서 보호되는 클랙식 모델 가상 컴퓨터에 대한 일반적인 관리 및 모니터링 관련 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="1becd-107">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1becd-108">참조 [Azure 가상 컴퓨터를 사용자 환경 tooback 준비](backup-azure-vms-prepare.md) 클래식 배포 작업에 대 한 자세한 내용은 Vm을 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="1becd-109">2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="1becd-110">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="1becd-111">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="1becd-112">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="1becd-113">2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="1becd-114">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="1becd-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="1becd-115">모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="1becd-116">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="1becd-117">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="1becd-118">보호된 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="1becd-118">Manage protected virtual machines</span></span>
<span data-ttu-id="1becd-119">toomanage 보호 되는 가상 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="1becd-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="1becd-120">tooview hello를 클릭 하는 가상 컴퓨터에 대 한 백업 설정을 관리 하 고 **보호 된 항목** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="1becd-121">보호 된 항목 toosee hello의 hello 이름을 클릭 **백업 세부 정보** hello 마지막 백업에 대 한 정보를 보여 주는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![가상 컴퓨터 백업](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="1becd-123">tooview hello를 클릭 하는 가상 컴퓨터에 대 한 백업 정책 설정을 관리 하 고 **정책** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![가상 컴퓨터 정책](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="1becd-125">hello **백업 정책** 기존 정책을 hello 표시를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="1becd-126">필요에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-126">You can modify as needed.</span></span> <span data-ttu-id="1becd-127">새 정책 toocreate 필요 하면 클릭 **만들기** hello에 **정책** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1becd-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="1becd-128">Note 하 tooremove 하려는 경우 정책을 안는 연결 된 모든 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="1becd-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![가상 컴퓨터 정책](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="1becd-130">가상 컴퓨터 hello에 대 한 작업 또는 상태에 대 한 자세한 정보를 얻을 수 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1becd-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="1becd-131">자세한 내용은 또는 특정 가상 컴퓨터에 대 한 작업을 필터링 hello 목록 tooget에서 작업을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![작업](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="1becd-133">가상 컴퓨터의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="1becd-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="1becd-134">보호를 위해 구성한 후에는 가상 컴퓨터의 주문형 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="1becd-135">Hello 초기 백업을 보류 중인 경우 hello 가상 컴퓨터에 대 한 주문형 백업 복사본이 생성 됩니다. 전체 hello 가상 컴퓨터의 Azure 백업 자격 증명 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="1becd-136">첫 번째 백업이 완료 되 면 경우 주문형으로 백업 됩니다 송신 변경 내용을 이전 백업 tooAzure 백업에서 자격 증명 모음, 즉 것만 항상 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="1becd-137">요청 시 백업의 보존 범위 백업 정책 해당 toohello VM 매일 보존 기간에 대해 지정 된 tooretention 값으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="1becd-138">가상 컴퓨터의 주문형 tootake 백업:</span><span class="sxs-lookup"><span data-stu-id="1becd-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="1becd-139">Toohello 이동 **보호 된 항목** 페이지를 선택 **Azure 가상 컴퓨터** 으로 **형식** (아직 선택 되지 않은) 하는 경우 클릭 하 고 **선택**단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="1becd-141">Hello 가상 컴퓨터를 주문형 tootake 백업을 클릭할 선택 **지금 백업** hello hello 페이지 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![지금 백업](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="1becd-143">이렇게 하면 선택한 hello 가상 컴퓨터에서 백업 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="1becd-144">이 작업을 통해 생성 되는 복구 지점의 보존 범위는 hello 가상 컴퓨터와 연결 된 hello 정책에 지정 된 것과 동일한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![백업 작업 만들기](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="1becd-146">hello에 가상 컴퓨터에 가상 컴퓨터를 드릴 다운 연관 tooview hello 정책 **보호 된 항목** 페이지와 이동 toobackup 정책 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="1becd-147">Hello 작업을 만든 후 클릭 **작업 보기** hello 알림 toosee hello hello 작업 페이지에서 해당 작업 표시줄에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![백업 작업 생성됨](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="1becd-149">Hello 작업을 성공적으로 완료 한 후는 복구 지점이 생성 될 수 있는 toorestore hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="1becd-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="1becd-150">이 또한 hello 복구 지점 열 값 1 씩에 **보호 된 항목** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1becd-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="1becd-151">가상 컴퓨터 보호 중지</span><span class="sxs-lookup"><span data-stu-id="1becd-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="1becd-152">다음 옵션 hello로 toostop hello 나중에 백업이 가상 컴퓨터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="1becd-153">Azure 백업 자격 증명 모음에 가상 컴퓨터와 연결된 백업 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="1becd-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="1becd-154">가상 컴퓨터와 연결된 백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="1becd-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="1becd-155">가상 컴퓨터와 연결 된 tooretain 백업 데이터를 선택한 경우에 hello 백업 데이터 toorestore hello 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="1becd-156">이러한 가상 컴퓨터의 가격 정보를 보려면 [여기](https://azure.microsoft.com/pricing/details/backup/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="1becd-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="1becd-157">가상 컴퓨터에 대 한 tooStop 보호:</span><span class="sxs-lookup"><span data-stu-id="1becd-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="1becd-158">너무 이동**보호 된 항목** 페이지로 돌아간 후 선택 **Azure 가상 컴퓨터** hello 필터 형식 (아직 선택 되지 않은) 하는 경우 클릭으로 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="1becd-160">Hello 가상 컴퓨터를 선택 하 고 클릭 **보호 중지** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![보호 중지](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="1becd-162">기본적으로 Azure 백업 삭제 되지 않습니다 hello 가상 컴퓨터와 연결 된 hello 백업 데이터.</span><span class="sxs-lookup"><span data-stu-id="1becd-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![보호 중지 확인](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="1becd-164">Toodelete 백업 데이터를 원하는 경우 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-164">If you want toodelete backup data, select hello check box.</span></span>

    ![확인란](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="1becd-166">Hello 백업 중지 이유를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1becd-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="1becd-167">선택 사항 이지만는 이유를 입력 및 데 도움이 되 hello 피드백에 Azure 백업 toowork hello 고객 시나리오 우선 순위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="1becd-168">클릭 **전송** 단추 toosubmit hello **보호를 중지** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="1becd-169">클릭 **작업 보기** toosee hello에 해당 하는 hello 작업이 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1becd-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![보호 중지](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="1becd-171">선택 하지 않은 경우 **연결 된 백업 데이터 삭제** 중 옵션 **보호 중지** post 작업 완료, 그런 다음 마법사를 보호 상태가 너무 변경**보호가 중지**.</span><span class="sxs-lookup"><span data-stu-id="1becd-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="1becd-172">hello 데이터 명시적으로 삭제 될 때까지 Azure 백업으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="1becd-173">Hello에 hello 가상 컴퓨터를 선택 하 여 항상 hello 데이터를 삭제할 수 있습니다 **보호 된 항목** 페이지를 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![보호 중지됨](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="1becd-175">Hello를 선택한 경우 **연결 된 백업 데이터 삭제** 옵션, hello 가상 컴퓨터에 포함 되지 hello **보호 된 항목** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1becd-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="1becd-176">가상 컴퓨터 다시 보호</span><span class="sxs-lookup"><span data-stu-id="1becd-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="1becd-177">Hello를 선택 하지 않은 경우 **백업 데이터를 연결 하는 삭제** 옵션을 **보호 중지**를 수행 하 여 hello 가상 컴퓨터를 다시 보호할 수를 hello 단계 비슷한 toobacking 가상 등록 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="1becd-178">보호를이 가상 컴퓨터 보관 되는 백업 데이터 이전 toostop protection 고 복구 지점 이후에 생성 되 면 다시 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="1becd-179">다시 보호 한 후 hello 가상 컴퓨터의 보호 상태가 변경 됩니다 너무**Protected** 지점이 있는 경우 복구 이전 너무**보호 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![다시 보호된 VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="1becd-181">Hello 가상 컴퓨터를 다시 보호 된 가상 컴퓨터를 보호 처음 hello 정책 보다 다른 정책을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="1becd-182">가상 컴퓨터 등록 취소</span><span class="sxs-lookup"><span data-stu-id="1becd-182">Unregister virtual machines</span></span>
<span data-ttu-id="1becd-183">하려는 경우 hello 백업 자격 증명 모음에서 tooremove hello 가상 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="1becd-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="1becd-184">Hello 클릭 **등록 취소** hello hello 페이지 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![보호 사용 안 함](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="1becd-186">알림 메시지는 hello 확인을 요청 하는 hello 화면 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="1becd-187">클릭 **예** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-187">Click **YES** toocontinue.</span></span>

    ![보호 사용 안 함](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="1becd-189">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="1becd-189">Delete Backup data</span></span>
<span data-ttu-id="1becd-190">하거나 가상 컴퓨터와 연결 된 hello 백업 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="1becd-191">보호 중지 작업 중</span><span class="sxs-lookup"><span data-stu-id="1becd-191">During Stop Protection Job</span></span>
* <span data-ttu-id="1becd-192">가상 컴퓨터에서 보호 중지 작업이 완료된 후</span><span class="sxs-lookup"><span data-stu-id="1becd-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="1becd-193">hello에 있는 가상 컴퓨터에서 백업 데이터 toodelete *보호가 중지* 상태 게시 성공적으로 완료 한 **백업 중지** 작업:</span><span class="sxs-lookup"><span data-stu-id="1becd-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="1becd-194">Toohello 이동 **보호 된 항목** 페이지를 선택 **Azure 가상 컴퓨터** 으로 *형식* hello 클릭 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="1becd-196">Hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-196">Select hello virtual machine.</span></span> <span data-ttu-id="1becd-197">hello 가상 컴퓨터에 포함 됩니다 **보호가 중지** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![보호 중지됨](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="1becd-199">Hello 클릭 **삭제** hello hello 페이지 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![백업 삭제](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="1becd-201">Hello에 **백업 데이터를 삭제** 마법사 (권장 사항) 백업 데이터를 삭제 하기 위한 이유를 선택 하 고 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![백업 데이터 삭제](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="1becd-203">그러면 선택한 가상 컴퓨터의 작업 toodelete 백업 데이터를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="1becd-204">클릭 **작업 보기** toosee 작업 페이지에서 해당 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![데이터 삭제 성공](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="1becd-206">Hello 작업이 완료 되 면 해당 toohello 가상 컴퓨터에서 제거할 항목 hello **보호 된 항목** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1becd-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="1becd-207">대시보드</span><span class="sxs-lookup"><span data-stu-id="1becd-207">Dashboard</span></span>
<span data-ttu-id="1becd-208">Hello에 **대시보드** 페이지 Azure 가상 컴퓨터, 저장소 및에 관련 된 hello 지난 24 시간 동안 작업에 대 한 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="1becd-209">백업 상태 및 연결된 백업 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-209">You can view backup status and any associated backup errors.</span></span>

![대시보드](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="1becd-211">Hello 대시보드의 값은 24 시간 마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="1becd-212">작업 감사</span><span class="sxs-lookup"><span data-stu-id="1becd-212">Auditing Operations</span></span>
<span data-ttu-id="1becd-213">Azure 백업 "작업" 작업 로그를 백업 쉽게 toosee hello 백업 자격 증명 모음에 대해 어떤 관리 작업이 정확 하 게 만드는 hello 고객에 의해 트리거되 hello에 대 한 검토를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="1becd-214">작업 로그 훌륭한 사후를 사용 하도록 설정 하 고 hello 백업 작업에 대 한 지원을 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="1becd-215">작업을 수행 하는 hello 작업 로그에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="1becd-216">등록</span><span class="sxs-lookup"><span data-stu-id="1becd-216">Register</span></span>
* <span data-ttu-id="1becd-217">등록 취소</span><span class="sxs-lookup"><span data-stu-id="1becd-217">Unregister</span></span>
* <span data-ttu-id="1becd-218">보호 구성</span><span class="sxs-lookup"><span data-stu-id="1becd-218">Configure protection</span></span>
* <span data-ttu-id="1becd-219">백업(예약된 백업 및 BackupNow 통해 요청된 백업 모두)</span><span class="sxs-lookup"><span data-stu-id="1becd-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="1becd-220">복원</span><span class="sxs-lookup"><span data-stu-id="1becd-220">Restore</span></span>
* <span data-ttu-id="1becd-221">보호 중지</span><span class="sxs-lookup"><span data-stu-id="1becd-221">Stop protection</span></span>
* <span data-ttu-id="1becd-222">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="1becd-222">Delete backup data</span></span>
* <span data-ttu-id="1becd-223">정책 추가</span><span class="sxs-lookup"><span data-stu-id="1becd-223">Add policy</span></span>
* <span data-ttu-id="1becd-224">정책 삭제</span><span class="sxs-lookup"><span data-stu-id="1becd-224">Delete policy</span></span>
* <span data-ttu-id="1becd-225">정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="1becd-225">Update policy</span></span>
* <span data-ttu-id="1becd-226">작업 취소</span><span class="sxs-lookup"><span data-stu-id="1becd-226">Cancel job</span></span>

<span data-ttu-id="1becd-227">tooview 작업이 해당 tooa 백업 자격 증명 모음을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="1becd-228">너무 이동**관리 서비스** Azure 포털에서 다음 hello를 클릭 하 고 **작업 로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![작업 로그](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="1becd-230">Hello 필터 선택 **백업** 으로 *형식* hello 백업 자격 증명 모음 이름을 지정 하 고 *서비스 이름* 을 클릭할 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![작업 로그 필터](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="1becd-232">Hello 작업 로그에서 모든 작업을 선택 하 고 클릭 **세부 정보** toosee 해당 tooan 작업에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![작업 로그 Fetching 세부 정보](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="1becd-234">hello **세부 정보 마법사** hello 작업, 작업 Id, 된 리소스를이 작업을 트리거할 hello 작업의 시작 시간에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![작업 세부 정보](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="1becd-236">경고 알림</span><span class="sxs-lookup"><span data-stu-id="1becd-236">Alert notifications</span></span>
<span data-ttu-id="1becd-237">Hello 작업에 대 한 사용자 지정 경고 알림을 포털에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="1becd-238">작업 로그 이벤트에서 PowerShell 기반 경고 규칙을 정의하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="1becd-239">*PowerShell 버전 1.3.0 이상*을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="1becd-240">백업 실패에 대 한 사용자 지정 알림 tooalert toodefine 샘플 명령은 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="1becd-241">**ResourceId**: 이 섹션에서 설명한 것처럼 작업 로그 팝업에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="1becd-242">ResourceUri 작업의 정보 팝업 창에서이 cmdlet에 제공 된 hello ResourceId toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="1becd-243">**OperationName**: hello 형식의 됩니다 "Microsoft.Backup/backupvault/<EventName>" 여기서 EventName는 레지스터, 등록 취소, ConfigureProtection, 백업, 복원, StopProtection, DeleteBackupData, 중 하나 CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="1becd-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="1becd-244">**상태**: 지원되는 값은 시작함, 성공함 및 실패함입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="1becd-245">**ResourceGroup**: 작업이 트리거되면 hello 리소스의 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="1becd-246">ResourceId 값에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="1becd-247">값 필드 간의 */resourceGroups/* 및 */providers/* ResourceId 값은 리소스 그룹에 대 한 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="1becd-248">**이름**: hello 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="1becd-249">**CustomEmail**: hello 사용자 지정 전자 메일 주소 toowhich toosend 경고 알림을 지정</span><span class="sxs-lookup"><span data-stu-id="1becd-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="1becd-250">**SendToServiceOwners**:이 옵션 경고 알림 tooall 관리자와 hello 구독의 공동 관리자를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="1becd-251">**New-AzureRmAlertRuleEmail** cmdlet에 사용될 수 있음</span><span class="sxs-lookup"><span data-stu-id="1becd-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="1becd-252">경고에 대한 제한</span><span class="sxs-lookup"><span data-stu-id="1becd-252">Limitations on Alerts</span></span>
<span data-ttu-id="1becd-253">이벤트 기반 경고는 다음과 같은 제한을 거쳐야 toohello:</span><span class="sxs-lookup"><span data-stu-id="1becd-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="1becd-254">Hello 백업 자격 증명 모음에 있는 모든 가상 컴퓨터에 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="1becd-255">사용자 지정할 수 것 백업 자격 증명 모음에 있는 가상 컴퓨터의 특정 집합에 대 한 tooget 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="1becd-256">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-256">This feature is in Preview.</span></span> [<span data-ttu-id="1becd-257">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="1becd-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="1becd-258">“alerts-noreply@mail.windowsazure.com”에서 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="1becd-259">현재 hello 전자 메일 보낸 사람을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1becd-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1becd-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1becd-260">Next steps</span></span>
* [<span data-ttu-id="1becd-261">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="1becd-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
