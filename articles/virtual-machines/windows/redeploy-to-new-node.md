---
title: "Azure의 aaaRedeploy Windows 가상 컴퓨터 | Microsoft Docs"
description: "어떻게 Azure toomitigate RDP 연결의 tooredeploy Windows 가상 컴퓨터를 발급 합니다."
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
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="7d0cc-103">Windows 가상 컴퓨터 toonew Azure 노드를 다시 배포</span><span class="sxs-lookup"><span data-stu-id="7d0cc-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="7d0cc-104">문제가 연결 된 경우 원격 데스크톱 (RDP) 문제 해결 연결 또는 응용 프로그램에 액세스할 tooWindows 기반 Azure 가상 컴퓨터 (VM) 재배포 hello VM 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="7d0cc-105">VM을 다시 배포할 때 hello VM tooa hello Azure 인프라 내에서 새 노드를 이동 하 고에 다시 모든 구성 옵션 및 관련된 리소스 그대로 유지 하 고 구동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="7d0cc-106">이 문서에서는 어떻게 hello Azure 포털 또는 Azure PowerShell을 사용 하 여 VM a tooredeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7d0cc-107">VM을 다시 배포 후에 hello 임시 디스크 손실 되 고 가상 네트워크 인터페이스와 연결 된 동적 IP 주소는 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="7d0cc-108">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="7d0cc-108">Using Azure PowerShell</span></span>
<span data-ttu-id="7d0cc-109">최신 Azure PowerShell hello가 있는지 확인 1.x 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="7d0cc-110">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7d0cc-111">hello 다음 예제에서는 배포 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7d0cc-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="7d0cc-112">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d0cc-112">Next steps</span></span>
<span data-ttu-id="7d0cc-113">Tooyour VM을 연결 하는 데 문제가 있는 경우에 특별 한 도움말을 찾을 수 있습니다 [RDP 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [RDP 문제 해결 단계를 자세히](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7d0cc-114">VM에서 실행 중인 응용 프로그램에 액세스할 수 없는 경우 [응용 프로그램 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 읽어볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d0cc-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

