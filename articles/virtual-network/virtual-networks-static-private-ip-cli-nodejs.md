---
title: "Vm-Azure CLI 1.0에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터에 대 한 Azure CLI (명령줄 인터페이스) 1.0 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="d0e4e-103">Hello Azure CLI 1.0을 사용 하 여 가상 컴퓨터에 대 한 개인 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d0e4e-104">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="d0e4e-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="d0e4e-105">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="d0e4e-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="d0e4e-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d0e4e-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -hello 리소스 관리 배포 모델에 대 한 우리의 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="d0e4e-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d0e4e-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d0e4e-109">수도 있습니다 [hello 클래식 배포 모델에 개인 고정 IP 주소 관리](virtual-networks-static-private-ip-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="d0e4e-110">hello 샘플 Azure CLI 명령 아래에 이미 만든 단순한 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="d0e4e-111">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="d0e4e-112">어떻게 toospecify 정적 개인 IP 주소는 VM을 만들 때</span><span class="sxs-lookup"><span data-stu-id="d0e4e-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="d0e4e-113">toocreate 라는 VM *DNS01* hello에 *프런트 엔드* 라는 VNet의 서브넷 *TestVNet* 의 정적 개인 ip *192.168.1.101*, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="d0e4e-114">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d0e4e-115">Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="d0e4e-116">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="d0e4e-117">Hello 실행 **azure 네트워크 공용 ip 만들기** toocreate hello VM에 대 한 공용 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="d0e4e-118">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="d0e4e-119">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="d0e4e-120">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="d0e4e-121">Hello hello 공용 IP 리소스 그룹의 이름에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="d0e4e-122">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-122">**-n (or --name)**.</span></span> <span data-ttu-id="d0e4e-123">Hello 공용 IP의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="d0e4e-124">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-124">**-l (or --location)**.</span></span> <span data-ttu-id="d0e4e-125">Azure 지역 hello 공용 IP 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="d0e4e-126">이 시나리오에서는 *centralus*입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="d0e4e-127">Hello 실행 **azure 네트워크 nic 만들기** 명령 toocreate 정적 개인 IP와 NIC 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="d0e4e-128">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="d0e4e-129">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="d0e4e-130">**-a(또는 --private-ip-address)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="d0e4e-131">NIC. hello에 대 한 정적 개인 IP 주소</span><span class="sxs-lookup"><span data-stu-id="d0e4e-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="d0e4e-132">**-m(또는 --subnet-vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="d0e4e-133">Hello hello NIC를 만들 위치는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="d0e4e-134">**-k(또는 --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="d0e4e-135">Hello NIC를 만들 위치 hello 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="d0e4e-136">Hello 실행 **azure vm 만들기** hello 공용 IP와 NIC를 사용 하 여 VM 위에서 만든 명령 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="d0e4e-137">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="d0e4e-138">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="d0e4e-139">**-y(또는 --os-type)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="d0e4e-140">형식의 하거나 VM hello에 대 한 시스템 운영 *Windows* 또는 *Linux*합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="d0e4e-141">**-f(또는 --nic-name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="d0e4e-142">Hello NIC hello VM의 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="d0e4e-143">**-i(또는 --public-ip-name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="d0e4e-144">Hello 공용 IP hello VM의 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="d0e4e-145">**-F(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="d0e4e-146">Hello hello VM을 만들 위치는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="d0e4e-147">**-j(또는 --vnet-subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="d0e4e-148">Hello VM 만들어지는 hello 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="d0e4e-149">어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="d0e4e-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="d0e4e-150">tooview hello 정적 개인 IP 주소 VM hello 다음 Azure CLI 명령을 실행 합니다. 위의 hello 스크립트를 사용 하 여 만든 hello에 대 한 정보 및 hello에 대 한 값이 확인 *개인 IP 할당 메서드* 및 *개인IP주소*:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="d0e4e-151">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="d0e4e-152">어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다</span><span class="sxs-lookup"><span data-stu-id="d0e4e-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="d0e4e-153">리소스 관리자에 대한 Azure CLI의 NIC에서는 정적 개인 IP 주소를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="d0e4e-154">동적 IP를 사용 하 여 새 NIC를 만들고, 제거 해야 hello hello VM에서에서 NIC를 이전 및 다음 hello 새 NIC toohello VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="d0e4e-155">toochange 위의 명령은 hello 사용 되는 VM int eh에 대 한 NIC hello, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="d0e4e-156">Hello 실행 **azure 네트워크 nic 만들** toocreate 동적 IP 할당을 사용 하 여 새 NIC 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="d0e4e-157">어떻게 않아도 toospecify hello IP 주소가이 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="d0e4e-158">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="d0e4e-159">Hello 실행 **azure vm 집합** 명령 toochange hello NIC hello VM에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="d0e4e-160">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="d0e4e-161">를 원하는 실행 hello **azure 네트워크 nic 삭제** toodelete hello 이전 NIC. 명령</span><span class="sxs-lookup"><span data-stu-id="d0e4e-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="d0e4e-162">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="d0e4e-163">정적 개인 IP tooadd tooan 기존 VM을 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d0e4e-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="d0e4e-164">정적 개인 IP 주소 toohello 위의 hello 스크립트를 사용 하 여 만든 VM에서 사용 하는 NIC tooadd hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="d0e4e-165">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d0e4e-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="d0e4e-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0e4e-166">Next steps</span></span>
* <span data-ttu-id="d0e4e-167">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d0e4e-168">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d0e4e-169">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e4e-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

