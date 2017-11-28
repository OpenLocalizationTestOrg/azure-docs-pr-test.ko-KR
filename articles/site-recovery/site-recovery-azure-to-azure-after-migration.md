---
title: "Site Recovery를 사용하여 Azure로 마이그레이션한 후 Azure 지역 간의 재해 복구를 설정하기 위한 컴퓨터 준비 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 Azure로 마이그레이션한 후 Azure 지역 간의 재해 복구를 설정하기 위해 컴퓨터를 준비하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="d6eb5-103">Azure Site Recovery를 사용하여 Azure로 마이그레이션한 후 Azure VM을 다른 지역에 복제</span><span class="sxs-lookup"><span data-stu-id="d6eb5-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="d6eb5-104">Azure VM(가상 컴퓨터)에 대한 Azure Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="d6eb5-105">개요</span><span class="sxs-lookup"><span data-stu-id="d6eb5-105">Overview</span></span>

<span data-ttu-id="d6eb5-106">이 문서에서는 Azure Site Recovery를 사용하여 Azure Virtual Machines를 온-프레미스 환경에서 Azure로 마이그레이션한 후 두 Azure 지역 간의 복제를 위해 이러한 컴퓨터를 준비하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="d6eb5-107">재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="d6eb5-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="d6eb5-108">워크로드를 Azure로 이동하는 기업이 점점 증가하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="d6eb5-109">업무에 중요한 온-프레미스 프로덕션 워크로드를 Azure로 이동하는 기업에서는 Azure 지역에서 중단으로부터 보호하고 규정을 준수하기 위해 이러한 워크로드에 대한 재해 복구를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="d6eb5-110">마이그레이션된 컴퓨터의 복제를 준비하기 위한 단계</span><span class="sxs-lookup"><span data-stu-id="d6eb5-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="d6eb5-111">마이그레이션된 컴퓨터를 다른 Azure 지역으로 복제하기 위한 설정을 준비하려면</span><span class="sxs-lookup"><span data-stu-id="d6eb5-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="d6eb5-112">마이그레이션을 완료하려면</span><span class="sxs-lookup"><span data-stu-id="d6eb5-112">Complete migration.</span></span>
2. <span data-ttu-id="d6eb5-113">필요한 경우 Azure 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="d6eb5-114">모바일 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="d6eb5-115">VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-115">Restart the VM.</span></span>

<span data-ttu-id="d6eb5-116">이러한 단계는 다음 섹션에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="d6eb5-117">1단계: Hyper-V VM, VMware VM 및 물리적 서버에서 실행 중인 워크로드를 마이그레이션하여 Azure VM에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="d6eb5-118">복제를 설정하고 온-프레미스 Hyper-V, VMware 및 실제 워크로드를 Azure로 마이그레이션하려면 [Azure Site Recovery를 사용하여 Azure 지역 간에 Azure IaaS 가상 컴퓨터 마이그레이션](site-recovery-migrate-to-azure.md) 문서의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="d6eb5-119">마이그레이션 후 장애 조치를 커밋하거나 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="d6eb5-120">대신 마이그레이션할 각 컴퓨터에 대해 **마이그레이션 완료** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="d6eb5-121">**복제된 항목**에서 VM를 마우스 오른쪽 단추로 클릭하고 **마이그레이션 완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="d6eb5-122">**확인**을 클릭하여 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="d6eb5-123">**Site Recovery 작업**의 마이그레이션 완료 작업을 모니터링하여 VM 속성에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="d6eb5-124">**마이그레이션 완료** 작업은 마이그레이션 프로세스를 완료하고 가상 컴퓨터에 대한 복제를 제거하며 컴퓨터에 대한 Site Recovery 청구를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="d6eb5-126">2단계 - 가상 컴퓨터에 Azure VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="d6eb5-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="d6eb5-127">Site Recovery 확장이 작동하고 VM을 보호하려면 Azure [VM 에이전트](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux)를 가상 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d6eb5-128">9.7.0.0 버전부터 모바일 서비스 설치 관리자는 Windows 가상 컴퓨터에 사용 가능한 최신 Azure VM 에이전트도 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="d6eb5-129">마이그레이션 시 가상 컴퓨터는 Site Recovery 확장을 포함하여 모든 VM 확장을 사용하기 위한 에이전트 설치 필수 구성 요소를 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="d6eb5-130">Azure VM 에이전트는 마이그레이션된 컴퓨터에 설치된 모바일 서비스가 버전 9.6 이하인 경우에만 수동으로 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="d6eb5-131">다음 표에서는 VM 에이전트를 설치하고 설치 유효성을 검사하는 방법에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="d6eb5-132">**작업**</span><span class="sxs-lookup"><span data-stu-id="d6eb5-132">**Operation**</span></span> | <span data-ttu-id="d6eb5-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d6eb5-133">**Windows**</span></span> | <span data-ttu-id="d6eb5-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="d6eb5-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6eb5-135">VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="d6eb5-135">Installing the VM agent</span></span> |<span data-ttu-id="d6eb5-136">[에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="d6eb5-137">설치를 완료하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="d6eb5-138">최신 [Linux 에이전트](../virtual-machines/linux/agent-user-guide.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="d6eb5-139">설치를 완료하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="d6eb5-140">리포지토리에서 배포 에이전트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="d6eb5-141">GitHub에서 직접 Linux VM 에이전트를 설치하는 것은 *좋지 않습니다*.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="d6eb5-142">VM 에이전트 설치 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="d6eb5-142">Validating the VM agent installation</span></span> |<span data-ttu-id="d6eb5-143">1. Azure VM에서 C:\WindowsAzure\Packages 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="d6eb5-144">WaAppAgent.exe 파일을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="d6eb5-145">2. 파일을 마우스 오른쪽 단추로 클릭하고 **속성**으로 이동한 다음 **세부 정보** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="d6eb5-146">**제품 버전** 필드가 2.6.1198.718 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="d6eb5-147">해당 없음</span><span class="sxs-lookup"><span data-stu-id="d6eb5-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="d6eb5-148">3단계: 마이그레이션된 가상 컴퓨터에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="d6eb5-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="d6eb5-149">온-프레미스 VMware 컴퓨터 또는 물리적 Windows/Linux 서버를 마이그레이션한 경우 마이그레이션된 가상 컴퓨터에서 모바일 서비스를 수동으로 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d6eb5-150">Azure로 마이그레이션된 Hyper-V VM에는 이 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="d6eb5-151">Windows Server VM에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="d6eb5-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="d6eb5-152">Windows Server 컴퓨터에서 모바일 서비스를 제거하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="d6eb5-153">Windows UI를 사용하여 제거</span><span class="sxs-lookup"><span data-stu-id="d6eb5-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="d6eb5-154">제어판에서 **프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="d6eb5-155">**Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버**를 선택한 다음 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="d6eb5-156">명령 프롬프트에서 제거</span><span class="sxs-lookup"><span data-stu-id="d6eb5-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="d6eb5-157">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="d6eb5-158">모바일 서비스를 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="d6eb5-159">Linux 컴퓨터에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="d6eb5-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="d6eb5-160">Linux 서버에서 **루트** 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="d6eb5-161">터미널에서 /user/local/ASR로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="d6eb5-162">모바일 서비스를 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="d6eb5-163">4단계: VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d6eb5-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="d6eb5-164">모바일 서비스를 제거한 후 다른 Azure 지역으로의 복제를 설정하기 전에 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d6eb5-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6eb5-165">Next steps</span></span>
- <span data-ttu-id="d6eb5-166">[Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="d6eb5-167">[Azure Virtual Machines 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb5-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
