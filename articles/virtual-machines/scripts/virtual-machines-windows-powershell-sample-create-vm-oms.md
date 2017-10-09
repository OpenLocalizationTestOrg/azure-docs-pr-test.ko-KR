---
title: "PowerShell 스크립트 샘플-aaaAzure OMS | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - OMS"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="80f25-103">PowerShell로 Operations Management Suite 모니터링 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="80f25-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="80f25-104">Azure 가상 컴퓨터를 만들고 hello Operations Management Suite (OMS) 에이전트를 설치 hello 시스템 OMS 작업 영역을 등록 하는이 스크립트 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="80f25-105">Hello 스크립트 실행 되 면 hello 가상 컴퓨터 hello OMS 콘솔에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="80f25-106">또한 tooupdate는 hello OMS 작업 영역 ID와 작업 영역 키를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="80f25-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="80f25-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="80f25-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="80f25-108">Clean up deployment</span></span> 

<span data-ttu-id="80f25-109">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="80f25-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="80f25-110">Script explanation</span></span>

<span data-ttu-id="80f25-111">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="80f25-112">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="80f25-113">명령</span><span class="sxs-lookup"><span data-stu-id="80f25-113">Command</span></span> | <span data-ttu-id="80f25-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="80f25-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80f25-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="80f25-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="80f25-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="80f25-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="80f25-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="80f25-118">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-118">Creates a subnet configuration.</span></span> <span data-ttu-id="80f25-119">이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="80f25-120">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="80f25-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="80f25-121">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="80f25-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="80f25-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="80f25-123">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="80f25-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="80f25-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="80f25-125">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="80f25-126">이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="80f25-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="80f25-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="80f25-128">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="80f25-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="80f25-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="80f25-130">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-130">Gets subnet information.</span></span> <span data-ttu-id="80f25-131">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="80f25-132">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="80f25-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="80f25-133">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="80f25-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="80f25-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="80f25-135">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-135">Creates a VM configuration.</span></span> <span data-ttu-id="80f25-136">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="80f25-137">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="80f25-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="80f25-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="80f25-139">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="80f25-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="80f25-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="80f25-141">VM 확장 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="80f25-142">이 경우 Operations Management Suite 에이전트 확장 hello 사용 되는 tooinstall hello OMS 에이전트 되며 hello OMS 작업 영역에서 VM을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="80f25-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="80f25-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="80f25-144">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80f25-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80f25-145">Next steps</span></span>

<span data-ttu-id="80f25-146">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="80f25-147">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="80f25-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
