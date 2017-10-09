---
title: "사이트 복구 자격 증명 모음 aaaUpgrade tooan Azure 복구 서비스 자격 증명 모음"
description: "어떻게 tooupgrade는 Azure Site Recovery 자격 증명 모음 tooa 복구 서비스 자격 증명 모음에 대해 알아봅니다."
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="30a63-103">사이트 복구 자격 증명 모음 tooan Azure 리소스 관리자 기반 복구 서비스 자격 증명 모음 업그레이드</span><span class="sxs-lookup"><span data-stu-id="30a63-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="30a63-104">이 문서에서는 Azure Site Recovery tooupgrade 진행 중인 복제에 영향 주지 않고 tooAzure 리소스 관리자 기반 복구 서비스 자격 증명 모음 자격 증명 모음 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="30a63-105">Azure Resource Manager 기능 및 이점에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a63-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="30a63-106">소개</span><span class="sxs-lookup"><span data-stu-id="30a63-106">Introduction</span></span>
<span data-ttu-id="30a63-107">복구 서비스 자격 증명 모음에는 hello 클라우드에서 기본적으로 백업 및 재해 복구를 관리 하기 위한 Azure 리소스 관리자 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="30a63-108">사용할 수 있는 통합 된 자격 증명 모음 hello 새 Azure 포털에서 하 고 hello 클래식 백업 대체 이며 사이트 복구 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="30a63-109">Recovery Services 자격 증명 모음은 다음을 포함하는 기능 배열을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="30a63-110">Azure Resource Manager 지원: 가상 컴퓨터 및 물리적 컴퓨터를 Azure Resource Manager 스택으로 보호 및 장애 조치(failover)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="30a63-111">디스크는 제외: 임시 파일 또는 않도록 toouse에 대 한 모든 대역폭이 높은 변동 데이터, 있는 경우 볼륨을 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="30a63-112">이 기능에서 현재 사용 된 *VMware tooAzure* 및 *Hyper-v tooAzure* tooother 시나리오에도 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="30a63-113">Premium 및 로컬 중복 저장소에 대 한 지원: 이제는 서버 보호할 프리미엄 저장소에서 높은 고객으로 tooprotect 응용 프로그램을 허용 하는 계정 입/출력 작업 / 초 (IOPS).</span><span class="sxs-lookup"><span data-stu-id="30a63-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="30a63-114">이 기능은 현재에서 사용할 수 있습니다. *VMware tooAzure*합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="30a63-115">간소화 되어 시작 환경: 향상 된 hello 시작 환경을 설계 되었습니다 쉽게 toomake 재해 복구 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="30a63-116">백업 및 사이트 복구 관리에서 같은 자격 증명 모음의 hello: 이제 재해 복구를 위해 서버를 보호 하거나 hello에서 백업을 수행할 수 같은 자격 증명 모음 관리 오버 헤드를 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="30a63-117">업그레이드 하는 hello 환경과 기능에 대 한 자세한 내용은 참조 hello [저장소, 백업 및 복구 블로그](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="30a63-118">핵심 기능</span><span class="sxs-lookup"><span data-stu-id="30a63-118">Salient features</span></span>

