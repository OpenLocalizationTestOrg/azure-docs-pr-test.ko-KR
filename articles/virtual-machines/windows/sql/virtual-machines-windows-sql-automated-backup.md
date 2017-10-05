---
title: "SQL Server 2014 Azure Virtual Machines의 자동화된 백업 | Microsoft Docs"
description: "Azure에서 실행되는 SQL Server 2014 VMs의 자동화된 백업 기능에 대해 설명합니다. 이 문서는 Resource Manager를 사용하는 VMs에만 적용됩니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="7c16f-104">SQL Server 2014 Virtual Machines의 자동화된 백업(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7c16f-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c16f-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="7c16f-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="7c16f-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="7c16f-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="7c16f-107">자동화된 백업에서는 SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM의 모든 기존 및 새 데이터베이스에 대해 [Microsoft Azure에 대한 관리되는 백업](https://msdn.microsoft.com/library/dn449496.aspx) 을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="7c16f-108">이를 통해 지속형 Azure Blob 저장소를 활용하는 일반 데이터베이스 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="7c16f-109">자동화된 백업은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="7c16f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c16f-110">Prerequisites</span></span>
<span data-ttu-id="7c16f-111">자동화된 백업을 사용하려면 다음 필수 조건을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="7c16f-112">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="7c16f-112">**Operating System**:</span></span>

- <span data-ttu-id="7c16f-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7c16f-113">Windows Server 2012</span></span>
- <span data-ttu-id="7c16f-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7c16f-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="7c16f-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7c16f-115">Windows Server 2016</span></span>

<span data-ttu-id="7c16f-116">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="7c16f-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="7c16f-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="7c16f-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="7c16f-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="7c16f-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c16f-119">자동화된 백업은 SQL Server 2014에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="7c16f-120">SQL Server 2016을 사용하는 경우 자동화된 백업 v2를 사용하여 데이터베이스를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="7c16f-121">자세한 내용은 [SQL Server 2016 Virtual Machines의 자동화된 백업 v2](virtual-machines-windows-sql-automated-backup-v2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="7c16f-122">**데이터베이스 구성**:</span><span class="sxs-lookup"><span data-stu-id="7c16f-122">**Database configuration**:</span></span>

- <span data-ttu-id="7c16f-123">대상 데이터베이스는 전체 복구 모델을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="7c16f-124">전체 복구 모델이 백업에 미치는 영향에 대한 자세한 내용은 [전체 복구 모델에서 백업](https://technet.microsoft.com/library/ms190217.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="7c16f-125">대상 데이터베이스는 기본 SQL Server 인스턴스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="7c16f-126">SQL Server IaaS 확장은 명명된 인스턴스를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="7c16f-127">**Azure 배포 모델**:</span><span class="sxs-lookup"><span data-stu-id="7c16f-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="7c16f-128">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="7c16f-128">Resource Manager</span></span>

<span data-ttu-id="7c16f-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="7c16f-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="7c16f-130">[최신 Azure PowerShell 명령을 설치합니다](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="7c16f-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="7c16f-131">자동화된 백업은 SQL Server IaaS 에이전트 확장에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="7c16f-132">현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="7c16f-133">자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="7c16f-134">설정</span><span class="sxs-lookup"><span data-stu-id="7c16f-134">Settings</span></span>

<span data-ttu-id="7c16f-135">다음 표에서는 자동화된 백업에 대해 구성할 수 있는 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="7c16f-136">실제 구성 단계는 Azure 포털 또는 Azure Windows PowerShell 명령 사용 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="7c16f-137">설정</span><span class="sxs-lookup"><span data-stu-id="7c16f-137">Setting</span></span> | <span data-ttu-id="7c16f-138">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="7c16f-138">Range (Default)</span></span> | <span data-ttu-id="7c16f-139">설명</span><span class="sxs-lookup"><span data-stu-id="7c16f-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c16f-140">**자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="7c16f-140">**Automated Backup**</span></span> | <span data-ttu-id="7c16f-141">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="7c16f-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="7c16f-142">SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="7c16f-143">**보존 기간**</span><span class="sxs-lookup"><span data-stu-id="7c16f-143">**Retention Period**</span></span> | <span data-ttu-id="7c16f-144">1-30일(30일)</span><span class="sxs-lookup"><span data-stu-id="7c16f-144">1-30 days (30 days)</span></span> | <span data-ttu-id="7c16f-145">백업 보존 기간(일 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="7c16f-146">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="7c16f-146">**Storage Account**</span></span> | <span data-ttu-id="7c16f-147">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="7c16f-147">Azure storage account</span></span> | <span data-ttu-id="7c16f-148">Blob 저장소에 자동화된 백업 파일을 저장하기 위해 사용하여 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="7c16f-149">모든 백업 파일을 저장하려면 컨테이너를 이 위치에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="7c16f-150">백업 파일 명명 규칙에는 날짜, 시간 및 컴퓨터 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="7c16f-151">**암호화**</span><span class="sxs-lookup"><span data-stu-id="7c16f-151">**Encryption**</span></span> | <span data-ttu-id="7c16f-152">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="7c16f-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="7c16f-153">암호화 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-153">Enables or disables encryption.</span></span> <span data-ttu-id="7c16f-154">암호화를 사용하면 백업을 복원하는 데 사용되는 인증서가 동일한 명명 규칙을 사용하여 동일한 `automaticbackup` 컨테이너에 지정한 저장소 계정에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="7c16f-155">암호가 변경되면 해당 암호를 사용하여 새 인증서가 생성되지만 이전 인증서도 이전 백업의 복원을 위해 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="7c16f-156">**암호**</span><span class="sxs-lookup"><span data-stu-id="7c16f-156">**Password**</span></span> | <span data-ttu-id="7c16f-157">암호 텍스트</span><span class="sxs-lookup"><span data-stu-id="7c16f-157">Password text</span></span> | <span data-ttu-id="7c16f-158">암호화 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-158">A password for encryption keys.</span></span> <span data-ttu-id="7c16f-159">암호화를 사용하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="7c16f-160">암호화된 백업을 복원하기 위해서는 올바른 암호 및 백업을 수행할 때 사용한 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="7c16f-161">포털에서 구성</span><span class="sxs-lookup"><span data-stu-id="7c16f-161">Configuration in the Portal</span></span>

<span data-ttu-id="7c16f-162">Azure Portal을 사용하여 프로비전 중에 또는 기존 SQL Server 2014 VMs에 대해 자동화된 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="7c16f-163">새 VM</span><span class="sxs-lookup"><span data-stu-id="7c16f-163">New VMs</span></span>

<span data-ttu-id="7c16f-164">Azure Portal을 사용하여 Resource Manager 배포 모델에서 새 SQL Server 2014 Virtual Machine을 만들 때 자동화된 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="7c16f-165">**SQL Server 설정** 블레이드에서 **자동화된 백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="7c16f-166">다음 Azure 포털 스크린샷은 **SQL 자동화된 백업** 블레이드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Azure 포털에서 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="7c16f-168">컨텍스트의 경우 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)의 전체 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="7c16f-169">기존 VM</span><span class="sxs-lookup"><span data-stu-id="7c16f-169">Existing VMs</span></span>

<span data-ttu-id="7c16f-170">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="7c16f-171">그런 다음 **설정** 블레이드의 **SQL Server 구성** 섹션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![기존 VM에 대한 SQL 자동화된 백업](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="7c16f-173">**SQL Server 구성** 블레이드에서 자동화된 백업 섹션의 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![기존 VM에 대한 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="7c16f-175">완료되면 **SQL Server 구성** 블레이드 아래쪽의 **확인** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="7c16f-176">처음으로 자동화된 백업을 사용 설정할 경우 Azure에서 백그라운드로 SQL Server IaaS 에이전트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="7c16f-177">이 시간 동안에는 구성된 자동화된 백업이 Azure 포털에 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="7c16f-178">에이전트가 설치 및 구성될 때까지 몇 분 정도 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="7c16f-179">그 후 Azure 포털에는 새 설정이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="7c16f-180">또한 템플릿을 사용하여 자동화된 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="7c16f-181">자세한 내용은 [자동화된 백업에 대한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="7c16f-182">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="7c16f-182">Configuration with PowerShell</span></span>

<span data-ttu-id="7c16f-183">PowerShell을 사용하여 자동화된 백업을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="7c16f-184">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-184">Before you begin, you must:</span></span>

- <span data-ttu-id="7c16f-185">[최신 Azure PowerShell을 다운로드하여 설치합니다](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="7c16f-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="7c16f-186">Windows PowerShell을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="7c16f-187">이렇게 하려면 프로비전 관련 문서의 [구독 구성](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) 섹션에서 설명하는 단계를 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="7c16f-188">SQL IaaS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="7c16f-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="7c16f-189">Azure Portal에서 SQL Server 가상 컴퓨터를 프로비전한 경우 SQL Server IaaS 확장이 이미 설치되어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="7c16f-190">**Get-AzureRmVM** 명령을 실행하고 **Extensions** 속성을 검사하여 VM에 대해 해당 확장이 설치되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="7c16f-191">SQL Server IaaS 에이전트 확장이 설치되어 있는 경우 "SqlIaaSAgent" 또는 "SQLIaaSExtension"으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="7c16f-192">확장에 대한 **ProvisioningState**가 "Succeeded"로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="7c16f-193">설치되지 않았거나 프로비전되지 못한 경우 다음 명령을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="7c16f-194">VM 이름 및 리소스 그룹 외에, VM이 있는 하위 지역(**$region**)도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="7c16f-195"><a id="verifysettings"></a> 현재 설정 확인</span><span class="sxs-lookup"><span data-stu-id="7c16f-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="7c16f-196">프로비전 동안 자동화된 백업을 사용하도록 설정한 경우 PowerShell을 사용하여 현재 구성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="7c16f-197">**Get-AzureRmVMSqlServerExtension** 명령을 실행하고 **AutoBackupSettings** 속성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="7c16f-198">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="7c16f-199">출력에 **Enable**이 **False**로 설정되어 표시되면 자동화된 백업을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="7c16f-200">다행히도 자동화된 백업도 같은 방식으로 사용하도록 설정하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="7c16f-201">이 정보에 대해서는 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="7c16f-202">변경을 수행한 후에 설정을 바로 확인하면 이전 구성 값을 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="7c16f-203">몇 분 정도 기다렸다가 설정을 다시 확인하여 변경 내용이 적용되었는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="7c16f-204">자동화된 백업 구성</span><span class="sxs-lookup"><span data-stu-id="7c16f-204">Configure Automated Backup</span></span>
<span data-ttu-id="7c16f-205">언제든지 PowerShell을 사용하여 자동화된 백업을 사용하도록 설정하고 해당 구성 및 동작을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="7c16f-206">먼저 백업 파일에 대한 저장소 계정을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="7c16f-207">다음 스크립트는 저장소 계정을 선택하거나 없으면 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-207">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="7c16f-208">자동화된 백업을 사용할 경우 프리미엄 저장소에 백업을 저장할 수 없지만 프리미엄 저장소를 사용하는 VM 디스크에서 백업을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="7c16f-209">그런 후 **New-AzureRmVMSqlServerAutoBackupConfig** 명령을 통해 자동화된 백업 설정을 사용하도록 지정하고 Azure Storage 계정에 백업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="7c16f-210">이 예제에서는 백업이 10일 동안 보관되도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="7c16f-211">두 번째 명령인 **Set-AzureRmVMSqlServerExtension**은 지정된 Azure VM을 이러한 설정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="7c16f-212">SQL Server IaaS 에이전트를 설치하고 구성하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="7c16f-213">SQL Server 2016 및 자동화된 백업 v2에만 적용되는 **New-AzureRmVMSqlServerAutoBackupConfig**에 대한 다른 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="7c16f-214">SQL Server 2014에서는 **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours** 및 **LogBackupFrequencyInMinutes** 설정을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="7c16f-215">SQL Server 2014 가상 컴퓨터에서 이러한 설정을 구성하려고 하면 오류는 발생하지 않지만 설정이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="7c16f-216">SQL Server 2016 가상 컴퓨터에서 이러한 설정을 사용하려면 [SQL Server 2016 Azure Virtual Machines용 자동화된 백업 v2](virtual-machines-windows-sql-automated-backup-v2.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="7c16f-217">암호화를 사용하려면 **CertificatePassword** 매개 변수에 대 한 암호(보안 문자열)와 함께 **EnableEncryption** 매개 변수를 전달 하도록 이전 스크립트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="7c16f-218">다음 스크립트를 사용하면 이전 예제의 자동화된 백업 설정을 사용하고 암호화를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="7c16f-219">설정이 적용되었는지 확인하려면 [자동화된 백업 구성을 확인](#verifysettings)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="7c16f-220">자동화된 백업 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="7c16f-220">Disable Automated Backup</span></span>

<span data-ttu-id="7c16f-221">자동화된 백업을 사용하지 않도록 설정하려면 동일한 스크립트를 **-Enable** 매개 변수 없이 **New-AzureRmVMSqlServerAutoBackupConfig** 명령에 대해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="7c16f-222">**-Enable** 매개 변수가 없는 경우 기능을 해제하는 명령을 신호로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="7c16f-223">설치와 마찬가지로 자동화된 백업을 사용하지 않도록 설정하는 데도 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="7c16f-224">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="7c16f-224">Example script</span></span>

<span data-ttu-id="7c16f-225">다음 스크립트는 VM에 대해 자동화된 백업을 사용하도록 설정하고 구성하기 위해 사용자 지정할 수 있는 변수 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="7c16f-226">사용자의 경우 요구 사항에 따라 스크립트를 사용자 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="7c16f-227">예를 들어 시스템 데이터베이스의 백업을 사용하지 않도록 설정하거나 암호화를 사용하도록 설정하려는 경우 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="7c16f-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c16f-228">Next steps</span></span>

<span data-ttu-id="7c16f-229">자동화된 백업은 Azure VM에서 관리되는 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="7c16f-230">따라서 [관리되는 백업 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) 하여 동작 및 의미를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c16f-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="7c16f-231">Azure VM의 SQL Server에 대한 추가적인 백업 및 복원 지침은 [Azure 가상 컴퓨터의 SQL Server 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="7c16f-232">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="7c16f-233">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c16f-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

