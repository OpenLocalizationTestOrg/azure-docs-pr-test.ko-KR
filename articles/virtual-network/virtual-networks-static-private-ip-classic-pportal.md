---
title: "VM(클래식)에 대한 개인 IP 주소 구성 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 가상 컴퓨터(클래식)에 대한 개인 IP 주소를 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="6dfbc-103">Azure Portal을 사용하여 가상 컴퓨터(클래식)에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="6dfbc-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="6dfbc-104">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="6dfbc-105">[리소스 관리자 배포 모델에서 정적 개인 IP 주소를 관리](virtual-networks-static-private-ip-arm-pportal.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="6dfbc-106">아래 샘플에는 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="6dfbc-107">이 문서에 표시된 대로 단계를 실행하려는 경우 먼저 [vnet 만들기](virtual-networks-create-vnet-classic-pportal.md)에 설명된 테스트 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="6dfbc-108">VM을 만들 때 정적 개인 IP 주소를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dfbc-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="6dfbc-109">*192.168.1.101*의 정적 개인 IP 주소를 사용하여 *TestVNet*이라는 VNet의 *FrontEnd* 서브넷에 *DNS01*이라는 VM을 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="6dfbc-110">브라우저에서 http://portal.azure.com으로 이동하고, 필요한 경우 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="6dfbc-111">**새로 만들기** > **계산** > **Windows Server 2012 R2 Datacenter**를 클릭하고 **배포 모델 선택** 목록에 **클래식**이 이미 표시되는지 확인한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="6dfbc-113">**VM 만들기** 블레이드에서 만들 VM의 이름(이 시나리오에서는*DNS01* ), 로컬 관리자 계정 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="6dfbc-115">**옵션 구성** > **네트워크** > **Virtual Network**를 클릭하고 **TestVNet**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="6dfbc-116">**TestVNet** 을 사용할 수 없는 경우 *미국 중부* 위치를 사용 중이고 이 문서의 시작 부분에서 설명한 테스트 환경을 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="6dfbc-118">**네트워크** 블레이드에서 현재 선택된 서브넷이 *FrontEnd*인지 확인하고 **IP 주소 할당** 아래에서 **IP 주소**를 클릭하고 **정적**을 클릭한 후 아래와 같이 **IP 주소**에 대해 *192.168.1.101*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="6dfbc-120">**IP 주소** 블레이드에서 **확인**을 클릭한 후 **네트워크** 블레이드에서 **확인**을 클릭하고 **옵션 구성** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="6dfbc-121">**VM 만들기** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="6dfbc-122">대시보드에 아래 타일이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="6dfbc-124">VM의 정적 개인 IP 주소 정보를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dfbc-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="6dfbc-125">위의 단계를 사용하여 만든 VM에 대한 정적 개인 IP 주소를 보려면 아래 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="6dfbc-126">Azure Portal에서 **모두 찾아보기** > **가상 컴퓨터(클래식)** > **DNS01All** > **모든 설정** > **IP 주소**를 클릭하고 아래와 같이 IP 주소 할당 및 IP 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="6dfbc-128">VM에서 정적 개인 IP 주소를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dfbc-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="6dfbc-129">위에서 만든 VM에서 정적 개인 IP 주소를 제거하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="6dfbc-130">위에 표시된 **IP 주소** 블레이드에서 **IP 주소 할당** 오른쪽에서 **동적**을 클릭한 후 **저장**, **예**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="6dfbc-132">기존 VM에 정적 개인 IP 주소를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dfbc-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="6dfbc-133">위의 단계를 사용하여 만든 VM에 정적 개인 IP 주소를 추가하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="6dfbc-134">위에 표시된 **IP 주소** 블레이드에서 **IP 주소 할당** 오른쪽에서 **정적**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="6dfbc-135">**IP 주소**에 *192.168.1.101*을 입력하고 **저장**을 클릭한 후 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dfbc-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6dfbc-136">Next steps</span></span>
* <span data-ttu-id="6dfbc-137">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="6dfbc-138">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="6dfbc-139">[예약된 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6dfbc-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

