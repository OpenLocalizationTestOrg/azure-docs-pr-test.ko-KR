---
title: "백업에 대 한 SQL Server 가상 컴퓨터 (클래식) aaaAutomated | Microsoft Docs"
description: "Azure 가상 컴퓨터의 리소스 관리자를 사용 하 여 실행 중인 SQL Server에 대 한 hello 자동화 된 백업 기능에 설명 합니다. "
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
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="f158c-103">Azure 가상 컴퓨터에서 SQL Server의 자동화된 백업(클래식)</span><span class="sxs-lookup"><span data-stu-id="f158c-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f158c-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="f158c-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="f158c-105">클래식</span><span class="sxs-lookup"><span data-stu-id="f158c-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="f158c-106">자동화 된 백업에서 자동으로 구성 [Azure 관리 되는 백업 tooMicrosoft](https://msdn.microsoft.com/library/dn449496.aspx) 모든 기존 및 새 데이터베이스를 SQL Server 2014 Standard 또는 Enterprise를 실행 하는 Azure VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="f158c-107">그러면 지속 Azure blob 저장소를 사용 하는 tooconfigure 정기적 데이터베이스 백업을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="f158c-108">자동화 된 백업 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f158c-109">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f158c-110">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f158c-111">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f158c-112">이 문서의 tooview hello 리소스 관리자 버전 참조 [Azure 가상 컴퓨터 리소스 관리자에서 SQL Server에 대 한 자동화 된 백업을](../sql/virtual-machines-windows-sql-automated-backup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f158c-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f158c-113">Prerequisites</span></span>
<span data-ttu-id="f158c-114">자동화 된 백업 toouse hello 다음 필수 구성 요소를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="f158c-115">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="f158c-115">**Operating System**:</span></span>

* <span data-ttu-id="f158c-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f158c-116">Windows Server 2012</span></span>
* <span data-ttu-id="f158c-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f158c-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="f158c-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f158c-118">Windows Server 2016</span></span>

<span data-ttu-id="f158c-119">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="f158c-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="f158c-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="f158c-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="f158c-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="f158c-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="f158c-122">SQL Server 2016의 경우 자동화된 백업이 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="f158c-123">**데이터베이스 구성**:</span><span class="sxs-lookup"><span data-stu-id="f158c-123">**Database configuration**:</span></span>

