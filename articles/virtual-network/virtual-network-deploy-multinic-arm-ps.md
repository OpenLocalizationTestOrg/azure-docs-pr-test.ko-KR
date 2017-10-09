---
title: "여러 Nic-Azure PowerShell을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate PowerShell을 사용 하 여 여러 Nic 사용 하 여 VM입니다."
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
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="ba914-103">PowerShell을 사용하여 다중 NIC이 있는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ba914-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba914-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba914-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="ba914-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ba914-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="ba914-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="ba914-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="ba914-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="ba914-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="ba914-108">Azure CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="ba914-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ba914-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ba914-110">사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](virtual-network-deploy-multinic-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="ba914-111">hello 다음 단계 사용 하 여 명명 된 리소스 그룹 *IaaSStory* hello 웹 서버 및 리소스 그룹에 대 한 명명 된 *IaaSStory 백 엔드* hello DB 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba914-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ba914-112">Prerequisites</span></span>
<span data-ttu-id="ba914-113">Hello DB 서버를 만들려면 먼저 toocreate hello *IaaSStory* 이 시나리오에 대 한 모든 hello 필요한 리소스의 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="ba914-114">이러한 리소스를 완료 하는 toocreate hello 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="ba914-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="ba914-115">너무 이동[hello 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="ba914-116">Hello 템플릿 페이지의 오른쪽 toohello **부모 리소스 그룹**, 클릭 **tooAzure 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="ba914-117">필요한 경우 hello 매개 변수 값을를 변경한 다음 hello Azure preview 포털 toodeploy hello 리소스 그룹의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba914-118">저장소 계정 이름이 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="ba914-119">Azure에서 중복된 저장소 계정 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="ba914-120">Hello 백 엔드 Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="ba914-120">Create hello back-end VMs</span></span>
<span data-ttu-id="ba914-121">hello 백 엔드 Vm hello 생성의 다음 리소스는 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="ba914-122">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="ba914-122">**Storage account for data disks**.</span></span> <span data-ttu-id="ba914-123">성능 향상을 위해 hello 데이터베이스 서버에 데이터 디스크 hello 프리미엄 저장소 계정을 사용 해야 하는 반도체 드라이브 (SSD) 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="ba914-124">있는지 hello toosupport 프리미엄 저장소를 배포 하는 Azure 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="ba914-125">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="ba914-125">**NICs**.</span></span> <span data-ttu-id="ba914-126">각 VM에 데이터베이스 액세스용으로 하나, 그리고 관리용으로 하나씩, 두 개의 NIC가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="ba914-127">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="ba914-127">**Availability set**.</span></span> <span data-ttu-id="ba914-128">모든 데이터베이스 서버를 추가할 tooa 단일 가용성 집합, tooensure hello Vm 중 하나 이상이 실행 되 고 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="ba914-129">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="ba914-129">Step 1 - Start your script</span></span>
<span data-ttu-id="ba914-130">Hello 사용 되는 전체 PowerShell 스크립트를 다운로드할 수 있습니다 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="ba914-131">사용자 환경에서 toochange hello 스크립트 toowork 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="ba914-132">Hello에 위의 배포 된 기존 리소스 그룹에 따라 hello 변수 값 변경 [필수 구성 요소](#Prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="ba914-133">Hello 값을 변경 hello 값을 기반으로 hello 변수 원하는 toouse 백 엔드 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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
3. <span data-ttu-id="ba914-134">배포에 필요한 hello 기존 리소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="ba914-135">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="ba914-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="ba914-136">Toocreate hello 데이터 디스크에 대 한 저장소 계정 새 리소스 그룹 및 모든 Vm에 대 한 가용성 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="ba914-137">Alos hello 로컬 관리자 계정 자격 증명에 필요한 각 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="ba914-138">toocreate 이러한 리소스를 실행한 다음 단계 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="ba914-139">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="ba914-140">위에서 만든 hello 리소스 그룹에 새로운 프리미엄 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="ba914-141">새 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="ba914-142">로컬 관리자에 게 각 VM에 사용 되는 계정 자격 증명 toobe를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="ba914-143">3 단계-hello Nic와 백 엔드 Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="ba914-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="ba914-144">처럼 많은 Vm을 하 고 만들 때 hello 필요한 Nic 및 Vm hello 루프 내 루프 toocreate toouse가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="ba914-145">toocreate hello Nic Vm에 단계를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="ba914-146">시작 된 `for` 루프 toorepeat hello 명령을 toocreate VM 한 두 개의 nic가 필요에 따라 여러 번의 hello hello 값에 기반 `$numberOfVMs` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="ba914-147">데이터베이스 액세스에 사용 되는 NIC hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="ba914-148">원격 액세스에 사용 되는 NIC hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="ba914-149">어떻게이 NIC에 NSG 연결 tooit 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="ba914-150">`vmConfig` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="ba914-151">VM 당 두 개의 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-151">Create two data disks per VM.</span></span> <span data-ttu-id="ba914-152">Hello 데이터 디스크 앞에서 만든 hello 프리미엄 저장소 계정에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

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

6. <span data-ttu-id="ba914-153">Hello 운영 체제 및 hello VM에 사용 되는 이미지 toobe 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="ba914-154">Hello 두 Nic toohello 위에서 만든 추가 `vmConfig` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="ba914-155">Hello OS 디스크를 만들고 hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="ba914-156">공지 hello `}` hello 종료 `for` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="ba914-157">4 단계-실행 hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="ba914-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="ba914-158">다운로드 하 고 변경 했으므로 hello 스크립트 toocreate hello 백 엔드 데이터베이스 여러 Nic 포함 하는 Vm을 스크립트 그 아니다를 요구 사항에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="ba914-159">스크립트를 저장 하 고 hello에서 실행 **PowerShell** 명령 프롬프트 또는 **PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="ba914-160">Hello 초기 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="ba914-161">몇 분 후 hello 자격 증명 프롬프트 및 입력 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="ba914-162">아래의 hello 출력 단일 VM을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-162">hello output below represents a single VM.</span></span> <span data-ttu-id="ba914-163">공지 hello 전체 프로세스 8 분 toocomplete를 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="ba914-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

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
