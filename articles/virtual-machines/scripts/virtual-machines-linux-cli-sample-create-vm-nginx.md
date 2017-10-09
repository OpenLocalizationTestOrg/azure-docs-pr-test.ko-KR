---
title: "CLI 스크립트 샘플-aaaAzure NGINX Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - NGINX를 사용하여 Linux VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>NGINX를 사용하여 VM 만들기

이 스크립트는 Azure 가상 컴퓨터를 만들고 Azure 가상 컴퓨터 사용자 지정 스크립트 확장 tooinstall NGINX hello를 사용 하 여 합니다. Hello 스크립트를 실행 한 후 hello hello 가상 컴퓨터의 공용 IP 주소에서 데모 웹 사이트를 액세스할 수 있습니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>사용자 지정 스크립트 확장

사용자 지정 스크립트 확장 hello hello 가상 컴퓨터에이 스크립트를 복사합니다. hello 스크립트 tooinstall 그런 다음를 실행 하 고 NGINX 웹 서버를 구성 합니다. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

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
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Hello 가상 컴퓨터를 만듭니다. 이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | 네트워크 보안 그룹 규칙 tooallow 만듭니다 트래픽 인바운드 합니다. 이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | 추가 하 고 가상 컴퓨터 확장 tooa VM을 실행 합니다. 이 샘플에서는 hello 사용자 지정 스크립트 확장 사용 되는 tooinstall NGINX 됩니다.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
