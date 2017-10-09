---
title: "PowerShell 스크립트 샘플-다른 지역의 VHD tooa 저장소 계정으로 내보내기/복사 스냅숏 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-동일한 서로 다른 지역에 VHD tooa 저장소 계정으로 내보내기/복사 스냅숏"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>PowerShell과 함께 다른 지역에 VHD tooa 저장소 계정으로 관리 되는 스냅숏 내보내기/복사

이 스크립트는 관리 되는 스냅숏 tooa 저장소 계정을 다른 지역에 내보냅니다. 먼저 hello hello 스냅숏의 SAS URI를 생성 하 고 다음 toocopy 사용 것 tooa 다른 지역의 저장소 계정입니다. 재해 복구를 위해 다른 지역에이 스크립트 toomaintain 백업을 관리 되는 디스크를 사용 합니다.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>스크립트 설명

다음 명령을 toogenerate 사용 하 여 관리 되는 스냅숏 및 복사본이 hello에 대 한 SAS URI 스냅숏 tooa 저장소 계정의 SAS URI를 사용 하 여이 스크립트입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | 사용 되는 toocopy 된 스냅숏을 대 한 SAS URI를 생성 하기 tooa 저장소 계정입니다. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Hello 계정 이름과 키를 사용 하 여 저장소 계정 컨텍스트를 만듭니다. 이 컨텍스트는 hello 저장소 계정에서 사용 되는 tooperform 읽기/쓰기 작업 수 있습니다. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | 복사본 hello 스냅숏 tooa 저장소 계정의 기본 VHD |

## <a name="next-steps"></a>다음 단계

[VHD에서 관리 디스크 만들기](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[관리 디스크에서 가상 컴퓨터 만들기](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
