---
title: "aaaAzure CLI 스크립트 샘플-VHD와 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 가상 하드 디스크를 사용하여 VM 만들기."
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>가상 하드 디스크를 사용하여 VM 만들기

이 예제는 VHD를 사용하여 가상 컴퓨터를 만듭니다.
리소스 그룹, 저장소 계정 및 컨테이너를 생성 한 다음 hello VHD toohello 컨테이너를 업로드 하 여 VM을 만듭니다.
대체 hello ssh 공용 액세스 toohello VM 수 있도록 공개 키로 키입니다.

부팅 가능 VHD가 필요합니다.
Https://azclisamples.blob.core.windows.net/vhds/sample.vhd에서 hello 사용 된 VHD를 다운로드 하거나 사용자 고유의 VHD를 사용할 수 있습니다. 이 스크립트 hello `~/sample.vhd`합니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | 저장소 계정을 나열합니다. |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | 저장소 계정 이름이 유효하고 이미 존재하는 계정인지 확인합니다. |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Hello 저장소 계정에 대 한 키를 나열합니다. |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Hello blob의 존재 여부 확인 |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | 저장소 계정으로 컨테이너를 만듭니다. |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | VHD 업로드 hello 여 hello 컨테이너에 blob을 만듭니다. |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | 함께 사용할 `--query` hello VM 이름을 사용 중인지 확인 합니다. | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hello 가상 컴퓨터를 만듭니다. |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Hello SSH 키 toogive hello 현재 사용자 액세스 toohello VM을 다시 설정합니다. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Hello 생성 된 VM의 hello IP 주소를 가져옵니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
