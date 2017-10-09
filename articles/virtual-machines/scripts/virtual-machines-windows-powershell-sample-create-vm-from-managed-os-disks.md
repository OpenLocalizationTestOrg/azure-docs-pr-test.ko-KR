---
title: "PowerShell 스크립트 샘플-aaaAzure 운영 체제 디스크와 관리 되는 디스크를 연결 하 여 VM 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 관리 디스크를 OS 디스크로 연결하여 VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a>PowerShell과 기존 관리 OS 디스크를 사용하여 가상 컴퓨터 만들기

이 스크립트는 기존 관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다. 이전 시나리오에서는 이 스크립트를 사용합니다.
* 다른 구독의 관리 디스크에서 복사된 기존의 관리 OS 디스크에서 VM 만들기
* 특수화된 VHD 파일에서 만든 기존 관리 디스크에서 VM 만들기 
* 스냅숏에서 만든 기존의 관리 OS 디스크에서 VM 만들기 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 tooget 관리 되는 디스크 속성을 다음 hello를 사용 하 여, 관리 되는 디스크 tooa 연결 새 VM 및 VM을 만듭니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [Get-AzureRmDisk](/powershell/module/azurerm.compute/Get-AzureRmDisk) | Hello 이름 및 디스크의 hello 리소스 그룹에 따라 디스크 개체를 가져옵니다. Hello의 id 속성 디스크 개체를 사용 하는 tooattach hello 디스크 tooa 반환 된 새 VM |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | VM 구성을 만듭니다. 이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다. hello 구성은 VM 만드는 동안 사용 됩니다. |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) | OS 디스크 tooa 새 가상 컴퓨터로 hello 디스크의 hello Id 속성을 사용 하 여 관리 되는 디스크 연결 |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | 공용 IP 주소를 만듭니다. |
| [새-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | 네트워크 인터페이스를 만듭니다. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | 가상 컴퓨터를 만듭니다. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 리소스 그룹 및 포함된 모든 리소스를 제거합니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
