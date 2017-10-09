---
title: "Azure 보안 센터에서 aaaJust 시간 가상 컴퓨터에 액세스 | Microsoft Docs"
description: "이 문서를 안내해 어떻게 just-in-time Azure 보안 센터를 통해 제어할 수에서 VM 액세스 액세스 tooyour Azure 가상 컴퓨터."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="6ea7e-103">Just-In-Time를 사용하여 가상 컴퓨터 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="6ea7e-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="6ea7e-104">시간 가상 컴퓨터 (VM)에 액세스는 인바운드 트래픽 tooyour Azure Vm에서 쉽게 액세스할 수 있도록 tooconnect tooVMs 필요할 때 제공 하는 동안 노출 tooattacks 감소를 사용 하는 toolock 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea7e-105">시간 기능에만 있는 hello 되며 미리 보기에서 hello 보안 센터의 표준 계층에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="6ea7e-106">참조 [가격 책정](security-center-pricing.md) 보안 센터에 대해 자세히 toolearn 가격 책정 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="6ea7e-107">공격 시나리오</span><span class="sxs-lookup"><span data-stu-id="6ea7e-107">Attack scenario</span></span>

<span data-ttu-id="6ea7e-108">무차별 암호 대입 공격 수단 toogain 액세스 tooa VM으로 일반적으로 대상 관리 포트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="6ea7e-109">성공 하면 공격자 hello VM에 대 한 제어를 수행할를 업데이트 하 고 한 발판을 마련 환경으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="6ea7e-110">한 가지 방법은 tooreduce 노출 tooa 무차별 암호 대입 공격은 toolimit hello의 포트가 열려 있는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="6ea7e-111">관리 포트가 언제 든 toobe 열기는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="6ea7e-112">Toobe만 해야 하는 동안 열려는 연결 된 VM을 예를 들어 tooperform toohello 관리 또는 유지 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="6ea7e-113">보안 센터를 사용 하는 just-in-time에서 활성화 되 면 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 공격자가 대상으로 지정할 수 있도록 액세스 toomanagement 포트를 제한 하는 (NSG) 규칙을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Just-In-Time 시나리오][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="6ea7e-115">Just-In-Time 액세스는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="6ea7e-115">How does just in time access work?</span></span>

<span data-ttu-id="6ea7e-116">Just-in-time에서 활성화 되 면 NSG 규칙을 만들어 보안 센터 인바운드 트래픽 tooyour Azure Vm 아래로 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="6ea7e-117">Hello 포트 선택 hello VM toowhich에 인바운드 트래픽을 잠기는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="6ea7e-118">이러한 포트는 hello 시간 솔루션에만 있는 것으로 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="6ea7e-119">보안 센터 해당 hello 사용자가을 확인 한 사용자 액세스 tooa VM를 요청 하면 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md) hello Azure 리소스에 대 한 쓰기 액세스를 제공 하는 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="6ea7e-120">인바운드 트래픽 toohello 관리 포트 지정 된 시간을 양의 hello에 대 한 쓰기 권한이 있는, hello 요청이 승인 되 고 보안 센터 (Nsg) 네트워크 보안 그룹 tooallow hello를 자동으로 구성 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="6ea7e-121">Hello 시간 기간이 만료 되 면 보안 센터 hello Nsg tootheir 이전 상태로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea7e-122">Security Center Just-In-Time VM 액세스는 현재 Azure Resource Manager를 통해 배포된 VM만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="6ea7e-123">클래식 hello 및 리소스 관리자 배포 모델에 대 한 자세한 참조 toolearn [Azure 리소스 관리자 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="6ea7e-124">Just-In-Time 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="6ea7e-124">Using just in time access</span></span>

<span data-ttu-id="6ea7e-125">hello **VM 액세스 시간에에서만** hello에 바둑판식으로 배열 **보안 센터** 블레이드 지난주 hello에 대 한 액세스 승인 된 요청 시간 액세스 및 hello 수에만 있는 것에 대해 구성 된 Vm의 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="6ea7e-126">선택 hello **VM 액세스 시간에에서만** 타일 및 hello **VM 액세스 시간에에서만** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Just-In-Time VM 액세스 타일][2]

