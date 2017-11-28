---
title: "Azure 클래식 배포 모델을 사용하여 Azure 백업 자격 증명 모음 및 서버 관리 | Microsoft Docs"
description: "이 자습서를 사용하여 Azure 백업 저장소 및 서버를 관리하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="5e49e-103">클래식 배포 모델을 사용하여 Azure 백업 자격 증명 모음 및 서버 관리</span><span class="sxs-lookup"><span data-stu-id="5e49e-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e49e-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="5e49e-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="5e49e-105">클래식</span><span class="sxs-lookup"><span data-stu-id="5e49e-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="5e49e-106">이 문서에서는 Azure 클래식 포털 및 Microsoft Azure 백업 에이전트를 통해 사용할 수 있는 백업 관리 작업의 개요를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e49e-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5e49e-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5e49e-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e49e-110">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="5e49e-111">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e49e-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="5e49e-112">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="5e49e-113">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="5e49e-114">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="5e49e-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="5e49e-115">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="5e49e-116">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="5e49e-117">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="5e49e-118">관리 포털 작업</span><span class="sxs-lookup"><span data-stu-id="5e49e-118">Management portal tasks</span></span>
1. <span data-ttu-id="5e49e-119">[관리 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5e49e-120">**복구 서비스**를 클릭한 후 백업 저장소의 이름을 클릭하여 빠른 시작 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![복구 서비스](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="5e49e-122">빠른 시작 페이지의 위쪽에 있는 옵션을 선택하여 사용 가능한 관리 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![관리 탭](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="5e49e-124">대시보드</span><span class="sxs-lookup"><span data-stu-id="5e49e-124">Dashboard</span></span>
<span data-ttu-id="5e49e-125">**대시보드**를 선택하여 서버의 사용 개요를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="5e49e-126">**사용 개요**에는 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="5e49e-127">클라우드에 등록된 Windows Server 수</span><span class="sxs-lookup"><span data-stu-id="5e49e-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="5e49e-128">클라우드에서 보호되는 Azure 가상 컴퓨터 수</span><span class="sxs-lookup"><span data-stu-id="5e49e-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="5e49e-129">Azure에서 사용된 총 저장소</span><span class="sxs-lookup"><span data-stu-id="5e49e-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="5e49e-130">최근 작업의 상태</span><span class="sxs-lookup"><span data-stu-id="5e49e-130">The status of recent jobs</span></span>

<span data-ttu-id="5e49e-131">대시보드 아래쪽에서 수행할 수 있는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="5e49e-132">**인증서 관리** - 서버를 등록하는 데 인증서가 사용된 경우 이 옵션을 통해 인증서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="5e49e-133">저장소 자격 증명을 사용하는 경우에는 **인증서 관리**를 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="5e49e-134">**삭제** - 현재 백업 저장소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="5e49e-135">백업 저장소가 더 이상 사용되지 않는 경우 삭제하여 저장소 공간을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="5e49e-136">**삭제**는 등록된 모든 서버가 저장소에서 삭제된 후에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![백업 대시보드 작업](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="5e49e-138">등록된 항목</span><span class="sxs-lookup"><span data-stu-id="5e49e-138">Registered items</span></span>
<span data-ttu-id="5e49e-139">**등록된 항목**을 선택하여 이 저장소에 등록된 서버의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![등록된 항목](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="5e49e-141">**형식** 필터는 기본적으로 Azure 가상 컴퓨터로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="5e49e-142">이 자격 증명 모음에 등록된 서버의 이름을 확인하려면 드롭다운 메뉴에서 **Windows Server**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="5e49e-143">여기서 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="5e49e-144">**다시 등록 허용** - 서버에 이 옵션이 선택된 경우 온-프레미스 Microsoft Azure Backup 에이전트에서 **등록 마법사**를 사용하여 백업 저장소에 서버를 다시 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="5e49e-145">인증서 오류로 인해 또는 서버를 다시 빌드해야 한 경우 다시 등록해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="5e49e-146">**삭제** - 백업 저장소에서 서버를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="5e49e-147">서버와 관련해서 저장된 모든 데이터가 즉시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![등록된 항목 작업](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="5e49e-149">보호된 항목</span><span class="sxs-lookup"><span data-stu-id="5e49e-149">Protected items</span></span>
<span data-ttu-id="5e49e-150">**보호된 항목**을 선택하여 서버에서 백업된 항목을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![보호된 항목](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="5e49e-152">구성</span><span class="sxs-lookup"><span data-stu-id="5e49e-152">Configure</span></span>
<span data-ttu-id="5e49e-153">**구성** 탭에서 적절한 저장소 중복 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="5e49e-154">저장소 중복 옵션을 선택하기에 가장 좋은 시기는 자격 증명 모음을 만든 후 자격 증명 모음에 컴퓨터를 등록하기 바로 직전입니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="5e49e-155">항목이 자격 증명 모음에 등록되고 나면 저장소 중복 옵션 잠기고 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![구성](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="5e49e-157">[저장소 중복](../storage/common/storage-redundancy.md)에 대한 자세한 내용은 이 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e49e-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="5e49e-158">Microsoft Azure 백업 에이전트 작업</span><span class="sxs-lookup"><span data-stu-id="5e49e-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="5e49e-159">콘솔</span><span class="sxs-lookup"><span data-stu-id="5e49e-159">Console</span></span>
<span data-ttu-id="5e49e-160">**Microsoft Azure 백업 에이전트**를 엽니다(*Microsoft Azure 백업*에 대한 컴퓨터를 검색하여 찾을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="5e49e-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![백업 에이전트](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="5e49e-162">백업 에이전트 콘솔의 오른쪽에 있는 **작업**에서 다음 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="5e49e-163">서버 등록</span><span class="sxs-lookup"><span data-stu-id="5e49e-163">Register Server</span></span>
* <span data-ttu-id="5e49e-164">백업 예약</span><span class="sxs-lookup"><span data-stu-id="5e49e-164">Schedule Backup</span></span>
* <span data-ttu-id="5e49e-165">지금 백업</span><span class="sxs-lookup"><span data-stu-id="5e49e-165">Back Up now</span></span>
* <span data-ttu-id="5e49e-166">속성 변경</span><span class="sxs-lookup"><span data-stu-id="5e49e-166">Change Properties</span></span>

![에이전트 콘솔 작업](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="5e49e-168">**데이터를 복구**하려면 [Windows 서버 또는 Windows 클라이언트 컴퓨터로 파일 복원](backup-azure-restore-windows-server.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e49e-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="5e49e-169">기존 백업 수정</span><span class="sxs-lookup"><span data-stu-id="5e49e-169">Modify an existing backup</span></span>
1. <span data-ttu-id="5e49e-170">Microsoft Azure 백업 에이전트에서 **백업 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="5e49e-172">**백업 예약 마법사**에서 **백업 항목 또는 시간 변경** 옵션을 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![예약된 백업 수정](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="5e49e-174">항목을 추가하거나 변경하려면 **백업할 항목 선택** 화면에서 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="5e49e-175">마법사의 이 페이지에서 **제외 설정**을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="5e49e-176">파일 또는 파일 형식을 제외하려면 [제외 설정](#exclusion-settings)추가 절차를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="5e49e-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="5e49e-177">백업할 파일 및 폴더를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![항목 추가](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="5e49e-179">**백업 일정**을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="5e49e-180">매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![백업 일정 변경](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="5e49e-182">백업 일정을 지정하는 방법은 [문서](backup-azure-backup-cloud-as-tape.md)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="5e49e-183">백업 복사본에 대한 **재방문 주기 정책**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![재방문 주기 정책 선택](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="5e49e-185">**확인** 화면에서 정보를 검토하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="5e49e-186">마법사가 **백업 일정** 생성을 완료하면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="5e49e-187">보호를 수정한 후 **작업** 탭으로 이동해 변경 내용이 백업 작업에 반영되는지 확인하여 백업이 올바르게 트리거되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="5e49e-188">네트워크 제한 사용</span><span class="sxs-lookup"><span data-stu-id="5e49e-188">Enable Network Throttling</span></span>
<span data-ttu-id="5e49e-189">Azure 백업 에이전트는 데이터 전송 중에 네트워크 대역폭이 사용되는 방식을 제어할 수 있는 제한 탭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="5e49e-190">근무 시간에 데이터를 백업해야 하는데 백업 프로세스가 다른 인터넷 트래픽을 방해하지 말아야 할 때 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="5e49e-191">데이터 전송 제한은 백업 및 복원 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="5e49e-192">제한을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="5e49e-192">To enable throttling:</span></span>

1. <span data-ttu-id="5e49e-193">**백업 에이전트**에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="5e49e-194">**백업 작업에 인터넷 대역폭 사용 제한 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![네트워크 제한](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="5e49e-196">제한을 사용하도록 설정했으면 **근무 시간** 및 **휴무 시간** 중에 백업 데이터 전송에 허용되는 대역폭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="5e49e-197">대역폭 값은 초당 512Kb(Kbps)에서 시작하여 최대 초당 1023Mb(Mbps)까지 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="5e49e-198">또한 **근무 시간**의 시작 및 완료 시간과 근무일로 간주되는 요일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="5e49e-199">지정된 근무 시간 이외의 시간은 휴무 시간으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="5e49e-200">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="5e49e-201">제외 설정</span><span class="sxs-lookup"><span data-stu-id="5e49e-201">Exclusion settings</span></span>
1. <span data-ttu-id="5e49e-202">**Microsoft Azure 백업 에이전트**를 엽니다(*Microsoft Azure 백업*에 대한 컴퓨터를 검색하여 찾을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="5e49e-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![백업 에이전트 열기](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="5e49e-204">Microsoft Azure 백업 에이전트에서 **백업 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="5e49e-206">백업 예약 마법사에서 **백업 항목 또는 시간 변경** 옵션을 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![일정 수정](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="5e49e-208">**제외 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-208">Click **Exclusions Settings**.</span></span>

    ![제외할 항목 선택](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="5e49e-210">**제외 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-210">Click **Add Exclusion**.</span></span>

    ![제외 추가](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="5e49e-212">위치를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-212">Select the location and then, click **OK**.</span></span>

    ![제외할 위치 선택](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="5e49e-214">**파일 형식** 필드에서 파일 확장명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-214">Add the file extension in the **File Type** field.</span></span>

    ![파일 형식별 제외](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="5e49e-216">.mp3 확장명 추가</span><span class="sxs-lookup"><span data-stu-id="5e49e-216">Adding an .mp3 extension</span></span>

    ![파일 형식 예](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="5e49e-218">다른 확장명을 추가하려면 **제외 추가**를 클릭하고 다른 파일 형식 확장명(.jpeg 확장명 추가)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![다른 파일 형식 예](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="5e49e-220">모든 확장을 추가했으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="5e49e-221">**확인 페이지**가 나타날 때까지 **다음**을 클릭하여 백업 예약 마법사를 계속 진행한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e49e-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![제외 확인](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="5e49e-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e49e-223">Next steps</span></span>
* [<span data-ttu-id="5e49e-224">Azure에서 Windows Server 또는 Windows 클라이언트 복원</span><span class="sxs-lookup"><span data-stu-id="5e49e-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="5e49e-225">Azure 백업에 대한 자세한 내용은 [Azure 백업 개요](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="5e49e-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="5e49e-226">[Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="5e49e-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