* <span data-ttu-id="30a63-119">진행 중인 복제에 영향을 주지 않음: 진행 중인 복제는 업그레이드 중과 후에 중단 없이 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="30a63-120">추가 비용 없음: 추가 비용 없이 업데이트된 기능의 전체 집합을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="30a63-121">데이터 손실 없음:이 프로세스는 업그레이드 및 마이그레이션 하지 이기 때문에 기존 복제 복구 지점 및 설정이 그대로 동안과 그 후 hello 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="30a63-122">Hello 자격 증명 모음 업그레이드 하는 동안 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="30a63-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="30a63-123">Hello 업그레이드 하는 동안 새 서버 등록 또는 복제 가상 컴퓨터 (VM)를 사용 하는 등의 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="30a63-124">데이터 읽기 또는 쓰기 toohello 자격 증명 모음의 보호 항목, 진행 중인 복제와 같은 데이터 toohello 자격을 포함 하는 작업은 중단 없이 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="30a63-125">Tooautomation 및 hello 업그레이드 한 후 도구 변경</span><span class="sxs-lookup"><span data-stu-id="30a63-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="30a63-126">Hello 클래식 배포 모델 toohello 리소스 관리자 배포 모델에서 업그레이드 하는 hello 자격 증명 모음 유형 hello 기존 자동화 또는 도구 tooensure hello 업그레이드 후 toowork 계속 되도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="30a63-127">Hello 업그레이드에 대 한 환경 준비</span><span class="sxs-lookup"><span data-stu-id="30a63-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="30a63-128">PowerShell을 설치 하거나 업그레이드할 tooversion 5 이상</span><span class="sxs-lookup"><span data-stu-id="30a63-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="30a63-129">Hello 최신 버전의 Azure PowerShell MSI 설치</span><span class="sxs-lookup"><span data-stu-id="30a63-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="30a63-130">Hello 복구 서비스 자격 증명 모음에 대 한 업그레이드 스크립트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="30a63-131">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30a63-131">Prerequisites</span></span>
<span data-ttu-id="30a63-132">사이트 복구에서 tooupgrade tooAzure 리소스 관리자 기반 복구 서비스 자격 증명 모음 자격 증명 모음, hello 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="30a63-133">최소 에이전트 버전이: 서버에 설치 하는 Azure Site Recovery Provider의 hello 버전 5.1.1700.0 있어야 합니다. 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="30a63-134">지원되는 구성: SAN(저장 영역 네트워크) 또는 SQL Server AlwaysOn 가용성 그룹으로 자격 증명 모음을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="30a63-135">다른 모든 구성은 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="30a63-136">Hello 업그레이드 후 PowerShell 통해 저장소 매핑을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="30a63-137">지원 되는 배포 시나리오: 자격 증명 모음 hello 아니어야 *VMware tooAzure* 레거시 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="30a63-138">계속 진행 하기 전에 먼저 toohello 향상 된 배포 모델을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="30a63-139">활성 사용자가 시작한 작업이 없습니다 관리와 관련 된 작업 평면: 업그레이드 하는 동안 액세스 toohello 관리 평면은 제한 되므로 hello 업그레이드를 트리거하기 전에 모든 관리 평면 동작을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="30a63-140">이 프로세스에는 진행 중인 복제가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="30a63-141">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="30a63-141">Frequently asked questions</span></span>

