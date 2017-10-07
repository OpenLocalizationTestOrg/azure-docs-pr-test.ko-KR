---
title: "CLI 스크립트 샘플-aaaAzure 복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>관리 되는 디스크 toosame 또는 CLI 다른 구독 복사

이 스크립트는 관리 되는 디스크 toosame 또는 다른 구독 복사 하지만 동일한 hello 영역입니다. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트를 사용 하 여 다음 명령을 toocreate 사용 하 여 hello 대상 구독에 관리 되는 새 디스크를 hello hello 원본의 Id 디스크를 관리 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Hello 관리 되는 디스크의 hello 이름과 리소스 그룹 속성을 사용 하 여 관리 되는 디스크의 모든 hello 속성을 가져옵니다. Id 속성에 사용 되는 toocopy hello 관리 되는 디스크 toodifferent 구독입니다.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | 관리 되는 디스크 Id 및 이름을 사용 하는 다른 구독에 새 관리 되는 디스크를 만들어 복사 hello 부모 디스크를 관리 합니다.  |

## <a name="next-steps"></a>다음 단계

[관리 디스크에서 가상 컴퓨터 만들기](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
