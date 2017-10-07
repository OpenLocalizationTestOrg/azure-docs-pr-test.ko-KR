---
title: "aaaAzure CLI 스크립트 샘플-Docker 호스트 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Docker 호스트 만들기"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a>Docker를 사용하여 VM 만들기

이 스크립트는 Docker를 사용하는 가상 컴퓨터를 만들고 Docker 컨테이너에서 NGINX를 실행하기 시작합니다. Hello 스크립트를 실행 한 후 hello NGINX 웹 서버 hello hello Azure 가상 컴퓨터의 FQDN 통해 액세스할 수 있습니다. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹을 연결 합니다. 이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/vm#open-port) | 네트워크 보안 그룹 규칙 tooallow 만듭니다 트래픽 인바운드 합니다. 이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | 추가 하 고 가상 컴퓨터 확장 tooa VM을 실행 합니다. 이 샘플에서는 hello Docker VM 확장은 사용 되는 tooconfigure Docker 호스트입니다.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
