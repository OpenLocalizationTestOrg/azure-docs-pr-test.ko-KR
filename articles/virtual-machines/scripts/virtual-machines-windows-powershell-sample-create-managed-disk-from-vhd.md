---
title: "PowerShell 스크립트 샘플-aaaAzure 동일 하거나 다른 구독에서 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만들 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기"
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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>PowerShell을 사용하여 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기

이 스크립트는 같은 구독 또는 다른 구독의 저장소 계정에 VHD 파일의 관리 디스크를 만듭니다. 이 스크립트 tooimport는 특수화 된 (하지 일반화/sysprepped) VHD toomanaged OS 디스크 toocreate 가상 컴퓨터를 사용 합니다. 또한 tooimport 데이터 VHD toomanaged 데이터 디스크를 사용 합니다. 

VHD 파일에서 단시간에 동일한 관리 디스크를 여러 개 만들지 마세요. toocreate 디스크 vhd 파일에서 관리 되는, hello vhd 파일의 blob 스냅숏이 생성 및 관리 되는 사용 되는 toocreate 디스크 됩니다. 하나의 blob 스냅숏을 만들지 못했습니다. 디스크는 1 분에서 만들 수 있습니다 due toothrottling 합니다. tooavoid 이러한 조절은 만들기는 [hello vhd 파일에서 관리 되는 스냅숏](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) 하 고 사용 하 여 hello 관리 됩니다 스냅숏 toocreate 여러 관리 되는 디스크 짧은 시간 내에 있습니다. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 다음 다른 구독에는 VHD에서 관리 되는 디스크를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | 디스크 만들기에 사용되는 디스크 구성을 만듭니다. 저장소 유형, 위치, 리소스 Id의 hello 저장소 계정 hello 부모 VHD 저장 된 VHD hello 부모의 VHD URI를 포함합니다. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | 매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다. |

## <a name="next-steps"></a>다음 단계

[관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
