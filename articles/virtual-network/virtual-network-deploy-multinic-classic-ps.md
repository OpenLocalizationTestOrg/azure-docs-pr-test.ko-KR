---
title: "다중 NIC이 있는 VM(클래식) 만들기 - Azure PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 다중 NIC이 있는 VM(클래식)을 만드는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="52faa-103">PowerShell을 사용하여 다중 NIC이 있는 VM(클래식) 만들기</span><span class="sxs-lookup"><span data-stu-id="52faa-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="52faa-104">Azure에서 VM(가상 컴퓨터)을 만들고 각 VM에 여러 NIC(네트워크 인터페이스)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="52faa-105">여러 NIC를 사용하면 NIC 간에 트래픽 유형을 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="52faa-106">예를 들어 하나의 NIC는 인터넷과 통신하는 동안 다른 NIC는 인터넷에 연결되지 않은 내부 리소스와만 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="52faa-107">여러 NIC 간에 네트워크 트래픽을 분리하는 기능은 응용 프로그램 전달 및 WAN 최적화 솔루션과 같은 많은 네트워크 가상 어플라이언스에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52faa-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="52faa-109">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="52faa-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="52faa-111">[Resource Manager 배포 모델](virtual-network-deploy-multinic-arm-ps.md)을 사용하여 이러한 단계를 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="52faa-112">다음 단계에서는 WEB 서버에 *IaaSStory*라는 리소스 그룹을, DB 서버에 *IaaSStory-BackEnd*라는 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52faa-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="52faa-113">Prerequisites</span></span>

<span data-ttu-id="52faa-114">DB 서버를 만들려면 먼저 이 시나리오에 필요한 모든 리소스로 *IaaSStory* 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="52faa-115">이러한 리소스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="52faa-116">[가상 네트워크 만들기](virtual-networks-create-vnet-classic-netcfg-ps.md) 문서에 나오는 단계를 따라 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="52faa-117">백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="52faa-117">Create the back-end VMs</span></span>
<span data-ttu-id="52faa-118">백 엔드 VM은 만드는 리소스에 따라 다음과 같이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="52faa-119">**백 엔드 서브넷**.</span><span class="sxs-lookup"><span data-stu-id="52faa-119">**Backend subnet**.</span></span> <span data-ttu-id="52faa-120">트래픽을 격리하기 위해서 데이터베이스 서버는 별도의 서브넷에 속하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="52faa-121">아래 스크립트는 이 서브넷이 *WTestVnet*이라는 vnet에 존재한다고 추정합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="52faa-122">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="52faa-122">**Storage account for data disks**.</span></span> <span data-ttu-id="52faa-123">성능 향상을 위해 데이터베이스 서버의 데이터 디스크는 SSD(반도체 드라이브) 기술을 사용하며, 이 기술에는 프리미엄 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="52faa-124">배포할 Azure 위치에서 프리미엄 저장소가 지원되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="52faa-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="52faa-125">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="52faa-125">**Availability set**.</span></span> <span data-ttu-id="52faa-126">모든 데이터베이스 서버가 단일 가용성 집합에 추가되어, 유지 관리 도중에 하나 이상의 VM이 실행 중이도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="52faa-127">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="52faa-127">Step 1 - Start your script</span></span>
<span data-ttu-id="52faa-128">사용되는 전체 PowerShell 스크립트를 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="52faa-129">다음 단계에 따라 스크립트를 사용자 환경에서 작동하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="52faa-130">위의 [필수 조건](#Prerequisites)에서 배포한 기존 리소스 그룹을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="52faa-131">백 엔드 배포에 사용하려는 값을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="52faa-132">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="52faa-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="52faa-133">새로운 클라우드 서비스, 모든 VM에 대한 데이터 디스크의 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="52faa-134">VM에 대한 로컬 관리자 계정 및 이미지도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="52faa-135">이러한 리소스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="52faa-136">새 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="52faa-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="52faa-137">새 프리미엄 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="52faa-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="52faa-138">앞에서 만든 저장소 계정을 구독에 대한 현재 저장소 계정으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="52faa-139">VM에 대한 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="52faa-140">로컬 관리자 계정 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="52faa-141">3단계: VM 만들기</span><span class="sxs-lookup"><span data-stu-id="52faa-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="52faa-142">루프를 사용하여 VM을 원하는 개수만큼 만들고 루프 내에서 필요한 NIC와 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="52faa-143">NIC와 VM을 만들려면 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="52faa-144">`$numberOfVMs` 변수 값을 기반으로 필요한 횟수만큼 VM 1개와 NIC 2개를 만드는 명령을 반복하는 `for` 루프를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="52faa-145">VM의 이미지, 크기, 가용성 집합을 지정하는 `VMConfig` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="52faa-146">VM을 Windows VM으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="52faa-147">기본 NIC를 설정하여 고정 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="52faa-148">각 VM에 두 번째 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="52faa-149">각 VM에 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-149">Create to data disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="52faa-150">각 VM을 만들고 루프를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="52faa-151">4단계 - 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="52faa-151">Step 4 - Run the script</span></span>
<span data-ttu-id="52faa-152">스크립트를 다운로드하여 요구에 맞게 변경했으므로, 이제 이 스크립트를 실행하여 여러 NIC와 백 엔드 데이터베이스 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="52faa-153">스크립트를 저장하여 **PowerShell** 명령 프롬프트 또는 **PowerShell ISE**에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="52faa-154">아래와 같이 초기 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="52faa-155">자격 증명 프롬프트에 필요한 정보를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="52faa-156">다음 출력이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="52faa-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
