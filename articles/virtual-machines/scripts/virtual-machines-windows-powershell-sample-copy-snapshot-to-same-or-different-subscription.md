---
title: "PowerShell 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독 복사 (이동) 스냅숏 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독 복사 (이동) 스냅숏"
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>PowerShell을 사용하여 같은 구독 또는 다른 구독에 관리 디스크의 스냅숏 복사

이 스크립트는 hello에는 스냅숏의 복사본을 만듭니다 같은 동일한 구독 또는 다른 구독 합니다. 데이터 보관을 위해이 스크립트 toomove 스냅숏 toodifferent 구독을 사용 합니다. 다른 구독에 스냅숏을 저장하여 기본 구독에서 스냅숏을 실수로 삭제하지 않도록 합니다. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 다음 사용 하 여 사용 하 여 hello 대상 구독에서 스냅숏 hello hello 소스 스냅숏의 Id입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmSnapshotConfig](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | 스냅숏 생성에 사용되는 스냅숏 구성을 만듭니다. Hello 리소스 hello 부모 스냅숏과 hello 부모 스냅숏의과 같은 위치 Id를 포함 합니다.  |
| [New-AzureRmSnapshot](/powershell/module/azurerm.compute/New-AzureRmDisk) | 매개 변수로 전달된 스냅숏 구성, 스냅숏 이름 및 리소스 그룹 이름을 사용하여 스냅숏을 만듭니다. |


## <a name="next-steps"></a>다음 단계

[스냅숏에서 가상 컴퓨터 만들기](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
