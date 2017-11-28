---
title: "VM에 대한 개인 IP 주소 구성 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 가상 컴퓨터에 대한 개인 IP 주소를 구성하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="5ec74-103">Azure Portal을 사용하여 가상 컴퓨터에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="5ec74-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ec74-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5ec74-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="5ec74-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ec74-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="5ec74-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5ec74-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="5ec74-107">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="5ec74-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="5ec74-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="5ec74-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="5ec74-109">Azure CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="5ec74-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5ec74-110">이 문서에서는 Resource Manager 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="5ec74-111">[클래식 배포 모델에서 정적 개인 IP 주소를 관리](virtual-networks-static-private-ip-classic-pportal.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="5ec74-112">아래 샘플에는 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="5ec74-113">이 문서에 표시된 대로 단계를 실행하려는 경우 먼저 [vnet 만들기](virtual-networks-create-vnet-arm-pportal.md)에 설명된 테스트 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="5ec74-114">정적 개인 IP 주소 테스트용 VM을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="5ec74-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="5ec74-115">Azure 포털을 사용하여 리소스 관리자 배포 모드에서 VM을 만드는 동안에는 정적 개인 IP 주소를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="5ec74-116">VM를 먼저 만들어야, tehn에서 해당 개인 IP를 정적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="5ec74-117">*TestVNet*이라는 VNet의 *FrontEnd* 서브넷에 *DNS01*이라는 VM을 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5ec74-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="5ec74-118">브라우저에서 http://portal.azure.com으로 이동하고, 필요한 경우 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="5ec74-119">아래 그림과 같이 **새로 만들기** > **계산** > **Windows Server 2012 R2 Datacenter**를 클릭하고 **배포 모델 선택** 목록에 **리소스 관리자**가 이미 표시되는지 확인한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="5ec74-121">**기본 사항** 블레이드에서 만들 VM의 이름(이 시나리오에서는*DNS01* ), 로컬 관리자 계정 및 암호를 아래 그림처럼 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![기본 사항 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="5ec74-123">선택된 **위치**가 *미국 중부*인지 확인한 후 **리소스 그룹** 아래에서 **기존 선택**을 클릭하고 **리소스 그룹**을 다시 클릭한 후 *TestRG*, **확인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![기본 사항 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="5ec74-125">**크기 선택** 블레이드에서 **A1 표준**을 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![크기 선택 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="5ec74-127">**설정** 블레이드에서 다음 속성이 아래 값으로 설정되어 있는지 확인하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="5ec74-128">-**저장소 계정**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="5ec74-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="5ec74-129">**네트워크**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="5ec74-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="5ec74-130">**서브넷**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="5ec74-130">**Subnet**: *FrontEnd*</span></span>
     
     ![크기 선택 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="5ec74-132">**요약** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="5ec74-133">대시보드에 아래 타일이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="5ec74-135">VM의 정적 개인 IP 주소 정보를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="5ec74-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="5ec74-136">위의 단계를 사용하여 만든 VM에 대한 정적 개인 IP 주소를 보려면 아래 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="5ec74-137">Azure Portal에서 **모두 찾아보기** > **Virtual machines** > **DNS01** > **모든 설정** > **네트워크 인터페이스**를 클릭한 후 나열된 네트워크 인터페이스만 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![VM 타일 배포](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="5ec74-139">**네트워크 인터페이스** 블레이드에서 **모든 설정** > **IP 주소**를 클릭하고 **할당** 및 **IP 주소** 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![VM 타일 배포](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="5ec74-141">기존 VM에 정적 개인 IP 주소를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="5ec74-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="5ec74-142">위의 단계를 사용하여 만든 VM에 정적 개인 IP 주소를 추가하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5ec74-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="5ec74-143">위에 표시된 **IP 주소** 블레이드에서 **할당** 아래에 **정적**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="5ec74-144">**IP 주소**에 *192.168.1.101*을 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="5ec74-146">**저장**을 클릭한 후에도 할당이 **동적**으로 설정된 것으로 확인되면 입력한 IP 주소가 이미 사용 중임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="5ec74-147">다른 IP 주소로 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="5ec74-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="5ec74-148">VM에서 정적 개인 IP 주소를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="5ec74-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="5ec74-149">위에서 만든 VM에서 정적 개인 IP 주소를 제거하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="5ec74-150">위에 표시된 **IP 주소** 블레이드에서 **할당** 아래에 **동적**을 클릭하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ec74-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ec74-151">Next steps</span></span>
* <span data-ttu-id="5ec74-152">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5ec74-153">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5ec74-154">[예약된 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec74-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

