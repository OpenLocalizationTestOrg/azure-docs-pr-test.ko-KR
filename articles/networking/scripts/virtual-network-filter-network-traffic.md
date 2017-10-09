---
title: "aaaAzure CLI 스크립트 샘플 필터 VM 네트워크 트래픽 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 인바운드 및 아웃바운드 VM 네트워크 트래픽을 필터링합니다."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링

이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다. 인바운드 네트워크 트래픽을 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP, HTTPS 및 SSH, 동안 아웃 바운드 트래픽을 toohello hello 백 엔드 서브넷에서 인터넷을 사용할 수 없습니다. Hello 스크립트를 실행 한 후 두 개의 Nic 하나의 가상 컴퓨터를 해야 합니다. 각 NIC가 연결 된 tooa 다른 서브넷입니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다. Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az network vnet create](/cli/azure/network/vnet#create) | Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | 백 엔드 서브넷을 만듭니다. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | Toosubnets Nsg를 연결합니다. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다. |
| [az network nic create](/cli/azure/network/nic#create) | 가상 네트워크 인터페이스를 만들고 toohello 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결 합니다. |
| [az network nsg create](/cli/azure/network/nsg#create) | 네트워크 보안 그룹 (NSG) 관련된 toohello 프런트 엔드 및 백 엔드 서브넷을 만듭니다. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |NSG 규칙을 허용 하거나 차단할 toospecific 서브넷 특정 포트를 만듭니다. |
| [az vm create](/cli/azure/vm#create) | 가상 컴퓨터를 만들고 NIC tooeach VM을 연결 합니다. 이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다. |
| [az group delete](/cli/azure/group#delete) | 리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](/cli/azure/overview)합니다.

추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md)
