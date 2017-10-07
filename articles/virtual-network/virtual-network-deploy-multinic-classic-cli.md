---
title: "여러 Nic-Azure CLI 1.0을 사용 하 여 VM (클래식) aaaCreate | Microsoft Docs"
description: "사용 하 여 여러 Nic 사용 하 여 VM (클래식) toocreate Azure CLI (명령줄 인터페이스) 1.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="5d4c5-103">Hello Azure CLI 1.0을 사용 하 여 여러 Nic를 포함 (클래식) VM 만들기</span><span class="sxs-lookup"><span data-stu-id="5d4c5-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="5d4c5-104">Azure에서 가상 컴퓨터 (Vm)를 만들고 Vm의 여러 네트워크 인터페이스 (Nic) tooeach 첨부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="5d4c5-105">여러 NIC를 사용하면 NIC 간에 트래픽 유형을 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="5d4c5-106">예를 들어 toohello 인터넷에 연결 되어 있지 내부 리소스와만 통신 다른 동안 NIC 인터넷 hello와 통신할 수 있는 하나.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="5d4c5-107">여러 Nic에 걸쳐 hello 기능 tooseparate 네트워크 트래픽을 응용 프로그램을 배달 및 WAN 최적화 솔루션 등에 많은 네트워크 가상 어플라이언스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d4c5-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5d4c5-109">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5d4c5-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5d4c5-111">자세한 내용은 방법 tooperform hello를 사용 하 여 이러한 단계 [리소스 관리자 배포 모델](virtual-network-deploy-multinic-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="5d4c5-112">hello 다음 단계 사용 하 여 명명 된 리소스 그룹 *IaaSStory* hello 웹 서버 및 리소스 그룹에 대 한 명명 된 *IaaSStory 백 엔드* hello DB 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d4c5-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5d4c5-113">Prerequisites</span></span>
<span data-ttu-id="5d4c5-114">Hello DB 서버를 만들려면 먼저 toocreate hello *IaaSStory* 이 시나리오에 대 한 모든 hello 필요한 리소스의 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="5d4c5-115">이러한 리소스를 전체 hello 수행 하는 단계는 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="5d4c5-116">Hello hello 단계를 수행 하 여 가상 네트워크 만들기 [가상 네트워크 만들기](virtual-networks-create-vnet-classic-cli.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="5d4c5-117">Hello 백 엔드 배포 Vm</span><span class="sxs-lookup"><span data-stu-id="5d4c5-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="5d4c5-118">hello 백 엔드 Vm hello 생성의 다음 리소스는 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="5d4c5-119">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-119">**Storage account for data disks**.</span></span> <span data-ttu-id="5d4c5-120">성능 향상을 위해 hello 데이터베이스 서버에 데이터 디스크 hello 프리미엄 저장소 계정을 사용 해야 하는 반도체 드라이브 (SSD) 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="5d4c5-121">있는지 hello toosupport 프리미엄 저장소를 배포 하는 Azure 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="5d4c5-122">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-122">**NICs**.</span></span> <span data-ttu-id="5d4c5-123">각 VM에 데이터베이스 액세스용으로 하나, 그리고 관리용으로 하나씩, 두 개의 NIC가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="5d4c5-124">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-124">**Availability set**.</span></span> <span data-ttu-id="5d4c5-125">모든 데이터베이스 서버를 추가할 tooa 단일 가용성 집합, tooensure hello Vm 중 하나 이상이 실행 되 고 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="5d4c5-126">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="5d4c5-126">Step 1 - Start your script</span></span>
<span data-ttu-id="5d4c5-127">사용 되는 hello 전체 bash 스크립트를 다운로드할 수 있습니다 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="5d4c5-128">Hello 단계 toochange hello 스크립트 toowork 사용자 환경에서 다음을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="5d4c5-129">Hello에 위의 배포 된 기존 리소스 그룹에 따라 hello 변수 값 변경 [필수 구성 요소](#Prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="5d4c5-130">Hello 값을 변경 hello 값을 기반으로 hello 변수 원하는 toouse 백 엔드 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="5d4c5-131">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="5d4c5-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="5d4c5-132">모든 백 엔드 VM에 대해 새 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="5d4c5-133">공지 hello 사용 hello `$backendCSName` hello 리소스 그룹 이름에 대 한 변수 및 `$location` hello Azure 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="5d4c5-134">OS hello에 대 한 프리미엄 저장소 계정 및 사용자 Vm에서 사용 하는 데이터 디스크 toobe를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="5d4c5-135">3단계 - 여러 NIC를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="5d4c5-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="5d4c5-136">루프 toocreate hello에 따라 여러 Vm을 시작 `numberOfVMs` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="5d4c5-137">각 VM에 대 한 hello 이름과 각 hello 두 Nic의 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="5d4c5-138">Hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-138">Create hello VM.</span></span> <span data-ttu-id="5d4c5-139">Hello의 hello 사용 확인 `--nic-config` 매개 변수를 이름, 서브넷 및 IP 주소에 있는 모든 Nic 목록이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

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

4. <span data-ttu-id="5d4c5-140">각 VM에 대해 두 개의 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="5d4c5-141">4 단계-실행 hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="5d4c5-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="5d4c5-142">다운로드 하 고 hello 스크립트 toocreate hello를 다시 실행 요구 사항에 따라 hello 스크립트를 변경 했으므로 여러 nic가 있는 데이터베이스 Vm을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="5d4c5-143">스크립트를 저장하고 **Bash** 터미널에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="5d4c5-144">아래와 같이 hello 초기 출력에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-144">You will see hello initial output, as shown below.</span></span>

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

2. <span data-ttu-id="5d4c5-145">몇 분 후 hello 실행이 종료 하 고 hello 나머지 hello 출력 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d4c5-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

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
