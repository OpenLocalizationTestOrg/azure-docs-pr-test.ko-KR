---
title: "Vm (클래식)-Azure 포털에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터 (클래식)에 대 한 Azure 포털을 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="7f510-103">Hello Azure 포털을 사용 하 여 가상 컴퓨터 (클래식)에 대 한 개인 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7f510-104">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="7f510-105">수도 있습니다 [hello 리소스 관리자 배포 모델에서 정적 개인 IP 주소 관리](virtual-networks-static-private-ip-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="7f510-106">다음 hello 샘플 단계를 이미 만든 단순한 환경을 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="7f510-107">이 문서에 표시 된 대로 toorun hello 단계를 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-classic-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="7f510-108">어떻게 toospecify 정적 개인 IP 주소는 VM을 만들 때</span><span class="sxs-lookup"><span data-stu-id="7f510-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="7f510-109">toocreate 라는 VM *DNS01* hello에 *프런트 엔드* 라는 VNet의 서브넷 *TestVNet* 의 정적 개인 ip *192.168.1.101*, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="7f510-110">브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7f510-111">클릭 **새로** > **계산** > **Windows Server 2012 R2 Datacenter**, 해당 hello 확인 **배포모델선택** 목록 표시 이미 **클래식**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="7f510-113">Hello에 **VM 만들기** 블레이드에서 만든 hello VM toobe hello 이름 입력 (*DNS01* 시나리오에서), 로컬 관리자 계정 및 암호 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="7f510-115">**옵션 구성** > **네트워크** > **Virtual Network**를 클릭하고 **TestVNet**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="7f510-116">경우 **TestVNet** 를 사용할 수 없으면 hello를 사용 하 고 있는지 확인 *중앙 미국* 위치 hello이이 문서의 시작 부분에 설명 된 hello 테스트 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="7f510-118">Hello에 **네트워크** 블레이드에서 현재 선택 된 확인 되었는지 hello 서브넷은 *프런트 엔드*, 클릭 **IP 주소**아래 **IP주소할당** 클릭 **정적**, 다음을 입력 하 고 *192.168.1.101* 에 대 한 **IP 주소** 아래와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="7f510-120">클릭 **확인** hello에 **IP 주소** 블레이드에서 클릭 **확인** hello에 **네트워크** 블레이드에서 하 고 클릭 **확인**hello에 **선택적 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="7f510-121">Hello에 **VM 만들기** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="7f510-122">공지 hello 타일 아래에 대시보드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="7f510-124">어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="7f510-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="7f510-125">tooview hello 정적 개인 IP 주소 정보 hello에 대 한 위의 hello 단계를 사용 하 여 만든 VM 아래 hello 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="7f510-126">Hello Azure Azure 포털에서 클릭 **모두 찾아보기** > **가상 컴퓨터 (클래식)** > **DNS01**  >   **모든 설정이** > **IP 주소** IP 주소 할당 및 IP 주소 아래와 같이 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="7f510-128">어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다</span><span class="sxs-lookup"><span data-stu-id="7f510-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="7f510-129">tooremove hello 정적 개인 IP 주소에서 VM을 위에서 만든 hello는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="7f510-130">Hello에서 **IP 주소** 위에 표시 된 블레이드 클릭 **동적** 의 오른쪽 toohello **IP 주소 할당**, 클릭 **저장**, 한 다음 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="7f510-132">정적 개인 IP tooadd tooan 기존 VM을 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f510-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="7f510-133">아래의 hello 단계를 수행 하는 tooadd는 정적 개인 IP 주소 toohello 위의 hello 단계를 사용 하 여 만든 VM:</span><span class="sxs-lookup"><span data-stu-id="7f510-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="7f510-134">Hello에서 **IP 주소** 위에 표시 된 블레이드 클릭 **정적** 의 오른쪽 toohello **IP 주소 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="7f510-135">**IP 주소**에 *192.168.1.101*을 입력하고 **저장**을 클릭한 후 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f510-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7f510-136">Next steps</span></span>
* <span data-ttu-id="7f510-137">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="7f510-138">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="7f510-139">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f510-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

