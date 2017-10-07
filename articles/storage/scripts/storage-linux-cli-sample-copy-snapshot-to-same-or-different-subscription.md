---
title: "CLI 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독과 CLI의 복사본 (이동) 스냅숏 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독과 CLI의 스냅숏 복사 (이동)"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>관리 되는 디스크 toosame 또는 다른 구독과 CLI의 스냅숏을 복사합니다

이 스크립트는 관리 되는 디스크 toosame 또는 다른 구독에 대 한 스냅숏을 복사합니다. 이 스크립트 toomove 스냅숏 toodifferent 구독을 사용 하 여 hello에 hello 부모 스냅숏의와 동일한 영역입니다.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 다음 사용 하 여 사용 하 여 hello 대상 구독에서 스냅숏 hello hello 소스 스냅숏의 Id입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | 모든 hello 속성의 hello 이름을 사용 하 여 스냅숏 및 hello 스냅숏의 리소스 그룹 속성을 가져옵니다. Id 속성은 사용 되는 toocopy hello 스냅숏 toodifferent 구독.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | 복사본의 Id 및 이름을 사용 하 여 다른 구독에서 스냅숏을 만들어 스냅숏 hello hello 부모 스냅숏의 합니다.  |

## <a name="next-steps"></a>다음 단계

[스냅숏에서 가상 컴퓨터 만들기](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
