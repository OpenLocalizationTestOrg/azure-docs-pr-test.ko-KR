---
title: "Azure DevTest Labs에서 기본 랩 정책 관리 | Microsoft Docs"
description: "DevTest Labs에서 랩에 대한 기본 정책(설정)을 지정하는 방법에 대해 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="34f04-103">Azure DevTest Labs에서 랩에 대한 기본 정책 관리</span><span class="sxs-lookup"><span data-stu-id="34f04-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="34f04-104">Azure DevTest Labs를 통해 각 랩에 대한 정책(설정)을 관리하여 비용을 제어하고 랩에서의 낭비를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="34f04-105">이 문서에서는 가장 중요한 두 가지 정책을 설정하여 단일 사용자가 클레임하거나 생성할 수 있는 VM(가상 컴퓨터) 수를 제한하고 자동 종료를 구성하는 방법을 확인하여 정책을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="34f04-106">모든 랩 정책을 설정하는 방법을 보려면 [Azure DevTest Labs에서 랩 정책 정의](devtest-lab-set-lab-policy.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34f04-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="34f04-107">Azure DevTest Labs의 랩 정책에 액세스</span><span class="sxs-lookup"><span data-stu-id="34f04-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="34f04-108">다음 단계에서는 Azure DevTest Labs에서 랩에 대한 정책을 설정하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="34f04-109">랩에 대한 정책을 보거나 변경하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="34f04-110">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="34f04-111">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="34f04-112">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="34f04-113">**구성 및 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-113">Select **Configuration and policies**.</span></span>

    ![정책 설정 블레이드](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="34f04-115">**구성 및 정책** 블레이드에는 지정할 수 있는 설정의 메뉴가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="34f04-116">이 문서에서는 **사용자당 가상 컴퓨터** 및 **자동 종료**에 대한 설명만 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="34f04-117">나머지 설정에 대해 알아보려면 [Azure DevTest Labs에서 랩에 대한 모든 정책 관리](./devtest-lab-set-lab-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34f04-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="34f04-118">사용자당 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-118">Set virtual machines per user</span></span>
<span data-ttu-id="34f04-119">**사용자당 가상 컴퓨터** 에 대한 정책을 사용하면 개별 사용자가 만들 수 있는 최대 VM 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="34f04-120">사용자 제한에 도달하면 사용자가 VM을 만들거나 클레임하는 경우 VM을 만들거나 클레임할 수 없다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="34f04-121">랩의 **구성 및 정책** 메뉴에서 **사용자당 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![사용자당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="34f04-123">**예**를 선택하여 사용자당 VM 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="34f04-124">사용자당 VM 수를 제한하지 않으려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="34f04-125">**예**를 선택하면 사용자가 만들거나 클레임할 수 있는 최대 VM 수를 나타내는 숫자 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="34f04-126">**예**를 선택하여 SSD(반도체 디스크)를 사용할 수 있는 사용자당 VM 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="34f04-127">SSD를 사용할 수 있는 VM 수를 제한하지 않으려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="34f04-128">**예**를 선택하면 SSD를 사용하여 만들 수 있는 최대 VM 수를 나타내는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="34f04-129">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="34f04-130">자동 종료 설정</span><span class="sxs-lookup"><span data-stu-id="34f04-130">Set auto-shutdown</span></span>
<span data-ttu-id="34f04-131">자동 종료 정책에서는 이 랩의 VM이 종료되는 시간을 지정하여 랩 낭비를 최소화할 수 있도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="34f04-132">랩의 **구성 및 정책** 블레이드에서 **자동 종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![자동 종료](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="34f04-134">이 정책을 사용하도록 설정하려면 **설정**을 선택하고 사용하지 않도록 설정하려면 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="34f04-135">이 정책을 사용하도록 설정한 경우 현재 랩의 모든 VM을 종료하는 시간(및 표준 시간대)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="34f04-136">지정된 자동 종료 시간 15분 전에 알림을 보내는 옵션으로 **예** 또는 **아니요**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="34f04-137">**예**를 지정한 경우 알림을 받을 웹후크 URL 끝점을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="34f04-138">웹후크에 대한 자세한 내용은 [웹후크 또는 API Azure Function 만들기](../azure-functions/functions-create-a-web-hook-or-api-function.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34f04-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="34f04-139">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-139">Select **Save**.</span></span>

    <span data-ttu-id="34f04-140">기본적으로 이 정책을 사용하도록 설정하면 현재 랩의 모든 VM에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="34f04-141">특정 VM에서 이 설정을 제거하려면 VM의 블레이드를 열고 해당 **자동 종료** 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="34f04-142">자동 시작 설정</span><span class="sxs-lookup"><span data-stu-id="34f04-142">Set auto-start</span></span>
<span data-ttu-id="34f04-143">자동 시작 정책을 사용하면 현재 랩의 VM을 시작할 시기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="34f04-144">랩의 **구성 및 정책** 블레이드에서 **자동 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![자동 시작](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="34f04-146">이 정책을 사용하도록 설정하려면 **설정**을 선택하고 사용하지 않도록 설정하려면 **해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="34f04-147">이 정책을 사용하도록 설정한 경우 예약 시작 시간, 표준 시간대 및 해당 시간이 적용되는 요일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="34f04-148">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-148">Select **Save**.</span></span>

    <span data-ttu-id="34f04-149">사용하도록 설정해도 이 정책이 현재 랩의 VM에 자동으로 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="34f04-150">이 설정을 특정 VM에 적용하려면 VM의 블레이드를 열고 해당 **자동 시작** 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="34f04-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="34f04-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34f04-151">Next steps</span></span>

- <span data-ttu-id="34f04-152">[Azure DevTest Labs에서 랩 정책 정의](devtest-lab-set-lab-policy.md) - 다른 랩 정책을 수정하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="34f04-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
