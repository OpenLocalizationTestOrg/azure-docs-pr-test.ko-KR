---
title: "PowerShell 스크립트 샘플-aaaAzure 다층 계층 응용 프로그램에 대 한 네트워크 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 다중 계층 응용 프로그램을 위한 가상 네트워크를 만듭니다."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>다중 계층 응용 프로그램을 위한 네트워크 만들기

이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다. 트래픽 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP 및 SSH, 트래픽 toohello 하는 동안 백 엔드 서브넷은 제한 된 tooMySQL, 3306 포트입니다. Hello 스크립트를 실행 한 후 웹 서버 및 MySQL 소프트웨어를 배포할 수 있는 각 서브넷에 각각 하나씩 두 개의 가상 컴퓨터가 해야 합니다.

필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다. Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [새-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | 백 엔드 서브넷을 만듭니다. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다. |
| [새-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | 가상 네트워크 인터페이스를 만들고 toohello 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결 합니다. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | 네트워크 보안 그룹 (NSG) 관련된 toohello 프런트 엔드 및 백 엔드 서브넷을 만듭니다. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |NSG 규칙을 허용 하거나 차단할 toospecific 서브넷 특정 포트를 만듭니다. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | 가상 컴퓨터를 만들고 NIC tooeach VM을 연결 합니다. 이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.

추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.
