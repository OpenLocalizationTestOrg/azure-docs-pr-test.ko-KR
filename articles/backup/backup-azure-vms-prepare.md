---
title: "aaaPreparing Azure 가상 컴퓨터를 사용자 환경 tooback | Microsoft Docs"
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
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a><span data-ttu-id="d43cd-104">사용자 환경 tooback Azure 가상 컴퓨터를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-104">Prepare your environment tooback up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d43cd-105">Resource Manager 모델</span><span class="sxs-lookup"><span data-stu-id="d43cd-105">Resource Manager model</span></span>](backup-azure-arm-vms-prepare.md)
> * [<span data-ttu-id="d43cd-106">클래식 모델</span><span class="sxs-lookup"><span data-stu-id="d43cd-106">Classic model</span></span>](backup-azure-vms-prepare.md)
>
>

<span data-ttu-id="d43cd-107">Azure VM(가상 컴퓨터)을 백업하려면 세 가지 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-107">Before you can back up an Azure virtual machine (VM), there are three conditions that must exist.</span></span>

* <span data-ttu-id="d43cd-108">백업 자격 증명 모음 toocreate 필요 하거나는 기존 백업 자격 증명 모음을 식별 *hello에서 VM으로 같은 지역*합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-108">You need toocreate a backup vault or identify an existing backup vault *in hello same region as your VM*.</span></span>
* <span data-ttu-id="d43cd-109">Azure 공용 인터넷 및 Azure 저장소 끝점 hello hello 간의 네트워크 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-109">Establish network connectivity between hello Azure public Internet addresses and hello Azure storage endpoints.</span></span>
* <span data-ttu-id="d43cd-110">Hello VM에 hello VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-110">Install hello VM agent on hello VM.</span></span>

