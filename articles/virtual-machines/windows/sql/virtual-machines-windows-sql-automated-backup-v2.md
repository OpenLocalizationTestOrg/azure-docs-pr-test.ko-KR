---
title: "aaaAutomated 백업 v 2에 대 한 SQL Server 2016 Azure 가상 컴퓨터 | Microsoft Docs"
description: "Azure에서 실행 중인 SQL Server 2016 Vm에 대 한 hello 자동화 된 백업 기능에 설명 합니다. 이 문서는 hello 리소스 관리자를 사용 하 여 특정 tooVMs입니다."
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
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="53241-104">SQL Server 2016 Azure Virtual Machines의 자동화된 백업 v2(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="53241-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53241-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="53241-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="53241-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="53241-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="53241-107">자동화 된 백업 v2 자동으로 구성 [Azure 관리 되는 백업 tooMicrosoft](https://msdn.microsoft.com/library/dn449496.aspx) 모든 기존 및 새 데이터베이스를 SQL Server 2016 Standard, Enterprise 또는 Developer 버전을 실행 하는 Azure VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="53241-108">그러면 지속 Azure blob 저장소를 사용 하는 tooconfigure 정기적 데이터베이스 백업을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="53241-109">자동화 된 백업 v2 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="53241-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="53241-110">Prerequisites</span></span>
<span data-ttu-id="53241-111">자동화 된 백업 v2 toouse hello 다음 필수 구성 요소를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="53241-112">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="53241-112">**Operating System**:</span></span>

- <span data-ttu-id="53241-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="53241-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="53241-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="53241-114">Windows Server 2016</span></span>

<span data-ttu-id="53241-115">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="53241-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="53241-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="53241-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="53241-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="53241-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="53241-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="53241-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53241-119">자동화된 백업 v2는 SQL Server 2016에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="53241-120">SQL Server 2014를 사용 하는 경우 자동화 된 백업 v1 tooback 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="53241-121">자세한 내용은 [SQL Server 2014 Azure Virtual Machines의 자동화된 백업](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53241-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="53241-122">**데이터베이스 구성**:</span><span class="sxs-lookup"><span data-stu-id="53241-122">**Database configuration**:</span></span>

- <span data-ttu-id="53241-123">대상 데이터베이스는 hello 전체 복구 모델을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="53241-124">자세한 내용은 hello 영향에 대 한 hello 전체 복구 모델의 백업에 [백업에서 hello 전체 복구 모델](https://technet.microsoft.com/library/ms190217.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="53241-125">시스템 데이터베이스는 toouse 전체 복구 모델을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="53241-126">그러나 모델 또는 MSDB에 사용 되는 로그 백업을 toobe 필요한 경우 전체 복구 모델을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="53241-127">대상 데이터베이스 hello 기본 SQL Server 인스턴스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="53241-128">SQL Server IaaS 확장 hello 명명 된 인스턴스를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="53241-129">**Azure 배포 모델**:</span><span class="sxs-lookup"><span data-stu-id="53241-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="53241-130">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="53241-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="53241-131">자동화 된 백업 hello 의존 **SQL Server IaaS 에이전트 확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="53241-132">현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="53241-133">자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53241-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="53241-134">설정</span><span class="sxs-lookup"><span data-stu-id="53241-134">Settings</span></span>
<span data-ttu-id="53241-135">hello 다음 설명 v2 자동화 된 백업을 구성할 수 있는 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="53241-136">hello 실제 구성 단계는 hello Azure 포털 또는 Azure Windows PowerShell 명령을 사용 하는지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="53241-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="53241-137">기본 설정</span><span class="sxs-lookup"><span data-stu-id="53241-137">Basic Settings</span></span>

| <span data-ttu-id="53241-138">설정</span><span class="sxs-lookup"><span data-stu-id="53241-138">Setting</span></span> | <span data-ttu-id="53241-139">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="53241-139">Range (Default)</span></span> | <span data-ttu-id="53241-140">설명</span><span class="sxs-lookup"><span data-stu-id="53241-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53241-141">**자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="53241-141">**Automated Backup**</span></span> | <span data-ttu-id="53241-142">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="53241-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="53241-143">SQL Server 2016 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="53241-144">**보존 기간**</span><span class="sxs-lookup"><span data-stu-id="53241-144">**Retention Period**</span></span> | <span data-ttu-id="53241-145">1-30일(30일)</span><span class="sxs-lookup"><span data-stu-id="53241-145">1-30 days (30 days)</span></span> | <span data-ttu-id="53241-146">일 tooretain 백업의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="53241-147">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="53241-147">**Storage Account**</span></span> | <span data-ttu-id="53241-148">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="53241-148">Azure storage account</span></span> | <span data-ttu-id="53241-149">Blob 저장소에 자동화 된 백업 파일을 저장 하기 위한 Azure 저장소 계정 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="53241-150">컨테이너는 모든 백업 파일에이 위치 toostore 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="53241-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="53241-151">hello 날짜, 시간 및 데이터베이스 GUID hello 백업 파일 명명 규칙에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="53241-152">**암호화**</span><span class="sxs-lookup"><span data-stu-id="53241-152">**Encryption**</span></span> |<span data-ttu-id="53241-153">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="53241-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="53241-154">암호화 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-154">Enables or disables encryption.</span></span> <span data-ttu-id="53241-155">지정 된 hello에 hello 사용 되는 인증서 toorestore hello 백업 암호화를 사용 하는 경우 동일한 hello에 저장소 계정 **automaticbackup** ô ä ¢ hello 사용 하 여 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="53241-156">Hello 암호를 변경 하는 경우 해당 암호와 새 인증서가 생성 하지만 hello 이전 인증서 toorestore 이전 백업을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="53241-157">**암호**</span><span class="sxs-lookup"><span data-stu-id="53241-157">**Password**</span></span> |<span data-ttu-id="53241-158">암호 텍스트</span><span class="sxs-lookup"><span data-stu-id="53241-158">Password text</span></span> | <span data-ttu-id="53241-159">암호화 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-159">A password for encryption keys.</span></span> <span data-ttu-id="53241-160">암호화를 사용하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="53241-161">암호화 된 백업에서 순서 toorestore hello 올바른 암호와 hello 백업을 수행한 hello 시 사용 된 인증서 관련된 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="53241-162">고급 설정</span><span class="sxs-lookup"><span data-stu-id="53241-162">Advanced Settings</span></span>

| <span data-ttu-id="53241-163">설정</span><span class="sxs-lookup"><span data-stu-id="53241-163">Setting</span></span> | <span data-ttu-id="53241-164">범위(기본값)</span><span class="sxs-lookup"><span data-stu-id="53241-164">Range (Default)</span></span> | <span data-ttu-id="53241-165">설명</span><span class="sxs-lookup"><span data-stu-id="53241-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53241-166">**시스템 데이터베이스 백업**</span><span class="sxs-lookup"><span data-stu-id="53241-166">**System Database Backups**</span></span> | <span data-ttu-id="53241-167">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="53241-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="53241-168">이 기능은 또한 hello 시스템 데이터베이스를 백업 됩니다 사용 하도록 설정 하는 경우: Master, MSDB 및 Model입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="53241-169">Hello MSDB 및 Model 데이터베이스에 대 한 이들이 전체 복구 모드에 로그 백업을 toobe 수행 하려는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="53241-170">Master의 경우에는 로그 백업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="53241-171">또한 TempDB에 대해서도 백업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="53241-172">**백업 일정**</span><span class="sxs-lookup"><span data-stu-id="53241-172">**Backup Schedule**</span></span> | <span data-ttu-id="53241-173">수동/자동(자동)</span><span class="sxs-lookup"><span data-stu-id="53241-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="53241-174">기본적으로 hello 백업 일정은 자동으로 결정 될 hello 로그 증가에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="53241-175">수동 백업 일정 hello 사용자 toospecify hello 시간 창 백업을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="53241-176">이 경우 백업 에서만 사용 됩니다 hello에서 발생 빈도 지정 하 고 hello 하는 동안 지정된 된 날의 시간 창을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="53241-177">**전체 백업 빈도**</span><span class="sxs-lookup"><span data-stu-id="53241-177">**Full backup frequency**</span></span> | <span data-ttu-id="53241-178">매일/매주</span><span class="sxs-lookup"><span data-stu-id="53241-178">Daily/Weekly</span></span> | <span data-ttu-id="53241-179">전체 백업의 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-179">Frequency of full backups.</span></span> <span data-ttu-id="53241-180">두 경우 모두 hello 다음 예약된 시간 기간 동안 전체 백업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="53241-181">매주 옵션을 선택하면 백업은 모든 데이터베이스가 성공적으로 백업될 때까지 여러 날에 걸쳐 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="53241-182">**전체 백업 시작 시간**</span><span class="sxs-lookup"><span data-stu-id="53241-182">**Full backup start time**</span></span> | <span data-ttu-id="53241-183">00:00 – 23:00(01:00)</span><span class="sxs-lookup"><span data-stu-id="53241-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="53241-184">전체 백업이 수행될 수 있는 지정된 날의 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="53241-185">**전체 백업 시간 기간**</span><span class="sxs-lookup"><span data-stu-id="53241-185">**Full backup time window**</span></span> | <span data-ttu-id="53241-186">1-23시간(1시간)</span><span class="sxs-lookup"><span data-stu-id="53241-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="53241-187">지정된 된 날짜는 전체 백업이 수행 될 수의 hello 시간 창의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="53241-188">**로그 백업 빈도**</span><span class="sxs-lookup"><span data-stu-id="53241-188">**Log backup frequency**</span></span> | <span data-ttu-id="53241-189">5-60분(60분)</span><span class="sxs-lookup"><span data-stu-id="53241-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="53241-190">로그 백업의 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="53241-191">전체 백업 빈도 이해</span><span class="sxs-lookup"><span data-stu-id="53241-191">Understanding full backup frequency</span></span>
<span data-ttu-id="53241-192">일별 및 주별 전체 백업 간의 중요 한 toounderstand hello 차이</span><span class="sxs-lookup"><span data-stu-id="53241-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="53241-193">이를 위해 다음과 같은 두 가지 예제 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="53241-194">시나리오 1: 매주 백업</span><span class="sxs-lookup"><span data-stu-id="53241-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="53241-195">매우 큰 데이터베이스를 많이 포함하는 SQL Server VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="53241-196">월요일, 다음 설정을 hello로 자동화 된 백업 v2 사용:</span><span class="sxs-lookup"><span data-stu-id="53241-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="53241-197">백업 일정: **수동**</span><span class="sxs-lookup"><span data-stu-id="53241-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="53241-198">전체 백업 빈도: **매주**</span><span class="sxs-lookup"><span data-stu-id="53241-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="53241-199">전체 백업 시작 시간: **01:00**</span><span class="sxs-lookup"><span data-stu-id="53241-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="53241-200">전체 백업 시간 기간: **1시간**</span><span class="sxs-lookup"><span data-stu-id="53241-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="53241-201">즉, 해당 hello 다음 사용 가능한 백업 기간 1 시간 동안 오전 1 시에 화요일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="53241-202">해당 시간에 자동화된 백업은 한 번에 하나씩 데이터베이스를 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="53241-203">이 시나리오에서는 사용자 데이터베이스는 전체 백업이 처음 몇 데이터베이스 hello에 대 한 완료 됩니다 충분히 큰입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="53241-204">그러나 1 시간 후 hello 데이터베이스 일부만 백업 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="53241-205">이 경우 자동화 된 백업 수요일 오전 1 시간 동안 1 다음 날 데이터베이스 hello 남은 hello 백업 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="53241-206">일부 데이터베이스가 백업 된 당시에서, 하는 경우 동일한 다음 날에 hello hello 다시 시도 합니다 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="53241-207">이 과정은 모든 데이터베이스가 성공적으로 백업될 때까지 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="53241-208">다시 화요일이 되면 자동화된 백업은 모든 데이터베이스를 다시 한 번 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="53241-209">이 시나리오에서는 자동화 된 백업에 대해서만 hello 지정 된 시간 창 내에서 작동 하 고 각 데이터베이스는 백업할 주 마다 한 번만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53241-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="53241-210">또한 수 있다는 것 백업을 toospan hello에 있는 여러 일 경우 수 없는 가능한 toocomplete 모든 백업이 하루에 대 한 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="53241-211">시나리오 2: 매일 백업</span><span class="sxs-lookup"><span data-stu-id="53241-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="53241-212">매우 큰 데이터베이스를 많이 포함하는 SQL Server VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="53241-213">월요일, 다음 설정을 hello로 자동화 된 백업 v2 사용:</span><span class="sxs-lookup"><span data-stu-id="53241-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="53241-214">백업 일정: 수동</span><span class="sxs-lookup"><span data-stu-id="53241-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="53241-215">전체 백업 빈도: 매일</span><span class="sxs-lookup"><span data-stu-id="53241-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="53241-216">전체 백업 시작 시간: 22:00</span><span class="sxs-lookup"><span data-stu-id="53241-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="53241-217">전체 백업 시간 기간: 6시간</span><span class="sxs-lookup"><span data-stu-id="53241-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="53241-218">즉, 해당 hello 다음 사용 가능한 백업 기간 월요일 오후 6 시간 동안 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="53241-219">해당 시간에 자동화된 백업은 한 번에 하나씩 데이터베이스를 백업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="53241-220">그런 다음 화요일 오후 10부터 6시간 동안 모든 데이터베이스의 전체 백업이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53241-221">매일 백업 일정을 계획할 때이 시간 내 모든 데이터베이스를 백업할 수 있습니다 넓은 시간 창 tooensure 예약 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="53241-222">이 hello이 있는 경우 많은 양의 데이터 tooback 위로에서 특히 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="53241-223">Hello 포털의 구성</span><span class="sxs-lookup"><span data-stu-id="53241-223">Configuration in hello Portal</span></span>

<span data-ttu-id="53241-224">프로 비전 하는 동안 이나 기존 SQL Server 2016 Vm hello Azure 포털 tooconfigure 자동화 된 백업 v 2를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="53241-225">새 VM</span><span class="sxs-lookup"><span data-stu-id="53241-225">New VMs</span></span>

<span data-ttu-id="53241-226">Azure 포털 tooconfigure 자동화 된 백업 v2 hello를 사용 하 여 hello 리소스 관리자 배포 모델에서 새 SQL Server 2016 가상 컴퓨터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="53241-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="53241-227">Hello에 **SQL Server 설정을** 블레이드를 **자동화 된 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="53241-228">hello 다음 Azure 포털 스크린샷은 hello **SQL 자동화 된 백업** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Azure 포털에서 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="53241-230">자동화된 백업 v2는 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="53241-231">컨텍스트에 대해 hello 전체 항목에 참조 [Azure에서 SQL Server 가상 컴퓨터 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="53241-232">기존 VM</span><span class="sxs-lookup"><span data-stu-id="53241-232">Existing VMs</span></span>

<span data-ttu-id="53241-233">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="53241-234">다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![기존 VM에 대한 SQL 자동화된 백업](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="53241-236">Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 단추 자동 백업 섹션.</span><span class="sxs-lookup"><span data-stu-id="53241-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![기존 VM에 대한 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="53241-238">완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="53241-239">설정 하는 경우 자동화 된 백업을 hello에 대 한 처음으로, Azure hello 백그라운드에서 hello SQL Server IaaS 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="53241-240">이 시간 동안 hello Azure 포털 표시 되지 않습니다 자동화 된 백업이 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="53241-241">Hello 에이전트 toobe 설치에 대 일 분 정도 기다린 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="53241-242">해당 hello Azure 후 포털 hello 새 설정이 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="53241-243">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="53241-243">Configuration with PowerShell</span></span>

<span data-ttu-id="53241-244">PowerShell tooconfigure 자동화 된 백업 v 2를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="53241-245">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-245">Before you begin, you must:</span></span>

- <span data-ttu-id="53241-246">[다운로드 및 설치 최신 Azure PowerShell hello](http://aka.ms/webpi-azps)합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="53241-247">Windows PowerShell을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="53241-248">Hello hello 단계를 수행 하 여이 작업을 수행할 수 [구독을 구성](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) 섹션의 항목을 프로 비전 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="53241-249">Hello SQL IaaS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="53241-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="53241-250">Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전 하는 경우 SQL Server IaaS 확장 hello 이미 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="53241-251">설치 되는 경우 VM에 대 한 호출 하 여 확인할 수 있습니다 **Get AzureRmVM** 명령과 hello 검사 **확장** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="53241-252">SQL Server IaaS 에이전트 확장 hello가 설치 된 경우 "SqlIaaSAgent" 또는 "SQLIaaSExtension"으로 나열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="53241-253">**ProvisioningState** 에 hello 확장 "Succeeded" 표시도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="53241-254">설치 되어 있지 않거나 toobe 프로 비전 실패를 하는 경우 다음 명령을 hello로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="53241-255">또한 toohello VM 이름 및 리소스 그룹에서 지정 해야 hello 영역 (**$region**) VM에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="53241-256"><a id="verifysettings"></a> 현재 설정 확인</span><span class="sxs-lookup"><span data-stu-id="53241-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="53241-257">자동화 된 백업 구축 하는 동안 설정한 경우 현재 구성 PowerShell toocheck를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="53241-258">Hello 실행 **Get AzureRmVMSqlServerExtension** 명령을 실행 한 hello 검사 **AutoBackupSettings** 속성:</span><span class="sxs-lookup"><span data-stu-id="53241-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="53241-259">유사한 toohello 다음 출력을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-259">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="53241-260">출력을 표시 하는 경우 **사용** 너무 설정**False**, tooenable 자동화 된 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="53241-261">hello 다행 스럽게도 사용 하도록 설정 하 고 hello에 자동화 된 백업을 구성할 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="53241-262">이 정보에 대 한 hello 다음 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="53241-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="53241-263">Hello 설정을 변경한 후 즉시을 선택 하면 경우 얻을 수 다시 hello 오래 된 구성 값 수입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="53241-264">몇 분 정도 기다린 후 hello 설정을 확인 toomake 변경 내용이 적용 되었는지 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="53241-265">자동화된 백업 v2 구성</span><span class="sxs-lookup"><span data-stu-id="53241-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="53241-266">사용할 수 있습니다 toomodify 뿐만 아니라 PowerShell tooenable 자동화 된 백업 구성 및 동작 언제 든 지.</span><span class="sxs-lookup"><span data-stu-id="53241-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="53241-267">첫째, 선택 하거나 hello에 대 한 저장소 계정에 백업 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="53241-268">hello 다음 스크립트 저장소 계정을 선택 하거나 선택 존재 하지 않는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53241-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="53241-269">자동화된 백업을 사용할 경우 프리미엄 저장소에 백업을 저장할 수 없지만 프리미엄 저장소를 사용하는 VM 디스크에서 백업을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="53241-270">다음 hello를 사용 하 여 **새로 AzureRmVMSqlServerAutoBackupConfig** tooenable 명령 및 hello Azure 저장소 계정에 자동화 된 백업 v2 hello 설정을 toostore 백업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="53241-271">이 예제에서는 hello 백업은 10 일 동안 유지 toobe를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="53241-272">시스템 데이터베이스 백업이 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-272">System database backups are enabled.</span></span> <span data-ttu-id="53241-273">전체 백업은 20시부터 시작해서 2시간 동안 진행되는 것으로 매주 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="53241-274">로그 백업은 30분 간격으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="53241-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="53241-275">두 번째 명령은 hello **집합 AzureRmVMSqlServerExtension**, 업데이트 hello 이러한 설정을 사용 하 여 Azure VM을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

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

<span data-ttu-id="53241-276">몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="53241-277">tooenable 암호화 hello 이전 스크립트 toopass hello 수정 **EnableEncryption** hello에 대 한 암호 (보안 문자열) 함께 매개 변수 **CertificatePassword** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="53241-278">hello 다음 스크립트 hello 이전 예제의 자동화 된 백업 설정을 hello 있으며 특정 암호화를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="53241-279">프로그램 설정이 적용 되어 tooconfirm [hello 자동화 된 백업 구성을 확인](#verifysettings)합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="53241-280">자동화된 백업 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="53241-280">Disable Automated Backup</span></span>
<span data-ttu-id="53241-281">자동화 된 백업, hello 하지 않고 동일한 스크립트 실행된 hello toodisable **-사용 하도록 설정** 매개 변수 toohello **새로 AzureRmVMSqlServerAutoBackupConfig** 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="53241-282">hello 없을 경우 hello **-사용 하도록 설정** 매개 변수가 신호 hello 명령 toodisable hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="53241-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="53241-283">설치의 경우와 마찬가지로 자동화 된 백업에 몇 분 toodisable를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="53241-284">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="53241-284">Example script</span></span>
<span data-ttu-id="53241-285">hello 다음 스크립트를 제공 변수의 tooenable를 사용자 지정할 수 있으며 VM에 대 한 자동화 된 백업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="53241-286">여기에서 toocustomize hello 스크립트 요구 사항에 기반 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53241-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="53241-287">예를 들어 시스템 데이터베이스의 toodisable hello 백업 하려는 경우 toomake 변경 내용이 거 나 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="53241-288">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53241-288">Next steps</span></span>
<span data-ttu-id="53241-289">자동화된 백업 v2는 Azure VM에서 관리되는 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="53241-290">것이 중요 너무[관리 되는 백업에 대 한 hello 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello 동작 및 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53241-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="53241-291">추가 백업 찾 및 hello 항목에 Azure Vm에서 SQL Server에 대 한 지침을 복원할 수 있습니다: [Azure 가상 컴퓨터의 SQL Server 용 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53241-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="53241-292">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53241-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="53241-293">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53241-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

