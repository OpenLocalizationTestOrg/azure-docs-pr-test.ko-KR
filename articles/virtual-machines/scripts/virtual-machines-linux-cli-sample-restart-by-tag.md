---
title: "Vm 다시 시작 스크립트 샘플 CLI-aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 태그 및 ID로 VM 다시 시작"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>VM 다시 시작

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

이 샘플 몇 가지 방법으로 tooget 일부 Vm을 표시 하 고 다시 시작 합니다.

처음 hello hello 리소스 그룹에 모든 hello Vm 다시 시작 합니다.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

hello 두 번째 가져옵니다 hello 태그가 지정 된 사용 하 여 Vm `az resouce list` 및 vm을 toohello 리소스를 필터링 하 고 해당 Vm을 다시 시작 합니다.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

이 샘플은 Bash 셸에서 작동합니다. Windows 클라이언트에서 Azure CLI 스크립트를 실행 하는 옵션에 대 한 참조 [hello Azure CLI Windows에서 실행 중인](../windows/cli-options.md)합니다.


## <a name="sample-script"></a>샘플 스크립트

hello 샘플에는 세 가지 스크립트에 있습니다.
첫 번째 hello 가상 컴퓨터를 프로비저닝하고 hello 합니다.
Hello 명령은 각 VM toobe 프로 비전에 대기 하지 않고 반환 하므로 hello 아니요 대기 옵션을 사용 합니다.
두 번째 hello hello Vm toobe 완전히 프로 비전을 기다립니다.
세 번째 스크립트 hello를 프로 비전 된 모든 hello Vm 다시 시작 하 고 정당한 hello 태그가 Vm을 지정 하는 다음 합니다.

### <a name="provision-hello-vms"></a>Hello Vm을 프로 비전

이 스크립트 리소스 그룹을 만들고 세 개의 Vm toorestart 만드는 합니다.
그 중 두 개의 VM에 태그가 지정됩니다.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Wait

이 스크립트는 hello tooprovision 실패 둘 중 하나 또는 모두 세 개의 Vm이 프로 비전 될 때까지 20 초 마다 프로 비전 상태를 확인 합니다.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Hello Vm을 다시 시작

이 스크립트는 모든 hello Vm hello 리소스 그룹에서 다시 시작 하 고 방금 hello 태그가 지정 된 Vm을 다시 시작 합니다.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, Vm 및 관련 된 모든 리소스를 수 있습니다.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hello 가상 컴퓨터를 만듭니다.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | 함께 사용할 `--query` tooensure hello Vm을 다시 시작 하기 전에 프로 비전 하 고 다음 tooget hello hello Vm toorestart의 Id를 해당 합니다. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | 함께 사용할 `--query` tooget hello hello 태그를 사용 하 여 hello Vm의 Id입니다. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Hello Vm을 다시 시작합니다. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
