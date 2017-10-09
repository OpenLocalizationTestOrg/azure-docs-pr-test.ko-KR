---
title: "aaaAutomated 백업에 대 한 SQL Server 2014 Azure 가상 컴퓨터 | Microsoft Docs"
description: "Azure에서 실행 중인 SQL Server 2014 Vm에 대 한 hello 자동화 된 백업 기능에 설명 합니다. 이 문서는 hello 리소스 관리자를 사용 하 여 특정 tooVMs입니다."
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="3a24b-104">SQL Server 2014 Virtual Machines의 자동화된 백업(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="3a24b-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a24b-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="3a24b-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="3a24b-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="3a24b-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="3a24b-107">자동화 된 백업에서 자동으로 구성 [Azure 관리 되는 백업 tooMicrosoft](https://msdn.microsoft.com/library/dn449496.aspx) 모든 기존 및 새 데이터베이스를 SQL Server 2014 Standard 또는 Enterprise를 실행 하는 Azure VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="3a24b-108">그러면 지속 Azure blob 저장소를 사용 하는 tooconfigure 정기적 데이터베이스 백업을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="3a24b-109">자동화 된 백업 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="3a24b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3a24b-110">Prerequisites</span></span>
<span data-ttu-id="3a24b-111">자동화 된 백업 toouse hello 다음 필수 구성 요소를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="3a24b-112">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="3a24b-112">**Operating System**:</span></span>

- <span data-ttu-id="3a24b-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3a24b-113">Windows Server 2012</span></span>
- <span data-ttu-id="3a24b-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3a24b-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="3a24b-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3a24b-115">Windows Server 2016</span></span>

<span data-ttu-id="3a24b-116">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="3a24b-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="3a24b-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="3a24b-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="3a24b-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="3a24b-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a24b-119">자동화된 백업은 SQL Server 2014에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="3a24b-120">SQL Server 2016을 사용 하는 경우 자동화 된 백업 v2 tooback 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="3a24b-121">자세한 내용은 [SQL Server 2016 Virtual Machines의 자동화된 백업 v2](virtual-machines-windows-sql-automated-backup-v2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a24b-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="3a24b-122">**데이터베이스 구성**:</span><span class="sxs-lookup"><span data-stu-id="3a24b-122">**Database configuration**:</span></span>

- <span data-ttu-id="3a24b-123">대상 데이터베이스는 hello 전체 복구 모델을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="3a24b-124">자세한 내용은 hello 영향에 대 한 hello 전체 복구 모델의 백업에 [백업에서 hello 전체 복구 모델](https://technet.microsoft.com/library/ms190217.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="3a24b-125">대상 데이터베이스 hello 기본 SQL Server 인스턴스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="3a24b-126">SQL Server IaaS 확장 hello 명명 된 인스턴스를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="3a24b-127">**Azure 배포 모델**:</span><span class="sxs-lookup"><span data-stu-id="3a24b-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="3a24b-128">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="3a24b-128">Resource Manager</span></span>

<span data-ttu-id="3a24b-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="3a24b-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="3a24b-130">[설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview) tooconfigure PowerShell과 함께 자동화 된 백업 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a24b-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3a24b-131">자동화 된 백업을 SQL Server IaaS 에이전트 확장 hello에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="3a24b-132">현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="3a24b-133">자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a24b-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="3a24b-134">설정</span><span class="sxs-lookup"><span data-stu-id="3a24b-134">Settings</span></span>

<span data-ttu-id="3a24b-135">hello 다음 설명에 대 한 자동화 된 백업을 구성할 수 있는 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="3a24b-136">hello 실제 구성 단계는 hello Azure 포털 또는 Azure Windows PowerShell 명령을 사용 하는지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="3a24b-137">설정</span><span class="sxs-lookup"><span data-stu-id="3a24b-137">Setting</span></span> | <span data-ttu-id="3a24b-138">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="3a24b-138">Range (Default)</span></span> | <span data-ttu-id="3a24b-139">설명</span><span class="sxs-lookup"><span data-stu-id="3a24b-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a24b-140">**자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="3a24b-140">**Automated Backup**</span></span> | <span data-ttu-id="3a24b-141">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="3a24b-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="3a24b-142">SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="3a24b-143">**보존 기간**</span><span class="sxs-lookup"><span data-stu-id="3a24b-143">**Retention Period**</span></span> | <span data-ttu-id="3a24b-144">1-30일(30일)</span><span class="sxs-lookup"><span data-stu-id="3a24b-144">1-30 days (30 days)</span></span> | <span data-ttu-id="3a24b-145">hello 수 일 tooretain 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="3a24b-146">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="3a24b-146">**Storage Account**</span></span> | <span data-ttu-id="3a24b-147">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="3a24b-147">Azure storage account</span></span> | <span data-ttu-id="3a24b-148">Blob 저장소에 자동화 된 백업 파일을 저장 하기 위한 Azure 저장소 계정 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="3a24b-149">컨테이너는 모든 백업 파일에이 위치 toostore 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="3a24b-150">hello 날짜, 시간 및 컴퓨터 이름 hello 백업 파일 명명 규칙에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="3a24b-151">**암호화**</span><span class="sxs-lookup"><span data-stu-id="3a24b-151">**Encryption**</span></span> | <span data-ttu-id="3a24b-152">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="3a24b-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="3a24b-153">암호화 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-153">Enables or disables encryption.</span></span> <span data-ttu-id="3a24b-154">지정 된 hello에 hello 사용 되는 인증서 toorestore hello 백업 암호화를 사용 하는 경우 동일한 hello에 저장소 계정 `automaticbackup` ô ä ¢ hello 사용 하 여 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="3a24b-155">Hello 암호를 변경 하는 경우 해당 암호와 새 인증서가 생성 하지만 hello 이전 인증서 toorestore 이전 백업을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="3a24b-156">**암호**</span><span class="sxs-lookup"><span data-stu-id="3a24b-156">**Password**</span></span> | <span data-ttu-id="3a24b-157">암호 텍스트</span><span class="sxs-lookup"><span data-stu-id="3a24b-157">Password text</span></span> | <span data-ttu-id="3a24b-158">암호화 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-158">A password for encryption keys.</span></span> <span data-ttu-id="3a24b-159">암호화를 사용하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="3a24b-160">암호화 된 백업에서 순서 toorestore hello 올바른 암호와 hello 백업을 수행한 hello 시 사용 된 인증서 관련된 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="3a24b-161">Hello 포털의 구성</span><span class="sxs-lookup"><span data-stu-id="3a24b-161">Configuration in hello Portal</span></span>

<span data-ttu-id="3a24b-162">프로 비전 하는 동안 이나 기존 SQL Server 2014 Vm에 Azure 포털 tooconfigure 자동화 된 백업 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="3a24b-163">새 VM</span><span class="sxs-lookup"><span data-stu-id="3a24b-163">New VMs</span></span>

<span data-ttu-id="3a24b-164">Azure 포털 tooconfigure 자동화 된 백업 hello를 사용 하 여 hello 리소스 관리자 배포 모델에서 새 SQL Server 2014 가상 컴퓨터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="3a24b-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="3a24b-165">Hello에 **SQL Server 설정을** 블레이드를 **자동화 된 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="3a24b-166">hello 다음 Azure 포털 스크린샷은 hello **SQL 자동화 된 백업** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Azure 포털에서 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="3a24b-168">컨텍스트에 대해 hello 전체 항목에 참조 [Azure에서 SQL Server 가상 컴퓨터 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="3a24b-169">기존 VM</span><span class="sxs-lookup"><span data-stu-id="3a24b-169">Existing VMs</span></span>

<span data-ttu-id="3a24b-170">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="3a24b-171">다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![기존 VM에 대한 SQL 자동화된 백업](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="3a24b-173">Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 단추 자동 백업 섹션.</span><span class="sxs-lookup"><span data-stu-id="3a24b-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![기존 VM에 대한 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="3a24b-175">완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="3a24b-176">설정 하는 경우 자동화 된 백업을 hello에 대 한 처음으로, Azure hello 백그라운드에서 hello SQL Server IaaS 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="3a24b-177">이 시간 동안 hello Azure 포털 표시 되지 않습니다 자동화 된 백업이 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="3a24b-178">Hello 에이전트 toobe 설치에 대 일 분 정도 기다린 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="3a24b-179">해당 hello Azure 후 포털 hello 새 설정이 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="3a24b-180">또한 템플릿을 사용하여 자동화된 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="3a24b-181">자세한 내용은 [자동화된 백업에 대한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a24b-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="3a24b-182">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="3a24b-182">Configuration with PowerShell</span></span>

<span data-ttu-id="3a24b-183">PowerShell tooconfigure 자동화 된 백업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="3a24b-184">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-184">Before you begin, you must:</span></span>

- <span data-ttu-id="3a24b-185">[다운로드 및 설치 최신 Azure PowerShell hello](http://aka.ms/webpi-azps)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="3a24b-186">Windows PowerShell을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="3a24b-187">Hello hello 단계를 수행 하 여이 작업을 수행할 수 [구독을 구성](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) 섹션의 항목을 프로 비전 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="3a24b-188">Hello SQL IaaS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="3a24b-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="3a24b-189">Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전 하는 경우 SQL Server IaaS 확장 hello 이미 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="3a24b-190">설치 되는 경우 VM에 대 한 호출 하 여 확인할 수 있습니다 **Get AzureRmVM** 명령과 hello 검사 **확장** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="3a24b-191">SQL Server IaaS 에이전트 확장 hello가 설치 된 경우 "SqlIaaSAgent" 또는 "SQLIaaSExtension"으로 나열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="3a24b-192">**ProvisioningState** 에 hello 확장 "Succeeded" 표시도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="3a24b-193">설치 되어 있지 않거나 toobe 프로 비전 실패를 하는 경우 다음 명령을 hello로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="3a24b-194">또한 toohello VM 이름 및 리소스 그룹에서 지정 해야 hello 영역 (**$region**) VM에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="3a24b-195"><a id="verifysettings"></a> 현재 설정 확인</span><span class="sxs-lookup"><span data-stu-id="3a24b-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="3a24b-196">자동화 된 백업 구축 하는 동안 설정한 경우 현재 구성 PowerShell toocheck를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="3a24b-197">Hello 실행 **Get AzureRmVMSqlServerExtension** 명령을 실행 한 hello 검사 **AutoBackupSettings** 속성:</span><span class="sxs-lookup"><span data-stu-id="3a24b-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="3a24b-198">유사한 toohello 다음 출력을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="3a24b-199">출력을 표시 하는 경우 **사용** 너무 설정**False**, tooenable 자동화 된 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="3a24b-200">hello 다행 스럽게도 사용 하도록 설정 하 고 hello에 자동화 된 백업을 구성할 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="3a24b-201">이 정보에 대 한 hello 다음 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a24b-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="3a24b-202">Hello 설정을 변경한 후 즉시을 선택 하면 경우 얻을 수 다시 hello 오래 된 구성 값 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="3a24b-203">몇 분 정도 기다린 후 hello 설정을 확인 toomake 변경 내용이 적용 되었는지 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="3a24b-204">자동화된 백업 구성</span><span class="sxs-lookup"><span data-stu-id="3a24b-204">Configure Automated Backup</span></span>
<span data-ttu-id="3a24b-205">사용할 수 있습니다 toomodify 뿐만 아니라 PowerShell tooenable 자동화 된 백업 구성 및 동작 언제 든 지.</span><span class="sxs-lookup"><span data-stu-id="3a24b-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="3a24b-206">첫째, 선택 하거나 hello에 대 한 저장소 계정에 백업 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="3a24b-207">hello 다음 스크립트 저장소 계정을 선택 하거나 선택 존재 하지 않는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="3a24b-208">자동화된 백업을 사용할 경우 프리미엄 저장소에 백업을 저장할 수 없지만 프리미엄 저장소를 사용하는 VM 디스크에서 백업을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="3a24b-209">다음 hello를 사용 하 여 **새로 AzureRmVMSqlServerAutoBackupConfig** tooenable 명령 및 hello Azure 저장소 계정에에서 hello 자동화 된 백업 설정을 toostore 백업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="3a24b-210">이 예제에서는 hello 백업은 10 일 동안 유지 toobe를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="3a24b-211">두 번째 명령은 hello **집합 AzureRmVMSqlServerExtension**, 업데이트 hello 이러한 설정을 사용 하 여 Azure VM을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="3a24b-212">몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="3a24b-213">에 대 한 설정은 다른 **새로 AzureRmVMSqlServerAutoBackupConfig** tooSQL Server 2016 및 자동화 된 백업 v 2를 적용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="3a24b-214">SQL Server 2014 hello 설정을 다음을 지원 하지 않습니다: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, 및 **LogBackupFrequencyInMinutes**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="3a24b-215">Tooconfigure SQL Server 2014 가상 컴퓨터에서 이러한 설정을 시도 하면 오류가 없는 있지만 hello 설정이 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="3a24b-216">SQL Server 2016 가상 컴퓨터에서 이러한 설정을 toouse을 원하는 경우 참조 [자동화 된 백업 v 2에 대 한 SQL Server 2016 Azure 가상 컴퓨터](virtual-machines-windows-sql-automated-backup-v2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="3a24b-217">tooenable 암호화 hello 이전 스크립트 toopass hello 수정 **EnableEncryption** hello에 대 한 암호 (보안 문자열) 함께 매개 변수 **CertificatePassword** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="3a24b-218">hello 다음 스크립트 hello 이전 예제의 자동화 된 백업 설정을 hello 있으며 특정 암호화를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="3a24b-219">프로그램 설정이 적용 되어 tooconfirm [hello 자동화 된 백업 구성을 확인](#verifysettings)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="3a24b-220">자동화된 백업 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="3a24b-220">Disable Automated Backup</span></span>

<span data-ttu-id="3a24b-221">자동화 된 백업, hello 하지 않고 동일한 스크립트 실행된 hello toodisable **-사용 하도록 설정** 매개 변수 toohello **새로 AzureRmVMSqlServerAutoBackupConfig** 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="3a24b-222">hello 없을 경우 hello **-사용 하도록 설정** 매개 변수가 신호 hello 명령 toodisable hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="3a24b-223">설치의 경우와 마찬가지로 자동화 된 백업에 몇 분 toodisable를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="3a24b-224">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="3a24b-224">Example script</span></span>

<span data-ttu-id="3a24b-225">hello 다음 스크립트를 제공 변수의 tooenable를 사용자 지정할 수 있으며 VM에 대 한 자동화 된 백업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="3a24b-226">여기에서 toocustomize hello 스크립트 요구 사항에 기반 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="3a24b-227">예를 들어 시스템 데이터베이스의 toodisable hello 백업 하려는 경우 toomake 변경 내용이 거 나 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="3a24b-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a24b-228">Next steps</span></span>

<span data-ttu-id="3a24b-229">자동화된 백업은 Azure VM에서 관리되는 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="3a24b-230">것이 중요 너무[관리 되는 백업에 대 한 hello 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello 동작 및 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="3a24b-231">추가 백업 찾 및 hello 항목에 Azure Vm에서 SQL Server에 대 한 지침을 복원할 수 있습니다: [Azure 가상 컴퓨터의 SQL Server 용 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a24b-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="3a24b-232">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a24b-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="3a24b-233">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a24b-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