<span data-ttu-id="6ea7e-128">hello **VM 액세스 시간에에서만** 블레이드 Vm의 hello 상태에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="6ea7e-129">**구성** -VM 액세스 시간에만 구성 된 toosupport 상태인 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="6ea7e-130">표시 되는 hello 데이터 hello 지난 주에 대 한 이며 승인 된 요청, 마지막 사용 날짜 및 시간 및 마지막 사용자의 각 VM hello 번호에 대 한 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="6ea7e-131">**권장** - Just-In-Time VM 액세스를 지원할 수 있지만 구성되지 않은 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="6ea7e-132">이러한 VM에는 Just-In-Time VM 액세스 제어를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="6ea7e-133">[Just-In-Time VM 액세스 사용](#enable-just-in-time-vm-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="6ea7e-134">**권장 사항 없음** -권장 toobe 하지 VM을 일으킬 수 있는 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="6ea7e-135">NSG-시간 솔루션에만 있는 hello 누락 된 위치에는 NSG toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="6ea7e-136">클래식 VM - Security Center Just-In-Time VM 액세스는 현재 Azure Resource Manager를 통해 배포된 VM만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="6ea7e-137">클래식 배포 시간 솔루션에만 있는 hello에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="6ea7e-138">다른-VM 하나 공용 IP 없습니다 아니며 위치에서 NSG를 포함 하지 않는 솔루션 hello 구독 또는 hello 리소스 그룹의 보안 정책을 hello 꺼져 just-in-time에서 hello 또는 해당 hello VM이이 범주에는.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="6ea7e-139">Just-In-Time 액세스 정책 구성</span><span class="sxs-lookup"><span data-stu-id="6ea7e-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="6ea7e-140">tooselect hello tooenable 원하는 Vm:</span><span class="sxs-lookup"><span data-stu-id="6ea7e-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="6ea7e-141">Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **권장** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Just-In-Time 액세스 사용][3]

2. <span data-ttu-id="6ea7e-143">아래 **Vm**, 원하는 tooenable hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="6ea7e-144">확인 표시 다음 tooa VM을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="6ea7e-145">**VM에서 JIT 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="6ea7e-146">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="6ea7e-147">기본 포트</span><span class="sxs-lookup"><span data-stu-id="6ea7e-147">Default ports</span></span>

<span data-ttu-id="6ea7e-148">보안 센터는 적시에 사용 하도록 권장 되는 hello 기본 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="6ea7e-149">Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **권장** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![기본 포트 표시][6]

2. <span data-ttu-id="6ea7e-151">**VM** 아래에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="6ea7e-152">이렇게 하면 추가 확인 표시가 다음 toohello VM과 열립니다 hello **JIT VM 액세스 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="6ea7e-153">이 블레이드는 hello 기본 포트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="6ea7e-154">포트 추가</span><span class="sxs-lookup"><span data-stu-id="6ea7e-154">Add ports</span></span>

<span data-ttu-id="6ea7e-155">Hello에서 **JIT VM 액세스 구성** 블레이드를 추가 하 고 수도 있습니다 tooenable hello 시간 솔루션에만 있는 것을 원하는 새 포트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="6ea7e-156">Hello에 **JIT VM 액세스 구성** 블레이드를 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="6ea7e-157">Hello 열립니다 **포트 구성 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-157">This opens hello **Add port configuration** blade.</span></span>

  ![포트 구성][7]

2. <span data-ttu-id="6ea7e-159">**포트 구성 추가** 허용 Ip, 소스 및 최대 요청 시간 hello 포트, 프로토콜 종류를 식별 블레이드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="6ea7e-160">승인 된 요청에 따라 hello IP 범위 허용된 tooget 액세스는 원본 Ip 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="6ea7e-161">최대 요청 시간은 hello 최대 시간 창은 특정 포트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="6ea7e-162">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="6ea7e-163">VM 액세스 tooa 요청</span><span class="sxs-lookup"><span data-stu-id="6ea7e-163">Requesting access tooa VM</span></span>

<span data-ttu-id="6ea7e-164">toorequest 액세스 tooa VM:</span><span class="sxs-lookup"><span data-stu-id="6ea7e-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="6ea7e-165">Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **자동 구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="6ea7e-166">아래 **Vm**, tooenable 액세스 해야 하는 hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="6ea7e-167">확인 표시 다음 tooa VM을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="6ea7e-168">**액세스 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-168">Select **Request access**.</span></span> <span data-ttu-id="6ea7e-169">Hello 열립니다 **액세스 권한을 요청** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-169">This opens hello **Request access** blade.</span></span>

  ![요청 액세스 tooa VM][4]

4. <span data-ttu-id="6ea7e-171">Hello에 **액세스 권한을 요청** hello 포트는 hello 원본 IP와 함께 각 VM hello 포트 tooopen는 hello에 대 한 포트를 열지 tooand hello 시간 창을 열에 대 한 구성 블레이드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="6ea7e-172">시간 정책에만 있는 hello에 구성 된 액세스만 toohello 포트를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="6ea7e-173">각 포트에 시간 정책에만 있는 hello에서 파생 된 최대 허용된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="6ea7e-174">**포트 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="6ea7e-175">Just-In-Time 액세스 정책 편집</span><span class="sxs-lookup"><span data-stu-id="6ea7e-175">Editing a just in time access policy</span></span>

<span data-ttu-id="6ea7e-176">VM의 시간 정책에 추가 하 고 해당 VM에 대 한 새 포트 tooopen를 구성 하 여 기존를 변경 하거나 다른 매개 변수를 변경 하 여 관련된 tooan 이미 보호 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="6ea7e-177">주문 tooedit에서 기존 VM의 시간 정책에만 hello **자동 구성** 탭을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="6ea7e-178">아래 **Vm**를 해당 VM에 대 한 hello 행 내에서 hello 세 점을 클릭 하면 포트 tooby VM tooadd를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="6ea7e-179">그러면 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-179">This opens a menu.</span></span>
2. <span data-ttu-id="6ea7e-180">선택 **편집** hello 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="6ea7e-181">Hello 열립니다 **JIT VM 액세스 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![정책 편집][8]

3. <span data-ttu-id="6ea7e-183">Hello에 **JIT VM 액세스 구성** 블레이드에서 해당 포트를 클릭 하 여 hello 이미 보호 된 포트의 기존 설정을 편집 하거나 하거나 선택할 수 있습니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="6ea7e-184">Hello 열립니다 **포트 구성 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-184">This opens hello **Add port configuration** blade.</span></span>

  ![포트 추가][7]

4. <span data-ttu-id="6ea7e-186">**포트 구성 추가** 블레이드 hello 포트, 프로토콜 종류, 허용 된 Ip, 소스 및 최대 요청 시간을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="6ea7e-187">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-187">Select **OK**.</span></span>
6. <span data-ttu-id="6ea7e-188">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="6ea7e-189">Just-In-Time 액세스 활동 감사</span><span class="sxs-lookup"><span data-stu-id="6ea7e-189">Auditing just in time access activity</span></span>

<span data-ttu-id="6ea7e-190">로그 검색을 사용하여 VM 활동에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="6ea7e-191">tooview 로그:</span><span class="sxs-lookup"><span data-stu-id="6ea7e-191">tooview logs:</span></span>

1. <span data-ttu-id="6ea7e-192">Hello에 **VM 액세스 시간에에서만** 블레이드, 선택 hello **자동 구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="6ea7e-193">아래 **Vm**를 해당 VM에 대 한 hello 행 내에서 hello 세 점을 클릭 하 여에 대 한 VM tooview 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="6ea7e-194">그러면 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-194">This opens a menu.</span></span>
3. <span data-ttu-id="6ea7e-195">선택 **활동 로그** hello 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="6ea7e-196">Hello 열립니다 **활동 로그** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-196">This opens hello **Activity log** blade.</span></span>

![활동 로그 선택][9]

<span data-ttu-id="6ea7e-198">hello **활동 로그** 블레이드 시간, 날짜 및 구독 함께 해당 VM에 대 한 이전 작업의 필터링된 된 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![활동 로그 보기][5]

<span data-ttu-id="6ea7e-200">선택 하 여 hello 로그 정보를 다운로드할 수 **여기 toodownload 모든 항목을 클릭 hello CSV로**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="6ea7e-201">Hello 필터를 수정 하 고 선택 **적용** toocreate 로그와으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="6ea7e-202">PowerShell을 통해 Just-In-Time VM 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="6ea7e-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="6ea7e-203">PowerShell 통해 시간 솔루션에만 순서 toouse hello에서 hello 있는지 확인 [최신](/powershell/azure/install-azurerm-ps) Azure PowerShell 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="6ea7e-204">Tooinstall hello 이렇게 해야 [최신](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) hello PowerShell 갤러리에서 Azure 보안 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="6ea7e-205">VM에 대한 Just-In-Time 정책 구성</span><span class="sxs-lookup"><span data-stu-id="6ea7e-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="6ea7e-206">tooconfigure just가 특정 VM에 시간 정책에 필요한 toorun이이 명령은 PowerShell 세션에서: ASCJITAccessPolicy 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="6ea7e-207">Hello cmdlet 설명서 toolearn 자세한를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="6ea7e-208">VM 액세스 tooa 요청</span><span class="sxs-lookup"><span data-stu-id="6ea7e-208">Requesting access tooa VM</span></span>

<span data-ttu-id="6ea7e-209">로 보호 되는 특정 VM tooaccess 시간 솔루션에만 있는 hello, PowerShell 세션에서 toorun이이 명령은 필요: ASCJITAccess 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="6ea7e-210">Hello cmdlet 설명서 toolearn 자세한를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ea7e-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ea7e-211">Next steps</span></span>
<span data-ttu-id="6ea7e-212">이 문서에서 배운 어떻게 just-in-time 보안 센터를 사용 하면 VM 액세스 액세스 tooyour Azure 제어 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="6ea7e-213">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="6ea7e-214">[보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="6ea7e-215">[보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="6ea7e-216">[보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="6ea7e-217">[관리 및 toosecurity 경고 응답](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="6ea7e-218">[파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="6ea7e-219">[보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="6ea7e-220">[Azure 보안 블로그](https://blogs.msdn.microsoft.com/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea7e-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