<span data-ttu-id="d43cd-111">이러한 조건에서 이미 환경에 존재 하 다음 toohello 진행을 알고 있는 경우 [VMs 문서를 백업](backup-azure-vms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-111">If you know these conditions already exist in your environment then proceed toohello [Back up your VMs article](backup-azure-vms.md).</span></span> <span data-ttu-id="d43cd-112">그렇지 않으면 읽어 보려면이 문서를 안내 합니다 hello 단계 tooprepare Azure VM을 사용자 환경 tooback 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-112">Otherwise, read on, this article will lead you through hello steps tooprepare your environment tooback up an Azure VM.</span></span>

##<a name="supported-operating-system-for-backup"></a><span data-ttu-id="d43cd-113">지원되는 백업용 운영 체제</span><span class="sxs-lookup"><span data-stu-id="d43cd-113">Supported operating system for backup</span></span>
 * <span data-ttu-id="d43cd-114">**Linux**: Azure Backup은 Core OS Linux를 제외한 [Azure 인증 배포 목록](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-114">**Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) except Core OS Linux.</span></span> <span data-ttu-id="d43cd-115">_도 하 게 다른 Bring-Your-소유-Linux 배포판 hello VM 에이전트는 hello 가상 컴퓨터에서 사용할 수 있는 정상적으로 작동 못할 수도 있으며 Python에 대 한 지원. 그러나 이러한 배포판을 백업에 대해서는 보증하지 않습니다._</span><span class="sxs-lookup"><span data-stu-id="d43cd-115">_Other Bring-Your-Own-Linux distributions also might work as long as hello VM agent is available on hello virtual machine and support for Python exists. However, we do not endorse those distributions for backup._</span></span>
 * <span data-ttu-id="d43cd-116">**Windows Server**: Windows Server 2008 R2 이전 버전은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-116">**Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.</span></span>


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a><span data-ttu-id="d43cd-117">VM 백업 및 복원 시의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="d43cd-117">Limitations when backing up and restoring a VM</span></span>
> [!NOTE]
> <span data-ttu-id="d43cd-118">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-118">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d43cd-119">hello 다음 목록에서는 hello 제한 hello 클래식 모델에 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d43cd-119">hello following list provides hello limitations when deploying in hello classic model.</span></span>
>
>

* <span data-ttu-id="d43cd-120">16개 이상의 데이터 디스크가 있는 가상 컴퓨터의 백업은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-120">Backing up virtual machines with more than 16 data disks is not supported.</span></span>
* <span data-ttu-id="d43cd-121">예약된 IP 주소가 있고 정의된 끝점이 없는 가상 컴퓨터의 백업은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-121">Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.</span></span>
* <span data-ttu-id="d43cd-122">백업 데이터는 탑재 된 네트워크 연결 된 드라이브 tooVM 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-122">Backup data doesn't include network mounted drives attached tooVM.</span></span>
* <span data-ttu-id="d43cd-123">복원하는 동안 기존 가상 컴퓨터의 교체는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-123">Replacing an existing virtual machine during restore is not supported.</span></span> <span data-ttu-id="d43cd-124">먼저 hello 기존 가상 컴퓨터 및 모든 관련된 디스크를 삭제 하 고 hello 데이터 백업에서 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-124">First delete hello existing virtual machine and any associated disks, and then restore hello data from backup.</span></span>
* <span data-ttu-id="d43cd-125">지역 간 백업 및 복원은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-125">Cross-region backup and restore is not supported.</span></span>
* <span data-ttu-id="d43cd-126">Azure의 모든 공용 영역에 사용할 hello Azure 백업 서비스를 사용 하 여 가상 컴퓨터를 백업 합니다 (hello 참조 [검사 목록](https://azure.microsoft.com/regions/#services) 지원 되는 지역).</span><span class="sxs-lookup"><span data-stu-id="d43cd-126">Backing up virtual machines by using hello Azure Backup service is supported in all public regions of Azure (see hello [checklist](https://azure.microsoft.com/regions/#services) of supported regions).</span></span> <span data-ttu-id="d43cd-127">원하는 hello 영역 지원 되지 않는 오늘 경우 자격 증명 모음을 만드는 동안 hello 드롭다운 목록에서 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-127">If hello region that you are looking for is unsupported today, it will not appear in hello dropdown list during vault creation.</span></span>
* <span data-ttu-id="d43cd-128">Hello Azure 백업 서비스를 사용 하 여 가상 컴퓨터를 백업 합니다. 선택 운영 체제 버전에 대해서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-128">Backing up virtual machines by using hello Azure Backup service is supported only for select operating system versions:</span></span>
* <span data-ttu-id="d43cd-129">다중 DC 구성의 일부인 도메인 컨트롤러(DC) VM 복원은 PowerShell을 통해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-129">Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell.</span></span> <span data-ttu-id="d43cd-130">[다중 DC 도메인 컨트롤러 복원](backup-azure-restore-vms.md#restoring-domain-controller-vms)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d43cd-130">Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).</span></span>
* <span data-ttu-id="d43cd-131">특수 한 네트워크 구성을 따르고 hello에 있는 가상 컴퓨터를 복원 PowerShell 통해만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-131">Restoring virtual machines that have hello following special network configurations is supported only through PowerShell.</span></span> <span data-ttu-id="d43cd-132">Hello에 hello 복원 워크플로 사용 하 여 만든 Vm hello 복원 작업이 완료 된 후 UI가 이러한 구성을는 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-132">VMs that you create by using hello restore workflow in hello UI will not have these network configurations after hello restore operation is complete.</span></span> <span data-ttu-id="d43cd-133">toolearn 더 참조 [특수 한 네트워크 구성으로 복원 Vm](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-133">toolearn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).</span></span>
  * <span data-ttu-id="d43cd-134">부하 분산 장치 구성에서의 가상 컴퓨터(내부 및 외부)</span><span class="sxs-lookup"><span data-stu-id="d43cd-134">Virtual machines under load balancer configuration (internal and external)</span></span>
  * <span data-ttu-id="d43cd-135">다중의 예약된 IP 주소가 있는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d43cd-135">Virtual machines with multiple reserved IP addresses</span></span>
  * <span data-ttu-id="d43cd-136">다중 네트워크 어댑터가 있는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d43cd-136">Virtual machines with multiple network adapters</span></span>

## <a name="create-a-backup-vault-for-a-vm"></a><span data-ttu-id="d43cd-137">VM에 대한 백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="d43cd-137">Create a backup vault for a VM</span></span>
<span data-ttu-id="d43cd-138">백업 자격 증명 모음에는 모든 hello 백업 및 시간에 따라 생성 된 복구 지점을 저장 하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-138">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="d43cd-139">hello 백업 자격 증명 모음에는 적용 된 toohello 가상 컴퓨터를 백업할 수 있는 hello 백업 정책이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-139">hello backup vault also contains hello backup policies that will be applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d43cd-140">2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-140">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span> <span data-ttu-id="d43cd-141">기존 백업 자격 증명 모음은 계속 지원 되며 가능한 너무[toocreate 백업 자격 증명 모음은 Azure PowerShell을 사용 하 여](./backup-client-automation-classic.md#create-a-backup-vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-141">Existing Backup vaults are still supported, and it is possible too[use Azure PowerShell toocreate Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault).</span></span> <span data-ttu-id="d43cd-142">이후의 향상 된 내용을 tooRecovery 서비스 자격 증명 모음을만 적용 되므로 모든 배포에 대해 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-142">However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply tooRecovery Services vaults, only.</span></span>


<span data-ttu-id="d43cd-143">이 이미지는 hello hello 관계 다양 한 Azure 백업 엔터티를 보여: ![Azure 백업 엔터티 및 관계](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span><span class="sxs-lookup"><span data-stu-id="d43cd-143">This image shows hello relationships between hello various Azure Backup entities: ![Azure Backup entities and relationships](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span></span>



## <a name="network-connectivity"></a><span data-ttu-id="d43cd-144">네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="d43cd-144">Network connectivity</span></span>
<span data-ttu-id="d43cd-145">순서 toomanage hello VM 스냅숏 백업 확장 hello 필요 연결 toohello Azure 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-145">In order toomanage hello VM snapshots, hello backup extension needs connectivity toohello Azure public IP addresses.</span></span> <span data-ttu-id="d43cd-146">Hello 오른쪽 인터넷에 연결 하지 않고 hello 가상 컴퓨터의 HTTP 요청 시간 제한 및 hello 백업 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-146">Without hello right Internet connectivity, hello virtual machine's HTTP requests time out and hello backup operation fails.</span></span> <span data-ttu-id="d43cd-147">배포에 액세스 제한이 있다면(예: 네트워크 보안 그룹(NSG)을 통해), 백업 트래픽에 대해 명확한 경로를 제공하기 위해 이 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-147">If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:</span></span>

* <span data-ttu-id="d43cd-148">[화이트 리스트 hello Azure 데이터 센터 IP 범위](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -어떻게 toowhitelist hello IP 주소에 대 한 지침은 hello 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-148">[Whitelist hello Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see hello article for instructions on how toowhitelist hello IP addresses.</span></span>
* <span data-ttu-id="d43cd-149">트래픽 라우팅을 위해 HTTP 프록시 서버를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-149">Deploy an HTTP proxy server for routing traffic.</span></span>

<span data-ttu-id="d43cd-150">어떤 옵션 toouse를 결정할 때는 hello 장단점은 관리 효율성, 세분화 된 제어 및 비용 까지입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-150">When deciding which option toouse, hello trade-offs are between manageability, granular control, and cost.</span></span>

| <span data-ttu-id="d43cd-151">옵션</span><span class="sxs-lookup"><span data-stu-id="d43cd-151">Option</span></span> | <span data-ttu-id="d43cd-152">장점</span><span class="sxs-lookup"><span data-stu-id="d43cd-152">Advantages</span></span> | <span data-ttu-id="d43cd-153">단점</span><span class="sxs-lookup"><span data-stu-id="d43cd-153">Disadvantages</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d43cd-154">허용 목록 IP 범위</span><span class="sxs-lookup"><span data-stu-id="d43cd-154">Whitelist IP ranges</span></span> |<span data-ttu-id="d43cd-155">추가 비용 없음</span><span class="sxs-lookup"><span data-stu-id="d43cd-155">No additional costs.</span></span><br><br><span data-ttu-id="d43cd-156">NSG에 대 한 액세스를 열기 위한 hello를 사용 하 여 <i>집합 AzureNetworkSecurityRule</i> cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d43cd-156">For opening access in an NSG, use hello <i>Set-AzureNetworkSecurityRule</i> cmdlet.</span></span> |<span data-ttu-id="d43cd-157">시간에 따른 영향을 받음 hello IP 범위 변경으로 복잡 한 toomanage 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-157">Complex toomanage as hello impacted IP ranges change over time.</span></span><br><br><span data-ttu-id="d43cd-158">Azure 및 뿐 아니라 저장소의 toohello 전체 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-158">Provides access toohello whole of Azure, and not just Storage.</span></span> |
| <span data-ttu-id="d43cd-159">HTTP 프록시</span><span class="sxs-lookup"><span data-stu-id="d43cd-159">HTTP proxy</span></span> |<span data-ttu-id="d43cd-160">Url 허용 hello 저장소 hello 프록시에 세부적으로 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-160">Granular control in hello proxy over hello storage URLs allowed.</span></span> <span data-ttu-id="d43cd-161">hello 프록시의 toosetup 세부적으로 제어 https://\*.blob.core.windows.net/\* URL 패턴 toobe 허용 목록 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-161">toosetup granular control in hello proxy, https://\*.blob.core.windows.net/\* URL Pattern needs toobe whitelisted.</span></span> <span data-ttu-id="d43cd-162">toowhitelist에만 저장소 계정에서 hello VM 사용 하는 hello https://\<storageAccount\>.blob.core.windows.net/\* URL 패턴 toobe 허용 목록 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-162">toowhitelist only hello storage account used by hello VM, https://\<storageAccount\>.blob.core.windows.net/\* URL pattern needs toobe whitelisted.</span></span> <br><span data-ttu-id="d43cd-163">단일 지점 인터넷 액세스 tooVMs 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-163">Single point of Internet access tooVMs.</span></span><br><span data-ttu-id="d43cd-164">IP 주소 변경 내용을 tooAzure 대상이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-164">Not subject tooAzure IP address changes.</span></span> |<span data-ttu-id="d43cd-165">Hello 프록시 소프트웨어와 함께 VM을 실행 하기 위한 추가 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-165">Additional costs for running a VM with hello proxy software.</span></span> |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a><span data-ttu-id="d43cd-166">화이트 리스트 hello Azure 데이터 센터 IP 범위</span><span class="sxs-lookup"><span data-stu-id="d43cd-166">Whitelist hello Azure datacenter IP ranges</span></span>
<span data-ttu-id="d43cd-167">toowhitelist hello Azure 데이터 센터 IP 범위를 참조 하십시오. hello [Azure 웹 사이트](http://www.microsoft.com/en-us/download/details.aspx?id=41653) hello IP 범위 및 지침에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-167">toowhitelist hello Azure datacenter IP ranges, please see hello [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on hello IP ranges, and instructions.</span></span>

### <a name="using-an-http-proxy-for-vm-backups"></a><span data-ttu-id="d43cd-168">VM 백업에 HTTP 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="d43cd-168">Using an HTTP proxy for VM backups</span></span>
<span data-ttu-id="d43cd-169">VM을 백업할 때 hello VM에 예비 내선 번호 hello hello 스냅숏 관리 명령을 tooAzure HTTPS API를 사용 하 여 저장소를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-169">When backing up a VM, hello backup extension on hello VM sends hello snapshot management commands tooAzure Storage using an HTTPS API.</span></span> <span data-ttu-id="d43cd-170">액세스 toohello에 대해 구성 된 hello 유일한 구성 요소 이므로 hello HTTP 프록시를 통해 hello 예비 내선 번호 트래픽을 라우팅할 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-170">Route hello backup extension traffic through hello HTTP proxy since it is hello only component configured for access toohello public Internet.</span></span>

> [!NOTE]
> <span data-ttu-id="d43cd-171">사용 해야 하는 hello 프록시 소프트웨어에 대 한 권장 사항 없음 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-171">There is no recommendation for hello proxy software that should be used.</span></span> <span data-ttu-id="d43cd-172">아웃 바운드 인력을 가진 프록시를 선택 하는 확인 하 고 hello 구성 단계와 호환 되는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-172">Ensure that you pick a proxy that has outbound stickiness and which is compatible with hello configuration steps below.</span></span> <span data-ttu-id="d43cd-173">제 3 자 있으며 소프트웨어 hello 프록시 설정도 수정 하지 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="d43cd-173">Make sure third party softwares do not modify hello proxy settings</span></span>
>
>

<span data-ttu-id="d43cd-174">아래 예제에서는 이미지 hello hello 세 가지 구성 단계가 필요한 toouse HTTP 프록시를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-174">hello example image below shows hello three configuration steps necessary toouse an HTTP proxy:</span></span>

* <span data-ttu-id="d43cd-175">응용 프로그램 VM 경로 대 한 모든 HTTP 트래픽이 바인딩된 hello 공용 인터넷을 통해 프록시 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-175">App VM routes all HTTP traffic bound for hello public Internet through Proxy VM.</span></span>
* <span data-ttu-id="d43cd-176">프록시 VM hello 가상 네트워크의 Vm에서 들어오는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-176">Proxy VM allows incoming traffic from VMs in hello virtual network.</span></span>
* <span data-ttu-id="d43cd-177">hello 그룹 NSG (네트워크 보안) 라는 NSF 잠금에는 보안 규칙 아웃 바운드 인터넷 트래픽을 허용 프록시 VM에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-177">hello Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.</span></span>

![HTTP 프록시 배포 다이어그램을 사용하는 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

<span data-ttu-id="d43cd-179">toouse HTTP 프록시 toocommunicating toohello 공용 인터넷을 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-179">toouse an HTTP proxy toocommunicating toohello public Internet, follow these steps:</span></span>

#### <a name="step-1-configure-outgoing-network-connections"></a><span data-ttu-id="d43cd-180">1단계.</span><span class="sxs-lookup"><span data-stu-id="d43cd-180">Step 1.</span></span> <span data-ttu-id="d43cd-181">나가는 네트워크 연결 구성</span><span class="sxs-lookup"><span data-stu-id="d43cd-181">Configure outgoing network connections</span></span>
###### <a name="for-windows-machines"></a><span data-ttu-id="d43cd-182">Windows 컴퓨터의 경우</span><span class="sxs-lookup"><span data-stu-id="d43cd-182">For Windows machines</span></span>
<span data-ttu-id="d43cd-183">로컬 시스템 계정에 대한 프록시 서버 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-183">This will setup proxy server configuration for Local System Account.</span></span>

1. <span data-ttu-id="d43cd-184">[PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span><span class="sxs-lookup"><span data-stu-id="d43cd-184">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span></span>
2. <span data-ttu-id="d43cd-185">관리자 권한 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-185">Run following command from elevated prompt,</span></span>

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     <span data-ttu-id="d43cd-186">Internet Explorer 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-186">It will open internet explorer window.</span></span>
3. <span data-ttu-id="d43cd-187">이동 tooTools-> 인터넷 옵션-> 연결-> LAN 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-187">Go tooTools -> Internet Options -> Connections -> LAN settings.</span></span>
4. <span data-ttu-id="d43cd-188">시스템 계정에 대한 프록시 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-188">Verify proxy settings for System account.</span></span> <span data-ttu-id="d43cd-189">프록시 IP 및 포트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-189">Set Proxy IP and port.</span></span>
5. <span data-ttu-id="d43cd-190">Internet Explorer를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-190">Close Internet Explorer.</span></span>

<span data-ttu-id="d43cd-191">시스템 수준의 프록시 구성을 설정하고 나가는 HTTP/HTTPS 트래픽에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-191">This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.</span></span>

<span data-ttu-id="d43cd-192">설치 프로그램 프록시 서버에 있으면 현재 사용자 계정 (로컬 시스템 계정이 아닌 함)를 사용 하 여 hello 스크립트 tooapply 다음 해당 tooSYSTEMACCOUNT:</span><span class="sxs-lookup"><span data-stu-id="d43cd-192">If you have setup a proxy server on a current user account(not a Local System Account), use hello following script tooapply them tooSYSTEMACCOUNT:</span></span>

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> <span data-ttu-id="d43cd-193">프록시 서버 로그에 "(407)프록시 인증 필요"가 발견되면, 인증이 제대로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-193">If you observe "(407)Proxy Authentication Required" in proxy server log, check your authentication is setup correctly.</span></span>
>
>

###### <a name="for-linux-machines"></a><span data-ttu-id="d43cd-194">Linux 컴퓨터의 경우</span><span class="sxs-lookup"><span data-stu-id="d43cd-194">For Linux machines</span></span>
<span data-ttu-id="d43cd-195">다음 줄 toohello hello 추가 ```/etc/environment``` 파일:</span><span class="sxs-lookup"><span data-stu-id="d43cd-195">Add hello following line toohello ```/etc/environment``` file:</span></span>

```
http_proxy=http://<proxy IP>:<proxy port>
```

<span data-ttu-id="d43cd-196">다음 줄 toohello hello 추가 ```/etc/waagent.conf``` 파일:</span><span class="sxs-lookup"><span data-stu-id="d43cd-196">Add hello following lines toohello ```/etc/waagent.conf``` file:</span></span>

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a><span data-ttu-id="d43cd-197">2단계.</span><span class="sxs-lookup"><span data-stu-id="d43cd-197">Step 2.</span></span> <span data-ttu-id="d43cd-198">Hello 프록시 서버에서 들어오는 연결을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-198">Allow incoming connections on hello proxy server:</span></span>
1. <span data-ttu-id="d43cd-199">Hello 프록시 서버에서 Windows 방화벽을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-199">On hello proxy server, open Windows Firewall.</span></span> <span data-ttu-id="d43cd-200">hello 가장 쉬운 방법은 tooaccess hello 방화벽은 고급 보안이 포함 된 Windows 방화벽에 대 한 toosearch입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-200">hello easiest way tooaccess hello firewall is toosearch for Windows Firewall with Advanced Security.</span></span>

    ![Hello 방화벽을 열으십시오](./media/backup-azure-vms-prepare/firewall-01.png)
2. <span data-ttu-id="d43cd-202">Hello Windows 방화벽 대화 상자에서 마우스 오른쪽 단추로 클릭 **인바운드 규칙** 클릭 **새 규칙...** .</span><span class="sxs-lookup"><span data-stu-id="d43cd-202">In hello Windows Firewall dialog, right-click  **Inbound Rules** and click **New Rule...**.</span></span>

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-02.png)
3. <span data-ttu-id="d43cd-204">Hello에 **새 인바운드 규칙 마법사**, hello 선택 **사용자 지정** hello에 대 한 옵션 **규칙 유형** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-204">In hello **New Inbound Rule Wizard**, choose hello **Custom** option for hello **Rule Type** and click **Next**.</span></span>
4. <span data-ttu-id="d43cd-205">Hello 페이지 tooselect hello에 **프로그램**, 선택 **모든 프로그램** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-205">On hello page tooselect hello **Program**, choose **All Programs** and click **Next**.</span></span>
5. <span data-ttu-id="d43cd-206">Hello에 **프로토콜 및 포트** 페이지 hello 다음 정보를 입력 하 고 클릭 **다음**:</span><span class="sxs-lookup"><span data-stu-id="d43cd-206">On hello **Protocol and Ports** page, enter hello following information and click **Next**:</span></span>

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-03.png)

   * <span data-ttu-id="d43cd-208">*프로토콜 유형*에서 *TCP*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-208">for *Protocol type* choose *TCP*</span></span>
   * <span data-ttu-id="d43cd-209">에 대 한 *로컬 포트* 선택 *특정 포트*, 아래의 hello 필드에 지정 hello ```<Proxy Port>``` 구성 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-209">for *Local port* choose *Specific Ports*, in hello field below specify hello ```<Proxy Port>``` that has been configured.</span></span>
   * <span data-ttu-id="d43cd-210">*원격 포트*에서 *모든 포트*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-210">for *Remote port* select *All Ports*</span></span>

     <span data-ttu-id="d43cd-211">Hello 마법사의 나머지에서는 hello 모든 hello 방식으로 toohello 종료를 클릭 하 고이 규칙 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-211">For hello rest of hello wizard, click all hello way toohello end and give this rule a name.</span></span>

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a><span data-ttu-id="d43cd-212">3단계.</span><span class="sxs-lookup"><span data-stu-id="d43cd-212">Step 3.</span></span> <span data-ttu-id="d43cd-213">예외 규칙 toohello NSG를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-213">Add an exception rule toohello NSG:</span></span>
<span data-ttu-id="d43cd-214">Azure PowerShell 명령 프롬프트를 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-214">In an Azure PowerShell command prompt, enter hello following command:</span></span>

<span data-ttu-id="d43cd-215">다음 명령을 hello 예외 toohello NSG를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-215">hello following command adds an exception toohello NSG.</span></span> <span data-ttu-id="d43cd-216">이 예외 10.0.0.5에서 모든 포트에서의 TCP 트래픽을 허용 tooany 포트 80 (HTTP) 또는 443 (HTTPS)에 대 한 인터넷 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-216">This exception allows TCP traffic from any port on 10.0.0.5 tooany Internet address on port 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="d43cd-217">특정 포트가 필요한 경우 hello 공용 인터넷을 toohello 포트 있는지 tooadd 수 ```-DestinationPortRange``` 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-217">If you require a specific port in hello public Internet, be sure tooadd that port toohello ```-DestinationPortRange``` as well.</span></span>

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

<span data-ttu-id="d43cd-218">*Hello, 적절 한 tooyour 배포 세부 정보로 hello 예에서 hello 이름을 바꾸는 것을 확인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d43cd-218">*Ensure that you replace hello names in hello example with hello details appropriate tooyour deployment.*</span></span>

## <a name="vm-agent"></a><span data-ttu-id="d43cd-219">VM 에이전트</span><span class="sxs-lookup"><span data-stu-id="d43cd-219">VM agent</span></span>
<span data-ttu-id="d43cd-220">Hello Azure 가상 컴퓨터를 백업할 수 있습니다, 전에 hello Azure VM 에이전트에 hello 가상 컴퓨터에 제대로 설치를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-220">Before you can back up hello Azure virtual machine, you should ensure that hello Azure VM agent is correctly installed on hello virtual machine.</span></span> <span data-ttu-id="d43cd-221">Hello VM 에이전트가 가상 컴퓨터를 hello hello 시 선택적 구성 요소를 만들어질 이므로, 해당 hello 확인란 hello 가상 컴퓨터 프로 비전 하기 전에 hello VM 에이전트 선택에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-221">Since hello VM agent is an optional component at hello time that hello virtual machine is created, ensure that hello check box for hello VM agent is selected before hello virtual machine is provisioned.</span></span>

### <a name="manual-installation-and-update"></a><span data-ttu-id="d43cd-222">수동 설치 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="d43cd-222">Manual installation and update</span></span>
<span data-ttu-id="d43cd-223">hello VM 에이전트 hello Azure 갤러리에서에서 생성 된 Vm에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-223">hello VM agent is already present in VMs that are created from hello Azure gallery.</span></span> <span data-ttu-id="d43cd-224">그러나 온-프레미스 데이터 센터에서 마이그레이션된 가상 컴퓨터 hello VM 에이전트가 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-224">However, virtual machines that are migrated from on-premises datacenters would not have hello VM agent installed.</span></span> <span data-ttu-id="d43cd-225">이러한 Vm에 대 한 hello VM 에이전트 toobe 명시적으로 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-225">For such VMs, hello VM agent needs toobe installed explicitly.</span></span> <span data-ttu-id="d43cd-226">에 대해 자세히 알아보세요 [hello VM에 에이전트를 설치 하는 기존 VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-226">Read more about [installing hello VM agent on an existing VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).</span></span>

| <span data-ttu-id="d43cd-227">**작업**</span><span class="sxs-lookup"><span data-stu-id="d43cd-227">**Operation**</span></span> | <span data-ttu-id="d43cd-228">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d43cd-228">**Windows**</span></span> | <span data-ttu-id="d43cd-229">**Linux**</span><span class="sxs-lookup"><span data-stu-id="d43cd-229">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d43cd-230">Hello VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="d43cd-230">Installing hello VM agent</span></span> |<li><span data-ttu-id="d43cd-231">다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-231">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="d43cd-232">관리자 권한 toocomplete hello 설치를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-232">You will need Administrator privileges toocomplete hello installation.</span></span> <li><span data-ttu-id="d43cd-233">[Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-233">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |<li> <span data-ttu-id="d43cd-234">Hello 최신 설치 [Linux 에이전트](https://github.com/Azure/WALinuxAgent) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-234">Install hello latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="d43cd-235">관리자 권한 toocomplete hello 설치를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-235">You will need Administrator privileges toocomplete hello installation.</span></span> <li> <span data-ttu-id="d43cd-236">[Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-236">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |
| <span data-ttu-id="d43cd-237">Hello VM 에이전트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-237">Updating hello VM agent</span></span> |<span data-ttu-id="d43cd-238">업데이트 hello VM 에이전트를 다시 설치 하는 hello 단순하게 [VM 에이전트 이진](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-238">Updating hello VM agent is as simple as reinstalling hello [VM agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><br><span data-ttu-id="d43cd-239">Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-239">Ensure that no backup operation is running while hello VM agent is being updated.</span></span> |<span data-ttu-id="d43cd-240">Hello 지침에 따라 [hello Linux VM 에이전트를 업데이트 ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-240">Follow hello instructions on [updating hello Linux VM agent ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><br><span data-ttu-id="d43cd-241">Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-241">Ensure that no backup operation is running while hello VM agent is being updated.</span></span> |
| <span data-ttu-id="d43cd-242">Hello VM 에이전트 설치 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="d43cd-242">Validating hello VM agent installation</span></span> |<li><span data-ttu-id="d43cd-243">Toohello 이동 *C:\WindowsAzure\Packages* hello Azure VM에서에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-243">Navigate toohello *C:\WindowsAzure\Packages* folder in hello Azure VM.</span></span> <li><span data-ttu-id="d43cd-244">Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-244">You should find hello WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="d43cd-245">Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 선택한 후 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 합니다. 이상.</span><span class="sxs-lookup"><span data-stu-id="d43cd-245">Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="d43cd-246">해당 없음</span><span class="sxs-lookup"><span data-stu-id="d43cd-246">N/A</span></span> |

<span data-ttu-id="d43cd-247">Hello에 대 한 자세한 내용은 [VM 에이전트](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) 및 [어떻게 tooinstall 것](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-247">Learn about hello [VM agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how tooinstall it](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).</span></span>

### <a name="backup-extension"></a><span data-ttu-id="d43cd-248">백업 확장</span><span class="sxs-lookup"><span data-stu-id="d43cd-248">Backup extension</span></span>
<span data-ttu-id="d43cd-249">hello 가상 컴퓨터를 tooback, hello Azure 백업 서비스 확장 toohello VM 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-249">tooback up hello virtual machine, hello Azure Backup service installs an extension toohello VM agent.</span></span> <span data-ttu-id="d43cd-250">hello Azure 백업 서비스에 원활 하 게 업그레이드 및 추가 사용자 개입 없이 hello 예비 내선 번호를 패치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-250">hello Azure Backup service seamlessly upgrades and patches hello backup extension without additional user intervention.</span></span>

<span data-ttu-id="d43cd-251">예비 내선 번호 hello hello VM을 실행 하는 경우 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-251">hello backup extension is installed if hello VM is running.</span></span> <span data-ttu-id="d43cd-252">또한 실행 중인 VM hello 응용 프로그램 일치 복구 지점의 얻을의 가장 큰 기회를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-252">A running VM also provides hello greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="d43cd-253">그러나 hello Azure 백업 서비스는 VM-hello tooback 계속 해제 되어, 고 hello 확장 수 없는 경우에 설치 (즉, 오프 라인 VM).</span><span class="sxs-lookup"><span data-stu-id="d43cd-253">However, hello Azure Backup service will continue tooback up hello VM--even if it is turned off, and hello extension could not be installed (aka Offline VM).</span></span> <span data-ttu-id="d43cd-254">이 경우 hello 복구 지점 수는 *크래시 일관성이 있는* 위에서 설명한 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-254">In this case, hello recovery point will be *crash consistent* as discussed above.</span></span>

## <a name="questions"></a><span data-ttu-id="d43cd-255">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="d43cd-255">Questions?</span></span>
<span data-ttu-id="d43cd-256">기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-256">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43cd-257">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d43cd-257">Next steps</span></span>
<span data-ttu-id="d43cd-258">VM를 백업 하기 위한 환경을 준비 했으면, 했으므로 다음 논리 단계는 toocreate 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-258">Now that you have prepared your environment for backing up your VM, your next logical step is toocreate a backup.</span></span> <span data-ttu-id="d43cd-259">문서를 계획 하는 hello Vm을 백업 하는 방법에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43cd-259">hello planning article provides more detailed information about backing up VMs.</span></span>

* [<span data-ttu-id="d43cd-260">가상 컴퓨터 설정</span><span class="sxs-lookup"><span data-stu-id="d43cd-260">Back up virtual machines</span></span>](backup-azure-vms.md)
* [<span data-ttu-id="d43cd-261">VM 백업 인프라 계획</span><span class="sxs-lookup"><span data-stu-id="d43cd-261">Plan your VM backup infrastructure</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="d43cd-262">가상 컴퓨터 백업 관리</span><span class="sxs-lookup"><span data-stu-id="d43cd-262">Manage virtual machine backups</span></span>](backup-azure-manage-vms.md)
