---
title: "Azure에서 Windows 가상 컴퓨터 다시 배포 | Microsoft Docs"
description: "RDP 연결 문제를 완화하도록 Azure에서 Windows 가상 컴퓨터를 다시 배포하는 방법입니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: a607d0747f64ee6b224d300113905f54e003aef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a><span data-ttu-id="d719b-103">새 Azure 노드로 Windows 가상 컴퓨터 다시 배포</span><span class="sxs-lookup"><span data-stu-id="d719b-103">Redeploy Windows virtual machine to new Azure node</span></span>
<span data-ttu-id="d719b-104">RDP(원격 데스크톱) 연결 문제 또는 Windows 기반 Azure VM(가상 컴퓨터)에 대한 응용 프로그램 액세스 문제를 해결하는 데 어려움이 있는 경우 VM을 다시 배포하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span></span> <span data-ttu-id="d719b-105">VM을 다시 배포하면 VM이 Azure 인프라 내의 새 노드로 이동된 다음 전원이 켜지고, 모든 구성 옵션 및 관련 리소스는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="d719b-106">이 문서에서는 Azure PowerShell 또는 Azure 포털을 사용하여 VM을 다시 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d719b-107">VM을 다시 배포한 후에 임시 디스크가 손실되고 가상 네트워크 인터페이스와 연결된 동적 IP 주소가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="d719b-108">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="d719b-108">Using Azure PowerShell</span></span>
<span data-ttu-id="d719b-109">최신 Azure PowerShell 1.x를 컴퓨터에 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="d719b-110">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d719b-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d719b-111">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="d719b-112">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d719b-112">Next steps</span></span>
<span data-ttu-id="d719b-113">VM에 연결하는 데 문제가 있는 경우 [RDP 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [자세한 RDP 문제 해결 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 특정 도움말을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d719b-114">VM에서 실행 중인 응용 프로그램에 액세스할 수 없는 경우 [응용 프로그램 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 읽어볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d719b-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

