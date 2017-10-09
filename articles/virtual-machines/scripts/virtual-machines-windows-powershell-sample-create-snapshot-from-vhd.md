---
title: "PowerShell 스크립트 샘플-aaaAzure에서에서 스냅숏을 만들려면 VHD toocreate에서 동일한 여러 개의 관리 되는 디스크 적은 양의 시간 | Microsoft Docs"
description: "Azure PowerShell 스크립트 예제-에서 스냅숏을 만들려면 VHD toocreate에서 동일한 관리 되는 디스크가 여러 적은 양의 시간"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>에서 스냅숏을 만들려면 VHD toocreate에서 동일한 관리 되는 디스크가 여러 적은 양의 PowerShell과 함께 시간

이 스크립트는 같은 구독 또는 다른 구독의 저장소 계정에 VHD 파일의 스냅숏을 만듭니다. 이 스크립트 tooimport 특수 (하지 일반화/sysprepped) VHD tooa 스냅숏 다음와 사용 hello 스냅숏 toocreate 동일한 여러 개의 관리 되는 디스크 작은 양의 시간입니다. 또한 tooimport 데이터 VHD tooa 스냅숏을 사용 하 고 적은 양의 시간 hello 스냅숏 toocreate 여러 관리 되는 디스크를 사용 합니다. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 다음 다른 구독에는 VHD에서 관리 되는 디스크를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | 디스크 만들기에 사용되는 디스크 구성을 만듭니다. 저장소 유형, 위치, 리소스 Id의 hello 부모 VHD 저장 된 hello 저장소 계정 및 hello 부모 VHD의 VHD URI를 포함 합니다. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | 매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다. |

## <a name="next-steps"></a>다음 단계

[스냅숏에서 관리 디스크 만들기](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