<span data-ttu-id="30a63-142">**이 업그레이드가 진행 중인 복제에 주는 영향은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="30a63-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="30a63-143">아니요.</span><span class="sxs-lookup"><span data-stu-id="30a63-143">No.</span></span> <span data-ttu-id="30a63-144">진행 중인 복제 하는 동안 및 hello 업그레이드 한 후 중단 없이 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="30a63-145">**사이트 간 VPN 및 IP 설정 같은 toonetwork 설정을 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="30a63-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="30a63-146">hello 업그레이드 hello 네트워크 설정에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="30a63-147">모든 Azure-온-프레미스 연결은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="30a63-148">**자격 증명 모음 toomy hello 가까운 미래에에서 tooupgrade 합니까 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="30a63-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="30a63-149">2017 년 9 월부터 hello 이전 Azure 포털에서 사이트 복구 자격 증명 모음에 대 한 지원이 중단 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="30a63-150">Hello 업그레이드 기능 toomove toohello 새 포털을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="30a63-151">**이 마이그레이션 계획으로 기존 도구는 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="30a63-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="30a63-152">도구 toohello 리소스 관리자 배포 모델을 업데이트, 업그레이드 계획에 고려해 야 합니다 hello 가장 중요 한 변경 내용 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="30a63-153">hello 복구 서비스 자격 증명 모음 hello 리소스 관리자 배포 모델을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="30a63-154">**기간 않습니다 hello 관리 평면 가동 중지 시간이 마지막?**</span><span class="sxs-lookup"><span data-stu-id="30a63-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="30a63-155">일반적으로 hello 업그레이드 약 15 too30 분 정도 걸리며 최대 1 시간까지 tooa을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="30a63-156">**업그레이드한 후에 롤백할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="30a63-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="30a63-157">아니요.</span><span class="sxs-lookup"><span data-stu-id="30a63-157">No.</span></span> <span data-ttu-id="30a63-158">Hello 리소스 성공적으로 업그레이드 된 후에 롤백이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="30a63-159">**있습니까 있는지 확인할 수 내 구독 또는 리소스 toosee 업그레이드할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="30a63-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="30a63-160">예.</span><span class="sxs-lookup"><span data-stu-id="30a63-160">Yes.</span></span> <span data-ttu-id="30a63-161">Hello 플랫폼에서 지 원하는 업그레이드 옵션을 hello 업그레이드 hello 첫 번째 단계는 hello 리소스가 업그레이드 가능성을 toovalidate을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="30a63-162">Hello 유효성 검사에 실패 하는 경우 적절 한 오류 메시지나 경고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="30a63-163">**Hello 업그레이드 문제를 보고 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="30a63-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="30a63-164">모든 오류의 경우 hello 업그레이드 하는 동안 hello 오류에 나열 된 hello 작업 ID를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="30a63-165">Microsoft 기술 지원 서비스는 hello 문제를 해결에서는 사전 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="30a63-166">구독 ID로, 자격 증명 모음 이름, 작업 id입니다. 지원 팀 hello 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="30a63-167">지원은 tooresolve hello 문제를 가능한 한 신속 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="30a63-168">명시적으로 지시 toodo 있지 않은 경우 hello 작업을 다시 시도 하지 마세요 Microsoft에서 등입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="30a63-169">Hello 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="30a63-169">Run hello script</span></span>

