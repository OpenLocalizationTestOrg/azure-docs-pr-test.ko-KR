---
title: "Azure DevTest Labs에서 가상 네트워크 구성 | Microsoft 문서"
description: "기존 가상 네트워크 및 서브넷을 구성하고 Azure DevTest Labs를 통해 VM에서 사용하는 방법에 대해 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="7cf1c-103">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="7cf1c-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="7cf1c-104">[아티팩트를 사용하여 랩에 VM 추가](devtest-lab-add-vm-with-artifacts.md)문서에 설명된 대로 랩에 VM을 만들 때 구성된 가상 네트워크를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="7cf1c-105">이 작업을 수행하는 시나리오 중 하나는 Express 경로 또는 사이트 간 VPN으로 구성된 가상 네트워크를 사용하여 VM에서 회사 네트워크 리소스에 액세스해야 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="7cf1c-106">다음 섹션에서는 VM을 만들 때 선택할 수 있도록 랩의 가상 네트워크 설정으로 기존 가상 네트워크를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="7cf1c-107">Azure 포털을 사용하여 랩에 대한 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="7cf1c-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="7cf1c-108">다음 단계에서는 동일한 랩에서 VM을 만들 때 사용할 수 있도록 랩에 기존 가상 네트워크(및 서브넷)를 추가하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="7cf1c-109">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="7cf1c-110">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="7cf1c-111">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="7cf1c-112">랩의 블레이드에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="7cf1c-113">랩의 **구성** 블레이드에서 **가상 네트워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="7cf1c-114">**가상 네트워크** 블레이드에서 현재 랩에 대해 구성한 가상 네트워크 및 랩에 대해 만들어진 기본 가상 네트워크의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="7cf1c-115">**+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-115">Select **+ Add**.</span></span>
   
    ![랩에 기존 가상 네트워크 추가](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="7cf1c-117">**가상 네트워크** 블레이드에서 **[가상 네트워크 선택]**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![기존 가상 네트워크 선택](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="7cf1c-119">**가상 네트워크 선택** 블레이드에서 원하는 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="7cf1c-120">블레이드에는 구독의 동일 지역에 속하는 모든 가상 네트워크가 랩으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="7cf1c-121">가상 네트워크를 선택하면 **가상 네트워크**로 되돌아가며, 블레이드 하단에 있는 목록에서 서브넷을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![서브넷 목록](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="7cf1c-123">랩 서브넷 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-123">The Lab Subnet blade is displayed.</span></span>

    ![랩 서브넷 블레이드](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="7cf1c-125">**랩 서브넷 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="7cf1c-126">서브넷이 랩 VM 생성에 사용되도록 하려면 **가상 컴퓨터를 만들 때 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="7cf1c-127">[shared public IP address](devtest-lab-shared-ip.md)(공유 공용 IP 주소)를 사용하도록 설정하려면 **Enable shared public IP**(공유 공용 IP 사용)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="7cf1c-128">서브넷에서 공용 IP 주소를 허용하려면 **Allow public IP creation(공용 IP 생성 허용)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="7cf1c-129">**사용자당 최대 가상 컴퓨터** 필드에서 각 서브넷에 대한 사용자당 최대 VM을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="7cf1c-130">VM 수에 제한을 두지 않으려면 이 필드는 공백으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="7cf1c-131">**확인**을 선택하여 랩 서브넷 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="7cf1c-132">**저장**을 선택하여 가상 네트워크 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="7cf1c-133">이제 가상 네트워크를 구성했으므로 VM을 만들 때 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="7cf1c-134">VM을 만들고 가상 네트워크를 지정하는 방법을 확인하려면 [아티팩트를 사용하여 랩에 VM 추가](devtest-lab-add-vm-with-artifacts.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="7cf1c-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7cf1c-135">Next steps</span></span>
<span data-ttu-id="7cf1c-136">랩에 원하는 가상 네트워크를 추가한 후에는 [랩에 VM을 추가](devtest-lab-add-vm-with-artifacts.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf1c-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

