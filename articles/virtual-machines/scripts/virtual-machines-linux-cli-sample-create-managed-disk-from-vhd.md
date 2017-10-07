---
title: "CLI 스크립트 샘플-aaaAzure hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만드는 구독과 동일한 구독 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만들려면 동일한 구독"
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만들 CLI와 동일한 구독

이 스크립트는 hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만듭니다 동일한 구독 합니다. 이 스크립트 tooimport는 특수화 된 (하지 일반화/sysprepped) VHD toomanaged OS 디스크 toocreate 가상 컴퓨터를 사용 합니다. 또는 tooimport 데이터 VHD toomanaged 데이터 디스크를 사용 하세요. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 다음 VHD에서 관리 되는 디스크를 사용합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | VHD의 URI를 사용 하 여 hello의 저장소 계정에 관리 되는 디스크를 만듭니다 동일한 구독 |

## <a name="next-steps"></a>다음 단계

[관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
