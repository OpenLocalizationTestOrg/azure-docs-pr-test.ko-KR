---
title: "CLI 스크립트 샘플-aaaAzure 부하를 분산 hello Azure CLI로 여러 웹 사이트 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-을 부하 분산 여러 웹 사이트 toohello 동일한 가상 컴퓨터"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>여러 웹 사이트 부하 분산

이 스크립트 샘플에서는 가용성 집합의 구성원인 두 개의 VM(가상 컴퓨터)과 가상 네트워크를 만듭니다. 부하 분산 장치에 대 한 두 개의 별도 트래픽을 전송 IP 주소 2 toohello Vm입니다. Hello 스크립트를 실행 한 후 웹 서버 소프트웨어 toohello Vm을 배포 하 고 각각 자체 IP 주소를 가진 여러 웹 사이트를 호스팅할 수 없습니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹에서 가상 네트워크 부하 분산 장치, 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Azure Virtual Network 및 서브넷을 만듭니다. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | 고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Azure Load Balancer를 만듭니다. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | 부하 분산 장치 프로브를 만듭니다. 부하 분산 장치 검색은 사용 되는 toomonitor hello 부하 분산 장치 집합의 각 VM입니다. 모든 VM에 액세스할 수 없게 됩니다, 트래픽 라우팅된 toohello VM 표시 되지 않습니다. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 부하 분산 장치 규칙을 만듭니다. 이 샘플에서는 포트 80에 대한 규칙을 만듭니다. HTTP 트래픽을 hello 부하 분산 장치에 도착 하면 때 라우트된 tooport 80 hello 부하 분산 장치 집합의 hello Vm 중 하나입니다. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Hello 부하 분산 장치에 대 한 프런트 엔드 IP 주소를 만듭니다. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | 백 엔드 주소 풀을 만듭니다. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | 가상 네트워크 카드를 만들고 toohello 가상 네트워크 및 서브넷에 연결 합니다. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 가용성 집합을 만듭니다. 가용성 집합으로 오류가 발생 하면 전체 집합 hello 영향을 받지 않습니다 되도록 hello 가상 컴퓨터는 실제 리소스 분배 하 여 응용 프로그램의 가동 시간을 확인 합니다. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | IP 구성을 만듭니다. Hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic 기능을 구독에 대해 사용할 수 있어야 합니다. 하나의 구성만 hello-기본 편집기로 지정 플래그를 사용 하 여 NIC 당 기본 IP 구성 hello로 지정 될 수 있습니다. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다. 이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.
