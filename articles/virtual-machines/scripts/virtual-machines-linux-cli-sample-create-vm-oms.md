---
title: "CLI 스크립트 샘플-aaaAzure OMS 모니터링과 함께 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - OMS 모니터링을 사용하여 Linux VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7a329d4f90a20e0e11faa1f5cafd0701574dc440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a>Operations Management Suite를 사용하여 VM 모니터링

Azure 가상 컴퓨터를 만들고 hello Operations Management Suite (OMS) 에이전트를 설치 hello 시스템 OMS 작업 영역을 등록 하는이 스크립트 합니다. Hello 스크립트 실행 되 면 hello 가상 컴퓨터 hello OMS 콘솔에 표시 됩니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다. 이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.  |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | 가상 컴퓨터에 대한 VM 확장을 실행합니다. 이 경우 Operations Management Suite 에이전트 확장 hello 사용 되는 tooinstall hello OMS 에이전트 되며 hello OMS 작업 영역에서 VM을 등록 합니다. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
