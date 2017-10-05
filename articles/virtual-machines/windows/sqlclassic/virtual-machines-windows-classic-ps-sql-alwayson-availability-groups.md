---
title: "PowerShell을 사용하여 Azure VM에 Always On 가용성 그룹 구성 | Microsoft Docs"
description: "이 자습서에서는 클래식 배포 모델로 생성된 리소스를 사용합니다. PowerShell을 사용하여 Azure에 Always On 가용성 그룹을 만듭니다."
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
ms.openlocfilehash: b99cf767fb931d3f7fe14fcbe7990126244613ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="364aa-104">PowerShell을 사용하여 Azure VM에 Always On 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="364aa-104">Configure the Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="364aa-105">클래식: UI</span><span class="sxs-lookup"><span data-stu-id="364aa-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="364aa-106">[클래식: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="364aa-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="364aa-107">시작하기 전에 이제 Azure Resource Manager 모델에서 이 작업을 완료할 수 있는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="364aa-108">새 배포에는 Azure Resource Manager 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="364aa-109">[Azure Virtual Machines의 SQL Server Always On 가용성 그룹](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364aa-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="364aa-110">대부분의 새로운 배포에서는 Azure Resource Manager 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-110">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="364aa-111">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="364aa-112">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-112">This article covers using the classic deployment model.</span></span>

<span data-ttu-id="364aa-113">Azure Virtual Machines(VM)는 데이터베이스 관리자가 고가용성 SQL Server 시스템의 비용을 절감하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-113">Azure virtual machines (VMs) can help database administrators to lower the cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="364aa-114">이 자습서에서는 Azure 환경 내에서 종단 간에 SQL Server Always On을 사용하여 가용성 그룹을 구현하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-114">This tutorial shows you how to implement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="364aa-115">자습서 마지막에서 Azure의 SQL Server Always On 솔루션은 다음 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-115">At the end of the tutorial, your SQL Server Always On solution in Azure will consist of the following elements:</span></span>

* <span data-ttu-id="364aa-116">프런트 엔드 및 백 엔드 서브넷을 비롯한 여러 서브넷을 포함하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="364aa-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="364aa-117">Active Directory 도메인을 포함한 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="364aa-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="364aa-118">백 엔드 서브넷에 배포되고 Active Directory 도메인에 가입된 SQL Server VM 2개</span><span class="sxs-lookup"><span data-stu-id="364aa-118">Two SQL Server VMs that are deployed to the back-end subnet and joined to the Active Directory domain.</span></span>
* <span data-ttu-id="364aa-119">노드 과반수 쿼럼 모델을 포함하는 3-노드 Windows 장애 조치(Failover) 클러스터</span><span class="sxs-lookup"><span data-stu-id="364aa-119">A three-node Windows failover cluster with the Node Majority quorum model.</span></span>
* <span data-ttu-id="364aa-120">가용성 데이터베이스의 동기 커밋 복제본 두 개가 포함된 가용성 그룹</span><span class="sxs-lookup"><span data-stu-id="364aa-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="364aa-121">이 시나리오의 좋은 점은 비용 효율성이나 다른 요소가 아닌 Azure에서의 간소함입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="364aa-122">예를 들어, Azure에서 계산 시간을 줄이기 위해 2-노드 장애 조치(Failover) 클러스터에서 도메인 컨트롤러를 쿼럼 파일 공유 감시로 사용하여 두 개의 복제본 가용성 그룹에 대한 VM 수를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-122">For example, you can minimize the number of VMs for a two-replica availability group to save on compute hours in Azure by using the domain controller as the quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="364aa-123">이 방법을 사용하면 위의 구성에서 하나로 VM 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-123">This method reduces the VM count by one from the above configuration.</span></span>

<span data-ttu-id="364aa-124">이 자습서는 각 단계를 상세히 설명하지 않고 위에서 설명한 솔루션을 설정하는 데 필요한 단계를 보여주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-124">This tutorial is intended to show you the steps that are required to set up the described solution above, without elaborating on the details of each step.</span></span> <span data-ttu-id="364aa-125">따라서 GUI 구성 단계를 제공하는 대신 PowerShell 스크립팅을 사용하여 각 단계를 신속히 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-125">Therefore, instead of providing the GUI configuration steps, it uses PowerShell scripting to take you quickly through each step.</span></span> <span data-ttu-id="364aa-126">이 자습서에서는 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-126">This tutorial assumes the following:</span></span>

* <span data-ttu-id="364aa-127">가상 컴퓨터 구독이 포함된 Azure 계정이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-127">You already have an Azure account with the virtual machine subscription.</span></span>
* <span data-ttu-id="364aa-128">[Azure PowerShell cmdlet](/powershell/azure/overview)이 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-128">You've installed the [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="364aa-129">온-프레미스 솔루션에 대한 Always On 가용성 그룹을 확실하게 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="364aa-130">자세한 내용은 [Always On 가용성 그룹(SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364aa-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-to-your-azure-subscription-and-create-the-virtual-network"></a><span data-ttu-id="364aa-131">Azure 구독에 연결하고 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="364aa-131">Connect to your Azure subscription and create the virtual network</span></span>
1. <span data-ttu-id="364aa-132">로컬 컴퓨터의 PowerShell 창에서 Azure 모듈을 가져오고, 게시 설정 파일을 사용자 컴퓨터에 다운로드한 다음 다운로드한 게시 설정을 가져와서 PowerShell 세션을 Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-132">In a PowerShell window on your local computer, import the Azure module, download the publishing settings file to your machine, and connect your PowerShell session to your Azure subscription by importing the downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="364aa-133">**Get-AzurePublishSettingsFile** 명령은 Azure에서 관리 인증서를 자동으로 생성하여 사용자 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-133">The **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it to your machine.</span></span> <span data-ttu-id="364aa-134">브라우저가 자동으로 열리고 Azure 구독에 대해 Microsoft 계정 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-134">A browser is automatically opened, and you're prompted to enter the Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="364aa-135">다운로드한 **.publishsettings** 파일에는 Azure 구독 관리에 필요한 모든 정보가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-135">The downloaded **.publishsettings** file contains all the information that you need to manage your Azure subscription.</span></span> <span data-ttu-id="364aa-136">이 파일을 로컬 디렉터리에 저장한 후 **Import-AzurePublishSettingsFile** 명령을 사용하여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-136">After saving this file to a local directory, import it by using the **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="364aa-137">.publishsettings 파일에는 Azure 구독 및 서비스를 관리하는 데 사용되는 자격 증명(인코딩 해제)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-137">The .publishsettings file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="364aa-138">이 파일의 보안을 유지하는 가장 좋은 방법은 소스 디렉터리 밖(예: Libraries\Documents 폴더)에 임시로 파일을 저장한 다음 가져오기가 완료되면 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-138">The security best practice for this file is to store it temporarily outside your source directories (for example, in the Libraries\Documents folder), and then delete it after the import has finished.</span></span> <span data-ttu-id="364aa-139">악의적인 사용자가 .publishsettings 파일에 액세스할 경우 Azure 서비스를 편집, 생성 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-139">A malicious user who gains access to the .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="364aa-140">클라우드 IT 인프라를 만드는 데 사용할 일련의 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-140">Define a series of variables that you'll use to create your cloud IT infrastructure.</span></span>

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

    <span data-ttu-id="364aa-141">명령이 나중에 성공적으로 실행되려면 다음에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-141">Pay attention to the following to ensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="364aa-142">**$storageAccountName** 및 **$dcServiceName** 변수는 인터넷에서 각각 클라우드 저장소 계정 및 클라우드 서버를 식별하는 데 사용되므로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used to identify your cloud storage account and cloud server, respectively, on the Internet.</span></span>
   * <span data-ttu-id="364aa-143">**$affinityGroupName** 및 **$virtualNetworkName** 변수에 지정하는 이름은 나중에 사용하게 될 가상 네트워크 구성 문서에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-143">The names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in the virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="364aa-144">**$sqlImageName** 은 SQL Server 2012 Service Pack 1 Enterprise Edition을 포함하는 VM 이미지의 업데이트된 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-144">**$sqlImageName** specifies the updated name of the VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="364aa-145">간단히 하기 위해 이 자습서에서는 전체적으로 **Contoso!000**을 동일한 암호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-145">For simplicity, **Contoso!000** is the same password that's used throughout the entire tutorial.</span></span>

3. <span data-ttu-id="364aa-146">선호도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="364aa-147">구성 파일을 가져와서 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="364aa-148">구성 파일은 다음 XML 문서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-148">The configuration file contains the following XML document.</span></span> <span data-ttu-id="364aa-149">간단히 말해 **ContosoAG**라는 선호도 그룹에 **ContosoNET**이라는 가상 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-149">In brief, it specifies a virtual network called **ContosoNET** in the affinity group called **ContosoAG**.</span></span> <span data-ttu-id="364aa-150">주소 공간은 **10.10.0.0/16**이고 서브넷 두 개 즉, **10.10.1.0/24** 및**10.10.2.0/24**있으며, 각각 프런트 서브넷 및 백 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-150">It has the address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are the front subnet and back subnet, respectively.</span></span> <span data-ttu-id="364aa-151">프런트 서브넷은 Microsoft SharePoint와 같은 클라이언트 응용 프로그램을 배치하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-151">The front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="364aa-152">백 서브넷은 SQL Server VM을 배치할 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-152">The back subnet is where you'll place the SQL Server VMs.</span></span> <span data-ttu-id="364aa-153">**$affinityGroupName** 및 **$virtualNetworkName** 변수를 앞에서 변경할 경우 아래의 해당하는 이름도 함께 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-153">If you change the **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change the corresponding names below.</span></span>

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

5. <span data-ttu-id="364aa-154">만든 선호도 그룹과 연결되는 저장소 계정을 만들고 해당 계정을 구독에서 현재 저장소 계정으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-154">Create a storage account that's associated with the affinity group that you created, and set it as the current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="364aa-155">새 클라우드 서비스와 가용성 집합에 도메인 컨트롤러 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-155">Create the domain controller server in the new cloud service and availability set.</span></span>

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

    <span data-ttu-id="364aa-156">이러한 파이프 명령은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-156">These piped commands do the following things:</span></span>

   * <span data-ttu-id="364aa-157">**New-AzureVMConfig** 는 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="364aa-158">**Add-AzureProvisioningConfig** 는 독립 실행형 Windows 서버의 구성 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-158">**Add-AzureProvisioningConfig** gives the configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="364aa-159">**Add-AzureDataDisk**는 Active Directory 데이터를 저장하는 데 사용할 데이터 디스크를 추가하며 캐싱 옵션은 None으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-159">**Add-AzureDataDisk** adds the data disk that you'll use for storing Active Directory data, with the caching option set to None.</span></span>
   * <span data-ttu-id="364aa-160">**New-AzureVM** 은 새 클라우드 서비스를 만들고 새 클라우드 서비스에 새 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-160">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span>

7. <span data-ttu-id="364aa-161">새 VM이 완전히 프로비전될 때까지 기다린 다음 작업 디렉터리에 원격 데스크톱 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-161">Wait for the new VM to be fully provisioned, and download the remote desktop file to your working directory.</span></span> <span data-ttu-id="364aa-162">새 Azure VM은 프로비전에 시간이 오래 걸리므로 새 VM이 사용 준비가 될 때까지 `while` 루프가 새 VM을 지속적으로 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-162">Because the new Azure VM takes a long time to provision, the `while` loop continues to poll the new VM until it's ready for use.</span></span>

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

<span data-ttu-id="364aa-163">이제 도메인 컨트롤러 서버가 성공적으로 프로비전되었습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-163">The domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="364aa-164">다음으로 이 도메인 컨트롤러 서버에 Active Directory 도메인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-164">Next, you'll configure the Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="364aa-165">로컬 컴퓨터에 PowerShell 창을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-165">Leave the PowerShell window open on your local computer.</span></span> <span data-ttu-id="364aa-166">이 창은 나중에 두 SQL Server VM을 만들 때 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-166">You'll use it again later to create the two SQL Server VMs.</span></span>

## <a name="configure-the-domain-controller"></a><span data-ttu-id="364aa-167">도메인 컨트롤러 구성</span><span class="sxs-lookup"><span data-stu-id="364aa-167">Configure the domain controller</span></span>
1. <span data-ttu-id="364aa-168">원격 데스크톱 파일을 실행하여 도메인 컨트롤러 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-168">Connect to the domain controller server by launching the remote desktop file.</span></span> <span data-ttu-id="364aa-169">새 VM을 만들 때 지정한 컴퓨터 관리자의 사용자 이름 AzureAdmin과 암호 **Contoso! 000**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-169">Use the machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created the new VM.</span></span>
2. <span data-ttu-id="364aa-170">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="364aa-171">다음 **DCPROMO.EXE** 명령을 실행하여 M 드라이브의 데이터 디렉터리로 **corp.contoso.com** 도메인을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-171">Run the following **DCPROMO.EXE** command to set up the **corp.contoso.com** domain, with the data directories on drive M.</span></span>

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

    <span data-ttu-id="364aa-172">명령이 완료되면 VM이 자동으로 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-172">After the command finishes, the VM restarts automatically.</span></span>

4. <span data-ttu-id="364aa-173">원격 데스크톱 파일을 실행하여 도메인 컨트롤러 서버에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-173">Connect to the domain controller server again by launching the remote desktop file.</span></span> <span data-ttu-id="364aa-174">이번에는 **CORP\Administrator**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="364aa-175">관리자 모드에서 PowerShell 창을 열고 다음 명령을 사용하여 Active Directory PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-175">Open a PowerShell window in administrator mode, and import the Active Directory PowerShell module by using the following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="364aa-176">다음 명령을 실행하여 도메인에 3명의 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-176">Run the following commands to add three users to the domain.</span></span>

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

    <span data-ttu-id="364aa-177">**CORP\Install**은 SQL Server 서비스 인스턴스, 장애 조치 클러스터, 가용성 그룹과 연관된 모든 항목을 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-177">**CORP\Install** is used to configure everything related to the SQL Server service instances, the failover cluster, and the availability group.</span></span> <span data-ttu-id="364aa-178">**CORP\SQLSvc1** 및 **CORP\SQLSvc2**는 두 SQL Server VM에 대한 SQL Server 서비스 계정으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as the SQL Server service accounts for the two SQL Server VMs.</span></span>
7. <span data-ttu-id="364aa-179">이후 다음 명령을 실행하여 도메인에서 컴퓨터 개체를 만들 권한을 **CORP\Install**에 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-179">Next, run the following commands to give **CORP\Install** the permissions to create computer objects in the domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="364aa-180">위에서 지정한 GUID는 컴퓨터 개체 유형의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-180">The GUID specified above is the GUID for the computer object type.</span></span> <span data-ttu-id="364aa-181">장애 조치(Failover) 클러스터에서 Active Directory 개체를 만들기 위해 **CORP\Install** 계정에는 **모든 속성 읽기** 및 **컴퓨터 개체 만들기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-181">The **CORP\Install** account needs the **Read All Properties** and **Create Computer Objects** permission to create the Active Direct objects for the failover cluster.</span></span> <span data-ttu-id="364aa-182">**모든 속성 읽기** 권한은 이미 CORP\Install에 기본적으로 부여되어 있으므로 명시적으로 부여하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-182">The **Read All Properties** permission is already given to CORP\Install by default, so you don't need to grant it explicitly.</span></span> <span data-ttu-id="364aa-183">장애 조치(Failover) 클러스터를 만드는 데 필요한 권한에 대한 자세한 내용은 [장애 조치 클러스터 단계별 가이드: Active Directory의 계정 구성](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364aa-183">For more information on permissions that are needed to create the failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="364aa-184">Active Directory 및 사용자 개체 구성을 완료하면 2개의 SQL Server VM이 생성되고 이 도메인에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-184">Now that you've finished configuring Active Directory and the user objects, you'll create two SQL Server VMs and join them to this domain.</span></span>

## <a name="create-the-sql-server-vms"></a><span data-ttu-id="364aa-185">SQL Server VM 만들기</span><span class="sxs-lookup"><span data-stu-id="364aa-185">Create the SQL Server VMs</span></span>
1. <span data-ttu-id="364aa-186">로컬 컴퓨터에 열려 있는 PowerShell 창을 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-186">Continue to use the PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="364aa-187">다음 추가 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-187">Define the following additional variables:</span></span>

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

    <span data-ttu-id="364aa-188">일반적으로 Azure Virtual Network의 **10.10.0.0/16** 서브넷에 만든 최초의 VM에 IP 주소 **10.10.0.4**가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-188">The IP address **10.10.0.4** is typically assigned to the first VM that you create in the **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="364aa-189">**IPCONFIG**를 실행하여 이것이 도메인 컨트롤러 서버의 주소인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-189">You should verify that this is the address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="364aa-190">다음 파이프 명령을 실행하여 이름이 **ContosoQuorum**인 장애 조치 클러스터의 첫 번째 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-190">Run the following piped commands to create the first VM in the failover cluster, named **ContosoQuorum**:</span></span>

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

    <span data-ttu-id="364aa-191">위의 명령과 관련하여 다음에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-191">Note the following regarding the command above:</span></span>

   * <span data-ttu-id="364aa-192">**New-AzureVMConfig** 는 원하는 가용성 집합 이름으로 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-192">**New-AzureVMConfig** creates a VM configuration with the desired availability set name.</span></span> <span data-ttu-id="364aa-193">이후의 VM은 동일한 가용성 집합에 가입할 수 있도록 같은 가용성 집합 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-193">The subsequent VMs will be created with the same availability set name so that they're joined to the same availability set.</span></span>
   * <span data-ttu-id="364aa-194">**Add-AzureProvisioningConfig**는 VM을 사용자가 만든 Active Directory 도메인에 가입시킵니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-194">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="364aa-195">**Set-AzureSubnet**은 백 서브넷에 VM을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-195">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="364aa-196">**New-AzureVM** 은 새 클라우드 서비스를 만들고 새 클라우드 서비스에 새 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-196">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span> <span data-ttu-id="364aa-197">**DnsSettings** 매개 변수는 새 클라우드 서비스에서 서버의 DNS 서버가 IP 주소 **10.10.0.4**를 갖도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-197">The **DnsSettings** parameter specifies that the DNS server for the servers in the new cloud service has the IP address **10.10.0.4**.</span></span> <span data-ttu-id="364aa-198">이 주소는 도메인 컨트롤러 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-198">This is the IP address of the domain controller server.</span></span> <span data-ttu-id="364aa-199">이 매개 변수는 클라우드 서비스의 새 VM을 성공적으로 Active Directory 도메인에 연결하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-199">This parameter is needed to enable the new VMs in the cloud service to join to the Active Directory domain successfully.</span></span> <span data-ttu-id="364aa-200">이 매개 변수가 없으면 VM이 프로비전된 후 도메인 컨트롤러 서버를 기본 DNS 서버로 사용하도록 VM에서 IPv4 설정을 수동으로 설정하고 VM을 Active Directory 도메인에 가입시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-200">Without this parameter, you must manually set the IPv4 settings in your VM to use the domain controller server as the primary DNS server after the VM is provisioned, and then join the VM to the Active Directory domain.</span></span>
3. <span data-ttu-id="364aa-201">다음 파이프 명령을 실행하여 이름이 **ContosoSQL1** 및 **ContosoSQL2**인 SQL Server VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-201">Run the following piped commands to create the SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

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

    <span data-ttu-id="364aa-202">위의 명령과 관련하여 다음에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-202">Note the following regarding the commands above:</span></span>

   * <span data-ttu-id="364aa-203">**New-AzureVMConfig**는 도메인 컨트롤러 서버와 동일한 가용성 집합 이름을 사용하며 가상 컴퓨터 갤러리의 SQL Server 2012 서비스 팩 1 Enterprise Edition 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-203">**New-AzureVMConfig** uses the same availability set name as the domain controller server, and uses the SQL Server 2012 Service Pack 1 Enterprise Edition image in the virtual machine gallery.</span></span> <span data-ttu-id="364aa-204">또한 운영 체제 디스크를 읽기 캐싱 전용(쓰기 캐싱 없음)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-204">It also sets the operating system disk to read-caching only (no write caching).</span></span> <span data-ttu-id="364aa-205">VM에 연결한 별도의 데이터 디스크에 데이터베이스 파일을 마이그레이션하고 읽기 또는 쓰기 캐싱 없이 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-205">We recommend that you migrate the database files to a separate data disk that you attach to the VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="364aa-206">그러나 운영 체제 디스크에서는 읽기 캐싱을 제거할 수 없으므로 운영 체제 디스크에서 쓰기 캐싱을 제거하는 것이 차선책입니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-206">However, the next best thing is to remove write caching on the operating system disk because you can't remove read caching on the operating system disk.</span></span>
   * <span data-ttu-id="364aa-207">**Add-AzureProvisioningConfig**는 VM을 사용자가 만든 Active Directory 도메인에 가입시킵니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-207">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="364aa-208">**Set-AzureSubnet**은 백 서브넷에 VM을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-208">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="364aa-209">**Add-AzureEndpoint**는 클라이언트 응용 프로그램이 인터넷의 SQL Server 서비스 인스턴스에 액세스할 수 있도록 액세스 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on the Internet.</span></span> <span data-ttu-id="364aa-210">ContosoSQL1 및 ContosoSQL2에 다른 포트가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-210">Different ports are given to ContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="364aa-211">**New-AzureVM** 은 ContosoQuorum과 동일한 클라우드 서비스에 새 SQL Server VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-211">**New-AzureVM** creates the new SQL Server VM in the same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="364aa-212">VM을 동일한 가용성 집합에 포함하려면 동일한 클라우드 서비스에 VM을 배치해야 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-212">You must place the VMs in the same cloud service if you want them to be in the same availability set.</span></span>
4. <span data-ttu-id="364aa-213">각 VM이 완전히 프로비전되고 각 VM이 작업 디렉터리에 원격 데스크톱 파일을 다운로드할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-213">Wait for each VM to be fully provisioned and for each VM to download its remote desktop file to your working directory.</span></span> <span data-ttu-id="364aa-214">`for` 루프가 3개의 새 VM을 순환하고 각 VM에 대해 최상위 중괄호 안의 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-214">The `for` loop cycles through the three new VMs and executes the commands inside the top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until the VM status is "ReadyRole"
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

    <span data-ttu-id="364aa-215">SQL Server VM이 프로비전되어 실행 중이지만 기본 옵션으로 SQL Server가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-215">The SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-the-failover-cluster-vms"></a><span data-ttu-id="364aa-216">장애 조치(Failover) 클러스터 VM 초기화</span><span class="sxs-lookup"><span data-stu-id="364aa-216">Initialize the failover cluster VMs</span></span>
<span data-ttu-id="364aa-217">이 섹션에서는 장애 조치(Failover) 클러스터 및 SQL Server 설치에 사용할 3개의 서버를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-217">In this section, you need to modify the three servers that you'll use in the failover cluster and the SQL Server installation.</span></span> <span data-ttu-id="364aa-218">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-218">Specifically:</span></span>

* <span data-ttu-id="364aa-219">모든 서버: **장애 조치(Failover) 클러스터링** 기능을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-219">All servers: You need to install the **Failover Clustering** feature.</span></span>
* <span data-ttu-id="364aa-220">모든 서버: **CORP\Install**을 컴퓨터 **관리자**로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-220">All servers: You need to add **CORP\Install** as the machine **administrator**.</span></span>
* <span data-ttu-id="364aa-221">ContosoSQL1 및 ContosoSQL2만 해당: 기본 데이터베이스에서 **CORP\Install**을 **sysadmin** 역할로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-221">ContosoSQL1 and ContosoSQL2 only: You need to add **CORP\Install** as a **sysadmin** role in the default database.</span></span>
* <span data-ttu-id="364aa-222">ContosoSQL1 및 ContosoSQL2만 해당: **NT AUTHORITY\System**을 다음 권한이 있는 로그인으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-222">ContosoSQL1 and ContosoSQL2 only: You need to add **NT AUTHORITY\System** as a sign-in with the following permissions:</span></span>

  * <span data-ttu-id="364aa-223">가용성 그룹 변경</span><span class="sxs-lookup"><span data-stu-id="364aa-223">Alter any availability group</span></span>
  * <span data-ttu-id="364aa-224">SQL 연결</span><span class="sxs-lookup"><span data-stu-id="364aa-224">Connect SQL</span></span>
  * <span data-ttu-id="364aa-225">서버 상태 보기</span><span class="sxs-lookup"><span data-stu-id="364aa-225">View server state</span></span>
* <span data-ttu-id="364aa-226">ContosoSQL1 및 ContosoSQL2만 해당: **TCP** 프로토콜은 이미 SQL Server VM에서 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-226">ContosoSQL1 and ContosoSQL2 only: The **TCP** protocol is already enabled on the SQL Server VM.</span></span> <span data-ttu-id="364aa-227">그래도 SQL Server의 원격 액세스를 위해 방화벽을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-227">However, you still need to open the firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="364aa-228">이제 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-228">Now, you're ready to start.</span></span> <span data-ttu-id="364aa-229">**ContosoQuorum**부터 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-229">Beginning with **ContosoQuorum**, follow the steps below:</span></span>

1. <span data-ttu-id="364aa-230">원격 데스크톱 파일을 실행하여 **ContosoQuorum** 에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-230">Connect to **ContosoQuorum** by launching the remote desktop files.</span></span> <span data-ttu-id="364aa-231">VM을 만들 때 지정한 컴퓨터 관리자의 사용자 이름 **AzureAdmin**과 암호 **Contoso!000**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-231">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="364aa-232">컴퓨터가 **corp.contoso.com**에 성공적으로 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-232">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="364aa-233">계속하기 전에 SQL Server 설치가 자동 초기화 작업 실행을 마칠 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-233">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="364aa-234">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="364aa-235">Windows 장애 조치 클러스터링 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-235">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="364aa-236">**CORP\Install**을 로컬 관리자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="364aa-237">ContosoQuorum에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="364aa-238">이제 이 서버에서는 작업을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="364aa-239">다음으로 **ContosoSQL1** 및 **ContosoSQL2**를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="364aa-240">아래 단계를 따릅니다. 이 절차는 SQL Server VM 모두에 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-240">Follow the steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="364aa-241">원격 데스크톱 파일을 실행하여두 SQL Server VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-241">Connect to the two SQL Server VMs by launching the remote desktop files.</span></span> <span data-ttu-id="364aa-242">VM을 만들 때 지정한 컴퓨터 관리자의 사용자 이름 **AzureAdmin**과 암호 **Contoso!000**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-242">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="364aa-243">컴퓨터가 **corp.contoso.com**에 성공적으로 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-243">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="364aa-244">계속하기 전에 SQL Server 설치가 자동 초기화 작업 실행을 마칠 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-244">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="364aa-245">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="364aa-246">Windows 장애 조치 클러스터링 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-246">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="364aa-247">**CORP\Install**을 로컬 관리자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="364aa-248">SQL Server PowerShell 공급자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-248">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="364aa-249">기본 SQL Server 인스턴스에 sysadmin 역할로 **CORP\Install**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-249">Add **CORP\Install** as the sysadmin role for the default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="364aa-250">위에서 설명한 3개의 권한이 있는 로그인으로 **NT AUTHORITY\System**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-250">Add **NT AUTHORITY\System** as a sign-in with the three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="364aa-251">SQL Server의 원격 액세스를 위해 방화벽을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-251">Open the firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="364aa-252">두 VM에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="364aa-253">마지막으로 가용성 그룹을 구성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-253">Finally, you're ready to configure the availability group.</span></span> <span data-ttu-id="364aa-254">SQL Server PowerShell 공급자를 사용하여 **ContosoSQL1**에서 모든 작업을 수행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-254">You'll use the SQL Server PowerShell Provider to perform all of the work on **ContosoSQL1**.</span></span>

## <a name="configure-the-availability-group"></a><span data-ttu-id="364aa-255">가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="364aa-255">Configure the availability group</span></span>
1. <span data-ttu-id="364aa-256">원격 데스크톱 파일을 실행하여 **ContosoSQL1** 에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-256">Connect to **ContosoSQL1** again by launching the remote desktop files.</span></span> <span data-ttu-id="364aa-257">컴퓨터 계정을 사용하여 로그인하는 대신 **CORP\Install**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-257">Instead of signing in by using the machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="364aa-258">관리자 모드에서 PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="364aa-259">다음 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-259">Define the following variables:</span></span>

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
4. <span data-ttu-id="364aa-260">SQL Server PowerShell 공급자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-260">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="364aa-261">ContosoSQL1의 SQL Server 서비스 계정을 CORP\SQLSvc1로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-261">Change the SQL Server service account for ContosoSQL1 to CORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="364aa-262">ContosoSQL2의 SQL Server 서비스 계정을 CORP\SQLSvc2로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-262">Change the SQL Server service account for ContosoSQL2 to CORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="364aa-263">**Azure VM에서 Always On 가용성 그룹을 위한 장애 조치 클러스터 만들기** 에서 [CreateAzureFailoverCluster.ps1](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) 을 로컬 작업 디렉터리로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) to the local working directory.</span></span> <span data-ttu-id="364aa-264">이 스크립트를 사용하면 작동 가능한 장애 조치(Failover) 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-264">You'll use this script to help you create a functional failover cluster.</span></span> <span data-ttu-id="364aa-265">Windows 장애 조치(Failover) 클러스터링이 Azure 네트워크와 상호 작용하는 방식에 대한 중요 정보는 [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364aa-265">For important information on how Windows Failover Clustering interacts with the Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="364aa-266">작업 디렉터리로 변경하고 다운로드한 스크립트로 장애 조치 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-266">Change to your working directory and create the failover cluster with the downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="364aa-267">**ContosoSQL1** 및 **ContosoSQL2**의 기본 SQL Server 인스턴스에 대해 Always On 가용성 그룹을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-267">Enable Always On availability groups for the default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

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
10. <span data-ttu-id="364aa-268">백업 디렉터리를 만들고 SQL Server 서비스 계정에 대한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-268">Create a backup directory and grant permissions for the SQL Server service accounts.</span></span> <span data-ttu-id="364aa-269">보조 복제본에서 가용성 데이터베이스를 준비할 때 이 디렉터리를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-269">You'll use this directory to prepare the availability database on the secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="364aa-270">**ContosoSQL1**에 이름이 **MyDB1**인 데이터베이스를 만들고 전체 백업과 로그 백업을 모두 만든 다음 **WITH NORECOVERY** 옵션을 사용하여 해당 백업을 **ContosoSQL2**에 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with the **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="364aa-271">SQL Server VM에 가용성 그룹 끝점을 만들고 끝점에 적합한 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-271">Create the availability group endpoints on the SQL Server VMs and set the proper permissions on the endpoints.</span></span>

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
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct1]" -ServerInstance $server2
13. <span data-ttu-id="364aa-272">가용성 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-272">Create the availability replicas.</span></span>

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
14. <span data-ttu-id="364aa-273">마지막으로, 가용성 그룹을 만들고 보조 복제본을 가용성 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-273">Finally, create the availability group and join the secondary replica to the availability group.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="364aa-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="364aa-274">Next steps</span></span>
<span data-ttu-id="364aa-275">이제 Azure에서 가용성 그룹을 만들어 SQL Server Always On을 성공적으로 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="364aa-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="364aa-276">이 가용성 그룹에 대한 수신기를 구성하려면 [Azure에서 Always On 가용성 그룹에 대한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364aa-276">To configure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="364aa-277">Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364aa-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
