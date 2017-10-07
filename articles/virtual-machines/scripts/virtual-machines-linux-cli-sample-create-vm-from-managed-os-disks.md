---
title: "aaaAzure CLI 스크립트 샘플-운영 체제 디스크와 관리 되는 디스크를 연결 하 여 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 관리 디스크를 OS 디스크로 연결하여 VM 만들기"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>CLI와 기존 관리 OS 디스크를 사용하여 가상 컴퓨터 만들기

이 스크립트는 기존 관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다. 이전 시나리오에서는 이 스크립트를 사용합니다.
* 다른 구독의 관리 디스크에서 복사된 기존의 관리 OS 디스크에서 VM 만들기
* 특수화된 VHD 파일에서 만든 기존 관리 디스크에서 VM 만들기 
* 스냅숏에서 만든 기존의 관리 OS 디스크에서 VM 만들기 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 tooget 관리 되는 디스크 속성을 다음 hello를 사용 하 여, 관리 되는 디스크 tooa 연결 새 VM 및 VM을 만듭니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | 디스크 이름 및 리소스 그룹 이름을 사용하여 관리 디스크 속성을 가져옵니다. Id 속성은 관리 되는 디스크 tooa tooattach를 사용 하는 새 VM |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 관리 OS 디스크를 사용하여 VM을 만듭니다. |
## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
