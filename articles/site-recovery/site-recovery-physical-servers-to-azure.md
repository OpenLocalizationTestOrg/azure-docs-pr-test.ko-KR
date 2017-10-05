---
title: "Azure에 물리적 서버 복제 | Microsoft Docs"
description: "Azure Site Recovery를 배포하여 Azure Portal을 사용하여 온-프레미스 Windows/Linux 물리적 서버에서 Azure로 복제, 장애 조치(failover) 및 복구를 오케스트레이션하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: a9655ce1540c788d02d178eb619d2051cddda1c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
---
# <a name="replicate-physical-machines-to-azure-by-using-site-recovery"></a><span data-ttu-id="166e9-103">Site Recovery를 사용하여 Azure에 물리적 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="166e9-103">Replicate physical machines to Azure by using Site Recovery</span></span>


<span data-ttu-id="166e9-104">이 문서에서는 Azure Portal에서 Azure Site Recovery 서비스를 사용하여 온-프레미스 물리적 컴퓨터를 Azure에 복제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-104">This article describes how to replicate on-premises physical machines to Azure by using the Azure Site Recovery service in the Azure portal.</span></span>

<span data-ttu-id="166e9-105">물리적 컴퓨터를 Azure에 마이그레이션하려는 경우(장애 조치만 해당) 자세히 알아보려면 [Site Recovery를 사용하여 Azure에 마이그레이션](site-recovery-migrate-to-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="166e9-105">If you want to migrate physical machines to Azure (failover only), read [Migrate to Azure with Site Recovery](site-recovery-migrate-to-azure.md) to learn more.</span></span>

<span data-ttu-id="166e9-106">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="166e9-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="166e9-107">Prerequisites</span></span>

<span data-ttu-id="166e9-108">**지원 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="166e9-108">**Support requirement**</span></span> | <span data-ttu-id="166e9-109">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="166e9-109">**Details**</span></span>
--- | ---
<span data-ttu-id="166e9-110">**Azure**</span><span class="sxs-lookup"><span data-stu-id="166e9-110">**Azure**</span></span> | <span data-ttu-id="166e9-111">[Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-111">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="166e9-112">**온-프레미스 구성 서버**</span><span class="sxs-lookup"><span data-stu-id="166e9-112">**On-premises configuration server**</span></span> | <span data-ttu-id="166e9-113">Windows Server 2012 R2 이상이 실행되는 온-프레미스 컴퓨터(물리적 또는 VMware VM).</span><span class="sxs-lookup"><span data-stu-id="166e9-113">On-premises machine (physical or VMware VM) running Windows Server 2012 R2 or later.</span></span> <span data-ttu-id="166e9-114">Site Recovery를 배포하는 동안 구성 서버를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-114">You set up the configuration server during Site Recovery deployment.</span></span><br/><br/> <span data-ttu-id="166e9-115">기본적으로 프로세스 서버와 마스터 대상 서버도 이 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-115">By default, the process server and master target server are also installed on this machine.</span></span> <span data-ttu-id="166e9-116">확장하는 경우 별도 프로세스 서버가 필요하며 구성 서버와 동일한 요구 사항을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-116">When you scale up, you might need a separate process server, and it has the same requirements as the configuration server.</span></span><br/><br/> <span data-ttu-id="166e9-117">이러한 구성 요소에 대 한 자세한 [원본 환경 설정을 설정](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-117">Learn more about these components in [Set up the source environment](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).</span></span>
<span data-ttu-id="166e9-118">**온-프레미스 VM**</span><span class="sxs-lookup"><span data-stu-id="166e9-118">**On-premises VMs**</span></span> | <span data-ttu-id="166e9-119">복제하려는 컴퓨터는 [지원되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)를 실행하고 [Azure 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-119">Machines you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="166e9-120">**URL**</span><span class="sxs-lookup"><span data-stu-id="166e9-120">**URLs**</span></span> | <span data-ttu-id="166e9-121">구성 서버는 다음 URL에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-121">The configuration server needs access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="166e9-122">IP 주소 기반 방화벽 규칙이 있는 경우 해당 규칙이 Azure와의 통신을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-122">If you have IP address-based firewall rules, ensure that they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="166e9-123">[Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS(443) 포트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-123">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="166e9-124">구독하는 Azure 지역과 미국 서부에 해당하는 IP 주소 범위를 허용하세요(액세스 제어 및 ID 관리에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="166e9-124">Allow IP address ranges for the Azure region of your subscription and for West US (used for access control and identity management).</span></span><br/><br/> <span data-ttu-id="166e9-125">MySQL을 다운로드할 URL인 http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-125">Allow this URL for the MySQL download: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.</span></span>
<span data-ttu-id="166e9-126">**모바일 서비스**</span><span class="sxs-lookup"><span data-stu-id="166e9-126">**Mobility service**</span></span> | <span data-ttu-id="166e9-127">이 서비스는 복제하려는 각 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-127">This service is installed on each machine you want to replicate.</span></span>

## <a name="limitations"></a><span data-ttu-id="166e9-128">제한 사항</span><span class="sxs-lookup"><span data-stu-id="166e9-128">Limitations</span></span>

<span data-ttu-id="166e9-129">**제한 사항**</span><span class="sxs-lookup"><span data-stu-id="166e9-129">**Limitation**</span></span> | <span data-ttu-id="166e9-130">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="166e9-130">**Details**</span></span>
--- | ---
<span data-ttu-id="166e9-131">**Azure**</span><span class="sxs-lookup"><span data-stu-id="166e9-131">**Azure**</span></span> | <span data-ttu-id="166e9-132">저장소 및 네트워크 계정은 자격 증명 모음과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-132">Storage and network accounts must be in the same region as the vault.</span></span><br/><br/> <span data-ttu-id="166e9-133">프리미엄 저장소 계정을 사용하는 경우 복제 로그를 저장할 표준 저장소 계정도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-133">If you use a premium storage account, you also need a standard store account to store replication logs.</span></span><br/><br/> <span data-ttu-id="166e9-134">중부 및 남부 인도에서는 프리미엄 계정에 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-134">You can't replicate to premium accounts in Central and South India.</span></span>
<span data-ttu-id="166e9-135">**온-프레미스 구성 서버**</span><span class="sxs-lookup"><span data-stu-id="166e9-135">**On-premises configuration server**</span></span> | <span data-ttu-id="166e9-136">VMware VM에서 구성 서버를 설치하는 경우 VM 어댑터 유형은 VMXNET3이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-136">If you install the configuration server on a VMware VM, the VM adapter type should be VMXNET3.</span></span> <span data-ttu-id="166e9-137">그렇지 않은 경우 [이 업데이트를 설치하세요.](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)</span><span class="sxs-lookup"><span data-stu-id="166e9-137">If it isn't, [install this update](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).</span></span><br/><br/> <span data-ttu-id="166e9-138">VMware VM을 사용하는 경우 vSphere PowerCLI 6.0을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-138">If you're using a VMware VM, vSphere PowerCLI 6.0 should be installed on it.</span></span><br/><br> <span data-ttu-id="166e9-139">컴퓨터는 도메인 컨트롤러가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-139">The machine shouldn't be a domain controller.</span></span><br/><br/> <span data-ttu-id="166e9-140">컴퓨터에는 고정 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-140">The machine should have a static IP address.</span></span><br/><br/> <span data-ttu-id="166e9-141">호스트 이름은 15자 이하여야 하고 운영 체제에서는 영어를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-141">The host name should be 15 characters or less, and the operating system should be in English.</span></span>
<span data-ttu-id="166e9-142">**복제된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="166e9-142">**Replicated machines**</span></span> | <span data-ttu-id="166e9-143">[Azure VM 제한 사항](site-recovery-prereq.md#azure-requirements)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-143">Verify [Azure VM limitations](site-recovery-prereq.md#azure-requirements).</span></span><br/><br/> <span data-ttu-id="166e9-144">일관된 데이터 지점으로 함께 복구할 동일한 워크로드를 실행하는 컴퓨터를 활성화하는 다중 VM 일관성을 사용하도록 설정하려면 컴퓨터에서 20004 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-144">If you want to enable multi-VM consistency, which enables machines running the same workload to be recovered together to a consistent data point, open port 20004 on the machine.</span></span><br/><br/> <span data-ttu-id="166e9-145">특정 유형의 [Linux 저장소](site-recovery-support-matrix-to-azure.md#support-for-storage)가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-145">Specific types of [Linux storage](site-recovery-support-matrix-to-azure.md#support-for-storage) are supported.</span></span>
<span data-ttu-id="166e9-146">**장애 복구**</span><span class="sxs-lookup"><span data-stu-id="166e9-146">**Failback**</span></span> | <span data-ttu-id="166e9-147">Azure에서 실제 컴퓨터로 장애 복구를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-147">You can't fail back from Azure to a physical machine.</span></span> <span data-ttu-id="166e9-148">장애 조치 후 온-프레미스로 장애 복구할 수 있으려면, VMware 환경이 필요합니다. 그래야 VMware VM으로 장애 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-148">If you want to be able to fail back to on-premises after failover, you need a VMware environment so that you can fail back to a VMware VM.</span></span>


## <a name="set-up-azure"></a><span data-ttu-id="166e9-149">Azure 설정</span><span class="sxs-lookup"><span data-stu-id="166e9-149">Set up Azure</span></span>

1. <span data-ttu-id="166e9-150">[Azure 네트워크를 설정합니다](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="166e9-150">[Set up an Azure network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

      <span data-ttu-id="166e9-151">a.</span><span class="sxs-lookup"><span data-stu-id="166e9-151">a.</span></span> <span data-ttu-id="166e9-152">Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-152">Azure VMs are placed in this network when they're created after failover.</span></span>

      <span data-ttu-id="166e9-153">b.</span><span class="sxs-lookup"><span data-stu-id="166e9-153">b.</span></span> <span data-ttu-id="166e9-154">Azure [Resource Manager](../resource-manager-deployment-model.md) 또는 클래식 모드에서 네트워크를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-154">You can set up a network in Azure [Resource Manager](../resource-manager-deployment-model.md) or in classic mode.</span></span>

2. <span data-ttu-id="166e9-155">복제 데이터를 저장할 [Azure Storage 계정](../storage/storage-create-storage-account.md#create-a-storage-account)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-155">Set up an [Azure storage account](../storage/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>

    <span data-ttu-id="166e9-156">a.</span><span class="sxs-lookup"><span data-stu-id="166e9-156">a.</span></span> <span data-ttu-id="166e9-157">계정은 표준 또는 [프리미엄](../storage/storage-premium-storage.md)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-157">The account can be standard or [premium](../storage/storage-premium-storage.md).</span></span>

    <span data-ttu-id="166e9-158">b.</span><span class="sxs-lookup"><span data-stu-id="166e9-158">b.</span></span> <span data-ttu-id="166e9-159">Resource Manager 또는 클래식 모드에서 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-159">You can set up an account in Resource Manager or in classic mode.</span></span>

## <a name="prepare-the-configuration-server"></a><span data-ttu-id="166e9-160">구성 서버를 준비합니다</span><span class="sxs-lookup"><span data-stu-id="166e9-160">Prepare the configuration server</span></span>

1. <span data-ttu-id="166e9-161">온-프레미스 물리적 서버 또는 VMware VM에 Windows Server 2012 R2 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-161">Install Windows Server 2012 R2 or later on an on-premises physical server or a VMware VM.</span></span>

2. <span data-ttu-id="166e9-162">[필수 조건](#prerequisites)에 나열된 URL에 대한 액세스 권한이 컴퓨터에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-162">Make sure the machine has access to the URLs listed in [Prerequisites](#prerequisites).</span></span>

## <a name="prepare-for-mobility-service-installation"></a><span data-ttu-id="166e9-163">모바일 서비스 설치 준비</span><span class="sxs-lookup"><span data-stu-id="166e9-163">Prepare for Mobility service installation</span></span>

<span data-ttu-id="166e9-164">물리적 컴퓨터에 모바일 서비스를 푸시하려면 프로세스 서버에서 컴퓨터에 액세스하는 데 사용할 수 있는 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-164">If you want to push the Mobility service to a physical machine, you need an account that can be used by the process server to access the machines.</span></span> <span data-ttu-id="166e9-165">이 계정은 푸시 설치에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-165">The account is used only for the push installation.</span></span> <span data-ttu-id="166e9-166">도메인 또는 로컬 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-166">You can use a domain or local account:</span></span>

  - <span data-ttu-id="166e9-167">Windows에서는 도메인 계정을 사용하지 않는 경우 로컬 컴퓨터에서 원격 사용자 액세스 제어를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-167">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="166e9-168">이렇게 하려면 레지스트리의 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**에서 값이 1인 **LocalAccountTokenFilterPolicy** DWORD 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-168">To do this, in the registry under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span> <span data-ttu-id="166e9-169">명령줄 인터페이스에서 Windows의 레지스트리 항목을 추가하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-169">If you want to add the registry entry for Windows from a command-line interface, type:</span></span>

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - <span data-ttu-id="166e9-170">Linux에서 계정은 원본 Linux 서버의 루트 사용자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-170">For Linux, the account should be a root user on the source Linux server.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="166e9-171">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="166e9-171">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-the-protection-goal"></a><span data-ttu-id="166e9-172">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="166e9-172">Select the protection goal</span></span>

<span data-ttu-id="166e9-173">복제할 대상과 복제할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-173">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="166e9-174">**복구 서비스 자격 증명 모음** > **자격 증명 모음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-174">Click **Recovery Services vaults** > **vault**.</span></span>
2. <span data-ttu-id="166e9-175">**리소스** 메뉴에서 **Site Recovery** > **인프라 준비** > **보호 목표**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-175">On the **Resource** menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. <span data-ttu-id="166e9-177">**보호 목표**에서 **Azure에** > **가상화되지 않음/기타**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-177">In **Protection goal**, select **To Azure** > **Not virtualized / Other**.</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="166e9-178">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="166e9-178">Set up the source environment</span></span>

<span data-ttu-id="166e9-179">구성 서버를 설정하고 자격 증명 모음에 등록한 후 VM을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-179">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="166e9-180">**Site Recovery** > **인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-180">Click **Site Recovery** > **Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="166e9-181">구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-181">If you don’t have a configuration server, click **+Configuration Server**.</span></span>

    ![원본 설정](./media/site-recovery-vmware-to-azure/set-source1.png)

3. <span data-ttu-id="166e9-183">**서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-183">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="166e9-184">**Site Recovery 통합 설치** 프로그램 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-184">Download the **Site Recovery Unified Setup** installation file.</span></span>
5. <span data-ttu-id="166e9-185">**자격 증명 모음 등록 키**를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-185">Download the **vault registration key**.</span></span> <span data-ttu-id="166e9-186">통합 설치를 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-186">You need this key when you run Unified Setup.</span></span> <span data-ttu-id="166e9-187">이 키는 생성된 날로부터 5일간 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-187">The key is valid for five days after you generate it.</span></span>

   ![원본 설정](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a><span data-ttu-id="166e9-189">Site Recovery 통합 설치 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="166e9-189">Run Site Recovery Unified Setup</span></span>

<span data-ttu-id="166e9-190">시작하기 전에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-190">Before you start, do the following:</span></span>

- <span data-ttu-id="166e9-191">간단한 비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="166e9-191">Get a quick video overview.</span></span> <span data-ttu-id="166e9-192">(비디오에서는 VMware VM 복제 방법을 설명하지만 프로세스는 물리적 컴퓨터 복제와 비슷함)</span><span class="sxs-lookup"><span data-stu-id="166e9-192">(The video describes how to replicate VMware VMs, but the process is similar for physical machine replication.)</span></span>

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- <span data-ttu-id="166e9-193">구성 서버 컴퓨터에서 시스템 시계가 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)와 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-193">On the configuration server machine, make sure that the system clock is synchronized with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="166e9-194">15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-194">If it's 15 minutes in front or behind, Setup might fail.</span></span>
- <span data-ttu-id="166e9-195">구성 서버 컴퓨터에서 로컬 관리자로 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-195">Run Setup as a local administrator on the configuration server machine.</span></span>
- <span data-ttu-id="166e9-196">TLS 1.0이 컴퓨터에서 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-196">Make sure TLS 1.0 is enabled on the machine.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="166e9-197">[명령줄](http://aka.ms/installconfigsrv)을 통해 구성 서버를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-197">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="166e9-198">대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="166e9-198">Set up the target environment</span></span>

<span data-ttu-id="166e9-199">대상 환경을 설정하기 전에 [Azure Storage 계정 및 네트워크](#set-up-azure)가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-199">Before you set up the target environment, check to make sure that you have an [Azure storage account and network](#set-up-azure).</span></span>

1. <span data-ttu-id="166e9-200">**인프라 준비** > **대상**을 클릭하고 사용하려는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-200">Click **Prepare Infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="166e9-201">대상 배포 모델이 Resource Manager인지, 클래식인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-201">Specify whether your target deployment model is Resource Manager or classic.</span></span>
3. <span data-ttu-id="166e9-202">Site Recovery가 호환되는 Azure Storage 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-202">Site Recovery checks to make sure that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![대상](./media/site-recovery-vmware-to-azure/gs-target.png)

4. <span data-ttu-id="166e9-204">저장소 계정 또는 네트워크를 만들지 않았으면 **+저장소 계정** 또는 **+네트워크**를 클릭하여 Resource Manager 계정이나 인라인 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-204">If you haven't created a storage account or network, click **+Storage account** or **+Network** to create a Resource Manager account or network inline.</span></span>

## <a name="set-up-replication-settings"></a><span data-ttu-id="166e9-205">복제 설정 지정</span><span class="sxs-lookup"><span data-stu-id="166e9-205">Set up replication settings</span></span>

<span data-ttu-id="166e9-206">시작하기 전에 간단한 비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="166e9-206">Before you start, get a quick video overview.</span></span> <span data-ttu-id="166e9-207">(비디오에서는 VMware VM 복제 방법을 설명하지만 프로세스는 물리적 컴퓨터 복제와 비슷함)</span><span class="sxs-lookup"><span data-stu-id="166e9-207">(The video describes how to replicate VMware VMs, but the process is similar for physical machine replication.)</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="166e9-208">새 복제 정책을 만들려면 **Site Recovery 인프라** > **복제 정책** > **+복제 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-208">To create a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="166e9-209">**복제 정책 만들기**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-209">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="166e9-210">**RPO 임계값**에서 RPO 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-210">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="166e9-211">이 값은 데이터 복구 지점 생성 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-211">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="166e9-212">연속 복제가 이 제한을 초과하면 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-212">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="166e9-213">**복구 지점 보존**에서 각 복구 지점에 대해 지속될 보존 시간을 시간 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-213">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="166e9-214">복제된 VM은 하나의 시간대에서 임의의 시점으로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-214">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="166e9-215">프리미엄 저장소에 복제된 컴퓨터에 대해 최대 24시간의 보존이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-215">Up to 24 hours' retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="166e9-216">표준 저장소에 복제된 컴퓨터의 경우 최대 72시간 동안 보존하도록 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-216">Up to 72 hours' retention is supported for machines replicated to standard storage.</span></span>
5. <span data-ttu-id="166e9-217">**앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-217">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots are created.</span></span> <span data-ttu-id="166e9-218">**확인** 을 클릭하여 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-218">Click **OK** to create the policy.</span></span>

    ![복제 정책](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. <span data-ttu-id="166e9-220">새 정책을 만들면 새 정책이 자동으로 구성 서버에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-220">When you create a new policy, it's automatically associated with the configuration server.</span></span> <span data-ttu-id="166e9-221">기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-221">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="166e9-222">예를 들어 복제 정책이 **rep-policy**인 경우 장애 복구(failback) 정책은 **rep-policy-failback**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-222">For example, if the replication policy is **rep-policy**, then the failback policy is **rep-policy-failback**.</span></span> <span data-ttu-id="166e9-223">이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-223">This policy isn't used until you initiate a failback from Azure.</span></span>  


## <a name="plan-capacity"></a><span data-ttu-id="166e9-224">용량 계획</span><span class="sxs-lookup"><span data-stu-id="166e9-224">Plan capacity</span></span>

1. <span data-ttu-id="166e9-225">기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-225">Now that you have your basic infrastructure set up, you can think about capacity planning and figure out whether you need additional resources.</span></span> <span data-ttu-id="166e9-226">[자세히 알아보기](site-recovery-plan-capacity-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="166e9-226">[Learn more](site-recovery-plan-capacity-vmware.md).</span></span>
2. <span data-ttu-id="166e9-227">용량 계획을 마쳤으면 **용량 계획을 완료하셨습니까?**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-227">When you’re done with capacity planning, select **Yes** in **Have you completed capacity planning?**</span></span>

   ![용량 계획](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a><span data-ttu-id="166e9-229">복제용 VM 준비</span><span class="sxs-lookup"><span data-stu-id="166e9-229">Prepare VMs for replication</span></span>

<span data-ttu-id="166e9-230">복제하려는 모든 컴퓨터에는 모바일 서비스가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-230">All machines that you want to replicate must have the Mobility service installed.</span></span> <span data-ttu-id="166e9-231">다양한 방법으로 모바일 서비스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-231">You can install the Mobility service in a number of ways:</span></span>

- <span data-ttu-id="166e9-232">프로세스 서버에서 푸시 설치를 사용하여 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-232">Install the service with a push installation from the process server.</span></span> <span data-ttu-id="166e9-233">이 방법을 사용하려면 미리 컴퓨터를 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-233">You need to prepare machines in advance to use this method.</span></span>
- <span data-ttu-id="166e9-234">System Center Configuration Manager 또는 Azure Automation DSC(필요한 상태 구성)와 같은 배포 도구를 사용하여 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-234">Install the service by using deployment tools such as System Center Configuration Manager or Azure Automation Desired State Configuration.</span></span>
- <span data-ttu-id="166e9-235">서비스를 수동으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-235">Install the service manually.</span></span>

<span data-ttu-id="166e9-236">[자세히 알아보기](site-recovery-vmware-to-azure-install-mob-svc.md).</span><span class="sxs-lookup"><span data-stu-id="166e9-236">[Learn more](site-recovery-vmware-to-azure-install-mob-svc.md).</span></span>


## <a name="enable-replication"></a><span data-ttu-id="166e9-237">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="166e9-237">Enable replication</span></span>

<span data-ttu-id="166e9-238">시작하기 전에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-238">Before you start:</span></span>

- <span data-ttu-id="166e9-239">Azure 사용자 계정에 특정 [사용 권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있어야 Azure에 새 가상 컴퓨터를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-239">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>
- <span data-ttu-id="166e9-240">VM을 추가하거나 수정하는 경우 변경 사항이 적용되어 포털에 표시되는 데 15분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-240">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect and for them to appear in the portal.</span></span>
- <span data-ttu-id="166e9-241">**구성 서버** > **마지막 연락**에서 VM을 마지막으로 검색한 시간을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-241">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="166e9-242">예약된 검색을 기다리지 않고 VM을 추가하려면 구성 서버를 강조 표시하고(클릭하지 않음) **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-242">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>
- <span data-ttu-id="166e9-243">복제를 사용하도록 설정하는 경우 푸시 설치용으로 VM이 준비되면 프로세스 서버가 자동으로 모바일 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-243">If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="166e9-244">간단한 비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="166e9-244">Get a quick video overview.</span></span> <span data-ttu-id="166e9-245">(비디오에서는 VMware VM 복제 방법을 설명하지만 프로세스는 물리적 컴퓨터 복제와 비슷함)</span><span class="sxs-lookup"><span data-stu-id="166e9-245">(The video describes how to replicate VMware VMs, but the process is similar for physical machine replication.)</span></span>

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a><span data-ttu-id="166e9-246">복제에서 디스크 제외</span><span class="sxs-lookup"><span data-stu-id="166e9-246">Exclude disks from replication</span></span>

<span data-ttu-id="166e9-247">기본적으로 컴퓨터의 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-247">By default, all disks on a machine are replicated.</span></span> <span data-ttu-id="166e9-248">디스크를 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-248">You can exclude disks from replication.</span></span> <span data-ttu-id="166e9-249">예를 들어 임시 데이터 또는 컴퓨터나 응용 프로그램이 다시 시작할 때마다 새로 고쳐지는 데이터(예: pagefile.sys 또는 SQL Server tempdb)가 포함된 디스크를 복제하고 싶지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-249">For example, you might not want to replicate disks with temporary data or data that's refreshed each time a machine or application restarts (for example, pagefile.sys or SQL Server tempdb).</span></span>

### <a name="replicate-vms"></a><span data-ttu-id="166e9-250">VM 복제</span><span class="sxs-lookup"><span data-stu-id="166e9-250">Replicate VMs</span></span>

1. <span data-ttu-id="166e9-251">**응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-251">Click **Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="166e9-252">**원본**에서 **온-프레미스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-252">In **Source**, select **On-premises**.</span></span>
3. <span data-ttu-id="166e9-253">**원본 위치**에서 구성 서버 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-253">In **Source location**, select the configuration server name.</span></span>
4. <span data-ttu-id="166e9-254">**컴퓨터 형식**에서 **물리적 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-254">In **Machine type**, select **Physical Machines**.</span></span>
5. <span data-ttu-id="166e9-255">**프로세스 서버**에서 프로세스 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-255">In **Process server**, choose the process server.</span></span> <span data-ttu-id="166e9-256">추가 프로세스 서버를 만들지 않은 경우 이 서버가 구성 서버가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-256">If you haven't created any additional process servers, this server is the configuration server.</span></span> <span data-ttu-id="166e9-257">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-257">Then click **OK**.</span></span>

    ![복제 활성화](./media/site-recovery-physical-to-azure/chooseVM.png)

6. <span data-ttu-id="166e9-259">**대상**에서 장애 조치(failover) 후 Azure VM을 만들 **구독** 및 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-259">In **Target**, select the **Subscription** and the **Resource group** in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="166e9-260">장애 조치 VM에 대해 Azure(클래식 또는 Resource Manager)에서 사용할 배포 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-260">Choose the deployment model that you want to use in Azure (classic or Resource Manager) for the failed-over VMs.</span></span>

7. <span data-ttu-id="166e9-261">데이터 복제에 사용할 Azure Storage 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-261">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="166e9-262">이미 설정한 계정을 사용하지 않으려면 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-262">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="166e9-263">장애 조치(Failover) 후 Azure VM이 연결될 **Azure 네트워크** 및 **서브넷**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-263">Select the **Azure network** and **Subnet** to which Azure VMs connect after failover.</span></span> <span data-ttu-id="166e9-264">컴퓨터마다 Azure 네트워크를 선택하려면 **나중에 구성** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-264">Select **Configure now for selected machines** to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="166e9-265">네트워크가 없는 경우 **만들어야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-265">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="166e9-266">기존 네트워크를 사용하지 않으려면 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-266">If you don't want to use an existing network, you can create one.</span></span>

    ![복제 활성화](./media/site-recovery-physical-to-azure/targetsettings.png)

9. <span data-ttu-id="166e9-268">**물리적 컴퓨터**에서 **+물리적 컴퓨터**를 클릭하고 **이름** 및 **IP 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-268">In **Physical machines**, click **+Physical machine** and enter the **Name** and **IP address**.</span></span> <span data-ttu-id="166e9-269">복제하려는 컴퓨터의 운영 체제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-269">Choose the operating system of the machine you want to replicate.</span></span> <span data-ttu-id="166e9-270">컴퓨터를 검색하여 목록에 표시할 때까지 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-270">It takes a few minutes until machines are discovered and shown in the list.</span></span>

    ![복제 활성화](./media/site-recovery-physical-to-azure/machineselect.png)

10. <span data-ttu-id="166e9-272">**속성** > **속성 구성**에서 프로세스 서버가 자동으로 컴퓨터에 모바일 서비스를 설치하는 데 사용할 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-272">In **Properties** > **Configure properties**, select the account to be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="166e9-273">기본적으로 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-273">By default, all disks are replicated.</span></span> <span data-ttu-id="166e9-274">**모든 디스크**를 클릭하고 복제하지 않으려는 디스크를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-274">Click **All Disks**, and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="166e9-275">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-275">Then click **OK**.</span></span> <span data-ttu-id="166e9-276">나중에 추가 VM 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-276">You can set additional VM properties later.</span></span>

    ![복제 활성화](./media/site-recovery-physical-to-azure/configprop.png)

12. <span data-ttu-id="166e9-278">**복제 설정** > **복제 설정 구성**에서 올바른 복제 정책이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-278">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="166e9-279">정책을 수정하면 복제 중인 컴퓨터와 새 컴퓨터에 변경 내용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-279">If you modify a policy, changes are applied to the replicating machine and to new machines.</span></span>
13. <span data-ttu-id="166e9-280">컴퓨터를 복제 그룹으로 수집하려는 경우 **다중 VM 일관성** 을 사용하도록 설정하고 그룹에 대한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-280">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="166e9-281">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-281">Then click **OK**.</span></span> <span data-ttu-id="166e9-282">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="166e9-282">Note that:</span></span>

    <span data-ttu-id="166e9-283">a.</span><span class="sxs-lookup"><span data-stu-id="166e9-283">a.</span></span> <span data-ttu-id="166e9-284">복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-284">Machines in replication groups replicate together and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>

    <span data-ttu-id="166e9-285">b.</span><span class="sxs-lookup"><span data-stu-id="166e9-285">b.</span></span> <span data-ttu-id="166e9-286">워크로드를 미러링하도록 VM 및 물리적 서버를 함께 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-286">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="166e9-287">다중 VM 일관성을 사용하면 워크로드 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-287">Enabling multi-VM consistency can affect workload performance.</span></span> <span data-ttu-id="166e9-288">컴퓨터가 동일한 워크로드를 실행하고 일관성이 필요한 경우에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-288">It should be used only if machines are running the same workload and you need consistency.</span></span>

    ![복제 활성화](./media/site-recovery-physical-to-azure/policy.png)

14. <span data-ttu-id="166e9-290">**복제 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-290">Click **Enable Replication**.</span></span> <span data-ttu-id="166e9-291">**설정** > **작업** > **Site Recovery 작업**에서 **보호 사용** 작업의 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-291">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="166e9-292">**보호 완료** 작업이 실행된 후에는 컴퓨터가 장애 조치(failover)를 수행할 준비가 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-292">After the **Finalize Protection** job runs, the machine is ready for failover.</span></span>

<span data-ttu-id="166e9-293">복제를 활성화한 후 푸시 설치를 설정하는 경우 모바일 서비스가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-293">After you enable replication, the Mobility service is installed if you set up push installation.</span></span> <span data-ttu-id="166e9-294">컴퓨터에서 모바일 서비스의 푸시 설치를 수행한 후 보호 작업이 시작되고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-294">After the Mobility service is push installed on a machine, a protection job starts and fails.</span></span> <span data-ttu-id="166e9-295">실패 후 각 컴퓨터를 수동으로 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-295">After the failure, you need to manually restart each machine.</span></span> <span data-ttu-id="166e9-296">그러면, 보호 작업이 다시 시작되고 초기 복제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-296">Then the protection job begins again, and initial replication occurs.</span></span>


### <a name="view-and-manage-azure-vm-properties"></a><span data-ttu-id="166e9-297">Azure VM 속성 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="166e9-297">View and manage Azure VM properties</span></span>

<span data-ttu-id="166e9-298">VM 속성을 확인하고 필요한 사항을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-298">We recommend that you verify the VM properties and make any changes you need.</span></span>

1. <span data-ttu-id="166e9-299">**복제된 항목**을 클릭하고 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-299">Click **Replicated items**, and select the machine.</span></span> <span data-ttu-id="166e9-300">**Essentials** 블레이드는 컴퓨터 설정 및 상태에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-300">The **Essentials** blade shows information about machines settings and status.</span></span>
2. <span data-ttu-id="166e9-301">**속성**에서 해당 VM에 대한 복제 및 장애 조치(failover) 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-301">In **Properties**, you can view replication and failover information for the VM.</span></span>
3. <span data-ttu-id="166e9-302">**계산 및 네트워크** > **계산 속성**에서 Azure VM 이름 및 대상 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-302">In **Compute and Network** > **Compute properties**, you can specify the Azure VM name and target size.</span></span> <span data-ttu-id="166e9-303">필요한 경우 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 을 준수하도록 이름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-303">Modify the name to comply with [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) if you need to.</span></span>
4. <span data-ttu-id="166e9-304">대상 네트워크, 서브넷 및 Azure VM에 할당될 IP 주소에 대한 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-304">Modify settings for the target network, subnet, and IP address that are assigned to the Azure VM:</span></span>

    <span data-ttu-id="166e9-305">a.</span><span class="sxs-lookup"><span data-stu-id="166e9-305">a.</span></span> <span data-ttu-id="166e9-306">대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-306">You can set the target IP address.</span></span>

    <span data-ttu-id="166e9-307">b.</span><span class="sxs-lookup"><span data-stu-id="166e9-307">b.</span></span>  <span data-ttu-id="166e9-308">주소를 입력하지 않으면 장애 조치(Failover)된 컴퓨터가 DHCP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-308">If you don't provide an address, the failed-over machine uses DHCP.</span></span>

    <span data-ttu-id="166e9-309">c.</span><span class="sxs-lookup"><span data-stu-id="166e9-309">c.</span></span> <span data-ttu-id="166e9-310">장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-310">If you set an address that isn't available at failover, failover doesn't work.</span></span>

    <span data-ttu-id="166e9-311">d.</span><span class="sxs-lookup"><span data-stu-id="166e9-311">d.</span></span> <span data-ttu-id="166e9-312">주소를 테스트 장애 조치(Failover) 네트워크에서 사용할 수 있는 경우 테스트 장애 조치(Failover)에 동일한 대상 IP 주소를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-312">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

    <span data-ttu-id="166e9-313">e.</span><span class="sxs-lookup"><span data-stu-id="166e9-313">e.</span></span> <span data-ttu-id="166e9-314">네트워크 어댑터 수는 대상 가상 컴퓨터에 대해 지정하는 크기에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-314">The number of network adapters is dictated by the size you specify for the target virtual machine:</span></span>

     - <span data-ttu-id="166e9-315">원본 컴퓨터의 네트워크 어댑터 수가 대상 컴퓨터 크기에 허용되는 어댑터 수보다 작거나 같은 경우, 대상의 어댑터 수는 소스와 동일하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-315">If the number of network adapters on the source machine is the same as, or less than, the number of adapters allowed for the target machine size, then the target has the same number of adapters as the source.</span></span>
     - <span data-ttu-id="166e9-316">원본 가상 컴퓨터의 어댑터의 수가 대상 크기에 허용된 수를 초과하면 대상 크기 최대치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-316">If the number of adapters for the source virtual machine exceeds the number allowed for the target size, then the target size maximum is used.</span></span>
     - <span data-ttu-id="166e9-317">예를 들어 원본 컴퓨터에 두 네트워크 어댑터가 있고 대상 컴퓨터 크기가 4를 지원하는 경우, 대상 컴퓨터에는 2개의 어댑터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-317">For example, if a source machine has two network adapters and the target machine size supports four, the target machine has two adapters.</span></span> <span data-ttu-id="166e9-318">원본 컴퓨터에 두 어댑터가 있지만 지원되는 대상 크기에서 하나만 지원하는 경우 대상 컴퓨터에는 하나의 어댑터만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-318">If the source machine has two adapters but the supported target size supports only one, then the target machine has only one adapter.</span></span>     
   - <span data-ttu-id="166e9-319">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 모두 동일한 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-319">If the virtual machine has multiple network adapters, they all connect to the same network.</span></span>
   - <span data-ttu-id="166e9-320">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 목록에서 첫 번째 어댑터가 Azure VM에서 *기본* 네트워크 어댑터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-320">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the *Default* network adapter in the Azure VM.</span></span>
5. <span data-ttu-id="166e9-321">**디스크**에서 복제될 VM 운영 체제 및 데이터 디스크를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-321">In **Disks**, you can see the VM operating system and the data disks that are replicated.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="166e9-322">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="166e9-322">Run a test failover</span></span>

<span data-ttu-id="166e9-323">모든 항목을 설정한 후 모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-323">After you've set up everything, run a test failover to make sure everything's working as expected.</span></span> <span data-ttu-id="166e9-324">시작하기 전에 간단한 동영상 개요를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-324">Watch a quick video overview before you start.</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. <span data-ttu-id="166e9-325">단일 컴퓨터를 장애 조치(failover)하려면 **설정** > **복제된 항목**에서 **테스트 장애 조치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-325">To fail over a single machine, in **Settings** > **Replicated Items**, click **Test failover**.</span></span>

    ![테스트 장애 조치(Failover)](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. <span data-ttu-id="166e9-327">복구 계획을 장애 조치(Failover)하려면 **설정** > **복구 계획**에서 계획을 마우스 오른쪽 버튼으로 클릭하고 **테스트 장애 조치(Failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-327">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="166e9-328">복구 계획을 만들려면 [다음 지침을 따릅니다](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="166e9-328">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  
3. <span data-ttu-id="166e9-329">**테스트 장애 조치**에서 장애 조치가 발생한 후에 Azure VM이 연결될 Azure 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-329">In **Test Failover**, select the Azure network to which Azure VMs are connected after failover occurs.</span></span>
4. <span data-ttu-id="166e9-330">**확인** 을 클릭하여 장애 조치(Failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-330">Click **OK** to begin the failover.</span></span> <span data-ttu-id="166e9-331">VM을 클릭하여 해당 속성을 열거나 자격 증명 모음 이름 > **설정** > **작업** > **Site Recovery 작업**의 **테스트 장애 조치(failover)**를 클릭하여 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-331">You can track progress by clicking the VM to open its properties or by clicking the **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="166e9-332">장애 조치가 완료되면 Azure Portal > **가상 컴퓨터**에서 복제본 Azure 컴퓨터가 표시되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-332">After the failover finishes, you should also be able to see the replica Azure machine appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="166e9-333">VM의 크기가 적당하고, 올바른 네트워크에 연결되었고, 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-333">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="166e9-334">[장애 조치(failover) 후 연결을 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)하는 경우 Azure VM에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-334">If you [prepared for connections after failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), you should be able to connect to the Azure VM.</span></span>
7. <span data-ttu-id="166e9-335">작업이 완료되면 복구 계획에서 **테스트 장애 조치 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-335">After you're done, click **Cleanup test failover** on the recovery plan.</span></span> <span data-ttu-id="166e9-336">**참고**에서 테스트 장애 조치와 관련된 모든 관측 내용을 기록하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-336">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="166e9-337">이 단계에서는 테스트 장애 조치 중에 만든 가상 컴퓨터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-337">This step deletes the virtual machines that were created during test failover.</span></span>

<span data-ttu-id="166e9-338">자세한 내용은 [Azure에 테스트 장애 조치](site-recovery-test-failover-to-azure.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="166e9-338">For more information, see the [Test failover to Azure](site-recovery-test-failover-to-azure.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="166e9-339">다음 단계</span><span class="sxs-lookup"><span data-stu-id="166e9-339">Next steps</span></span>

<span data-ttu-id="166e9-340">복제를 작동 및 실행한 후 가동 중단이 발생하면 Azure에 장애 조치되고 복제된 데이터에서 Azure VM이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-340">After you get replication up and running, when an outage occurs you fail over to Azure, and Azure VMs are created from the replicated data.</span></span> <span data-ttu-id="166e9-341">그러면 기본 위치가 정상 작업 상태로 돌아와 다시 기본 위치로 돌아갈 때까지 Azure의 워크로드와 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-341">You can then access workloads and apps in Azure, until you fail back to your primary location when it returns to normal operations.</span></span>

- <span data-ttu-id="166e9-342">여러 장애 조치(failover) 유형 및 장애 조치(failover) 실행 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="166e9-342">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="166e9-343">컴퓨터를 복제하고 장애 복구하는 대신 마이그레이션하는 경우 [여기를 참조하세요](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span><span class="sxs-lookup"><span data-stu-id="166e9-343">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="166e9-344">물리적 컴퓨터를 복제하는 경우 VMware 환경으로만 장애 복구(failback)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166e9-344">When replicating physical machines, you can only failback to a VMware environment.</span></span> <span data-ttu-id="166e9-345">[장애 복구(failback)에 대해 자세히 읽어보세요](site-recovery-failback-azure-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="166e9-345">[Read about failback](site-recovery-failback-azure-to-vmware.md).</span></span>

## <a name="third-party-software-notices-and-information"></a><span data-ttu-id="166e9-346">타사 소프트웨어 통지 및 정보</span><span class="sxs-lookup"><span data-stu-id="166e9-346">Third-party software notices and information</span></span>
<span data-ttu-id="166e9-347">Do Not Translate or Localize</span><span class="sxs-lookup"><span data-stu-id="166e9-347">Do Not Translate or Localize</span></span>

<span data-ttu-id="166e9-348">The software and firmware running in the Microsoft product or service is based on or incorporates material from the projects listed below (collectively, “Third Party Code”).</span><span class="sxs-lookup"><span data-stu-id="166e9-348">The software and firmware running in the Microsoft product or service is based on or incorporates material from the projects listed below (collectively, “Third-Party Code”).</span></span> <span data-ttu-id="166e9-349">Microsoft is not the original author of the Third-Party Code.</span><span class="sxs-lookup"><span data-stu-id="166e9-349">Microsoft is not the original author of the Third-Party Code.</span></span> <span data-ttu-id="166e9-350">The original copyright notice and license, under which Microsoft received such Third-Party Code, are set forth below.</span><span class="sxs-lookup"><span data-stu-id="166e9-350">The original copyright notice and license, under which Microsoft received such Third-Party Code, are set forth below.</span></span>

<span data-ttu-id="166e9-351">The information in Section A is regarding Third-Party Code components from the projects listed below.</span><span class="sxs-lookup"><span data-stu-id="166e9-351">The information in Section A is regarding Third-Party Code components from the projects listed below.</span></span> <span data-ttu-id="166e9-352">Such licenses and information are provided for informational purposes only.</span><span class="sxs-lookup"><span data-stu-id="166e9-352">Such licenses and information are provided for informational purposes only.</span></span> <span data-ttu-id="166e9-353">This Third-Party Code is being relicensed to you by Microsoft under Microsoft's software licensing terms for the Microsoft product or service.</span><span class="sxs-lookup"><span data-stu-id="166e9-353">This Third-Party Code is being relicensed to you by Microsoft under Microsoft's software licensing terms for the Microsoft product or service.</span></span>  

<span data-ttu-id="166e9-354">The information in Section B is regarding Third Party Code components that are being made available to you by Microsoft under the original licensing terms.</span><span class="sxs-lookup"><span data-stu-id="166e9-354">The information in Section B is regarding Third Party Code components that are being made available to you by Microsoft under the original licensing terms.</span></span>

<span data-ttu-id="166e9-355">The complete file can be found on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428).</span><span class="sxs-lookup"><span data-stu-id="166e9-355">The complete file can be found on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428).</span></span> <span data-ttu-id="166e9-356">Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.</span><span class="sxs-lookup"><span data-stu-id="166e9-356">Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.</span></span>
