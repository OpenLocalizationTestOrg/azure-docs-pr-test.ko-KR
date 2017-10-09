---
title: "Vm (클래식)-Azure CLI 1.0에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터 (클래식)에 대 한 Azure CLI (명령줄 인터페이스) 1.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="3abb1-103">Hello Azure CLI 1.0을 사용 하 여 가상 컴퓨터 (클래식)에 대 한 개인 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3abb1-104">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="3abb1-105">수도 있습니다 [hello 리소스 관리자 배포 모델에서 정적 개인 IP 주소 관리](virtual-networks-static-private-ip-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="3abb1-106">hello 샘플 Azure CLI 명령 아래에 이미 만든 단순한 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="3abb1-107">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="3abb1-108">어떻게 toospecify 정적 개인 IP 주소는 VM을 만들 때</span><span class="sxs-lookup"><span data-stu-id="3abb1-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="3abb1-109">명명 된 새 VM toocreate *DNS01* 라는 새 클라우드 서비스에 *TestService* 위의 hello 시나리오에 따라, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="3abb1-110">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="3abb1-111">Hello 실행 **azure 서비스를 만들** toocreate hello 클라우드 서비스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="3abb1-112">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3abb1-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="3abb1-113">Hello 실행 **azure vm 만들기** 명령 toocreate hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="3abb1-114">개인 고정 IP 주소에 대 한 hello 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="3abb1-115">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="3abb1-116">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3abb1-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
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
   
   * <span data-ttu-id="3abb1-117">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-117">**-l (or --location)**.</span></span> <span data-ttu-id="3abb1-118">Azure 지역 hello VM 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="3abb1-119">이 시나리오에서는 *centralus*입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="3abb1-120">**-n(또는 --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="3abb1-121">만든 hello VM toobe의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="3abb1-122">**-w(또는 --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="3abb1-123">Hello hello VM을 만들 위치는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="3abb1-124">**-S(또는 --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="3abb1-125">Hello VM에 대 한 정적 개인 IP 주소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="3abb1-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-126">**TestService**.</span></span> <span data-ttu-id="3abb1-127">Hello VM 만들어지는 hello 클라우드 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="3abb1-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="3abb1-129">이미지는 toocreate hello VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="3abb1-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-130">**adminuser**.</span></span> <span data-ttu-id="3abb1-131">Windows VM hello에 대 한 로컬 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="3abb1-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="3abb1-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="3abb1-133">Windows VM hello에 대 한 로컬 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="3abb1-134">어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="3abb1-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="3abb1-135">tooview hello 정적 개인 IP 주소 VM hello 다음 Azure CLI 명령을 실행 합니다. 위의 hello 스크립트를 사용 하 여 만든 hello에 대 한 정보 및 hello 값에 대 한 관찰 *네트워크 StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="3abb1-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="3abb1-136">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3abb1-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="3abb1-137">어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다</span><span class="sxs-lookup"><span data-stu-id="3abb1-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="3abb1-138">VM toohello 다음 Azure CLI 명령이 실행된 hello 위의 hello 스크립트에 추가 하는 tooremove hello 정적 개인 IP 주소.</span><span class="sxs-lookup"><span data-stu-id="3abb1-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="3abb1-139">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3abb1-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="3abb1-140">어떻게 tooadd 정적 개인 IP tooan 기존 VM</span><span class="sxs-lookup"><span data-stu-id="3abb1-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="3abb1-141">정적 개인 IP 주소 toohello VM 사용 하 여 만든 녀석 위의 hello 스크립트 명령을 다음 tooadd:</span><span class="sxs-lookup"><span data-stu-id="3abb1-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="3abb1-142">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3abb1-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="3abb1-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3abb1-143">Next steps</span></span>
* <span data-ttu-id="3abb1-144">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="3abb1-145">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="3abb1-146">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3abb1-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

