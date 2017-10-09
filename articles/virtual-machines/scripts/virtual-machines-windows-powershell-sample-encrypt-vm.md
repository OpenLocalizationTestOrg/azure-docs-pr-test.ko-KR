---
title: "Windows VM을 암호화 하는 PowerShell 스크립트 샘플-aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Windows VM 암호화"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a>Azure PowerShell을 사용하여 Windows 가상 컴퓨터 암호화

이 스크립트는 보안 Azure Key Vault, 암호화 키, Azure Active Directory 서비스 주체 및 Windows VM(가상 컴퓨터)을 만듭니다. 그런 다음 VM hello 암호화 키를 키 자격 증명 모음 및 서비스 사용자 자격 증명 제공 hello를 사용 하 여 암호화 됩니다.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

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
| [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | 암호화 키와 같은 Azure 키 자격 증명 모음 toostore 보안 데이터를 만듭니다. |
| [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | Key Vault에서 암호화 키를 만듭니다. |
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Azure Active Directory 서비스를 인증 하 고 tooencryption 키 액세스를 제어 하는 주 toosecurely 만듭니다. |
| [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | Hello 서비스 보안 주체 액세스 tooencryption 키 hello 키 자격 증명 모음 toogrant에 사용 권한을 설정합니다. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | 서브넷 구성을 만듭니다. 이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다. |
| [새-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | 가상 네트워크를 만듭니다. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | 공용 IP 주소를 만듭니다. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | 네트워크 보안 그룹 규칙 구성을 만듭니다. 이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | 네트워크 보안 그룹을 만듭니다. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | 서브넷 정보를 가져옵니다. 이 정보는 네트워크 인터페이스를 만들 때 사용됩니다. |
| [새-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | 네트워크 인터페이스를 만듭니다. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | VM 구성을 만듭니다. 이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다. hello 구성은 VM 만드는 동안 사용 됩니다. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | 가상 컴퓨터를 만듭니다. |
| [Get-AzureRmKeyVault](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | Hello 키 자격 증명 모음에 필요한 정보를 가져옵니다 |
| [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | Hello 서비스 사용자 자격 증명 및 암호화 키를 사용 하는 VM에서 암호화를 설정 합니다. |
| [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | Hello hello VM 암호화 프로세스 상태가 표시 됩니다. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 리소스 그룹 및 포함된 모든 리소스를 제거합니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
