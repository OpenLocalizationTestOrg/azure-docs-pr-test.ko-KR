---
title: "Azure Virtual Machines를 백업하기 위한 환경 준비 | Microsoft Docs"
description: "환경이 Azure의 가상 컴퓨터를 백업할 준비가 되었는지 확인합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: "백업; 백업;"
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 072efdccaa8df5d430314d753a437b524986b53c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-your-environment-to-back-up-azure-virtual-machines"></a><span data-ttu-id="08c65-104">Azure 가상 컴퓨터를 백업하기 위한 환경 준비</span><span class="sxs-lookup"><span data-stu-id="08c65-104">Prepare your environment to back up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08c65-105">Resource Manager 모델</span><span class="sxs-lookup"><span data-stu-id="08c65-105">Resource Manager model</span></span>](backup-azure-arm-vms-prepare.md)
> * [<span data-ttu-id="08c65-106">클래식 모델</span><span class="sxs-lookup"><span data-stu-id="08c65-106">Classic model</span></span>](backup-azure-vms-prepare.md)
>
>

<span data-ttu-id="08c65-107">Azure VM(가상 컴퓨터)을 백업하려면 세 가지 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-107">Before you can back up an Azure virtual machine (VM), there are three conditions that must exist.</span></span>

* <span data-ttu-id="08c65-108">*VM과 동일한 지역*에서 백업 자격 증명 모음을 만들거나 기존 백업 자격 증명 모음을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-108">You need to create a backup vault or identify an existing backup vault *in the same region as your VM*.</span></span>
* <span data-ttu-id="08c65-109">Azure 공용 인터넷 주소와 Azure 저장소 끝점 간의 네트워크 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-109">Establish network connectivity between the Azure public Internet addresses and the Azure storage endpoints.</span></span>
* <span data-ttu-id="08c65-110">VM에 VM 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-110">Install the VM agent on the VM.</span></span>

<span data-ttu-id="08c65-111">사용자 환경이 이러한 조건을 이미 갖춘 경우 [VM 문서 백업](backup-azure-vms.md)을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-111">If you know these conditions already exist in your environment then proceed to the [Back up your VMs article](backup-azure-vms.md).</span></span> <span data-ttu-id="08c65-112">그렇지 않으면 이 문서에 따라 Azure VM을 백업하도록 환경을 준비하는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-112">Otherwise, read on, this article will lead you through the steps to prepare your environment to back up an Azure VM.</span></span>

