---
title: "SQL Server 2016 Azure Virtual Machines의 자동화된 백업 v2 | Microsoft Docs"
description: "Azure에서 실행되는 SQL Server 2016 VM의 자동화된 백업 기능에 대해 설명합니다. 이 문서는 Resource Manager를 사용하는 VM에만 적용됩니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: e7e14b0243f82c672392d5ab4bb6aca01156465b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="1c3bc-104">SQL Server 2016 Azure Virtual Machines의 자동화된 백업 v2(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c3bc-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1c3bc-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="1c3bc-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="1c3bc-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="1c3bc-107">자동화된 백업 v2에서는 SQL Server 2016 Standard, Enterprise 또는 Developer 버전을 실행하는 Azure VM의 모든 기존 및 새 데이터베이스에 대해 [Microsoft Azure에 대한 관리되는 백업](https://msdn.microsoft.com/library/dn449496.aspx)을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-107">Automated Backup v2 automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="1c3bc-108">이를 통해 지속형 Azure Blob 저장소를 활용하는 일반 데이터베이스 백업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="1c3bc-109">자동화된 백업 v2는 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-109">Automated Backup v2 depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="1c3bc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1c3bc-110">Prerequisites</span></span>
<span data-ttu-id="1c3bc-111">자동화된 백업 v2를 사용하려면 다음 필수 조건을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-111">To use Automated Backup v2, review the following prerequisites:</span></span>

<span data-ttu-id="1c3bc-112">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="1c3bc-112">**Operating System**:</span></span>

- <span data-ttu-id="1c3bc-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1c3bc-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="1c3bc-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1c3bc-114">Windows Server 2016</span></span>

<span data-ttu-id="1c3bc-115">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="1c3bc-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="1c3bc-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="1c3bc-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="1c3bc-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="1c3bc-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="1c3bc-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="1c3bc-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3bc-119">자동화된 백업 v2는 SQL Server 2016에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="1c3bc-120">SQL Server 2014를 사용하는 경우 자동화된 백업 v1을 사용하여 데이터베이스를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-120">If you are using SQL Server 2014, you can use Automated Backup v1 to back up your databases.</span></span> <span data-ttu-id="1c3bc-121">자세한 내용은 [SQL Server 2014 Azure Virtual Machines의 자동화된 백업](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="1c3bc-122">**데이터베이스 구성**:</span><span class="sxs-lookup"><span data-stu-id="1c3bc-122">**Database configuration**:</span></span>

