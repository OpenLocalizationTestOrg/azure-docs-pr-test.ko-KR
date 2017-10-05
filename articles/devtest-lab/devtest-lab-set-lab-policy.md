---
title: "Azure DevTest Labs에서 랩 정책 관리 | Microsoft 문서"
description: "VM 크기, 사용자당 최대 VM 수 및 자동 종료와 같은 랩 정책을 정의하는 방법에 대해 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="75aea-103">Azure DevTest Labs에서 랩에 대한 모든 정책 관리</span><span class="sxs-lookup"><span data-stu-id="75aea-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="75aea-104">Azure DevTest Labs에서는 각 랩의 정책(설정)을 관리하여 랩에서 비용을 관리하고 낭비를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="75aea-105">이 문서에서는 각 정책을 설정하는 방법에 대해 단계별로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="75aea-106">허용된 가상 컴퓨터 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="75aea-107">허용 VM 크기를 설정하는 정책은 랩에서 허용되는 VM 크기를 지정함으로써 랩의 낭비가 최소화되도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="75aea-108">이 정책이 활성화되면 이 목록의 VM 크기만 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="75aea-109">랩의 **구성 및 정책** 블레이드에서 **허용된 가상 컴퓨터 크기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![허용된 가상 컴퓨터 크기](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="75aea-111">이 정책을 사용하도록 설정하려면 **설정**을 선택하고 사용하지 않도록 설정하려면 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="75aea-112">이 정책을 사용하도록 설정한 경우 랩에서 만들 수 있는 하나 이상의 VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="75aea-113">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="75aea-114">사용자당 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-114">Set virtual machines per user</span></span>
<span data-ttu-id="75aea-115">**사용자당 가상 컴퓨터** 에 대한 정책을 사용하면 개별 사용자가 만들 수 있는 최대 VM 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="75aea-116">사용자 제한에 도달하면 사용자가 VM을 만들거나 클레임하는 경우 VM을 만들거나 클레임할 수 없다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="75aea-117">랩의 **구성 및 정책** 메뉴에서 **사용자당 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![사용자당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="75aea-119">**예**를 선택하여 사용자당 VM 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="75aea-120">사용자당 VM 수를 제한하지 않으려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="75aea-121">**예**를 선택하면 사용자가 만들거나 클레임할 수 있는 최대 VM 수를 나타내는 숫자 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="75aea-122">**예**를 선택하여 SSD(반도체 디스크)를 사용할 수 있는 사용자당 VM 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="75aea-123">SSD를 사용할 수 있는 VM 수를 제한하지 않으려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="75aea-124">**예**를 선택하면 SSD를 사용하여 만들 수 있는 최대 VM 수를 나타내는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="75aea-125">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="75aea-126">랩당 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-126">Set virtual machines per lab</span></span>
<span data-ttu-id="75aea-127">**랩당 가상 컴퓨터** 에 대한 정책을 사용하면 현재 랩에 대해 생성할 수 있는 최대 VM 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="75aea-128">랩 제한에 도달하면 사용자가 VM을 만들려고 하는 경우 VM을 만들 수 없다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="75aea-129">랩의 **구성 및 정책** 메뉴에서 **랩당 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![랩당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="75aea-131">**예**를 선택하여 랩당 VM 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="75aea-132">랩당 VM 수를 제한하지 않으려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="75aea-133">**예**를 선택하면 사용자가 만들거나 클레임할 수 있는 최대 VM 수를 나타내는 숫자 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="75aea-134">**예**를 선택하여 SSD(반도체 디스크)를 사용할 수 있는 사용자당 VM 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="75aea-135">SSD를 사용할 수 있는 VM 수를 제한하지 않으려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="75aea-136">**예**를 선택하면 SSD를 사용하여 만들 수 있는 최대 VM 수를 나타내는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="75aea-137">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="75aea-138">자동 종료 설정</span><span class="sxs-lookup"><span data-stu-id="75aea-138">Set auto-shutdown</span></span>
<span data-ttu-id="75aea-139">자동 종료 정책에서는 이 랩의 VM이 종료되는 시간을 지정하여 랩 낭비를 최소화할 수 있도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="75aea-140">랩의 **구성 및 정책** 블레이드에서 **자동 종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![자동 종료](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="75aea-142">이 정책을 사용하도록 설정하려면 **설정**을 선택하고 사용하지 않도록 설정하려면 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="75aea-143">이 정책을 사용하도록 설정한 경우 현재 랩의 모든 VM을 종료하는 시간(및 표준 시간대)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="75aea-144">지정된 자동 종료 시간 15분 전에 알림을 보내는 옵션으로 **예** 또는 **아니요**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="75aea-145">**예**를 지정한 경우 알림을 받을 웹후크 URL 끝점을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="75aea-146">웹후크에 대한 자세한 내용은 [웹후크 또는 API Azure Function 만들기](../azure-functions/functions-create-a-web-hook-or-api-function.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75aea-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="75aea-147">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-147">Select **Save**.</span></span>

    <span data-ttu-id="75aea-148">기본적으로 이 정책을 사용하도록 설정하면 현재 랩의 모든 VM에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="75aea-149">특정 VM에서 이 설정을 제거하려면 VM의 블레이드를 열고 해당 **자동 종료** 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="75aea-150">자동 시작 설정</span><span class="sxs-lookup"><span data-stu-id="75aea-150">Set auto-start</span></span>
<span data-ttu-id="75aea-151">자동 시작 정책을 사용하면 현재 랩의 VM을 시작할 시기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="75aea-152">랩의 **구성 및 정책** 블레이드에서 **자동 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![자동 시작](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="75aea-154">이 정책을 사용하도록 설정하려면 **설정**을 선택하고 사용하지 않도록 설정하려면 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="75aea-155">이 정책을 사용하도록 설정한 경우 예약 시작 시간, 표준 시간대 및 해당 시간이 적용되는 요일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="75aea-156">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-156">Select **Save**.</span></span>

    <span data-ttu-id="75aea-157">사용하도록 설정해도 이 정책이 현재 랩의 VM에 자동으로 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="75aea-158">이 설정을 특정 VM에 적용하려면 VM의 블레이드를 열고 해당 **자동 시작** 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="75aea-159">만료 날짜 설정</span><span class="sxs-lookup"><span data-stu-id="75aea-159">Set expiration date</span></span>
<span data-ttu-id="75aea-160">[VM을 만들 때](devtest-lab-add-vm.md) 만료 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="75aea-161">**고급 설정**에서 달력 아이콘을 선택하고 VM이 자동으로 삭제될 날짜를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="75aea-162">기본적으로 VM은 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="75aea-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75aea-163">Next steps</span></span>
<span data-ttu-id="75aea-164">랩에 대한 다양한 VM 정책 설정을 정의 및 적용한 후에는 다음 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="75aea-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="75aea-165">[공유 IP 주소 이해](devtest-lab-shared-ip.md) - DevTest Labs에서 공유 IP 주소를 사용하여 랩 VM에 연결하는 데 필요한 공용 IP 주소 수를 최소화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="75aea-166">[비용 관리 구성](devtest-lab-configure-cost-management.md) - **월간 예상 원가 추세** 차트 사용 방법을 보여 줍니다</span><span class="sxs-lookup"><span data-stu-id="75aea-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="75aea-167">현재까지의 예상 비용과 예상되는 월말 비용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="75aea-168">[사용자 지정 이미지 만들기](devtest-lab-create-template.md) - VM을 만들 때 사용자 지정 이미지 또는 마켓플레이스 이미지 중에서 기본 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="75aea-169">이 문서에는 VHD 파일에서 사용자 지정 이미지를 만드는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="75aea-170">[마켓플레이스 이미지 구성](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs에서 Azure Marketplace 이미지에 기반하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="75aea-171">이 문서에서는 랩에서 VM을 만들 때 사용할 수 있는 Azure 마켓플레이스 이미지(있는 경우)를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="75aea-172">[랩에서 VM 만들기](devtest-lab-add-vm-with-artifacts.md) - 기본 이미지(사용자 지정 또는 마켓플레이스 이미지)에서 VM을 만드는 방법 및 VM에서 아티팩트 작업 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75aea-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

