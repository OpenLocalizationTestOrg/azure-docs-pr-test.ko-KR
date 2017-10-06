---
title: "CLI 스크립트 샘플-운영 체제 디스크를 탑재 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 운영 체제 디스크 탑재"
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
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>VM 운영 체제 디스크 문제 해결

이 스크립트를 데이터 디스크 tooa 두 번째 가상 컴퓨터로 실패 했거나 문제가 있는 가상 컴퓨터의 hello 운영 체제 디스크를 탑재합니다. 디스크 문제를 해결하거나 데이터를 복구할 때 유용할 수 있습니다. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | 가상 컴퓨터 목록을 반환합니다. 이 경우 hello 쿼리 옵션에 사용 되는 tooreturn hello 가상 컴퓨터 운영 체제 디스크입니다. 이 값 tooa 변수 이름 'uri' 추가 됩니다. |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | 가상 컴퓨터를 삭제합니다. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 가상 컴퓨터를 만듭니다.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | 디스크 tooa 가상 컴퓨터를 연결합니다. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | 반환 hello 가상 컴퓨터의 IP 주소입니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
