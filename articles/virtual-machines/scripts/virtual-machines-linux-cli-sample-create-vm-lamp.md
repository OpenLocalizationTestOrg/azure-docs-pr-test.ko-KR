---
title: "CLI 스크립트 샘플-aaaAzure hello Load-Balanced 가상 Machin 크기 집합의 LAMP 스택 배포 | Microsoft Docs"
description: "사용자 지정 스크립트 확장 toodeploy hello LAMP 스택 부하에서를 사용 하 여 Azure에서 설정 하는 분산 된 가상 컴퓨터 크기 = 합니다."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>부하 분산 된 가상 컴퓨터 크기 집합의 hello LAMP 스택 배포

이 예제에서는 가상 컴퓨터 크기 집합을 만들고 hello 크기 집합의 각 가상 컴퓨터에서 사용자 지정 스크립트 toodeploy hello LAMP 스택을 실행 하는 확장을 적용 합니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>연결

이 코드 toosee tooconnect tooyour Vm 및 눈금 설정 하는 방법을 사용 합니다.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, hello 크기 집합, Vm 및 관련 된 모든 리소스 따라를 실행 합니다.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | 가상 컴퓨터 확장 집합을 만듭니다. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 부하가 분산된 끝점을 추가합니다. |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | VM의 배포에서 hello 사용자 지정 스크립트를 실행 하는 hello 확장 만들기 |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Hello 확장 적용 하기 전에 배포 된 hello VM 인스턴스에서 hello 사용자 지정 스크립트를 실행 toohello 크기 집합입니다. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | Hello에 크기 집합 VM 인스턴스를 더 추가 하 여 확장 합니다. hello 사용자 지정 스크립트는 배포 하는 경우 이러한 이벤트에 대해 실행 됩니다. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Hello hello 샘플에서 만들어진 Vm의 hello IP 주소를 가져옵니다. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Hello 프런트 엔드 및 백 엔드 hello 부하 분산 장치에서 사용 하는 포트를 가져옵니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
