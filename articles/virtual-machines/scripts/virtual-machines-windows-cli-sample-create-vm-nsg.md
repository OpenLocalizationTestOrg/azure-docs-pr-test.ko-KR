---
title: "CLI 스크립트 샘플-aaaAzure 내부 및 외부 NSG 갖는 두 개의 Vm을 만들 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 내부 및 외부 NSG를 사용하여 두 개의 VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>가상 컴퓨터 간의 네트워크 트래픽 보안

이 스크립트 두 가상 컴퓨터를 만들고 들어오는 트래픽을 tooboth의 보안을 유지 합니다. 인터넷에서 액세스할 수 있는 가상 컴퓨터는 hello 이며가 NSG ()를 네트워크 보안 그룹 구성 tooallow 트래픽 포트 3389와 포트 80에서 합니다. hello 두 번째 가상 컴퓨터에 액세스할 수 없는 인터넷 hello 및에 구성 된 NSG tooonly hello 첫 번째 가상 컴퓨터에서 트래픽을 허용 합니다. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Azure Virtual Network 및 서브넷을 만듭니다. |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | 서브넷을 만듭니다. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다. 이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.  |
| [az network nsg rule update](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | NSG 규칙을 업데이트합니다. 이 샘플에서는 hello 백 엔드 규칙이 업데이트 toopass hello 프런트 엔드 서브넷 에서만에서 트래픽을 통해 되었습니다. |
| [az network nsg rule list](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | 네트워크 보안 그룹 규칙에 대한 정보를 반환합니다. 이 샘플에서는 hello 규칙 이름은 hello 스크립트에서 나중에 사용 하기 위해 변수에 저장 됩니다. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
