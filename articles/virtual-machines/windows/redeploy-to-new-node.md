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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Windows 가상 컴퓨터 toonew Azure 노드를 다시 배포
문제가 연결 된 경우 원격 데스크톱 (RDP) 문제 해결 연결 또는 응용 프로그램에 액세스할 tooWindows 기반 Azure 가상 컴퓨터 (VM) 재배포 hello VM 도움이 될 수 있습니다. VM을 다시 배포할 때 hello VM tooa hello Azure 인프라 내에서 새 노드를 이동 하 고에 다시 모든 구성 옵션 및 관련된 리소스 그대로 유지 하 고 구동 합니다. 이 문서에서는 어떻게 hello Azure 포털 또는 Azure PowerShell을 사용 하 여 VM a tooredeploy 합니다.

> [!NOTE]
> VM을 다시 배포 후에 hello 임시 디스크 손실 되 고 가상 네트워크 인터페이스와 연결 된 동적 IP 주소는 업데이트 됩니다. 


## <a name="using-azure-powershell"></a>Azure PowerShell 사용
최신 Azure PowerShell hello가 있는지 확인 1.x 컴퓨터에 설치 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

hello 다음 예제에서는 배포 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>다음 단계
Tooyour VM을 연결 하는 데 문제가 있는 경우에 특별 한 도움말을 찾을 수 있습니다 [RDP 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [RDP 문제 해결 단계를 자세히](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. VM에서 실행 중인 응용 프로그램에 액세스할 수 없는 경우 [응용 프로그램 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 읽어볼 수도 있습니다.

