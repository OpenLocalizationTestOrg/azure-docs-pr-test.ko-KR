---
title: "aaaConfigure hello Always On 가용성 그룹에 PowerShell을 사용 하 여 Azure VM | Microsoft Docs"
description: "이 자습서에서는 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 사용 합니다. Azure에서 PowerShell toocreate Always On 가용성 그룹을 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="30b51-104">PowerShell과 함께 Azure VM에서 hello Always On 가용성 그룹을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30b51-105">클래식: UI</span><span class="sxs-lookup"><span data-stu-id="30b51-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="30b51-106">[클래식: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="30b51-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="30b51-107">시작하기 전에 이제 Azure Resource Manager 모델에서 이 작업을 완료할 수 있는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="30b51-108">새 배포에는 Azure Resource Manager 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="30b51-109">[Azure Virtual Machines의 SQL Server Always On 가용성 그룹](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30b51-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30b51-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="30b51-111">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="30b51-112">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="30b51-113">Azure 가상 컴퓨터 (Vm)는 고가용성 SQL Server 시스템의 데이터베이스 관리자가 toolower hello 비용을 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="30b51-114">이 자습서에서는 SQL Server Always On-종단 Azure 환경 내를 사용 하 여 가용성 tooimplement 그룹화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="30b51-115">Hello 자습서의 hello 끝 요소 다음 hello Azure에서 SQL Server Always On 솔루션 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="30b51-116">프런트 엔드 및 백 엔드 서브넷을 비롯한 여러 서브넷을 포함하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="30b51-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="30b51-117">Active Directory 도메인을 포함한 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="30b51-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="30b51-118">배포 된 toohello 백 엔드 서브넷 및 Active Directory 도메인에 가입된 toohello 두 SQL Server Vm</span><span class="sxs-lookup"><span data-stu-id="30b51-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="30b51-119">Hello 노드 과반수 쿼럼 모델 3 노드 Windows 장애 조치 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="30b51-120">가용성 데이터베이스의 동기 커밋 복제본 두 개가 포함된 가용성 그룹</span><span class="sxs-lookup"><span data-stu-id="30b51-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="30b51-121">이 시나리오의 좋은 점은 비용 효율성이나 다른 요소가 아닌 Azure에서의 간소함입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="30b51-122">예를 들어 hello 2 개 노드 장애 조치 클러스터에서 쿼럼 파일 공유 감시로 hello 도메인 컨트롤러를 사용 하 여 Azure에서 계산 시간 hello 2 복제본 가용성 그룹 toosave에 대 한 Vm 수를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="30b51-123">이 메서드는 hello 구성 이상에서 씩 hello VM 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="30b51-124">이 자습서는 단계를 필요한 tooset hello hello tooshow 각 단계의 hello 세부 사항까지 설명 하지 않고 솔루션 위에서 설명 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="30b51-125">따라서 대신 제공 하는 hello GUI 구성 단계를 사용 하 여 PowerShell tootake 스크립팅을 통해 신속 하 게 각 한 단계씩 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="30b51-126">이 자습서에서는 hello 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="30b51-127">가상 컴퓨터 구독이 hello는 Azure 계정이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="30b51-128">이전에 설치한 hello [Azure PowerShell cmdlet](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="30b51-129">온-프레미스 솔루션에 대한 Always On 가용성 그룹을 확실하게 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="30b51-130">자세한 내용은 [Always On 가용성 그룹(SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30b51-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="30b51-131">Tooyour Azure 구독을 연결 하 고 hello 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="30b51-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="30b51-132">로컬 컴퓨터의 PowerShell 창에서 hello Azure 모듈을 가져올 게시 설정 파일 tooyour 컴퓨터 hello를 다운로드 하 여 hello 다운로드 한 게시 설정을 가져와서 PowerShell 세션 tooyour Azure 구독을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="30b51-133">hello **Get-azurepublishsettingsfile** 명령에서 자동으로 azure 관리 인증서를 생성 하 고 tooyour 컴퓨터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="30b51-134">브라우저는 자동으로 열리고 Azure 구독에 대 한 증명된 tooenter hello Microsoft 계정 자격 증명을 하는.</span><span class="sxs-lookup"><span data-stu-id="30b51-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="30b51-135">다운로드 한 hello **.publishsettings** 파일 모든 hello 필요한 정보를 toomanage Azure 구독에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="30b51-136">이 파일 tooa 로컬 디렉터리를 저장 한 후 hello를 사용 하 여 가져올 **Import-azurepublishsettingsfile** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="30b51-137">hello.publishsettings 파일은 Azure 구독 및 서비스 사용자 자격 증명 (인코딩되지 않음)을 사용 하는 tooadminister를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="30b51-138">이 파일에 대 한 보안 모범 사례 hello toostore은 일시적으로 원본 디렉터리 외부 (예를 들어 hello: Libraries\Documents 폴더), 그 다음 hello 가져오기 완료 된 후 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="30b51-139">Access toohello.publishsettings 파일을 얻은 악의적인 사용자는 수 편집 만들고 Azure 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="30b51-140">일련의 합니다를 사용 하는 toocreate 클라우드 IT 인프라 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="30b51-141">명령을 나중에 성공할 tooensure 다음 주의 toohello 지불:</span><span class="sxs-lookup"><span data-stu-id="30b51-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="30b51-142">변수 **$storageAccountName** 및 **$dcServiceName** 이기 때문에 고유 해야 tooidentify 클라우드 저장소 계정과 클라우드 서버를 각각 사용, 인터넷 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="30b51-143">변수에 대 한 지정한 이름과 hello **$affinityGroupName** 및 **$virtualNetworkName** hello 나중에 사용할 가상 네트워크 구성 문서에 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="30b51-144">**$sqlImageName** SQL Server 2012 서비스 팩 1 Enterprise Edition을 포함 하는 hello VM 이미지의 업데이트 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="30b51-145">간단한 설명을 위해 **Contoso! 000** 동일 hello는 hello 전체 자습서 전체에서 사용 되는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="30b51-146">선호도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="30b51-147">구성 파일을 가져와서 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="30b51-148">hello 구성 파일에 다음 XML 문서 hello 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="30b51-149">이라는 가상 네트워크를 지정 간단히 말해서 **ContosoNET** 라는 hello 선호도 그룹에 **ContosoAG**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="30b51-150">Hello 주소 공간 **10.10.0.0/16** 있으며, 두 서브넷 **10.10.1.0/24** 및 **10.10.2.0/24**, 않는 hello 프런트 서브넷과 백 서브넷인 각각.</span><span class="sxs-lookup"><span data-stu-id="30b51-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="30b51-151">hello 프런트 서브넷은 Microsoft SharePoint와 같은 클라이언트 응용 프로그램을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="30b51-152">hello 백 서브넷은 hello SQL Server Vm을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="30b51-153">Hello를 변경 하는 경우 **$affinityGroupName** 및 **$virtualNetworkName** 변수 이전에 변경 해야 hello 이름 아래에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="30b51-154">Hello 선호도 그룹을 만든 구독에 hello 현재 저장소 계정으로 설정 하와 연결 된 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="30b51-155">Hello 새 클라우드 서비스 및 가용성 집합의 hello 도메인 컨트롤러 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="30b51-156">이러한 파이프 된 명령은 다음 작업 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="30b51-157">**New-AzureVMConfig** 는 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="30b51-158">**추가 AzureProvisioningConfig** 제공 hello 독립 실행형 Windows 서버의 구성 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="30b51-159">**추가 AzureDataDisk** 하는 옵션 집합 tooNone 캐싱 hello로 Active Directory 데이터를 저장 하는 데 사용할 hello 데이터 디스크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="30b51-160">**새 AzureVM** 새 클라우드 서비스를 만들고 만듭니다 hello 새 클라우드 서비스에서 새 Azure VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="30b51-161">Hello 새 VM toobe 완전히 프로 비전 기다렸다가 hello 원격 데스크톱 파일 tooyour 작업 디렉터리를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="30b51-162">를 하기 때문에 hello 새 Azure VM 오랜 시간이 tooprovision hello `while` 루프가 toopoll 사용할 준비가 될 때까지 새 VM을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="30b51-163">hello 도메인 컨트롤러 서버는 이제 성공적으로 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="30b51-164">다음으로,이 도메인 컨트롤러 서버에는 hello Active Directory 도메인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="30b51-165">로컬 컴퓨터에 hello PowerShell 창을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="30b51-166">사용 않으려는 다시 이후 toocreate hello 두 SQL Server Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="30b51-167">Hello 도메인 컨트롤러 구성</span><span class="sxs-lookup"><span data-stu-id="30b51-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="30b51-168">Hello 원격 데스크톱 파일을 시작 하 여 toohello 도메인 컨트롤러 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="30b51-169">Hello 컴퓨터 관리자의 AzureAdmin 사용자 이름과 암호를 사용 하 여 **Contoso! 000**를 만들 때 지정 하는 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="30b51-170">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="30b51-171">Hello 다음 실행 **DCPROMO 합니다. EXE** hello 명령 tooset **corp.contoso.com** M 드라이브에 데이터 디렉터리 hello와 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="30b51-172">Hello 명령이 완료 된 후 자동으로 hello VM 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="30b51-173">Hello 원격 데스크톱 파일을 시작 하 여 toohello 도메인 컨트롤러 서버를 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="30b51-174">이번에는 **CORP\Administrator**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="30b51-175">관리자 모드에서 PowerShell 창을 열고 hello 다음 명령을 사용 하 여 hello Active Directory PowerShell 모듈을 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="30b51-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="30b51-176">다음 명령을 tooadd 세 개의 사용자 toohello 도메인 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="30b51-177">**CORP\Install** tooconfigure 사용 되는 모든 항목은 관련 toohello SQL Server 서비스 인스턴스, 장애 조치 클러스터 hello hello 가용성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="30b51-178">**CORP\SQLSvc1** 및 **CORP\SQLSvc2** hello 두 SQL Server Vm에 대 한 hello SQL Server 서비스 계정으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="30b51-179">다음을 실행 하는 hello 다음 명령을 toogive **CORP\Install** hello hello 도메인에서 권한을 toocreate 컴퓨터 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="30b51-180">hello 위에서 지정한 GUID는 hello 컴퓨터 개체 유형에 대 한 hello GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="30b51-181">hello **CORP\Install** 계정 필요한 hello **모든 속성 읽기** 및 **컴퓨터 개체 만들기** hello 장애 조치에 대 한 개체 사용 권한 toocreate hello 활성 직접 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="30b51-182">hello **모든 속성 읽기** 권한이 부여 되어 tooCORP\Install 기본적으로 toogrant 필요는 없습니다 것 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="30b51-183">권한에 대 한 자세한 내용은 필요한 toocreate hello 장애 조치 클러스터에 대 한 참조 [장애 조치 클러스터 단계별 가이드: Active Directory에서 계정 구성](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="30b51-184">Active Directory와 hello 사용자 개체의 구성을 완료 했으므로 다음에 두 SQL Server Vm을 만들 고 toothis 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="30b51-185">Hello SQL Server Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="30b51-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="30b51-186">로컬 컴퓨터에서 열려 있는 toouse hello PowerShell 창을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="30b51-187">Hello 다음 추가 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="30b51-188">IP 주소를 hello **10.10.0.4** toohello는 일반적으로 할당 hello에서 만드는 첫 번째 VM **10.10.0.0/16** Azure 가상 네트워크의 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="30b51-189">실행 하 여 hello 서버의 주소를 도메인 컨트롤러 인지 확인 해야 **IPCONFIG**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="30b51-190">다음 파이프 된 명령은 toocreate hello를 먼저 실행된 hello hello 장애 조치 클러스터의 VM 이름이 **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="30b51-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="30b51-191">위의 hello 명령에 대 한 hello 다음 note:</span><span class="sxs-lookup"><span data-stu-id="30b51-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="30b51-192">**New-azurevmconfig** hello 원하는 가용성 집합 이름을 사용 하 여 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="30b51-193">hello 다음 Vm 만들어집니다 hello로 동일한 가용성 집합 이름이 가입 하는 되도록 toohello 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="30b51-194">**추가 AzureProvisioningConfig** 조인 hello 만든 VM toohello Active Directory 도메인.</span><span class="sxs-lookup"><span data-stu-id="30b51-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="30b51-195">**Set-azuresubnet** 장소 hello 백 서브넷에 VM을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="30b51-196">**새 AzureVM** 새 클라우드 서비스를 만들고 만듭니다 hello 새 클라우드 서비스에서 새 Azure VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="30b51-197">hello **DnsSettings** hello hello 새 클라우드 서비스의 서버에서 hello IP 주소에 대 한 매개 변수를 해당 hello DNS 서버 지정 **10.10.0.4**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="30b51-198">도메인 컨트롤러 서버 hello의 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="30b51-199">이 매개 변수는 필요 tooenable hello 클라우드 서비스 toojoin toohello Active Directory 도메인에 새 Vm을 성공적으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="30b51-200">이 매개 변수가 없으면 수동으로 설정 해야 hello IPv4 설정을 VM toouse hello 도메인 컨트롤러 서버에서 hello 주 DNS 서버로 hello VM 프로 비전 되 고 다음 hello VM toohello Active Directory 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="30b51-201">명명 된 SQL Server Vm toocreate hello 명령 실행된 hello 다음 파이프 된 **ContosoSQL1** 및 **ContosoSQL2**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="30b51-202">위 hello 명령에 대 한 hello 다음 note:</span><span class="sxs-lookup"><span data-stu-id="30b51-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="30b51-203">**New-azurevmconfig** 사용 하 여 hello hello 도메인 컨트롤러 서버와 동일한 가용성 집합 이름을 사용 하 여 hello hello 가상 컴퓨터 갤러리의 SQL Server 2012 서비스 팩 1 엔터프라이즈 버전 이미지 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="30b51-204">또한 운영 체제 디스크 tooread 캐싱 전용 (쓰기 캐싱이 아닌) hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="30b51-205">Hello 데이터베이스 파일 tooa 별도 데이터 디스크는 연결 toohello VM 및 없는 읽기 사용 하 여 구성 하거나 쓰기 캐싱을 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="30b51-206">그러나 hello 차선책은 hello 운영 체제 디스크에 대 한 캐싱을 읽기 tooremove 제거할 수는 없으므로 쓰기 hello 운영 체제 디스크에 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="30b51-207">**추가 AzureProvisioningConfig** 조인 hello 만든 VM toohello Active Directory 도메인.</span><span class="sxs-lookup"><span data-stu-id="30b51-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="30b51-208">**Set-azuresubnet** 장소 hello 백 서브넷에 VM을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="30b51-209">**추가 AzureEndpoint** 클라이언트 응용 프로그램 hello 인터넷에서 이러한 SQL Server 서비스 인스턴스에 액세스할 수 있도록 액세스 끝점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="30b51-210">TooContosoSQL1 및 ContosoSQL2 서로 다른 포트가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="30b51-211">**새 AzureVM** 만듭니다 새 SQL Server VM hello hello에서 동일한 클라우드 서비스 ContosoQuorum으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="30b51-212">동일한 클라우드 서비스 하려는 경우에 toobe hello hello Vm을 배치 해야 hello 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="30b51-213">각 VM toodownload 및 각 VM toobe 완전히 프로 비전에 대 한 원격 데스크톱 파일 tooyour 작업 디렉터리로를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="30b51-214">hello `for` 루프 세 개의 새로운 Vm hello을 순환 하 고 각각의 hello 최상위 중괄호 안의 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="30b51-215">hello SQL Server Vm이 이제 프로 비전 하 고 실행 되지만 SQL Server와 함께 기본 옵션으로 설치 하는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="30b51-216">Hello 장애 조치 클러스터 Vm 초기화</span><span class="sxs-lookup"><span data-stu-id="30b51-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="30b51-217">이 섹션에는 hello 장애 조치 클러스터와 hello SQL Server 설치에 사용할 toomodify hello 3 명의 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="30b51-218">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-218">Specifically:</span></span>

* <span data-ttu-id="30b51-219">모든 서버: tooinstall hello 필요한 **장애 조치 클러스터링** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="30b51-220">모든 서버: tooadd 필요한 **CORP\Install** hello 컴퓨터로 **관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="30b51-221">ContosoSQL1 및 ContosoSQL2만: tooadd 필요한 **CORP\Install** 로 **sysadmin** hello 기본 데이터베이스의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="30b51-222">ContosoSQL1 및 ContosoSQL2만: tooadd 필요한 **NT AUTHORITY\System** 다음 권한을 hello로 로그인 기능으로:</span><span class="sxs-lookup"><span data-stu-id="30b51-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="30b51-223">가용성 그룹 변경</span><span class="sxs-lookup"><span data-stu-id="30b51-223">Alter any availability group</span></span>
  * <span data-ttu-id="30b51-224">SQL 연결</span><span class="sxs-lookup"><span data-stu-id="30b51-224">Connect SQL</span></span>
  * <span data-ttu-id="30b51-225">서버 상태 보기</span><span class="sxs-lookup"><span data-stu-id="30b51-225">View server state</span></span>
* <span data-ttu-id="30b51-226">ContosoSQL1 및 ContosoSQL2만: hello **TCP** 프로토콜이 hello SQL Server VM에서 이미 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="30b51-227">그러나 여전히 tooopen hello 방화벽에 필요한 SQL Server의 원격 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="30b51-228">이제 준비 toostart 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-228">Now, you're ready toostart.</span></span> <span data-ttu-id="30b51-229">부터는 **ContosoQuorum**, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="30b51-230">너무 연결**ContosoQuorum** hello 원격 데스크톱 파일을 시작 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="30b51-231">Hello 컴퓨터 관리자의 이름을 사용 하 여 **AzureAdmin** 및 암호 **Contoso! 000**, hello Vm을 만들 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="30b51-232">hello 컴퓨터 성공적으로 가입한 너무 확인**corp.contoso.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="30b51-233">계속 하기 전에 hello 자동화 된 초기화 작업을 실행 하는 hello SQL Server 설치 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="30b51-234">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="30b51-235">Hello Windows 장애 조치 클러스터링 기능을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="30b51-236">**CORP\Install**을 로컬 관리자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="30b51-237">ContosoQuorum에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="30b51-238">이제 이 서버에서는 작업을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="30b51-239">다음으로 **ContosoSQL1** 및 **ContosoSQL2**를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="30b51-240">두 SQL Server Vm에 대 한 동일한 hello 단계 아래를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="30b51-241">Hello 원격 데스크톱 파일을 시작 하 여 toohello 두 SQL Server Vm을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="30b51-242">Hello 컴퓨터 관리자의 이름을 사용 하 여 **AzureAdmin** 및 암호 **Contoso! 000**, hello Vm을 만들 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="30b51-243">hello 컴퓨터 성공적으로 가입한 너무 확인**corp.contoso.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="30b51-244">계속 하기 전에 hello 자동화 된 초기화 작업을 실행 하는 hello SQL Server 설치 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="30b51-245">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="30b51-246">Hello Windows 장애 조치 클러스터링 기능을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="30b51-247">**CORP\Install**을 로컬 관리자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="30b51-248">Hello를 SQL Server PowerShell 공급자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="30b51-249">추가 **CORP\Install** hello 기본 SQL Server 인스턴스에 대 한 hello sysadmin 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="30b51-250">추가 **NT AUTHORITY\System** 위에서 설명한 세 hello 권한으로 로그인 기능으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="30b51-251">SQL Server의 원격 액세스에 대 한 hello 방화벽을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="30b51-252">두 VM에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="30b51-253">마지막으로 준비 tooconfigure hello 가용성 그룹 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="30b51-254">Hello SQL Server PowerShell 공급자 tooperform에 hello 사용를 사용 하 여 **ContosoSQL1**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="30b51-255">Hello 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="30b51-255">Configure hello availability group</span></span>
1. <span data-ttu-id="30b51-256">너무 연결**ContosoSQL1** hello 원격 데스크톱 파일을 시작 하 여 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="30b51-257">Hello 컴퓨터 계정을 사용 하 여 로그인 하는 대신 사용 하 여 로그인 **CORP\Install**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="30b51-258">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="30b51-259">Hello 다음 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="30b51-260">Hello를 SQL Server PowerShell 공급자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="30b51-261">ContosoSQL1 tooCORP\SQLSvc1에 대 한 hello SQL Server 서비스 계정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="30b51-262">ContosoSQL2 tooCORP\SQLSvc2에 대 한 hello SQL Server 서비스 계정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="30b51-263">다운로드 **CreateAzureFailoverCluster.ps1** 에서 [Always On 가용성 그룹에서 Azure VM에 대 한 장애 조치 클러스터 만들기](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello 로컬 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="30b51-264">이 스크립트 toohelp 기능 장애 조치 클러스터를 만들고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="30b51-265">Windows 장애 조치 클러스터링과 상호 작용 방식 hello Azure에 대 한 중요 정보에 대 한 네트워크, 참조 [Azure 가상 컴퓨터의 SQL Server에 대 한 고가용성 및 재해 복구](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="30b51-266">Tooyour 작업 디렉터리를 변경 하 고 다운로드 한 hello 스크립트와 함께 hello 장애 조치 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="30b51-267">Hello 기본 SQL Server 인스턴스에 대 한 Always On 가용성 그룹에서 사용 하도록 설정 **ContosoSQL1** 및 **ContosoSQL2**합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="30b51-268">백업 디렉터리를 만들고 hello SQL Server 서비스 계정에 대 한 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="30b51-269">Hello 보조 복제본에서이 디렉터리 tooprepare hello 가용성 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="30b51-270">데이터베이스를 만들 **ContosoSQL1** 호출 **MyDB1**, 전체 백업과 로그 백업을 모두 및에 복원할 **ContosoSQL2** hello로 **WITH NORECOVERY** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="30b51-271">Hello SQL Server Vm에 hello 가용성 그룹 끝점을 만들고 hello 끝점에 hello 적절 한 사용 권한을 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="30b51-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="30b51-272">Hello 가용성 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="30b51-273">마지막으로 hello 가용성 그룹과 조인 hello toohello 가용성 그룹 보조 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="30b51-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30b51-274">Next steps</span></span>
<span data-ttu-id="30b51-275">이제 Azure에서 가용성 그룹을 만들어 SQL Server Always On을 성공적으로 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="30b51-276">이 가용성 그룹에 대 한 수신기 tooconfigure 참조 [Azure에서 Always On 가용성 그룹에 대 한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b51-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="30b51-277">Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30b51-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
