---
title: "패브릭 aaaService 노드 형식 및 VM 크기 집합이 | Microsoft Docs"
description: "서비스 패브릭 노드 형식 tooVM 크기 집합의 관계 및 tooremote tooa VM 크기 집합 인스턴스 또는 클러스터 노드를 연결 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>서비스 패브릭 노드 형식 및 가상 컴퓨터 크기 집합 간의 hello 관계
가상 컴퓨터 크기 집합은 toodeploy를 사용 하 고 집합으로 가상 컴퓨터의 컬렉션을 관리할 수는 Azure 계산 리소스입니다. 서비스 패브릭 클러스터에 정의된 모든 노드 유형은 별도의 VM 확장 집합으로 설치됩니다. 각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.

다음 스크린 샷에서 hello 클러스터에는 두 노드 종류를 보여 줍니다: 프런트 엔드 및 백 엔드 합니다.  각 노드 형식에는 5개의 노드가 있습니다.

![두 가지 노드 유형이 있는 클러스터의 스크린 샷][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>VM 크기 집합 인스턴스 toonodes 매핑
위에서 볼 수 있듯이 hello VM 크기 집합 인스턴스는 인스턴스 0에서에서 시작 하 고 높아집니다. hello 번호 매기기 hello 이름에 반영 됩니다. 예를 들어, BackEnd_0 hello 백 엔드 VM 크기 집합의 인스턴스 0입니다. 이 특정 VM 크기 조정 설정에는 BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 및 BackEnd_4라는 5개의 인스턴스가 있습니다.

VM 크기 조정 설정을 확대하는 경우 새 인스턴스가 생성됩니다. hello VM 크기 집합 이름 + 인스턴스 번호를 다음 hello hello 새 VM 크기 집합 인스턴스 이름은 일반적으로 것입니다. 이 예제에서는 BackEnd_5입니다.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>매핑 VM 크기 집합 부하 분산 장치 tooeach 노드 유형/VM 크기 집합
म 때 제공 되는, 다음의 리소스 그룹 아래의 모든 리소스 목록을 가져올 hello 샘플 리소스 관리자 템플릿을 사용 hello 포털에서 클러스터를 배포 하는 경우 각 VM 크기 집합 또는 노드 형식에 대 한 hello 부하 분산 장치 표시 됩니다.

hello 이름은 다음과 같이: **LB-&lt;NodeType 이름&gt;**합니다. 예를 들어 이 스크린 샷에 표시된 대로 LB-sfcluster4doc-0입니다.

![리소스][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>원격 연결 tooa VM 크기 집합 인스턴스 또는 클러스터 노드
클러스터에 정의된 모든 노드 유형은 별도의 VM 확장 집합으로 설치됩니다.  의미 hello 노드 유형에 확장할 수 있습니다 또는 독립적으로 아래쪽 및 다른 VM Sku 구성 될 수 있습니다. 단일 인스턴스 Vm 달리 hello VM 크기 집합 인스턴스는 자체의 가상 IP 주소를 얻지 못합니다. 비트 될 수 있도록 IP에 대 한 원하는 어려운 주소와 포트 tooremote를 사용할 수 있는 연결 tooa 특정 인스턴스.

다음은 hello 단계 toodiscover 따를 수 있습니다 이러한.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>1 단계: hello hello 노드 형식에 대 한 가상 IP 주소 및 RDP에 대 한 인바운드 NAT 규칙 확인
순서 tooget 해야 하는, tooget hello 인바운드 NAT 규칙에 대 한 hello 리소스 정의의 일부로 정의 된 값을 **Microsoft.Network/loadBalancers**합니다.

Hello 포털에서 toohello 부하 분산 장치 블레이드를 탐색 한 다음 **설정을**합니다.

![LBBlade][LBBlade]

**설정**에서 **인바운드 NAT 규칙**을 클릭합니다. 이 구문은 이제 IP 주소와 포트 tooremote를 사용할 수 있는 hello 제공 toohello 첫 번째 VM 크기 집합 인스턴스를 연결 합니다. 아래 hello 스크린샷에서 편이 **104.42.106.156** 및 **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>2 단계: tooremote를 사용할 수 있는 hello 포트에 대해 알아봅니다 연결 toohello 특정 VM 크기 집합 인스턴스/노드
이 문서의 앞부분에서 hello VM 크기 집합 인스턴스 toohello 노드 매핑 하는 방법에 대 한 설명이 있습니다. 해당 toofigure 끝 hello 정확한 포트를 사용 합니다.

hello VM 크기 집합 인스턴스의 오름차순 hello 포트가 할당 됩니다. 따라서 hello 프런트 엔드 노드 형식에 대 한 예제에서 hello 5 개의 인스턴스 각각에 대 한 hello 포트는 다음 hello를 사용 합니다. 하면 toodo 필요한 VM 크기 집합 인스턴스에 대 한 동일한 매핑을 hello 이제 합니다.

| **VM 확장 집합 인스턴스** | **포트** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>3 단계: 원격 연결 toohello 특정 VM 크기 집합 인스턴스
아래의 스크린 샷은 hello tooconnect toohello FrontEnd_1 원격 데스크톱 연결을 사용 했습니다.

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>어떻게 toochange hello RDP 포트 범위 값은
### <a name="before-cluster-deployment"></a>클러스터 배포 전에
리소스 관리자 템플릿을 사용 하 여 hello 클러스터를 설정 하는 경우 hello에 hello 범위를 지정할 수 있습니다 **inboundNatPools**합니다.

Toohello 리소스 정의 대 한 이동 **Microsoft.Network/loadBalancers**합니다. 에 대 한 hello 설명 하는 아래 **inboundNatPools**합니다.  Hello 대체 *가 frontendPortRangeStart* 및 *frontendPortRangeEnd* 값입니다.

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>클러스터 배포 후에
이 좀 더 참여 하 고 재생 되지 hello Vm에서 발생할 수 있습니다. 지금 Azure PowerShell을 사용 하 여 tooset 새 값을 갖게 됩니다. 컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다. 이전 수행 하지 않은 경우 것이 좋다는에 설명 된 hello 단계를 수행한 [어떻게 tooinstall Azure PowerShell 및 구성 합니다.](/powershell/azure/overview)

Azure 계정 tooyour에 로그인 합니다. Powershell이 어떤 이유로 인해 실패하면 Azure PowerShell이 올바르게 설치되었는지 확인해야 합니다.

```
Login-AzureRmAccount
```

Hello tooget 부하 분산 장치에 대 한 내용은 다음을 실행 하 고 hello 값에 대 한 hello 설명에 대 한 참조 **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

이제 설정 *frontendPortRangeEnd* 및 *가 frontendPortRangeStart* 원하는 toohello 값입니다.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>다음 단계
* [Hello "배포 아무 곳 이나" 기능 및 Azure에서 관리 하는 클러스터와 비교의 개요](service-fabric-deploy-anywhere.md)
* [클러스터 보안](service-fabric-cluster-security.md)
* [ 서비스 패브릭 SDK 및 시작](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
