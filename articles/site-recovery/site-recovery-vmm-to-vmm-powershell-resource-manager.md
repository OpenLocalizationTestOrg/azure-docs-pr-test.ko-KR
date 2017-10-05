---
title: "PowerShell을 사용하여 보조 사이트에 VMM의 Hyper-V VM 복제(Azure Resource Manager) | Microsoft Docs"
description: "Azure Site Recovery를 배포하고 PowerShell을 사용하여 VMM 클라우드의 Hyper-V VM을 보조 VMM 사이트에 복제, 장애 조치(Failover) 및 복구하는 작업을 어떻게 조정해야 하는지 설명합니다(Resource Manager)."
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
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="f2c18-103">PowerShell을 사용하여 보조 VMM 사이트에 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f2c18-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2c18-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f2c18-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="f2c18-105">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="f2c18-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="f2c18-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2c18-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="f2c18-107">Azure Site Recovery에 오신 것을 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="f2c18-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="f2c18-108">System Center VMM(Virtual Machine Manager) 클라우드에서 관리되는 온-프레미스 Hyper-V 가상 컴퓨터를 보조 사이트에 복제하려는 경우 이 문서를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="f2c18-109">이 문서에서는 System Center VMM 클라우드의 Hyper-V 가상 컴퓨터를 보조 사이트의 System Center VMM 클라우드로 복제하도록 Azure Site Recovery를 설정할 때 수행해야 하는 일반적인 작업을 PowerShell을 사용하여 자동화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="f2c18-110">이 문서는 시나리오의 필수 조건을 포함하고 있으며, 다음 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="f2c18-111">복구 서비스 자격 증명 모음을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2c18-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="f2c18-112">원본 VMM 서버 및 대상 VMM 서버에 Azure Site Recovery 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="f2c18-113">VMM 서버를 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="f2c18-114">VMM 클라우드에 대한 복제 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="f2c18-115">정책의 복제 설정이 보호된 모든 가상 컴퓨터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="f2c18-116">가상 컴퓨터에 대한 보호를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="f2c18-117">VM의 장애 조치를 개별적으로 또는 복구 계획의 일부로 테스트하여 모든 것이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="f2c18-118">VM의 계획된 또는 계획되지 않은 장애 조치를 개별적으로 또는 복구 계획의 일부로 수행하여 모든 것이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="f2c18-119">이 시나리오를 설정하는 동안 문제가 발생할 경우 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에 문의 사항을 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="f2c18-120">Azure에는 리소스를 만들고 작업하기 위한 두 가지 [배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 인 Azure Resource Manager 모델과 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f2c18-121">또한 Azure에는 두 가지 포털이 있는데, 하나는 클래식 배포 모델을 지원하는 Azure 클래식 포털이고 다른 하나는 두 가지 배포 모델을 모두 지원하는 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="f2c18-122">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="f2c18-123">온-프레미스 필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2c18-123">On-premises prerequisites</span></span>
<span data-ttu-id="f2c18-124">이 시나리오를 배포하기 위해 기본 및 보조 온-프레미스 사이트에서 필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="f2c18-125">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="f2c18-125">**Prerequisites**</span></span> | <span data-ttu-id="f2c18-126">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="f2c18-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c18-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="f2c18-127">**VMM**</span></span> |<span data-ttu-id="f2c18-128">기본 사이트에서 VMM 서버 1개, 보조 사이트에서 VMM 서버 1개를 배포할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="f2c18-129">[단일 VMM 서버의 클라우드 간에 복제](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)에 문의 사항을 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="f2c18-130">이렇게 하려면 VMM 서버에 둘 이상의 클라우드가 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="f2c18-131">VMM 서버는 최신 업데이트를 설치한 System Center 2012 SP1 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="f2c18-132">각 VMM 서버에는 하나 이상의 클라우드가 구성되어 있어야 하고 모든 클라우드에 Hyper-V 용량 프로필이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="f2c18-133">클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="f2c18-134">[VMM 패브릭 클라우드 패브릭 구성](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric) 및 [연습: System Center 2012 SP1 VMM으로 사설 클라우드 만들기](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)에서 VMM 클라우드 설정에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="f2c18-135">VMM 서버는 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="f2c18-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="f2c18-136">**Hyper-V**</span></span> |<span data-ttu-id="f2c18-137">Hyper-V 서버는 Hyper-V 역할로 Windows Server 2012 이상을 실행해야 하며 최신 업데이트가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="f2c18-138">Hyper-V 서버에 VM이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="f2c18-139">Hyper-V 호스트 서버는 기본 및 보조 VMM 클라우드의 호스트 그룹에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="f2c18-140">Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="f2c18-141">Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="f2c18-142">클러스터 브로커를 수동으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="f2c18-143">[자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2c18-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="f2c18-144">**공급자**</span><span class="sxs-lookup"><span data-stu-id="f2c18-144">**Provider**</span></span> |<span data-ttu-id="f2c18-145">사이트 복구 배포 중에 VMM 서버에 Azure Site Recovery 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="f2c18-146">공급자는 HTTPS 443을 통해 Site Recovery와 통신하여 복제를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="f2c18-147">LAN 또는 VPN 연결을 통해 기본 및 보조 Hyper-V 서버 간에 데이터 복제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="f2c18-148">VMM 서버에서 실행되는 공급자는 다음 URL에 액세스할 수 있어야 합니다. *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f2c18-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="f2c18-149">또한 VMM 서버에서 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653)로의 방화벽 통신을 허용하고 HTTPS(443) 프로토콜을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="f2c18-150">네트워크 매핑 필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2c18-150">Network mapping prerequisites</span></span>
<span data-ttu-id="f2c18-151">네트워크 매핑 기능은 다음을 위해 기본 및 보조 VMM 서버의 VMM VM 네트워크 간을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="f2c18-152">장애 조치(Failover) 후 보조 Hyper-V 호스트에 복제본 VM을 최적으로 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="f2c18-153">복제본 VM을 해당 VM 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="f2c18-154">네트워크 매핑을 구성하지 않으면 장애 조치 후에 복제본 VM이 어떤 네트워크에도 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="f2c18-155">Site Recovery를 배포하는 동안 네트워크 매핑을 설정하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="f2c18-156">원본 Hyper-V 호스트 서버의 VM이 VMM VM 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="f2c18-157">해당 네트워크가 클라우드와 연결된 논리 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="f2c18-158">복구에 사용할 보조 클라우드에 해당 VM 네트워크가 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="f2c18-159">해당 VM 네트워크는 보조 클라우드와 연결된 논리 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="f2c18-160">아래 문서에서 VMM 네트워크를 구성하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="f2c18-161">VMM에서 논리 네트워크를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2c18-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="f2c18-162">VMM에서 VM 네트워크 및 게이트웨이를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2c18-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="f2c18-163">[알아보세요](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) .</span><span class="sxs-lookup"><span data-stu-id="f2c18-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="f2c18-164">PowerShell 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f2c18-164">PowerShell prerequisites</span></span>
<span data-ttu-id="f2c18-165">Azure PowerShell을 사용할 준비가 되었는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="f2c18-166">이미 PowerShell을 사용하고 있는 경우 버전 0.8.10 이상으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="f2c18-167">PowerShell 설치에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azureps-cmdlets-docs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f2c18-168">PowerShell을 설정 및 구성하면 [여기](/powershell/azure/overview)에서 서비스에 사용 가능한 모든 cmdlet을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="f2c18-169">Azure PowerShell에서 매개 변수 값, 입력, 출력이 일반적으로 처리되는 방법 등 cmdlet를 사용하는 데 도움이 되는 팁을 보려면 [Azure Cmdlet 시작하기](/powershell/azure/get-started-azureps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="f2c18-170">1단계: 구독 설정</span><span class="sxs-lookup"><span data-stu-id="f2c18-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="f2c18-171">Azure powershell에서 다음 cmdlet을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="f2c18-172">구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="f2c18-173">각 구독의 subscriptionID 목록도 함께 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="f2c18-174">복구 서비스 자격 증명 모음을 만들려는 구독의 subscriptionID를 메모합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="f2c18-175">구독 ID를 알려주어 복구 서비스 자격 증명 모음을 만들 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="f2c18-176">2단계: 복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="f2c18-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="f2c18-177">또한 Azure Resource Manager 리소스 그룹이 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="f2c18-178">새 복구 서비스 자격 증명 모음을 만들고, 만든 ASR 자격 증명 모음 개체를 변수에 저장합니다(나중에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="f2c18-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="f2c18-179">Get-AzureRMRecoveryServicesVault cmdlet을 사용하여 ASR 자격 증명 모음 개체 게시 만들기를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="f2c18-180">3단계: 복구 서비스 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="f2c18-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="f2c18-181">자격 증명 모음을 이미 만든 경우 아래 명령을 실행하여 자격 증명 모음을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="f2c18-182">다음 명령을 실행하여 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="f2c18-183">4단계: Azure Site Recovery 공급자 설치</span><span class="sxs-lookup"><span data-stu-id="f2c18-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="f2c18-184">VMM 컴퓨터에서 다음 명령을 실행하여 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="f2c18-185">다음 명령을 실행하고 다운로드한 공급자를 사용하여 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="f2c18-186">다음 명령을 사용하여 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="f2c18-187">설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="f2c18-188">다음 명령을 사용하여 자격 증명 모음에 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="f2c18-189">5단계: 복제 정책 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="f2c18-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="f2c18-190">다음 명령을 실행하여 Hyper-V 2012 R2 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="f2c18-191">VMM 클라우드는 서로 다른 버전의 Windows Server에서 실행되는 Hyper-V 호스트를 포함할 수 있으나(Hyper-V 필수 구성 요소에 나와 있음) 복제 정책은 OS 버전마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="f2c18-192">운영 체제 버전마다 다른 호스트가 실행되고 있는 경우 각 형식의 OS 버전에 대해 별도의 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="f2c18-193">예를 들어 Windows Server 2012에서 5개의 호스트가 실행되고 있고 Windows Server 2012 R2에서 3개의 호스트가 실행되고 있는 경우 각 운영 체제 버전 형식에 대해 하나씩 2개의 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="f2c18-194">다음 명령을 실행하여 기본 보호 컨테이너(기본 VMM 클라우드) 및 복구 보호 컨테이너(복구 VMM 클라우드)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="f2c18-195">정책의 이름을 사용하여 1단계에서 만든 정책을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="f2c18-196">복제 정책을 사용하여 보호 컨테이너(VMM 클라우드) 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="f2c18-197">정책 연결 작업이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="f2c18-198">다음 PowerShell 코드 조각을 사용하여 작업이 완료되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="f2c18-199">작업에서 처리를 완료하면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="f2c18-200">작동 완료 여부를 확인하려면 [작업 모니터](#monitor)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="f2c18-201">6단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="f2c18-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="f2c18-202">첫 번째 명령은 현재 Azure Site Recovery 자격 증명 모음의 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="f2c18-203">이 명령은 $Servers 어레이 변수에 Microsoft Azure Site Recovery 서버를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="f2c18-204">아래 명령은 원본 VMM 서버 및 대상 VMM 서버에 대한 사이트 복구 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="f2c18-205">원본 VMM 서버는 서버 배열의 첫 번째 또는 두 번째 서버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="f2c18-206">VMM 서버의 이름을 확인하고 네트워크를 적절히 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="f2c18-207">최종 cmdlet는 기본 네트워크와 복구 네트워크 사이에 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="f2c18-208">이 cmdlet는 $PrimaryNetworks의 첫 번째 요소로 기본 네트워크를 지정하고, $RecoveryNetworks의 첫 번째 요소로 복구 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="f2c18-209">7단계: 저장소 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="f2c18-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="f2c18-210">아래 명령으로 저장소 분류의 목록을 $storageclassifications 변수로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="f2c18-211">아래 명령으로 원본 분류를 $SourceClassificaion 변수로 가져오고, 대상 분류를 $TargetClassification 변수로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="f2c18-212">원본 및 대상 분류는 배열의 임의 요소일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="f2c18-213">$storageclassifications 배열에서 원본 및 대상 분류의 인덱스를 알아보려면 아래 명령의 출력을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c18-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="f2c18-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="f2c18-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="f2c18-215">아래 cmdlet은 원본 분류와 대상 분류 간에 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="f2c18-216">8단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="f2c18-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="f2c18-217">서버, 클라우드 및 네트워크가 제대로 구성되었으면 클라우드에서 가상 컴퓨터에 대한 보호를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="f2c18-218">보호를 활성화하려면 다음 명령을 실행하여 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="f2c18-219">다음 명령을 실행하여 VM(보호 엔터티)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="f2c18-220">다음 명령을 실행하여 VM에 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="f2c18-221">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="f2c18-221">Test your deployment</span></span>
<span data-ttu-id="f2c18-222">배포를 테스트하려면 단일 가상 컴퓨터에 대한 테스트 장애 조치(Failover)를 실행하거나, 여러 개의 가상 컴퓨터로 구성된 복구 계획을 만들고 이 계획에 대한 테스트 장애 조치(Failover)를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="f2c18-223">테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="f2c18-224">Azure 포털에서 응용 프로그램에 대한 복구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="f2c18-225">작동 완료 여부를 확인하려면 [작업 모니터](#monitor)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="f2c18-226">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="f2c18-226">Run a test failover</span></span>
1. <span data-ttu-id="f2c18-227">아래 cmdlet를 실행하여 VM에 대해 테스트 장애 조치(Failover)를 수행하려는 VM 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="f2c18-228">다음을 수행하여 VM의 테스트 장애 조치(Failover)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="f2c18-229">다음을 수행하여 복구 계획의 테스트 장애 조치(Failover)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="f2c18-230">계획된 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="f2c18-230">Run a planned failover</span></span>
1. <span data-ttu-id="f2c18-231">다음을 수행하여 VM의 계획된 장애 조치(Failover)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="f2c18-232">다음을 수행하여 복구 계획의 계획된 장애 조치(Failover)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="f2c18-233">계획되지 않은 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="f2c18-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="f2c18-234">다음을 수행하여 VM의 계획되지 않은 장애 조치(Failover)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="f2c18-235">2.다음을 수행하여 복구 계획의 계획되지 않은 장애 조치(Failover)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="f2c18-236"><a name=monitor></a> 작업 모니터</span><span class="sxs-lookup"><span data-stu-id="f2c18-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="f2c18-237">다음 명령을 사용하여 작업을 모니터합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="f2c18-238">처리가 완료될 때까지 기다린 후 다음 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c18-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="f2c18-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2c18-239">Next steps</span></span>
<span data-ttu-id="f2c18-240">[자세히 알아보세요](/powershell/module/azurerm.recoveryservices.backup/#recovery) .</span><span class="sxs-lookup"><span data-stu-id="f2c18-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
