---
title: "Windows Azure VM에 대한 네트워크 인터페이스를 다시 설정하는 방법 | Microsoft Docs"
description: "Windows Azure VM에 대한 네트워크 인터페이스를 다시 설정하는 방법을 보여 줍니다."
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="d810d-103">Windows Azure VM에 대한 네트워크 인터페이스를 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d810d-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d810d-104">기본 NIC(네트워크 인터페이스)를 사용하지 않도록 설정하거나 NIC에 대한 고정 IP를 수동으로 설정한 후에는 Microsoft Azure Windows VM(Virtual Machine)에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="d810d-105">이 문서에서는 원격 연결 문제를 해결하기 위해 Azure Windows VM에 대한 네트워크 인터페이스를 다시 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="d810d-106">네트워크 인터페이스 다시 설정</span><span class="sxs-lookup"><span data-stu-id="d810d-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="d810d-107">클래식 VM</span><span class="sxs-lookup"><span data-stu-id="d810d-107">For Classic VMs</span></span>

<span data-ttu-id="d810d-108">네트워크 인터페이스를 다시 설정하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d810d-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="d810d-109">[Azure 포털]( https://ms.portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="d810d-110">**Virtual Machines(클래식)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="d810d-111">영향을 받는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="d810d-112">**IP 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="d810d-113">**개인 IP 할당**이 **정적**이 아닌 경우 **정적**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="d810d-114">**IP 주소**를 서브넷에서 사용할 수 있는 다른 IP 주소로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="d810d-115">[저장]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-115">Select Save.</span></span>
8.  <span data-ttu-id="d810d-116">가상 컴퓨터를 다시 시작하여 시스템에 대한 새 NIC를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="d810d-117">컴퓨터에 RDP를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-117">Try to RDP to your machine.</span></span> <span data-ttu-id="d810d-118">성공할 경우 개인 IP 주소를 원래대로 변경할 수 있습니다(원하는 경우).</span><span class="sxs-lookup"><span data-stu-id="d810d-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="d810d-119">그렇지 않은 경우 현재 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="d810d-120">리소스 그룹 모델에서 배포된 VM의 경우</span><span class="sxs-lookup"><span data-stu-id="d810d-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="d810d-121">[Azure 포털]( https://ms.portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="d810d-122">영향을 받는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="d810d-123">**네트워크 인터페이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="d810d-124">컴퓨터와 연결된 네트워크 인터페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="d810d-125">**IP 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="d810d-126">IP를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-126">Select the IP.</span></span> 
7.  <span data-ttu-id="d810d-127">**개인 IP 할당**이 **정적**이 아닌 경우 **정적**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="d810d-128">**IP 주소**를 서브넷에서 사용할 수 있는 다른 IP 주소로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="d810d-129">가상 컴퓨터를 다시 시작하여 시스템에 대한 새 NIC를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="d810d-130">컴퓨터에 RDP를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-130">Try to RDP to your machine.</span></span> <span data-ttu-id="d810d-131">성공할 경우 개인 IP 주소를 원래대로 변경할 수 있습니다(원하는 경우).</span><span class="sxs-lookup"><span data-stu-id="d810d-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="d810d-132">그렇지 않은 경우 현재 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="d810d-133">사용할 수 없는 NIC를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="d810d-134">컴퓨터에 원격 데스크톱을 수행한 후 잠재적인 문제를 방지하기 위해 이전 NIC를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="d810d-135">장치 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="d810d-136">**보기** > **숨겨진 장치 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="d810d-137">**네트워크 어댑터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="d810d-138">“Microsoft Hyper-V 네트워크 어댑터”로 명명된 어댑터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="d810d-139">사용할 수 없는 어댑터는 회색으로 표시된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="d810d-140">어댑터를 마우스 오른쪽 단추로 클릭하고 [제거]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-140">Right-click the adapter and then select Uninstall.</span></span>

    ![NIC 이미지](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="d810d-142">이름이 “Microsoft Hyper-V 네트워크 어댑터”이고 사용할 수 없는 어댑터만 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="d810d-143">다른 숨겨진 어댑터를 제거하는 경우 추가 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="d810d-144">이제 사용할 수 없는 모든 어댑터가 시스템에서 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="d810d-144">Now all unavailable adapter should be cleared out from your system.</span></span>