---
title: "aaaManage 끝점 Azure 액세스 제어 목록 | PowerShell | 클래식 | Microsoft Docs"
description: "자세한 내용은 방법 toomanage Acl powershell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="c8349-103">PowerShell을 사용 하 여 hello 클래식 배포 모델에서 끝점 액세스 제어 목록 관리</span><span class="sxs-lookup"><span data-stu-id="c8349-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="c8349-104">수 만들고 hello 관리 포털 또는 Azure PowerShell을 사용 하 여 서식 끝점에 대 한 네트워크 액세스 제어 목록 (Acl)을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="c8349-105">이 항목에서는 PowerShell을 사용하여 완료할 수 있는 ACL 공통 작업의 절차에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="c8349-106">Hello 목록은 Azure PowerShell cmdlet 참조 [Azure 관리 Cmdlet](http://go.microsoft.com/fwlink/?LinkId=317721)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="c8349-107">ACL에 대한 자세한 내용은 [네트워크 ACL(액세스 제어 목록)이란?](virtual-networks-acl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8349-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="c8349-108">Hello 관리 포털을 사용 하 여 Acl toomanage 경우 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="c8349-109">Azure PowerShell을 사용하여 네트워크 ACL 관리</span><span class="sxs-lookup"><span data-stu-id="c8349-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="c8349-110">Azure PowerShell cmdlet toocreate를 사용할 수 있습니다 제거 (set)를 구성 및 네트워크 액세스 제어 목록 (Acl).</span><span class="sxs-lookup"><span data-stu-id="c8349-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="c8349-111">PowerShell을 사용 하 여 ACL을 구성 하는 hello 방법 중 일부의 몇 가지 예가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="c8349-112">hello ACL PowerShell cmdlet의 전체 목록은 tooretrieve hello 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="c8349-113">원격 서브넷의 액세스를 허용하는 규칙이 있는 네트워크 ACL 만들기</span><span class="sxs-lookup"><span data-stu-id="c8349-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="c8349-114">다음 예제에서는 hello 방식으로 toocreate를 규칙이 포함 된 새 ACL을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="c8349-115">그런 다음이 ACL이 적용 됩니다 tooa 가상 컴퓨터 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="c8349-116">아래의 hello 예에서 hello ACL 규칙에서 원격 서브넷의에서 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="c8349-117">원격 서브넷에 대 한 허용 규칙이 포함 된 새 네트워크 ACL toocreate Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="c8349-118">복사를 원하는 값으로 hello 스크립트 구성 아래 hello 스크립트를 붙여 넣고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="c8349-119">Hello 새로운 네트워크 ACL 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="c8349-120">원격 서브넷에서의 액세스를 허용하는 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="c8349-121">규칙을 설정 하면 아래 hello 예제에서 *100* (200 이상의 규칙을 통해 있는 우선 순위) tooallow hello 원격 서브넷 *10.0.0.0/8* toohello 가상 컴퓨터 끝점에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="c8349-122">사용자 고유의 구성 요구 사항과 함께 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="c8349-123">hello 이름이 "SharePoint ACL config" 한다고 toocall이이 규칙 hello 알기 쉬운 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="c8349-124">추가 규칙에 대 한 hello cmdlet, 사용자 고유의 구성 요구 사항과 함께 hello 값 대체를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="c8349-125">있는지 toochange hello 규칙 번호 순서 tooreflect hello 순서 hello 규칙 toobe 적용 하려는 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="c8349-126">hello 낮은 규칙 번호가 hello 더 높은 숫자 보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="c8349-127">다음으로 새 끝점 (추가)을 만들 하거나 기존 끝점 (Set)에 대 한 hello ACL을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="c8349-128">이 예제에서는 새 가상 컴퓨터 끝점을 호출 hello로 업데이트 하 고 "웹" hello 가상 컴퓨터 끝점 ACL 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="c8349-129">다음으로 hello cmdlet을 조합 하 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="c8349-130">예를 들어 hello 조합 된 cmdlet은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="c8349-131">원격 서브넷의 액세스를 허용하는 네트워크 ACL 규칙 제거</span><span class="sxs-lookup"><span data-stu-id="c8349-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="c8349-132">다음 예제에서는 hello 방식으로 tooremove를 네트워크 ACL 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="c8349-133">허용 된 네트워크 ACL 규칙 tooremove 규칙 원격 서브넷에 대 한 Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="c8349-134">복사를 원하는 값으로 hello 스크립트 구성 아래 hello 스크립트를 붙여 넣고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="c8349-135">첫 번째 단계는 hello 가상 컴퓨터 끝점에 대 한 tooget hello 네트워크 ACL 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="c8349-136">그런 다음 hello ACL 규칙을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="c8349-137">이 경우 규칙 ID를 기준으로 규칙을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="c8349-138">이렇게 하면만 제거 hello 규칙 ID 0 hello ACL에서.</span><span class="sxs-lookup"><span data-stu-id="c8349-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="c8349-139">Hello 가상 컴퓨터 끝점에서 hello ACL 개체를 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="c8349-140">다음으로 hello 네트워크 ACL 개체 toohello 가상 컴퓨터 끝점을 적용 하 고 hello 가상 컴퓨터를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="c8349-141">가상 컴퓨터 끝점에서 네트워크 ACL 제거</span><span class="sxs-lookup"><span data-stu-id="c8349-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="c8349-142">특정 시나리오에서 가상 컴퓨터 끝점에서 네트워크 ACL 개체 tooremove를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="c8349-143">Azure PowerShell ISE를 열고 있는 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="c8349-144">복사를 원하는 값으로 hello 스크립트 구성 아래 hello 스크립트를 붙여 넣고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8349-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="c8349-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8349-145">Next steps</span></span>
[<span data-ttu-id="c8349-146">네트워크 ACL(액세스 제어 목록)이란?</span><span class="sxs-lookup"><span data-stu-id="c8349-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

