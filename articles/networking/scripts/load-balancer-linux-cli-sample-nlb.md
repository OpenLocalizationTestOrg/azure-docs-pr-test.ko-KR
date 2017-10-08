---
title: "CLI 스크립트 샘플-고가용성을 위한 부하 분산 트래픽 tooVMs aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-고가용성을 위한 부하 분산 트래픽 tooVMs"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>고가용성을 위한 분산 트래픽 tooVMs 로드

이 스크립트 예제에서는 필요한 모든 것을 만듭니다 toorun 여러 Ubuntu 가상 컴퓨터에서 항상 사용 가능한 구성 및 부하 분산 구성 합니다. Hello 스크립트를 실행 한 후 3 개의 가상 컴퓨터가 Azure 가용성 집합에 가입된 tooan 될 것 이며는 Azure 부하 분산 장치를 통해 액세스할 수 있습니다. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Azure Virtual Network 및 서브넷을 만듭니다. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | 고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Azure Load Balancer를 만듭니다. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | 부하 분산 장치 프로브를 만듭니다. 부하 분산 장치 검색은 사용 되는 toomonitor hello 부하 분산 장치 집합의 각 VM입니다. 모든 VM에 액세스할 수 없게 됩니다, 트래픽 라우팅된 toohello VM 표시 되지 않습니다. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 부하 분산 장치 규칙을 만듭니다. 이 샘플에서는 포트 80에 대한 규칙을 만듭니다. HTTP 트래픽을 hello 부하 분산 장치에 도착 하면 때 라우트된 tooport 80 hello hello LB 집합에는 Vm 중 하나입니다. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | 부하 분산 장치 NAT(네트워크 주소 변환) 규칙을 만듭니다.  NAT 규칙 hello VM에서 부하 분산 장치 tooa 포트의 포트를 매핑합니다. 이 샘플에서 NAT 규칙 hello 부하 분산 장치 집합의 SSH 트래픽 tooeach VM에 대해 생성 됩니다.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Hello 인터넷 및 hello 가상 컴퓨터 간의 보안 경계를 네트워크 보안 그룹 (NSG)을 만듭니다. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | NSG 규칙 tooallow 만듭니다 트래픽 인바운드 합니다. 이 샘플에서 SSH 트래픽에 대해 포트 22가 열립니다. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | 가상 네트워크 카드를 만들고 toohello 가상 네트워크, 서브넷 및 NSG를 연결 합니다. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 가용성 집합을 만듭니다. 가용성 집합으로 오류가 발생 하면 전체 집합 hello 영향을 받지 않습니다 되도록 hello 가상 컴퓨터는 실제 리소스 분배 하 여 응용 프로그램의 가동 시간을 확인 합니다. |
| [az vm create](/cli/azure/vm#create) | Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다. 이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 설명서](../cli-samples.md)합니다.
