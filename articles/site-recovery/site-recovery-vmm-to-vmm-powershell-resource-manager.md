---
title: "PowerShell (Azure 리소스 관리자)과 함께 VMM tooa 보조 사이트의 Hyper-v Vm aaaReplicate | Microsoft Docs"
description: "Toodeploy Azure Site Recovery tooorchestrate 복제, 장애 조치 및 복구 VMM에서 Hyper-v Vm의 클라우드 tooa PowerShell (리소스 관리자)을 사용 하는 보조 VMM 사이트를 어떻게 설명"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="ed5a6-103">VMM 클라우드 tooa 보조 VMM 사이트에서 PowerShell (리소스 관리자)를 사용 하 여 Hyper-v 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="ed5a6-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed5a6-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ed5a6-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="ed5a6-105">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="ed5a6-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="ed5a6-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ed5a6-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="ed5a6-107">TooAzure 사이트 복구를 시작!</span><span class="sxs-lookup"><span data-stu-id="ed5a6-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="ed5a6-108">Tooreplicate 온-프레미스 System Center Virtual Machine Manager (VMM) 클라우드 tooa 보조 사이트의 관리 되는 Hyper-v 가상 컴퓨터를 원하는 경우이 문서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="ed5a6-109">이 문서에서는 어떻게 toouse PowerShell tooautomate 일반적인 작업 tooperform 때 필요한 보조 사이트에서 System Center VMM 클라우드에 tooSystem 센터 VMM 클라우드의 Azure Site Recovery tooreplicate Hyper-v 가상 컴퓨터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="ed5a6-110">hello 문서에서는 hello 시나리오에 대 한 필수 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="ed5a6-111">어떻게 tooset 복구 서비스 자격 증명 모음을</span><span class="sxs-lookup"><span data-stu-id="ed5a6-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="ed5a6-112">Hello 원본 VMM 서버와 대상 VMM 서버 hello에 hello Azure Site Recovery Provider를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="ed5a6-113">VMM 서버 hello hello 자격 증명 모음 등록</span><span class="sxs-lookup"><span data-stu-id="ed5a6-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="ed5a6-114">VMM 클라우드 hello에 대 한 복제 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="ed5a6-115">hello 복제 설정을 hello 정책에 적용 된 tooall 보호 된 가상 컴퓨터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="ed5a6-116">Hello 가상 컴퓨터에 대 한 보호를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="ed5a6-117">개별적으로 또는 복구의 일부로 Vm의 테스트 hello 장애 조치 계획 toomake 모든 기능이 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="ed5a6-118">개별적으로 또는 모든 기능이 예상 대로 작동 하는지 확인 하는 복구 계획 toomake의 일환으로 계획 된 또는 Vm의 경우 계획 되지 않은 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="ed5a6-119">이 시나리오를 설정 하는 문제를 실행 하는 경우 hello에 질문을 게시할 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="ed5a6-120">Azure에는 리소스를 만들고 작업하기 위한 두 가지 [배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 인 Azure Resource Manager 모델과 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ed5a6-121">Azure는 두 개의 포털 – hello 클래식 배포 모델을 지 원하는 Azure 클래식 포털 hello 및 두 가지 경우 모두 지원 하 여 Azure 포털 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="ed5a6-122">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="ed5a6-123">온-프레미스 필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed5a6-123">On-premises prerequisites</span></span>
<span data-ttu-id="ed5a6-124">필요한 사항 hello에서 기본 및 보조 온-프레미스 사이트 toodeploy이이 시나리오:</span><span class="sxs-lookup"><span data-stu-id="ed5a6-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="ed5a6-125">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="ed5a6-125">**Prerequisites**</span></span> | <span data-ttu-id="ed5a6-126">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ed5a6-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="ed5a6-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="ed5a6-127">**VMM**</span></span> |<span data-ttu-id="ed5a6-128">Hello 기본 사이트에서 VMM 서버와 보조 사이트 hello에에서 VMM 서버를 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="ed5a6-129">[단일 VMM 서버의 클라우드 간에 복제](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)에 문의 사항을 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="ed5a6-130">toodo이 해야 hello VMM 서버에 구성 된 둘 이상의 클라우드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="ed5a6-131">VMM 서버를 하나 이상 실행 해야 hello 최신 업데이트로 System Center 2012 SP1.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="ed5a6-132">각 VMM 서버 하나에 있어야 하거나 추가 클라우드를 구성 하 고 모든 클라우드 hello Hyper-v 용량 프로필이 설정 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="ed5a6-133">클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="ed5a6-134">VMM 클라우드를 설정 하는 방법에 대 한 자세한 정보 [구성 hello VMM 클라우드 패브릭](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), 및 [연습: System Center 2012 SP1 vmm 사설 클라우드를 만들어](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="ed5a6-135">VMM 서버는 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="ed5a6-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="ed5a6-136">**Hyper-V**</span></span> |<span data-ttu-id="ed5a6-137">Hyper-v 서버가 이상 실행 해야 hello Hyper-v 역할과 Windows Server 2012 및 최신 업데이트가 설치 되어 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="ed5a6-138">Hyper-V 서버에 VM이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="ed5a6-139">Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 호스트 그룹에 들어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="ed5a6-140">Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="ed5a6-141">Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="ed5a6-142">Tooconfigure hello 클러스터 브로커를 수동으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="ed5a6-143">[자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed5a6-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="ed5a6-144">**공급자**</span><span class="sxs-lookup"><span data-stu-id="ed5a6-144">**Provider**</span></span> |<span data-ttu-id="ed5a6-145">사이트 복구 배포 하는 동안 VMM 서버에 hello Azure Site Recovery Provider를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="ed5a6-146">hello 공급자 HTTPS 443 tooorchestrate 복제 통해 Site Recovery와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="ed5a6-147">데이터 복제 hello LAN 통해 hello 기본 및 보조 Hyper-v 서버 또는 VPN 연결 간에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="ed5a6-148">hello hello VMM 서버에서 실행 중인 공급자 필요한 액세스 toothese Url: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="ed5a6-149">또한 VMM 서버 toohello hello에서에서 방화벽 통신을 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) hello HTTPS (443) 프로토콜을 허용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="ed5a6-150">네트워크 매핑 필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed5a6-150">Network mapping prerequisites</span></span>
<span data-ttu-id="ed5a6-151">네트워크 매핑은 hello 기본 및 보조 VMM 서버를 VMM VM 네트워크 간에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="ed5a6-152">장애 조치(Failover) 후 보조 Hyper-V 호스트에 복제본 VM을 최적으로 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="ed5a6-153">복제본 Vm tooappropriate VM 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="ed5a6-154">네트워크를 구성 하지 않으면 매핑 복제본 Vm 수 없습니다 연결된 tooany 네트워크 장애 조치 후.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="ed5a6-155">네트워크를 tooset 하려는 경우 사이트 복구 시 매핑 배포 여기는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="ed5a6-156">Hello 원본 Hyper-v 호스트 서버에 있는 Vm 연결된 tooa VMM VM 네트워크 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="ed5a6-157">해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="ed5a6-158">복구에 사용할 보조 클라우드를 hello 구성 해당 VM 네트워크에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="ed5a6-159">해당 VM 네트워크에 연결 된 tooa hello 보조 클라우드와 연결 된 논리 네트워크 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="ed5a6-160">Hello 문서 아래에서 VMM 네트워크를 구성 하는 방법에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ed5a6-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="ed5a6-161">어떻게 tooconfigure VMM에서에서 논리 네트워크</span><span class="sxs-lookup"><span data-stu-id="ed5a6-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="ed5a6-162">어떻게 tooconfigure VM 네트워크 및 VMM에서 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="ed5a6-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="ed5a6-163">[알아보세요](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) .</span><span class="sxs-lookup"><span data-stu-id="ed5a6-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="ed5a6-164">PowerShell 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ed5a6-164">PowerShell prerequisites</span></span>
<span data-ttu-id="ed5a6-165">Azure PowerShell 준비 toogo 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="ed5a6-166">PowerShell을 이미 사용 중인 tooupgrade tooversion 0.8.10 맞춰야 이상.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="ed5a6-167">PowerShell 설정에 대 한 정보를 참조 hello [tooinstall 안내 하 고 Azure powershell](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="ed5a6-168">Hello hello 서비스에 대 한 사용 가능한 cmdlet의 모든 볼 수를 설정 하 고 PowerShell을 구성한 후 [여기](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="ed5a6-169">매개 변수 값, 입력 및 출력이 처리 되는 방법과 일반적으로 Azure PowerShell 같은 hello cmdlet을 사용 하는 데 도움이 되는 팁에 대 한 toolearn 참조 hello [tooget Azure cmdlet 시작 안내](/powershell/azure/get-started-azureps)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="ed5a6-170">1 단계: hello 구독 설정</span><span class="sxs-lookup"><span data-stu-id="ed5a6-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="ed5a6-171">Azure powershell, 로그인 tooyour Azure 계정에서에서: hello 다음 cmdlet을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ed5a6-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="ed5a6-172">구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="ed5a6-173">이 또한은 나열 hello subscriptionIDs 각 hello 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="ed5a6-174">Hello 구독의 toocreate hello 복구 서비스 자격 증명 모음 원하는 hello subscriptionID 다운 note</span><span class="sxs-lookup"><span data-stu-id="ed5a6-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="ed5a6-175">hello에 복구 서비스 자격 증명 모음이 toobe hello 구독 ID를 언급 하 여 만든 hello 구독 설정</span><span class="sxs-lookup"><span data-stu-id="ed5a6-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="ed5a6-176">2단계: 복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="ed5a6-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="ed5a6-177">또한 Azure Resource Manager 리소스 그룹이 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="ed5a6-178">새 복구 서비스 자격 증명 모음을 만들고 (됩니다 나중에 사용) 변수에 ASR 자격 증명 모음 개체를 만든 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="ed5a6-179">Hello AzureRMRecoveryServicesVault Get cmdlet을 사용 하 여 hello ASR 자격 증명 모음 개체 post 만들기를 검색할 수도 있습니다.-</span><span class="sxs-lookup"><span data-stu-id="ed5a6-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="ed5a6-180">3 단계: hello 복구 서비스 자격 증명 모음 컨텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="ed5a6-181">자격 증명 모음은 이미 만든 경우 명령 tooget hello 자격 증명 모음 아래 hello을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="ed5a6-182">아래의 명령 hello를 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="ed5a6-183">4 단계: hello Azure Site Recovery Provider 설치</span><span class="sxs-lookup"><span data-stu-id="ed5a6-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="ed5a6-184">Hello VMM 컴퓨터에서 hello 다음 명령을 실행 하 여 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="ed5a6-185">다운로드 한 hello 공급자를 사용 하 여 hello 다음 명령을 실행 하 여 hello 파일 추출</span><span class="sxs-lookup"><span data-stu-id="ed5a6-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="ed5a6-186">다음 명령을 hello를 사용 하 여 hello 공급자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-186">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="ed5a6-187">Hello 설치 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="ed5a6-188">Hello 서버 hello 다음 명령을 사용 하 여 hello 자격 증명 모음에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="ed5a6-189">5단계: 복제 정책 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="ed5a6-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="ed5a6-190">Hyper-v 2012 R2 복제 정책을 hello 다음 명령을 실행 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="ed5a6-191">VMM 클라우드 hello에 다른 버전의 Windows Server (했 듯이 hello Hyper-v 필수 구성 요소)를 실행 하는 Hyper-v 호스트 포함 될 수 있지만 hello 복제 정책 특정 OS 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="ed5a6-192">운영 체제 버전마다 다른 호스트가 실행되고 있는 경우 각 형식의 OS 버전에 대해 별도의 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="ed5a6-193">예를 들어 Windows Server 2012에서 5개의 호스트가 실행되고 있고 Windows Server 2012 R2에서 3개의 호스트가 실행되고 있는 경우 각 운영 체제 버전 형식에 대해 하나씩 2개의 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="ed5a6-194">Hello 다음 명령을 실행 하 여 hello 주 보호 컨테이너 (기본 VMM 클라우드) 및 복구 보호 컨테이너 (복구 VMM 클라우드)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="ed5a6-195">사용 하 여 1 단계에서 만든 hello 정책을 검색 하는 hello 정책의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="ed5a6-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="ed5a6-196">Hello 복제 정책을 사용 하 여 hello 보호 컨테이너 (VMM 클라우드)의 hello 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="ed5a6-197">Hello 정책 연결 작업 toocomplete 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="ed5a6-198">다음 PowerShell 코드 조각을 hello를 사용 하 여 hello 작업이 완료 된 경우를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="ed5a6-199">Hello 작업 처리를 완료 한 후에 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="ed5a6-200">hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="ed5a6-201">6단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="ed5a6-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="ed5a6-202">첫 번째 명령은 hello hello 현재 Azure Site Recovery 자격 증명 모음에 대 한 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="ed5a6-203">hello 명령은 hello Microsoft Azure Site Recovery 서버 hello $Servers 배열 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="ed5a6-204">아래 명령 hello hello 원본 VMM 서버와 대상 VMM 서버 hello에 대 한 hello 사이트 복구 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="ed5a6-205">첫 번째 또는 두 번째에 한 hello 서버 배열 hello hello 원본 VMM 서버를 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="ed5a6-206">Hello hello VMM 서버 이름을 확인 하 고 hello 네트워크를 적절 하 게 가져올</span><span class="sxs-lookup"><span data-stu-id="ed5a6-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="ed5a6-207">hello 최종 cmdlet은 기본 네트워크 hello와 hello 복구 네트워크 간의 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="ed5a6-208">hello cmdlet $RecoveryNetworks의 hello 첫 번째 요소로 $PrimaryNetworks 및 hello 복구 네트워크의 hello 첫 번째 요소로 hello 주 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="ed5a6-209">7단계: 저장소 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="ed5a6-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="ed5a6-210">아래의 명령 hello hello 목록이 $storageclassifications 변수로 저장소 분류를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="ed5a6-211">명령 아래 hello $SourceClassificaion 변수로 hello 소스 분류 및 대상 분류 $TargetClassification 변수로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="ed5a6-212">hello 원본 및 대상 분류 hello 배열에 있는 모든 요소를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="ed5a6-213">Toohello 출력의 hello $storageclassifications 배열에 있는 원본 및 대상 분류의 명령 toofigure hello 인덱스 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="ed5a6-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="ed5a6-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="ed5a6-215">hello cmdlet 아래에 hello 소스 분류 및 hello 대상 분류 간에 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="ed5a6-216">8단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="ed5a6-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="ed5a6-217">Hello 서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="ed5a6-218">hello 명령 tooget hello 보호 컨테이너를 다음 실행 tooenable 보호:</span><span class="sxs-lookup"><span data-stu-id="ed5a6-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="ed5a6-219">Hello 다음 명령을 실행 하 여 hello 보호 엔터티를 (VM)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="ed5a6-220">Hello 다음 명령을 실행 하 여 hello VM에 대 한 복제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="ed5a6-221">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="ed5a6-221">Test your deployment</span></span>
<span data-ttu-id="ed5a6-222">tootest 단일 가상 컴퓨터에 대 한 테스트 장애 조치를 실행 하거나 hello에 대 한 테스트 장애 조치를 실행 하 고 여러 가상 컴퓨터의 구성 된 복구 계획을 만들 수 있습니다 배포를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="ed5a6-223">테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="ed5a6-224">Azure 포털에서 응용 프로그램에 대한 복구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="ed5a6-225">hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="ed5a6-226">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="ed5a6-226">Run a test failover</span></span>
1. <span data-ttu-id="ed5a6-227">Hello cmdlet tooget hello VM 네트워크 toowhich Vm을 tootest 장애 조치 하려면 아래를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="ed5a6-228">Hello 다음을 수행 하 여 VM의 테스트 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="ed5a6-229">Hello 다음을 수행 하 여 복구 계획의 테스트 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="ed5a6-230">계획된 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="ed5a6-230">Run a planned failover</span></span>
1. <span data-ttu-id="ed5a6-231">Hello 다음을 수행 하 여 VM의 계획된 된 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="ed5a6-232">Hello 다음을 수행 하 여 복구 계획의 계획된 된 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="ed5a6-233">계획되지 않은 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="ed5a6-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="ed5a6-234">Hello 다음을 수행 하 여 VM의 경우 계획 되지 않은 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="ed5a6-235">2. hello 다음을 수행 하 여 복구 계획의 계획 되지 않은 경우 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="ed5a6-236"><a name=monitor></a> 작업 모니터</span><span class="sxs-lookup"><span data-stu-id="ed5a6-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="ed5a6-237">다음 명령을 toomonitor hello 활동 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="ed5a6-238">Note toowait 사이 처리 toofinish hello에 대 한 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5a6-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="ed5a6-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed5a6-239">Next steps</span></span>
<span data-ttu-id="ed5a6-240">[자세히 알아보세요](/powershell/module/azurerm.recoveryservices.backup/#recovery) .</span><span class="sxs-lookup"><span data-stu-id="ed5a6-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