* <span data-ttu-id="f158c-124">대상 데이터베이스는 hello 전체 복구 모델을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="f158c-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="f158c-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="f158c-126">[설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="f158c-127">**SQL Server IaaS 확장**:</span><span class="sxs-lookup"><span data-stu-id="f158c-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="f158c-128">[SQL Server IaaS 확장 hello 설치](../classic/sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="f158c-129">설정</span><span class="sxs-lookup"><span data-stu-id="f158c-129">Settings</span></span>
<span data-ttu-id="f158c-130">hello 다음 설명에 대 한 자동화 된 백업을 구성할 수 있는 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="f158c-131">클래식 Vm에 대 한 PowerShell tooconfigure를 이러한 설정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="f158c-132">설정</span><span class="sxs-lookup"><span data-stu-id="f158c-132">Setting</span></span> | <span data-ttu-id="f158c-133">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="f158c-133">Range (Default)</span></span> | <span data-ttu-id="f158c-134">설명</span><span class="sxs-lookup"><span data-stu-id="f158c-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f158c-135">**자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="f158c-135">**Automated Backup**</span></span> |<span data-ttu-id="f158c-136">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="f158c-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="f158c-137">SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="f158c-138">**보존 기간**</span><span class="sxs-lookup"><span data-stu-id="f158c-138">**Retention Period**</span></span> |<span data-ttu-id="f158c-139">1-30일(30일)</span><span class="sxs-lookup"><span data-stu-id="f158c-139">1-30 days (30 days)</span></span> |<span data-ttu-id="f158c-140">hello 수 일 tooretain 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="f158c-141">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="f158c-141">**Storage Account**</span></span> |<span data-ttu-id="f158c-142">Azure 저장소 계정 (hello 지정한 VM에 대 한 만든 hello 저장소 계정)</span><span class="sxs-lookup"><span data-stu-id="f158c-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="f158c-143">Blob 저장소에 자동화 된 백업 파일을 저장 하기 위한 Azure 저장소 계정 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="f158c-144">컨테이너는 모든 백업 파일에이 위치 toostore 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="f158c-145">hello 날짜, 시간 및 컴퓨터 이름 hello 백업 파일 명명 규칙에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="f158c-146">**암호화**</span><span class="sxs-lookup"><span data-stu-id="f158c-146">**Encryption**</span></span> |<span data-ttu-id="f158c-147">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="f158c-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="f158c-148">암호화 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-148">Enables or disables encryption.</span></span> <span data-ttu-id="f158c-149">Hello 인증서를 사용 하는 toorestore hello 백업 hello에 있는 저장소 계정의 지정 된 암호화를 사용 하는 경우 hello ô ä ¢ hello 사용 하 여 동일한 automaticbackup 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="f158c-150">Hello 암호를 변경 하는 경우 해당 암호와 새 인증서가 생성 하지만 hello 이전 인증서 toorestore 이전 백업을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="f158c-151">**암호**</span><span class="sxs-lookup"><span data-stu-id="f158c-151">**Password**</span></span> |<span data-ttu-id="f158c-152">암호 텍스트(없음)</span><span class="sxs-lookup"><span data-stu-id="f158c-152">Password text (None)</span></span> |<span data-ttu-id="f158c-153">암호화 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-153">A password for encryption keys.</span></span> <span data-ttu-id="f158c-154">암호화를 사용하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="f158c-155">암호화 된 백업에서 순서 toorestore hello 올바른 암호와 hello 백업을 수행한 hello 시 사용 된 인증서 관련된 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="f158c-156">**시스템 데이터베이스 백업**</span><span class="sxs-lookup"><span data-stu-id="f158c-156">**Backup system databases**</span></span> | <span data-ttu-id="f158c-157">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="f158c-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="f158c-158">Master, Model 및 MSDB의 전체 백업</span><span class="sxs-lookup"><span data-stu-id="f158c-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="f158c-159">**백업 일정 구성**</span><span class="sxs-lookup"><span data-stu-id="f158c-159">**Configure backup schedule**</span></span> | <span data-ttu-id="f158c-160">수동/자동(자동)</span><span class="sxs-lookup"><span data-stu-id="f158c-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="f158c-161">선택 **자동** tooautomatically 전체 걸리며 로그 백업을 기반으로 로그 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="f158c-162">선택 **수동** toospecify hello 일정에 대 한 전체 및 로그 백업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="f158c-163">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="f158c-163">Configuration with PowerShell</span></span>
<span data-ttu-id="f158c-164">다음 PowerShell 예에서는 hello, 기존 SQL Server 2014 VM에 대 한 자동화 된 백업은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="f158c-165">hello **새로 AzureVMSqlServerAutoBackupConfig** 명령은 hello $storageaccount 변수에 지정 된 hello Azure 저장소 계정에 hello 자동화 된 백업 설정을 toostore 백업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="f158c-166">이러한 백업은 10일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="f158c-167">hello **집합 AzureVMSqlServerExtension** 명령 업데이트 hello 이러한 설정을 사용 하 여 Azure VM을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="f158c-168">몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="f158c-169">tooenable 암호화 hello CertificatePassword 매개 변수에 대 한 hello 이전 스크립트 toopass hello EnableEncryption 매개 변수는 암호 (보안 문자열)와 함께 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="f158c-170">hello 다음 스크립트 hello 이전 예제의 자동화 된 백업 설정을 hello 있으며 특정 암호화를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="f158c-171">toodisable 자동 백업이 실행된 hello hello 하지 않고 동일한 스크립트 **-사용 하도록 설정** 매개 변수 toohello **새로 AzureVMSqlServerAutoBackupConfig**합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="f158c-172">설치의 경우와 마찬가지로 자동화 된 백업에 몇 분 toodisable를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="f158c-173">SQL Server IaaS 에이전트 hello 사용 안하고 hello 이전에 구성 된 관리 백업 설정이 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="f158c-174">자동화 된 백업을 사용 하지 않도록 설정 하거나 hello SQL Server IaaS 에이전트를 제거 하기 전에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f158c-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f158c-175">Next steps</span></span>
<span data-ttu-id="f158c-176">자동화된 백업은 Azure VM에서 관리되는 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="f158c-177">것이 중요 너무[관리 되는 백업에 대 한 hello 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello 동작 및 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="f158c-178">추가 백업 찾 및 hello 항목에 Azure Vm에서 SQL Server에 대 한 지침을 복원할 수 있습니다: [Azure 가상 컴퓨터의 SQL Server 용 백업 및 복원](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f158c-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="f158c-179">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f158c-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="f158c-180">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f158c-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

