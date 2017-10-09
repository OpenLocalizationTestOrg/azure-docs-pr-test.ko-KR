---
title: "CLI 스크립트 샘플-aaaAzure 스냅숏에서 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 스냅숏에서 VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a>CLI를 사용하여 스냅숏에서 가상 컴퓨터 만들기

이 스크립트는 OS 디스크의 스냅숏에서 가상 컴퓨터를 만듭니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 있는 관리 되는 디스크, 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | 스냅숏 이름 및 리소스 그룹 이름을 사용하여 스냅숏을 가져옵니다. Id의 개체를 반환 하는 hello 속성이 사용 되는 관리 되는 디스크 toocreate입니다.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | 스냅숏 Id, 디스크 이름, 저장소 유형 및 크기를 사용하여 스냅숏에서 관리 디스크를 만듭니다.  |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 관리 OS 디스크를 사용하여 VM을 만듭니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
