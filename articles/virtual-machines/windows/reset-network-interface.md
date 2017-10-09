---
title: "Windows Azure VM에 대 한 aaaHow tooreset 네트워크 인터페이스 | Microsoft Docs"
description: "Tooreset Azure Windows VM에 대 한 인터페이스에 네트워크 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="1034c-103">Tooreset은 Azure Windows VM에 대 한 인터페이스에 네트워크 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1034c-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1034c-104">Hello 기본 NIC (네트워크 인터페이스)를 사용 하지 않도록 설정한 후에 tooMicrosoft Azure Windows 가상 컴퓨터 (VM)를 연결할 수 없거나 수동으로 NIC. hello에 대 한 고정 IP 설정</span><span class="sxs-lookup"><span data-stu-id="1034c-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="1034c-105">이 문서에서는 tooreset hello 원격 연결 문제를 해결할 수 있는 Azure Windows VM에 대 한 네트워크 인터페이스에 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="1034c-106">네트워크 인터페이스 다시 설정</span><span class="sxs-lookup"><span data-stu-id="1034c-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="1034c-107">클래식 VM</span><span class="sxs-lookup"><span data-stu-id="1034c-107">For Classic VMs</span></span>

<span data-ttu-id="1034c-108">tooreset 네트워크 인터페이스를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="1034c-109">Toohello 이동 [Azure 포털]( https://ms.portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="1034c-110">**Virtual Machines(클래식)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="1034c-111">가상 컴퓨터 선택 hello에 영향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="1034c-112">**IP 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="1034c-113">경우 hello **개인 IP 할당** 않습니다 **정적**도 변경**정적**합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="1034c-114">변경 hello **IP 주소** hello 서브넷에서에서 사용할 수 있는 tooanother IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="1034c-115">[저장]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-115">Select Save.</span></span>
8.  <span data-ttu-id="1034c-116">가상 컴퓨터 hello tooinitialize hello 새 NIC toohello 시스템 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="1034c-117">TooRDP tooyour 컴퓨터를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1034c-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="1034c-118">성공 하면 원하는 경우 개인 IP 주소 다시 toohello 원래 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="1034c-119">그렇지 않은 경우 현재 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="1034c-120">리소스 그룹 모델에서 배포된 VM의 경우</span><span class="sxs-lookup"><span data-stu-id="1034c-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="1034c-121">Toohello 이동 [Azure 포털]( https://ms.portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="1034c-122">가상 컴퓨터 선택 hello에 영향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="1034c-123">**네트워크 인터페이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="1034c-124">Hello 컴퓨터와 연결 된 네트워크 인터페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="1034c-125">**IP 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="1034c-126">Hello IP를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="1034c-127">경우 hello **개인 IP 할당** 않습니다 **정적**도 변경**정적**합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="1034c-128">변경 hello **IP 주소** hello 서브넷에서에서 사용할 수 있는 tooanother IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="1034c-129">가상 컴퓨터 hello tooinitialize hello 새 NIC toohello 시스템 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="1034c-130">TooRDP tooyour 컴퓨터를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1034c-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="1034c-131">성공 하면 원하는 경우 개인 IP 주소 다시 toohello 원래 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="1034c-132">그렇지 않은 경우 현재 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="1034c-133">삭제 hello 사용할 수 없는 Nic</span><span class="sxs-lookup"><span data-stu-id="1034c-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="1034c-134">원격 데스크톱 toohello 컴퓨터 수 후에 hello 이전 Nic tooavoid hello 잠재적인 문제를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="1034c-135">장치 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="1034c-136">**보기** > **숨겨진 장치 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="1034c-137">**네트워크 어댑터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="1034c-138">"Microsoft Hyper-v 네트워크 어댑터"로 지정 하는 hello 어댑터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="1034c-139">사용할 수 없는 어댑터는 회색으로 표시된 것을 볼 수 있습니다. Hello 어댑터를 마우스 오른쪽 단추로 클릭 하 고 제거를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![hello NIC의 hello 이미지](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="1034c-141">만 hello 이름이 "Microsoft Hyper-v 네트워크 어댑터" hello 사용할 수 없는 어댑터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="1034c-142">Hello의 숨겨진된 그 밖의 어댑터를 제거 하는 경우 추가 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="1034c-143">이제 사용할 수 없는 모든 어댑터가 시스템에서 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="1034c-143">Now all unavailable adapter should be cleared out from your system.</span></span>