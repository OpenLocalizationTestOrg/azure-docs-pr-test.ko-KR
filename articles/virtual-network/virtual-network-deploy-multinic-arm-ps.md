---
title: "다중 NIC이 있는 VM 만들기 - Azure PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 다중 NIC이 있는 VM을 만드는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3a11afd8fbd6a5e6b94cf1ebee7ea20665421bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="adb7c-103">PowerShell을 사용하여 다중 NIC이 있는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="adb7c-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="adb7c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="adb7c-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="adb7c-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="adb7c-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="adb7c-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="adb7c-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="adb7c-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="adb7c-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="adb7c-108">Azure CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="adb7c-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="adb7c-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="adb7c-110">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](virtual-network-deploy-multinic-classic-ps.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="adb7c-111">다음 단계에서는 WEB 서버에 *IaaSStory*라는 리소스 그룹을, DB 서버에 *IaaSStory-BackEnd*라는 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-111">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adb7c-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="adb7c-112">Prerequisites</span></span>
<span data-ttu-id="adb7c-113">DB 서버를 만들려면 먼저 이 시나리오에 필요한 모든 리소스로 *IaaSStory* 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-113">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="adb7c-114">이러한 리소스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-114">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="adb7c-115">[템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-115">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="adb7c-116">템플릿 페이지에서 **Parent resource group(부모 리소스 그룹)** 오른쪽에 있는 **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-116">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="adb7c-117">필요한 경우 매개 변수 값을 변경한 다음 Azure Preview 포털의 단계에 따라 리소스 그룹을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-117">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adb7c-118">저장소 계정 이름이 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="adb7c-119">Azure에서 중복된 저장소 계정 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="adb7c-120">백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="adb7c-120">Create the back-end VMs</span></span>
<span data-ttu-id="adb7c-121">백 엔드 VM은 만드는 리소스에 따라 다음과 같이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-121">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="adb7c-122">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-122">**Storage account for data disks**.</span></span> <span data-ttu-id="adb7c-123">성능 향상을 위해 데이터베이스 서버의 데이터 디스크는 SSD(반도체 드라이브) 기술을 사용하며, 이 기술에는 프리미엄 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="adb7c-124">배포할 Azure 위치에서 프리미엄 저장소가 지원되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="adb7c-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="adb7c-125">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-125">**NICs**.</span></span> <span data-ttu-id="adb7c-126">각 VM에 데이터베이스 액세스용으로 하나, 그리고 관리용으로 하나씩, 두 개의 NIC가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="adb7c-127">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-127">**Availability set**.</span></span> <span data-ttu-id="adb7c-128">모든 데이터베이스 서버가 단일 가용성 집합에 추가되어, 유지 관리 도중에 하나 이상의 VM이 실행 중이도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-128">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="adb7c-129">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="adb7c-129">Step 1 - Start your script</span></span>
<span data-ttu-id="adb7c-130">사용되는 전체 PowerShell 스크립트를 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-130">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="adb7c-131">다음 단계에 따라 스크립트를 사용자 환경에서 작동하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-131">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="adb7c-132">위의 [필수 조건](#Prerequisites)에서 배포한 기존 리소스 그룹을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-132">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="adb7c-133">백 엔드 배포에 사용하려는 값을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-133">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="adb7c-134">배포에 필요한 기존 리소스를 찾아옵니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-134">Retrieve the existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="adb7c-135">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="adb7c-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="adb7c-136">새로운 리소스 그룹, 데이터 디스크의 저장소 계정, 모든 VM에 대한 가용성 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-136">You need to create a new resource group, a storage account for the data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="adb7c-137">각 VM에 대한 로컬 관리자 계정 자격 증명도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-137">You alos need the local administrator account credentials for each VM.</span></span> <span data-ttu-id="adb7c-138">이러한 리소스를 만들려면 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-138">To create these resources, execute the following steps.</span></span>

1. <span data-ttu-id="adb7c-139">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="adb7c-140">위에서 만든 리소스 그룹에 프리미엄 저장소 계정을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-140">Create a new premium storage account in the resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="adb7c-141">새 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="adb7c-142">각 VM에 사용될 로컬 관리자 계정 자격 증명을 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-142">Get the local administrator account credentials to be used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="adb7c-143">3단계 - NIC 및 백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="adb7c-143">Step 3 - Create the NICs and back-end VMs</span></span>
<span data-ttu-id="adb7c-144">루프를 사용하여 VM을 원하는 개수만큼 만들고 루프 내에서 필요한 NIC와 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-144">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="adb7c-145">NIC와 VM을 만들려면 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-145">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="adb7c-146">`$numberOfVMs` 변수 값을 기반으로 필요한 횟수만큼 VM 1개와 NIC 2개를 만드는 명령을 반복하는 `for` 루프를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-146">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="adb7c-147">데이터베이스 액세스에 사용되는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-147">Create the NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="adb7c-148">원격 액세스에 사용되는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-148">Create the NIC used for remote access.</span></span> <span data-ttu-id="adb7c-149">NIC에 NSG가 연결되는 방법에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-149">Notice how this NIC has an NSG associated to it.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="adb7c-150">`vmConfig` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="adb7c-151">VM 당 두 개의 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-151">Create two data disks per VM.</span></span> <span data-ttu-id="adb7c-152">데이터 디스크는 앞에서 만든 프리미엄 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-152">Notice that the data disks are in the premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="adb7c-153">운영 체제와 VM에 사용될 이미지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-153">Configure the operating system, and image to be used for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="adb7c-154">위에서 만든 NIC 2개를 `vmConfig` 개체에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-154">Add the two NICs created above to the `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="adb7c-155">OS 디스크를 만들고 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-155">Create the OS disk and create the VM.</span></span> <span data-ttu-id="adb7c-156">`}` 기호는 `for` 루프를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-156">Notice the `}` ending the `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="adb7c-157">4단계 - 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="adb7c-157">Step 4 - Run the script</span></span>
<span data-ttu-id="adb7c-158">스크립트를 다운로드하여 요구에 맞게 변경했으므로, 이제 이 스크립트를 실행하여 여러 NIC와 백 엔드 데이터베이스 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-158">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="adb7c-159">스크립트를 저장하여 **PowerShell** 명령 프롬프트 또는 **PowerShell ISE**에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-159">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="adb7c-160">아래와 같이 초기 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-160">You will see the initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="adb7c-161">몇 분 후에 자격 증명 프롬프트에 정보를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-161">After a few minutes, fill out the credentials prompt and click **OK**.</span></span> <span data-ttu-id="adb7c-162">아래 출력은 단일 VM을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-162">The output below represents a single VM.</span></span> <span data-ttu-id="adb7c-163">전체 프로세스를 완료하는 데 8분이 소요되었습니다.</span><span class="sxs-lookup"><span data-stu-id="adb7c-163">Notice the entire process took 8 minutes to complete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
