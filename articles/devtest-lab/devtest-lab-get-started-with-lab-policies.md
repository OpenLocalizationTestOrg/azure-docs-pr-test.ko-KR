---
title: "Azure DevTest Labs에서 aaaManage 기본 랩 정책 | Microsoft Docs"
description: "자세한 내용은 방법 tooset DevTest Labs에 랩에 대 한 hello 기본 정책 (설정)의 일부"
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
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f77c0-103">Azure DevTest Labs에서 랩에 대한 기본 정책 관리</span><span class="sxs-lookup"><span data-stu-id="f77c0-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="f77c0-104">Azure DevTest Labs toocontrol 비용 수 있고 각 랩에 대 한 정책 설정 ()를 관리 하 여 환경에서 낭비를 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="f77c0-105">이 문서에서는 있습니다 정책 시작 방법을 tooset hello 가장 중요 정책-제한의 두 hello 수가 학습 하 여 생성 또는 한 명의 사용자와 구성 자동 종료에서 요구 될 수 있는 가상 컴퓨터 (VM).</span><span class="sxs-lookup"><span data-stu-id="f77c0-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="f77c0-106">tooview 어떻게 tooset 모든 랩 정책 hello 문서 참조 [Azure DevTest Labs에 랩 정책을 정의](devtest-lab-set-lab-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="f77c0-107">Azure DevTest Labs의 랩 정책에 액세스</span><span class="sxs-lookup"><span data-stu-id="f77c0-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="f77c0-108">hello 다음 단계를 안내 합니다 Azure DevTest Labs에 랩에 대 한 정책 설정.</span><span class="sxs-lookup"><span data-stu-id="f77c0-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="f77c0-109">랩에 대 한 hello 정책 tooview (및 변경) 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f77c0-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="f77c0-110">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="f77c0-111">선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="f77c0-112">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="f77c0-113">**구성 및 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-113">Select **Configuration and policies**.</span></span>

    ![정책 설정 블레이드](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="f77c0-115">hello **구성 및 정책** 블레이드 지정할 수 있는 설정의 메뉴를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="f77c0-116">이 문서에서는 대 한 hello 설정만 **사용자 당 가상 컴퓨터** 및 **자동 종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="f77c0-117">toolearn 설정을 남은 hello에 대 한 참조 [Azure DevTest Labs에 랩에 대 한 모든 정책을 관리](./devtest-lab-set-lab-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="f77c0-118">사용자당 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-118">Set virtual machines per user</span></span>
<span data-ttu-id="f77c0-119">에 대 한 정책을 hello **사용자 당 가상 컴퓨터** toospecify hello 최대 개별 사용자가 만들 수 있는 Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="f77c0-120">경우 사용자가 toocreate 또는 클레임 VM hello 사용자도 충족 될 경우에 오류 메시지가 표시 되는 해당 hello VM 생성/을 요구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="f77c0-121">Hello 랩에 **구성 및 정책** 메뉴 선택 **사용자 당 가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![사용자당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="f77c0-123">선택 **예** Vm 사용자 당 toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="f77c0-124">Vm 사용자 당 toolimit hello 수 하지 않으려면 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="f77c0-125">선택 하는 경우 **예**, hello를 만들거나 사용자가 소유 하는 Vm의 최대 수를 나타내는 숫자 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="f77c0-126">선택 **예** SSD (반도체 디스크)를 사용할 수 있는 Vm toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="f77c0-127">SSD를 사용할 수 있는 Vm toolimit hello 수 하지 않으려면 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="f77c0-128">선택 하는 경우 **예**, hello SSD를 사용 하 여 만들 수 있는 Vm의 최대 수를 나타내는 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="f77c0-129">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="f77c0-130">자동 종료 설정</span><span class="sxs-lookup"><span data-stu-id="f77c0-130">Set auto-shutdown</span></span>
<span data-ttu-id="f77c0-131">hello 자동 종료 정책을 toominimize 랩이이 랩의이 Vm을 종료 하는 toospecify hello 시간을 허용 하 여 낭비를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="f77c0-132">Hello 랩에 **구성 및 정책** 블레이드를 **자동 종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![자동 종료](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="f77c0-134">선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="f77c0-135">이 정책을 사용 하는 경우 모든 Vm 아래로 hello 시간 (및 표준 시간대) tooshut hello 현재 랩에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="f77c0-136">지정 **예** 또는 **아니요** 알림 15 분 이전 toohello 옵션 toosend hello에 대 한 자동 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="f77c0-137">지정 하는 경우 **예**, webhook URL 끝점 tooreceive hello 알림을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="f77c0-138">웹후크에 대한 자세한 내용은 [웹후크 또는 API Azure Function 만들기](../azure-functions/functions-create-a-web-hook-or-api-function.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f77c0-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="f77c0-139">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-139">Select **Save**.</span></span>

    <span data-ttu-id="f77c0-140">기본적으로 활성화 되어 있는 경우,이 정책은 tooall Vm hello 현재 랩에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="f77c0-141">tooremove가 특정 VM에서이 설정을 열고 hello VM 블레이드 및 변경의 **자동 종료** 설정</span><span class="sxs-lookup"><span data-stu-id="f77c0-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="f77c0-142">자동 시작 설정</span><span class="sxs-lookup"><span data-stu-id="f77c0-142">Set auto-start</span></span>
<span data-ttu-id="f77c0-143">hello 자동 시작 정책은 있도록 toospecify hello 현재 랩에 hello Vm을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="f77c0-144">Hello 랩에 **구성 및 정책** 블레이드를 **자동 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![자동 시작](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="f77c0-146">선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="f77c0-147">이 정책을 사용 하면 예약 된 hello 시작 시간, 표준 시간대 및 시간에 적용 되는 hello에 대 한 hello 주의 hello 일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="f77c0-148">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f77c0-148">Select **Save**.</span></span>

    <span data-ttu-id="f77c0-149">사용할 수 있는 경우이 정책은에 없는 경우 자동으로 적용 된 tooany Vm hello 현재 랩</span><span class="sxs-lookup"><span data-stu-id="f77c0-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="f77c0-150">tooapply이 설정은 tooa 특정 VM, 열기 hello VM 블레이드 및 변경의 **자동 시작** 설정</span><span class="sxs-lookup"><span data-stu-id="f77c0-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f77c0-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f77c0-151">Next steps</span></span>

- <span data-ttu-id="f77c0-152">[Azure DevTest Labs에 랩 정책을 정의](devtest-lab-set-lab-policy.md) -자세한 방법을 toomodify 다른 랩 정책</span><span class="sxs-lookup"><span data-stu-id="f77c0-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
