---
title: "DPM 작업 부하 tooAzure 클래식 포털을 aaaBack | Microsoft Docs"
description: "소개 toobacking hello Azure 백업 서비스를 사용 하 여 DPM 서버를"
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
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a><span data-ttu-id="0d141-104">Dpm 작업 부하 tooAzure tooback 준비</span><span class="sxs-lookup"><span data-stu-id="0d141-104">Preparing tooback up workloads tooAzure with DPM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d141-105">Azure 백업 서버</span><span class="sxs-lookup"><span data-stu-id="0d141-105">Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
> * [<span data-ttu-id="0d141-106">SCDPM</span><span class="sxs-lookup"><span data-stu-id="0d141-106">SCDPM</span></span>](backup-azure-dpm-introduction.md)
> * [<span data-ttu-id="0d141-107">Azure 백업 서버(클래식)</span><span class="sxs-lookup"><span data-stu-id="0d141-107">Azure Backup Server (Classic)</span></span>](backup-azure-microsoft-azure-backup-classic.md)
> * [<span data-ttu-id="0d141-108">SCDPM(클래식)</span><span class="sxs-lookup"><span data-stu-id="0d141-108">SCDPM (Classic)</span></span>](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="0d141-109">이 문서에서는 System Center Data Protection Manager (DPM) 서버 및 작업 소개 toousing Microsoft Azure 백업 tooprotect를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-109">This article provides an introduction toousing Microsoft Azure Backup tooprotect your System Center Data Protection Manager (DPM) servers and workloads.</span></span> <span data-ttu-id="0d141-110">이 문서를 읽어 보면 다음을 이해하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-110">By reading it, you’ll understand:</span></span>

* <span data-ttu-id="0d141-111">Azure DPM 서버 백업 작동 방식</span><span class="sxs-lookup"><span data-stu-id="0d141-111">How Azure DPM server backup works</span></span>
* <span data-ttu-id="0d141-112">hello 필수 구성 요소 tooachieve 부드러운 백업 경험</span><span class="sxs-lookup"><span data-stu-id="0d141-112">hello prerequisites tooachieve a smooth backup experience</span></span>
* <span data-ttu-id="0d141-113">발생 하는 일반적인 오류 hello와 방법을 사람과 toodeal</span><span class="sxs-lookup"><span data-stu-id="0d141-113">hello typical errors encountered and how toodeal with them</span></span>
* <span data-ttu-id="0d141-114">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="0d141-114">Supported scenarios</span></span>

<span data-ttu-id="0d141-115">System Center DPM 백업 파일 및 애플리케이션 데이터</span><span class="sxs-lookup"><span data-stu-id="0d141-115">System Center DPM backs up file and application data.</span></span> <span data-ttu-id="0d141-116">TooDPM 백업 된 데이터 디스크에 테이프에 저장할 또는 tooAzure Microsoft Azure 백업에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-116">Data backed up tooDPM can be stored on tape, on disk, or backed up tooAzure with Microsoft Azure Backup.</span></span> <span data-ttu-id="0d141-117">DPM 은 Azure 백업과 다음과 같이 상호작용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-117">DPM interacts with Azure Backup as follows:</span></span>

* <span data-ttu-id="0d141-118">**물리적 서버 또는 온-프레미스 가상 컴퓨터로 배포 된 DPM** — DPM을 물리적 서버 또는 백업할 수 있습니다는 온-프레미스 Hyper-v 가상 컴퓨터로 배포 되는 경우를 데이터 tooan Azure 백업 자격 증명 모음에 또한 toodisk 및 테이프 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-118">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data tooan Azure Backup vault in addition toodisk and tape backup.</span></span>
* <span data-ttu-id="0d141-119">**Azure 가상 컴퓨터로 배포하는 DPM** — System Center 2012 R2 업데이트 3부터 DPM을 Azure 가상 컴퓨터로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-119">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span></span> <span data-ttu-id="0d141-120">DPM 데이터 tooAzure 디스크를 백업할 수는 Azure 가상 컴퓨터로 배포 하는 경우 toohello DPM Azure 가상 컴퓨터를 연결 하거나 tooan Azure 백업 자격 증명 모음을 백업 하 여 hello 데이터 저장소를 오프 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-120">If DPM is deployed as an Azure virtual machine you can back up data tooAzure disks attached toohello DPM Azure virtual machine, or you can offload hello data storage by backing it up tooan Azure Backup vault.</span></span>

## <a name="why-backup-your-dpm-servers"></a><span data-ttu-id="0d141-121">DPM 서버를 백업하는 이유</span><span class="sxs-lookup"><span data-stu-id="0d141-121">Why backup your DPM servers?</span></span>
<span data-ttu-id="0d141-122">Azure 백업을 사용 하 여 DPM 서버를 백업 하기 위한의 hello 비즈니스 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-122">hello business benefits of using Azure Backup for backing up DPM servers include:</span></span>

* <span data-ttu-id="0d141-123">온-프레미스 DPM 배포에 대 한 대체 toolong 용어 배포 tootape로 Azure 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-123">For on-premises DPM deployment, you can use Azure backup as an alternative toolong-term deployment tootape.</span></span>
* <span data-ttu-id="0d141-124">Azure에서 내 DPM 배포를 Azure 백업 하면 hello Azure 디스크에서에서 toooffload 저장소 수 있게 tooscale를 Azure 백업 및 최신 데이터를 디스크에 오래 된 데이터를 저장 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-124">For DPM deployments in Azure, Azure Backup allows you toooffload storage from hello Azure disk, allowing you tooscale up by storing older data in Azure Backup and new data on disk.</span></span>

## <a name="how-does-dpm-server-backup-work"></a><span data-ttu-id="0d141-125">DPM 서버 백업 작동 방식</span><span class="sxs-lookup"><span data-stu-id="0d141-125">How does DPM server backup work?</span></span>
<span data-ttu-id="0d141-126">hello 데이터의 지정 시간 스냅숏이 필요한 첫 번째 가상 컴퓨터를 tooback 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-126">tooback up a virtual machine, first a point-in-time snapshot of hello data is needed.</span></span> <span data-ttu-id="0d141-127">hello Azure 백업 서비스를 시작 hello 백업 작업 hello에 예약 된 시간, 및 트리거 hello 예비 내선 번호 tootake 스냅숏으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-127">hello Azure Backup service initiates hello backup job at hello scheduled time, and triggers hello backup extension tootake a snapshot.</span></span> <span data-ttu-id="0d141-128">hello 게스트 VSS와 hello 예비 내선 번호 좌표 tooachieve 일관성 서비스 및 일관성에 도달한 후 hello Azure 저장소 서비스의 hello blob 스냅샷 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-128">hello backup extension coordinates with hello in-guest VSS service tooachieve consistency, and invokes hello blob snapshot API of hello Azure Storage service once consistency has been reached.</span></span> <span data-ttu-id="0d141-129">이 tooshut 필요 없이 tooget hello 디스크 hello 가상 컴퓨터의 일관 된 스냅숏을 수행 아래로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-129">This is done tooget a consistent snapshot of hello disks of hello virtual machine, without having tooshut it down.</span></span>

<span data-ttu-id="0d141-130">Hello 스냅숏 수행 된 후 hello 데이터 hello Azure 백업 서비스 toohello 백업 자격 증명 모음으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-130">After hello snapshot has been taken, hello data is transferred by hello Azure Backup service toohello backup vault.</span></span> <span data-ttu-id="0d141-131">hello 서비스를 식별 하 고 hello 백업 저장소 및 네트워크를 효율적으로 만드는 hello 마지막 백업에서 변경 된 블록만 hello 전송 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-131">hello service takes care of identifying and transferring only hello blocks that have changed from hello last backup making hello backups storage and network efficient.</span></span> <span data-ttu-id="0d141-132">Hello 데이터 전송이 완료 되 면 hello 스냅숏을 제거 되 고 복구 지점이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-132">When hello data transfer is completed, hello snapshot is removed and a recovery point is created.</span></span> <span data-ttu-id="0d141-133">이 복구 지점은 hello Azure 클래식 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-133">This recovery point can be seen in hello  Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0d141-134">Linux 가상 컴퓨터의 경우 파일 일치 백업만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-134">For Linux virtual machines, only file-consistent backup is possible.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="0d141-135">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0d141-135">Prerequisites</span></span>
<span data-ttu-id="0d141-136">DPM 데이터를 Azure 백업 tooback를 다음과 같이 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-136">Prepare Azure Backup tooback up DPM data as follows:</span></span>

1. <span data-ttu-id="0d141-137">**백업 자격 증명 모음을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="0d141-137">**Create a Backup vault**.</span></span> <span data-ttu-id="0d141-138">구독에서 백업 자격 증명 모음을 만들지 않은 경우 참조 hello Azure이 문서의-포털 버전 [dpm 작업 부하 tooAzure tooback 준비](backup-azure-dpm-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-138">If you haven't created a Backup vault in your subscription, see hello Azure portal version of this article - [Prepare tooback up workloads tooAzure with DPM](backup-azure-dpm-introduction.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0d141-139">2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-139">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
  > <span data-ttu-id="0d141-140">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-140">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="0d141-141">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-141">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0d141-142">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-142">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="0d141-143">2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-143">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="0d141-144">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="0d141-144">**By November 1, 2017**:</span></span>
  >- <span data-ttu-id="0d141-145">모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-145">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
  >- <span data-ttu-id="0d141-146">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-146">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="0d141-147">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-147">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
  >

2. <span data-ttu-id="0d141-148">**자격 증명 모음 자격 증명을 다운로드** -에 Azure 백업으로 toohello 자격 증명 모음을 만든 hello 관리 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-148">**Download vault credentials** — In Azure Backup, upload hello management certificate you created toohello vault.</span></span>
3. <span data-ttu-id="0d141-149">**Hello Azure 백업 에이전트를 설치 하 고 hello 서버 등록** -에서 Azure 백업, 각 DPM 서버에 hello 에이전트를 설치 하 고 hello 백업 자격 증명 모음에 hello DPM 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-149">**Install hello Azure Backup Agent and register hello server** — From Azure Backup, install hello agent on each DPM server and register hello DPM server in hello backup vault.</span></span>

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a><span data-ttu-id="0d141-150">요구 사항(및 제한 사항)</span><span class="sxs-lookup"><span data-stu-id="0d141-150">Requirements (and limitations)</span></span>
* <span data-ttu-id="0d141-151">DPM은 물리적 서버 또는 System Center 2012 SP1 또는 System Center 2012 R2에 설치된 Hyper-V 가상 컴퓨터로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-151">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span></span> <span data-ttu-id="0d141-152">최소 System Center 2012 R2 DPM 2012 R2 업데이트 롤업 3에서 실행되는 Azure 가상 컴퓨터 또는 최소 System Center 2012 R2 업데이트 롤업 5에서 실행되는 VMWare의 Windows 가상 컴퓨터로도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-152">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span></span>
* <span data-ttu-id="0d141-153">DPM을 System Center 2012 SP1에서 실행 중인 경우 System Center Data Protection Manager SP1용 업데이트 롤업 2를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-153">If you’re running DPM with System Center 2012 SP1, you should install Update Rollup 2 for System Center Data Protection Manager SP1.</span></span> <span data-ttu-id="0d141-154">Hello Azure 백업 에이전트를 설치 하기 전에 이것이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-154">This is required before you can install hello Azure Backup Agent.</span></span>
* <span data-ttu-id="0d141-155">hello DPM 서버에 Windows PowerShell 및.Net 있어야 Framework 4.5가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-155">hello DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span></span>
* <span data-ttu-id="0d141-156">DPM은 대부분 작업 tooAzure 백업에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-156">DPM can back up most workloads tooAzure Backup.</span></span> <span data-ttu-id="0d141-157">Hello Azure 백업에 대 한 참조를 지원 되는 작업의 전체 목록은 아래 항목을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-157">For a full list of what’s supported see hello Azure Backup support items below.</span></span>
* <span data-ttu-id="0d141-158">Hello "tootape 복사" 옵션으로 Azure 백업에 저장 된 데이터를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-158">Data stored in Azure Backup can’t be recovered with hello “copy tootape” option.</span></span>
* <span data-ttu-id="0d141-159">Azure 계정이 있으세요 hello Azure 백업 기능을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-159">You’ll need an Azure account with hello Azure Backup feature enabled.</span></span> <span data-ttu-id="0d141-160">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-160">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0d141-161">[Azure 백업 가격 정책](https://azure.microsoft.com/pricing/details/backup/)을 읽어보십시오.</span><span class="sxs-lookup"><span data-stu-id="0d141-161">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>
* <span data-ttu-id="0d141-162">Azure 백업을 사용 하 여 hello Azure 백업 에이전트 toobe tooback를 원하는 hello 서버에 설치 된 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-162">Using Azure Backup requires hello Azure Backup Agent toobe installed on hello servers you want tooback up.</span></span> <span data-ttu-id="0d141-163">각 서버에 백업 되 고, 로컬 여유 저장소로 사용할 수 있는 hello 데이터의 hello 크기의 10% 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-163">Each server must have at least 10% of hello size of hello data that is being backed up, available as local free storage.</span></span> <span data-ttu-id="0d141-164">예를 들어, 100GB 데이터의 백업 10GB의 사용 가능한 공간 hello 스크래치 위치에는 최소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-164">For example, backing up 100 GB of data requires a minimum of 10 GB of free space in hello scratch location.</span></span> <span data-ttu-id="0d141-165">Hello 최소 10% 이지만, 가능 hello 캐시 위치에 사용할 로컬 여유 저장소 공간 toobe의 15%를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-165">While hello minimum is 10%, 15% of free local storage space toobe used for hello cache location is recommended.</span></span>
* <span data-ttu-id="0d141-166">데이터는 hello Azure 자격 증명 모음 저장소에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-166">Data will be stored in hello Azure vault storage.</span></span> <span data-ttu-id="0d141-167">없는 제한 toohello 양의 데이터 tooan Azure 백업 자격 증명 모음에 백업할 수 있지만 (예: 가상 컴퓨터 또는 데이터베이스) 데이터 소스의 hello 크기 54,400 GB를 초과 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-167">There’s no limit toohello amount of data you can back up tooan Azure Backup vault but hello size of a data source (for example a virtual machine or database) shouldn’t exceed 54,400 GB.</span></span>

<span data-ttu-id="0d141-168">이러한 파일 형식은 tooAzure 백업에 대 한 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-168">These file types are supported for back up tooAzure:</span></span>

* <span data-ttu-id="0d141-169">암호화(전체 백업에만 해당)</span><span class="sxs-lookup"><span data-stu-id="0d141-169">Encrypted (Full backups only)</span></span>
* <span data-ttu-id="0d141-170">압축(증분 백업 지원)</span><span class="sxs-lookup"><span data-stu-id="0d141-170">Compressed (Incremental backups supported)</span></span>
* <span data-ttu-id="0d141-171">스파스(증분 백업 지원)</span><span class="sxs-lookup"><span data-stu-id="0d141-171">Sparse (Incremental backups supported)</span></span>
* <span data-ttu-id="0d141-172">압축 및 스파스(스파스로 처리됨)</span><span class="sxs-lookup"><span data-stu-id="0d141-172">Compressed and sparse (Treated as Sparse)</span></span>

<span data-ttu-id="0d141-173">다음은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-173">And these are unsupported:</span></span>

* <span data-ttu-id="0d141-174">대/소문자 구분 파일 시스템의 서버는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-174">Servers on case-sensitive file systems aren’t supported.</span></span>
* <span data-ttu-id="0d141-175">하드 링크(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="0d141-175">Hard links (Skipped)</span></span>
* <span data-ttu-id="0d141-176">재분석 지점(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="0d141-176">Reparse points (Skipped)</span></span>
* <span data-ttu-id="0d141-177">암호화 및 압축(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="0d141-177">Encrypted and compressed (Skipped)</span></span>
* <span data-ttu-id="0d141-178">암호화 및 스파스(건너뜀)</span><span class="sxs-lookup"><span data-stu-id="0d141-178">Encrypted and sparse (Skipped)</span></span>
* <span data-ttu-id="0d141-179">압축된 스트림</span><span class="sxs-lookup"><span data-stu-id="0d141-179">Compressed stream</span></span>
* <span data-ttu-id="0d141-180">스파스 스트림</span><span class="sxs-lookup"><span data-stu-id="0d141-180">Sparse stream</span></span>

> [!NOTE]
> <span data-ttu-id="0d141-181">s p 1부터, System Center 2012 DPM의 Microsoft Azure 백업을 사용 하 여 DPM tooAzure에 의해 보호 되는 워크 로드를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d141-181">From in System Center 2012 DPM with SP1 onwards, you can backup up workloads protected by DPM tooAzure using Microsoft Azure Backup.</span></span>
>
>
