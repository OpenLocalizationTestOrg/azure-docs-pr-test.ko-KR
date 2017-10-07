---
title: "여러 Nic-Azure PowerShell을 사용 하 여 VM (클래식) aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate PowerShell을 사용 하 여 여러 Nic 사용 하 여 VM (클래식)."
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
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="2f74e-103">PowerShell을 사용하여 다중 NIC이 있는 VM(클래식) 만들기</span><span class="sxs-lookup"><span data-stu-id="2f74e-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="2f74e-104">Azure에서 가상 컴퓨터 (Vm)를 만들고 Vm의 여러 네트워크 인터페이스 (Nic) tooeach 첨부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="2f74e-105">여러 NIC를 사용하면 NIC 간에 트래픽 유형을 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="2f74e-106">예를 들어 toohello 인터넷에 연결 되어 있지 내부 리소스와만 통신 다른 동안 NIC 인터넷 hello와 통신할 수 있는 하나.</span><span class="sxs-lookup"><span data-stu-id="2f74e-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="2f74e-107">여러 Nic에 걸쳐 hello 기능 tooseparate 네트워크 트래픽을 응용 프로그램을 배달 및 WAN 최적화 솔루션 등에 많은 네트워크 가상 어플라이언스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f74e-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2f74e-109">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="2f74e-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2f74e-111">자세한 내용은 방법 tooperform hello를 사용 하 여 이러한 단계 [리소스 관리자 배포 모델](virtual-network-deploy-multinic-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="2f74e-112">hello 다음 단계 사용 하 여 명명 된 리소스 그룹 *IaaSStory* hello 웹 서버 및 리소스 그룹에 대 한 명명 된 *IaaSStory 백 엔드* hello DB 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f74e-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2f74e-113">Prerequisites</span></span>

<span data-ttu-id="2f74e-114">Hello DB 서버를 만들려면 먼저 toocreate hello *IaaSStory* 이 시나리오에 대 한 모든 hello 필요한 리소스의 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="2f74e-115">이러한 리소스를 전체 hello 수행 하는 단계는 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="2f74e-116">Hello hello 단계를 수행 하 여 가상 네트워크 만들기 [가상 네트워크 만들기](virtual-networks-create-vnet-classic-netcfg-ps.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="2f74e-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="2f74e-117">Hello 백 엔드 Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="2f74e-117">Create hello back-end VMs</span></span>
<span data-ttu-id="2f74e-118">hello 백 엔드 Vm hello 생성의 다음 리소스는 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="2f74e-119">**백 엔드 서브넷**.</span><span class="sxs-lookup"><span data-stu-id="2f74e-119">**Backend subnet**.</span></span> <span data-ttu-id="2f74e-120">hello 데이터베이스 서버는 별도 서브넷 toosegregate 트래픽의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="2f74e-121">아래의 hello 스크립트 라는 vnet에이 서브넷 tooexist 리라 전망 *WTestVnet*합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="2f74e-122">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="2f74e-122">**Storage account for data disks**.</span></span> <span data-ttu-id="2f74e-123">성능 향상을 위해 hello 데이터베이스 서버에 데이터 디스크 hello 프리미엄 저장소 계정을 사용 해야 하는 반도체 드라이브 (SSD) 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="2f74e-124">있는지 hello toosupport 프리미엄 저장소를 배포 하는 Azure 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="2f74e-125">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="2f74e-125">**Availability set**.</span></span> <span data-ttu-id="2f74e-126">모든 데이터베이스 서버를 추가할 tooa 단일 가용성 집합, tooensure hello Vm 중 하나 이상이 실행 되 고 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="2f74e-127">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="2f74e-127">Step 1 - Start your script</span></span>
<span data-ttu-id="2f74e-128">Hello 사용 되는 전체 PowerShell 스크립트를 다운로드할 수 있습니다 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="2f74e-129">사용자 환경에서 toochange hello 스크립트 toowork 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="2f74e-130">Hello에 위의 배포 된 기존 리소스 그룹에 따라 hello 변수 값 변경 [필수 구성 요소](#Prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="2f74e-131">Hello 값을 변경 hello 값을 기반으로 hello 변수 원하는 toouse 백 엔드 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="2f74e-132">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="2f74e-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="2f74e-133">모든 Vm에 대 한 hello 데이터 디스크에 대 한 새 클라우드 서비스와 저장소 계정 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="2f74e-134">또한 해야 toospecify 이미지 및 로컬 관리자 계정을 hello Vm에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="2f74e-135">이러한 리소스를 완료 하는 toocreate hello 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="2f74e-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="2f74e-136">새 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2f74e-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="2f74e-137">새 프리미엄 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2f74e-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="2f74e-138">구독에 대 한 현재 저장소 계정을 hello로 위에서 만든 집합 hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="2f74e-139">Hello VM에 대 한 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="2f74e-140">Hello 로컬 관리자 계정 자격 증명을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="2f74e-141">3단계: VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2f74e-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="2f74e-142">처럼 많은 Vm을 하 고 만들 때 hello 필요한 Nic 및 Vm hello 루프 내 루프 toocreate toouse가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="2f74e-143">toocreate hello Nic Vm에 단계를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="2f74e-144">시작 된 `for` 루프 toorepeat hello 명령을 toocreate VM 한 두 개의 nic가 필요에 따라 여러 번의 hello hello 값에 기반 `$numberOfVMs` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="2f74e-145">만들기는 `VMConfig` hello 이미지, 크기 및 가용성 hello VM에 대 한 집합을 지정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="2f74e-146">Windows VM으로 hello VM을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="2f74e-147">Hello 기본 NIC 설정 하 고 고정 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="2f74e-148">각 VM에 두 번째 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="2f74e-149">각 VM에 대 한 toodata 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-149">Create toodata disks for each VM.</span></span>

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

7. <span data-ttu-id="2f74e-150">각 VM 및 종료 hello 루프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="2f74e-151">4 단계-실행 hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="2f74e-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="2f74e-152">다운로드 하 고 변경 했으므로 hello 스크립트 toocreate hello 백 엔드 데이터베이스 여러 Nic 포함 하는 Vm을 스크립트 그 아니다를 요구 사항에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="2f74e-153">스크립트를 저장 하 고 hello에서 실행 **PowerShell** 명령 프롬프트 또는 **PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="2f74e-154">아래와 같이 hello 초기 출력에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="2f74e-155">필요한 자격 증명 프롬프트가 hello 및 클릭에서 hello 정보를 채울 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="2f74e-156">아래 hello 출력 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f74e-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
