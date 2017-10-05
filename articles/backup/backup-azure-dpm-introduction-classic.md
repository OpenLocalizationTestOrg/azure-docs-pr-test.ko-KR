---
title: "Azure 클래식 포털에 DPM 워크로드 백업 | Microsoft Docs"
description: "Azure 백업 서비스를 사용하여 DPM 서버를 백업하는 방법 소개"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "System Center Data Protection Manager, 데이터 보호 관리자, dpm 백업"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: a9a516cfdfaf4b95c4f0121a66e90f6e71206e9f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="preparing-to-back-up-workloads-to-azure-with-dpm"></a><span data-ttu-id="48cda-104">DPM을 통해 Azure에서 워크로드 백업 준비</span><span class="sxs-lookup"><span data-stu-id="48cda-104">Preparing to back up workloads to Azure with DPM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48cda-105">Azure 백업 서버</span><span class="sxs-lookup"><span data-stu-id="48cda-105">Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
> * [<span data-ttu-id="48cda-106">SCDPM</span><span class="sxs-lookup"><span data-stu-id="48cda-106">SCDPM</span></span>](backup-azure-dpm-introduction.md)
> * [<span data-ttu-id="48cda-107">Azure 백업 서버(클래식)</span><span class="sxs-lookup"><span data-stu-id="48cda-107">Azure Backup Server (Classic)</span></span>](backup-azure-microsoft-azure-backup-classic.md)
> * [<span data-ttu-id="48cda-108">SCDPM(클래식)</span><span class="sxs-lookup"><span data-stu-id="48cda-108">SCDPM (Classic)</span></span>](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="48cda-109">이 문서에서는 Microsoft Azure 백업을 사용하여 System Center Data Protection Manager(DPM) 서버와 워크로드를 보호하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-109">This article provides an introduction to using Microsoft Azure Backup to protect your System Center Data Protection Manager (DPM) servers and workloads.</span></span> <span data-ttu-id="48cda-110">이 문서를 읽어 보면 다음을 이해하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-110">By reading it, you’ll understand:</span></span>

* <span data-ttu-id="48cda-111">Azure DPM 서버 백업 작동 방식</span><span class="sxs-lookup"><span data-stu-id="48cda-111">How Azure DPM server backup works</span></span>
* <span data-ttu-id="48cda-112">원활한 백업 경험을 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="48cda-112">The prerequisites to achieve a smooth backup experience</span></span>
* <span data-ttu-id="48cda-113">발생하는 일반적인 오류 및 오류를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="48cda-113">The typical errors encountered and how to deal with them</span></span>
* <span data-ttu-id="48cda-114">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="48cda-114">Supported scenarios</span></span>

<span data-ttu-id="48cda-115">System Center DPM 백업 파일 및 애플리케이션 데이터</span><span class="sxs-lookup"><span data-stu-id="48cda-115">System Center DPM backs up file and application data.</span></span> <span data-ttu-id="48cda-116">DPM에 백업된 데이터는 테이프나 디스크에 저장하거나 Microsoft Azure 백업을 사용하여 Azure에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-116">Data backed up to DPM can be stored on tape, on disk, or backed up to Azure with Microsoft Azure Backup.</span></span> <span data-ttu-id="48cda-117">DPM 은 Azure 백업과 다음과 같이 상호작용합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-117">DPM interacts with Azure Backup as follows:</span></span>

* <span data-ttu-id="48cda-118">**물리적 서버 또는 온-프레미스 가상 컴퓨터로 배포하는 DPM** — DPM을 물리적 서버 또는 온-프레미스 Hyper-V 가상 컴퓨터로 배포하는 경우, 디스크나 테이프 백업에 더해 데이터를 Azure 백업 자격 증명 모음에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-118">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data to an Azure Backup vault in addition to disk and tape backup.</span></span>
* <span data-ttu-id="48cda-119">**Azure 가상 컴퓨터로 배포하는 DPM** — System Center 2012 R2 업데이트 3부터 DPM을 Azure 가상 컴퓨터로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-119">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span></span> <span data-ttu-id="48cda-120">DPM을 Azure 가상 컴퓨터로 배포하는 경우, 데이터를 DPM Azure 가상 컴퓨터에 연결된 Azure 디스크에 백업하거나 데이터 스토리지를 Azure 백업 자격 증명 모음에 백업하여 오프로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-120">If DPM is deployed as an Azure virtual machine you can back up data to Azure disks attached to the DPM Azure virtual machine, or you can offload the data storage by backing it up to an Azure Backup vault.</span></span>

## <a name="why-backup-your-dpm-servers"></a><span data-ttu-id="48cda-121">DPM 서버를 백업하는 이유</span><span class="sxs-lookup"><span data-stu-id="48cda-121">Why backup your DPM servers?</span></span>
<span data-ttu-id="48cda-122">DPM 서버 백업에 Azure 백업을 사용할 경우의 비즈니스 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-122">The business benefits of using Azure Backup for backing up DPM servers include:</span></span>

* <span data-ttu-id="48cda-123">온-프레미스 DPM 배포의 경우, 테이프에 대한 장기 배포 대신 Azure 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-123">For on-premises DPM deployment, you can use Azure backup as an alternative to long-term deployment to tape.</span></span>
* <span data-ttu-id="48cda-124">Azure로 DPM을 배포하는 경우, Azure 백업을 사용하면 Azure 디스크에서 저장소를 오프로드할 수 있어 오래된 데이터를 Azure 백업에 저장하고 새 데이터를 디스크에 저장하여 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-124">For DPM deployments in Azure, Azure Backup allows you to offload storage from the Azure disk, allowing you to scale up by storing older data in Azure Backup and new data on disk.</span></span>

## <a name="how-does-dpm-server-backup-work"></a><span data-ttu-id="48cda-125">DPM 서버 백업 작동 방식</span><span class="sxs-lookup"><span data-stu-id="48cda-125">How does DPM server backup work?</span></span>
<span data-ttu-id="48cda-126">가상 컴퓨터를 백업하려면 먼저 데이터의 지정 시간 스냅숏이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-126">To back up a virtual machine, first a point-in-time snapshot of the data is needed.</span></span> <span data-ttu-id="48cda-127">Azure 백업 서비스는 예약된 시간에 백업 작업을 시작하고 스냅숏을 만드는 백업 확장을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-127">The Azure Backup service initiates the backup job at the scheduled time, and triggers the backup extension to take a snapshot.</span></span> <span data-ttu-id="48cda-128">백업 확장은 일관성을 유지하기 위해 게스트 내 VSS 서비스와 조정되고, 일관성이 달성되면 Azure 저장소 서비스의 Blob 스냅숏 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-128">The backup extension coordinates with the in-guest VSS service to achieve consistency, and invokes the blob snapshot API of the Azure Storage service once consistency has been reached.</span></span> <span data-ttu-id="48cda-129">이 작업은 종료하지 않고 가상 컴퓨터의 일관된 디스크 스냅숏을 가져오기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-129">This is done to get a consistent snapshot of the disks of the virtual machine, without having to shut it down.</span></span>

<span data-ttu-id="48cda-130">스냅숏이 생성된 후 Azure 백업 서비스가 백업 자격 증명 모음으로 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-130">After the snapshot has been taken, the data is transferred by the Azure Backup service to the backup vault.</span></span> <span data-ttu-id="48cda-131">서비스는 마지막 백업에서 변경된 블록만 식별하고 전송하여 백업 자격 증명 모음 및 네트워크를 효율적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-131">The service takes care of identifying and transferring only the blocks that have changed from the last backup making the backups storage and network efficient.</span></span> <span data-ttu-id="48cda-132">데이터 전송이 완료되면 스냅숏이 제거되고 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-132">When the data transfer is completed, the snapshot is removed and a recovery point is created.</span></span> <span data-ttu-id="48cda-133">이 복구 지점은 Azure 클래식 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-133">This recovery point can be seen in the  Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="48cda-134">Linux 가상 컴퓨터의 경우 파일 일치 백업만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-134">For Linux virtual machines, only file-consistent backup is possible.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="48cda-135">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48cda-135">Prerequisites</span></span>
<span data-ttu-id="48cda-136">DPM 데이터를 백업하기 위해 다음과 같이 Azure 백업을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-136">Prepare Azure Backup to back up DPM data as follows:</span></span>

1. <span data-ttu-id="48cda-137">**백업 자격 증명 모음을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="48cda-137">**Create a Backup vault**.</span></span> <span data-ttu-id="48cda-138">구독에서 백업 자격 증명 모음을 만들지 않은 경우 이 문서의 Azure Portal 버전 - [DPM을 사용하여 Azure로 작업 백업 준비](backup-azure-dpm-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48cda-138">If you haven't created a Backup vault in your subscription, see the Azure portal version of this article - [Prepare to back up workloads to Azure with DPM](backup-azure-dpm-introduction.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="48cda-139">2017년 3월부터는 백업 자격 증명 모음을 만드는 데 더 이상 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-139">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
  > <span data-ttu-id="48cda-140">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-140">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="48cda-141">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48cda-141">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="48cda-142">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-142">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="48cda-143">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-143">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="48cda-144">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="48cda-144">**By November 1, 2017**:</span></span>
  >- <span data-ttu-id="48cda-145">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-145">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
  >- <span data-ttu-id="48cda-146">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-146">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="48cda-147">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-147">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
  >

2. <span data-ttu-id="48cda-148">**저장소 자격 증명 다운로드** — Azure 백업에서 자격 증명 모음에 대해 만든 관리 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-148">**Download vault credentials** — In Azure Backup, upload the management certificate you created to the vault.</span></span>
3. <span data-ttu-id="48cda-149">**Azure 백업 에이전트 설치 및 서버 등록** — Azure 백업에서 각 DPM 서버에 에이전트를 설치하고 백업 자격 증명 모음에 DPM 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-149">**Install the Azure Backup Agent and register the server** — From Azure Backup, install the agent on each DPM server and register the DPM server in the backup vault.</span></span>

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a><span data-ttu-id="48cda-150">요구 사항(및 제한 사항)</span><span class="sxs-lookup"><span data-stu-id="48cda-150">Requirements (and limitations)</span></span>
* <span data-ttu-id="48cda-151">DPM은 물리적 서버 또는 System Center 2012 SP1 또는 System Center 2012 R2에 설치된 Hyper-V 가상 컴퓨터로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-151">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span></span> <span data-ttu-id="48cda-152">최소 System Center 2012 R2 DPM 2012 R2 업데이트 롤업 3에서 실행되는 Azure 가상 컴퓨터 또는 최소 System Center 2012 R2 업데이트 롤업 5에서 실행되는 VMWare의 Windows 가상 컴퓨터로도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-152">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span></span>
* <span data-ttu-id="48cda-153">DPM을 System Center 2012 SP1에서 실행 중인 경우 System Center Data Protection Manager SP1용 업데이트 롤업 2를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-153">If you’re running DPM with System Center 2012 SP1, you should install Update Rollup 2 for System Center Data Protection Manager SP1.</span></span> <span data-ttu-id="48cda-154">Azure 백업 에이전트를 설치하기 전에 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-154">This is required before you can install the Azure Backup Agent.</span></span>
* <span data-ttu-id="48cda-155">DPM 서버는 Windows PowerShell 및 .Net Framework 4.5가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-155">The DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span></span>
* <span data-ttu-id="48cda-156">DPM은 대부분의 워크로드를 Azure 백업에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-156">DPM can back up most workloads to Azure Backup.</span></span> <span data-ttu-id="48cda-157">지원되는 전체 목록은 아래의 Azure 백업 지원 항목을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="48cda-157">For a full list of what’s supported see the Azure Backup support items below.</span></span>
* <span data-ttu-id="48cda-158">Azure 백업에 저장된 데이터는 “테이프에 복사” 옵션으로 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-158">Data stored in Azure Backup can’t be recovered with the “copy to tape” option.</span></span>
* <span data-ttu-id="48cda-159">Azure 백업 기능을 사용할 수 있는 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-159">You’ll need an Azure account with the Azure Backup feature enabled.</span></span> <span data-ttu-id="48cda-160">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-160">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="48cda-161">[Azure 백업 가격 정책](https://azure.microsoft.com/pricing/details/backup/)을 읽어보십시오.</span><span class="sxs-lookup"><span data-stu-id="48cda-161">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>
* <span data-ttu-id="48cda-162">Azure 백업을 사용하려면 백업하고자 하는 서버에 Azure 백업 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-162">Using Azure Backup requires the Azure Backup Agent to be installed on the servers you want to back up.</span></span> <span data-ttu-id="48cda-163">각 서버에서는 백업 중인 데이터 크기의 10% 이상을 로컬 저장소로 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-163">Each server must have at least 10% of the size of the data that is being backed up, available as local free storage.</span></span> <span data-ttu-id="48cda-164">예를 들어 100GB 데이터를 백업하는 경우 스크래치 위치에 최소 10GB의 여유 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-164">For example, backing up 100 GB of data requires a minimum of 10 GB of free space in the scratch location.</span></span> <span data-ttu-id="48cda-165">최소값은 10%이지만 15%의 로컬 여유 저장소 공간을 캐시 위치에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-165">While the minimum is 10%, 15% of free local storage space to be used for the cache location is recommended.</span></span>
* <span data-ttu-id="48cda-166">데이터는 Azure 자격 증명 모음 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-166">Data will be stored in the Azure vault storage.</span></span> <span data-ttu-id="48cda-167">Azure 백업 자격 증명 모음에 백업할 수 있는 데이터의 양에는 제한이 없지만 데이터 원본(예를 들면 가상 컴퓨터 또는 데이터베이스)의 크기는 54,400GB를 초과해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-167">There’s no limit to the amount of data you can back up to an Azure Backup vault but the size of a data source (for example a virtual machine or database) shouldn’t exceed 54,400 GB.</span></span>

<span data-ttu-id="48cda-168">다음 파일 형식은 Azure에 대한 백업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-168">These file types are supported for back up to Azure:</span></span>

* <span data-ttu-id="48cda-169">암호화(전체 백업에만 해당)</span><span class="sxs-lookup"><span data-stu-id="48cda-169">Encrypted (Full backups only)</span></span>
* <span data-ttu-id="48cda-170">압축(증분 백업 지원)</span><span class="sxs-lookup"><span data-stu-id="48cda-170">Compressed (Incremental backups supported)</span></span>
* <span data-ttu-id="48cda-171">스파스(증분 백업 지원)</span><span class="sxs-lookup"><span data-stu-id="48cda-171">Sparse (Incremental backups supported)</span></span>
* <span data-ttu-id="48cda-172">압축 및 스파스(스파스로 처리됨)</span><span class="sxs-lookup"><span data-stu-id="48cda-172">Compressed and sparse (Treated as Sparse)</span></span>

<span data-ttu-id="48cda-173">다음은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-173">And these are unsupported:</span></span>

* <span data-ttu-id="48cda-174">대/소문자 구분 파일 시스템의 서버는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-174">Servers on case-sensitive file systems aren’t supported.</span></span>
* <span data-ttu-id="48cda-175">하드 링크(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="48cda-175">Hard links (Skipped)</span></span>
* <span data-ttu-id="48cda-176">재분석 지점(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="48cda-176">Reparse points (Skipped)</span></span>
* <span data-ttu-id="48cda-177">암호화 및 압축(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="48cda-177">Encrypted and compressed (Skipped)</span></span>
* <span data-ttu-id="48cda-178">암호화 및 스파스(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="48cda-178">Encrypted and sparse (Skipped)</span></span>
* <span data-ttu-id="48cda-179">압축된 스트림</span><span class="sxs-lookup"><span data-stu-id="48cda-179">Compressed stream</span></span>
* <span data-ttu-id="48cda-180">스파스 스트림</span><span class="sxs-lookup"><span data-stu-id="48cda-180">Sparse stream</span></span>

> [!NOTE]
> <span data-ttu-id="48cda-181">System Center 2012 DPM SP1부터는 DPM으로 보호되는 워크로드를 Microsoft Azure 백업을 사용하여 Azure에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48cda-181">From in System Center 2012 DPM with SP1 onwards, you can backup up workloads protected by DPM to Azure using Microsoft Azure Backup.</span></span>
>
>
