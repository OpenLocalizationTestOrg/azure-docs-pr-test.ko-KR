---
title: "다중 NIC가 있는 VM(클래식) 만들기 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 1.0을 사용하여 다중 NIC가 있는 VM(클래식)을 만드는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b62421b7289650818748d0016dccfdf42ef0a768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="41dca-103">Azure CLI 1.0을 사용하여 다중 NIC가 있는 VM(클래식) 만들기</span><span class="sxs-lookup"><span data-stu-id="41dca-103">Create a VM (Classic) with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="41dca-104">Azure에서 VM(가상 컴퓨터)을 만들고 각 VM에 여러 NIC(네트워크 인터페이스)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="41dca-105">여러 NIC를 사용하면 NIC 간에 트래픽 유형을 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="41dca-106">예를 들어 하나의 NIC는 인터넷과 통신하는 동안 다른 NIC는 인터넷에 연결되지 않은 내부 리소스와만 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="41dca-107">여러 NIC 간에 네트워크 트래픽을 분리하는 기능은 응용 프로그램 전달 및 WAN 최적화 솔루션과 같은 많은 네트워크 가상 어플라이언스에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41dca-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="41dca-109">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="41dca-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="41dca-111">[Resource Manager 배포 모델](virtual-network-deploy-multinic-arm-cli.md)을 사용하여 이러한 단계를 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="41dca-112">다음 단계에서는 WEB 서버에 *IaaSStory*라는 리소스 그룹을, DB 서버에 *IaaSStory-BackEnd*라는 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41dca-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41dca-113">Prerequisites</span></span>
<span data-ttu-id="41dca-114">DB 서버를 만들려면 먼저 이 시나리오에 필요한 모든 리소스로 *IaaSStory* 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="41dca-115">이러한 리소스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="41dca-116">[가상 네트워크 만들기](virtual-networks-create-vnet-classic-cli.md) 문서에 나오는 단계를 따라 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-the-back-end-vms"></a><span data-ttu-id="41dca-117">백 엔드 VM 배포</span><span class="sxs-lookup"><span data-stu-id="41dca-117">Deploy the back-end VMs</span></span>
<span data-ttu-id="41dca-118">백 엔드 VM은 만드는 리소스에 따라 다음과 같이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="41dca-119">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="41dca-119">**Storage account for data disks**.</span></span> <span data-ttu-id="41dca-120">성능 향상을 위해 데이터베이스 서버의 데이터 디스크는 SSD(반도체 드라이브) 기술을 사용하며, 이 기술에는 프리미엄 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-120">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="41dca-121">배포할 Azure 위치에서 프리미엄 저장소가 지원되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="41dca-121">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="41dca-122">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="41dca-122">**NICs**.</span></span> <span data-ttu-id="41dca-123">각 VM에 데이터베이스 액세스용으로 하나, 그리고 관리용으로 하나씩, 두 개의 NIC가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="41dca-124">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="41dca-124">**Availability set**.</span></span> <span data-ttu-id="41dca-125">모든 데이터베이스 서버가 단일 가용성 집합에 추가되어, 유지 관리 도중에 하나 이상의 VM이 실행 중이도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-125">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="41dca-126">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="41dca-126">Step 1 - Start your script</span></span>
<span data-ttu-id="41dca-127">사용되는 전체 bash 스크립트를 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-127">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="41dca-128">다음 단계에 완료하여 스크립트가 사용자 환경에서 작동하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-128">Complete the following steps to change the script to work in your environment:</span></span>

1. <span data-ttu-id="41dca-129">위의 [필수 조건](#Prerequisites)에서 배포한 기존 리소스 그룹을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-129">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="41dca-130">백 엔드 배포에 사용하려는 값을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-130">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="41dca-131">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="41dca-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="41dca-132">모든 백 엔드 VM에 대해 새 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="41dca-133">리소스 그룹 이름에 `$backendCSName` 변수가, Azure 지역에 대해서는 `$location`이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-133">Notice the use of the `$backendCSName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="41dca-134">VM에서 사용할 OS 및 데이터 디스크에 대해 프리미엄 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-134">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="41dca-135">3단계 - 여러 NIC를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="41dca-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="41dca-136">`numberOfVMs` 변수를 기반으로 하여 여러 VM을 만드는 루프를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-136">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="41dca-137">각 VM에 대해 NIC 두 개의 이름과 IP 주소를 각각 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-137">For each VM, specify the name and IP address of each of the two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="41dca-138">VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-138">Create the VM.</span></span> <span data-ttu-id="41dca-139">이름, 서브넷, IP 주소와 함께 모든 NIC 목록을 포함하는 `--nic-config` 매개 변수 사용에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-139">Notice the usage of the `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="41dca-140">각 VM에 대해 두 개의 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="41dca-141">4단계 - 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="41dca-141">Step 4 - Run the script</span></span>
<span data-ttu-id="41dca-142">스크립트를 다운로드하여 요구에 맞게 변경했으므로, 이제 이 스크립트를 실행하여 여러 NIC를 사용하여 백 엔드 데이터베이스 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-142">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="41dca-143">스크립트를 저장하고 **Bash** 터미널에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="41dca-144">아래와 같이 초기 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-144">You will see the initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="41dca-145">몇 분 후에 실행이 종료되고 아래와 같이 출력의 나머지 부분이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dca-145">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