<span data-ttu-id="30a63-170">PowerShell에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="30a63-171">업그레이드 하는 hello 자격 증명 모음과 연결 된 구독 Id: hello 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="30a63-172">업그레이드 하는 hello 자격 증명 모음의 VaultName: hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="30a63-173">업그레이드 하는 hello 자격 증명 모음의 위치: hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="30a63-174">ResourceType: Site Recovery 자격 증명 모음에 대한 HyperVRecoveryManagerVault입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="30a63-175">TargetResourceGroupName: hello 넣을 hello 리소스 그룹에 배치 하는 자격 증명 모음 toobe를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="30a63-176">TargetResourceGroupName은 Azure Resource Manager의 기존 리소스 그룹 또는 새 리소스 그룹일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="30a63-177">제공 된 TargetResourceGroupName hello가 없는 경우 만들어집니다 hello 업그레이드의 일부로 hello에 동일한 hello 자격 증명 모음과 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="30a63-178">자세한 내용은의 hello "리소스 그룹" 섹션을 참조 하십시오. [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="30a63-179">리소스 그룹 이름 지정 주체 toocertain 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="30a63-180">tooprevent 자격 증명 모음 있는지 tooobserve hello 명명 규칙을 신중 하 게 될 실패를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="30a63-181">예:</span><span class="sxs-lookup"><span data-stu-id="30a63-181">For example:</span></span>
    >
    ><span data-ttu-id="30a63-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="30a63-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="30a63-183">또는 다음 스크립트는 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="30a63-184">필요한 hello 매개 변수에 대 한 hello 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="30a63-185">PowerShell 스크립트 hello 메시지 있습니다 tooenter 자격 증명을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="30a63-186">입력을 두 번 hello 클래식 배포 모델 계정에 대 한 한 번에 대해서 한 hello Azure 리소스 관리자 계정.</span><span class="sxs-lookup"><span data-stu-id="30a63-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="30a63-187">자격 증명을 입력 한 후 사용자 인프라 설치 충족 hello 요구 사항에 앞에서 언급 한 hello 스크립트 실행 검사 toodetermine 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="30a63-188">Hello 필수 구성 요소를 검사 하 고 확인 한 후 메시지 표시 tooproceed hello 자격 증명 모음 업그레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="30a63-189">업그레이드 자격 증명 모음 hello 업그레이드 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="30a63-190">hello 전체 업그레이드는 15 too30 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="30a63-191">Hello 업그레이드가 성공적으로 완료 된 후 hello 새 Azure 포털의 hello 업그레이드 모음에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="30a63-192">업그레이드 후 자격 증명 모음 관리</span><span class="sxs-lookup"><span data-stu-id="30a63-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="30a63-193">Hello 복구 서비스 자격 증명 모음에서 Azure Site Recovery를 사용 하 여 복제</span><span class="sxs-lookup"><span data-stu-id="30a63-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="30a63-194">이제 하나의 영역 tooanother에서 Azure Vm을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="30a63-195">자세한 내용은 [Azure Site Recovery를 사용하여 지역 간 Azure VM 복제](site-recovery-azure-to-azure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a63-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="30a63-196">VMware Vm tooAzure를 복제 하는 방법에 대 한 자세한 내용은 참조 [Site Recovery와 VMware Vm 복제 tooAzure](vmware-walkthrough-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="30a63-197">Hyper-v Vm (VMM 없음) tooAzure를 복제 하는 방법에 대 한 자세한 내용은 참조 [복제 Hyper-v 가상 컴퓨터 (VMM 없음) tooAzure](hyper-v-site-walkthrough-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="30a63-198">(VMM)과 Hyper-v Vm tooAzure를 복제 하는 방법에 대 한 자세한 내용은 참조 [복제 Hyper-v 가상 컴퓨터에서 사이트 복구를 사용 하 여 VMM 클라우드에 tooAzure hello Azure 포털](vmm-to-azure-walkthrough-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="30a63-199">하이퍼-VMs (VMM)과 tooa 보조 사이트를 복제 하는 방법에 대 한 자세한 내용은 참조 [복제 Hyper-v 가상 컴퓨터 VMM 클라우드에 tooa 보조 VMM 사이트를 사용 하 여 Azure 포털 hello](site-recovery-vmm-to-vmm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="30a63-200">VMware Vm tooa 보조 사이트를 복제 하는 방법에 대 한 자세한 내용은 참조 [Replicate 온-프레미스 VMware 가상 컴퓨터 또는 실제 서버 hello 클래식 Azure 포털에서 보조 사이트 tooa](site-recovery-vmware-to-vmware.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="30a63-201">복제된 항목 보기</span><span class="sxs-lookup"><span data-stu-id="30a63-201">View your replicated items</span></span>

<span data-ttu-id="30a63-202">hello 다음 이미지에서는 hello 자격 증명 모음에 대 한 주요 엔터티를 표시 하는 hello 복구 서비스 자격 증명 모음 대시보드 페이지</span><span class="sxs-lookup"><span data-stu-id="30a63-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="30a63-203">tooview hello 자격 증명 모음에 있는 보호 된 엔터티 목록을 선택 **사이트 복구** > **복제 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![복제된 항목](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="30a63-205">hello 다음 그림에 나와 복제 된 항목 및 hello를 보기 위한 hello 워크플로 **장애 조치** 장애 조치를 개시 하는 것에 대 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![복제된 항목](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="30a63-207">복제 설정 보기</span><span class="sxs-lookup"><span data-stu-id="30a63-207">View your replication settings</span></span>

<span data-ttu-id="30a63-208">Hello 사이트 복구 자격 증명 모음에 각 보호 그룹은 다른 복제 설정을 복사 빈도, 복구 지점 보존, 응용 프로그램 일관성 스냅숏 빈도와 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="30a63-209">Hello 복구 서비스 자격 증명 모음에 이러한 설정은 복제 정책으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="30a63-210">hello hello 정책 이름은 hello 보호 그룹이 나 hello hello 이름을 *primarycloud_Policy*합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="30a63-211">복제 정책에 대 한 자세한 내용은 참조 [VMware tooAzure에 대 한 복제 정책을 관리](site-recovery-setup-replication-settings-vmware.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30a63-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