- <span data-ttu-id="1c3bc-123">대상 데이터베이스는 전체 복구 모델을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="1c3bc-124">전체 복구 모델이 백업에 미치는 영향에 대한 자세한 내용은 [전체 복구 모델에서 백업](https://technet.microsoft.com/library/ms190217.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="1c3bc-125">시스템 데이터베이스는 전체 복구 모델을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-125">System databases do not have to use full recovery model.</span></span> <span data-ttu-id="1c3bc-126">그러나 Model 또는 MSDB에 대해 로그 백업을 수행해야 할 경우 전체 복구 모델을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-126">However, if you require log backups to be taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="1c3bc-127">대상 데이터베이스는 기본 SQL Server 인스턴스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-127">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="1c3bc-128">SQL Server IaaS 확장은 명명된 인스턴스를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-128">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="1c3bc-129">**Azure 배포 모델**:</span><span class="sxs-lookup"><span data-stu-id="1c3bc-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="1c3bc-130">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="1c3bc-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="1c3bc-131">자동화된 백업은 **SQL Server IaaS 에이전트 확장**에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-131">Automated Backup relies on the **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="1c3bc-132">현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="1c3bc-133">자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="1c3bc-134">설정</span><span class="sxs-lookup"><span data-stu-id="1c3bc-134">Settings</span></span>
<span data-ttu-id="1c3bc-135">다음 표에서는 자동화된 백업 v2에 대해 구성할 수 있는 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-135">The following table describes the options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="1c3bc-136">실제 구성 단계는 Azure 포털 또는 Azure Windows PowerShell 명령 사용 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="1c3bc-137">기본 설정</span><span class="sxs-lookup"><span data-stu-id="1c3bc-137">Basic Settings</span></span>

| <span data-ttu-id="1c3bc-138">설정</span><span class="sxs-lookup"><span data-stu-id="1c3bc-138">Setting</span></span> | <span data-ttu-id="1c3bc-139">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-139">Range (Default)</span></span> | <span data-ttu-id="1c3bc-140">설명</span><span class="sxs-lookup"><span data-stu-id="1c3bc-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c3bc-141">**자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-141">**Automated Backup**</span></span> | <span data-ttu-id="1c3bc-142">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="1c3bc-143">SQL Server 2016 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="1c3bc-144">**보존 기간**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-144">**Retention Period**</span></span> | <span data-ttu-id="1c3bc-145">1-30일(30일)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-145">1-30 days (30 days)</span></span> | <span data-ttu-id="1c3bc-146">백업 보존 기간(일 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-146">The number of days to retain backups.</span></span> |
| <span data-ttu-id="1c3bc-147">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-147">**Storage Account**</span></span> | <span data-ttu-id="1c3bc-148">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="1c3bc-148">Azure storage account</span></span> | <span data-ttu-id="1c3bc-149">Blob 저장소에 자동화된 백업 파일을 저장하기 위해 사용하여 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-149">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="1c3bc-150">모든 백업 파일을 저장하려면 컨테이너를 이 위치에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-150">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="1c3bc-151">백업 파일 명명 규칙에는 날짜, 시간 및 데이터베이스 GUID가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-151">The backup file naming convention includes the date, time, and database GUID.</span></span> |
| <span data-ttu-id="1c3bc-152">**암호화**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-152">**Encryption**</span></span> |<span data-ttu-id="1c3bc-153">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="1c3bc-154">암호화 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-154">Enables or disables encryption.</span></span> <span data-ttu-id="1c3bc-155">암호화 기능을 사용하면 백업을 복원하는 데 사용되는 인증서가 동일한 명명 규칙을 사용하여 동일한 **automaticbackup** 컨테이너에 지정한 저장소 계정에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-155">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same **automaticbackup** container using the same naming convention.</span></span> <span data-ttu-id="1c3bc-156">암호가 변경되면 해당 암호를 사용하여 새 인증서가 생성되지만 이전 인증서도 이전 백업의 복원을 위해 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-156">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="1c3bc-157">**암호**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-157">**Password**</span></span> |<span data-ttu-id="1c3bc-158">암호 텍스트</span><span class="sxs-lookup"><span data-stu-id="1c3bc-158">Password text</span></span> | <span data-ttu-id="1c3bc-159">암호화 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-159">A password for encryption keys.</span></span> <span data-ttu-id="1c3bc-160">암호화를 사용하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="1c3bc-161">암호화된 백업을 복원하기 위해서는 올바른 암호 및 백업을 수행할 때 사용한 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-161">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="1c3bc-162">고급 설정</span><span class="sxs-lookup"><span data-stu-id="1c3bc-162">Advanced Settings</span></span>

| <span data-ttu-id="1c3bc-163">설정</span><span class="sxs-lookup"><span data-stu-id="1c3bc-163">Setting</span></span> | <span data-ttu-id="1c3bc-164">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-164">Range (Default)</span></span> | <span data-ttu-id="1c3bc-165">설명</span><span class="sxs-lookup"><span data-stu-id="1c3bc-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c3bc-166">**시스템 데이터베이스 백업**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-166">**System Database Backups**</span></span> | <span data-ttu-id="1c3bc-167">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="1c3bc-168">사용하도록 설정하면 이 기능은 시스템 데이터베이스인 Master, MSDB 및 Model도 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-168">When enabled, this feature will also back up the system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="1c3bc-169">MSDB 및 Model 데이터베이스의 경우 로그 백업이 수행되도록 하려면 전체 복구 모드인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-169">For the MSDB and Model databases, verify that they are in full recovery mode if you want log backups to be taken.</span></span> <span data-ttu-id="1c3bc-170">Master의 경우에는 로그 백업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="1c3bc-171">또한 TempDB에 대해서도 백업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="1c3bc-172">**백업 일정**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-172">**Backup Schedule**</span></span> | <span data-ttu-id="1c3bc-173">수동/자동(자동)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="1c3bc-174">기본적으로 백업 일정은 로그 증가에 따라 자동으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-174">By default, the backup schedule will be automatically determined based on the log growth.</span></span> <span data-ttu-id="1c3bc-175">수동 백업 일정을 사용하면 백업에 대한 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-175">Manual backup schedule allows the user to specify the time window for backups.</span></span> <span data-ttu-id="1c3bc-176">이 경우 백업은 지정된 빈도로, 지정된 날의 지정된 기간 동안에만 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-176">In this case, backups will only ever take place at the specified frequency and during the specified time window of a given day.</span></span> |
| <span data-ttu-id="1c3bc-177">**전체 백업 빈도**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-177">**Full backup frequency**</span></span> | <span data-ttu-id="1c3bc-178">매일/매주</span><span class="sxs-lookup"><span data-stu-id="1c3bc-178">Daily/Weekly</span></span> | <span data-ttu-id="1c3bc-179">전체 백업의 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-179">Frequency of full backups.</span></span> <span data-ttu-id="1c3bc-180">두 경우 모두 전체 백업은 예약된 다음 기간 동안 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-180">In both cases, full backups will begin during the next scheduled time window.</span></span> <span data-ttu-id="1c3bc-181">매주 옵션을 선택하면 백업은 모든 데이터베이스가 성공적으로 백업될 때까지 여러 날에 걸쳐 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="1c3bc-182">**전체 백업 시작 시간**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-182">**Full backup start time**</span></span> | <span data-ttu-id="1c3bc-183">00:00 – 23:00(01:00)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="1c3bc-184">전체 백업이 수행될 수 있는 지정된 날의 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="1c3bc-185">**전체 백업 시간 기간**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-185">**Full backup time window**</span></span> | <span data-ttu-id="1c3bc-186">1-23시간(1시간)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="1c3bc-187">전체 백업이 수행될 수 있는 지정된 날의 시간 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-187">Duration of the time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="1c3bc-188">**로그 백업 빈도**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-188">**Log backup frequency**</span></span> | <span data-ttu-id="1c3bc-189">5-60분(60분)</span><span class="sxs-lookup"><span data-stu-id="1c3bc-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="1c3bc-190">로그 백업의 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="1c3bc-191">전체 백업 빈도 이해</span><span class="sxs-lookup"><span data-stu-id="1c3bc-191">Understanding full backup frequency</span></span>
<span data-ttu-id="1c3bc-192">매일 및 매주 전체 백업 간 차이를 이해하는 것은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-192">It is important to understand the difference between daily and weekly full backups.</span></span> <span data-ttu-id="1c3bc-193">이를 위해 다음과 같은 두 가지 예제 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="1c3bc-194">시나리오 1: 매주 백업</span><span class="sxs-lookup"><span data-stu-id="1c3bc-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="1c3bc-195">매우 큰 데이터베이스를 많이 포함하는 SQL Server VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="1c3bc-196">월요일에서 다음 설정으로 자동화된 백업 v2를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-196">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="1c3bc-197">백업 일정: **수동**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="1c3bc-198">전체 백업 빈도: **매주**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="1c3bc-199">전체 백업 시작 시간: **01:00**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="1c3bc-200">전체 백업 시간 기간: **1시간**</span><span class="sxs-lookup"><span data-stu-id="1c3bc-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="1c3bc-201">즉, 사용 가능한 다음 백업 기간은 화요일 오전 1시부터 1시간 동안입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-201">This means that the next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="1c3bc-202">해당 시간에 자동화된 백업은 한 번에 하나씩 데이터베이스를 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="1c3bc-203">이 시나리오에서는 처음 두 데이터베이스에 대해 전체 백업이 완료될 정도로 데이터베이스가 큽니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-203">In this scenario, your databases are large enough that full backups will complete for the first couple databases.</span></span> <span data-ttu-id="1c3bc-204">그러나 1시간 후에 모든 데이터베이스가 백업되지는 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-204">However, after one hour not all of the databases have been backed up.</span></span>

<span data-ttu-id="1c3bc-205">이 경우 자동화된 백업은 다음 날인 수요일에 오전 1시부터 1시간 동안 나머지 데이터베이스를 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-205">When this happens, Automated Backup will begin backing up the remaining databases the next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="1c3bc-206">해당 시간에 모든 데이터베이스이 백업되지는 않을 경우 다음 날 같은 시간에 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-206">If not all databases have been backed up in that time, it will try again the next day at the same time.</span></span> <span data-ttu-id="1c3bc-207">이 과정은 모든 데이터베이스가 성공적으로 백업될 때까지 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="1c3bc-208">다시 화요일이 되면 자동화된 백업은 모든 데이터베이스를 다시 한 번 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="1c3bc-209">이 시나리오에서는 자동화된 백업이 지정된 기간 내에만 작동하며 각 데이터베이스가 매주 한 번 백업될 것임을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-209">This scenario shows that Automated Backup will only operate within the specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="1c3bc-210">또한 하루에 모든 백업을 완료할 수 없는 경우 여러 날에 걸쳐 백업이 진행될 수 있다는 사실도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-210">This also shows that it is possible for backups to span multiple days in the case where it is not possible to complete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="1c3bc-211">시나리오 2: 매일 백업</span><span class="sxs-lookup"><span data-stu-id="1c3bc-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="1c3bc-212">매우 큰 데이터베이스를 많이 포함하는 SQL Server VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="1c3bc-213">월요일에서 다음 설정으로 자동화된 백업 v2를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-213">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="1c3bc-214">백업 일정: 수동</span><span class="sxs-lookup"><span data-stu-id="1c3bc-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="1c3bc-215">전체 백업 빈도: 매일</span><span class="sxs-lookup"><span data-stu-id="1c3bc-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="1c3bc-216">전체 백업 시작 시간: 22:00</span><span class="sxs-lookup"><span data-stu-id="1c3bc-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="1c3bc-217">전체 백업 시간 기간: 6시간</span><span class="sxs-lookup"><span data-stu-id="1c3bc-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="1c3bc-218">즉, 사용 가능한 다음 백업 기간은 월요일 오후 10시부터 6시간 동안입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-218">This means that the next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="1c3bc-219">해당 시간에 자동화된 백업은 한 번에 하나씩 데이터베이스를 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="1c3bc-220">그런 다음 화요일 오후 10부터 6시간 동안 모든 데이터베이스의 전체 백업이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3bc-221">매일 백업 일정을 계획할 때는 모든 데이터베이스가 이 시간 내에 백업될 수 있도록 넓은 기간을 예약하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-221">When scheduling daily backups, it is recommended that you schedule a wide time window to ensure all databases can be backed up within this time.</span></span> <span data-ttu-id="1c3bc-222">특히 백업할 데이터양이 클 경우 이러한 점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-222">This is especially important in the case where you have a large amount of data to back up.</span></span>

## <a name="configuration-in-the-portal"></a><span data-ttu-id="1c3bc-223">포털에서 구성</span><span class="sxs-lookup"><span data-stu-id="1c3bc-223">Configuration in the Portal</span></span>

<span data-ttu-id="1c3bc-224">Azure Portal을 사용하여 프로비전 중에 또는 기존 SQL Server 2016 VM에 대해 자동화된 백업 v2를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-224">You can use the Azure portal to configure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="1c3bc-225">새 VM</span><span class="sxs-lookup"><span data-stu-id="1c3bc-225">New VMs</span></span>

<span data-ttu-id="1c3bc-226">Azure Portal을 사용하여 Resource Manager 배포 모델에서 새 SQL Server 2016 가상 컴퓨터를 만들 때 자동화된 백업 v2를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-226">Use the Azure portal to configure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in the Resource Manager deployment model.</span></span> 

<span data-ttu-id="1c3bc-227">**SQL Server 설정** 블레이드에서 **자동화된 백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-227">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="1c3bc-228">다음 Azure 포털 스크린샷은 **SQL 자동화된 백업** 블레이드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-228">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Azure 포털에서 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="1c3bc-230">자동화된 백업 v2는 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="1c3bc-231">컨텍스트의 경우 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)의 전체 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-231">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="1c3bc-232">기존 VM</span><span class="sxs-lookup"><span data-stu-id="1c3bc-232">Existing VMs</span></span>

<span data-ttu-id="1c3bc-233">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="1c3bc-234">그런 다음 **설정** 블레이드의 **SQL Server 구성** 섹션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-234">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![기존 VM에 대한 SQL 자동화된 백업](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="1c3bc-236">**SQL Server 구성** 블레이드에서 자동화된 백업 섹션의 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-236">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![기존 VM에 대한 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="1c3bc-238">완료되면 **SQL Server 구성** 블레이드 아래쪽의 **확인** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-238">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="1c3bc-239">처음으로 자동화된 백업을 사용 설정할 경우 Azure에서 백그라운드로 SQL Server IaaS 에이전트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-239">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="1c3bc-240">이 시간 동안에는 구성된 자동화된 백업이 Azure 포털에 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-240">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="1c3bc-241">에이전트가 설치 및 구성될 때까지 몇 분 정도 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-241">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="1c3bc-242">그 후 Azure 포털에는 새 설정이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-242">After that the Azure portal will reflect the new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="1c3bc-243">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="1c3bc-243">Configuration with PowerShell</span></span>

<span data-ttu-id="1c3bc-244">PowerShell을 사용하여 자동화된 백업 v2를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-244">You can use PowerShell to configure Automated Backup v2.</span></span> <span data-ttu-id="1c3bc-245">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-245">Before you begin, you must:</span></span>

- <span data-ttu-id="1c3bc-246">[최신 Azure PowerShell을 다운로드하여 설치합니다](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="1c3bc-246">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="1c3bc-247">Windows PowerShell을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="1c3bc-248">이렇게 하려면 프로비전 관련 문서의 [구독 구성](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) 섹션에서 설명하는 단계를 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-248">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="1c3bc-249">SQL IaaS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="1c3bc-249">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="1c3bc-250">Azure Portal에서 SQL Server 가상 컴퓨터를 프로비전한 경우 SQL Server IaaS 확장이 이미 설치되어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-250">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="1c3bc-251">**Get-AzureRmVM** 명령을 실행하고 **Extensions** 속성을 검사하여 VM에 대해 해당 확장이 설치되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="1c3bc-252">SQL Server IaaS 에이전트 확장이 설치되어 있는 경우 "SqlIaaSAgent" 또는 "SQLIaaSExtension"으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-252">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="1c3bc-253">확장에 대한 **ProvisioningState**가 "Succeeded"로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-253">**ProvisioningState** for the extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="1c3bc-254">설치되지 않았거나 프로비전되지 못한 경우 다음 명령을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-254">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="1c3bc-255">VM 이름 및 리소스 그룹 외에, VM이 있는 하위 지역(**$region**)도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-255">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="1c3bc-256"><a id="verifysettings"></a> 현재 설정 확인</span><span class="sxs-lookup"><span data-stu-id="1c3bc-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="1c3bc-257">프로비전 동안 자동화된 백업을 사용하도록 설정한 경우 PowerShell을 사용하여 현재 구성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-257">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="1c3bc-258">**Get-AzureRmVMSqlServerExtension** 명령을 실행하고 **AutoBackupSettings** 속성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-258">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="1c3bc-259">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-259">You should get output similar to the following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="1c3bc-260">출력에 **Enable**이 **False**로 설정되어 표시되면 자동화된 백업을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-260">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="1c3bc-261">다행히도 자동화된 백업도 같은 방식으로 사용하도록 설정하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-261">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="1c3bc-262">이 정보에 대해서는 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-262">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="1c3bc-263">변경을 수행한 후에 설정을 바로 확인하면 이전 구성 값을 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-263">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="1c3bc-264">몇 분 정도 기다렸다가 설정을 다시 확인하여 변경 내용이 적용되었는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-264">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="1c3bc-265">자동화된 백업 v2 구성</span><span class="sxs-lookup"><span data-stu-id="1c3bc-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="1c3bc-266">언제든지 PowerShell을 사용하여 자동화된 백업을 사용하도록 설정하고 해당 구성 및 동작을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-266">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="1c3bc-267">먼저 백업 파일에 대한 저장소 계정을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-267">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="1c3bc-268">다음 스크립트는 저장소 계정을 선택하거나 없으면 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-268">The following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="1c3bc-269">자동화된 백업을 사용할 경우 프리미엄 저장소에 백업을 저장할 수 없지만 프리미엄 저장소를 사용하는 VM 디스크에서 백업을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="1c3bc-270">그런 후 **New-AzureRmVMSqlServerAutoBackupConfig** 명령을 통해 자동화된 백업 v2 설정을 사용하도록 지정하고 Azure Storage 계정에 백업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-270">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup v2 settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="1c3bc-271">이 예제에서는 백업이 10일 동안 보관되도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-271">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="1c3bc-272">시스템 데이터베이스 백업이 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-272">System database backups are enabled.</span></span> <span data-ttu-id="1c3bc-273">전체 백업은 20시부터 시작해서 2시간 동안 진행되는 것으로 매주 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="1c3bc-274">로그 백업은 30분 간격으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="1c3bc-275">두 번째 명령인 **Set-AzureRmVMSqlServerExtension**은 지정된 Azure VM을 이러한 설정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-275">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="1c3bc-276">SQL Server IaaS 에이전트를 설치하고 구성하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-276">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="1c3bc-277">암호화를 사용하려면 **CertificatePassword** 매개 변수에 대 한 암호(보안 문자열)와 함께 **EnableEncryption** 매개 변수를 전달 하도록 이전 스크립트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-277">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="1c3bc-278">다음 스크립트를 사용하면 이전 예제의 자동화된 백업 설정을 사용하고 암호화를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-278">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="1c3bc-279">설정이 적용되었는지 확인하려면 [자동화된 백업 구성을 확인](#verifysettings)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-279">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="1c3bc-280">자동화된 백업 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="1c3bc-280">Disable Automated Backup</span></span>
<span data-ttu-id="1c3bc-281">자동화된 백업을 사용하지 않도록 설정하려면 동일한 스크립트를 **-Enable** 매개 변수 없이 **New-AzureRmVMSqlServerAutoBackupConfig** 명령에 대해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-281">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="1c3bc-282">**-Enable** 매개 변수가 없는 경우 기능을 해제하는 명령을 신호로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-282">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="1c3bc-283">설치와 마찬가지로 자동화된 백업을 사용하지 않도록 설정하는 데도 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-283">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="1c3bc-284">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="1c3bc-284">Example script</span></span>
<span data-ttu-id="1c3bc-285">다음 스크립트는 VM에 대해 자동화된 백업을 사용하도록 설정하고 구성하기 위해 사용자 지정할 수 있는 변수 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-285">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="1c3bc-286">사용자의 경우 요구 사항에 따라 스크립트를 사용자 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-286">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="1c3bc-287">예를 들어 시스템 데이터베이스의 백업을 사용하지 않도록 설정하거나 암호화를 사용하도록 설정하려는 경우 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-287">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="1c3bc-288">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c3bc-288">Next steps</span></span>
<span data-ttu-id="1c3bc-289">자동화된 백업 v2는 Azure VM에서 관리되는 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="1c3bc-290">따라서 [관리되는 백업 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) 하여 동작 및 의미를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-290">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="1c3bc-291">Azure VM의 SQL Server에 대한 추가적인 백업 및 복원 지침은 [Azure 가상 컴퓨터의 SQL Server 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="1c3bc-292">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="1c3bc-293">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c3bc-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

