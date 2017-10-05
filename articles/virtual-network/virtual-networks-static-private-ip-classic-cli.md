---
title: "VM(클래식)에 대한 개인 IP 주소 구성 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 1.0을 사용하여 가상 컴퓨터(클래식)에 대한 개인 IP 주소를 구성하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed0fe2fea20671063395b9ff089599853278989d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-cli-10"></a><span data-ttu-id="135f4-103">Azure CLI 1.0을 사용하여 가상 컴퓨터(클래식)에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="135f4-103">Configure private IP addresses for a virtual machine (Classic) using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="135f4-104">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="135f4-105">[리소스 관리자 배포 모델에서 정적 개인 IP 주소를 관리](virtual-networks-static-private-ip-arm-cli.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="135f4-106">아래 샘플 Azure CLI 명령에는 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-106">The sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="135f4-107">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [vnet 만들기](virtual-networks-create-vnet-classic-cli.md)에 설명된 테스트 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="135f4-108">VM을 만들 때 정적 개인 IP 주소를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="135f4-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="135f4-109">위의 시나리오를 기반으로 *TestService*라는 새 클라우드 서비스에 *DNS01*이라는 VM을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-109">To create a new VM named *DNS01* in a new cloud service named *TestService* based on the scenario above, follow these steps:</span></span>

1. <span data-ttu-id="135f4-110">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="135f4-111">**azure service create** 명령을 실행하여 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-111">Run the **azure service create** command to create the cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="135f4-112">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="135f4-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="135f4-113">**azure create vm** 명령을 실행하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-113">Run the **azure create vm** command to create the VM.</span></span> <span data-ttu-id="135f4-114">정적 개인 IP 주소에 대한 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-114">Notice the value for a static private IP address.</span></span> <span data-ttu-id="135f4-115">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-115">The list shown after the output explains the parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="135f4-116">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="135f4-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting to "Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="135f4-117">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="135f4-117">**-l (or --location)**.</span></span> <span data-ttu-id="135f4-118">VM을 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-118">Azure region where the VM will be created.</span></span> <span data-ttu-id="135f4-119">이 시나리오에서는 *centralus*입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="135f4-120">**-n(또는 --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="135f4-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="135f4-121">만들 VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-121">Name of the VM to be created.</span></span>
   * <span data-ttu-id="135f4-122">**-w(또는 --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="135f4-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="135f4-123">VM이 만들어지는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-123">Name of the VNet where the VM will be created.</span></span> 
   * <span data-ttu-id="135f4-124">**-S(또는 --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="135f4-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="135f4-125">VM에 대한 정적 개인 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-125">Static private IP address for the VM.</span></span>
   * <span data-ttu-id="135f4-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="135f4-126">**TestService**.</span></span> <span data-ttu-id="135f4-127">VM이 만들어지는 클라우드 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-127">Name of the cloud service where the VM will be created.</span></span>
   * <span data-ttu-id="135f4-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="135f4-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="135f4-129">VM을 만드는 데 사용한 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-129">Image used to create the VM.</span></span>
   * <span data-ttu-id="135f4-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="135f4-130">**adminuser**.</span></span> <span data-ttu-id="135f4-131">Windows VM에 대한 로컬 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-131">Local administrator for the Windows VM.</span></span>
   * <span data-ttu-id="135f4-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="135f4-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="135f4-133">Windows VM에 대한 로컬 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-133">Local administrator password for the Windows VM.</span></span>

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="135f4-134">VM의 정적 개인 IP 주소 정보를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="135f4-134">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="135f4-135">위의 스크립트로 만든 VM에 대한 정적 개인 IP 주소 정보를 보려면 다음 Azure CLI 명령을 실행하고 *Network StaticIP*에 대한 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-135">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="135f4-136">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="135f4-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="135f4-137">VM에서 정적 개인 IP 주소를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="135f4-137">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="135f4-138">위의 스크립트에서 VM에 추가된 정적 개인 IP 주소를 제거하려면 다음 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-138">To remove the static private IP address added to the VM in the script above, run the following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="135f4-139">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="135f4-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-to-add-a-static-private-ip-to-an-existing-vm"></a><span data-ttu-id="135f4-140">기존 VM에 정적 개인 IP를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="135f4-140">How to add a static private IP to an existing VM</span></span>
<span data-ttu-id="135f4-141">위의 스크립트를 사용하여 만든 VM에 정적 개인 IP 주소를 추가하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-141">To add a static private IP address to the VM created using the script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="135f4-142">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="135f4-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="135f4-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="135f4-143">Next steps</span></span>
* <span data-ttu-id="135f4-144">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="135f4-145">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="135f4-146">[예약된 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="135f4-146">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