##<a name="supported-operating-system-for-backup"></a><span data-ttu-id="08c65-113">지원되는 백업용 운영 체제</span><span class="sxs-lookup"><span data-stu-id="08c65-113">Supported operating system for backup</span></span>
 * <span data-ttu-id="08c65-114">**Linux**: Azure 백업은 Core OS Linux를 제외한 [Azure 인증 배포 목록](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-114">**Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) except Core OS Linux.</span></span> <span data-ttu-id="08c65-115">_가상 컴퓨터에서 VM 에이전트를 사용할 수 있고 Python에 대한 지원이 지속하는 한 기타 Bring-Your-Own-Linux 배포도 작동합니다. 그러나 이러한 배포판을 백업에 대해서는 보증하지 않습니다._</span><span class="sxs-lookup"><span data-stu-id="08c65-115">_Other Bring-Your-Own-Linux distributions also might work as long as the VM agent is available on the virtual machine and support for Python exists. However, we do not endorse those distributions for backup._</span></span>
 * <span data-ttu-id="08c65-116">**Windows Server**: Windows Server 2008 R2 이전 버전은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-116">**Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.</span></span>


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a><span data-ttu-id="08c65-117">VM 백업 및 복원 시의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="08c65-117">Limitations when backing up and restoring a VM</span></span>
> [!NOTE]
> <span data-ttu-id="08c65-118">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-118">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="08c65-119">다음 목록에서는 클래식 모델에서 배포할 때의 제한 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-119">The following list provides the limitations when deploying in the classic model.</span></span>
>
>

* <span data-ttu-id="08c65-120">16개 이상의 데이터 디스크가 있는 가상 컴퓨터의 백업은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-120">Backing up virtual machines with more than 16 data disks is not supported.</span></span>
* <span data-ttu-id="08c65-121">예약된 IP 주소가 있고 정의된 끝점이 없는 가상 컴퓨터의 백업은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-121">Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.</span></span>
* <span data-ttu-id="08c65-122">백업 데이터는 VM에 연결된 네트워크 탑재된 드라이브를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-122">Backup data doesn't include network mounted drives attached to VM.</span></span>
* <span data-ttu-id="08c65-123">복원하는 동안 기존 가상 컴퓨터의 교체는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-123">Replacing an existing virtual machine during restore is not supported.</span></span> <span data-ttu-id="08c65-124">먼저 기존 가상 컴퓨터와 관련 디스크를 모두 삭제한 다음 백업에서 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-124">First delete the existing virtual machine and any associated disks, and then restore the data from backup.</span></span>
* <span data-ttu-id="08c65-125">지역 간 백업 및 복원은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-125">Cross-region backup and restore is not supported.</span></span>
* <span data-ttu-id="08c65-126">Azure 백업 서비스를 사용한 가상 컴퓨터 백업은 Azure의 모든 공용 지역에서 지원됩니다(지원되는 지역은 [검사 목록](https://azure.microsoft.com/regions/#services) 참조).</span><span class="sxs-lookup"><span data-stu-id="08c65-126">Backing up virtual machines by using the Azure Backup service is supported in all public regions of Azure (see the [checklist](https://azure.microsoft.com/regions/#services) of supported regions).</span></span> <span data-ttu-id="08c65-127">찾는 지역이 현재 지원되지 않는 경우, 자격 증명 모음을 만드는 동안 드롭다운 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-127">If the region that you are looking for is unsupported today, it will not appear in the dropdown list during vault creation.</span></span>
* <span data-ttu-id="08c65-128">Azure 백업 서비스를 사용하는 가상 컴퓨터 백업은 선택한 운영 체제 버전에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-128">Backing up virtual machines by using the Azure Backup service is supported only for select operating system versions:</span></span>
* <span data-ttu-id="08c65-129">다중 DC 구성의 일부인 도메인 컨트롤러(DC) VM 복원은 PowerShell을 통해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-129">Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell.</span></span> <span data-ttu-id="08c65-130">[다중 DC 도메인 컨트롤러 복원](backup-azure-restore-vms.md#restoring-domain-controller-vms)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-130">Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).</span></span>
* <span data-ttu-id="08c65-131">다음과 같은 특수 네트워크 구성을 포함하는 가상 컴퓨터 복원은 PowerShell 통해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-131">Restoring virtual machines that have the following special network configurations is supported only through PowerShell.</span></span> <span data-ttu-id="08c65-132">UI에서 복원 워크플로를 사용하여 만든 VM은 복원 작업이 완료된 후 이러한 네트워크 구성을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-132">VMs that you create by using the restore workflow in the UI will not have these network configurations after the restore operation is complete.</span></span> <span data-ttu-id="08c65-133">자세한 내용은 [특수 네트워크 구성을 가진 VM 복원](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-133">To learn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).</span></span>
  * <span data-ttu-id="08c65-134">부하 분산 장치 구성에서의 가상 컴퓨터(내부 및 외부)</span><span class="sxs-lookup"><span data-stu-id="08c65-134">Virtual machines under load balancer configuration (internal and external)</span></span>
  * <span data-ttu-id="08c65-135">다중의 예약된 IP 주소가 있는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="08c65-135">Virtual machines with multiple reserved IP addresses</span></span>
  * <span data-ttu-id="08c65-136">다중 네트워크 어댑터가 있는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="08c65-136">Virtual machines with multiple network adapters</span></span>

## <a name="create-a-backup-vault-for-a-vm"></a><span data-ttu-id="08c65-137">VM에 대한 백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="08c65-137">Create a backup vault for a VM</span></span>
<span data-ttu-id="08c65-138">백업 자격 증명 모음은 모든 백업과 시간에 따라 생성된 복구 지점을 저장하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-138">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="08c65-139">백업 자격 증명 모음에는 백업 중인 가상 컴퓨터에 적용할 백업 정책도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-139">The backup vault also contains the backup policies that will be applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08c65-140">2017년 3월부터는 백업 자격 증명 모음을 만드는 데 더 이상 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-140">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span> <span data-ttu-id="08c65-141">기존 백업 자격 증명 모음은 계속 지원되고 [Azure PowerShell을 사용하여 백업 자격 증명 모음을 만들](./backup-client-automation-classic.md#create-a-backup-vault) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-141">Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault).</span></span> <span data-ttu-id="08c65-142">하지만 향후 향상되는 기능이 Recovery Services 자격 증명 모음에만 적용되므로 Microsoft에서는 모든 배포에 Recovery Services 자격 증명 모음을 만들도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-142">However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.</span></span>


<span data-ttu-id="08c65-143">이 그림은 여러 Azure Backup 엔터티 간의 관계를 보여 줍니다. ![Azure Backup 엔터티 및 관계](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span><span class="sxs-lookup"><span data-stu-id="08c65-143">This image shows the relationships between the various Azure Backup entities: ![Azure Backup entities and relationships](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span></span>



## <a name="network-connectivity"></a><span data-ttu-id="08c65-144">네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="08c65-144">Network connectivity</span></span>
<span data-ttu-id="08c65-145">VM 스냅숏을 관리하려면, 백업 확장에 Azure 공용 IP 주소에 대한 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-145">In order to manage the VM snapshots, the backup extension needs connectivity to the Azure public IP addresses.</span></span> <span data-ttu-id="08c65-146">올바른 인터넷 연결이 없으면, 가상 컴퓨터의 HTTP 요청 시간이 초과되고 백업 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-146">Without the right Internet connectivity, the virtual machine's HTTP requests time out and the backup operation fails.</span></span> <span data-ttu-id="08c65-147">배포에 액세스 제한이 있다면(예: 네트워크 보안 그룹(NSG)을 통해), 백업 트래픽에 대해 명확한 경로를 제공하기 위해 이 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-147">If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:</span></span>

* <span data-ttu-id="08c65-148">[Azure 데이터 센터 IP 범위 허용 목록](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - IP 주소 허용 목록을 만드는 방법에 대한 지침은 이 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-148">[Whitelist the Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see the article for instructions on how to whitelist the IP addresses.</span></span>
* <span data-ttu-id="08c65-149">트래픽 라우팅을 위해 HTTP 프록시 서버를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-149">Deploy an HTTP proxy server for routing traffic.</span></span>

<span data-ttu-id="08c65-150">사용할 옵션을 결정할 때는, 관리 효율성, 세부적인 제어 및 비용 사이에 균형을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-150">When deciding which option to use, the trade-offs are between manageability, granular control, and cost.</span></span>

| <span data-ttu-id="08c65-151">옵션</span><span class="sxs-lookup"><span data-stu-id="08c65-151">Option</span></span> | <span data-ttu-id="08c65-152">장점</span><span class="sxs-lookup"><span data-stu-id="08c65-152">Advantages</span></span> | <span data-ttu-id="08c65-153">단점</span><span class="sxs-lookup"><span data-stu-id="08c65-153">Disadvantages</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c65-154">허용 목록 IP 범위</span><span class="sxs-lookup"><span data-stu-id="08c65-154">Whitelist IP ranges</span></span> |<span data-ttu-id="08c65-155">추가 비용 없음</span><span class="sxs-lookup"><span data-stu-id="08c65-155">No additional costs.</span></span><br><br><span data-ttu-id="08c65-156">NSG에서 액세스를 여는 경우 <i>Set-AzureNetworkSecurityRule</i> cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-156">For opening access in an NSG, use the <i>Set-AzureNetworkSecurityRule</i> cmdlet.</span></span> |<span data-ttu-id="08c65-157">시간이 지남에 따라 영향을 받는 IP 범위가 변경되기 때문에 관리하기가 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-157">Complex to manage as the impacted IP ranges change over time.</span></span><br><br><span data-ttu-id="08c65-158">저장소 뿐만 아니라 Azure 전체에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-158">Provides access to the whole of Azure, and not just Storage.</span></span> |
| <span data-ttu-id="08c65-159">HTTP 프록시</span><span class="sxs-lookup"><span data-stu-id="08c65-159">HTTP proxy</span></span> |<span data-ttu-id="08c65-160">허용되는 저장소 URL에 걸친 프록시에서 세부적인 제어</span><span class="sxs-lookup"><span data-stu-id="08c65-160">Granular control in the proxy over the storage URLs allowed.</span></span> <span data-ttu-id="08c65-161">프록시에서 세분화된 제어를 설정하려면 https://\*.blob.core.windows.net/\* URL 패턴을 허용 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-161">To setup granular control in the proxy, https://\*.blob.core.windows.net/\* URL Pattern needs to be whitelisted.</span></span> <span data-ttu-id="08c65-162">VM에서 사용하는 저장소 계정만 허용 목록에 추가하려면 https://\<storageAccount\>.blob.core.windows.net/\* URL 패턴을 허용 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-162">To whitelist only the storage account used by the VM, https://\<storageAccount\>.blob.core.windows.net/\* URL pattern needs to be whitelisted.</span></span> <br><span data-ttu-id="08c65-163">VM에 대한 인터넷 액세스의 단일 지점</span><span class="sxs-lookup"><span data-stu-id="08c65-163">Single point of Internet access to VMs.</span></span><br><span data-ttu-id="08c65-164">Azure IP 주소 변경이 적용되지 않음</span><span class="sxs-lookup"><span data-stu-id="08c65-164">Not subject to Azure IP address changes.</span></span> |<span data-ttu-id="08c65-165">프록시 소프트웨어를 사용하여 VM을 실행하기 위한 추가 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-165">Additional costs for running a VM with the proxy software.</span></span> |

### <a name="whitelist-the-azure-datacenter-ip-ranges"></a><span data-ttu-id="08c65-166">Azure 데이터 센터 IP 범위 허용 목록</span><span class="sxs-lookup"><span data-stu-id="08c65-166">Whitelist the Azure datacenter IP ranges</span></span>
<span data-ttu-id="08c65-167">Azure 데이터 센터 IP 범위의 허용 목록을 만들려면, [Azure 웹 사이트](http://www.microsoft.com/en-us/download/details.aspx?id=41653)에서 IP 범위에 대한 자세한 내용과 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-167">To whitelist the Azure datacenter IP ranges, please see the [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on the IP ranges, and instructions.</span></span>

### <a name="using-an-http-proxy-for-vm-backups"></a><span data-ttu-id="08c65-168">VM 백업에 HTTP 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="08c65-168">Using an HTTP proxy for VM backups</span></span>
<span data-ttu-id="08c65-169">VM을 백업할 때, VM의 백업 확장이 HTTPS API를 사용하여 Azure 저장소에 스냅숏 관리 명령을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-169">When backing up a VM, the backup extension on the VM sends the snapshot management commands to Azure Storage using an HTTPS API.</span></span> <span data-ttu-id="08c65-170">공용 인터넷에 액세스하도록 구성된 유일한 구성 요소이므로, HTTP 프록시를 통해 백업 확장 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-170">Route the backup extension traffic through the HTTP proxy since it is the only component configured for access to the public Internet.</span></span>

> [!NOTE]
> <span data-ttu-id="08c65-171">사용해야 할 프록시 소프트웨어에 대한 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-171">There is no recommendation for the proxy software that should be used.</span></span> <span data-ttu-id="08c65-172">아웃바운드 연결이 있고 아래의 구성 단계와 호환되는 프록시를 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-172">Ensure that you pick a proxy that has outbound stickiness and which is compatible with the configuration steps below.</span></span> <span data-ttu-id="08c65-173">타사 소프트웨어는 프록시 설정을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-173">Make sure third party softwares do not modify the proxy settings</span></span>
>
>

<span data-ttu-id="08c65-174">아래 예제 이미지는 HTTP 프록시를 사용하는 데 필요한 세 가지 구성 단계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-174">The example image below shows the three configuration steps necessary to use an HTTP proxy:</span></span>

* <span data-ttu-id="08c65-175">앱 VM은 프록시 VM을 통해 공용 인터넷으로 향하는 모든 HTTP 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-175">App VM routes all HTTP traffic bound for the public Internet through Proxy VM.</span></span>
* <span data-ttu-id="08c65-176">프록시 VM은 가상 네트워크의 VM에서 들어오는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-176">Proxy VM allows incoming traffic from VMs in the virtual network.</span></span>
* <span data-ttu-id="08c65-177">NSF-lockdown이라는 이름의 네트워크 보안 그룹(NSG)에 프록시 VM의 아웃바운드 인터넷 트래픽을 허용하는 보안 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-177">The Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.</span></span>

![HTTP 프록시 배포 다이어그램을 사용하는 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

<span data-ttu-id="08c65-179">공용 인터넷 통신에 HTTP 프록시를 사용하려면, 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-179">To use an HTTP proxy to communicating to the public Internet, follow these steps:</span></span>

#### <a name="step-1-configure-outgoing-network-connections"></a><span data-ttu-id="08c65-180">1단계.</span><span class="sxs-lookup"><span data-stu-id="08c65-180">Step 1.</span></span> <span data-ttu-id="08c65-181">나가는 네트워크 연결 구성</span><span class="sxs-lookup"><span data-stu-id="08c65-181">Configure outgoing network connections</span></span>
###### <a name="for-windows-machines"></a><span data-ttu-id="08c65-182">Windows 컴퓨터의 경우</span><span class="sxs-lookup"><span data-stu-id="08c65-182">For Windows machines</span></span>
<span data-ttu-id="08c65-183">로컬 시스템 계정에 대한 프록시 서버 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-183">This will setup proxy server configuration for Local System Account.</span></span>

1. <span data-ttu-id="08c65-184">[PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span><span class="sxs-lookup"><span data-stu-id="08c65-184">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span></span>
2. <span data-ttu-id="08c65-185">관리자 권한 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-185">Run following command from elevated prompt,</span></span>

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     <span data-ttu-id="08c65-186">Internet Explorer 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-186">It will open internet explorer window.</span></span>
3. <span data-ttu-id="08c65-187">도구 -> 인터넷 옵션 -> 연결 -> LAN 설정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-187">Go to Tools -> Internet Options -> Connections -> LAN settings.</span></span>
4. <span data-ttu-id="08c65-188">시스템 계정에 대한 프록시 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-188">Verify proxy settings for System account.</span></span> <span data-ttu-id="08c65-189">프록시 IP 및 포트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-189">Set Proxy IP and port.</span></span>
5. <span data-ttu-id="08c65-190">Internet Explorer를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-190">Close Internet Explorer.</span></span>

<span data-ttu-id="08c65-191">시스템 수준의 프록시 구성을 설정하고 나가는 HTTP/HTTPS 트래픽에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-191">This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.</span></span>

<span data-ttu-id="08c65-192">현재 사용자 계정(로컬 시스템 계정이 아닌)으로 프록시 서버를 설정한 경우에는, 다음 스크립트를 사용하여 SYSTEMACCOUNT에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-192">If you have setup a proxy server on a current user account(not a Local System Account), use the following script to apply them to SYSTEMACCOUNT:</span></span>

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> <span data-ttu-id="08c65-193">프록시 서버 로그에 "(407)프록시 인증 필요"가 발견되면, 인증이 제대로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-193">If you observe "(407)Proxy Authentication Required" in proxy server log, check your authentication is setup correctly.</span></span>
>
>

###### <a name="for-linux-machines"></a><span data-ttu-id="08c65-194">Linux 컴퓨터의 경우</span><span class="sxs-lookup"><span data-stu-id="08c65-194">For Linux machines</span></span>
<span data-ttu-id="08c65-195">다음 줄을 ```/etc/environment``` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-195">Add the following line to the ```/etc/environment``` file:</span></span>

```
http_proxy=http://<proxy IP>:<proxy port>
```

<span data-ttu-id="08c65-196">```/etc/waagent.conf``` 파일에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-196">Add the following lines to the ```/etc/waagent.conf``` file:</span></span>

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-the-proxy-server"></a><span data-ttu-id="08c65-197">2단계.</span><span class="sxs-lookup"><span data-stu-id="08c65-197">Step 2.</span></span> <span data-ttu-id="08c65-198">프록시 서버에서 들어오는 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-198">Allow incoming connections on the proxy server:</span></span>
1. <span data-ttu-id="08c65-199">프록시 서버에서 Windows 방화벽을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-199">On the proxy server, open Windows Firewall.</span></span> <span data-ttu-id="08c65-200">방화벽에 액세스하는 가장 쉬운 방법은 고급 보안이 포함된 Windows 방화벽을 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-200">The easiest way to access the firewall is to search for Windows Firewall with Advanced Security.</span></span>

    ![방화벽 열기](./media/backup-azure-vms-prepare/firewall-01.png)
2. <span data-ttu-id="08c65-202">Windows 방화벽 대화 상자에서 마우스 오른쪽 단추로 **인바운드 규칙**을 클릭한 다음 **새 규칙...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-202">In the Windows Firewall dialog, right-click  **Inbound Rules** and click **New Rule...**.</span></span>

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-02.png)
3. <span data-ttu-id="08c65-204">**새 인바운드 규칙 마법사**에서 **규칙 형식**에 **사용자 지정** 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-204">In the **New Inbound Rule Wizard**, choose the **Custom** option for the **Rule Type** and click **Next**.</span></span>
4. <span data-ttu-id="08c65-205">**프로그램**을 선택하려는 페이지에서 **모든 프로그램**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-205">On the page to select the **Program**, choose **All Programs** and click **Next**.</span></span>
5. <span data-ttu-id="08c65-206">**프로토콜 및 포트** 페이지에서 다음 정보를 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-206">On the **Protocol and Ports** page, enter the following information and click **Next**:</span></span>

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-03.png)

   * <span data-ttu-id="08c65-208">*프로토콜 유형*에서 *TCP*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-208">for *Protocol type* choose *TCP*</span></span>
   * <span data-ttu-id="08c65-209">*로컬 포트*에서 *특정 포트*를 선택하고 아래의 필드에서 구성되어 있는 ```<Proxy Port>```를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-209">for *Local port* choose *Specific Ports*, in the field below specify the ```<Proxy Port>``` that has been configured.</span></span>
   * <span data-ttu-id="08c65-210">*원격 포트*에서 *모든 포트*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-210">for *Remote port* select *All Ports*</span></span>

     <span data-ttu-id="08c65-211">마법사의 나머지 부분의 경우 끝까지 클릭하고 이 규칙에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-211">For the rest of the wizard, click all the way to the end and give this rule a name.</span></span>

#### <a name="step-3-add-an-exception-rule-to-the-nsg"></a><span data-ttu-id="08c65-212">3단계.</span><span class="sxs-lookup"><span data-stu-id="08c65-212">Step 3.</span></span> <span data-ttu-id="08c65-213">NSG에 예외 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="08c65-213">Add an exception rule to the NSG:</span></span>
<span data-ttu-id="08c65-214">Azure PowerShell 명령 프롬프트에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-214">In an Azure PowerShell command prompt, enter the following command:</span></span>

<span data-ttu-id="08c65-215">다음 명령은 NSG에 예외를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-215">The following command adds an exception to the NSG.</span></span> <span data-ttu-id="08c65-216">이 예외는 10.0.0.5의 모든 포트에서 오는 TCP 트래픽을 포트 80(HTTP) 또는 443(HTTPS)의 모든 인터넷 주소에 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-216">This exception allows TCP traffic from any port on 10.0.0.5 to any Internet address on port 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="08c65-217">공용 인터넷에 특정 포트가 필요하면, 해당 포트를 ```-DestinationPortRange``` 에도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-217">If you require a specific port in the public Internet, be sure to add that port to the ```-DestinationPortRange``` as well.</span></span>

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

<span data-ttu-id="08c65-218">*배포에 적절한 세부 정보를 사용하여 예제에서 이름을 대체하도록 합니다.*</span><span class="sxs-lookup"><span data-stu-id="08c65-218">*Ensure that you replace the names in the example with the details appropriate to your deployment.*</span></span>

## <a name="vm-agent"></a><span data-ttu-id="08c65-219">VM 에이전트</span><span class="sxs-lookup"><span data-stu-id="08c65-219">VM agent</span></span>
<span data-ttu-id="08c65-220">Azure 가상 컴퓨터 백업을 시작하기 전에 Azure VM 에이전트가 가상 컴퓨터에 올바르게 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-220">Before you can back up the Azure virtual machine, you should ensure that the Azure VM agent is correctly installed on the virtual machine.</span></span> <span data-ttu-id="08c65-221">VM 에이전트는 가상 컴퓨터를 만들 때의 선택적 구성 요소이므로 가상 컴퓨터를 프로비전하기 전에 VM 에이전트에 대한 확인란이 선택되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-221">Since the VM agent is an optional component at the time that the virtual machine is created, ensure that the check box for the VM agent is selected before the virtual machine is provisioned.</span></span>

### <a name="manual-installation-and-update"></a><span data-ttu-id="08c65-222">수동 설치 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="08c65-222">Manual installation and update</span></span>
<span data-ttu-id="08c65-223">Azure 갤러리에서 만든 VM에는 VM 에이전트가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-223">The VM agent is already present in VMs that are created from the Azure gallery.</span></span> <span data-ttu-id="08c65-224">그러나 온-프레미스 데이터 센터에서 마이그레이션한 가상 컴퓨터에는 VM 에이전트가 설치되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-224">However, virtual machines that are migrated from on-premises datacenters would not have the VM agent installed.</span></span> <span data-ttu-id="08c65-225">이러한 VM의 경우 VM 에이전트를 명시적으로 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-225">For such VMs, the VM agent needs to be installed explicitly.</span></span> <span data-ttu-id="08c65-226">[기존 VM에 VM 에이전트 설치](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-226">Read more about [installing the VM agent on an existing VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).</span></span>

| <span data-ttu-id="08c65-227">**작업**</span><span class="sxs-lookup"><span data-stu-id="08c65-227">**Operation**</span></span> | <span data-ttu-id="08c65-228">**Windows**</span><span class="sxs-lookup"><span data-stu-id="08c65-228">**Windows**</span></span> | <span data-ttu-id="08c65-229">**Linux**</span><span class="sxs-lookup"><span data-stu-id="08c65-229">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c65-230">VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="08c65-230">Installing the VM agent</span></span> |<li><span data-ttu-id="08c65-231">[에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-231">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="08c65-232">설치를 완료하려면 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-232">You will need Administrator privileges to complete the installation.</span></span> <li><span data-ttu-id="08c65-233">[VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 하여 에이전트가 설치되었다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-233">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |<li> <span data-ttu-id="08c65-234">GitHub에서 최신 [Linux 에이전트](https://github.com/Azure/WALinuxAgent) 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-234">Install the latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="08c65-235">설치를 완료하려면 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-235">You will need Administrator privileges to complete the installation.</span></span> <li> <span data-ttu-id="08c65-236">[VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 하여 에이전트가 설치되었다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-236">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |
| <span data-ttu-id="08c65-237">VM 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="08c65-237">Updating the VM agent</span></span> |<span data-ttu-id="08c65-238">VM 에이전트 업데이트는 [VM 에이전트 이진](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)을 다시 설치하면 되는 간단한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-238">Updating the VM agent is as simple as reinstalling the [VM agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><br><span data-ttu-id="08c65-239">VM 에이전트를 업데이트하는 동안 실행 중인 백업 작업이 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-239">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |<span data-ttu-id="08c65-240">[Linux VM 에이전트 업데이트](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-240">Follow the instructions on [updating the Linux VM agent ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><br><span data-ttu-id="08c65-241">VM 에이전트를 업데이트하는 동안 실행 중인 백업 작업이 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-241">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |
| <span data-ttu-id="08c65-242">VM 에이전트 설치 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="08c65-242">Validating the VM agent installation</span></span> |<li><span data-ttu-id="08c65-243">Azure VM에서 *C:\WindowsAzure\Packages* 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-243">Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM.</span></span> <li><span data-ttu-id="08c65-244">WaAppAgent.exe 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-244">You should find the WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="08c65-245">파일을 마우스 오른쪽 단추로 클릭하고 **속성**으로 이동한 다음 **세부 정보** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-245">Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="08c65-246">제품 버전 필드가 2.6.1198.718 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-246">The Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="08c65-247">해당 없음</span><span class="sxs-lookup"><span data-stu-id="08c65-247">N/A</span></span> |

<span data-ttu-id="08c65-248">[VM 에이전트](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) 및 [설치 방법](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="08c65-248">Learn about the [VM agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how to install it](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).</span></span>

### <a name="backup-extension"></a><span data-ttu-id="08c65-249">백업 확장</span><span class="sxs-lookup"><span data-stu-id="08c65-249">Backup extension</span></span>
<span data-ttu-id="08c65-250">가상 컴퓨터를 백업하기 위해 Azure 백업 서비스는 VM 에이전트 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-250">To back up the virtual machine, the Azure Backup service installs an extension to the VM agent.</span></span> <span data-ttu-id="08c65-251">Azure 백업 서비스는 추가 사용자 개입 없이 원활하게 백업 확장을 업그레이드 및 패치합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-251">The Azure Backup service seamlessly upgrades and patches the backup extension without additional user intervention.</span></span>

<span data-ttu-id="08c65-252">백업 확장은 VM을 실행하는 경우 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-252">The backup extension is installed if the VM is running.</span></span> <span data-ttu-id="08c65-253">또한 실행 중인 VM은 응용 프로그램 일치 복구 지점을 확보하는 가장 큰 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-253">A running VM also provides the greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="08c65-254">그러나 Azure 백업 서비스는 VM이 꺼져 확장을 설치할 수 없더라도(즉, 오프라인 VM) VM을 계속 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-254">However, the Azure Backup service will continue to back up the VM--even if it is turned off, and the extension could not be installed (aka Offline VM).</span></span> <span data-ttu-id="08c65-255">이 경우 복구 지점은 위에서 설명한 대로 *크래시 일관성 상태* 가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-255">In this case, the recovery point will be *crash consistent* as discussed above.</span></span>

## <a name="questions"></a><span data-ttu-id="08c65-256">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="08c65-256">Questions?</span></span>
<span data-ttu-id="08c65-257">질문이 있거나 포함되었으면 하는 기능이 있는 경우 [의견을 보내 주세요](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="08c65-257">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08c65-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08c65-258">Next steps</span></span>
<span data-ttu-id="08c65-259">VM을 백업하기 위한 환경을 준비했으므로 이제 백업을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-259">Now that you have prepared your environment for backing up your VM, your next logical step is to create a backup.</span></span> <span data-ttu-id="08c65-260">계획 문서에서는 VM 백업에 대한 보다 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08c65-260">The planning article provides more detailed information about backing up VMs.</span></span>

* [<span data-ttu-id="08c65-261">가상 컴퓨터 설정</span><span class="sxs-lookup"><span data-stu-id="08c65-261">Back up virtual machines</span></span>](backup-azure-vms.md)
* [<span data-ttu-id="08c65-262">VM 백업 인프라 계획</span><span class="sxs-lookup"><span data-stu-id="08c65-262">Plan your VM backup infrastructure</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="08c65-263">가상 컴퓨터 백업 관리</span><span class="sxs-lookup"><span data-stu-id="08c65-263">Manage virtual machine backups</span></span>](backup-azure-manage-vms.md)
