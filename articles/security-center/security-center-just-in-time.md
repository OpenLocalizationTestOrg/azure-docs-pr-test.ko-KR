---
title: "Azure Security Center에서 Just-In-Time 가상 컴퓨터 액세스 | Microsoft Docs"
description: "이 문서에서는 Azure Security Center에서 Just-In-Time VM 액세스가 Azure 가상 컴퓨터에 대한 액세스를 제어하는 데 어떻게 도움이 되는지 보여 줍니다."
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
ms.openlocfilehash: 5bb87488dcfc79ed4baa1dbd81dc4e1174f84e4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="00639-103">Just-In-Time를 사용하여 가상 컴퓨터 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="00639-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="00639-104">Just-In-Time VM(가상 컴퓨터) 액세스를 사용하면 Azure VM으로의 인바운드 트래픽을 잠글 수 있어 필요할 때 VM 연결을 위한 간편한 액세스를 제공하면서도 공격에 대한 노출을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-104">Just in time virtual machine (VM) access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="00639-105">Just-In-Time 기능은 미리 보기로 제공되며 Security Center의 표준 계층에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-105">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span>  <span data-ttu-id="00639-106">Security Center의 가격 책정 계층에 대해 자세히 알아보려면 [가격 책정](security-center-pricing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00639-106">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="00639-107">공격 시나리오</span><span class="sxs-lookup"><span data-stu-id="00639-107">Attack scenario</span></span>

<span data-ttu-id="00639-108">무차별 암호 대입 공격(brute force attack)은 일반적으로 VM에 대한 액세스 권한을 얻는 방법으로 관리 포트를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-108">Brute force attacks commonly target management ports as a means to gain access to a VM.</span></span> <span data-ttu-id="00639-109">성공하면 공격자가 VM을 제어할 수 있으며 사용자 환경으로의 발판을 마련하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-109">If successful, an attacker can take control over the VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="00639-110">무차별 암호 대입 공격을 줄이기 위한 한 가지 방법은 포트가 열려 있는 시간의 양을 제한하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00639-110">One way to reduce exposure to a brute force attack is to limit the amount of time that a port is open.</span></span> <span data-ttu-id="00639-111">관리 포트는 항상 열려 있을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-111">Management ports do not need to be open at all times.</span></span> <span data-ttu-id="00639-112">예를 들어 관리 또는 유지 관리 작업을 수행하기 위해 VM에 연결되는 동안에만 열려 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-112">They only need to be open while you are connected to the VM, for example to perform management or maintenance tasks.</span></span> <span data-ttu-id="00639-113">Just-In-Time이 활성화되면 Security Center는 관리 포트에 대한 액세스를 제한하는 [NSG(네트워크 보안 그룹)](../virtual-network/virtual-networks-nsg.md) 규칙을 사용하여 공격자의 대상이 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access to management ports so they cannot be targeted by attackers.</span></span>

![Just-In-Time 시나리오][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="00639-115">Just-In-Time 액세스는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="00639-115">How does just in time access work?</span></span>

<span data-ttu-id="00639-116">Just-In-Time이 활성화되면 Security Center는 NSG 규칙을 만들어 Azure VM으로의 인바운드 트래픽을 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="00639-116">When just in time is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="00639-117">VM에서 인바운드 트래픽을 잠글 포트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-117">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="00639-118">이러한 포트는 Just-In-Time 솔루션에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-118">These ports are controlled by the just in time solution.</span></span>

<span data-ttu-id="00639-119">사용자가 VM에 액세스를 요청하면 Security Center는 해당 사용자에게 Azure 리소스에 대한 쓰기 액세스 권한을 제공하는 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md) 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-119">When a user requests access to a VM, Security Center checks that the user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for the Azure resource.</span></span> <span data-ttu-id="00639-120">쓰기 권한이 있는 경우 요청이 승인되고 Security Center가 지정된 시간 동안 관리 포트로의 인바운드 트래픽을 허용하도록 NSG(네트워크 보안 그룹)을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-120">If they have write permissions, the request is approved and Security Center automatically configures the Network Security Groups (NSGs) to allow inbound traffic to the management ports for the amount of time you specified.</span></span> <span data-ttu-id="00639-121">시간이 만료되면 Security Center에서 NSG를 이전 상태로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-121">After the time has expired, Security Center restores the NSGs to their previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="00639-122">Security Center Just-In-Time VM 액세스는 현재 Azure Resource Manager를 통해 배포된 VM만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="00639-123">클래식 및 Resource Manager 배포 모델에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00639-123">To learn more about the classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="00639-124">Just-In-Time 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="00639-124">Using just in time access</span></span>

