---
title: "aaaWhat Azure 네트워크 액세스 제어 목록 인지 확인"
description: "Azure에서 액세스 제어 목록에 대한 자세한 정보"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>끝점 액세스 제어 목록이란?

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 Resource Manager와 클래식이라는 두 가지 [배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다. 

끝점 ACL(액세스 제어 목록)은 Azure 배포에 사용할 수 있는 보안 향상 기능입니다. ACL은 hello 기능 tooselectively 허용을 제공 하거나 가상 컴퓨터 끝점에 대 한 트래픽을 거부 합니다. 이 패킷 필터링 기능을 통해 보안을 강화할 수 있습니다. 끝점에 대해서만 네트워크 ACL을 지정할 수 있습니다. 가상 네트워크 또는 가상 네트워크에 포함된 특정 서브넷에 대해서는 ACL을 지정할 수 없습니다. Acl을 가능 하면 대신 toouse 보안 Nsg (네트워크 그룹)이 좋습니다. Nsg에 대 한 자세한 toolearn 참조 [네트워크 보안 그룹 개요](virtual-networks-nsg.md)

PowerShell 또는 hello Azure 포털을 사용 하 여 Acl은 구성할 수 있습니다. PowerShell을 사용 하 여 네트워크 ACL tooconfigure 참조 [PowerShell을 사용 하 여 끝점에 대 한 관리 액세스 제어 목록](virtual-networks-acl-powershell.md)합니다. 사용 하 여 네트워크 ACL tooconfigure hello Azure 포털에서 참조 [어떻게 tooset 끝점 tooa 가상 컴퓨터를](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

네트워크 Acl을 사용 하 여 할 수 있는 hello 다음:

* 선택적으로 허용 하거나 원격 서브넷 IPv4 주소 범위 tooa 가상 컴퓨터 입력된 끝점에 따라 들어오는 트래픽을 거부 합니다.
* IP 주소를 블랙리스트에 올립니다.
* 가상 컴퓨터 끝점별로 여러 규칙을 생성합니다.
* 규칙 집합이 지정 된 가상 컴퓨터 끝점 (가장 낮은 toohighest)에 적용 되는 올바른 tooensure hello 순서 지정 규칙 사용
* 특정 원격 서브넷 IPv4 주소에 대해 ACL을 지정합니다.

Hello 참조 [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) ACL 제한에 대 한 문서입니다.

## <a name="how-acls-work"></a>ACL의 작동 방식
ACL은 규칙 목록이 포함된 개체입니다. ACL을 만들고 tooa 가상 컴퓨터 끝점을 적용할 때 VM의 호스트 노드 hello에서 발생 하는 패킷 필터링 합니다. 즉, 원격 IP 주소 로부터 hello 트래픽은 VM에 대 한 대신 일치 하는 ACL 규칙에 대 한 hello 호스트 노드에서 필터링 됩니다. 이 VM이 패킷 필터링 시 hello 귀중 한 CPU 사이클을 소비에서 차단 합니다.

가상 컴퓨터를 만들 때에 들어오는 모든 트래픽은으로 위치 tooblock에 기본 ACL 저장 됩니다. 그러나 끝점 (포트 3389)를 만든 경우 다음 hello 기본 ACL이 수정 tooallow 해당 끝점에 대 한 모든 인바운드 트래픽입니다. 모든 원격 서브넷 으로부터 인바운드 트래픽을 toothat 끝점 허용 다음 및 없는 방화벽 프로 비전은 필요 합니다. 해당 포트에 대해 끝점을 만들지 않으면 다른 모든 포트가 인바운드 트래픽에 대해 차단됩니다. 기본적으로 아웃바운드 트래픽은 허용됩니다.

**기본 ACL 테이블의 예**

| **규칙 번호** | **원격 서브넷** | **끝점** | **허용/거부** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |허용 |

## <a name="permit-and-deny"></a>허용 및 거부
"허용" 또는 "거부"를 지정하는 규칙을 만들어 가상 컴퓨터 입력 끝점에 대한 네트워크 트래픽을 선택적으로 허용하거나 거부할 수 있습니다. 것이 중요 한 toonote 기본적으로는 끝점을 만들 때 모든 트래픽을 사용할 수 있는 toohello 끝점입니다. 이런 이유로 toounderstand toocreate 허용/거부 규칙 및 hello 네트워크를 통해 세분화 된 제어 하려는 경우 우선 순위 hello 적절 한 순서 대로 배치 하는 방법 트래픽을 하는 중요 한 것 tooallow tooreach hello 가상 컴퓨터 끝점을 선택 합니다.

포인트 tooconsider:

1. **ACL 없음 –** 기본적으로는 끝점을 만들 때 트래픽이 허용 hello 끝점에 대 한 모든 합니다.
2. **허용** - "허용" 범위를 하나 이상 추가할 경우 기본적으로 다른 모든 범위를 거부하는 것입니다. IP 범위를 허용 하는 hello 패킷만 수 toocommunicate hello 가상 컴퓨터 끝점을 사용 됩니다.
3. **거부** - "거부" 범위를 하나 이상 추가할 경우 기본적으로 다른 모든 트래픽 범위를 허용하는 것입니다.
4. **허용 및 거부-조합** "허용"의 조합을 사용할 수 있습니다 및 허용 또는 거부 toobe 범위 "거부" toocarve 특정 IP 아웃 하려는 경우.

## <a name="rules-and-rule-precedence"></a>규칙 및 규칙 우선 순위
특정 가상 컴퓨터 끝점에 대해 네트워크 ACL을 설정할 수 있습니다. 예를 들어 특정 IP 주소에 대한 액세스를 제한하는 가상 컴퓨터에서 만든 RDP 끝점에 대한 네트워크 ACL을 지정할 수 있습니다. hello 아래 표에 방식으로 toogrant 액세스 toopublic Vip (가상 Ip) RDP에 대 한 특정 범위 toopermit 액세스 합니다. 다른 모든 원격 IP는 거부됩니다. 여기서는 *가장 낮은 값이 우선하는* 규칙 순서를 따릅니다.

### <a name="multiple-rules"></a>여러 규칙
Hello 아래의 예제에서는 두 개의 공용 IPv4 주소 범위 (65.0.0.0/8, 및 159.0.0.0/8) 에서만에서 tooallow 액세스 toohello RDP 끝점을 사용 하려는 경우이 위해서는 두 개를 지정 하 여 *허용* 규칙입니다. 이 경우 가상 컴퓨터에 대해 기본적으로 RDP 만들어지므로 원격 서브넷에 따라 액세스 toohello RDP 포트 아래로 toolock을 좋습니다. hello 관리 되는 코드 방식으로 toogrant 액세스 toopublic Vip (가상 Ip) RDP에 대 한 특정 범위 toopermit 액세스 합니다. 다른 모든 원격 IP는 거부됩니다. 네트워크 ACL을 특정 가상 컴퓨터 끝점에 대해 설정할 수 있으며 기본적으로 액세스가 거부되므로 이 규칙이 작동됩니다.

**예 - 여러 규칙**

| **규칙 번호** | **원격 서브넷** | **끝점** | **허용/거부** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |허용 |
| 200 |159.0.0.0/8 |3389 |허용 |

### <a name="rule-order"></a>규칙 순서
끝점에 대해 여러 규칙을 지정할 수 있습니다, 때문에 방법을 tooorganize 규칙에에서 있어야 순서 toodetermine 규칙에 우선 합니다. hello 규칙 순서에 따라 우선 순위를 지정합니다. 네트워크 ACL은 *가장 낮은 값이 우선하는* 규칙 순서를 따릅니다. 에서는 아래 hello 예제 hello 끝점 포트 80에서 선택적으로 권한이 부여 됩니다 액세스 tooonly 특정 IP 주소 범위입니다. tooconfigure이 거부 규칙 했으므로 (규칙 \# 100) hello 175.1.0.1/24 공간에 대 한 주소에 대 한 합니다. 두 번째 규칙은 우선 순위 200 허용 액세스할 175.0.0.0/8에서 다른 주소 tooall 있는지 지정 합니다.

**예 - 규칙 우선 순위**

| **규칙 번호** | **원격 서브넷** | **끝점** | **허용/거부** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |거부 |
| 200 |175.0.0.0/8 |80 |허용 |

## <a name="network-acls-and-load-balanced-sets"></a>네트워크 ACL 및 부하 분산된 집합
부하 분산된 집합 끝점에서 네트워크 ACL을 지정할 수 있습니다. ACL은 부하 분산 집합에 대 한 지정 된 경우에 부하 분산된 집합 ACL은 가상 컴퓨터에 적용 된 tooall 네트워크를 hello 합니다. 예를 들어 부하 분산 집합은 "포트 80"으로 만들어지며 hello 부하 분산 집합 3 개의 Vm, VM가 자동으로 하나의 "포트 80" 끝점에서 ACL 만든 hello 네트워크를 포함 하는 경우 적용 toohello 다른 Vm 됩니다.

![네트워크 ACL 및 부하 분산된 집합](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>다음 단계
[PowerShell을 사용하여 끝점에 대한 액세스 제어 목록 관리](virtual-networks-acl-powershell.md)

