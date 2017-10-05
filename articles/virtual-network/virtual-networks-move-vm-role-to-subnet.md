---
title: "VM(클래식) 또는 Cloud Services 역할 인스턴스를 다른 서브넷으로 이동 - Azure PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 VM(클래식) 및 Cloud Services 역할 인스턴스를 다른 서브넷으로 이동하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="cc758-103">PowerShell을 사용하여 VM(클래식) 또는 Cloud Services 역할 인스턴스를 다른 서브넷으로 이동</span><span class="sxs-lookup"><span data-stu-id="cc758-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="cc758-104">PowerShell을 사용하여 동일한 가상 네트워크(VNet)에 있는 한 서브넷에서 다른 서브넷으로 VM(클래식)을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="cc758-105">PowerShell을 사용하지 않고 CSCFG 파일을 편집하여 역할 인스턴스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="cc758-106">이 문서에서는 클래식 배포 모델을 통해서만 배포된 VM을 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="cc758-107">다른 서브넷으로 VM을 이동하는 이유</span><span class="sxs-lookup"><span data-stu-id="cc758-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="cc758-108">서브넷 마이그레이션은 기존 서브넷이 너무 작고 해당 서브넷에서 실행 중인 기존 VM으로 인해 확장할 수 없는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="cc758-109">이 경우 새로운, 더 큰 서브넷을 만들고 새 서브넷으로 VM을 마이그레이션한 다음 마이그레이션이 완료된 후 이전의 빈 서브넷을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="cc758-110">다른 서브넷으로 VM을 이동하는 방법</span><span class="sxs-lookup"><span data-stu-id="cc758-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="cc758-111">VM을 이동하려면 아래 예를 템플릿으로 사용하여 Set-AzureSubnet PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="cc758-112">아래 예제에서는 현재 서브넷에서 Subnet-2로 TestVM을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="cc758-113">사용 중인 환경에 맞게 예를 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="cc758-114">절차의 일부로 Update-AzureVM cmdlet을 실행할 때마다 VM이 업데이트 프로세스의 일환으로 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="cc758-115">VM에 대한 고정 내부 개인 IP를 지정한 경우 먼저 해당 설정을 제거해야 새 서브넷으로 VM을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="cc758-116">이 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="cc758-117">다른 서브넷으로 역할 인스턴스를 이동하려면</span><span class="sxs-lookup"><span data-stu-id="cc758-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="cc758-118">역할 인스턴스를 이동하려면 CSCFG 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="cc758-119">아래 예제에서는 가상 네트워크 *VNETName*의 "Role0"을 현재 서브넷에서 *Subnet-2*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="cc758-120">역할 인스턴스가 이미 배포되었기 때문에 서브넷 이름 = Subnet-2를 변경하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="cc758-121">사용 중인 환경에 맞게 예를 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc758-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
