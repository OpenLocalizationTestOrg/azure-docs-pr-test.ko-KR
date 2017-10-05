---
title: "SQL Server 가상 컴퓨터의 자동화된 백업(클래식) | Microsoft Docs"
description: "리소스 관리자를 사용하여 Azure 가상 컴퓨터에서 실행 중인 SQL Server에 대한 자동화된 백업 기능에 대해 설명합니다. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: f7664291c2f45c422d52f682d08dbb67ab32b099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="c58fa-103">Azure 가상 컴퓨터에서 SQL Server의 자동화된 백업(클래식)</span><span class="sxs-lookup"><span data-stu-id="c58fa-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c58fa-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="c58fa-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="c58fa-105">클래식</span><span class="sxs-lookup"><span data-stu-id="c58fa-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="c58fa-106">자동화된 백업에서는 SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM의 모든 기존 및 새 데이터베이스에 대해 [Microsoft Azure에 대한 관리되는 백업](https://msdn.microsoft.com/library/dn449496.aspx) 을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="c58fa-107">이를 통해 지속형 Azure Blob 저장소를 활용하는 일반 데이터베이스 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="c58fa-108">자동화된 백업은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c58fa-109">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c58fa-110">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c58fa-111">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c58fa-112">이 문서의 Resource Manager 버전을 보려면 [Azure 가상 컴퓨터 Resource Manager에서 SQL Server의 자동화된 백업](../sql/virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fa-112">To view the Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c58fa-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c58fa-113">Prerequisites</span></span>
<span data-ttu-id="c58fa-114">자동화된 백업을 사용하려면 다음 필수 조건을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fa-114">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="c58fa-115">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="c58fa-115">**Operating System**:</span></span>

* <span data-ttu-id="c58fa-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c58fa-116">Windows Server 2012</span></span>
* <span data-ttu-id="c58fa-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c58fa-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="c58fa-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c58fa-118">Windows Server 2016</span></span>

<span data-ttu-id="c58fa-119">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="c58fa-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="c58fa-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="c58fa-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="c58fa-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="c58fa-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="c58fa-122">SQL Server 2016의 경우 자동화된 백업이 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="c58fa-123">**데이터베이스 구성**:</span><span class="sxs-lookup"><span data-stu-id="c58fa-123">**Database configuration**:</span></span>

* <span data-ttu-id="c58fa-124">대상 데이터베이스는 전체 복구 모델을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-124">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="c58fa-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="c58fa-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="c58fa-126">[최신 Azure PowerShell cmdlet을 설치합니다](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c58fa-126">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="c58fa-127">**SQL Server IaaS 확장**:</span><span class="sxs-lookup"><span data-stu-id="c58fa-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="c58fa-128">[SQL Server IaaS 확장을 설치합니다](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c58fa-128">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="c58fa-129">설정</span><span class="sxs-lookup"><span data-stu-id="c58fa-129">Settings</span></span>
<span data-ttu-id="c58fa-130">다음 표에서는 자동화된 백업에 대해 구성할 수 있는 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-130">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="c58fa-131">클래식 VM의 경우 이러한 설정을 구성하려면 PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-131">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="c58fa-132">설정</span><span class="sxs-lookup"><span data-stu-id="c58fa-132">Setting</span></span> | <span data-ttu-id="c58fa-133">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="c58fa-133">Range (Default)</span></span> | <span data-ttu-id="c58fa-134">설명</span><span class="sxs-lookup"><span data-stu-id="c58fa-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c58fa-135">**자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="c58fa-135">**Automated Backup**</span></span> |<span data-ttu-id="c58fa-136">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="c58fa-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="c58fa-137">SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="c58fa-138">**보존 기간**</span><span class="sxs-lookup"><span data-stu-id="c58fa-138">**Retention Period**</span></span> |<span data-ttu-id="c58fa-139">1-30일(30일)</span><span class="sxs-lookup"><span data-stu-id="c58fa-139">1-30 days (30 days)</span></span> |<span data-ttu-id="c58fa-140">백업 보존 기간(일 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-140">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="c58fa-141">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="c58fa-141">**Storage Account**</span></span> |<span data-ttu-id="c58fa-142">Azure 저장소 계정(지정된 VM에 대해 만든 저장소 계정)</span><span class="sxs-lookup"><span data-stu-id="c58fa-142">Azure storage account (the storage account created for the specified VM)</span></span> |<span data-ttu-id="c58fa-143">Blob 저장소에 자동화된 백업 파일을 저장하기 위해 사용하여 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-143">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="c58fa-144">모든 백업 파일을 저장하려면 컨테이너를 이 위치에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-144">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="c58fa-145">백업 파일 명명 규칙에는 날짜, 시간 및 컴퓨터 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-145">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="c58fa-146">**암호화**</span><span class="sxs-lookup"><span data-stu-id="c58fa-146">**Encryption**</span></span> |<span data-ttu-id="c58fa-147">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="c58fa-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="c58fa-148">암호화 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-148">Enables or disables encryption.</span></span> <span data-ttu-id="c58fa-149">암호화 기능을 사용하면 백업을 복원하는 데 사용되는 인증서가 동일한 명명 규칙을 사용하여 동일한 자동 백업 컨테이너에 지정한 저장소 계정에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-149">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span></span> <span data-ttu-id="c58fa-150">암호가 변경되면 해당 암호를 사용하여 새 인증서가 생성되지만 이전 인증서도 이전 백업의 복원을 위해 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-150">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="c58fa-151">**암호**</span><span class="sxs-lookup"><span data-stu-id="c58fa-151">**Password**</span></span> |<span data-ttu-id="c58fa-152">암호 텍스트(없음)</span><span class="sxs-lookup"><span data-stu-id="c58fa-152">Password text (None)</span></span> |<span data-ttu-id="c58fa-153">암호화 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-153">A password for encryption keys.</span></span> <span data-ttu-id="c58fa-154">암호화를 사용하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="c58fa-155">암호화된 백업을 복원하기 위해서는 올바른 암호 및 백업을 수행할 때 사용한 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-155">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> | <span data-ttu-id="c58fa-156">**시스템 데이터베이스 백업**</span><span class="sxs-lookup"><span data-stu-id="c58fa-156">**Backup system databases**</span></span> | <span data-ttu-id="c58fa-157">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="c58fa-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="c58fa-158">Master, Model 및 MSDB의 전체 백업</span><span class="sxs-lookup"><span data-stu-id="c58fa-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="c58fa-159">**백업 일정 구성**</span><span class="sxs-lookup"><span data-stu-id="c58fa-159">**Configure backup schedule**</span></span> | <span data-ttu-id="c58fa-160">수동/자동(자동)</span><span class="sxs-lookup"><span data-stu-id="c58fa-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="c58fa-161">로그 증가에 따라 전체 및 로그 백업을 자동으로 수행하려면 **자동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-161">Select **Automated** to automatically take full and log backups based on log growth.</span></span> <span data-ttu-id="c58fa-162">전체 및 로그 백업 일정을 지정하려면 **수동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-162">Select **Manual** to specify the schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="c58fa-163">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="c58fa-163">Configuration with PowerShell</span></span>
<span data-ttu-id="c58fa-164">다음 PowerShell 예제에서는 기존 SQL Server 2014 VM에 대해 자동화된 백업이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-164">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="c58fa-165">**New-AzureVMSqlServerAutoBackupConfig** 명령은 $storageaccount 변수로 지정한 Azure 저장소 계정에 백업을 저장하는 자동화된 백업 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-165">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span></span> <span data-ttu-id="c58fa-166">이러한 백업은 10일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="c58fa-167">**Set-AzureVMSqlServerExtension** 명령은 지정된 Azure VM을 이러한 설정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-167">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="c58fa-168">SQL Server IaaS 에이전트를 설치하고 구성하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-168">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="c58fa-169">암호화를 사용하려면 CertificatePassword 매개 변수에 대 한 암호(보안 문자열)와 함께 EnableEncryption 매개 변수를 전달 하도록 이전 스크립트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-169">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span></span> <span data-ttu-id="c58fa-170">다음 스크립트를 사용하면 이전 예제의 자동화된 백업 설정을 사용하고 암호화를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-170">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="c58fa-171">자동 백업을 사용하지 않으려면 동일한 스크립트를 **-Enable** 매개 변수 없이 **New-AzureVMSqlServerAutoBackupConfig**에 대해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-171">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="c58fa-172">설치와 마찬가지로 자동화된 백업을 사용하지 않도록 설정하는 데도 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-172">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="c58fa-173">SQL Server IaaS 에이전트를 비활성화하고 제거해도 이전에 구성한 관리된 백업 설정은 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-173">Disabling and uninstalling the SQL Server IaaS Agent does not remove the previously configured Managed Backup settings.</span></span> <span data-ttu-id="c58fa-174">SQL Server IaaS 에이전트를 비활성화 또는 제거하기 전에 자동화된 백업을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-174">You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c58fa-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c58fa-175">Next steps</span></span>
<span data-ttu-id="c58fa-176">자동화된 백업은 Azure VM에서 관리되는 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="c58fa-177">따라서 [관리되는 백업 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) 하여 동작 및 의미를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fa-177">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="c58fa-178">Azure VM의 SQL Server에 대한 추가적인 백업 및 복원 지침은 [Azure 가상 컴퓨터의 SQL Server 백업 및 복원](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fa-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="c58fa-179">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fa-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="c58fa-180">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fa-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

