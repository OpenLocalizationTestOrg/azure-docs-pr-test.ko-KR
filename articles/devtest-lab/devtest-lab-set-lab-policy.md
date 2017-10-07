---
title: "Azure DevTest Labs에서 aaaManage 랩 정책 | Microsoft Docs"
description: "자세한 내용은 VM과 같은 toodefine 랩 정책 크기, 사용자 당 최대 Vm 하는 방법 및 종료 자동화 합니다."
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
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="85e54-103">Azure DevTest Labs에서 랩에 대한 모든 정책 관리</span><span class="sxs-lookup"><span data-stu-id="85e54-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="85e54-104">Azure DevTest Labs에서는 각 랩의 정책(설정)을 관리하여 랩에서 비용을 관리하고 낭비를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="85e54-105">이 문서에 대 한 단계별 자세히 설명 방법을 tooset 각 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="85e54-106">허용된 가상 컴퓨터 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="85e54-107">hello 설정 hello에 대 한 정책을 허용 toominimize 랩 toospecify hello 랩에는 VM 크기는 사용할 수 있도록 하 여 낭비 하는 VM 크기는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="85e54-108">이 정책은 인증 된 경우이 목록에서 VM 크기만 사용된 toocreate Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="85e54-109">Hello 랩에 **구성 및 정책** 블레이드를 **가상 컴퓨터 크기를 허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![허용된 가상 컴퓨터 크기](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="85e54-111">선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="85e54-112">이 정책을 사용하도록 설정한 경우 랩에서 만들 수 있는 하나 이상의 VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="85e54-113">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="85e54-114">사용자당 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-114">Set virtual machines per user</span></span>
<span data-ttu-id="85e54-115">에 대 한 정책을 hello **사용자 당 가상 컴퓨터** toospecify hello 최대 개별 사용자가 만들 수 있는 Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="85e54-116">경우 사용자가 toocreate 또는 클레임 VM hello 사용자도 충족 될 경우에 오류 메시지가 표시 되는 해당 hello VM 생성/을 요구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="85e54-117">Hello 랩에 **구성 및 정책** 메뉴 선택 **사용자 당 가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![사용자당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="85e54-119">선택 **예** Vm 사용자 당 toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="85e54-120">Vm 사용자 당 toolimit hello 수 하지 않으려면 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="85e54-121">선택 하는 경우 **예**, hello를 만들거나 사용자가 소유 하는 Vm의 최대 수를 나타내는 숫자 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="85e54-122">선택 **예** SSD (반도체 디스크)를 사용할 수 있는 Vm toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="85e54-123">SSD를 사용할 수 있는 Vm toolimit hello 수 하지 않으려면 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="85e54-124">선택 하는 경우 **예**, hello SSD를 사용 하 여 만들 수 있는 Vm의 최대 수를 나타내는 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="85e54-125">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="85e54-126">랩당 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-126">Set virtual machines per lab</span></span>
<span data-ttu-id="85e54-127">에 대 한 정책을 hello **랩 당 가상 컴퓨터** hello 현재 랩에 대 한 hello toospecify 만들 수 있는 Vm의 최대 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="85e54-128">사용자가 VM toocreate hello 랩 제한을 충족 될 경우에 경우 오류 메시지가 표시 되는 해당 hello VM을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="85e54-129">Hello 랩에 **구성 및 정책** 메뉴 선택 **랩 당 가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![랩당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="85e54-131">선택 **예** Vm 랩 당 toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="85e54-132">Vm 당 랩 toolimit hello 수 하지 않으려면 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="85e54-133">선택 하는 경우 **예**, hello를 만들거나 사용자가 소유 하는 Vm의 최대 수를 나타내는 숫자 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="85e54-134">선택 **예** SSD (반도체 디스크)를 사용할 수 있는 Vm toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="85e54-135">SSD를 사용할 수 있는 Vm toolimit hello 수 하지 않으려면 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="85e54-136">선택 하는 경우 **예**, hello SSD를 사용 하 여 만들 수 있는 Vm의 최대 수를 나타내는 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="85e54-137">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="85e54-138">자동 종료 설정</span><span class="sxs-lookup"><span data-stu-id="85e54-138">Set auto-shutdown</span></span>
<span data-ttu-id="85e54-139">hello 자동 종료 정책을 toominimize 랩이이 랩의이 Vm을 종료 하는 toospecify hello 시간을 허용 하 여 낭비를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="85e54-140">Hello 랩에 **구성 및 정책** 블레이드를 **자동 종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![자동 종료](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="85e54-142">선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="85e54-143">이 정책을 사용 하는 경우 모든 Vm 아래로 hello 시간 (및 표준 시간대) tooshut hello 현재 랩에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="85e54-144">지정 **예** 또는 **아니요** 알림 15 분 이전 toohello 옵션 toosend hello에 대 한 자동 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="85e54-145">지정 하는 경우 **예**, webhook URL 끝점 tooreceive hello 알림을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="85e54-146">웹후크에 대한 자세한 내용은 [웹후크 또는 API Azure Function 만들기](../azure-functions/functions-create-a-web-hook-or-api-function.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85e54-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="85e54-147">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-147">Select **Save**.</span></span>

    <span data-ttu-id="85e54-148">기본적으로 활성화 되어 있는 경우,이 정책은 tooall Vm hello 현재 랩에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="85e54-149">tooremove가 특정 VM에서이 설정을 열고 hello VM 블레이드 및 변경의 **자동 종료** 설정</span><span class="sxs-lookup"><span data-stu-id="85e54-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="85e54-150">자동 시작 설정</span><span class="sxs-lookup"><span data-stu-id="85e54-150">Set auto-start</span></span>
<span data-ttu-id="85e54-151">hello 자동 시작 정책은 있도록 toospecify hello 현재 랩에 hello Vm을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="85e54-152">Hello 랩에 **구성 및 정책** 블레이드를 **자동 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![자동 시작](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="85e54-154">선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="85e54-155">이 정책을 사용 하면 예약 된 hello 시작 시간, 표준 시간대 및 시간에 적용 되는 hello에 대 한 hello 주의 hello 일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="85e54-156">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-156">Select **Save**.</span></span>

    <span data-ttu-id="85e54-157">사용할 수 있는 경우이 정책은에 없는 경우 자동으로 적용 된 tooany Vm hello 현재 랩</span><span class="sxs-lookup"><span data-stu-id="85e54-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="85e54-158">tooapply이 설정은 tooa 특정 VM, 열기 hello VM 블레이드 및 변경의 **자동 시작** 설정</span><span class="sxs-lookup"><span data-stu-id="85e54-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="85e54-159">만료 날짜 설정</span><span class="sxs-lookup"><span data-stu-id="85e54-159">Set expiration date</span></span>
<span data-ttu-id="85e54-160">만료 날짜를 설정할 수 있습니다 날짜 있습니다 [hello VM을 만들](devtest-lab-add-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="85e54-161">**고급 설정**, 선택 hello 달력 아이콘 toospecify hello VM에 날짜를 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="85e54-162">기본적으로 VM hello 만료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="85e54-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85e54-163">Next steps</span></span>
<span data-ttu-id="85e54-164">정의 하 고 적용 되 면 hello 랩에 대 한 다양 한 VM 정책 설정, 다음 일부의 tootry 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="85e54-165">[IP 주소를 공유 이해](devtest-lab-shared-ip.md) -어떻게 공유 IP에 설명 주소는 공용 IP 주소가 필요한 tooconnect tooyour 랩 Vm의 DevTest Labs toominimize hello 번호에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="85e54-166">[비용 관리 구성](devtest-lab-configure-cost-management.md) -에서는 방법을 toouse hello **월별 예상 비용 추세** 차트</span><span class="sxs-lookup"><span data-stu-id="85e54-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="85e54-167">tooview 현재 달의 예상된 비용 누계와 프로젝션 hello 월말의 비용 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="85e54-168">[사용자 지정 이미지 만들기](devtest-lab-create-template.md) - VM을 만들 때 사용자 지정 이미지 또는 마켓플레이스 이미지 중에서 기본 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="85e54-169">이 문서에서는 어떻게 toocreate 사용자 지정은 VHD 파일에서을 이미지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="85e54-170">[마켓플레이스 이미지 구성](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs에서 Azure Marketplace 이미지에 기반하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="85e54-171">이 문서에서는 설명 방법을 toospecify Azure 마켓플레이스 이미지 될 수 있는 경우 있는 환경에서 Vm을 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="85e54-172">[랩에서 VM 만들기](devtest-lab-add-vm-with-artifacts.md) -보여 줍니다 방법을 toocreate 기본 이미지에서 VM (어느 사용자 지정 또는 마켓플레이스), 방법과 VM의 아티팩트로 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e54-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

