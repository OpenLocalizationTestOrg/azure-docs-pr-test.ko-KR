---
title: "aaaConfigure DevTest Labs Azure에서에서 가상 네트워크 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 기존 가상 네트워크 및 서브넷에 Azure DevTest Labs를 사용 하 여 VM에서 사용 하 고"
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
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="e68fd-103">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="e68fd-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="e68fd-104">Hello 문서에 설명 된 대로 [tooa 랩 아티팩트를 사용 하 여 VM을 추가할](devtest-lab-add-vm-with-artifacts.md)랩에 VM을 만들 때, 구성 된 가상 네트워크를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="e68fd-105">이 작업을 수행 하는 시나리오 중 하나를 사용 하 여 Vm에서 회사 네트워크 리소스를 사이트 간 VPN 또는 express 경로도로 구성 된 가상 네트워크 hello tooaccess 해야 할 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="e68fd-106">hello 다음 섹션에서는 설명 방법을 tooadd 한다는 Vm을 만들 때 사용할 수 있는 toochoose은 랩의 가상 네트워크 설정으로 기존 가상 네트워크가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="e68fd-107">Hello Azure 포털을 사용 하 여 랩에 대 한 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="e68fd-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="e68fd-108">hello 다음 단계에 관한 hello에 VM을 만들 때 사용할 수 있도록 기존 가상 네트워크 (및 서브넷) tooa 랩을 추가 동일한 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="e68fd-109">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e68fd-110">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="e68fd-111">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="e68fd-112">Hello 랩 블레이드에서 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="e68fd-113">Hello 랩에 **구성** 블레이드를 **가상 네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="e68fd-114">Hello에 **가상 네트워크** 블레이드에 hello 현재 랩 뿐만 아니라 랩에 대해 만들어진 hello 기본 가상 네트워크에 대 한 구성 된 가상 네트워크의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="e68fd-115">**+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-115">Select **+ Add**.</span></span>
   
    ![기존 가상 네트워크 tooyour 랩을 추가합니다](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="e68fd-117">Hello에 **가상 네트워크** 블레이드를 **[가상 네트워크 선택]**합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![기존 가상 네트워크 선택](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="e68fd-119">Hello에 **가상 네트워크 선택** 블레이드, 선택 hello 원하는 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="e68fd-120">hello 블레이드 표시 되는 모든 hello 가상 네트워크는 아래 hello 동일 지역 hello 랩 hello 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="e68fd-121">가상 네트워크를 선택한 후 toohello 반환될지 **가상 네트워크** hello hello 블레이드 맨 아래에 hello 목록의 hello 서브넷을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![서브넷 목록](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="e68fd-123">hello 랩 서브넷 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-123">hello Lab Subnet blade is displayed.</span></span>

    ![랩 서브넷 블레이드](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="e68fd-125">**랩 서브넷 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="e68fd-126">VM 만들기 랩에서 사용 되는 서브넷 toobe tooallow 선택 **가상 컴퓨터 생성에 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="e68fd-127">tooenable는 [공용 IP 주소를 공유](devtest-lab-shared-ip.md)선택, **공용 IP를 공유 하는 활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="e68fd-128">tooallow 공용 IP 주소는 서브넷에서 선택 **공용 IP를 만들 수 있도록**합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="e68fd-129">Hello에 **사용자 당 최대 가상 컴퓨터** 필드에서 지정 각 서브넷에 대 한 사용자 당 최대 Vm hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="e68fd-130">VM 수에 제한을 두지 않으려면 이 필드는 공백으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="e68fd-131">선택 **확인** tooclose hello 랩 서브넷 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="e68fd-132">선택 **저장** tooclose hello 가상 네트워크 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="e68fd-133">Hello 가상 네트워크는 구성 했으므로 VM을 만들 때 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="e68fd-134">toosee 어떻게 toocreate VM 가상 네트워크를 지정 하 고 toohello 문서를 참조 하십시오 [tooa 랩 아티팩트를 사용 하 여 VM을 추가할](devtest-lab-add-vm-with-artifacts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="e68fd-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e68fd-135">Next steps</span></span>
<span data-ttu-id="e68fd-136">Hello 원하는 tooyour 랩 가상 네트워크를 추가 하면 hello에는 너무[추가 VM tooyour 랩](devtest-lab-add-vm-with-artifacts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e68fd-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

