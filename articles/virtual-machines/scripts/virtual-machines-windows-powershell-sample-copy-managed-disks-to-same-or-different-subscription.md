---
title: "PowerShell 스크립트 샘플-aaaAzure 복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a>관리 되는 복사본에에서 디스크를 hello 동일 구독 또는 PowerShell과 함께 다른 구독

이 스크립트는 hello에 기존의 관리 되는 디스크의 복사본을 만듭니다 동일한 구독 또는 다른 구독 합니다. hello 디스크가 새로 만들어집니다 hello에 동일 지역 hello 부모 디스크를 관리 합니다.   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트를 사용 하 여 다음 명령을 toocreate 사용 하 여 hello 대상 구독에 관리 되는 새 디스크를 hello hello 원본의 Id 디스크를 관리 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | 디스크 만들기에 사용되는 디스크 구성을 만듭니다. Hello 리소스 Id hello 부모 디스크와 부모 디스크의 hello 위치과 같은 위치를 포함 합니다.  |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | 매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다. |


## <a name="next-steps"></a>다음 단계

[관리 디스크에서 가상 컴퓨터 만들기](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
