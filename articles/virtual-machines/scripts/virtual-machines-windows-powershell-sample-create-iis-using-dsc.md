---
title: "PowerShell 스크립트 샘플-aaaAzure dsc IIS | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - DSC를 사용하는 IIS"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: ef855bf92ef7b0fd07466527bc5f71f688e150fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a>PowerShell을 사용하여 IIS VM 만들기

이 스크립트는 Windows Server 2016을 실행 하는 Azure 가상 컴퓨터 만들고 hello Azure 가상 컴퓨터 DSC 확장 tooinstall IIS를 사용 하 여 합니다. Hello 스크립트를 실행 한 후 hello 기본 IIS 웹 사이트 hello hello 가상 컴퓨터의 공용 IP 주소에 액세스할 수 있습니다.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | 서브넷 구성을 만듭니다. 이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다. |
| [새-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | 가상 네트워크를 만듭니다. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | 공용 IP 주소를 만듭니다. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | 네트워크 보안 그룹 규칙 구성을 만듭니다. 이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | 네트워크 보안 그룹을 만듭니다. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | 서브넷 정보를 가져옵니다. 이 정보는 네트워크 인터페이스를 만들 때 사용됩니다. |
| [새-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | 네트워크 인터페이스를 만듭니다. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | VM 구성을 만듭니다. 이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다. hello 구성은 VM 만드는 동안 사용 됩니다. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | 가상 컴퓨터를 만듭니다. |
| [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) | VM 확장 toohello 가상 컴퓨터를 추가 합니다. 이 샘플에서 hello 사용자 지정 스크립트 확장 사용 되는 tooinstall IIS는 합니다. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 리소스 그룹 및 포함된 모든 리소스를 제거합니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