<span data-ttu-id="00639-125">**Security Center** 블레이드의 **Just-In-Time VM 액세스** 타일에는 Just-In-Time 액세스에 대해 구성된 VM 수와 지난 주 승인된 액세스 요청 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-125">The **Just in time VM access** tile on the **Security Center** blade shows the number of VMs configured for just in time access and the number of approved access requests made in the last week.</span></span>

<span data-ttu-id="00639-126">**Just-In-Time VM 액세스** 타일을 선택하면 **Just-In-Time VM 액세스** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-126">Select the **Just in time VM access** tile and the **Just in time VM access** blade opens.</span></span>

![Just-In-Time VM 액세스 타일][2]

<span data-ttu-id="00639-128">**Just-In-Time VM 액세스** 블레이드는 VM 상태에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-128">The **Just in time VM access** blade provides information on the state of your VMs:</span></span>

- <span data-ttu-id="00639-129">**구성됨** - Just-In-Time VM 액세스를 지원하도록 구성된 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="00639-129">**Configured** - VMs that have been configured to support just in time VM access.</span></span> <span data-ttu-id="00639-130">표시된 데이터는 지난 주에 대한 데이터이며 각 VM에 대해 승인된 요청 수, 마지막 액세스 날짜 및 시간, 마지막 사용자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-130">The data presented is for the last week and includes for each VM the number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="00639-131">**권장** - Just-In-Time VM 액세스를 지원할 수 있지만 구성되지 않은 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="00639-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="00639-132">이러한 VM에는 Just-In-Time VM 액세스 제어를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="00639-133">[Just-In-Time VM 액세스 사용](#enable-just-in-time-vm-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00639-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="00639-134">**권장 사항 없음** - VM이 권장되지 않을 수 있는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="00639-134">**No recommendation** - Reasons that can cause a VM not to be recommended are:</span></span>
  - <span data-ttu-id="00639-135">누락된 NSG - Just-In-Time 솔루션을 사용하려면 NSG가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-135">Missing NSG - The just in time solution requires an NSG to be in place.</span></span>
  - <span data-ttu-id="00639-136">클래식 VM - Security Center Just-In-Time VM 액세스는 현재 Azure Resource Manager를 통해 배포된 VM만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="00639-137">클래식 배포는 Just-In-Time 솔루션에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-137">A classic deployment is not supported by the just in time solution.</span></span>
  - <span data-ttu-id="00639-138">기타 - Just-In-Time 솔루션이 구독 또는 리소스 그룹의 보안 정책에서 해제되거나 VM에 공용 IP가 없거나 NSG가 없는 경우 VM은 이 범주에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-138">Other - A VM is in this category if the just in time solution is turned off in the security policy of the subscription or the resource group, or that the VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="00639-139">Just-In-Time 액세스 정책 구성</span><span class="sxs-lookup"><span data-stu-id="00639-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="00639-140">사용하도록 설정할 VM을 선택하려면</span><span class="sxs-lookup"><span data-stu-id="00639-140">To select the VMs that you want to enable:</span></span>

1. <span data-ttu-id="00639-141">**Just-In-Time VM 액세스** 블레이드에서 **권장** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-141">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Just-In-Time 액세스 사용][3]

2. <span data-ttu-id="00639-143">**VM** 아래에서 사용하도록 설정할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-143">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="00639-144">그러면 VM 옆에 있는 확인 표시가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-144">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="00639-145">**VM에서 JIT 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="00639-146">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="00639-147">기본 포트</span><span class="sxs-lookup"><span data-stu-id="00639-147">Default ports</span></span>

<span data-ttu-id="00639-148">Security Center에서 Just-In-Time 사용을 권장하는 기본 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-148">You can see the default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="00639-149">**Just-In-Time VM 액세스** 블레이드에서 **권장** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-149">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![기본 포트 표시][6]

2. <span data-ttu-id="00639-151">**VM** 아래에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="00639-152">그러면 VM 옆에 있는 확인 표시가 선택되고 **JIT VM 액세스 구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-152">This puts a checkmark next to the VM and opens the **JIT VM access configuration** blade.</span></span> <span data-ttu-id="00639-153">이 블레이드에 기본 포트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-153">This blade displays the default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="00639-154">포트 추가</span><span class="sxs-lookup"><span data-stu-id="00639-154">Add ports</span></span>

<span data-ttu-id="00639-155">**JIT VM 액세스 구성** 블레이드에서 Just-In-Time 솔루션을 사용하려는 새 포트를 추가 및 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-155">From the **JIT VM access configuration** blade, you can also add and configure a new port on which you want to enable the just in time solution.</span></span>

1. <span data-ttu-id="00639-156">**JIT VM 액세스 구성** 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-156">On the **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="00639-157">그러면 **포트 추가 구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-157">This opens the **Add port configuration** blade.</span></span>

  ![포트 구성][7]

2. <span data-ttu-id="00639-159">**포트 추가 구성** 블레이드에서 포트, 프로토콜 유형, 허용되는 원본 IP 및 최대 요청 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-159">On **Add port configuration** blade, you identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="00639-160">허용되는 원본 IP는 승인된 요청 시 액세스 권한을 얻도록 허용된 IP 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="00639-160">Allowed source IPs are the IP ranges allowed to get access upon an approved request.</span></span>

  <span data-ttu-id="00639-161">최대 요청 시간은 특정 포트를 열 수 있는 최대 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="00639-161">Maximum request time is the maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="00639-162">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-162">Select **OK**.</span></span>

## <a name="requesting-access-to-a-vm"></a><span data-ttu-id="00639-163">VM에 대한 액세스 요청</span><span class="sxs-lookup"><span data-stu-id="00639-163">Requesting access to a VM</span></span>

<span data-ttu-id="00639-164">VM에 대한 액세스를 요청하려면</span><span class="sxs-lookup"><span data-stu-id="00639-164">To request access to a VM:</span></span>

1. <span data-ttu-id="00639-165">**Just-In-Time VM 액세스** 블레이드에서 **구성됨** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-165">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="00639-166">**VM** 아래에서 액세스가 가능하도록 할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-166">Under **VMs**, select the VMs that you want to enable access.</span></span> <span data-ttu-id="00639-167">그러면 VM 옆에 있는 확인 표시가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-167">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="00639-168">**액세스 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-168">Select **Request access**.</span></span> <span data-ttu-id="00639-169">그러면 **액세스 요청** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-169">This opens the **Request access** blade.</span></span>

  ![VM에 대한 액세스 요청][4]

4. <span data-ttu-id="00639-171">**액세스 요청** 블레이드에서 각 VM에 대해, 열어 둘 포트, 포트가 열려 있는 원본 IP 및 포트를 열어 둘 기간을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-171">On the **Request access** blade, you configure for each VM the ports to open along with the source IP that the port is opened to and the time window for which the port is opened.</span></span> <span data-ttu-id="00639-172">Just-In-Time 정책에 구성된 포트에만 액세스를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-172">You can request access only to the ports that are configured in the just in time policy.</span></span> <span data-ttu-id="00639-173">각 포트에는 Just-In-Time 정책에서 파생된 최대 허용된 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-173">Each port has a maximum allowed time derived from the just in time policy.</span></span>
5. <span data-ttu-id="00639-174">**포트 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="00639-175">Just-In-Time 액세스 정책 편집</span><span class="sxs-lookup"><span data-stu-id="00639-175">Editing a just in time access policy</span></span>

<span data-ttu-id="00639-176">해당 VM에 대해 열 새 포트를 추가 및 구성하거나 이미 보호된 포트와 관련된 다른 매개 변수를 변경하여 VM의 기존 Just-In-Time 정책을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-176">You can change a VM's existing just in time policy by adding and configuring a new port to open for that VM, or by changing any other parameter related to an already protected port.</span></span>

<span data-ttu-id="00639-177">VM의 Just-In-Time 정책을 편집하기 위해 **구성됨** 탭이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00639-177">In order to edit an existing just in time policy of a VM, the **Configured** tab is used:</span></span>

1. <span data-ttu-id="00639-178">**VM** 아래에서 해당 VM에 대한 행 안의 3개 점을 클릭하여 포트를 추가할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-178">Under **VMs**, select a VM to add a port to by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="00639-179">그러면 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-179">This opens a menu.</span></span>
2. <span data-ttu-id="00639-180">메뉴에서 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-180">Select **Edit** in the menu.</span></span> <span data-ttu-id="00639-181">그러면 **JIT VM 액세스 구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-181">This opens the **JIT VM access configuration** blade.</span></span>

  ![정책 편집][8]

3. <span data-ttu-id="00639-183">**JIT VM 액세스 구성** 블레이드에서 포트를 클릭하여 이미 보호된 포트의 기존 설정을 편집하거나 **추가**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-183">On the **JIT VM access configuration** blade, you can either edit the existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="00639-184">그러면 **포트 추가 구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-184">This opens the **Add port configuration** blade.</span></span>

  ![포트 추가][7]

4. <span data-ttu-id="00639-186">**포트 추가 구성** 블레이드에서 포트, 프로토콜 유형, 허용되는 원본 IP 및 최대 요청 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-186">On **Add port configuration** blade identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="00639-187">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-187">Select **OK**.</span></span>
6. <span data-ttu-id="00639-188">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="00639-189">Just-In-Time 액세스 활동 감사</span><span class="sxs-lookup"><span data-stu-id="00639-189">Auditing just in time access activity</span></span>

<span data-ttu-id="00639-190">로그 검색을 사용하여 VM 활동에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="00639-191">로그를 보려면</span><span class="sxs-lookup"><span data-stu-id="00639-191">To view logs:</span></span>

1. <span data-ttu-id="00639-192">**Just-In-Time VM 액세스** 블레이드에서 **구성됨** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-192">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="00639-193">**VM** 아래에서 해당 VM에 대한 행 안의 3개 점을 클릭하여 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-193">Under **VMs**, select a VM to view information about by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="00639-194">그러면 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-194">This opens a menu.</span></span>
3. <span data-ttu-id="00639-195">메뉴에서 **활동 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-195">Select **Activity Log** in the menu.</span></span> <span data-ttu-id="00639-196">그러면 **활동 로그** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00639-196">This opens the **Activity log** blade.</span></span>

![활동 로그 선택][9]

<span data-ttu-id="00639-198">**활동 로그** 블레이드는 시간, 날짜 및 구독과 함께 해당 VM에 대한 이전 작업의 필터링된 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-198">The **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![활동 로그 보기][5]

<span data-ttu-id="00639-200">**여기를 클릭하여 모든 항목을 CSV로 다운로드하세요.**를 선택하여 로그 정보를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-200">You can download the log information by selecting **Click here to download all the items as CSV**.</span></span>

<span data-ttu-id="00639-201">필터를 수정하고 **적용**을 선택하여 검색 및 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00639-201">Modify the filters and select **Apply** to create a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="00639-202">PowerShell을 통해 Just-In-Time VM 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="00639-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="00639-203">PowerShell을 통해 Just-In-Time 솔루션을 사용하려면 [최신](/powershell/azure/install-azurerm-ps) 버전의 Azure PowerShell 버전이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-203">In order to use the just in time solution via PowerShell, make sure you have the [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="00639-204">그러면 PowerShell 갤러리에서 [최신](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-204">Once you do, you need to install the [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from the PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="00639-205">VM에 대한 Just-In-Time 정책 구성</span><span class="sxs-lookup"><span data-stu-id="00639-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="00639-206">특정 VM에서 Just-In-Time 정책을 구성하려면 PowerShell 세션에서 Set-ASCJITAccessPolicy 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-206">To configure a just in time policy on a specific VM, you need to run this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="00639-207">cmdlet 설명서에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="00639-207">Follow the cmdlet documentation to learn more.</span></span>

### <a name="requesting-access-to-a-vm"></a><span data-ttu-id="00639-208">VM에 대한 액세스 요청</span><span class="sxs-lookup"><span data-stu-id="00639-208">Requesting access to a VM</span></span>

<span data-ttu-id="00639-209">Just-In-Time 솔루션으로 보호되는 특정 VM에 액세스하려면 PowerShell 세션에서 Invoke-ASCJITAccess를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00639-209">To access a specific VM that is protected with the just in time solution, you need to run this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="00639-210">cmdlet 설명서에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="00639-210">Follow the cmdlet documentation to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00639-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00639-211">Next steps</span></span>
<span data-ttu-id="00639-212">이 문서에서는 Azure Security Center에서 Just-In-Time VM 액세스가 Azure 가상 컴퓨터에 대한 액세스를 제어하는 데 어떻게 도움이 되는지 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-212">In this article, you learned how just in time VM access in Security Center helps you control access to your Azure virtual machines.</span></span>

<span data-ttu-id="00639-213">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00639-213">To learn more about Security Center, see the following:</span></span>

- <span data-ttu-id="00639-214">[보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00639-214">[Setting security policies](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="00639-215">[보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00639-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="00639-216">[보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00639-216">[Security health monitoring](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
- <span data-ttu-id="00639-217">[보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00639-217">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
- <span data-ttu-id="00639-218">[파트너 솔루션 모니터링](security-center-partner-solutions.md) - 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00639-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="00639-219">[보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
- <span data-ttu-id="00639-220">[Azure 보안 블로그](https://blogs.msdn.microsoft.com/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00639-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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
